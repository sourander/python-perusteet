!!! warning

    Tämä materiaali on historiasyistä tässä. Tulevaisuudessa sen sisältö hajautetaan eri lukujen alle (esim. Muuttujatyypit/Yleistä).

Python lyhyesti:

- Python-ohjelma koostuu riveistä, jotka suoritetaan järjestyksessä ylhäältä alas.
- Rivit päättyvän rivinvaihtoon (tarkemmin merkkeihin `LF` tai `CR+LF`). Siispä komentoja ei päätetä esimerkiksi `;`-merkkiin, kuten monissa muissa kielissä.
- Tyhjät rivit ovat sallittuja ja luettavuuden parantamiseksi jopa suositeltavia. Koodin voi jakaa loogisiin kokonaisuuksiin samalla tavalla kuin tavallisessa tekstissä kappaleet.
- Koodia ei erikseen käännetä binääriksi vaan Python-tulkki lukee `.py`-tiedostoa ja tulkkaa sitä tavukoodiksi. Kyseessä on siis **tulkattava** ohjelmointikieli.
- Python on olio-ohjelmointikieli, mutta ei sulje pois muiden paradigmojen kuten proseduraalisen tai funktionaalisen ohjelmoinnin käyttöä.
- Koodin on luonut Guido van Rossum ja sen nimi tulee Monty Python's Flying Circus -tv-sarjasta. Mikäli sarja on sinulle tuttu, tulet huomaamaan dokumentaatiossa useita viitteitä ohjelmaan, kuten egg, ham, spam, spam, spam ...
- Kooditiedostot ovat tavallisesti UTF-8 -enkoodattuja ja tukevat näin valtavaa merkistöä. Myös emojit toimivat. :snake:
- Sisennyksellä on erityinen merkitys! Sillä on siis merkitystä, että alkaako rivi ilman välilyöntejä vai 4, 8, 16 tai jollakin muulla määrällä välilyöntejä. Konventio on, että välilyöntejä on aina neljällä jaollinen määrä, ja että sisennykseen käytetään nimenomaan välilyöntiä eikä koskaan tabulaattoria.

!!! question "Tehtävä"

    Lue Python Docsin oma [Whetting Your Appetite](https://docs.python.org/3/tutorial/appetite.html), joka mainostaa Pythonin vahvuuksia

Tietokoneohjelmat tallentavat tietokoneen muistiin (eli "rammiin") muuttujien arvot. Monissa matalamman tason ohjelmointikielissä, kuten C-kielessä, arvot tallennetaan muistiin kohtalaisen raakana. Python on hyvin korkean tason (eng. high level) ohjelmointikieli, joten yksinkertaisimmatkin asiat kuten kokonaisluvut (eng. integer) tallennetaan muistiin _objekteina_. Pythonissa ei ole C-kielestä tuttu pointtereita.

## Esimerkkikoodia

Jotta Python tulisi välittömästi tutuksi, hypätään suoraan altaan syvään päätyyn ja tuijotetaan koodia. Mikäli et ole aiemmin ohjelmoinut millään kielellä, et välttämättä ymmärrä alla olevaa koodia kokonaisuudessaan. Yritetään silti silmäillä, mitä siinä tapahtuu. Koodissa määritellään tyypillinen Python-funktio. Kyseinen funktio ottaa sisäänsä yhden positionaalisen argumentin (`words`) sekä kaksi keyword argumenttia (`per_row` sekä `margin`). Funktio ottaa sisäänsä listan sanoja ja tulostaa ne ruudulle tabulaarisessa muodossa. Esimerkki funktiokutsusta on hieman alempana.

```python
def print_as_tabular(           # (1)
        words:list[str],        # (2)
        per_row:int=5,
        margin:int=2
    ):                          # (3)

    # Calculate variables       # (4)
    column_width = max([len(x) for x in words]) + margin
    n_words = len(words)                                  # (5)

    # Loop and print
    for batch in range(0, n_words, per_row):              # (6)
        row_words = words[batch:batch + per_row]
        for word in row_words:
            print(f"{word:<{column_width}}", end="")      # (7)
        print()
```

1. Funktio määritellään `def`-sanalla. Funktion nimi on tässä tapauksessa `print_as_tabular`. Argumentit määritellään funktion nimen jälkeen sulkujen väliin pilkulla erotettuna.
2. Funktion ensimmäinen argumentti ei sisällä default-arvoa ja on näin positionaalinen argumentti. Käyttäjän on pakko antaa sille arvo funktiota kutsuttaessa. Rivi sisältää myös Pythonissa suhteellisen tuoreen `type hint`-vihjeen, joka on `list[str]`. Näin käyttäjä sekä IDE kuten VSCode tietävät, että ensimmäisen argumentin kuuluisi olla lista, joka sisältää merkkijonoja. Kaksi muuta argumenttia ovat vailla default-arvoa, mutta myös niillä on tyyppivihje (`int`). Positionaaliset argumentit tulee aina määritellä ennen keyword-argumentteja.
3. Funktion määrittely lopetetaan sulken jälkeen puolipisteeseen. Funktion runko jatkuu seuraavilla riveillä siten, että sitä on sisennetty neljällä välilyönnillä. Pythonissa lähes aina yksittäinen rivi sisältää jonkin kokonaisuuden, kuten funktion määrittelyn. Sulkeet ovat poikkeus. Sulkeiden välissä olevan sisällön saa jakaa haluamalleen määrälle rivejä, kunhan noudattaa sisennyssääntöjä.
4. Yhden rivin kommentit aloitetaan risuaidalla.
5. Uusia muuttujia ei tarvitse erikseen alustaa mitenkään eikä niille tarvitse määritellä tiettyä tyyppiä kuten `int` tai `str`. Tyyppivihje on kuitenkin tuettuna; sitä ei vain käytetä tässä esimerkissä.
6. Kontrolli- ja silmukkarakenteet kuten `for` muistuttavat funktion määrittelyä rakenteeltaan. Rivin viimeinen merkki on puolipiste. Rakenteen runko on sisennetty 4 välilyönnillä määrittelyyn nähden.
7. Tavallisesti sisäänrakennetun `print`-funktion kutsuminen luo yhden rivin per kutsu. Tässä sitä rikotaan antamalla funktiolle keyword-argumentti `end`, jossa rivi lopetetaan rivinvaihdon sijasta pelkällä tyhjällä.

## Varatut avainsanat

Pythonissa, kuten muissakin ohjelmointikielissä, on tiettyjä sanoja, joita ei saa käyttää koodissa esimerkiksi muuttujien niminä. Kehitysympäristöt kuten Visual Studio Code onneksi useimmiten varoittavat näistä, tai vähintään sanat piirtyy ruutuun eri värillä kuin muut sanat. Pythonin varatut avainsanat löytyvät `keyword`-kirjastosta. Kirjasto on sisäänrakennetut, joten sitä ei tarvitse erikseen asentaa tai ladata.

```python
import keyword

# Kutsutaan yllä luomaamme funktiota.
# Funktio tulostaa ruudulle listan tabulaariseen muotoon.
print_as_tabular(keyword.kwlist)
```

Ruudulle tulostuu:

```
False     None      True      and       as
assert    async     await     break     class
continue  def       del       elif      else
except    finally   for       from      global
if        import    in        is        lambda
nonlocal  not       or        pass      raise
return    try       while     with      yield
```

Listalla näkyvistä sanoista lähes jokainen tulee tämän kurssin aikana sinulle tutuksi.

## Välteltävät avainsanat

Yllä listattujen ehdottomasti kiellettyjen sanojen lisäksi on sisäänrakennettuja funktioita, joiden jyrääminen omille funktioilla on hyvän tavan vastaista. Nämä löytyvät `builtins`-kirjastosta. Tulostetaan niistä vain ne, jotka alkavat pienellä kirjaimella. Suurella kirjaimella alkavat ovat pääosin poikkeuksia (eng. exceptions). Näitä ovat muun muassa `SyntaxError`, jonka Python nostaa aina kun koodi sisältää jotakin, mitä ei voi suorittaa, tai `IndentationError`, jonka Python nostaa mikäli sinulla on epäkelpo määrä välilyöntejä koodissa. Alla on koodi, joka tulostaa vain pienellä kirjaimella alkavat:

```python
import builtins

# Haetaan builtins:sta vain pienellä kirjaimella alkavat
low_case_builtins = [x for x in dir(builtins) if x[0].islower()]

# Hyödynnetään taas yllä luomaamme funktiota
# Onpa funktiot näppäriä, ei tarvi kirjoittaa koodia monesti!
print_as_tabular(low_case_builtins, per_row=4)
```

Ruudulle tulostuu:

```
abs           aiter         all           anext         any           ascii
bin           bool          breakpoint    bytearray     bytes         callable
chr           classmethod   compile       complex       copyright     credits
delattr       dict          dir           display       divmod        enumerate
eval          exec          execfile      filter        float         format
frozenset     get_ipython   getattr       globals       hasattr       hash
help          hex           id            input         int           isinstance
issubclass    iter          len           license       list          locals
map           max           memoryview    min           next          object
oct           open          ord           pow           print         property
range         repr          reversed      round         runfile       set
setattr       slice         sorted        staticmethod  str           sum
super         tuple         type          vars          zip
```

## Case: Snake case

Monissa ohjelmointikielissä, kuten Javassa, käytetään niin sanottua camel casea, jossa muuttuja voi olla muotoa `myVariableName`, luokat ovat yleensä kapitaaleilla alkavaa Pascal casea eli `MyClassName`. Pythonissa on käytössä **snake case**. Noudata seuraavia PEP 8 -suosituksia.

| Entiteetti          | Esimerkki                                 |
| ------------------- | ----------------------------------------- |
| Muuttuja (variable) | `a`, `car`, `cars`, `my_variable`         |
| Funktio (function)  | `is_boolean`, `get_item`, `calculate`     |
| Luokka (class)      | `Car`, `CarList`, `Calculator`, `User`    |
| Moduuli (module)    | `main.py`, `__init__.py`, `my_program.py` |
| Paketti (package)   | `helpers`, `utils`, `models`.             |

Suosi kuvaavia nimiä silloin kun mahdollista. Tämä auttaa pitämään koodisi luettavana ilman valtavaa määrää avustavaa dokumentaatiota. Mikäli jokin asia on lista, kuten `cars`, niin pidä nimi monikossa. Tämä mahdollistaa helppolukuisen `for car in cars`-lauseen kuten myös `if 'Ferrari' in cars`-lauseen.

Pakettien nimiin voi sisällyttää hätätapauksessa myös alaviivan `_` kuten `my_package`, mutta ei koskaan väliviivaa. Ethän siis tee Python-moduuleja sisältävää kansiota, jonka nimi on `my-package`. Projektikansio voi, kuten gitin parhaat käytännöt sanelevat, sisältää väliviivan. Alla vielä korostava esimerkki:

```
~/Code/gitname/project-x/                   # Projektin pääkansio sisältää
~/Code/gitname/project-x/README.md          # .git-kansion, README:n ja muuta
~/Code/gitname/project-x/.git/
~/Code/gitname/project-x/project_x/main.py    # <= Pythonille OK
~/Code/gitname/project-x/project-x/main.py    # <= EI
```

Aputiedostot, kuten `./data/my-awesome-image.png` saavat sisältää väliviivoja, mutta pidät väliviivat poissa kaikesta, mikä liittyy suoranaisesti Pythoniin. Väliviiva on matemaattinen miinusoperaatio.

PEP 8 -tyyliohje löytyy kokonaisuudessaan täältä: [PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/). Osan tyylivirheistä voi korjata automaattisten työkalujen kuten [black](https://github.com/psf/black) avulla. Näihin tutustutaan kurssin loppupuolella ajan sallimissa rajoissa.

Lopuksi on hyvä mainita vielä piilotetut tai salaiset muuttujat. Jos näet muuttujan muotoa `_variable` tai `_Foo__variable`, älä pakota sille mitään arvoa vaan anna sen olla. Lisäksi Pythonissa on tiettyjä erityisiä, "magic object or attributes"-ryhmään kuuluvia itemeitä, jotka tunnistaa kahdella alaviivalla alkavasta ja loppuvasta nimestä. Näitä ovat esimerkiksi `__init.py__`-moduulin nimi, `__str__`-funktio, `__name__`-objekti ja niin edelleen. Älä keksi vastaavia itse lisää vaan käytä niitä kuten dokumentaatio neuvoo.

## Muuttujien nimet

Muuttujien nimistä on hyvä käydä vielä pari lisäkäytäntöä sekä sääntöä. Pidättäydy ASCII-merkistössä eli mieluiten kirjaimissa a-z. Jätä suuret kirjaimet luokkien ja pysyvien muuttujien käyttöön. Python sallii tiettyjä erityismerkkejä muuttujan nimeksi. Älä käytä niitä. Alla esimerkki:

```bash
π = 3.141592653589793  # EI
pi = 3.141592653589793 # KYLLÄ

Θ = 1.12               # EI
theta = 1.12           # KYLLÄ
```

Yllä olevan hyvän käytännön lisäksi on myös sääntöjä, joita on pakko noudattaa, tai muuten Python nostaa `SyntaxError`:n tai muun. Näitä sääntöjä ovat:

1. Muuttujan nimi ei saa alkaa numerolla.
2. Muuttuja ei saa sisältää välilyöntejä
3. Muuttuja ei saa sisältää valtaosaa erikoismerkeistä

Alla esimerkkejä, jotka eivät kertakaikkiaan käy:

```python
1_cat_named = "Miaw"
99luftballons = "Song"
"food" = "Egg, ham, spam without spam"
my favorite pet = "Parrot"
my-favorite-pet-race = "Norwegian Blue"
💩 = "Mr. Hankey"
```
