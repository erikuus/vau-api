---
description: Päringu dokumentatsioon
---

# Asutuse vaatamine

## <mark style="color:green;">GET</mark> ra/company/view

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ra/company/view?token={{accessToken}}&id={{companyId}}
```
{% endcode %}

Väljastab asutuse andmed identifikaatori alusel.

VAU-s on kirjeldatud kahte tüüpi asutusi – koostöölepinguga ja garantiikirjaga –, millega saab kliente siduda. Kui klient, kes on seotud mõne asutusega, vormistab tasulise tellimuse (nt säilikutellimuse või arhiivipäringu), peab ta valima, kas tegutseb eraisikuna või asutuse nimel. Asutuse nimel esitatud  tellimusi menetletakse teisiti kui eraisikuna esitatuid.

Koostöölepinguga asutuse nimel esitatud tellimused täidetakse ilma arvet esitamata. Garantiikirjaga asutuse puhul täidetakse tellimused enne arve esitamist – teenuste arvestused jäävad ootele ja vormistatakse hiljem koondarvena.

Kuna mõned asutused soovivad saada osakondade lõikes eraldi koondarveid, võimaldab VAU määrata osakondi eraldi asutustena. Sellisel juhul on üldandmed (registrikood, aadress jm) samad, kuid asutuse nimele lisatakse sulgudes osakonna nimi.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="123">NIMI</th><th width="106">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Asutuse identifikaator</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request 
GET 'https://www.ra.ee/vau/index.php/api/ra/company/view?token=3d1140862f01aa039322ca47c60a15a8&id=10' \
```
{% endcode %}

### Vastuse näide

Asutuse väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "companyDetailView": {
        "id": 10,
        "name": "AS Eesti Meedia",
        "reg_nr": "10184643",
        "address": "Maakri tn 23a, 10145 Tallinn, Eesti",
        "email": "arved@eestimeedia.ee",
        "type": "Garantiikiri",
        "valid_from": "01.09.2017",
        "valid_to": "31.05.2024"
    }
}
```

### Veateade

**error 11010** - asutust ei leitud (määratud identifikaatoriga asutust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 11010,
    "errorMessage": "The requested company does not exist"
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
