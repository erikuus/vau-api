---
description: Päringu dokumentatsioon
---

# Töötajate sirvimine

## <mark style="color:green;">GET</mark> ska/employee/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ska/employee/list?token={{accessToken}}&firstname={{searchString}}&lastname={{searchString}}&email={{searchString}}&phone={{searchString}}&department_id={{departmentId}}
```
{% endcode %}

Väljastab töötajate nimekirja otsiparameetrite alusel, mida võib, aga ei pea kasutama. Maksimaalselt väljastatakse 100 töötaja andmed. Töötajad on järjestatud perekonnanime järgi kasvavalt (ASC).

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="168">NIMI</th><th width="192">TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>firstname</td><td>String</td><td>Töötaja eesnimi (lubatud metamärgid)</td><td></td></tr><tr><td>lastname</td><td>String</td><td>Töötaja perekonnanimi (lubatud metamärgid)</td><td></td></tr><tr><td>email</td><td>String</td><td>Töötaja e-posti aadress (lubatud metamärgid)</td><td></td></tr><tr><td>phone</td><td>String</td><td>Töötaja telefoninumber (lubatud metamärgid)</td><td></td></tr><tr><td>department_id</td><td>Integer</td><td>Üksuse identifikaator, kuhu töötaja kuulub</td><td></td></tr></tbody></table>

{% hint style="info" %}
Otsingu metamärgid: \* - tähistab mistahes hulka märke; ? - tähistab ühte märki. Näiteks: otsing "eri\*" leiab "Eri", "Erik", "Erika"; otsing "eri?" leiab eelmainitutest ainult "Erik".
{% endhint %}

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/employee/list?token=24aad44bab3b258b06e809cc53e9083e&firstname=Mari*&lastname=?ä???&email=*@sotsiaalkindlustusamet.ee&department_id=17' \
```
{% endcode %}

### Vastuse näide

Töötajate nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "employeeListView": [
        {
            "id": 274,
            "Eesnimi": "Maritana",
            "Perekonnanimi": "Järve",
            "E-post": "Maritana.Jarve@sotsiaalkindlustusamet.ee",
            "Telefon": "6408115",
            "Üksus": "SKA Menetlustalitus"
        },
        {
            "id": 154,
            "Eesnimi": "Mari",
            "Perekonnanimi": "Räppo",
            "E-post": "Mari.Rappo@sotsiaalkindlustusamet.ee",
            "Telefon": "640 8101",
            "Üksus": "SKA Menetlustalitus"
        }
    ]
}
```

{% hint style="info" %}
Töötajate andmed väljastatakse eestikeelsete väljanimedega, nii et neid on võimalik kasutajaliideses vahetult kuvada.
{% endhint %}

Mitte ühtegi töötajat ei leitud.

```json
{
    "responseStatus": "ok",
    "employeeListView": []
}
```
