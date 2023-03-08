---
description: Päringu dokumentatsioon
---

# Taotluse oleku vaatamine

## <mark style="color:green;">GET</mark> ska/application/status

```
{{apiBaseUrl}}/ska/application/status?token={{accessToken}}&id={{applicationId}}
```

Väljastab taotluse identifikaatori alusel info selle kohta, millises olekus on taotluse menetlemine Rahvusarhiivis.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Taotluse identifikaator<br><br><em>NB! Taotluse identifikaatori saamise kohta vaata</em> <a data-mention href="taotluse-loomine.md">taotluse-loomine.md</a><em></em></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/application/status?token=db9a1afb27d892ad3303095ce580f9cc&id=16610'
```
{% endcode %}

### Vastuse näide

Taotluse menetlemise oleku väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "applicationStatus": {
        "code": "REJECTED",
        "text": "Tagasilükatud",
        "htmlMessage": "<p>Rahvusarhiivil ei ole võimalik päringule vastata, kuna vastavaid dokumente ei ole Rahvusarhiivile üle antud. Soovitame pöörduda Tallinna Tööstushariduskeskuse poole (info@tthk.ee).</p>"
    }
}
```

Taotlus võib olla järgmistes olekutes:

<table><thead><tr><th>CODE</th><th>TEXT</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>DRAFT</td><td>Koostamisel</td><td>Taotlus on salvestatud, aga Rahvusarhiivi saatmata. Seda saab veel muuta ja sellele saab lisada manusena faile.</td><td></td></tr><tr><td>SUBMITTED</td><td>Saabunud</td><td>Taotlus on saadetud Rahvusarhiivi. See on saabunud Rahvusarhiivi arhiivipäringute haldamise moodulisse, aga seda ei ole seal veel menetlema hakatad. Taotlust ei saa enam muuta ega kustutada ja sellele ei saa lisada faile.</td><td></td></tr><tr><td>REJECTED</td><td>Tagasilükatud</td><td>Rahvusarhiivil ei ole võimalik arhiiviteatist väljastada. Taotluse menetlemine Rahvusarhiivis on lõpetatud.<br><br><em>NB! Selle oleku puhul on</em> <code>htmlMessage</code> <em>väli päringu vastuses täidetud.</em></td><td></td></tr><tr><td>FORWARDED</td><td>Edastatud</td><td>Taotlus on edastatud Tallinna Linnaarhiivi, kuna Rahvusarhiivil puuduvad dokumendid, mille alusel saaks koostada arhiiviteatise. Taotluse menetlemine Rahvusarhiivis on lõpetatud.</td><td></td></tr><tr><td>ASSIGNED_UNIT</td><td>Määratud</td><td>Rahvusarhiiv on hinnanud, et saab taotluse töösse võtta, ja on esimese sammuna määranud üksuse, kelle ülesandeks on seda taotlust menetleda.</td><td></td></tr><tr><td>WAITING_PAYMENT</td><td>Makse ootel</td><td>Taotlejale on saadetud makseteade arhiiviteatise eest riigilõivu tasumiseks, aga makset ei ole veel laekunud, mistõttu arhiiviteatist ei ole hakatud veel koostama.</td><td></td></tr><tr><td>CANCELED</td><td>Tühistatud</td><td>Taotlus on tühistatud. Taotluse menetlemine Rahvusarhiivis on lõpetatud.<br><br><em>NB! Põhjused võivad olla erinevad. Näiteks võib taotleja leida üles dokumendi, mida ta arvas mitte omavat.</em></td><td></td></tr><tr><td>OUTDATED</td><td>Aegunud</td><td>Kui taotlus on olnud makse ootel 14 päeva, saadetakse taotlejale esimene meeldetuletus. Kui taotlus on olnud makse ootel 28 päeva, saadetakse taotlejale teine meeldetuletus. Kui taotlus on olnud makse ootel 42 päeva, märgitakse see aegunuks. Makselink, mis saadeti taotlejale e-kirjaga, enam ei toimi, aga kui makse laekub eraldi pangaülekandega, võetakse taotlus uuesti töösse.</td><td></td></tr><tr><td>PAID</td><td>Makstud</td><td>Taotleja on tasunud riigilõivu. Taotlus ootab töösse võtmist ehk arhivaarile edastamist.</td><td></td></tr><tr><td>BEING_PROCESSED</td><td>Töösse võetud</td><td>Taotlus on edastatud arhivaarile, kes koostab sellele vastuseks arhiiviteatise.</td><td></td></tr><tr><td>READY</td><td>Valmis</td><td>Arhiiviteatis on valmis.<br><br><em>NB! Kui taotlus on selles olekus, saab kasutada päringut</em> <a data-mention href="taotluse-vastuse-vaatamine.md">taotluse-vastuse-vaatamine.md</a></td><td></td></tr><tr><td>COMPLETED</td><td>Lõpetatud</td><td>Sotsiaalkindlustusameti osakonnale on saadetud e-kiri, mis sisaldab e-arhiiviteatise allalaadimise linki. Taotluse menetlemine Rahvusarhiivis on lõpetatud.<br><br><em>NB! Kui taotlus on selles olekus, saab kasutada päringut</em> <a data-mention href="taotluse-vastuse-vaatamine.md">taotluse-vastuse-vaatamine.md</a></td><td></td></tr></tbody></table>

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
