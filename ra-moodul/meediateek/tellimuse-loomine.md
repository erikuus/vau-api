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

<table><thead><tr><th width="287.6171875">NIMI</th><th width="131.32421875">TÜÜP (PIKKUS)</th><th>SELGITUS</th></tr></thead><tbody><tr><td>client_vau_id *</td><td>Integer</td><td>Tellija VAU kasutajakonto identifikaator</td></tr><tr><td>client_comment</td><td>Text</td><td>Tellija märkused tellimuse kohta</td></tr><tr><td>client_company_id</td><td>Integer</td><td>Koostöölepingu või garantiikirjaga asutus<br><br>Kui klient on seotud sellise asutusega, tuleb tellimuse juures täita vaid <code>client_company_id</code> – teisi asutuse välju pole vaja täita</td></tr><tr><td>client_company_country_id</td><td>Integer</td><td>Esindatava asutuse riik (country.id)</td></tr><tr><td>client_company</td><td>String (256)</td><td>Esindatava asutuse nimi</td></tr><tr><td>client_company_nr</td><td>String (256)</td><td>Esindatava asutuse registrikood<br><br>Kasutajaliideses on soovitav kasutada selle küsimiseks <em>autocomplete</em> välja, mis pakub valikuid äriregistri teenuse kaudu <a href="https://ariregister.rik.ee/est/api/autocomplete">https://ariregister.rik.ee/est/api/autocomplete</a></td></tr><tr><td>client_company_email</td><td>String (256)</td><td>Esindatava asutuse e-post</td></tr><tr><td>client_company_address_street</td><td>String (256)</td><td>Tänav/maja</td></tr><tr><td>client_company_address_city</td><td>String (256)</td><td>Linn/vald</td></tr><tr><td>client_company_address_county</td><td>String (256)</td><td>Maakond</td></tr><tr><td>client_company_address_zip</td><td>String (16)</td><td>Postiindeks</td></tr><tr><td>order_type *</td><td>Integer</td><td><p>Tellimuse liik</p><p><br><em>1 - Laenutus</em></p><p><em>2- Siselaenutus</em></p><p><em>3 - Kauglaenutus</em></p><p><em>4 - Deponeerimine</em></p><p><em>5 - Koopia</em></p><p><em>6 - Virtuaalne tellimus</em></p></td></tr><tr><td>order_purpose_code *</td><td>Integer</td><td><p>Kasutuseesmärk<br><br><em>1 - Teadustöö</em></p><p><em>2 - Kodu-uurimine</em></p><p><em>3 - Genealoogia</em></p><p><em>4 - Õppetöö</em></p><p><em>5 - Õiguste tõestamine</em></p><p><em>6 - Muu</em></p><p><em>7 - Genealoogia/kodu-uurimine</em></p><p><em>8 - Teadustöö/kodu-uurimine</em></p><p><em>10 - Isiklikuks kasutuseks</em></p><p><em>11 - Publikatsioon</em></p><p><em>12 - Ajakirjandus</em></p><p><em>13 - Avalik üritus (tasuta)</em></p><p><em>14 - Avalik üritus (tasuline)</em></p><p><em>15 - Telefilm/telesaade</em></p><p><em>16 - Film</em></p><p><em>17 - Veeb</em></p><p><em>18 - Reklaam</em></p></td></tr><tr><td>order_purpose_comment</td><td>Text</td><td>Kasutuse täpsustus<br><br><em>Kohustuslik, kui kasutuseesmärk on 1, 4, 6, 11-18</em></td></tr></tbody></table>

#### MeediateekOrderRow

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="211.86328125">NIMI</th><th width="154.77734375">TÜÜP</th><th>SELGITUS</th></tr></thead><tbody><tr><td>erply_product_code *</td><td>String (256)</td><td>Tootekood ERPLY majandustarkvaras</td></tr><tr><td>refcode *</td><td>String (256)</td><td>Kirjeldusüksuse leidandmed</td></tr><tr><td>amount *</td><td>Integer</td><td><p><em>Kogus</em></p><p><br><em>- digikoopiate puhul 1</em><br><em>- filmi/heli lõikude puhul sekundipõhine</em></p></td></tr><tr><td>online_copy_title</td><td>String (256)</td><td>Veebikoopia pealkiri<br><em>video/heli puhul</em></td></tr><tr><td>online_copy_filename</td><td>String (256)</td><td>Veebikoopia failinimi<br><em>video/heli puhul</em></td></tr><tr><td>time_from</td><td>String (16)</td><td>Ajakood, lõigu algus</td></tr><tr><td>time_to</td><td>String (16)</td><td>Ajakood, lõigu lõpp</td></tr></tbody></table>

### Päringu näide (cUrl)

```shell
curl --location 'https://www.ra.ee/vautest/index.php/api/ra/meediateekOrder/create?token=129f104682e2306339184f4ee59ea018' \
--header 'Content-Type: application/json' \
--data-raw '{
  "MeediateekOrder": {
    "client_vau_id": 3,
    "client_comment": "Testtellimus Postmani jaoks",
    "client_company_id": null,
    "client_company_country_id": 1,
    "client_company": "Näidisettevõte OÜ",
    "client_company_nr": "12345678",
    "client_company_email": "info@naidisettevote.ee",
    "client_company_address_street": "Näidisväli 12",
    "client_company_address_city": "Tallinn",
    "client_company_address_county": "Harju maakond",
    "client_company_address_zip": "10123",
    "order_type": 5,
    "order_purpose_code": 6,
    "order_purpose_comment": "Testimise eesmärgil"
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

**error 12051** - päringu _raw body_ ei sisalda _JSON_ _stringi_ või selles puudub _MeediateekOrder_ objekt

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
