---
description: Päringu dokumentatsioon
---

# Teenuste sirvimine

## <mark style="color:green;">GET</mark> ra/service/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/service/list?token={{accessToken}}
```
{% endcode %}

Väljastab teenuste gruppide nimekirja. Teenuste grupid on järjestatud kasvavalt (ASC) järjekorranumbri (position) järgi, mille on määranud VAU haldurid.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="197">NIMI</th><th width="152">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/service/list?token=3d1140862f01aa039322ca47c60a15a8' \
```
{% endcode %}

### Vastuse näide

Teenuste gruppide nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "serviceListView": [
        {
            "id": 3,
            "name_et": "Digikoopia",
            "name_en": "Digital copy",
            "position": 1
        },
        {
            "id": 2,
            "name_et": "Paberkoopia",
            "name_en": "Paper Copy",
            "position": 2
        },
        {
            "id": 1,
            "name_et": "Kirjutus andmekandjale",
            "name_en": "Writing on storage media",
            "position": 3
        },
        {
            "id": 11,
            "name_et": "Muud teenused",
            "name_en": "Other services",
            "position": 4
        },
        {
            "id": 12,
            "name_et": "Fotost koopia valmistamine",
            "name_en": "Photo copy",
            "position": 5
        }
    ]
}
```

Mitte ühtegi teenuste gruppi ei leitud.

```json
{
    "responseStatus": "ok",
    "serviceListView": []
}
```
