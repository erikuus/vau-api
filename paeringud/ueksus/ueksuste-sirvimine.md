---
description: Päringu dokumentatsioon
---

# Üksuste sirvimine

## <mark style="color:green;">GET</mark> ska/department/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ska/department/list?token={{accessToken}}&name={{searchString}}&address={{searchString}}&zip={{searchString}}&email={{searchString}}&phone={{searchString}}
```
{% endcode %}

Väljastab üksuste nimekirja otsiparameetrite alusel, mida võib, aga ei pea kasutama. Maksimaalselt väljastatakse 100 üksuse andmed. Üksused on järjestatud nime järgi kasvavalt (ASC).

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>name</td><td>String </td><td>Üksuse nimi (lubatud metamärgid)</td><td></td></tr><tr><td>address</td><td>String </td><td>Üksuse aadress (lubatud metamärgid)</td><td></td></tr><tr><td>zip</td><td>String </td><td>Üksuse postiindeks (lubatud metamärgid)</td><td></td></tr><tr><td>email</td><td>String </td><td>Üksuse e-posti aadress (lubatud metamärgid)</td><td></td></tr><tr><td>phone</td><td>String</td><td>Üksuse telefoninumber (lubatud metamärgid)</td><td></td></tr></tbody></table>

{% hint style="info" %}
Otsingu metamärgid: \* - tähistab mistahes hulka märke; ? - tähistab ühte märki. Näiteks: otsing "eri\*" leiab "Eri", "Erik", "Erika"; otsing "eri?" leiab eelmainitutest ainult "Erik".
{% endhint %}

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/department/list?token=ea2397458ba644c6fd2d70b05adb6661&name=ska*&address=*tallinn&zip=15092&email=info@*&phone=???? 612 1360' \
```
{% endcode %}

### Vastuse näide

Üksuste nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "departmentListView": [
        {
            "id": 17,
            "Nimi": "SKA Menetlustalitus",
            "Aadress": "Paldiski mnt 80, Tallinn",
            "Postiindeks": "15092",
            "E-post": "info@sotsiaalkindlustusamet.ee",
            "Telefon": "+372 612 1360"
        },
        {
            "id": 16,
            "Nimi": "SKA Teabehalduse osakond",
            "Aadress": "Paldiski mnt 80, Tallinn",
            "Postiindeks": "15092",
            "E-post": "info@sotsiaalkindlustusamet.ee",
            "Telefon": "+372 612 1360"
        }
    ]
}
```

{% hint style="info" %}
Üksuste andmed väljastatakse eestikeelsete väljanimedega, nii et neid on võimalik kasutajaliideses vahetult kuvada.
{% endhint %}

Mitte ühtegi üksust ei leitud.

```json
{
    "responseStatus": "ok",
    "departmentListView": []
}
```
