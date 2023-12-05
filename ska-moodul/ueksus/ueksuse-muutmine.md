---
description: Päringu dokumentatsioon
---

# Üksuse muutmine

## <mark style="color:blue;">PUT</mark> ska/department/update

```
{{apiBaseUrl}}/ska/department/update?token={{accessToken}}&id={{departmentId}}
```

Muudab üksuse andmeid identifikaatori alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="135">NIMI</th><th width="103">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Üksuse identifikaator<br><br><em>NB! Üksuse identifikaatori saamise kohta vaata</em> <a data-mention href="ueksuse-loomine.md">ueksuse-loomine.md</a><em>ja</em> <a data-mention href="ueksuse-leidmine.md">ueksuse-leidmine.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="248">NIMI</th><th>TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>name *</td><td>String (256)</td><td>Üksuse nimi</td><td></td></tr><tr><td>address *</td><td>String (256)</td><td>Üksuse aadress</td><td></td></tr><tr><td>zip *</td><td>String (16)</td><td>Üksuse postiindeks</td><td></td></tr><tr><td>email *</td><td>String (128)</td><td>Üksuse e-posti aadress</td><td></td></tr><tr><td>phone *</td><td>String (16)</td><td>Üksuse telefoninumber</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request PUT 'https://www.ra.ee/vau/index.php/api/ska/department/update?token=bd266e2a556dc5331917d86252262c30&id=30' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Test osakond_",
    "address": "Tammsaare 8-25, Tartu_",
    "zip": "51006_",
    "email": "erik.uus@gmail.com",
    "phone": "+372 5322 5388_"
}'
```
{% endcode %}

### Vastuse näide

Üksuse muutmine õnnestub.

```json
{
    "responseStatus": "ok"
}
```

### Veateated

**error 4010** - üksust ei leitud (määratud identifikaatoriga üksust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 4010,
    "errorMessage": "The requested department does not exist."
}
```

**error 4040** - üksust ei saa muuta, kuna sisendväärtused ei valideeru&#x20;

```json
{
    "responseStatus": "error",
    "errorCode": 4040,
    "errorMessage": "Could not update department",
    "errors": {
        "name": [
            "Nimi ei tohi olla tühi."
        ],
        "email": [
            "E-post ei ole korrektne e-posti aadress."
        ]
    }
}
```

**error 4041** - päringu _raw body_ ei sisalda _JSON_ _stringi_

```json
{
    "responseStatus": "error",
    "errorCode": 4041,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 4042** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 4042,
    "errorMessage": "Is not PUT request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
