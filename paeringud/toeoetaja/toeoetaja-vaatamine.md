---
description: Päringu dokumentatsioon
---

# Töötaja vaatamine

## <mark style="color:green;">GET</mark> ska/employee/view

```
{{apiBaseUrl}}/ska/employee/view?token={{accessToken}}&id={{employeeId}}
```

Väljastab töötaja andmed identifikaatori alusel.

### Parameetrid (query params)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>token *</td><td>String</td><td><a data-mention href="../../juurdepaeaesukood.md">juurdepaeaesukood.md</a></td><td></td></tr><tr><td>id *</td><td>Integer</td><td>Töötaja identifikaator<br><br><em>NB! Töötaja identifikaatori saamise kohta vaata</em> <a data-mention href="toeoetaja-loomine.md">toeoetaja-loomine.md</a> <em>ja</em> <a data-mention href="toeoetaja-leidmine.md">toeoetaja-leidmine.md</a></td><td></td></tr></tbody></table>

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request GET 'https://www.ra.ee/vau/index.php/api/ska/employee/view?token=ea2397458ba644c6fd2d70b05adb6661&id=301'
```
{% endcode %}

### Vastuse näide

Töötaja andmete väljastamine õnnestub.&#x20;

```json
{
    "responseStatus": "ok",
    "employeeDetailView": {
        "Eesnimi": "Erik",
        "Perekonnanimi": "Uus",
        "E-post": "erik.uus@ra.ee",
        "Telefon": "+372 5322 5388",
        "Üksus": "Test osakond"
    }
}
```

{% hint style="info" %}
Töötaja andmed väljastatakse eestikeelsete väljanimedega, nii et neid on võimalik kasutajaliideses vahetult kuvada.
{% endhint %}

### Veateade

**error 5010** - töötajat ei leitud (määratud identifikaatoriga töötajat andmebaasis ei ole)

```json
{
    "responseStatus": "error",
    "errorCode": 5010,
    "errorMessage": "The requested employee does not exist."
}
```

{% hint style="info" %}
Pane tähele, et selles näites "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 OK".
{% endhint %}
