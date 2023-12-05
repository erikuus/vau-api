---
description: Päringu dokumentatsioon
---

# Töötaja muutmine

## <mark style="color:blue;">PUT</mark> ska/employee/update

```
{{apiBaseUrl}}/ska/employee/update?token={{accessToken}}&id={{employeeId}}
```

Muudab töötaja andmeid identifikaatori alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="155">NIMI</th><th width="94">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Töötaja identifikaator<br><br><em>NB! Töötaja identifikaatori saamise kohta vaata</em> <a data-mention href="toeoetaja-loomine.md">toeoetaja-loomine.md</a> <em>ja</em> <a data-mention href="toeoetaja-leidmine.md">toeoetaja-leidmine.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="195">NIMI</th><th width="163">TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>firstname *</td><td>String (128)</td><td>Töötaja eesnimi</td><td></td></tr><tr><td>lastname *</td><td>String (128)</td><td>Töötaja perekonnanimi</td><td></td></tr><tr><td>email *</td><td>String (128)</td><td>Töötaja e-posti aadress</td><td></td></tr><tr><td>phone *</td><td>String (16)</td><td>Töötaja telefoninumber</td><td></td></tr><tr><td>department_id *</td><td>Integer</td><td>Üksuse identifikaator, kuhu töötaja kuulub<br><br><em>NB! Üksuse identifikaatori saamise kohta vaata</em> <a data-mention href="../ueksus/ueksuse-loomine.md">ueksuse-loomine.md</a><em>ja</em> <a data-mention href="../ueksus/ueksuse-leidmine.md">ueksuse-leidmine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request PUT 'https://www.ra.ee/vau/index.php/api/ska/employee/update?token=ea2397458ba644c6fd2d70b05adb6661&id=268' \
--header 'Content-Type: application/json' \
--data-raw '{
    "firstname": "Erik_",
    "lastname": "Uus_",
    "email": "erik.uus@gmail.com",
    "phone": "+372 5322 5389",
    "department_id": 16
}'
```
{% endcode %}

### Vastuse näide

Töötaja muutmine õnnestub.

```json
{
    "responseStatus": "ok"
}
```

### Veateated

**error 5010** - töötajat ei leitud (määratud identifikaatoriga töötajat andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 5010,
    "errorMessage": "The requested employee does not exist."
}
```

**error 5040** - töötajat ei saa muuta, kuna sisendväärtused ei valideeru&#x20;

```json
{
    "responseStatus": "error",
    "errorCode": 5040,
    "errorMessage": "Could not update employee",
    "errors": {
        "firstname": [
            "Eesnimi ei tohi olla tühi."
        ],
        "department_id": [
            "Üksus \"16000\" ei eksisteeri."
        ],
        "email": [
            "E-post ei ole korrektne e-posti aadress."
        ]
    }
}
```

**error 5041** - päringu _raw body_ ei sisalda _JSON_ _stringi_

```json
{
    "responseStatus": "error",
    "errorCode": 5041,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 5042** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 5042,
    "errorMessage": "Is not PUT request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
