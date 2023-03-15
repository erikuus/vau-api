---
description: >-
  Kasutades baasklassi, loome uue üksuse, vaatame selle andmeid, muudame neid,
  vaatame muudetud andmeid, pärime üksuse ID, kustutame üksuse ja vaatame kõiki
  üksusi, mis jäid alles pärast uue üksuse kust
---

# SKA mooduli kasutusnäide

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
Pane tähele, et selle näite puhul baasklass pärib juurdepääsukoodi ainult üksuse loomisel. Kõigi järgnevate päringute puhul võetakse see juba sessioonist.
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

