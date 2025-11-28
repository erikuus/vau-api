---
description: Päringu dokumentatsioon
---

# Tellimuse loomine

## <mark style="color:orange;">POST</mark> ra/meediateekOrder/create

```
{{apiBaseUrl}}/ra/meediateekOrder/create?token={{accessToken}}
```

Loob uue Meediateegi tellimuse ja tagastab selle identifikaatori.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="248">NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

JSON peab sisaldama tellimuse objekti `MeediateekOrder`:

```json
{
  "MeediateekOrder": { /* … */ }
}
```

Teenuseread tuleb lisada `MeediateekOrderRow` kaudu:

```json
{
  "MeediateekOrder": { /* … */ },
  "MeediateekOrderRow": [
    { /* … */ },
    { /* … */ }
  ]
}
```

**MeediateekOrder**

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="287.6171875">NIMI</th><th width="131.32421875">TÜÜP (PIKKUS)</th><th>SELGITUS</th></tr></thead><tbody><tr><td>client_vau_id *</td><td>Integer</td><td>Tellija VAU kasutajakonto identifikaator</td></tr><tr><td>client_comment</td><td>Text</td><td>Tellija märkused tellimuse kohta</td></tr><tr><td>billing_type_code *</td><td>Integer</td><td><p>Maksmise viis<br></p><p>Lubatud väärtused on:</p><p><code>2</code> - Arvega tasumine<br><code>3</code> - Veebimakse<br><code>4</code> - Koostööleping või garantiikiri<br><br>Kohustuslik väli, mis määrab, millised muud väljad on nõutavad või lubatud (vaata <a href="tellimuse-loomine.md#valideerimisreeglid">Valideerimisreeglid</a>)</p></td></tr><tr><td>invoice_type_code</td><td>Integer</td><td><p>Arve tüüp<br></p><p>Lubatud väärtused on:</p><p><code>2</code> - Arve asutusele<br><code>3</code> - Arve eraisikule e-postiga<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine). </p></td></tr><tr><td>client_company_id</td><td>Integer</td><td><p>Koostöölepingu või garantiikirjaga asutus<br><br>Kohustuslik, kui <code>billing_type_code=4</code> (koostöölepingu või garantiikirjaga asutusega arveldamine). Keelatud kõigil muudel juhtudel.</p><p><br>Asutuse andmeid saab pärida kasutades API endpoint'e <a href="../asutus/kasutaja-asutuste-sirvimine.md">Kasutaja asutuste sirvimine</a> ja <a href="../asutus/asutuse-vaatamine.md">Asutuse vaatamine</a></p></td></tr><tr><td>invoice_private_email</td><td>String (256)</td><td>Eraisiku e-posti aadress, kuhu saadetakse arve<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=3</code> (arve eraisikule e-postiga). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company</td><td>String (256)</td><td>Arve saaja asutuse nimi<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_nr</td><td>String (32)</td><td>Arve saaja asutuse registrikood<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele) ja <code>invoice_company_country_id=1</code> (Eesti). Keelatud kõigil muudel juhtudel<br><br>Kasutajaliideses on soovitav kasutada <em>autocomplete</em> välja, mis pakub valikuid äriregistri teenuse kaudu ja täidab automaatselt registrikoodi ja aadressi väljad. Teenuse aadress on: <a href="https://ariregister.rik.ee/est/api/autocomplete">https://ariregister.rik.ee/est/api/autocomplete</a></td></tr><tr><td>invoice_company_type</td><td>Integer</td><td><p>Arve saaja välisriigi asutuse tüüp<br></p><p>Lubatud väärtused on:</p><p><code>1</code> - Valitsusasutus (Government Agency)<br><code>2</code> - Kohalik omavalitsus (Local Government Agency)<br><code>3</code> - Rahvusvaheline organisatsioon (International Organisation) <br><code>4</code> - Krediidi- või finantseerimisasutus (Credit or Financial Institution)<br><code>5</code> - Muu (Other)<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele) ja <code>invoice_company_country_id≠1</code> (välisriik). Keelatud kõigil muudel juhtudel</p></td></tr><tr><td>invoice_company_email</td><td>String (256)</td><td>Arve saaja asutuse e-post<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_street</td><td>String (256)</td><td>Arve saaja asutuse aadress: tänav/maja<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_city</td><td>String (256)</td><td>Arve saaja asutuse aadress: linn/vald<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_county</td><td>String (256)</td><td>Arve saaja asutuse aadress: maakond<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_zip</td><td>String (16)</td><td>Arve saaja asutuse aadress: postiindeks<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_country_id</td><td>Integer</td><td>Arve saaja asutuse riik<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (arvega tasumine) ja <code>invoice_type_code=2</code> (arve asutusele). Keelatud kõigil muudel juhtudel<br><br>Riikide andmeid saab pärida kasutades API endpoint'i <a href="../riik/riikide-sirvimine.md">Riikide sirvimine</a></td></tr><tr><td>order_type *</td><td>Integer</td><td><p>Tellimuse liik</p><p></p><p>Meediateegi tellimuse puhul lubatud</p><p><code>5</code> - Koopia</p></td></tr><tr><td>order_purpose_code *</td><td>Integer</td><td><p>Kasutuseesmärk</p><p></p><p>Lubatud väärtused on:</p><p><code>1</code> - Teadustöö</p><p><code>2</code> - Kodu-uurimine</p><p><code>3</code> - Genealoogia</p><p><code>4</code> - Õppetöö</p><p><code>5</code> - Õiguste tõestamine</p><p><code>6</code> - Muu</p><p><code>7</code> - Genealoogia/kodu-uurimine</p><p><code>8</code> - Teadustöö/kodu-uurimine</p><p><code>10</code> - Isiklikuks kasutuseks</p><p><code>11</code> - Publikatsioon</p><p><code>12</code> - Ajakirjandus</p><p><code>13</code> - Avalik üritus (tasuta)</p><p><code>14</code> - Avalik üritus (tasuline)</p><p><code>15</code> - Telefilm/telesaade</p><p><code>16</code> - Film</p><p><code>17</code> - Veeb</p><p><code>18</code> - Reklaam</p><p><br>Klassifikaatori andmeid saab pärida kasutades API endpoint'i <a href="../klassifikaatorid/klassifikaatorite-sirvimine.md">Klassifikaatorite sirvimine</a> (<code>type=purpose_meediateek</code>)</p></td></tr><tr><td>order_purpose_comment</td><td>Text</td><td>Kasutuse täpsustus<br><br>Kohustuslik, kui <code>order_purpose_code</code> on üks järgnevatest: <code>1</code>, <code>4</code>, <code>6</code>, <code>11</code>, <code>12</code>, <code>13</code>, <code>14</code>, <code>15</code>, <code>16</code>, <code>17</code>, <code>18</code>. Keelatud kõigil muudel juhtudel</td></tr></tbody></table>

#### MeediateekOrderRow

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="211.86328125">NIMI</th><th width="154.77734375">TÜÜP</th><th>SELGITUS</th></tr></thead><tbody><tr><td>erply_product_code *</td><td>String (256)</td><td>Tootekood ERPLY majandustarkvaras</td></tr><tr><td>refcode *</td><td>String (256)</td><td>Kirjeldusüksuse leidandmed<br><br>Need peavad olema AIS-is kirjeldatud arhivaali leidandmed. Vaata näiteks seda kirjeldust <a href="https://www.meediateek.ee/photo/view?id=1136982">https://www.meediateek.ee/photo/view?id=1136982</a> Kirjeldusüksuse leidandmed on ERA.5925.1.257 (mitte <del>ERA.5925.1.257.1.25</del>)</td></tr><tr><td>amount *</td><td>Integer</td><td>Kogus (tk, sekund, tund)</td></tr><tr><td>online_copy_title</td><td>String (256)</td><td>Veebikoopia pealkiri video/heli puhul</td></tr><tr><td>online_copy_filename</td><td>String (256)</td><td>Veebikoopia failinimi video/heli puhul</td></tr><tr><td>time_from</td><td>String (16)</td><td>Ajakood, lõigu algus</td></tr><tr><td>time_to</td><td>String (16)</td><td>Ajakood, lõigu lõpp</td></tr></tbody></table>

### Valideerimisreeglid

API valideerib tellimuse andmeid rangelt, mis tagab andmete kooskõla ja takistab vastuoluliste väljadega tellimuste loomist.

#### Lubatud kombinatsioonid

Tellimuse maksmise ja arveldamise väljad peavad vastama ühele järgnevatest viiest kombinatsioonist:

<table><thead><tr><th width="160.31640625">billing_type_code</th><th width="165.83984375">invoice_type_code</th><th width="214.83203125">Kohustuslikud väljad</th><th>KEELATUD väljad</th></tr></thead><tbody><tr><td>3 (Veebimakse)</td><td>-</td><td>Ainult põhiväljad: <code>client_vau_id</code>, <code>order_type</code>, <code>order_purpose_code</code></td><td><code>invoice_type_code</code>, <code>client_company_id</code>, <code>invoice_private_email</code>, kõik <code>invoice_company_*</code> väljad</td></tr><tr><td>4 (Garantiikiri või koostööleping)</td><td>-</td><td>Põhiväljad + <code>client_company_id</code></td><td><code>invoice_type_code</code>, <code>invoice_private_email</code>, kõik <code>invoice_company_*</code> väljad</td></tr><tr><td>2 (Arve)</td><td>3 (Eraisik)</td><td>Põhiväljad + <code>invoice_type_code</code> + <code>invoice_private_email</code></td><td><code>client_company_id</code>, kõik <code>invoice_company_*</code> väljad</td></tr><tr><td>2 (Arve)</td><td>2 (Asutus)</td><td>Põhiväljad + <code>invoice_type_code</code> + kõik <code>invoice_company_*</code> väljad (v.a. <code>invoice_company_nr</code> ja <code>invoice_company_type</code> , mis sõltuvad riigist)</td><td><code>client_company_id</code>, <code>invoice_private_email</code></td></tr><tr><td>2 (Arve)</td><td>2 (Asutus)</td><td><p>Kui <code>invoice_company_</code></p><p><code>country_id=1</code> (Eesti), on kohstuslik ka <code>invoice_company_nr</code> (registrikood)</p></td><td><code>invoice_company_type</code></td></tr><tr><td>2 (Arve)</td><td>2 (Asutus)</td><td><p>Kui <code>invoice_company_</code></p><p><code>country_id≠1</code> (välisriik), on kohustuslik ka <code>invoice_company_type</code></p></td><td><code>invoice_company_nr</code></td></tr></tbody></table>

{% hint style="warning" %}
**Oluline:** API lükkab tagasi päringud, mis sisaldavad keelatud välju antud kombinatsiooni puhul. Näiteks kui `billing_type_code=3` (veebimakse), siis `invoice_type_code` või `client_company_id` saatmine toob kaasa vea 12050.
{% endhint %}

#### Kasutuseesmärgi täpsustus

Väli `order_purpose_comment` on:

* **Kohustuslik**, kui `order_purpose_code` on üks järgnevatest: **1, 4, 6, 11, 12, 13, 14, 15, 16, 17, 18**
* **Keelatud** kõigil muudel juhtudel

#### Otsustamise juhend

Vali õige kombinatsioon järgmise loogika alusel:

**1. Kui klient maksab veebis (veebimakse):**

* `billing_type_code=3`
* Ära lisa ühtegi teist maksmise/arve välja

**2. Kui klient kuulub koostöölepingu/garantiikirjaga asutusse:**

* `billing_type_code=4`
* `client_company_id=[asutuse ID]`
* Ära lisa `invoice_type_code` ega `invoice_*` välju

**3. Kui saadetakse arve eraisikule:**

* `billing_type_code=2`
* `invoice_type_code=3`
* `invoice_private_email=[e-posti aadress]`
* Ära lisa `client_company_id` ega `invoice_company_*` välju

**4. Kui saadetakse arve Eesti asutusele:**

* `billing_type_code=2`
* `invoice_type_code=2`
* `invoice_company_country_id=1`
* `invoice_company=[nimi]`
* `invoice_company_nr=[registrikood]`
* `invoice_company_email`, `invoice_company_address_*` (kõik aadressiväljad)
* Ära lisa `invoice_company_type` (see on ainult välisriikide jaoks)

**5. Kui saadetakse arve välisriigi asutusele:**

* `billing_type_code=2`
* `invoice_type_code=2`
* `invoice_company_country_id=[riigi ID, ≠1]`
* `invoice_company=[nimi]`
* `invoice_company_type=[1-5]`
* `invoice_company_email`, `invoice_company_address_*` (kõik aadressiväljad)
* Ära lisa `invoice_company_nr` (registrikood on ainult Eesti asutuste jaoks)

#### Ekraanivideo konteksti mõistmiseks

Allolev video näitab, kuidas toimub makseviisi valimine VAUs. See aitab mõista, milline peaks olema UI, mille kaudu API päring koostatakse.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FHOyaA46hU1pdqKYrmFZE%2Fuploads%2F1AGKGNZDPBS6BbRdNPzk%2Ftellimuse_koostamine_1.mp4?alt=media&token=37d8bf3a-3907-4e51-881b-7bb8bcff45d8" %}

### Päringu näide (cUrl)

```shell
curl --location 'https://www.ra.ee/vau/index.php/api/ra/meediateekOrder/create?token=129f104682e2306339184f4ee59ea018' \
--header 'Content-Type: application/json' \
--data-raw '{
  "MeediateekOrder": {
    "client_vau_id": 3,
    "client_comment": "Testtellimus",
    "billing_type_code": 3,
    "order_type": 5,
    "order_purpose_code": 2,
  },
  "MeediateekOrderRow": [
    {
      "erply_product_code": "0122",
      "refcode": "EAA.1414.1.272",
      "amount": 1,
      "online_copy_title": "Ateena akropoli foto",
      "online_copy_filename": "eaa1414_001_0000272_00000_00001_f.jpg",
      "time_from": "",
      "time_to": ""
    },
    {
      "erply_product_code": "1601",
      "refcode": "EFA.203.f.2984",
      "amount": 1,
      "online_copy_title": "Tõravere",
      "online_copy_filename": "efa0203_f_02984_est_00-0-02_00_p_a_HD_v_tk02_PRD.mp4",
      "time_from": "00:01:00",
      "time_to": "00:02:30"
    }
  ]
}'
```

### Vastuse näide

Tellimuse loomine õnnestub ja tagastatakse loodud tellimuse identifikaator.

```json
{
    "responseStatus": "ok",
    "orderId": 1
}
```

### Veateated

**error 12050** - tellimust ei saa luua, kuna sisendväärtused ei valideeru

**Näide 1:** Kohustuslikud väljad on tühjad

```json
{
    "responseStatus": "error",
    "errorCode": 12050,
    "errorMessage": "Could not create order",
    "errors": [
        {
            "order_type": [
                "Tellimuse liik ei tohi olla tühi."
            ],
            "order_purpose_code": [
                "Kasutuseesmärk ei tohi olla tühi."
            ]
        },
        {
            "erply_product_code": [
                "ERPLY tootekood ei tohi olla tühi."
            ],
            "refcode": [
                "Kirjeldusüksuse leidandmed ei tohi olla tühi."
            ]
        },
        {
            "amount": [
                "Kogus peab olema arv."
            ]
        }
    ]
}
```

**Näide 2:** Keelatud väljad on esitatud (veebimakse puhul ei tohi olla invoice\_type\_code)

```json
{
    "responseStatus": "error",
    "errorCode": 12050,
    "errorMessage": "Could not create order",
    "errors": [
        {
            "invoice_type_code": [
                "Arve tüüpi ei tohiks esitada, kui maksmise viis ei ole Arve (3)."
            ]
        }
    ]
}
```

**Näide 3:** Eraisikule arvet luues ei tohi esitada asutuse andmeid

```json
{
    "responseStatus": "error",
    "errorCode": 12050,
    "errorMessage": "Could not create order",
    "errors": [
        {
            "invoice_company": [
                "Asutuse arve välja \"invoice_company\" ei tohiks esitada, kui arve tüüp ei ole Asutus (3)."
            ]
        }
    ]
}
```

**Näide 4:** Kasutuseesmärgi täpsustus on nõutud, aga puudub

```json
{
    "responseStatus": "error",
    "errorCode": 12050,
    "errorMessage": "Could not create order",
    "errors": [
        {
            "order_purpose_comment": [
                "Kasutuse täpsustus ei tohi olla tühi."
            ]
        }
    ]
}
```

**error 12051** - päringu _raw body_ ei sisalda _JSON_ _stringi,_ selles puudub _MeediateekOrder või MeediateekOrderRow_ objekt või _MeediateekOrderRow_ on tühi.

```json
{
    "responseStatus": "error",
    "errorCode": 12051,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 12052** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 12052,
    "errorMessage": "Is not POST request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
