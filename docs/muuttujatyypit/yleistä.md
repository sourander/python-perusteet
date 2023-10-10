Tämän otsakkeen alla olevissa luvuissa käsitellään osa Pythonin sisäänrakennetuista tietotyypeistä:

| Ryhmä dokumentaatiossa | Käsitellään luvussa (linkki)          | Ei käsitellä |
| ---------------------- | ------------------------------------- | ------------ |
| Numeric Types          | [int ja float](numerot.md)            | `complex`    |
| Sequence Types         | [list, tuple ja range](sekvenssit.md) |              |
| Text Sequence Type     | [str](merkkijono.md)                  |              |
| Binary Sequence Types  | [bytes ja bytearray](tavut.md)        | `memoryview` |
| Set Types              | [set ja frozenset](joukko.md)         |              |
| Mapping Type           | `dict`                                |              |
| Boolean Type           | `bool` (lue alta)                     |              |
| None Type              | `NoneType` (lue alta)                 |              |



### Boolean

Pythonin tietotyyppi `bool` edustaa Boolen algebran totuusarvoja **tosi** ja **epätosi**. Pythonissa boolean-muuttujat ovat sisäisesti numeroita, tarkemmin kokonaislukuja. Luku 0 vertautuu samaksi kuin False, luku 1 vertautuu samaksi kuin True.

```python
>>> 0 == False
True

>>> 1 == True
True

>>> False.real
0

>>> True.real
1

# Huomaa, että luku 2 ja muut luvut eivät ole True eivätkä False
>>> 2 == True or 2 == False
False
```

Tyypillisesti törmäät boolean arvoisin Pythonissa, kun vertailet kahta tai useampaa arvoa keskenään.

```python
>>> 3 > 2.0
True
```

Python käyttää konstruktoria `bool()` aina kun käytät `if` tai `while` kontrollirakenteita. Konstruktori käsittelee nollaa edustavia lukuja sekä tyhjiä sekvenssejä Falsena. Seuraavat kaksi ovat siis täysin samoja komentoja:

```python
my_name = "Bond, James Bond"

# Vaihtoehto 1: Pythonista tuttu tiivis tapa tarkistaa, että
# merkkijono ei ole tyhjä eli pelkkä "".
if my_name:
  print("I have a name")

# Vaihtoehto 2: täysin turhan "verbose"
if bool(my_name):
  print("I have a name")
```



### NoneType

Monissa muissa kielissä on `null`. Pythonissa on `None`. Nonea ei kuulu vertailla yhtä kuin (eli `==`) operaattorilla vaan identeettiä vertailevalla operaattorilla `is`. None on singulariteetti Jos siis haluat tietää, onko jonkin arvo Pythonissa None, tarkista se näin:

```python
>>> my_val = 2
>>> my_val is None
False

>>> my_val = None
>>> my_val is None
True
```

None itsessään on `bool`-konstruktorin näkökulmasta epätosi eli False, eli tämä toimii:

```python
my_name = None

if my_name:
  print("I have a name")
else:
  print("I have no name")
```

Miksikö yllä oleva toimii? Koska boolen konstruktori palauttaa Nonesta Falsen:

```python
>>> bool(None)
>>> False
```

Booleanilla ja NoneTypellä ei tee paljoakaan ennen kuin osaa käyttää muita muuttujatyyppejä. Nämä, ja varsinkin boolen totuusarvo, tulevat toistuvasti vastaan seuraavissa luvuissa. Tärkeintä on muistaa, että None:n identiteetti kuuluu tarkistaa sanalla `is`. None on niin sanottu singleton, eli jokainen instanssi None:sta on se täysin sama None sinun tietokoneesi muistissa. Käytännössä None tulee sinulle tutuksi funktioiden myötä eli myöhemmissä luvuissa tällä kurssilla.



## Opiskeluohje

Tämän otsakkeen luvut ovat **tarkoituksella lyhyitä ja tiiviitä**. Oppimiskäyrä saattaa siis tuntua hieman jyrkältä: tämä on tarkoitus. Luvut pyrkivät hyödyntämään kahta asiaa:

1. Tyypillisesti koodin lukeminen on helpompaa kuin sen kirjoittaminen.
2. Netti on pullollaan Python-tutoriaaleja. Luku toimii ponnahduslautana oikeaan suuntaan.

Lue esimerkin koodi rauhallisesti, tulkitse mitä se tekee, ja tarpeen mukaan lue lisätietoa Pythonin dokumentaatiosta tai tutoriaaleista. Kokeile snippettejä omassa ympäristössä ja aja sitä paloina. Lisää `print()`-lausekkeita koodin lomaan, kunnes koet ymmärtäväsi, mitä koodi tekee.

Lukujen yhteydessä esitellään myös Pythonin sisäänrakennettuja moduuleja, jotka liittyvät vahvasti kyseiseen muuttujatyyppiin.

Pythonin oma dokumentaatio listaa Pythonin sisäänrakennetut tietotyypit täällä: [Built-in Types](https://docs.python.org/3/library/stdtypes.html)