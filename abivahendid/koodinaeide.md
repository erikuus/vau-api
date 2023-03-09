---
description: PHP baasklass ja selle kasutusnäide
---

# Koodinäide

## Baasklass

Ehkki see baasklass on kirjutatud PHP programmeerimiskeeles, demonstreerib see üldprintsiipi, kuidas on mõistlik API poole pöörduda. Pane tähele, kuidas juurdepääsukoodi ja selle kehtivusaega hoitakse sessioonis. Uus kood päritakse automaatselt ainult siis, kui koodi sessioonis ei ole või see on aegunud. Ja alati, kui uus kood päritakse, salvestatakse see jälle sessiooni.&#x20;

```php
<?php
/**
 * Baasklass Rahvusarhiivi API kasutamiseks
 *
 * @author Erik Uus <erik.uus@gmail.com>
 * @version 1.0
 */

namespace rahvusarhiiv;

class Api
{
    const PHP_SESSION_NOT_STARTED = 1001;
    const CURL_ERROR = 1002;
    const UNEXPECTED_RESPONSE = 1003;

    /**
     * @var string $baseUrl Rahvusarhiivi API juuraadress
     */
    public $baseUrl;
    /**
     * @var string $username Rahvusarhiivis registreeritud kasutajanimi
     */
    public $username;
    /**
     * @var string $password Rahvusarhiivis registreeritud salasõna
     */
    public $password;

    /**
     * Teeb API päringu ja tagastab selle vastuse.
     * @param string $method - päringu meetod [GET|POST|PUT|DELETE]
     * @param string $request - päringu tee, näiteks '/ska/application/view'
     * @param array $params - päringu URL parameetrid (token lisatakse automaatselt)
     * @param mixed $body - päringu keha (string, kui raw; array, kui form-data)
     * @param string $boolean - kas päringu keha on JSON string
     * @return array - päringu vastus
     */
    public function sendRequest($method, $request, $params = [], $body = null, $json = false)
    {
        $curl = curl_init();

        $opts = [
            CURLOPT_URL => $this->getUrl($request, $params),
            CURLOPT_RETURNTRANSFER => true,
            CURLOPT_ENCODING => '',
            CURLOPT_MAXREDIRS => 10,
            CURLOPT_TIMEOUT => 0,
            CURLOPT_FOLLOWLOCATION => true,
            CURLOPT_SSL_VERIFYHOST => false,
            CURLOPT_SSL_VERIFYPEER => false,
            CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
            CURLOPT_CUSTOMREQUEST => $method
        ];

        if ($body) {
            $opts[CURLOPT_POSTFIELDS] = $body;
        }

        if ($json) {
            $opts[CURLOPT_HTTPHEADER] = [
                'Content-Type: application/json'
            ];
        }

        curl_setopt_array($curl, $opts);

        $jsonResponse = curl_exec($curl);
        $curlError = curl_error($curl);
        curl_close($curl);

        if ($curlError) {
            throw new \Exception('CURL error: ' . $curlError, self::CURL_ERROR);
        }

        $response = json_decode($jsonResponse, true);
        if (isset($response['responseStatus'])) {
            if ($response['responseStatus'] == 'ok') {
                return $response;
            } else {
                throw new \Exception($response['errorMessage'], $response['errorCode']);
            }
        } else {
            throw new \Exception('Unexpected response', self::UNEXPECTED_RESPONSE);
        }
    }

    /**
     * Moodustab päringu täieliku aadressi, lisades päringu tee ette juuraadressi
     * ja parameetritesse juurdepääsukoodi. Erandina ei lisata juurdepääsukoodi
     * päringule, mis ise väljastab juurdepääsukoodi.
     * @param string $request - päringu tee, näiteks '/ska/application/view'
     * @param array $params - päringu parameetrid, näiteks ['id' => 12094]
     * @return string - päringu täielik aadress
     */
    public function getUrl($request, $params)
    {
        if ($request == '/user/verify') {
            return $this->baseUrl . $request;
        } else {
            $params['token'] = $this->getAccessToken();
            return $this->baseUrl . $request . '?' . http_build_query($params);
        }
    }

    /**
     * Tagastab API juurdepääsukoodi. Kõigepealt vaadatakse sessiooni. Kui sessioonis
     * on kood olemas ja see ei ole veel aegunud, tagastatakse kood sessioonist. Kui
     * koodi sessioonis ei ole või see on aegunud, päritakse API kaudu uus kood,
     * salvestatakse see sessiooni ja tagastatakse.
     * @return string - juurdepääsukood
     */
    protected function getAccessToken()
    {
        if (!isset($_SESSION)) {
            throw new \Exception('PHP session not started', self::PHP_SESSION_NOT_STARTED);
        }

        if (!$this->isValidAccessTokenInSession()) {
            $response = $this->requestNewAccessToken();
            $this->saveAccessTokenToSession($response);
            return $response['accessToken'];
        } else {
            return $_SESSION['ApiAccessToken'][$this->username];
        }
    }

    /**
     * Kontrollib, kas sessioonis on juurdepääsukood, mis ei ole aegunud.
     * @return boolean - true, kui vastav kood on olemas
     */
    protected function isValidAccessTokenInSession()
    {
        return
            isset($_SESSION['ApiAccessToken'][$this->username]) &&
            isset($_SESSION['ApiAccessTokenExpires'][$this->username]) &&
            $_SESSION['ApiAccessTokenExpires'][$this->username] > time() ? true : false;
    }

    /**
     * Pärib API kaudu uue juurdepääsukoodi.
     * @return array - päringu vastus
     */
    protected function requestNewAccessToken()
    {
        return $this->sendRequest('POST', '/user/verify', [], [
            'username' => $this->username,
            'password' => $this->password
        ]);
    }

    /**
     * Salvestab juurdepääsukoodi ja selle aegumise aja sessiooni. Et vältida olukorda,
     * kus kood aegub pärast selle sessioonist lugemist ja enne selle päringus 
     * kasutamist, vähendatakse koodi kehtivusaega sessioonis 10 sekundi võrra.
     * @param array - juurdepääsukoodi päringu vastus
     */
    protected function saveAccessTokenToSession($response)
    {
        $_SESSION['ApiAccessToken'][$this->username] = $response['accessToken'];
        $_SESSION['ApiAccessTokenExpires'][$this->username] = $response['requestUnixTime'] + $response['tokenLifetime'] - 10;
    }
}

```

## SKA mooduli kasutusnäide

Kasutades baasklassi, loome uue üksuse, vaatame selle andmeid, muudame neid, vaatame muudetud andmeid, pärime üksuse ID, kustutame üksuse ja vaatame kõiki üksusi, mis jäid alles pärast uue üksuse kustutamist.

```php
<?php
require_once dirname(__FILE__) . '/api.php';
use rahvusarhiiv\Api;

try {
    session_start();

    $api = new Api();
    $api->baseUrl = 'https://www.ra.ee/vautest/index.php/api';
    $api->username = 'erik';
    $api->password = '******';

    // loome uue üksuse
    $body = '{
        "name": "Test osakond",
        "address": "Tammsaare 8-25, Tartu",
        "zip": "51006",
        "email": "erik.uus@ra.ee",
        "phone": "+372 5322 5388"
    }';
    $response = $api->sendRequest('POST', '/ska/department/create', [], $body, true);
    $departmentId = $response['departmentId'];

    // vaatame uut üksust
    echo '<h1>Uus üksus</h1>';
    $response = $api->sendRequest('GET', '/ska/department/view', ['id' => $departmentId]);
    foreach ($response['departmentDetailView'] as $key => $value) {
        echo $key . ': ' . $value . '<br />';
    }

    // muudame üksust
    $body = '{
        "name": "Test osakond_",
        "address": "Tammsaare 8-25, Tartu_",
        "zip": "51006_",
        "email": "erik.uus@gmail.com",
        "phone": "+372 5322 5388_"
    }';
    $api->sendRequest('PUT', '/ska/department/update', ['id' => $departmentId], $body, true);

    // vaatame muudetud üksust
    echo '<h1>Muudetud üksus</h1>';
    $response = $api->sendRequest('GET', '/ska/department/view', ['id' => $departmentId]);
    foreach ($response['departmentDetailView'] as $key => $value) {
        echo $key . ': ' . $value . '<br />';
    }

    // leiame üksuse ID selle nime järgi
    echo '<h1>Üksuse ID on</h1>';
    $response = $api->sendRequest('POST', '/ska/department/find', ['name'=>'Test osakond_'], $body, true);
    echo $response['departmentId'];

    // kustutame üksuse
    $response = $api->sendRequest('DELETE', '/ska/department/delete', ['id' => $departmentId]);

    // vaatame kõik üksusi, mis jäid alles pärast kustutamist 
    echo '<h1>Kõik üksused pärast kustutamist</h1>';
    $response = $api->sendRequest('GET', '/ska/department/list');
    foreach ($response['departmentListView'] as $department) {
        echo '<p>';
        foreach ($department as $key => $value) {
            echo $key . ': ' . $value . '<br />';
        }
        echo '</p>';
    }
} catch (\Exception $e) {
    echo $e->getCode() . ': ' . $e->getMessage();
}

```

{% hint style="info" %}
Pane tähele, et selle näite puhul baasklass pärib juurdepääsukoodi ainult üksuse loomisel. Kõigi järgnevate päringute puhul võetakse see juba sessioonist.&#x20;
{% endhint %}

Ülaltoodud skript väljastab järgmise lehekülje:

#### <mark style="color:blue;">Uus üksus</mark>

<mark style="color:blue;">Nimi: Test osakond</mark>\ <mark style="color:blue;">Aadress: Tammsaare 8-25, Tartu</mark>\ <mark style="color:blue;">Postiindeks: 51006</mark>\ <mark style="color:blue;">E-post: erik.uus@ra.ee</mark>\ <mark style="color:blue;">Telefon: +372 5322 5388</mark>

#### <mark style="color:blue;">Muudetud üksus</mark>

<mark style="color:blue;">Nimi: Test osakond\_</mark>\ <mark style="color:blue;">Aadress: Tammsaare 8-25, Tartu\_</mark>\ <mark style="color:blue;">Postiindeks: 51006\_</mark>\ <mark style="color:blue;">E-post: erik.uus@gmail.com</mark>\ <mark style="color:blue;">Telefon: +372 5322 5388\_</mark>

#### <mark style="color:blue;">Üksuse ID on</mark>

<mark style="color:blue;">40</mark>

#### <mark style="color:blue;">Kõik üksused pärast kustutamist</mark>

<mark style="color:blue;">id: 16</mark>\ <mark style="color:blue;">Nimi: SKA Info- ja dokumendihalduse osakond</mark>\ <mark style="color:blue;">Aadress: Endla 8, Tallinn</mark>\ <mark style="color:blue;">Postiindeks: 15092</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 6408141</mark>

<mark style="color:blue;">id: 18</mark>\ <mark style="color:blue;">Nimi: SKA Klienditeeninduse osakond</mark>\ <mark style="color:blue;">Aadress: Endla 8, Tallinn</mark>\ <mark style="color:blue;">Postiindeks: 15092</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 6408141</mark>

<mark style="color:blue;">id: 19</mark>\ <mark style="color:blue;">Nimi: SKA Ohvriabi osakond</mark>\ <mark style="color:blue;">Aadress: Endla 8, Tallinn</mark>\ <mark style="color:blue;">Postiindeks: 15092</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 640 8141</mark>

<mark style="color:blue;">id: 17</mark>\ <mark style="color:blue;">Nimi: SKA Pensionitalitus</mark>\ <mark style="color:blue;">Aadress: Endla 8, Tallinn</mark>\ <mark style="color:blue;">Postiindeks: 15092</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 6408141</mark>

<mark style="color:blue;">id: 21</mark>\ <mark style="color:blue;">Nimi: SKA Pensionitalitus Pärnus</mark>\ <mark style="color:blue;">Aadress: Lai 14, Pärnu</mark>\ <mark style="color:blue;">Postiindeks: 80010</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 4477606</mark>

<mark style="color:blue;">id: 24</mark>\ <mark style="color:blue;">Nimi: SKA Pensionitalitus Tallinnas</mark>\ <mark style="color:blue;">Aadress: Endla 8, Tallinn</mark>\ <mark style="color:blue;">Postiindeks: 15092</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 664 0104</mark>

<mark style="color:blue;">id: 23</mark>\ <mark style="color:blue;">Nimi: SKA Pensionitalitus Tartus</mark>\ <mark style="color:blue;">Aadress: Põllu 1A, Tartu</mark>\ <mark style="color:blue;">Postiindeks: 50303</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 744 7905</mark>

<mark style="color:blue;">id: 22</mark>\ <mark style="color:blue;">Nimi: SKA Pensionitalitus Viljandis</mark>\ <mark style="color:blue;">Aadress: Vabaduse plats 6, Viljandi</mark>\ <mark style="color:blue;">Postiindeks: 71020</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 435 0580</mark>

<mark style="color:blue;">id: 20</mark>\ <mark style="color:blue;">Nimi: SKA Välishüvitiste üksus</mark>\ <mark style="color:blue;">Aadress: Endla 8, Tallinn</mark>\ <mark style="color:blue;">Postiindeks: 15092</mark>\ <mark style="color:blue;">E-post: info@sotsiaalkindlustusamet.ee</mark>\ <mark style="color:blue;">Telefon: 640 8118</mark>
