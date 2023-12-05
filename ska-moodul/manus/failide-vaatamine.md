---
description: Päringu dokumentatsioon
---

# Failide vaatamine

## <mark style="color:green;">GET</mark> ska/file/list

{% code overflow="wrap" %}
```
{{apiBaseUrl}}/ska/file/list?token={{accessToken}}&application_id={{applicationId}}
```
{% endcode %}

Väljastab taotluse identifikaatori järgi sellele taotlusele lisatud failide nimekirja. Failid on järjestatud failinime järgi kasvavalt (ASC).

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th width="168">NIMI</th><th width="107">TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>application_id</td><td>Integer</td><td>Taotluse identifikaator, mille faile vaadatakse<br><br><em>NB! Taotluse identifikaatori saamise kohta vaata</em> <a data-mention href="../taotlus/taotluse-loomine.md">taotluse-loomine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/file/list?token=fad056fddce1abf150f33d49a5653969&application_id=16610' \
```
{% endcode %}

### Vastuse näide

Failide nimekirja väljastamine õnnestub.

```json
{
    "responseStatus": "ok",
    "fileListView": [
        {
            "id": 23,
            "url": "https://www.ra.ee/eteatis/index.php/file/download?code=EZSjmi-V0wE2K1v5",
            "filename": "Kukk-paringu-lisa.pdf",
            "filesize": "120 KB",
            "creator": "Ele Keskküla",
            "modified": "02.03.2018 15:48"
        },
        {
            "id": 24,
            "url": "https://www.ra.ee/eteatis/index.php/file/download?code=qpFWHN103uyKvuZ4",
            "filename": "Kukk-sunnitunnistus.pdf",
            "filesize": "312 KB",
            "creator": "Ele Keskküla",
            "modified": "02.03.2018 15:48"
        }
    ]
}
```

Mitte ühtegi faili ei leitud.

```json
{
    "responseStatus": "ok",
    "fileListView": []
}
```

### Veateade

**error 6010** - taotlust ei leitud (määratud identifikaatoriga taotlust andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 6010,
    "errorMessage": "The requested application does not exist"
}
```
