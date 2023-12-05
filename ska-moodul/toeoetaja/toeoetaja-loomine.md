---
description: Päringu dokumentatsioon
---

# Töötaja loomine

## <mark style="color:orange;">POST</mark> ska/employee/create

```
{{apiBaseUrl}}/ska/employee/create?token={{accessToken}}
```

Loob uue töötaja ja tagastab selle identifikaatori.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="248">NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="193">NIMI</th><th width="156">TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>firstname *</td><td>String (128)</td><td>Töötaja eesnimi</td><td></td></tr><tr><td>lastname *</td><td>String (128)</td><td>Töötaja perekonnanimi</td><td></td></tr><tr><td>email *</td><td>String (128)</td><td>Töötaja e-posti aadress</td><td></td></tr><tr><td>phone *</td><td>String (16)</td><td>Töötaja telefoninumber</td><td></td></tr><tr><td>department_id *</td><td>Integer</td><td>Üksuse identifikaator, kuhu töötaja kuulub<br><br><em>NB! Üksuse identifikaatori saamise kohta vaata</em> <a data-mention href="../ueksus/ueksuse-loomine.md">ueksuse-loomine.md</a><em>ja</em> <a data-mention href="../ueksus/ueksuse-leidmine.md">ueksuse-leidmine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request POST 'https://www.ra.ee/vau/index.php/api/ska/employee/create?token=ea2397458ba644c6fd2d70b05adb6661' \
--header 'Content-Type: application/json' \
--data-raw '{
    "firstname": "Erik",
    "lastname": "Uus",
    "email": "erik.uus@ra.ee",
    "phone": "+372 5322 5388",
    "department_id": 30
}'
```
{% endcode %}

### Vastuse näide

Uue töötaja loomine õnnestub ja tagastatakse loodud töötaja identifikaator.

```json
{
    "responseStatus": "ok",
    "employeeId": 301
}
```

### Veateated

**error 5050** - töötajat ei saa luua, kuna sisendväärtused ei valideeru&#x20;

```json
{
    "responseStatus": "error",
    "errorCode": 5050,
    "errorMessage": "Could not create employee",
    "errors": {
        "firstname": [
            "Eesnimi ei tohi olla tühi."
        ],
        "email": [
            "E-post ei ole korrektne e-posti aadress."
        ]
    }
}
```

**error 5051** - päringu _raw body_ ei sisalda _JSON_ _stringi_

```json
{
    "responseStatus": "error",
    "errorCode": 5051,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 5052** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 5052,
    "errorMessage": "Is not POST request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
