---
description: Miks API SKA moodul on loodud ja mida sellega teha saab?
---

# Sissejuhatus

## Veebirakendus

Alates 2013. aastast on Sotsiaalkindlustusameti töötajad saanud kasutada Rahvusarhiivi loodud ja Rahvusarhiivi domeenis asuvat veebirakendust [https://www.ra.ee/eteatis/](https://www.ra.ee/eteatis/), et taotleda sealtkaudu Rahvusarhiivilt e-arhiiviteatisi.

Nimetatud veebirakendus võimaldab luua, muuta ja kustutada e-arhiiviteatise taotlusi, kasutajaid (SKA töötajaid, kes taotlusi koostavad) ja üksuseid (SKA osakondi, millesse töötajad kuuluvad). Loodud taotlustele on võimalik lisada faile ja lõplikult vormistatud taotlused saab saata Rahvusarhiivi, nii et need laekuvad Rahvusarhiivi arhiiviteatiste menetlemise moodulisse.

Veebirakendus on selles mõttes autonoomne, et selle kasutajad (SKA töötajad) saavad kõiki vajalikke tegevusi teha ilma välise abita (Rahvusarhiivi töötajate abita).&#x20;

**Veebirakenduse ekraanivaated**

<div align="left">

<figure><img src="../.gitbook/assets/E-arhiiviteatis-Uus-taotlus (1).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/E-arhiiviteatis-Taotlused.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/E-arhiiviteatis-Vaata-taotlust.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/E-arhiiviteatis-Halda-üksusi (1).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/E-arhiiviteatis-Halda-töötajaid.png" alt=""><figcaption></figcaption></figure>

</div>

## API

API moodul, mida järgnevad leheküljed dokumenteerivad, dubleerib ülalmainitud veebirakenduse kõiki funktsioone.&#x20;

API kaudu saab luua, muuta ja kustutada e-arhiiviteatise taotlusi, SKA töötajaid, kes taotlusi koostavad, ja SKA üksuseid, millesse töötajad kuuluvad. Loodud taotlustele on võimalik lisada faile ja lõplikult vormistatud taotlused saab saata Rahvusarhiivi, nii et need laekuvad Rahvusarhiivi arhiiviteatiste menetlemise moodulisse.

Niisiis on selle API abil võimalik luua mistahes teise infosüsteemi osana mistahes domeeni alla kasutajaliides, mis sarnaneb Rahvusarhiivi loodud rakendusega[ https://www.ra.ee/eteatis/](https://www.ra.ee/eteatis/).

API kasutab sama _backendi_ ja salvestab andmeid samasse andmebaasi, kuhu veebirakendus. API kaudu loodud taotlusi saab vaadata veebirakenduses ja vastupidi — veebirakenduses loodud taotluste andmeid saab pärida API kaudu.&#x20;

**Postman ekraanivaade**

<figure><img src="../.gitbook/assets/ska-api.png" alt=""><figcaption></figcaption></figure>
