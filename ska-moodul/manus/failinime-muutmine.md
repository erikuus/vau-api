---
description: Päringu dokumentatsioon
---

# Failinime muutmine

## <mark style="color:blue;">PUT</mark> ska/file/rename

```
{{apiBaseUrl}}/ska/file/rename?token={{accessToken}}&id={{fileId}}
```

Muudab failinime identifikaatori alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="133">NIMI</th><th width="132">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Faili identifikaator<br><br><em>NB! Faili identifikaatori saamise kohta vaata</em> <a data-mention href="faili-lisamine.md">faili-lisamine.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="174">NIMI</th><th width="155">TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>employee_id *</td><td>Integer</td><td>Töötaja identifikaator, kes failinime muudab<br><br><em>NB! Töötaja identifikaatori saamise kohta vaata</em> <a data-mention href="../toeoetaja/toeoetaja-loomine.md">toeoetaja-loomine.md</a> <em>ja</em> <a data-mention href="../toeoetaja/toeoetaja-leidmine.md">toeoetaja-leidmine.md</a></td><td></td></tr><tr><td>file_name *</td><td>String (256)</td><td>Failinimi, mis võib sisaldada ainult täppideta tähti, numbreid ja sidekriipsu. Lubatud on järgmised failinime laiendused: bdoc, ddoc, asice, pdf, jpeg, jpg, png</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request PUT 'https://www.ra.ee/vau/index.php/api/ska/file/rename?token=24aad44bab3b258b06e809cc53e9083e&id=400' \
--header 'Content-Type: application/json' \
--data-raw '{
    "employee_id": 301,
    "file_name": "test1.jpg"
}'
```
{% endcode %}

### Vastuse näide

Failinime muutmine õnnestub.

```json
{
    "responseStatus": "ok"
}
```

### Veateated

**error 6040** - failinime ei saa muuta (määratlemata tehnilistel põhjustel)

```json
{
    "responseStatus": "error",
    "errorCode": 6040,
    "errorMessage": "Could not rename file"
}
```

**error 6041** - failinime ei saa muuta, kuna sisendväärtused ei valideeru

```json
{
    "responseStatus": "error",
    "errorCode": 6041,
    "errorMessage": "Could not rename file",
    "errors": {
        "file_name": [
            "Failinimi \"test1.jpg\" on juba kasutuses."
        ],
        "employee_id": [
            "Töötaja \"0\" ei eksisteeri."
        ]
    }
}
```

**error 6042** - päringu _raw body_ ei sisalda _JSON_ _stringi_

```json
{
    "responseStatus": "error",
    "errorCode": 6042,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 6043** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 6043,
    "errorMessage": "Is not PUT request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
