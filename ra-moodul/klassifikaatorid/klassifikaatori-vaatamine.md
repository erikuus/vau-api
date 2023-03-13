---
description: Päringu dokumentatsioon
---

# Klassifikaatori vaatamine

## <mark style="color:green;">GET</mark> ra/lookup/view

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/lookup/view?token={{accessToken}}&type={{lookupType}}&code={{lookupCode}}
```
{% endcode %}

Väljastab klassifikaatori andmed koodi alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>type *</td><td>String</td><td><p>Klassifikaatori tüüp</p><p></p><p>Võimalikud väärtused on: <code>purpose</code> või <code>measure_unit</code></p></td><td></td></tr><tr><td>code *</td><td>Integer</td><td>Klassifikaatori kood<br><br><em>Klassifikaatori koodi saamise kohta vaata</em> <a href="klassifikaatorite-sirvimine.md#vastuse-naeide"><em>siit</em></a><em></em></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ra/lookup/view?token=9c7ac26ae69ba392be82c2315d3c45e3&type=purpose&code=1' \
```
{% endcode %}

### Vastuse näide

Klassifikaatori andmete väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "lookupDetailView": {
        "code": 1,
        "name_et": "Teadustöö",
        "name_en": "Scientific research",
        "position": 1
    }
}
```

### Veateade

**error 7010** - klassifikaatorit ei leitud (määratud koodiga klassifikaatorit andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 7010,
    "errorMessage": "The requested lookup does not exist"
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
