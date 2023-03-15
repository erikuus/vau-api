---
description: Päringu dokumentatsioon
---

# Hinna vaatamine

## <mark style="color:green;">GET</mark> ra/price/view

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/price/view?token={{accessToken}}&id={{priceId}}
```
{% endcode %}

Väljastab hinnakirja rea identifikaatori alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Hinnakirja rea identifikaator<br><br><em>Identifikaatori saamise kohta vaata</em> <a href="hindade-sirvimine.md#paeringu-naeide-curl"><em>siit</em></a><em></em></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/price/view?token=3d1140862f01aa039322ca47c60a15a8&id=389' \
```
{% endcode %}

### Vastuse näide

Hinnakirja rea väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "priceDetailView": {
        "archive_unit": "Rahvusarhiiv Tartus",
        "order_type": "Koopia",
        "service_name": "Digikoopia",
        "service_et": "kuni A2 formaadis tarbekoopia (tekstidokumentidest jms), kaader",
        "service_en": "Research copy, image",
        "erply_code": "0121",
        "price": 0.4,
        "measure_unit": "tk",
        "inside": false
    }
}
```

### Veateade

**error 8010** - hinnakirja rida ei leitud (määratud identifikaatoriga hinda andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 8010,
    "errorMessage": "The requested price does not exist"
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
