---
description: Päringu dokumentatsioon
---

# Taotluse saatmine

## <mark style="color:blue;">PUT</mark> ska/application/send

```

{{apiBaseUrl}}/ska/application/send?token={{accessToken}}&id={{applicationId}}
```

Saadab taotluse Rahvusarhiivi. Saadetud taotlus ilmub Rahvusarhiivi arhiivipäringute haldamise moodulisse ja Rahvusarhiivi töötajad hakkavad seda menetlema.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Taotluse identifikaator<br><br><em>NB! Taotluse identifikaatori saamise kohta vaata</em> <a data-mention href="taotluse-loomine.md">taotluse-loomine.md</a><em></em></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request PUT 'https://www.ra.ee/vau/index.php/api/ska/application/send?token=db9a1afb27d892ad3303095ce580f9cc&id=16610'
```
{% endcode %}

### Vastuse näide

Taotluse saatmine Rahvusarhiivi õnnestub.

```json
{
    "responseStatus": "ok"
}
```

### Veateated

**error 3010** - taotlust ei leitud (määratud identifikaatoriga taotlust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 3010,
    "errorMessage": "The requested application does not exist"
}
```

**error 3030** - taotlust ei saa saata, kuna see on juba saadetud

```json
{
    "responseStatus": "error",
    "errorCode": 3030,
    "errorMessage": "The requested application is already sent"
}
```

**error 3031** - taotlust ei saa saata (määratlemata tehnilistel põhjustel)

```json
{
    "responseStatus": "error",
    "errorCode": 3031,
    "errorMessage": "Sending application failed"
}
```

**error 3032** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 3032,
    "errorMessage": "Is not PUT request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 __ OK".&#x20;
{% endhint %}
