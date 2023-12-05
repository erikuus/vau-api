---
description: Päringu dokumentatsioon
---

# Taotluse vastuse vaatamine

## <mark style="color:green;">GET</mark> ska/application/result

<pre><code><strong>{{apiBaseUrl}}/ska/application/result?token={{accessToken}}&#x26;id={{applicationId}}
</strong></code></pre>

Väljastab e-arhiiviteatise (digitaalselt allkirjastatud faili andmed ja allalaadimise lingi), mille Rahvusarhiivi arhivaar koostas talle saadetud taotluse alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="134">NIMI</th><th width="112">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Taotluse identifikaator<br><br><em>NB! Taotluse identifikaatori saamise kohta vaata</em> <a data-mention href="taotluse-loomine.md">taotluse-loomine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/application/result?token=846a0a7bc2be5e66cba566b0fcaeac3f&id=16610'
```
{% endcode %}

### Vastuse näide

E-arhiiviteatise (digitaalselt allkirjastatud faili andmed ja allalaadimise lingi) väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "resultFiles": [
        {
            "url": "https://www.ra.ee/vautest/upload/enquiry/2022/08/00c95808-20a2-4986-5a7f-066cb87c6bb1/erik-uus-eteatis.asice",
            "filename": "erik-uus-eteatis.asice",
            "filesize": "199 KB",
            "creator": "Erik Uus",
            "modified": "18.08.2022 11:42"
        }
    ]
}
```

Mitte ühtegi e-arhiiviteatist (faili) ei leitud.

```json
{
    "responseStatus": "ok",
    "resultFiles": []
}
```

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
