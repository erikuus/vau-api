---
description: Päringu dokumentatsioon
---

# Töötaja leidmine

## <mark style="color:green;">GET</mark> ska/employee/find

```
{{apiBaseUrl}}/ska/employee/find?token={{accessToken}}&email={{employeeEmail}}
```

Väljastab töötaja identifikaatori töötaja e-posti aadressi alusel.&#x20;

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>email</td><td>String</td><td>Töötaja e-posti aadress (tõstutundetu)</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/employee/find?token=24aad44bab3b258b06e809cc53e9083e&email=erik.UUS@gmail.COM' \
```
{% endcode %}

### Vastuse näide

Töötaja identifikaatori väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "employeeId": 301
}
```

### Veateade

**error 5020** - töötajat ei leitud (määratud e-posti aadressiga töötajat andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 5020,
    "errorMessage": "The requested employee does not exist."
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
