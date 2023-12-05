---
description: Päringu dokumentatsioon
---

# Hindade sirvimine

## <mark style="color:green;">GET</mark> ra/price/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/price/list?token={{accessToken}}&unit_id={{unitId}}&order_type={{orderType}}&service_id={{serviceId}}&service_et={{searchString}}&service_en={{searchString}}&price={{price}}&erply_code={{erplyCode}}&inside={{inside}}
```
{% endcode %}

Väljastab hinnakirja otsiparameetrite alusel, mida võib, aga ei pea kasutama. Hinnad on järjestatud kasvavalt (ASC) arhiiviüksuse ID (unit.id), teenusegrupi järjekorranumbri (service.position) ja teenuse järjekorranumbri (position) järgi, millest kaks viimast on määranud VAU haldurid.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="197">NIMI</th><th width="152">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>unit_id</td><td>Integer</td><td>Arhiiviüksuse identifikaator<br><br><em>Identifikaatori saamise kohta vaata</em> <a href="../arhiiviueksus/ueksuse-vaatamine.md#paeringu-naeide-curl"><em>siit</em></a></td><td></td></tr><tr><td>order_type</td><td>Integer </td><td>Kood, mis viitab tellimuse tüübile, millega hind seostub<br><br>Tellimuse tüübikoodid on järgmised: <br>1 - Laenutus <br>2 - Siselaenutus <br>3 - Kauglaenutus <br>4 - Deponeerimine <br>5 - Koopia <br>6 - Virtuaalne tellimus<br><br>NB! Hetkel on tasulised tellimused ainult koopia ja kauglaenutus. See võib muutuda.</td><td></td></tr><tr><td>service_id</td><td>Integer</td><td>Teenuste grupi identifikaator<br><br>Identifikaatori saamise kohta vaata <a href="../teenus/teenuste-sirvimine.md#paeringu-naeide-curl">siit</a></td><td></td></tr><tr><td>service_et</td><td>String </td><td>Teenuse nimetus eesti keeles <br>(lubatud metamärgid)</td><td></td></tr><tr><td>service_en</td><td>String</td><td>Teenuse nimetus inglise keeles <br>(lubatud metamärgid)</td><td></td></tr><tr><td>price</td><td>Number</td><td>Teenuse hind</td><td></td></tr><tr><td>erply_code</td><td>String</td><td>Teenuse kood ERPLY raamatupidamisesüsteemis</td><td></td></tr><tr><td>inside</td><td>Boolean</td><td>Kas teenus on kasutamiseks ainult arhiivisiseselt? Kui jah (true), siis seda ei näidata kliendile, kes tellimust koostab, vaid ainult arhiivitöötajale, kes tellimust haldab </td><td></td></tr></tbody></table>

{% hint style="info" %}
Otsingu metamärgid: \* - tähistab mistahes hulka märke; ? - tähistab ühte märki. Näiteks: otsing "eri\*" leiab "Eri", "Erik", "Erika"; otsing "eri?" leiab eelmainitutest ainult "Erik".
{% endhint %}

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/price/list?token=3d1140862f01aa039322ca47c60a15a8&unit_id=1&order_type=5&service_id=3
&inside=false' \
```
{% endcode %}

### Vastuse näide

Hinnakirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "priceListView": [
        {
            "id": 389,
            "archive_unit": "Rahvusarhiiv Tartus",
            "order_type": "Koopia",
            "service_name": "Digikoopia",
            "service_et": "kuni A2 formaadis tarbekoopia (tekstidokumentidest jms), kaader",
            "service_en": "Research copy, image",
            "erply_code": "0121",
            "price": 0.4,
            "measure_unit": "tk",
            "inside": false,
            "position": 1
        },
        {
            "id": 380,
            "archive_unit": "Rahvusarhiiv Tartus",
            "order_type": "Koopia",
            "service_name": "Digikoopia",
            "service_et": "kuni A3 formaadis, trükikvaliteediga (fotodest, kaartidest jms), kaader/foto",
            "service_en": "<A3 with print quality, image",
            "erply_code": "0122",
            "price": 2.5,
            "measure_unit": "tk",
            "inside": false,
            "position": 2
        },
        {
            "id": 317,
            "archive_unit": "Rahvusarhiiv Tartus",
            "order_type": "Koopia",
            "service_name": "Digikoopia",
            "service_et": "A2 kuni A0 formaadist, trükikvaliteediga (fotodest, kaartidest jms), kaader",
            "service_en": "<A0 with print quality (of maps, photographs etc.), image",
            "erply_code": "0123",
            "price": 10,
            "measure_unit": "tk",
            "inside": false,
            "position": 3
        }
    ]
}
```

Mitte ühtegi hinda ei leitud.

```json
{
    "responseStatus": "ok",
    "priceListView": []
}
```
