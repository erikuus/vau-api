---
description: Päringu dokumentatsioon
---

# Üksuse loomine

## <mark style="color:orange;">POST</mark> ska/department/create

```
{{apiBaseUrl}}/ska/department/create?token={{accessToken}}
```

Loob uue üksuse ja tagastab selle identifikaatori.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>name *</td><td>String (256)</td><td>Üksuse nimi</td><td></td></tr><tr><td>address *</td><td>String (256)</td><td>Üksuse aadress</td><td></td></tr><tr><td>zip *</td><td>String (16)</td><td>Üksuse postiindeks</td><td></td></tr><tr><td>email *</td><td>String (128)</td><td>Üksuse e-posti aadress</td><td></td></tr><tr><td>phone *</td><td>String (16)</td><td>Üksuse telefoninumber</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request POST 'https://www.ra.ee/vau/index.php/api/ska/department/create?token=bd266e2a556dc5331917d86252262c30' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Test osakond",
    "address": "Tammsaare 8-25, Tartu",
    "zip": "51006",
    "email": "erik.uus@ra.ee",
    "phone": "+372 5322 5388"
}'
```
{% endcode %}

### Vastuse näide

Uue üksuse loomine õnnestub ja tagastatakse loodud üksuse identifikaator.

```json
{
    "responseStatus": "ok",
    "departmentId": 30
}
```

### Veateated

**error 4050** - üksust ei saa luua, kuna sisendväärtused ei valideeru&#x20;

```json
{
    "responseStatus": "error",
    "errorCode": 4050,
    "errorMessage": "Could not create department",
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

**error 4051** - päringu _raw body_ ei sisalda _JSON_ _stringi_

```json
{
    "responseStatus": "error",
    "errorCode": 4051,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 4052** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 4052,
    "errorMessage": "Is not POST request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 __ OK".&#x20;
{% endhint %}
