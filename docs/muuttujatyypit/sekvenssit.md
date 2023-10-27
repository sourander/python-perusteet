Pythonissa on useita tietotyyppejä, jotka lukeutuvat sekvensseihin, kuten [Yleistä](yleistä.md)-luvussa listattiin. Sekvenssit ovat joukkio elementtejä tietyssä järjestyksessä. Jokaisella elementillä on indeksi. Ensimmäisen elementin indeksi on nolla (eli lista on `zero-indexed`). Yksi on jo sinulle aiemmin tuttu: merkkijonot eli `str`. Tässä luvussa käsitellään kolme uutta: `list`, `tuple` ja `range`. Suomeksi nämä kääntyisivät listaksi, monikoksi ja kenties arvojoukoksi, mutta tässä luvussa käytetään vain ja ainoastaan niiden alkuperäisiä nimiä Finglish-tyylisesti taivutettuna. Merkkijono on staattisesti tyypitetty sekvenssi, eli jokainen merkki on Unicode-koodipiste.

Range poikkeaa tuplesta ja listasta siten, että se on lasketaan auki vasta kun on pakko eli se on jossain määrin lazy evaluated. Kun edistyt Pythonissa, tulet oppimaan tähän liittyvien generaattoreiden käytön. Toistaiseksi voit hyväksyä, että range on tasavälinen sekvenssi, jota voi loopata ja jonka voi kääntää listaksi.

## Sekvenssien luonti

```python
# Lista
items = ["abc", 42, 42, 3.14]

# Tuple - kaksi vaihtoehtoa
items = ("abc", 42, 42, 3.14)
items = "abc", 42, 42, 3.14

# Range - harvoin oikeasti osoitetaan muuttujaan!
thousand_elems = range(1000)

# Range - alku ja loppu
twenty_to_thirty = range(20, 30)

# Range - alku, loppu ja askelkoko
odd_numbers_before_twenty = range(1, 20, 2)
```

Sekvenssin voi luoda myös kutsumalla kyseisen tyypin konstruktoria. Huomaa, että argumentin on oltava iteroitava objekti eli iterable. Mikäli termi on vieras, kannattaa lukaista [Python Glossary: Iterable](https://docs.python.org/3/glossary.html#term-iterable). Huomaa, että tämä ei toimi rangen kanssa.

```python
# Listasta tupleksi
>>> my_list = [1, 2, 3]
>>> tuple(my_list)
(1, 2, 3)

# Tuplesta listaksi
my_tuple = (1, 2, 3)
tuple(my_tuple)

# Rangesta listaksi
list(range(6))
[0, 1, 2, 3, 4, 5]
```

Huomaa, että myös merkkijono on iterable - sehän on yksi sekvensseistä itsekin.

```python
>>> list("spam")
['s', 'p', 'a', 'm']
```

## Immutability

Yllä olevien esimerkkien perusteella lista ja tuple saattavat tuntua huomattavan samanlaisilta. On siis tärkeää painottaa heti alkuun, että niillä on merkittävä eroavaisuus: immutability eli muuttumattomuus. Pythonin listaan voi lisätä ja siitä voi poistaa elementtejä luomisen jälkeen, joten useimmissa ohjelmointikielissä sen vastine olisi "dynamic array".

!!! tip

    Muistisääntö saattaa auttaa tässä ainakin aluksi. Muutettavia (eli mutable) tietotyyppejä Pythonissa ovat **LSD**: List, Set, Dict.

Käytännössä tämä tarkoittaa juuri sitä, miltä se kuulostaa. Listaa voi muuttaa luomisen jälkeen, tuplea ei.

```python
# Listan muuttaminen
>>> items = ["a", "b", "c"]
>>> items[0] = "x"
>>> print(items)
['x', 'b', 'c']

# Saman yrittäminen tuplelle
>>> items = ("a", "b", "c")
>>> items[0] = "x"
>>> print(items)
??? # Kokeile, mitä tulostuu !
```

## Sekvenssit ja operaatiot

### Aritmaattiset, Vertailu ja Loogiset

Nämä toimivat listan ja tuplen kanssa samalla tavalla kuin merkkijonojen kanssa. Rangen kanssa näistä ei toimi mikään. Kokeile seuraavia kertauksen ja todistamisen vuoksi:

```python
# Operaattori: +
(1, 2, 3) + (4, 5, 6)

# Operaattori: *
(1, 2, 3) * 5

# Operaattori: >
(4, 5, 6) > (1, 2, 3)

# Operaattori: <=
(1, 1, 2) > (1, 1, 3)

# Operaattori: or
() or (1, 2, 3)
```

### Sekvenssi-operaatiot

| Operaatio            | Selite                                                |
| :------------------- | :---------------------------------------------------- |
| `4 in (3, 4, 5)`     | Tarkistaa, sisältyykö elementti sekvenssiin.          |
| `8 not in (3, 4, 5)` | Yllä olevan negaatio                                  |
| `(1, 2, 3)[i:j:k]`   | Indeksointi ja rajaus (eng. slicing). Lue alta lisää. |
| `len((1, 2, 3))`     | Elementtien määrä                                     |
| `min((1, 2, 3))`     | Pienin elementti                                      |
| `max((1, 2, 3))`     | Suurin elementti                                      |
| `(1, 2, 3).index(2)` | Etsityn elementin indeksi.                            |
| `(2, 2, 2).count(2)` | Kysytyn elementin lukumäärä                           |

!!! question "Tehtävä"

    Kokeile yllä olevia operaatioita listan tai rangen kanssa. Näin syntaksi jää paremmin mieleesi!

## Sekvenssin käsittely

### Sekvenssin pilkkominen

Listan ja sekvenssin pilkkominen on huomattavasti monipuolisempi ominaisuus kuin muut yllä listatut sekvenssioperaatiot. Sillä voi näppärästi päästä käsiksi haluttuihin elementteihin tai esimerkiksi kääntää listan edes-takaisin. Siksi tälle operaatiolle on varattu oma otsikkonsa. Huomaa, että `range(i, j, k)`-konstruktori toimii hyvin samalla tavalla kuin indeksointiin ja leikkelyyn käytetty syntaksi (`[i:j:k]`), jossa argumentit ovat:

| `[i:j:k]` | Selite                                                                                      |
| --------- | ------------------------------------------------------------------------------------------- |
| `i`       | Start eli aloituspiste. Inklusiivinen.                                                      |
| `j`       | End eli lopetuspiste. Eksklusiivinen eli kirjoitettu numero ei kuulu mukaan valintaan.      |
| `k`       | Step size eli askelkoko. Startin ja endin väli käydään askelletaan läpi tällä välityksellä. |

Lue alla oleva koodi huolella läpi ja kokeile sitä itse käytännössä.

```python
# Luodaan lista numeroista 0-20
>>> nums = list(range(21))

# Kymmenes elementti listalla
>>> nums[10]
10

# Elementit kolmesta kuuteen asti (huom! eksklusiivisuus)
>>> nums[3:6]
[3, 4, 5]

# Negatiivinen indeksi
>>> nums[-1]
20

# Positiivinen ja negatiivinen indeksi
>>> nums[9:-9]
[9, 10, 11]

# Pelkkä step size annettuna
>>> nums[::5]
[0, 5, 10, 15, 20]

# Samat stepit yhdestä alkaen
>>> nums[1::5]
[1, 6, 11, 16]

# Negatiivinen step kääntää listan edestakaisin
>>> nums[:13:-1]
[20, 19, 18, 17, 16, 15, 14]
```

!!! question "Tehtävä"

    Kokeile, mitä pelkkä `nums[::-1]` tekee!


### Sekvenssin pakkaus ja purku

Sekvenssin `packing` ja `unpacking` ovat yllättävän näppärä tapa käsitellä listoja tai tupleja. Pakkaus tarkoittaa sitä, että useasta muuttujasta luodaan yksi sekvenssi. Purku tarkoittaa sitä, että sekvenssistä luodaan useampi muuttuja. Pakkaus ja purku toimivat samalla tavalla listan ja tuplen kanssa. Pakkaus tuottaa tupleja, purku purkaa listoja.

```python
# Pakkaus
>>> my_tuple = 1, 2, 3  # tai (1, 2, 3)
>>> my_tuple
(1, 2, 3)

# Purku
>>> a, b, c = my_tuple
>>> a
1

# Purku ja pakkaus sekaisin
>>> eka, toka, *loput = 1, 2, 3, 4, 5
>>> loput
[3, 4, 5]

# Purku
>>> (*letters, ) = "kissa"
>>> letters
['k', 'i', 's', 's', 'a']
```

Pakkauksen ja purun kanssa voi käyttää myös tähteä (`*`) edustamaan n-kappaletta elementtejä.

```python
# Pakkaus
>>> eka, toka, *loput = 1, 2, 3, 4, 5
>>> loput
[3, 4, 5]


### Sekvenssin aggregointi

Mikäli haluat tietää listan suurimman tai pienimmän arvon, tai kaikkien arvojen summan, tähän löytyy valmiit funktiot min, max ja sum.

```python
grades = [3, 4, 2, 5, 1, 1]

average = sum(grades) / len(grades)
print(f"Average (mean) grade is {average:.2f}.")
```

## Listalle ominaiset operaatiot

### Listan järjestäminen

Listan voi järjestää sort metodilla. Mikäli listan elementti on iterable, se järjestetään vakiona sen ensimmäisen elementin mukaan. Huomaa, että sort järjestää listan `in-place`-tyylisesti. Metodi ei siis palauta uutta, järjestettyä listaa, vaan lista itsessään päivittyy.

```python
scores = [(3, 5), (7,4), (2, 1), (5, 6)]
scores.sort()
print(scores)
[(2, 1), (3, 5), (5, 6), (7, 4)]
```

Mikäli haluat luoda uuden, järjestetyn listan, käydä Pythonin sisäänrakennettua funktiota sorted.

```python
scores = [(3, 5), (7,4), (2, 1), (5, 6)]
sorted_scores = sorted(scores)
```

Mikäli haluat järjestää listan elementit jollakin muulla tavalla kuin ensimmäisen entiteetin mukaan, sort-metodille tai sorted-funktiolle pitää antaa funktio, joka palauttaa järjestykseen käytettävän numeron. Funktiot opetetaan kurssilla myöhemmin, mutta alla on yksi tapa esiteltynä sekä tavallisen funktion että lambda-funktion avulla. Kummatkin tekevät saman asian.

```python
# Järjestysfunktion määrittely
def sort_by_second(x):
    return x[1]

# Järjestäminen funktiolla
scores = [(3, 5), (7,4), (2, 1), (5, 6)]
print(sorted(scores, key=sort_by_second))

# Järjestäminen lambda-funktiolla
print(sorted(scores, key=lambda x: x[1]))
```

Järjestys on vakiona pienestä suureen. Sen voi vaihtaa käänteiseksi avainsana-argumentin avulla. Alla esimerkki, jossa järjestämiseen käytetään Pythonin sisäänrakennettua summafunktiota:

```python
>>> sorted(scores, key=sum, reverse=True)
[(7, 4), (5, 6), (3, 5), (2, 1)]
```


### Listan kopiointi

Listalla on oma metodeja, joita muut sekvenssit eivät toteuta. Tutustut näistä useimpiin alla olevissa harjoituksissa. Alla käsitellään niistä yksi, joka on merkittävästi monimutkaisempi kuin muut eli `copy`.

```python
# ab on lista, johon kuuluvat merkkijonot a ja b
a = "egg"
b = "ham"
ab = [a, b]

# Orig on kolmielementtinen lista. Kolmas elementti on lista ab.
orig = [0, 1, ab]
print(orig)
```

Yllä oleva koodi tulostaa seuraavan. Listassa `orig` on siis kolme elementtiä, joista kolmas on lista.:

```
[0, 1, ['egg', 'ham']]
```

Yritetään kopioida lista.

```python
# Luodaan listasta shallow copy
shallow = orig.copy()

# Ja deep copy, johon tarvitaan copy.deepcopy
from copy import deepcopy
deep = deepcopy(orig)

# Tulostetaan
print(f"{'Original:':>10} {orig}")
print(f"{'Shallow:':>10} {shallow}")
print(f"{'Deep:':>10} {deep}")
```

Tämä tulostaa arvatenkin kolme täysin samanlaista listaa:

```
[0, 1, ['egg', 'ham']]
[0, 1, ['egg', 'ham']]
[0, 1, ['egg', 'ham']]
```

Mitä tapahtuu, jos me muokkaamme listoja, joista listat on kasattu ja/tai kopioitu?

```python
# Muokataan alkuperäistä ab-listan ensimmäistä elementtiä
# Vaihdetaan siis kananmuna vähän parempaan täytteseen
ab[0] = "spam"

# Muokataan myös alkuperäisen listan kolmannen elementin toista elementtiä
# Vaihdetaan siis kinkku vähän parempaan täytteeseen
orig[2][1] = "SPAM"

# Tulostetaan
print(f"{'Original:':>10} {orig}")
print(f"{'Shallow:':>10} {shallow}")
print(f"{'Deep:':>10} {deep}")
```

Tämä tulostaa, ehkä hieman yllättäen, kaksi identtistä ja yhden uniikin listan:

```python
 Original: [0, 1, ['spam', 'SPAM']]
  Shallow: [0, 1, ['spam', 'SPAM']]
     Deep: [0, 1, ['egg', 'ham']]
```

Mitä tästä opimme? Jos haluat listasta kopion, muista, että `.copy()` palauttaa SHALLOW-tyyppisen kopion. Tämä voi aiheuttaa vaikeasti debugattavia ongelmia, mikäli lista on moniulotteinen eli sisältää listoja (tai esimerkiksi dictionaryjä).

## Moduuli: itertools

Listan ja tuplen yhteydessä erittäin hyödyllinen kirjasto on itertools, josta löyty metodit permutaation, kombinaation ja karteesisen tulon laskemiseen joukkojen osalta. Tutustu myös muihin metodeihin: [Python docs: itertools](https://docs.python.org/3/library/itertools.html). Alla esimerkki, jossa generoidaan kaikki 3-täytteiset valkoiset tai punaiset pizzat.

```python
import itertools

# Tuples of ingredients
base = ("tomato sauce", "french cream")
ingredients = ("egg", "ham", "spam", "pineapple", "blue cheese")

# Find all unique combinations of 3 ingredients
unique_ingredient_sets = itertools.combinations(ingredients, 3)

# Create all possible 3-ingredient pizzas
pairs = list(itertools.product(base, unique_ingredient_sets))

# Print the pairs
for pair in pairs:
    print(pair)
```

## Harjoituksia

### Harjoittele: Listan omat metodit

Listalla on omia metodeita, joita muut sekvenssit toteuta. Näitä ovat `append`, `clear`, `extend`, `insert`, `pop`, `remove` ja `reverse`. Tutustu funktioihin seuraavalla tavalla:

```python
# Katso metodin oma docstring
# Kaava: help(nums.metodi)
>>> nums = [1, 2, 3, 4]
>>> help(nums.append)
# Lue output !
```

Kun olet tutustunut kunkin metodin help-tekstiin eli docstringiin, kokeile kutakin käytännössä.

### Harjoittele: Array

Mikäli tarvitset sekvenssiä, joka koostuu vain yhden tyyppisistä muuttujista, ja haluat olla varma ettei sinne vahingossakaan voi laittaa muita, Python tarjoaa myös tyyppimääritellyn `array`:n. Koska kyseinen sekvenssi on tyypitetty, se on muistinkäytön suhteen tehokkaampi kuin lista tai tuple. Tutustu tähän lyhyesti ja pohdi, missä sitä voisi käyttää.

```python
import array
arr = array.array('d', [1, 2, 3])
arr.append(42)
arr.append(123)
print(arr)
```

### Harjoittele: Statistiikka

Pythonin statistics-kirjastosta löytyvat mode, mean ja median funktiot. Käytä näitä tarkistamaan oma laskelmasi assert:n avulla. Korvaa alla olevassa koodissa None omalla laskukaavallasi. Huomaa, että saat luoda uusia muuttujia tarpeen mukaan.

```python
import random
from statistics import mode, mean, median

numbers = list(range(16))
random.shuffle(numbers)

# calculate mean
manual_mean = None # laske tämä itse
assert manual_mean == mean(numbers)

# calculate median
manual_median = None # laske tämä itse
assert manual_mean == median(numbers), f"Median is {manual_median}, should be {median(numbers)}"

# calculate mode
manual_mode = None # laske tämä itse
assert manual_mode == mode(numbers), f"Mode is {manual_mode}, should be {mode(numbers)}"
```

### Harjoittele: Anagrammi

Yllä esiteltiin moduuli itertools. Käytä funktiota `itertools.permutations()` ja luo kaikki sanan "kissa" anagrammit – oli niissä suomen kielen kannalta järkeä tai ei.

```python
import itertools

# Example using a tuple
letters = list("kissa")

# Create an iterator that generates permutations of the tuple
permutations = None # Tee toteutus tässä

# Print the permutations
for perm in permutations:
    print(perm)
```

Pohdi, kuinka selvittäisit, mitkä näistä sanoista ovat oikeasti suomen kielen sanoja.
