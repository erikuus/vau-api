---
description: Päringu dokumentatsioon
---

# Töötaja kustutamine

## <mark style="color:red;">DELETE</mark> ska/employee/delete

```
{{apiBaseUrl}}/ska/employee/delete?token={{accessToken}}&id={{employeeId}}
```

Kustutab töötaja identifikaatori alusel. Tegemist on n-ö SOFT DELETE kustutamisega, mis tähendab seda, et andmed jäävad andmebaasi alles ja need on jätkuvalt nähtavad taotluste juures, aga kustutatud töötaja identifikaatorit ei saa enam päringutes kasutada.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="150">NIMI</th><th width="104">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Töötaja identifikaator<br><br><em>NB! Töötaja identifikaatori saamise kohta vaata</em> <a data-mention href="toeoetaja-loomine.md">toeoetaja-loomine.md</a> <em>ja</em> <a data-mention href="toeoetaja-leidmine.md">toeoetaja-leidmine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request DELETE 'https://www.ra.ee/vau/index.php/api/ska/employee/delete?token=24aad44bab3b258b06e809cc53e9083e&id=301' \
```
{% endcode %}

### Vastuse näide

Töötaja on kustutatud.

```json
{
    "responseStatus": "ok"
}
```

### Veateade

**error 5010** - töötajat ei leitud (määratud identifikaatoriga töötajat andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 5010,
    "errorMessage": "The requested employee does not exist."
}
```

**error 5030** - töötajat ei saa kustutada (määratlemata tehnilistel põhjustel)

```json
{
    "responseStatus": "error",
    "errorCode": 5030,
    "errorMessage": "Could not delete employee"
}
```

**error 5031** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 5031,
    "errorMessage": "Is not DELETE request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
