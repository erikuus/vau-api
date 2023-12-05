---
description: Päringu dokumentatsioon
---

# Klassifikaatorite sirvimine

## <mark style="color:green;">GET</mark> ra/lookup/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/lookup/list?token={{accessToken}}&type={{lookupType}}
```
{% endcode %}

Väljastab klassifikaatorite nimekirja tüübi alusel. Väljastatakse kõik määratud tüüpi klassifikaatorid. Klassifikaatorid on järjestatud kasvavalt (ASC) järjekorranumbri (position) järgi, mille on määranud VAU haldurid.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="197">NIMI</th><th width="152">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>type *</td><td>String </td><td><p>Klassifikaatori tüüp </p><p></p><p>Võimalikud väärtused on: <code>purpose</code> või <code>measure_unit</code></p></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/lookup/list?token=9c7ac26ae69ba392be82c2315d3c45e3&type=purpose' \
```
{% endcode %}

### Vastuse näide

Klassifikaatorite nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "lookupListView": [
        {
            "code": 1,
            "name_et": "Teadustöö",
            "name_en": "Scientific research",
            "position": 1
        },
        {
            "code": 2,
            "name_et": "Kodu-uurimine",
            "name_en": "Local history research",
            "position": 2
        },
        {
            "code": 3,
            "name_et": "Genealoogia",
            "name_en": "Genealogical research",
            "position": 3
        },
        {
            "code": 4,
            "name_et": "Õppetöö",
            "name_en": "Studies",
            "position": 4
        },
        {
            "code": 5,
            "name_et": "Õiguste tõestamine",
            "name_en": "Legal issues",
            "position": 5
        },
        {
            "code": 6,
            "name_et": "Muu",
            "name_en": "Other",
            "position": 6
        },
        {
            "code": 7,
            "name_et": "Genealoogia/Kodu-uurimine",
            "name_en": "Genealogical research/Local history research",
            "position": 7
        },
        {
            "code": 8,
            "name_et": "Teadustöö/Kodu-uurimine",
            "name_en": "Scientific research/Local history research",
            "position": 8
        }
    ]
}
```

Mitte ühtegi klassifikaatorit ei leitud (näiteks kui tüüp on valesti määratud).

```json
{
    "responseStatus": "ok",
    "lookupListView": []
}
```
