---
description: Päringu dokumentatsioon
---

# Säiliku värskendamine

## <mark style="color:blue;">PUT</mark> ra/item/refresh

```

{{apiBaseUrl}}/ra/item/refresh?token={{accessToken}}&refcode={{itemRefcode}}
```

Märgib VAU andmebaasi, et säiliku andmeid on vaja uuendada, kuna neid on AIS-is muudetud.&#x20;

Alati, kui AIS-is muudetakse säiliku pealkirja, hoidlat, riiulit, kappi või lauda, peab AIS saatma VAU-le selle lihtsa PUT-päringu. Päringu käigus pannakse säiliku leidandmete järgi VAU-s säiliku tabelis välja refresh\_required väärtuseks TRUE.

VAU-s töötab eraldiseisev cron-töö, mis iga minuti järel kontrollib kõiki lipuga märgitud kirjeid, võtab AIS-ist uued andmed ja ajakohastab oma andmebaasi, seejärel eemaldab märgistuslipu.&#x20;

Nii on vastutused selgelt jaotatud: API teeb ainult ühe konkreetse muudatuse – seab säilikule lipu, et andmed vajavad värskendamist – ja kõik keerulisem (andmete uuendamine, vea­käsitlus jne) jääb cron-töö kanda.

See lähenemine muudab süsteemi vastupidavamaks: kui uuendamisel tekib mõni viga, saab järgmine cron-jooks tööd katkestatud kohast jätkata. Samuti aitab see vältida olukordi, kus mitmed järjestikused muudatused tekitaksid ülekoormuse. Lisaks väldime üleliigset andmesidet. Kuna VAU-s ei ole kõiki AIS-is olemasolevaid säilikuid, poleks alati kõigi andmete saatmine põhjendatud. Lahendus on ka hästi skaleeritav.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="116">NIMI</th><th width="94">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>refcode *</td><td>String</td><td>Säiliku leidandmed AIS-is</td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell


curl --location --request PUT 'https://www.ra.ee/vau/index.php/api/ra/item/refresh?token=db9a1afb27d892ad3303095ce580f9cc&refcode=ERA.1356.3.2061'
```
{% endcode %}

### Vastuse näide

Säiliku andmete värskendamise vajaduse märkimine õnnestub.

```json
{
    "responseStatus": "ok"
}
```

### Veateated

**error 10010** - säiliku andmete värskendamise vajaduse märkimine ebaõnnestub (määratlemata tehnilistel põhjustel)

```json
{
    "responseStatus": "error",
    "errorCode": 10010,
    "errorMessage": "Could not update item"
}
```

**error 10011** - leidandmed puuduvad

```json
{
    "responseStatus": "error",
    "errorCode": 10011,
    "errorMessage": "Refcode parameter is missing"
}
```

**error 10012** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 10012,
    "errorMessage": "Is not PUT request"
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".&#x20;
{% endhint %}
