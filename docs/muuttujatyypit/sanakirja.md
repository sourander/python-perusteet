Sanakirja, englanniksi `dictionary` ja Pythonissa lyhyesti `dict`, muistuttaa rakenteeltaan fyysisen maailman sanakirjaa. Tietojenkäsittelyssä tämän termin kattokäsite on hakurakenne (associative array) ja monista kielistä löytyy jokin toteutus hajautustaulusta (hash map). Pythonissa se on dictionary. Aivan kuten paperinen sanakirja, myös Pythonin sanakirjan jokainen entiteetti sisältää kaksi entiteettiä: avaimen ja arvon.

## Sanakirjan luonti

Sanakirja määritellään aaltosulkeisiin aivan kuten joukko, mutta sen sisälle tulee pilkulla erotettuna entiteettejä, jotka koostuvat puolipisteellä erotellusta avaimesta ja arvosta.

```python
>>> {"avain": "arvo"}
{'avain': 'arvo'}

>>> dict(avain="arvo")
{'avain': 'arvo'}

>>> dict([(1, 2), (3, 4)])
 {1: 2, 3: 4}
```

Hieman pidempi sanakirja on seuraava, joka sisältää Jukka Korpelan _Pienehkön sivistyssanakirjan_ ensimmäiset kolme sanaa (lyhennettyjen) selitteiden kanssa.

```python
dictionary = {
    "à": "kukin, kappaleelta; vaihteluvälin ilmaisemiseen",
    "a cappella": "moniäänisesti ilman säestäviä soittimia esitettävä; näin esitetty laulu tms.",
    "à la": "jonkun tai jonkin mukaan, tapaan"
}
```

Sanakirjan luomisessa voi helpottaa Pythonin zip funktio, joka laittaa kaksi (tai enemmän) iteroitavaa muuttujaa yhteen vetoketjun lailla. Kokeile ajaa seuraava koodi esimerkiksi Jupyter Notebookissa:

```python
keys = ["jack", "lisa", "elisa"]
values = [
    ["spam", "pineapple"],
    ["egg", "ham", "spam"],
    ["spam", "double spam"]
]

favorite_foods = dict(zip(keys, values))
print(favorite_foods)
```

Sanakirjan avaimen on oltava häshättävissä eli ajettavissa onnistuneesti Pythonin hash funktion läpi. Muista: **L**ist, **S**et, **D**ictionary eli **LSD**. Mikäli kokeilet ajaa koodin `hash([1, 2, 3])`, Python nostaa varoituksen. Tämä tarkoittaa, että sanakirjaa ei voi myöskään käyttää sanakirjan avaimena – ja on vaikea keksiä miksi joku haluaisikaan. Sanakirja voi kuitenkin olla hyvin sanakirjan avaimen takana oleva arvo! Näin syntyy sisäikkäinen rakenne, joka on REST API:ien maailmasta tutun JSON:n kaltainen. Alla rankasti lyhennetty pseudoesimerkki sanakirjasta, joka on muotoiltu [Databricks Clusters API](https://docs.databricks.com/api/workspace/clusters/list):n palauttamasta JSON:sta.

```python
response = {
    "clusters":
      [
          {
              "cluster_name": "my-cluster",
              "spark_version": "8.2.x-scala2.12",
              "aws_attributes": {
                  "zone_id": "us-west-2c"
              },
              "num_workers": 30,
              "node_type_id": "i3.xlarge",
              "state": "TERMINATED",
              "start_time": 1618263108824,
              "terminated_time": 1619746525713,
              "termination_reason": {
                  "code": "INACTIVITY"
              }
          }
      ],
      # [...], second cluster here
      # [...], third cluster here
}
```

!!! warning

    Muistathan, että jokaisen avaimen tulee olla uniikki (hajautusarvoltaan).

## Sanakirjan käyttö

### Arvojen lisääminen

Sanakirjaan voi lisätä sijoittaa avaimia asettamalla niille arvon.

```python
alice = {"name": "Alice", "age": 42}
alice["pet"] = "parrot"
```

Huomaa, että Python ei varoita, jos avain on jo olemassa:

```python
alice["name"] = "Alice Smith"
```

### Arvojen noutaminen

Huomaa, että sanakirja ei ole sekvenssi. Et voi siis viitata niihin indeksinumerolla muotoa `alice[0]`.

```python
>>> alice = {"name": "Alice", "age": 42}
>>> alice["name"]
'Alice'

# Mikäli yrität noutaa olemattoman arvon...
>>> alice["number"]
KeyError: 'number'

# Tähän löytyy get-metodi, jonka oletus on None
# tai käyttäjän määrittämä arvo
>>> alice.get("number", "N/A")
'N/A'
```

### Arvojen muokkaus

Arvoja voi muokata sijoittamalla avaimeen uuden arvon.

```python
>>> alice = {"name": "Alice", "age": 42}
>>> alice["age"] = alice["age"] + 1
>>> print(alice)
{'name': 'Alice', 'age': 43}
```

## Sanakirja ja operaatiot

### Aritmeettiset, vertailu ja loogiset

Aritmeettiset ja vertailuoperaattorit, poislukien `==`, eivät toimi sanakirjojen kanssa. Loogiset toimivat samalla tavalla kuin sekvenssien ja joukkojen kanssa. Loogiset peraatiot kuten `and` käsittelee `bool()`-funktion palauttamaa arvoa. Tyhjä sanakirja eli `bool(dict())` palauttaa arvon False, ja mikä tahansa ei-tyhjä sanakirja palauttaa Truen.

### Sanakirja

Aivan kuten joukolla, myös sanakirjalla on nippu omia, hyödyllisiä operaatioita tai metodeja.

| Operaatio      | Selite                                                               |
| -------------- | -------------------------------------------------------------------- |
| list(d)        | Palauttaa listan avaimista.                                          |
| len(d)         | Palauttaa avainten lukumäärän                                        |
| d[key]         | Palauttaa avaimen key arvon                                          |
| d.get(key)     | Palauttaa avaimen key arvon (tai None)                               |
| d[key] = value | Asettaa avaimen key arvoksi value                                    |
| del d[key]     | Poistaa avaimen key ja sen arvon                                     |
| key in d       | Palauttaa True, jos avain key on sanakirjassa d, muuten False        |
| iter(d)        | Palauttaa sanakirjan avaimet iteraattorina                           |
| d.pop(key)     | Poistaa avaimen key ja palauttaa sen arvon                           |
| d.popitem()    | Poistaa ja palauttaa viimeiseksi lisätyn avaimen ja arvon            |
| d.reverse()    | Kääntää sanakirjan avaimet                                           |
| d &#124; other | Palauttaa yhdistetyn, uuden sanakirjan, joka sisältää d:n ja other:n |

## Sanakirjan käyttö Stack:nä

Sanakirjaa voi käyttää `.popitem()`:n avulla stäkkinä. Tuoreissa Pythonin versioissa (3.7+) dictionary muistaa järjestyksen, jossa entiteetit on siihen lisätty. Kokeile, mitä alla oleva koodi tulostaa. Tutki, missä järjestyksessä entiteetit tulostuvat, ja lisäksi missä tietotyypissä ne ovat.

```python
my_stack = dict()
my_stack['a'] = 1
my_stack['b'] = 2
my_stack['c'] = 3

for _ in range(2):
    print(my_stack.popitem())

my_stack['z'] = 20
my_stack['x'] = 19
my_stack['y'] = 18

while my_stack:
    print(my_stack.popitem())
```

## Moduuli: JSON

Sanakirja ja JSON ovat muodoltaan läheistä sukua toisilleen. JSON on JavaScript Object Notation, joka on JavaScriptin objektien ja sanakirjojen muotoiluun tarkoitettu notaatio. Pythonin JSON-moduuli tarjoaa kaksi funktiota, `json.dumps()` ja `json.loads()`, jotka muuntavat Pythonin sanakirjan JSON-muotoon ja takaisin.

```python
import json

ingredients = [
    {"id": 0, "name": "Egg", "price": 1.00},
    {"id": 1, "name": "Ham", "price": 0.50},
    {"id": 2, "name": "Späm", "price": 42.00},
]

# Python -> JSON
ingredients_json = json.dumps(ingredients, indent=4)
print("JSON: ", ingredients_json)

# JSON -> Python
ingredients_dict = json.loads(ingredients_json)
assert ingredients_dict == ingredients
```

Aja yllä oleva koodi ja tutki, kuinka Späm-sanan ääkkönen käyttäytyy JSON-merkkijonoksi materialisoituna. Kokeile myös, mitä tapahtuu, jos käytät parametriä `ensure_ascii=False` `json.dumps()`-funktiolle. Huomaa, että mikäli kirjoitat jälkimmäisellä tavalla JSON-tiedoston, joudut määrittämään tiedoston koodauksen, jotta ääkköset tallentuvat oikein. UTF-8 on tällöin suositus.

## Harjoittele

### Harjoittele JSON:sta objektiksi ja takaisin

Tallenna [wikipediasta löytyvä JSON-esimerkki](https://en.wikipedia.org/wiki/JSON#Syntax) tiedostoon `input.json`. Voit tehdä tämän vaiheen Visual Studio Codella, Pythonilla, vim:llä tai muulla valitsemallasi työkalulla. JSON kokonaisuudessaan alla:

```json
{
  "first_name": "John",
  "last_name": "Smith",
  "is_alive": true,
  "age": 27,
  "address": {
    "street_address": "21 2nd Street",
    "city": "New York",
    "state": "NY",
    "postal_code": "10021-3100"
  },
  "phone_numbers": [
    {
      "type": "home",
      "number": "212 555-1234"
    },
    {
      "type": "office",
      "number": "646 555-4567"
    }
  ],
  "children": [
    "Catherine",
    "Thomas",
    "Trevor"
  ],
  "spouse": null
}
```

Tee sitten seuraavat:

1. Lue tiedosto `input.json` ja tallenna sen sisältö muuttujaan `data`.
2. Muunna `data` Pythonin sanakirjaksi.
3. Lisää John:lle uusi lapsi, esimerkiksi "Jane".
4. Lisää John:lle uusi puhelinnumero, esimerkiksi "555-555-5555"
5. Muunna sanakirja takaisin JSON-muotoon.
6. Tallenna JSON-tiedosto `output.json`-nimellä.


### Harjoittele: Pydantic Model

Tutustu [Pydantic](https://pydantic-docs.helpmanual.io/) kirjastoon ja sen [Model](https://pydantic-docs.helpmanual.io/usage/models/) -luokkaan. Pydantic on Pythonin kirjasto, joka tarjoaa työkaluja tietotyyppien validointiin ja muuntamiseen. Se on erityisen hyödyllinen REST API:en kanssa työskennellessä. Pydanticin Model-luokka tarjoaa työkaluja Pythonin sanakirjojen muuntamiseen Pythonin luokiksi ja takaisin. Alla esimerkki kirjaston käytöstä:

```python
from pydantic import BaseModel, Field
from enum import Enum
from typing import List

class SpeciesEnum(str, Enum):
    cat = "cat"
    dog = "dog"

class Pet(BaseModel):
    name: str
    species: SpeciesEnum
    # Age field is in years and must be between 0 and 40
    age_years: int = Field(gt=-1, lt=41)


class Owner(BaseModel):
    name: str
    pets: List[Pet]

# Define
kitty = Pet(name="Kitty", species="cat", age_years=0)
puppy = Pet(name="Puppy", species="dog", age_years=7)
lisa = Owner(name="Lisa", pets=[kitty, puppy])

# Loop
for pet in lisa.pets:
    print(f"{pet.name} is a {pet.species} and is {pet.age_years} years old")
```

Jatka harjoitusta siten, että luet datan JSON-merkkijonon sisältävästä muuttujasta. Alla pohja:

```python
# Täytä nämä tiedot. Voit halutessasi luoda JSON-tiedoston ja
# lukea datan sieltä.
owner_data = """
{
  "name": "Unknown",
  "pets": []
}
"""

# Tutustu tähän metodiin
Owner.model_validate_json(owner_data) 
```

!!! tip

    Huomaathan, että pydantic ei ole Pythonin sisäänrakennettu kirjasto. Sinun tulee asentaa se paketinhallinnalla (pip tai poetry).