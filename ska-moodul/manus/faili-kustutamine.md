---
description: Päringu dokumentatsioon
---

# Faili kustutamine

## <mark style="color:red;">DELETE</mark> ska/file/delete

```
{{apiBaseUrl}}/ska/file/delete?token={{accessToken}}&id={{fileId}}
```

Kustutab faili identifikaatori alusel. Faili saab kustutada taotluselt, mis ei ole veel Rahvusarhiivi saadetud.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Faili identifikaator<br><br><em>NB! Faili identifikaatori saamise kohta vaata</em> <a data-mention href="faili-lisamine.md">faili-lisamine.md</a><em></em></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request DELETE 'https://www.ra.ee/vau/index.php/api/ska/file/delete?token=24aad44bab3b258b06e809cc53e9083e&id=400' \
```
{% endcode %}

### Vastuse näide

Fail on kustutatud.

```json
{
    "responseStatus": "ok"
}
```

### Veateade

**error 6020** - faili ei leitud (määratud identifikaatoriga faili andmebaasis registreeritud ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 6020,
    "errorMessage": "The requested file does not exist"
}
```

**error 6030** - faili ei saa kustutada, kuna taotlus on juba Rahvusarhiivi saadetud

```json
{
    "responseStatus": "error",
    "errorCode": 6030,
    "errorMessage": "The requested application is in sent status and file could not be uploaded"
}
```

**error 6031** - faili ei saa kustutada (määratlemata tehnilistel põhjustel)

```json
{
    "responseStatus": "error",
    "errorCode": 6031,
    "errorMessage": "Could not delete file"
}
```

**error 6032** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 6032,
    "errorMessage": "Is not DELETE request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 __ OK".&#x20;
{% endhint %}
