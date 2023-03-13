---
description: Kasutaja tuvastamine ja juurdepääsukoodi väljastamine
---

# Kasutaja

## <mark style="color:orange;">POST</mark> user/verify

```
{{apiBaseUrl}}/user/verify
```

Kõigile päringutele tuleb ühe parameetrina lisada juurde ajutiselt kehtiv juurdepääsukood ehk _token_. _Tokeni_ väljastab päring, mis kontrollib kasutajanime ja salasõna järgi, kas kasutaja on olemas.

### Sisend (body form-data)

\*-ga märgitud on kohustuslikud

<table><thead><tr><th>NIMI</th><th>TÜÜP</th><th>SELGITUS</th><th data-hidden></th></tr></thead><tbody><tr><td>username *</td><td>String</td><td>Rahvusarhiivis registreeritud kasutajanimi</td><td></td></tr><tr><td>password *</td><td>String</td><td>Rahvusarhiivis registreeritud salasõna</td><td></td></tr></tbody></table>

Kasutajanime ja salasõna saamise kohta vaata [juurdepaeaesutaotlus.md](../juurdepaeaesutaotlus.md "mention")

### Päringu näide (cUrl)

{% code overflow="wrap" %}
```shell
curl --location --request POST 'https://www.ra.ee/vau/index.php/api/user/verify' \
--form 'username="erik"' \
--form 'password="******"'
```
{% endcode %}

### Vastuse näide

Kasutaja autentimine õnnestub ja väljastatakse ajutine [juurdepaeaesukood.md](../juurdepaeaesukood.md "mention")

```json
{
    "responseStatus": "ok",
    "userId": 3,
    "userFirstname": "Erik",
    "userLastname": "Uus",
    "userEmail": "erik.uus@ra.ee",
    "accessToken": "c7234cb8fd247d668062c55a6b1c4be2",
    "tokenLifetime": 3600,
    "requestUnixTime": 1660032944
}
```

{% hint style="info" %}
Seda tuleb mõista nii, et token "c7234cb8fd247d668062c55a6b1c4be2" kehtib 3600 sekundit alates päringu esitamise hetkest, mille UNIX ajatempel on 1660032944.
{% endhint %}

### Veateated

**error 1010** - vale meetod

```json
{
    "responseStatus": "error",
    "errorCode": 1010,
    "errorMessage": "Is not POST request"
}
```

**error 1011** - kohustuslikud väljad täitmata

```json
{
    "responseStatus": "error",
    "errorCode": 1011,
    "errorMessage": "Could not verify user",
    "errors": {
        "username": [
            "Kasutajanimi ei tohi olla tühi."
        ],
        "password": [
            "Salasõna ei tohi olla tühi."
        ]
    }
}
```

**error 1011** - vale salasõna

```json
{
    "responseStatus": "error",
    "errorCode": 1011,
    "errorMessage": "Could not verify user",
    "errors": {
        "password": [
            "Vale salasõna"
        ]
    }
}
```

{% hint style="info" %}
Pane tähele, et neis näidetes "responseStatus" on "error", aga vastuse "HTTP response status code" on "200 __ OK".&#x20;
{% endhint %}
