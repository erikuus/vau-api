---
description: Päringu dokumentatsioon
---

# Taotluse loomine

## <mark style="color:orange;">POST</mark> ska/application/create

```
{{apiBaseUrl}}/ska/application/create?token={{accessToken}}
```

Loob uue taotluse ja tagastab selle identifikaatori.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr></tbody></table>

### Sisend (body raw json)

JSON peab sisaldama vähemalt taotluse objekti `Application`:

```json
{
    "Application": {}
}
```

Kui taotlusele soovitakse lisada üks või mitu õppeastust ja/või töökohta, siis peab JSON sisaldama ka `Study` ja/või `Work` objekte:&#x20;

```json
{
    "Application": {},
    "Study": [{},{}],
    "Work": [{},{}]    
}
```

#### Application

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>applicant_firstname *</td><td>String (64)</td><td>Taotleja eesnimi</td><td></td></tr><tr><td>applicant_lastname *</td><td>String (64)</td><td>Taotleja perekonnanimi</td><td></td></tr><tr><td>applicant_birthday *</td><td>Date</td><td>Taotleja sünnikuupäev<br><br><em>NB! Lubatud formaat on</em> <code>dd.MM.yyyy</code></td><td></td></tr><tr><td>applicant_address *</td><td>String (256)</td><td>Taotleja aadress</td><td></td></tr><tr><td>applicant_zip *</td><td>String (16)</td><td>Taotleja aadressi postiindeks</td><td></td></tr><tr><td>applicant_phone</td><td>String (64)</td><td>Taotleja telefoninumber</td><td></td></tr><tr><td>applicant_email</td><td>String (256)</td><td>Taotleja e-posti aadress</td><td></td></tr><tr><td>applicant_id_nr</td><td>String(11)</td><td>Taotleja isikukood<br><br><em>NB! Veebirakenduse sisestusvormis isikukoodi ei ole, mistõttu seda pole ka seniste taotluste juures. Kuna Rahvusarhiivil on palju ka välismaiseid kliente, moodustatakse kliendikood nimest ja sünnikuupäevast. Isikukood on lisatud spetsiaalselt API jaoks ja seda saab kasutada otsingus.</em></td><td></td></tr><tr><td>applicant_names_info</td><td>String</td><td>Taotleja nimemuutused ja erinevad nimekujud õppimise/töötamise ajal</td><td></td></tr><tr><td>applicant_department_id</td><td>Integer</td><td>Üksuse identifikaator, juhul kui teatise tellijaks ja riigilõivu tasujaks ei ole isik, vaid üksus</td><td></td></tr><tr><td>study_comments</td><td>String</td><td>Märkused, täiendused õppimise kohta<br><br><em>NB! Selle välja väärtus salvestatakse ainult siis, kui on määratud vähemalt üks õppeasutus, st</em> <code>JSON</code><em>-is on vähemalt üks</em> <code>Study</code> <em>objekt.</em>  </td><td></td></tr><tr><td>work_pension_info</td><td>String</td><td>Õigus sooduspensionile, vajalike tingimuste kirjeldus<br><br><em>NB! Selle välja väärtus salvestatakse ainult siis, kui on määratud vähemalt üks töökoht, st</em> <code>JSON</code><em>-is on vähemalt üks</em> <code>Work</code> <em>objekt.</em></td><td></td></tr><tr><td>work_comments</td><td>String</td><td>Märkused, täiendused töötamise kohta<br><br><em>NB! Selle välja väärtus salvestatakse ainult siis, kui on määratud vähemalt üks töökoht, st</em> <code>JSON</code><em>-is on vähemalt üks</em> <code>Work</code> <em>objekt.</em></td><td></td></tr><tr><td>farm_info</td><td>String</td><td>Talus töötamine: maakond, vald, talu nimi, aeg</td><td></td></tr><tr><td>military_info</td><td>String</td><td>Sõjaväeteenistus: Eesti Kaitseväes teenimise puhul väeosa ja teenimise aeg, Saksa sõjaväes teenimise puhul kõik teadaolevad andmed</td><td></td></tr><tr><td>rear_info</td><td>String</td><td>Viibimine nõukogude tagalas: kellega koos tagalasse saadeti (andmed vanemate kohta) ja kõik muud teadaolevad andmed</td><td></td></tr><tr><td>prison_info</td><td>String</td><td>Vangilaagris ja asumisel viibimine: kellega koos laagrisse/asumisele saadeti (andmed vanemate kohta), millal ja kelle poolt karistatud, karistuse kandmise aeg ja koht, vabanemise aeg</td><td></td></tr><tr><td>work_camp_info</td><td>String</td><td>Töölaagris, koonduslaagris või sõjavangilaagris viibimine: laagri nimetus, kinnipidamise ja vabastamise aeg</td><td></td></tr><tr><td>ww2_estonia_info</td><td>String</td><td>II maailmasõja ajal Eestisse toomine: kellega koos toodi (andmed vanemate kohta), toomise aeg ja koht, laagrite nimed ja kinnipidamisaeg, kuhu suunati elama ja tööle</td><td></td></tr><tr><td>ww2_germany_info</td><td>String</td><td>II maailmasõja ajal Saksamaale saatmine: kellega koos saadeti (andmed vanemate kohta), kust ja millal saadeti, laagrite nimed, töökohad Saksamaal, Eestisse naasmise aeg ja koht</td><td></td></tr><tr><td>other_comments</td><td>String</td><td>Muud märkused ja täiendused taotluse kohta</td><td></td></tr><tr><td>taxnotice_delivery_method *</td><td>String</td><td>Valik: kas taotleja soovib arhiivilt teadet riigilõivu tasumise kohta tavapostiga või e-postiga<br><br><em>NB! Lubatud väärtused on:</em><br><em></em><code>DELIVERY_POSTAL</code> <em>või</em> <code>DELIVERY_EMAIL</code></td><td></td></tr><tr><td>copy_delivery_method</td><td>String</td><td>Valik: kas taotleja soovib koopiat arhiiviteatisest tavapostiga või e-postiga<br><br><em>NB! Lubatud väärtused on:</em><br><em></em><code>DELIVERY_POSTAL</code> <em>või</em> <code>DELIVERY_EMAIL</code></td><td></td></tr><tr><td>employee_id</td><td>Integer</td><td>Sotsiaalkindlustusameti töötaja, kes taotluse koostas/sisestas<br><br><em>NB! Töötaja identifikaatori saamise kohta vaata</em> <a data-mention href="../toeoetaja/toeoetaja-loomine.md">toeoetaja-loomine.md</a> <em>ja</em> <a data-mention href="../toeoetaja/toeoetaja-leidmine.md">toeoetaja-leidmine.md</a><em></em></td><td></td></tr><tr><td>department_id</td><td>Integer</td><td>Sotsiaalkindlustusameti üksus, kuhu arhiiviteatis edastatakse<br><br><em>NB! Üksuse identifikaatori saamise kohta vaata</em> <a data-mention href="../ueksus/ueksuse-loomine.md">ueksuse-loomine.md</a><em>ja</em> <a data-mention href="../ueksus/ueksuse-leidmine.md">ueksuse-leidmine.md</a><em></em></td><td></td></tr></tbody></table>

#### Study

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>institution *</td><td>String (512)</td><td>Õppeasutuse nimetus</td><td></td></tr><tr><td>period *</td><td>String (512)</td><td>Õppimise aeg (kuupäevaliselt)</td><td></td></tr><tr><td>specialty</td><td>String (512)</td><td>Eriala</td><td></td></tr></tbody></table>

#### Work

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP (PIKKUS)</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>institution *</td><td>String (512)</td><td>Asutuse nimetus</td><td></td></tr><tr><td>period *</td><td>String (512)</td><td>Töötamise aeg (kuupäevaliselt)</td><td></td></tr><tr><td>specialty *</td><td>String (512)</td><td>Eriala</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

```shell
curl --location --request POST 'https://www.ra.ee/vau/index.php/api/ska/application/create?token=db9a1afb27d892ad3303095ce580f9cc' \
--header 'Content-Type: application/json' \
--data-raw '{
    "Application": {
        "applicant_firstname": "Erik",
        "applicant_lastname": "Uus",
        "applicant_birthday": "30.07.1973",
        "applicant_address": "Tammsaare 8-25",
        "applicant_id_nr": "37307302715",
        "applicant_zip": "51006",
        "applicant_phone": "+37253225388",
        "applicant_email": "erik.uus@gmail.com",
        "applicant_names_info": "Uks, Uss",
        "applicant_department_id": null,
        "study_comments": "Märkused, täiendused",
        "work_pension_info": "Õigus sooduspensionile, vajalike tingimuste kirjeldus",
        "work_comments": "Märkused, täiendused",
        "farm_info": "Maakond, vald, talu nimi, aeg",
        "military_info": "Kirjeldus; Eesti Kaitseväes teenimise puhul märkida väeosa ja teenimise aeg, Saksa sõjaväes teenimise puhul kõik teadaolevad andmed",
        "rear_info": "Kirjeldus; kellega koos tagalasse saadeti (andmed vanemate kohta) ja märkida kõik teadaolevad andmed",
        "prison_info": "Kirjeldus; kellega koos laagrisse/asumisele saadeti (andmed vanemate kohta), millal ja kelle poolt karistatud, karistuse kandmise aeg ja koht, vabanemise aeg",
        "work_camp_info": "Laagri nimetus, kinnipidamise ja vabastamise aeg",
        "ww2_estonia_info": "Kirjeldus; kellega koos toodi (andmed vanemate kohta), toomise aeg ja koht, laagrite nimed ja kinnipidamisaeg, kuhu suunati elama ja tööle",
        "ww2_germany_info": "Kirjeldus; kellega koos saadeti (andmed vanemate kohta), kust ja millal saadeti, laagrite nimed, töökohad Saksamaal, Eestisse naasmise aeg ja koht",
        "other_comments": "Märkused, täiendused",
        "taxnotice_delivery_method": "DELIVERY_EMAIL",
        "copy_delivery_method": "DELIVERY_EMAIL",
        "employee_id": null,
        "department_id": null
    },
    "Study": [
        {
            "institution": "Nõo Keskkool",
            "period": "1980 - 1991",
            "specialty": ""
        },
        {
            "institution": "Tartu Ülikool",
            "period": "1991 - 1995",
            "specialty": "usuteadus"
        }
    ],
    "Work": [
        {
            "institution": "Rahvusarhiiv",
            "period": "2006 - 2022",
            "specialty": "programmeerija"
        },
        {
            "institution": "Babahh OÜ",
            "period": "2014 - 2018",
            "specialty": "programmeerija"
        }
    ]
}'
```

### Vastuse näide

Taotluse loomine õnnestub ja tagastatakse loodud taotluse identifikaator.

```json
{
    "responseStatus": "ok",
    "applicationId": 16610
}
```

### Veateated

**error 3050** - taotlust ei saa luua, kuna sisendväärtused ei valideeru&#x20;

```json
{
    "responseStatus": "error",
    "errorCode": 3050,
    "errorMessage": "Could not create application",
    "errors": [
        {
            "applicant_firstname": [
                "Eesnimi ei tohi olla tühi."
            ],
            "taxnotice_delivery_method": [
                "Mittelubatud väärtus."
            ],
            "employee_id": [
                "Töötaja peab olema arv."
            ],
            "department_id": [
                "Üksus \"0\" ei eksisteeri."
            ]
        }
    ]
}
```

**error 3051** - päringu _raw body_ ei sisalda _JSON_ _stringi_ või selles puudub _Application_ objekt

```json
{
    "responseStatus": "error",
    "errorCode": 3051,
    "errorMessage": "Request body is invalid or empty"
}
```

**error 3052** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 3052,
    "errorMessage": "Is not POST request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 __ OK".&#x20;
{% endhint %}
