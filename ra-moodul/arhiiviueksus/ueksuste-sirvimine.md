---
description: Päringu dokumentatsioon
---

# Üksuste sirvimine

## <mark style="color:green;">GET</mark> ra/unit/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/unit/list?token={{accessToken}}
```
{% endcode %}

Väljastab arhiiviüksuste nimekirja. Arhiiviüksused on järjestatud kasvavalt (ASC) identifikaatori järgi.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="197">NIMI</th><th width="152">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/unit/list?token=3d1140862f01aa039322ca47c60a15a8' \
```
{% endcode %}

### Vastuse näide

Arhiiviüksuste nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "unitListView": [
        {
            "id": 1,
            "code": "Tartu",
            "title_et": "Rahvusarhiiv Tartus",
            "title_en": "National Archives in Tartu"
        },
        {
            "id": 2,
            "code": "Filmiarhiiv",
            "title_et": "Filmiarhiiv",
            "title_en": "Film Archives"
        },
        {
            "id": 3,
            "code": "Tallinn",
            "title_et": "Rahvusarhiiv Tallinnas",
            "title_en": "National Archives in Tallinn"
        },
        {
            "id": 7,
            "code": "Rakvere",
            "title_et": "Rahvusarhiiv Rakveres",
            "title_en": "National Archives in Rakvere"
        },
        {
            "id": 9,
            "code": "Valga",
            "title_et": "Rahvusarhiiv Valgas",
            "title_en": "National Archives in Valga"
        }
    ]
}
```

Mitte ühtegi arhiiviüksust ei leitud.

```json
{
    "responseStatus": "ok",
    "unitListView": []
}
```
