---
description: Päringu dokumentatsioon
---

# Riikide sirvimine

## <mark style="color:green;">GET</mark> ra/country/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/country/list?token={{accessToken}}&is_eu={{isEu}}
```
{% endcode %}

Väljastab riikide nimekirja. Väljastatakse kõik riigid, mis on järjestatud tähestikuliselt (ASC) eestikeelse nime (name_et) järgi. Valikuliselt saab filtreerida EL liikmesuse alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="197">NIMI</th><th width="152">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>is_eu</td><td>Integer</td><td><p>EL liikmesuse filter (valikuline)</p><p></p><p>Võimalikud väärtused: <code>0</code> (mitte EL riigid), <code>1</code> (EL riigid), või jäta määramata (kõik riigid)</p></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

Kõik riigid:

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/country/list?token=9c7ac26ae69ba392be82c2315d3c45e3' \
```
{% endcode %}

Ainult EL riigid:

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/country/list?token=9c7ac26ae69ba392be82c2315d3c45e3&is_eu=1' \
```
{% endcode %}

### Vastuse näide

Riikide nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "countryListView": [
        {
            "id": 1,
            "name_et": "Eesti",
            "name_en": "Estonia",
            "short_name": "Eesti",
            "code_number": "233",
            "code": "EST",
            "code2": "EE",
            "latitude": "58.595272",
            "longitude": "25.013607",
            "is_eu": true
        },
        {
            "id": 2,
            "name_et": "Läti",
            "name_en": "Latvia",
            "short_name": "Läti",
            "code_number": "428",
            "code": "LVA",
            "code2": "LV",
            "latitude": "56.879635",
            "longitude": "24.603189",
            "is_eu": true
        },
        {
            "id": 3,
            "name_et": "Leedu",
            "name_en": "Lithuania",
            "short_name": "Leedu",
            "code_number": "440",
            "code": "LTU",
            "code2": "LT",
            "latitude": "55.169438",
            "longitude": "23.881275",
            "is_eu": true
        }
    ]
}
```

Mitte ühtegi riiki ei leitud (näiteks kui is_eu väärtus on vigane).

```json
{
    "responseStatus": "ok",
    "countryListView": []
}
```

### Postman test

```javascript
pm.test("Schema is valid", () => {
    const schema = {
        "type": "object",
        "properties": {
            "responseStatus": { "type": "string" },
            "countryListView": {
                "type": "array",
                "items": {
                    "properties": {
                        "id": { "type": "integer" },
                        "name_et": { "type": "string" },
                        "name_en": { "type": "string" },
                        "short_name": { "type": "string" },
                        "code_number": { "type": "string" },
                        "code": { "type": "string" },
                        "code2": { "type": "string" },
                        "latitude": { "type": "string" },
                        "longitude": { "type": "string" },
                        "is_eu": { "type": "boolean" }
                    },
                    "required": [
                        "id",
                        "name_et",
                        "name_en",
                        "short_name",
                        "code_number",
                        "code",
                        "code2",
                        "latitude",
                        "longitude",
                        "is_eu"
                    ]
                }                   
            }                                
        },                
        "required": ["responseStatus", "countryListView"]
    };    
    pm.response.to.have.jsonSchema(schema);
});
```
