---
description: Päringu dokumentatsioon
---

# Testimine

## <mark style="color:green;">GET</mark> ska/department/test

```
{{apiBaseUrl}}/ska/department/test?token={{accessToken}}
```

Testib, kas üksust puudutav päringute grupp on kättesaadav. Normaaljuhul pole see vajalik, aga kui mingil tehnilisel põhjusel üksust puudutav päringute grupp muutub kättesaamatuks, näiteks annavad kõik päringud vastuseks Internal Server Error, saab selle päringu kaudu tuvastada, millal päringud muutuvad jälle kättesaadavaks.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="160">NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/department/test?token=bd266e2a556dc5331917d86252262c30' \
```
{% endcode %}

### Vastuse näide

Päringute grupp on kättesaadav.

```json
{
    "responseStatus": "ok"
}
```

### Veateade

Päringute grupp ei ole serveri sisemise vea tõttu kättesaadav.

```json
{
    "responseStatus": "error",
    "errorCode": 500,
    "errorMessage": "DepartmentController does not have a method \"test\"."
}
```

