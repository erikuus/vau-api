---
description: Mis on API juurdepääsukood? Kuidas seda saada? Kui kaua see kehtib?
---

# Juurdepääsukood

## Mis see on?

Kõigile API päringutele tuleb ühe parameetrina lisada ajutiselt kehtiv juurdepääsukood ehk _access token_. Näiteks:

```
{{apiBaseUrl}}/ska/application/view?token=71e0d98f1ab52c225d655359190b6844&id=16610
```

kus _token_ on _"_&#x37;1e0d98f1ab52c225d655359190b6844".

## Kuidas seda saada?

_Tokeni_ väljastab päring [`user/verify`](kasutaja-tuvastamine.md), mis kontrollib kasutajanime ja salasõna järgi, kas kasutaja on olemas.&#x20;

## Kui kaua see kehtib?

Eelviidatud päringu vastus näitab ka seda, kui kaua token kehtib. Näiteks:

```json
{
    "responseStatus": "ok",
    "userId": 3,
    "userFirstname": "Erik",
    "userLastname": "Uus",
    "userEmail": "erik.uus@ra.ee",
    "accessToken": "71e0d98f1ab52c225d655359190b6844",
    "tokenLifetime": 3600,
    "requestUnixTime": 1660724872
}
```

ütleb, et _token_ "71e0d98f1ab52c225d655359190b6844" kehtib 3600 sekundit alates päringu esitamise hetkest, mille UNIX ajatempel on 1660724872.

## **Veateated**&#x20;

_Tokeni_ kasutamisel päringutes võivad esineda järgmised vead.

**error 2010** - _token_ on aegunud või sellist tokenit andmebaasis ei eksisteeri

```json
{
    "responseStatus": "error",
    "errorCode": 2010,
    "errorMessage": "Access token is invalid or expired"
}
```

{% hint style="info" %}
Sellisel juhul tuleb lihtsalt pärida uus _token._
{% endhint %}

**error 2011** - andmebaasis puudub info selle kohta, millisele kasutajale _token_ kuulub

```json
{
    "responseStatus": "error",
    "errorCode": 2011,
    "errorMessage": "Access token has no user"
}
```

{% hint style="info" %}
See on API viga, mida ideaalis ei tohiks kunagi juhtuda.
{% endhint %}

**error 2012** - _token_ on olemas ja kehtib, aga see kuulub kasutajale, kellel puudub käesoleva API-mooduli kasutusõigus

```json
{
    "responseStatus": "error",
    "errorCode": 2012,
    "errorMessage": "User does not have the proper credential to access this action",
    "userName": "erik"
}
```

{% hint style="info" %}
Sellisel juhul tuleb esitada [juurdepaeaesutaotlus.md](juurdepaeaesutaotlus.md "mention")
{% endhint %}

**error 2013** - päringule ei ole lisatud _tokenit_

```json
{
    "responseStatus": "error",
    "errorCode": 2013,
    "errorMessage": "No access token"
}
```

{% hint style="info" %}
Sellisel juhul tuleb pärida _token_ ja lisada see päringule.
{% endhint %}
