---
description: Päringu dokumentatsioon
---

# Üksuse vaatamine

## <mark style="color:green;">GET</mark> ra/price/view

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/unit/view?token={{accessToken}}&code={{unitCode}}
```
{% endcode %}

Väljastab arhiiviüksuse andmed koodi (lühinime) alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="123">NIMI</th><th width="106">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>code *</td><td>String</td><td>Arhiiviüksuse kood ehk lühinimi<br><br><em>Koodi ehk lühinime saamise kohta vaata</em> <a href="../../ska-moodul/ueksus/ueksuste-sirvimine.md#vastuse-naeide"><em>siit</em></a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/unit/view?token=3d1140862f01aa039322ca47c60a15a8&code=Tartu' \
```
{% endcode %}

### Vastuse näide

Üksuse väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "unitDetailView": {
        "id": 1,
        "code": "Tartu",
        "title_et": "Rahvusarhiiv Tartus",
        "title_en": "National Archives in Tartu"
    }
}
```

### Veateade

**error 9010** - arhiiviüksust ei leitud (määratud koodiga üksust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 9010,
    "errorMessage": "The requested unit does not exist"
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
