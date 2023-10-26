Tässä osiossa on esitelty Pythonin muuttujatyypit siinä laajuudessa, että voit luoda kokonaisia ohjelmia koskematta yhteenkään uuteen aiheeseen. Tämän osion jälkeen voit siirtyä opiskelemaan Pythonin muita ominaisuuksia, kuten ehtolauseita ja silmukoita.

Pythonin muuttujatyypit ovat hyvin yksinkertaisia, mutta niiden avulla voidaan kuitenkin tehdä monimutkaisia ohjelmia. Tämä on yksi Pythonin vahvuuksista: se on helppo oppia, mutta sillä voi luoda tuotantokäyttöön soveltuvia applikaatioita.

## Muuttujatyypin valitseminen

Pythonissa on useita erilaisia muuttujatyyppejä, ja niiden valitseminen voi olla aluksi vaikeaa. Tässä on muutamia vinkkejä, joiden avulla voit valita sopivan muuttujatyypin:

- Jos muuttujan arvo on kokonaisluku, käytä `int`-tyyppiä.
- Jos muuttujan arvo on desimaaliluku, käytä `float`-tyyppiä.
- Jos muuttujan arvo on teksti, käytä `str`-tyyppiä.
- Jos muuttujan arvo on totuusarvo, käytä `bool`-tyyppiä.
- NoneType on hyvä paikanpitäjä silloin, kun muuttujan arvoa ei ole vielä määritelty.

Mikäli arvo on ihmiskielessä monikko, kuten `colors`, käytä jotakin seuraavista tyypeistä:

- `list` on hyvä valinta, jos sinulla on tarve muuttaa sekvenssin sisältöä ohjelman suorituksen aikana.
- `tuple` on hyvä valinta, jos yllä oleva ei ole totta.
- `set` tulee usein tarpeeseen vain kun sinulla on tarve tutkia, onko jokin arvo olemassa tai verrata kahden eri sekvenssin populaatiota.

Mikäli tarvitset "look-up"-tyylisen tietorakenteen, käytä dict-tyyppiä. Tämä tarkoittaa, että sinulla on tarve löytää arvoja avaimen perusteella. Esimerkiksi, jos sinulla on tarve löytää henkilön nimi henkilötunnuksen perusteella, käytä dict-tyyppiä. Tällöin henkilötunnus on avain ja nimi on arvo.

Seuraavissa osioissa tutustutaan kontrollirakenteisiin, joiden avulla voidaan ohjata ohjelman suoritusta. Kontrollirakenteet ovat välttämättömiä, jotta ohjelmasta saadaan tehtyä jotakin järkevää.