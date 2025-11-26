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

Teenuseread tuleb lisada massiiv `MeediateekOrderRow`:

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

<table><thead><tr><th width="287.6171875">NIMI</th><th width="131.32421875">TÜÜP (PIKKUS)</th><th>SELGITUS</th></tr></thead><tbody><tr><td>client_vau_id *</td><td>Integer</td><td>Tellija VAU kasutajakonto identifikaator</td></tr><tr><td>client_comment</td><td>Text</td><td>Tellija märkused tellimuse kohta</td></tr><tr><td>billing_type_code *</td><td>Integer</td><td>Maksmise viis<br><br><em>2 - Arve</em><br><em>3 - Veebimakse</em><br><em>4 - Koondarve</em><br><br>Kohustuslik väli, mis määrab, millised muud väljad on nõutavad või lubatud (vaata <a href="#valideerimisreeglid">Valideerimisreeglid</a>)</td></tr><tr><td>invoice_type_code</td><td>Integer</td><td>Arve tüüp<br><br><em>2 - Asutus</em><br><em>3 - Eraisik e-arve</em><br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve). Keelatud, kui <code>billing_type_code</code> on 3 või 4</td></tr><tr><td>client_company_id</td><td>Integer</td><td>Koostöölepingu või garantiikirjaga asutus<br><br>Kohustuslik, kui <code>billing_type_code=4</code> (Koondarve). Keelatud, kui <code>billing_type_code</code> on 2 või 3<br><br>Asutuse andmeid saab pärida kasutades API endpoint'e <a href="../asutus/kasutaja-asutuste-sirvimine.md">Kasutaja asutuste sirvimine</a> ja <a href="../asutus/asutuse-vaatamine.md">Asutuse vaatamine</a></td></tr><tr><td>invoice_private_email</td><td>String (256)</td><td>Eraisiku e-posti aadress, kuhu saadetakse arve<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=3</code> (Eraisik e-arve). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company</td><td>String (256)</td><td>Arveldatava asutuse nimi<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_nr</td><td>String (32)</td><td>Arveldatava asutuse registrikood<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus) JA <code>invoice_company_country_id=1</code> (Eesti). Keelatud kõigil muudel juhtudel<br><br>Kasutajaliideses on soovitav kasutada <em>autocomplete</em> välja, mis pakub valikuid äriregistri teenuse kaudu <a href="https://ariregister.rik.ee/est/api/autocomplete">https://ariregister.rik.ee/est/api/autocomplete</a></td></tr><tr><td>invoice_company_type</td><td>Integer</td><td>Arveldatava välisriigi asutuse tüüp<br><br><em>1 - Valitsusasutus</em><br><em>2 - Kohalik omavalitsus</em><br><em>3 - Rahvusvaheline organisatsioon</em><br><em>4 - Krediidi/rahaasutus</em><br><em>5 - Muu</em><br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus) JA <code>invoice_company_country_id≠1</code> (välisriik). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_email</td><td>String (256)</td><td>Arveldatava asutuse e-post<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_street</td><td>String (256)</td><td>Arveldatava asutuse aadress: tänav/maja<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_city</td><td>String (256)</td><td>Arveldatava asutuse aadress: linn/vald<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_county</td><td>String (256)</td><td>Arveldatava asutuse aadress: maakond<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_address_zip</td><td>String (16)</td><td>Arveldatava asutuse aadress: postiindeks<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel</td></tr><tr><td>invoice_company_country_id</td><td>Integer</td><td>Arveldatava asutuse riik<br><br>Kohustuslik, kui <code>billing_type_code=2</code> (Arve) JA <code>invoice_type_code=2</code> (Asutus). Keelatud kõigil muudel juhtudel<br><br>Riikide andmeid saab pärida kasutades API endpoint'i <a href="../riik/riikide-sirvimine.md">Riikide sirvimine</a></td></tr><tr><td>order_type *</td><td>Integer</td><td><p>Tellimuse liik</p><p><br><em>1 - Laenutus</em></p><p><em>2- Siselaenutus</em></p><p><em>3 - Kauglaenutus</em></p><p><em>4 - Deponeerimine</em></p><p><em>5 - Koopia</em></p><p><em>6 - Virtuaalne tellimus</em></p></td></tr><tr><td>order_purpose_code *</td><td>Integer</td><td><p>Kasutuseesmärk</p><p><br><em>1 - Teadustöö</em></p><p><em>2 - Kodu-uurimine</em></p><p><em>3 - Genealoogia</em></p><p><em>4 - Õppetöö</em></p><p><em>5 - Õiguste tõestamine</em></p><p><em>6 - Muu</em></p><p><em>7 - Genealoogia/kodu-uurimine</em></p><p><em>8 - Teadustöö/kodu-uurimine</em></p><p><em>10 - Isiklikuks kasutuseks</em></p><p><em>11 - Publikatsioon</em></p><p><em>12 - Ajakirjandus</em></p><p><em>13 - Avalik üritus (tasuta)</em></p><p><em>14 - Avalik üritus (tasuline)</em></p><p><em>15 - Telefilm/telesaade</em></p><p><em>16 - Film</em></p><p><em>17 - Veeb</em></p><p><em>18 - Reklaam</em></p><br>Klassifikaatori andmeid saab pärida kasutades API endpoint'i <a href="../klassifikaatorid/klassifikaatorite-sirvimine.md">Klassifikaatorite sirvimine</a> (type=purpose_meediateek)</td></tr><tr><td>order_purpose_comment</td><td>Text</td><td>Kasutuse täpsustus<br><br>Kohustuslik, kui <code>order_purpose_code</code> on üks järgnevatest: 1, 4, 6, 11, 12, 13, 14, 15, 16, 17, 18. Keelatud kõigil muudel juhtudel</td></tr></tbody></table>

#### MeediateekOrderRow

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="211.86328125">NIMI</th><th width="154.77734375">TÜÜP</th><th>SELGITUS</th></tr></thead><tbody><tr><td>erply_product_code *</td><td>String (256)</td><td>Tootekood ERPLY majandustarkvaras</td></tr><tr><td>refcode *</td><td>String (256)</td><td>Kirjeldusüksuse leidandmed</td></tr><tr><td>amount *</td><td>Integer</td><td><p><em>Kogus</em></p><p><br><em>- digikoopiate puhul 1</em><br><em>- filmi/heli lõikude puhul sekundipõhine</em></p></td></tr><tr><td>online_copy_title</td><td>String (256)</td><td>Veebikoopia pealkiri<br><em>video/heli puhul</em></td></tr><tr><td>online_copy_filename</td><td>String (256)</td><td>Veebikoopia failinimi<br><em>video/heli puhul</em></td></tr><tr><td>time_from</td><td>String (16)</td><td>Ajakood, lõigu algus</td></tr><tr><td>time_to</td><td>String (16)</td><td>Ajakood, lõigu lõpp</td></tr></tbody></table>

### Valideerimisreeglid

API valideerib tellimuse andmeid range kontrolliga, mis tagab andmete kooskõla ja takistab vastuoluliste väljadega tellimuste loomist.

#### Lubatud kombinatsioonid

Tellimuse maksmise ja arveldamise väljad peavad vastama ühele järgnevatest viiest kombinatsioonist:

<table><thead><tr><th width="150">billing_type_code</th><th width="150">invoice_type_code</th><th>Kohustuslikud väljad</th><th>KEELATUD väljad</th></tr></thead><tbody><tr><td>3 (Veebimakse)</td><td>-</td><td>Ainult põhiväljad: <code>client_vau_id</code>, <code>order_type</code>, <code>order_purpose_code</code></td><td><code>invoice_type_code</code>, <code>client_company_id</code>, <code>invoice_private_email</code>, kõik <code>invoice_company_*</code> väljad</td></tr><tr><td>4 (Koondarve)</td><td>-</td><td>Põhiväljad + <code>client_company_id</code></td><td><code>invoice_type_code</code>, <code>invoice_private_email</code>, kõik <code>invoice_company_*</code> väljad</td></tr><tr><td>2 (Arve)</td><td>3 (Eraisik e-arve)</td><td>Põhiväljad + <code>invoice_type_code</code> + <code>invoice_private_email</code></td><td><code>client_company_id</code>, kõik <code>invoice_company_*</code> väljad</td></tr><tr><td>2 (Arve)</td><td>2 (Asutus)</td><td>Põhiväljad + <code>invoice_type_code</code> + kõik <code>invoice_company_*</code> väljad (v.a. <code>invoice_company_nr</code> ja <code>invoice_company_type</code> - need sõltuvad riigist)</td><td><code>client_company_id</code>, <code>invoice_private_email</code></td></tr><tr><td>2 (Arve)</td><td>2 (Asutus)</td><td>Kui <code>invoice_company_country_id=1</code> (Eesti): lisaks <code>invoice_company_nr</code> (registrikood)</td><td><code>invoice_company_type</code></td></tr><tr><td>2 (Arve)</td><td>2 (Asutus)</td><td>Kui <code>invoice_company_country_id≠1</code> (välisriik): lisaks <code>invoice_company_type</code></td><td><code>invoice_company_nr</code></td></tr></tbody></table>

{% hint style="warning" %}
**Oluline:** API lükkab tagasi päringud, mis sisaldavad keelatud välju antud kombinatsiooni puhul. Näiteks kui `billing_type_code=3` (Veebimakse), siis `invoice_type_code` või `client_company_id` sisaldamine toob kaasa vea 12050.
{% endhint %}

#### Kasutuseesmärgi täpsustus

Väli `order_purpose_comment` on:
- **Kohustuslik**, kui `order_purpose_code` on üks järgnevatest: **1, 4, 6, 11, 12, 13, 14, 15, 16, 17, 18**
- **Keelatud** kõigil muudel juhtudel (nt. kui `order_purpose_code=2, 3, 5, 7, 8 või 10`)

#### Otsustamise juhend

Vali õige kombinatsioon järgmise loogika alusel:

**1. Kui klient maksab veebis (veebimakse):**
- `billing_type_code=3`
- Ära lisa ühtegi teist maksmise/arveldamise välja

**2. Kui klient kuulub koostöölepingu/garantiikirjaga asutusse:**
- `billing_type_code=4`
- `client_company_id=[asutuse ID]`
- Ära lisa `invoice_type_code` ega `invoice_*` välju

**3. Kui saadetakse arve eraisikule:**
- `billing_type_code=2`
- `invoice_type_code=3`
- `invoice_private_email=[e-posti aadress]`
- Ära lisa `client_company_id` ega `invoice_company_*` välju

**4. Kui saadetakse arve Eesti asutusele:**
- `billing_type_code=2`
- `invoice_type_code=2`
- `invoice_company_country_id=1`
- `invoice_company=[nimi]`
- `invoice_company_nr=[registrikood]`
- `invoice_company_email`, `invoice_company_address_*` (kõik aadressiväljad)
- Ära lisa `invoice_company_type` (see on ainult välisriikide jaoks)

**5. Kui saadetakse arve välisriigi asutusele:**
- `billing_type_code=2`
- `invoice_type_code=2`
- `invoice_company_country_id=[riigi ID, ≠1]`
- `invoice_company=[nimi]`
- `invoice_company_type=[1-5]`
- `invoice_company_email`, `invoice_company_address_*` (kõik aadressiväljad)
- Ära lisa `invoice_company_nr` (registrikood on ainult Eesti asutuste jaoks)

### Päringu näide (cUrl)

```shell
curl --location 'https://www.ra.ee/vautest/index.php/api/ra/meediateekOrder/create?token=129f104682e2306339184f4ee59ea018' \
--header 'Content-Type: application/json' \
--data-raw '{
  "MeediateekOrder": {
    "client_vau_id": 3,
    "client_comment": "Testtellimus Postmani jaoks",
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

**Näide 2:** Keelatud väljad on esitatud (veebimakse puhul ei tohi olla invoice_type_code)

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
