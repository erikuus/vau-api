---
description: >-
  Kasutades baasklassi, leiame ühe arhiiviüksuse avalikud tasulised digikoopia
  teenused: nimetused, koodid, hinnad.
---

# RA mooduli kasutusnäide

```php
<?php
require_once dirname(__FILE__) . '/api.php';
use rahvusarhiiv\Api;

try {
    session_start();

    $api = new Api();
    $api->baseUrl = 'https://www.ra.ee/vau/index.php/api';
    $api->username = 'erik';
    $api->password = '******';

    // leia Tartu arhiiviüksuse ID
    $response = $api->sendRequest('GET', '/ra/unit/view', [
        'code' => 'Tartu'
    ]);
    if (isset($response['unitDetailView'])) {
        $unitId = $response['unitDetailView']['id'];
        // päri selle üksuse avalikud tasulised digikoopia teenused
        $response = $api->sendRequest('GET', '/ra/price/list', [
            'unit_id' => $unitId,
            'service_id' => 3,
            'inside' => false
        ]);
        foreach ($response['priceListView'] as $price) {
            echo '<p>';
            foreach ($price as $key => $value) {
                echo $key . ': ' . htmlentities($value) . '<br />';
            }
            echo '</p>';
        }
    } else {
        echo 'Ei leidnud üksuse koodi.';
    }
} catch (\Exception $e) {
    echo $e->getCode() . ': ' . $e->getMessage();
}
```

{% hint style="info" %}
Pane tähele, et selle näite puhul baasklass pärib juurdepääsukoodi ainult üksuse ID leidmisel. Hinnakirja päringu puhul võetakse see juba sessioonist.
{% endhint %}

Ülaltoodud skript väljastab järgmise lehekülje:

<mark style="color:blue;">id: 389</mark>\ <mark style="color:blue;">archive\_unit: Rahvusarhiiv Tartus</mark>\ <mark style="color:blue;">order\_type: Koopia</mark>\ <mark style="color:blue;">service\_name: Digikoopia</mark>\ <mark style="color:blue;">service\_et: kuni A2 formaadis tarbekoopia (tekstidokumentidest jms), kaader</mark>\ <mark style="color:blue;">service\_en: Research copy, image</mark>\ <mark style="color:blue;">erply\_code: 0121</mark>\ <mark style="color:blue;">price: 0.4</mark>\ <mark style="color:blue;">measure\_unit: tk</mark>\ <mark style="color:blue;">inside:</mark>\ <mark style="color:blue;">position: 1</mark>\


<mark style="color:blue;">id: 380</mark>\ <mark style="color:blue;">archive\_unit: Rahvusarhiiv Tartus</mark>\ <mark style="color:blue;">order\_type: Koopia</mark>\ <mark style="color:blue;">service\_name: Digikoopia</mark>\ <mark style="color:blue;">service\_et: kuni A3 formaadis, trükikvaliteediga (fotodest, kaartidest jms), kaader/foto</mark>\ <mark style="color:blue;">service\_en: \<A3 with print quality, image</mark>\ <mark style="color:blue;">erply\_code: 0122</mark>\ <mark style="color:blue;">price: 2.5</mark>\ <mark style="color:blue;">measure\_unit: tk</mark>\ <mark style="color:blue;">inside:</mark>\ <mark style="color:blue;">position: 2</mark>\ <mark style="color:blue;"></mark>

<mark style="color:blue;">id: 317</mark>\ <mark style="color:blue;">archive\_unit: Rahvusarhiiv Tartus</mark>\ <mark style="color:blue;">order\_type: Koopia</mark>\ <mark style="color:blue;">service\_name: Digikoopia</mark>\ <mark style="color:blue;">service\_et: A2 kuni A0 formaadist, trükikvaliteediga (fotodest, kaartidest jms), kaader</mark>\ <mark style="color:blue;">service\_en: \<A0 with print quality (of maps, photographs etc.), image</mark>\ <mark style="color:blue;">erply\_code: 0123</mark>\ <mark style="color:blue;">price: 10</mark>\ <mark style="color:blue;">measure\_unit: tk</mark>\ <mark style="color:blue;">inside:</mark>\ <mark style="color:blue;">position: 3</mark>
