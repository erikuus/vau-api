---
description: Postman kollektsioon via JSON link
---

# Postman

Kui arendaja on [Postman](https://www.postman.com/)-i registreeritud kasutaja, on võimalik jagada temaga kollektsiooni kõigist selle API päringutest. Ligipääsu saamiseks tuleb saata taotlus e-kirjaga aadressil admin.vau@ra.ee

<figure><img src="../.gitbook/assets/api.png" alt=""><figcaption></figcaption></figure>

Kollektsiooni jagamine toimub _Via JSON Link_. Pärast kollektsioonile ligipääsu saamist tuleb luua n-ö keskkond.

<figure><img src="../.gitbook/assets/api-enviroment.png" alt=""><figcaption></figcaption></figure>

Muutujate `username` ja `password` __ kohta loe siit [juurdepaeaesutaotlus.md](../juurdepaeaesutaotlus.md "mention")

Muutujad `username2` ja `password2` on vajalikud ainult testide jaoks (nimelt sellel kasutajal puudub e-arhiiviteatise taotlemise API kasutusõigus) ja nende väärtused saadetakse koos jagamise lingiga.

Kollektsiooni kasutamisel tuleb esimese asjana jooksutada [`user/verify`](../paeringud/kasutaja.md) päringut ja kopeerida vastusest `accessToken` väärtus keskkonna samanimelise muutuja väärtuseks. Kui _token_ aegub, tuleb seda tegevust korrata.

{% hint style="info" %}
Päringute gruppe saab käivitada suvalises järjekorras, aga grupi sees tuleks päringuid käivitada järjest. Näiteks`application/create`enne ja`application/update` pärast ja`application/delete`kõige lõpus. Siis ei ole vaja päringutes identifikaatoreid käsitsi muuta. Taotluse loomise päring omistab tagastatud uue taotluse ID väärtuse muutujale, mida järgnevad päringud kasutavad.
{% endhint %}
