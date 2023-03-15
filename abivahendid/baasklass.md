---
description: PHP baasklass VAU API kasutamiseks
---

# Baasklass

{% hint style="info" %}
Pane tähele, kuidas juurdepääsukoodi ja selle kehtivusaega hoitakse sessioonis. Uus kood päritakse automaatselt ainult siis, kui koodi sessioonis ei ole või see on aegunud. Ja alati, kui uus kood päritakse, salvestatakse see jälle sessiooni.
{% endhint %}

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
