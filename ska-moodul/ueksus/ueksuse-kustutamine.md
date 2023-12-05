---
description: Päringu dokumentatsioon
---

# Üksuse kustutamine

## <mark style="color:red;">DELETE</mark> ska/department/delete

```
{{apiBaseUrl}}/ska/department/delete?token={{accessToken}}&id={{departmentId}}
```

Kustutab üksuse identifikaatori alusel. Tegemist on n-ö SOFT DELETE kustutamisega, mis tähendab seda, et andmed jäävad andmebaasi alles ja need on jätkuvalt nähtavad taotluste juures, aga kustutatud üksuse identifikaatorit ei saa enam päringutes kasutada.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="149">NIMI</th><th width="101">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Üksuse identifikaator<br><br><em>NB! Üksuse identifikaatori saamise kohta vaata</em> <a data-mention href="ueksuse-loomine.md">ueksuse-loomine.md</a><em>ja</em> <a data-mention href="ueksuse-leidmine.md">ueksuse-leidmine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request DELETE 'https://www.ra.ee/vau/index.php/api/ska/department/delete?token=ea2397458ba644c6fd2d70b05adb6661&id=30' \
```
{% endcode %}

### Vastuse näide

Üksus on kustutatud.

```json
{
    "responseStatus": "ok"
}
```

### Veateade

**error 4010** - üksust ei leitud (määratud identifikaatoriga üksust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 4010,
    "errorMessage": "The requested department does not exist."
}
```

**error 4030** - üksust ei saa kustutada (määratlemata tehnilistel põhjustel)

```json
{
    "responseStatus": "error",
    "errorCode": 4030,
    "errorMessage": "Could not delete department"
}
```

**error 4031** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 4031,
    "errorMessage": "Is not DELETE request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
