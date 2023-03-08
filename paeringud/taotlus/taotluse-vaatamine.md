---
description: Päringu dokumentatsioon
---

# Taotluse vaatamine

## <mark style="color:green;">GET</mark> ska/application/view

```
{{apiBaseUrl}}/ska/application/view?token={{accessToken}}&id={{applicationId}}
```

Väljastab taotluse andmed identifikaatori alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Taotluse identifikaator<br><br><em>NB! Taotluse identifikaatori saamise kohta vaata</em> <a data-mention href="taotluse-loomine.md">taotluse-loomine.md</a><em></em></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/application/view?token=db9a1afb27d892ad3303095ce580f9cc&id=16610'
```
{% endcode %}

### Vastuse näide

Taotluse andmete väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "applicationDetailView": {
        "Taotluse esitaja andmed": {
            "Eesnimi": "Erik",
            "Perekonnanimi": "Uus",
            "Isikukood": "37307302715",
            "Sünnikuupäev": "30.07.1973",
            "Aadress": "Tammsaare 8-25",
            "Postiindeks": "51006",
            "Telefon või mobiiltelefon": "+37253225388",
            "E-posti aadress": "erik.uus@gmail.com",
            "Nimemuutused ja erinevad nimekujud õppimise/töötamise ajal": "Uks, Uss",
            "Teatise tellijaks ja riigilõivu tasujaks ei ole isik, vaid": "Test osakond"
        },
        "Taotluse sisu": {
            "Õppimine": {
                "Õppeasutused": [
                    {
                        "Õppeasutuse nimetus": "Nõo Keskkool",
                        "Õppimise aeg (kuupäevaliselt)": "1980 - 1991",
                        "Eriala": null
                    },
                    {
                        "Õppeasutuse nimetus": "Tartu Ülikool",
                        "Õppimise aeg (kuupäevaliselt)": "1991 - 1995",
                        "Eriala": "usuteadus"
                    }
                ],
                "Märkused, täiendused": "Märkused, täiendused"
            },
            "Töötamine": {
                "Asutused": [
                    {
                        "Asutuse nimetus": "Rahvusarhiiv",
                        "Töötamise aeg (kuupäevaliselt)": "2006 - 2022",
                        "Eriala": "programmeerija"
                    },
                    {
                        "Asutuse nimetus": "Babahh OÜ",
                        "Töötamise aeg (kuupäevaliselt)": "2014 - 2018",
                        "Eriala": "programmeerija"
                    }
                ],
                "Õigus sooduspensionile, vajalike tingimuste kirjeldus": "Õigus sooduspensionile, vajalike tingimuste kirjeldus",
                "Märkused, täiendused": "Märkused, täiendused"
            },
            "Talus töötamine": {
                "Maakond, vald, talu nimi, aeg": "Maakond, vald, talu nimi, aeg"
            },
            "Sõjaväeteenistus": {
                "Kirjeldus; Eesti Kaitseväes teenimise puhul märkida väeosa ja teenimise aeg, Saksa sõjaväes teenimise puhul kõik teadaolevad andmed": "Kirjeldus; Eesti Kaitseväes teenimise puhul märkida väeosa ja teenimise aeg, Saksa sõjaväes teenimise puhul kõik teadaolevad andmed"
            },
            "Viibimine nõukogude tagalas": {
                "Kirjeldus; kellega koos tagalasse saadeti (andmed vanemate kohta) ja märkida kõik teadaolevad andmed": "Kirjeldus; kellega koos tagalasse saadeti (andmed vanemate kohta) ja märkida kõik teadaolevad andmed"
            },
            "Vangilaagris ja asumisel viibimine": {
                "Kirjeldus; kellega koos laagrisse/asumisele saadeti (andmed vanemate kohta), millal ja kelle poolt karistatud, karistuse kandmise aeg ja koht, vabanemise aeg": "Kirjeldus; kellega koos laagrisse/asumisele saadeti (andmed vanemate kohta), millal ja kelle poolt karistatud, karistuse kandmise aeg ja koht, vabanemise aeg"
            },
            "Töölaagris, koonduslaagris või sõjavangilaagris viibimine": {
                "Laagri nimetus, kinnipidamise ja vabastamise aeg": "Laagri nimetus, kinnipidamise ja vabastamise aeg"
            },
            "II maailmasõja ajal Eestisse toomine": {
                "Kirjeldus; kellega koos toodi (andmed vanemate kohta), toomise aeg ja koht, laagrite nimed ja kinnipidamisaeg, kuhu suunati elama ja tööle": "Kirjeldus; kellega koos toodi (andmed vanemate kohta), toomise aeg ja koht, laagrite nimed ja kinnipidamisaeg, kuhu suunati elama ja tööle"
            },
            "II maailmasõja ajal Saksamaale saatmine": {
                "Kirjeldus; kellega koos saadeti (andmed vanemate kohta), kust ja millal saadeti, laagrite nimed, töökohad Saksamaal, Eestisse naasmise aeg ja koht": "Kirjeldus; kellega koos saadeti (andmed vanemate kohta), kust ja millal saadeti, laagrite nimed, töökohad Saksamaal, Eestisse naasmise aeg ja koht"
            },
            "Muud märkused, täiendused": "Märkused, täiendused"
        },
        "Taotlusega seotud failid": [
            {
                "url": "https://www.ra.ee/eteatis/index.php/file/download?code=yD0FmubzIzi8BAj8",
                "filename": "test.jpg",
                "filesize": "11 KB",
                "creator": "Erik Uus",
                "modified": "18.08.2022 15:27"
            }
        ],
        "Taotluse esitaja soovid ja eelistused": {
            "Soovin arhiivilt teadet riigilõivu tasumise kohta": "E-postiga",
            "Soovin koopiat arhiiviteatisest": "E-postiga"
        },
        "Üksus, kuhu arhiiviteatis edastatakse": {
            "Nimi": "Test osakond",
            "Aadress": "Tammsaare 8-25, Tartu",
            "E-post": "erik.uus@ra.ee",
            "Telefon": "+372 5322 5388"
        },
        "Vormi täitnud töötaja andmed": {
            "Eesnimi": "Erik",
            "Perekonnanimi": "Uus",
            "Telefon": "+372 5322 5388"
        },
        "Taotluse andmed": {
            "Koostatud": "17.08.2022 13:04",
            "Saadetud": "18.08.2022 10:12"
        }
    }
}
```

{% hint style="info" %}
Taotluse andmed väljastatakse eestikeelsete väljanimedega, nii et neid on võimalik kasutajaliideses vahetult kuvada.
{% endhint %}

{% hint style="info" %}
Pane tähele, et ülaltoodud näites on mitmete väljade väärtuseks pandud väljade nimed. Seda on tehtud ainult seepärast, et näite koostamine oleks lihtsam. Samal põhjusel on dokumentatsiooni autor märkinud nii taotleja kui töötaja andmeteks oma isikuandmed.
{% endhint %}

### Veateade

**error 3010** - taotlust ei leitud (määratud identifikaatoriga taotlust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 3010,
    "errorMessage": "The requested application does not exist"
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
