Silmukat eli toistolauseet tai -rakenteet ovat aiemmin esiteltyjen ehtolauseiden rinnalla yksi ohjelmoinnin perusrakenteista. Silmukoiden avulla voidaan toistaa samaa koodia useita kertoja. Pythonissa on kaksi erilaista silmukkaa: `for` ja `while`. Vastaavat silmukat löytyvät myös muista ohjelmointikielistä. 

Silmukoiden lisäksi toistuvuutta voi lisätä funktio-ohjelmoinnin paradigman mukaisesti sekä ulkoisten kirjastojen kuten itertools avulla. Nämä käsitellään tässä materiaalissa vain pintaraapaisuna.

!!! tip 

    Silmukat ovat tapa vähentää toistoa. Mikäli huomaat kirjoittavasi samaa koodia useaan kertaan, kannattaa miettiä, voisiko sen korvata silmukalla. Tästä käytetään usein muistisääntönä lyhennettä DRY (Don't Repeat Yourself).

## Silmukoiden käyttö

### For

For-lauseketta voi käyttää minkä tahansa iteroitavan objektin kanssa. Pythonin sisäänrakennetuista tietotyypeistä iteroitavia ovat muun muassa sekvenssit: lista, sanakirja tai merkkijono. For-lauseketta jatketaan, kunnes iteraattori ilmoittaa, että itemit ovat loppu (StopIteration-niminen Exception).

```python

# Iteraraattori voi olla mikä tahansa kurssilla esitellyistä sekvensseistä.
persons: list|set|dict|str|tuple|range|bytes = [
    "John",
    "Jane",
    "Joe",
    "Jill"
]

for person in persons:
    print(person)
```

!!! question "Tehtävä"

    Kokeile, kuinka for käyttäytyy sanakirjan (dict) avulla. Selvitä, kuinka iteroit sanakirjan avaimia, arvoja tai molempia.

### While

While-lauseke on toinen silmukkatyyppi. Se toistaa koodia niin kauan kuin ehto on tosi. Totuusarvo evaluoidaan ennen silmukan suorittamista, joten silmukkaa ei välttämättä suoriteta kertaakaan.

```python
condition = False

while condition:
    print("Tämä ei tulostu koskaan.")
```

!!! warning

    While-silmukka on hyvin helppo kirjoittaa niin, että se ei koskaan lopu. Tämä johtaa ohjelman jumiutumiseen. Tämän vuoksi while-silmukkaa käytettäessä tulee olla erityisen tarkkana. Alla oleva sovellus ei lakkaa koskaan ajamasta itseään.

    ```python
    while True:
        print("Cat")
    ```

### Aputyökalut: continue ja break

#### Continue

Continue lauseke hyppää yhden iteraation yli. Esimerkiksi seuraava koodi tulostaa vain parilliset luvut.

```python
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
```

#### Break

Break lauseke keskeyttää silmukan suorituksen. Esimerkiksi seuraava koodi tulostaa luvut 0-4.

```python
for i in range(10):
    if i >= 5:
        break
    print(i)
```

## Silmukka ja Else

Else lauseke on hieman harvemmin käytetty silmukoiden yhteydessä, joten se saattaa herättää kummastusta lukijassa. Sille voi kuitenkin löytyä joskus paikkansa. Toisin kuin ehtolauseiden kanssa, joissa `else`-lauseke suoritetaan vain jos mikään `if` tai `elif` ei toteutunut, silmukoiden kanssa `else` toteutetaan StopIteration-exceptionin heittämisen jälkeen eli silmukasta poistuttaessa. Mikäli silmukan ajaminen keskeytetään `break`-lauseella, `else`-lauseketta ei suoriteta.

```python
ingredients = ['Egg', 'Ham', 'Pineapple']

# USe for else to check if the list contains 'Spam'
for ingredient in ingredients:
    if ingredient == 'Spam':
        print('Spam found!')
        break
else:
    print('No Spam found!')
```

## One-liner: comprehension

Pythonin sekvenssejä voi luoda myös comprehensionin avulla. Comprehension on Pythonin syntaktista sokeria (eli lyhyt syntaksi jollekin pidemmälle asialle), joka mahdollistaa listojen, sanakirjojen ja muiden sekvenssien luomisen yhdellä rivillä. Näinpä siis törmäät siihen usein seuraavissa sanapareissa

* list comprehension
* set comprehension
* dict(ionary) comprehension

List comprehensionin syntaksi on seuraava:

```text
# Lyhyt
[f(y) for y in z]

# Pidempi
[f(y) for y in z if g(y)]
```

* f(y) : expression
    * Palautuvan listan jokainen arvo käsitellään tämän lausekkeen avulla.
* y : muuttuja
    * Loopin sisällä käsiteltävä muuttuja.
* z : iterable
    * Loopattavata iterable, kuten lista, sanakirja tai merkkijono.
* g(y) : condition
    * Ehto, joka määrittää, otetaanko item mukaan lopulliseen listaan.

Yllä oleva esimerkki voi olla vaikea lähestyä, joten tutki alla olevaa esimerkkiä, jossa `my_list`-lista käsitellään list comprehensionin avulla.

```python
my_list = [1, 2, 3, 4, 5]

# Pitkä muoto
my_list_squared = []
for x in my_list:
    my_list_squared.append(x ** 2)

# Lyhyt muoto
my_list_squared = [x ** 2 for x in my_list]
```

Mikäli haluat comprehensionin palauttavan sanakirjan, käytä dict comprehensionia. Tarvitset tähän aaltosulkeet ja kaksoispisteen, aivan kuten muutenkin sanakirjan kanssa. Alla lyhyt esimerkki, jossa aiemmin käytetty lista käännetään sanakirjaksi. Avain on arvo merkkijonona, arvo on alkuperäinen arvo potenssiin kaksi.

```python
# Käytä aaltosulkeita ja kaksoispistettä, aivan kuten muutenkin dictin kanssa.
my_dict = {str(x): x ** 2 for x in my_list}
```

## Harjoittele

### Harjoittele: Lemmikkieläimet

Pythonilla voi iteroida mitä tahansa objektia, joka toteuttaa `__iter__` ja `__next__` metodit. Alla esimerkki. Silmukka alustaa iteraattorin kutsumalla `__iter__`-metodia. Tämän jälkeen silmukka kutsuu `__next__`-metodia, kunnes se heittää StopIteration-exceptionin.

```python
class MyIterator:
    def __init__(self, max:int):
        self.max = max
        self.n = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.n < self.max:
            result = 2 ** self.n
            self.n += 1
            return result
        else:
            raise StopIteration
```

Sitä voi ajaa seuraavalla tavalla:

```python
for i in MyIterator(5):
    print(i)
```

Muokkaa iteraattoria siten, että korvaat `max`-parametrin listalla pets. Tulosta tämän jälkeen kaikkien lemmikkien nimet for loopin avulla.

### Harjoittele: Tulosta iteroitavat tietotyypit

Tulosta for-silmukalla kaikki kurssilla esitellyt iteroitavat tietotyypit (paitsi NoneType). Käytä apuna Pythonin sisäänrakennettua [hasattr](https://docs.python.org/3/library/functions.html#hasattr)-funktiota. Yllä olevasta tehtävästä voit selvittää, mikä metodi iteroitavat objektin tulee toteuttaa.

```python
list_of_all_types = [
    bool,
    str,
    int,
    float,
    list,
    tuple,
    range,
    bytes,
    bytearray,
    set,
    frozenset,
    dict,
]
```

Tulostathan myös iteroitavien tietotyyppien nimet selkokielisinä. Hyväksyttävä tuloste on esimerkiksi:

```text
Iterable data types are:
- str
```

### Harjoittele: Silmukka ja else

Alla on dummy-pelisessio, joka vastaa `is_running()` kyselyyn 80 % todennäköisyydellä True. Tulosta pelisession aikakoodi niin kauan kuin serveri pyörii. Mikäli serverin ajo on loppunut, lokita ajanhetki.

```python
import random
from datetime import datetime

# A function that returns False with a 20 % probability.
class Gamesession:
    def __init__(self):
        pass

    @staticmethod
    def get_server_time() -> str:
        return datetime.now().replace(microsecond=0).isoformat()

    def is_running(self) -> bool:
        """Return True with 80 % probability."""
        return random.random() < 0.8
```

Alla on runko, jolla pääset alkuun:

```python
gamesession = Gamesession()

while gamesession.is_running():
    pass # Tähän server_time toteutus
    print(f"[{server_time}] Game session running...")
else:
    pass # ... ja tähän
    print(f"[{server_time}] Game session ended...")
```

### Harjoittele: 5 sekunnin while

Kirjoita koodi, joka ajaa while-looppia, kunnes 5 sekuntia on kulunut. Käytä apuna datetime-kirjastoa. Mikäli koodi jää ikuiseen looppiin, pysäytä se Jupyter Notebookin Interrupt-näppäimellä. Mikäli ajat koodia komentoriviltä, saman asian hoitaa pikanäppäin ++ctrl+c++.

```python
from datetime import datetime, timedelta

end_time = None  # Kuinka lasket nyt + 5 sekuntia ?

while False:   # <== Ratkaise tämä ehto. Mihin vertaat ja mitä?
    pass
else:
    print("5 seconds have passed!")
```