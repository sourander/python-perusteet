Pythonin tyypillisimmin käytössä olevat numeraaliset tietotyypit ovat kokonaisluku eli integer (`int`) sekä desimaaliluku eli floating point number (`float`). Tarkemmin ottaen kyseessä ei kuitenkaan ole desimaali- vaan liukuluku; tästä aiheesta on listätietoa alla. Pythonissa on myös kompleksiluku (`complex`), mutta se jätetään tässä materiaalissa käsittelemättä. Vahvasti tyypitetyissä kielissä, kuten C ja Java, on eri kokoisille luvuille omat muuttujatyyppinsä. Esimerkiksi pieniä lukuja varten, jotka mahtuvat välille `-128...127`, on oma muuttujatyyppintä byte. 1, 2, 3 ja 4-tavuisia numeroita varten ovat erikseen byte, short, int ja long. Pythonissa kaikkia näitä varten käytetään samaa tyyppiä: `int`. Myös `float` aina aina float, eikä eriksee 4- tai 8-tavuinen `float` tai `double`.

## Numeroiden luonti

Alla olevassa snippetissä luodaan kokonaisluku ja desimaaliluku ja tulostetaan niiden arvot aiemmin opittua F-stringiä hyödyntäen:

```python
n_apples = 1024
total_weight = 201.54
print(f"We have {n_apples} apples and they weight {total_weight} kilos.")
```

Suuret luvut voi kirjoittaa myös alaviivan tai tieteellisen notaation avulla. Huomaa, että Python ei kuitenkaan parsi alaviivaa sen tarkemmin. Tästä esimerkki alla:

```python
million = 1_000_000  # int
billion = 1e9        # float

million = 1_00_0000  # Python ei valita tästä
```

## Numerot ja operaatiot

Huomaa, että merkkijonot-luvussa tämä otsikko oli vielä "operaattorit". Numeroiden kohdalla tämä on laajennettu sisältämään operaattoreiden (`+`, `%`, `and`, ...) lisäksi myös muita operaatioita, kuten Pythonin sisäänrakennettujen funktioiden käytön.

### Aritmaattiset

| Operaatio       | Selite                                       |
| :-------------- | :------------------------------------------- |
| `x + y`         | *x* plus *y* (summa)                         |
| `x - y`         | *x* miinus *y* (erotus)                      |
| `x * y`         | *x* kertaa *y* (tulo)                        |
| `x / y`         | *x* jaettuna *y*:llä (osamäärä)              |
| `x // y`        | Osamäärä pyöristettynä alas kokonaisluvuksi. |
| `x % y`         | Jakojäännös                                  |
| `-x`            | *x*:n negaatio                               |
| `abs(x)`        | x:n absoluuttinen arvo                       |
| `int(x)`        | x konvertoituna kokonaisluvuksi              |
| `float(x)`      | x konvertoituna desimaaliluvuksi             |
| `divmod(x, y)`  | Tuple-muodossa seuraavat: `(x // y, x % y)`  |
| `x ** y`        | *x* potenssiin y                             |
| `round(x[, n])` | Pyöristä n desimaalin tarkkuudella. Vakio 0. |

Huomaa, että Python sallii matemaattiset operaatiot eri numeeristen tyyppien välillä. Voit siis esimerkiksi vähentää kokonaisluvusta desimaaliluvun. Operaatiosta palautuvan luvun tietotyyppi riippuu operaatiosta. Esimerkiksi jakolasku palauttaa aina `float`:n, vaikka luku olisi jaollinen.

### Vertailu

| Operaattori  | Esimerkki    |
| ------------ | ------------ |
| ==           | `3 == 2 + 1` |
| !=           | `3 != 4`     |
| >, <, >=, <= | `2.51 > 2`   |

### Loogiset

| Operaattori | Esimerkki |
| ----------- | --------- |
| and         | `2 and 3` |
| or          | `0 or 42` |
| not         | `not 0`   |

!!! question "Tehtävä"
    Kokeile kaikki yllä olevat operaattorit läpi. Selvitä, mitä ne tekevät. Loogiset operaattorit, saattavat tuntua lukujen kanssa epäloogisilta. Ota selvää!

### Bitti

Kokeile ajaa alla olevan taulukon esimerkit Pythonissa. Selvitä, mitä tapahtuu, jos muutat arvoja. Jos et onnistu päättelemään operaattoreiden toiminnallisuutta, lue aiheesta lisää esimerkiksi [Wikipedia: Bittioperaatio](https://fi.wikipedia.org/wiki/Bittioperaatio).

| Operaattori | Termi tai selite  | Esimerkki          |
| ----------- | ----------------- | ------------------ |
| &           | AND               | `0b1111 & 0b1111`  |
| \|          | OR                | `0b0000 OR 0b1111` |
| ^           | XOR               | `0b1010 ^ 0b0101`  |
| ~           | NOT               | `~ 0b0111`         |
| <<          | Siirto vasemmalle | `0b0001 << 1`      |
| >>          | Siirto oikealle   | `0b0010 >> 1`      |

!!! tip
    Näistä on esimerkkejä alempana tässä samassa luvussa. 



## Numeroiden muotoilu

Numeroita voi muotoilla F-stringin avulla. Kokeile ajaa alla oleva koodi, joka tulostaa edellisestä luvusta tutut Unicode plane -alueet.

```python
for section in range(17):
    start = (2 ** 16 * section)
    end = start + 2 ** 16 - 1
    
    print(f"{section:<2}{start:>10}{end:>10}")
```

Aiemmin tutun "padding and aligning"-operaation lisäksi numeroita voi muotoilla huomattavan monilla muilla tavoin. Alla joitakin valittuja esimerkkejä:

| `{muuttuja:muotoiluohjeet}` | Tuloste     | Selite                                              |
| --------------------------- | ----------- | --------------------------------------------------- |
| `{10:X}`                    | `A`         | Esitä luku heksadesimaalina (isot kirjaimet)        |
| `{10:x}`                    | `a`         | Esitä luku heksadesimaalina (pienet kirjaimet)      |
| `{10:#X}`                   | `0xa`       | Esitä luku heksadesimaalina `0x` etuliitteen kera.) |
| `{10:2x}`                   | `" a"`      | Esitä luku vähintään kahden merkin mittaisena.      |
| `{10:0x2}`                  | `0a`        | ... ja tyhjät paikat täytettynä nollilla.           |
| `{1234567:,}`               | `1,234,567` | Tulosta tuhansien välein pilkut.                    |
| `{pi:.2f}`                  | `3.14`      | Tulosta 2 desimaalin tarkkuudella.                  |
| `{42:.2f}`                  | `42.00`     | ... joka pätee myös kokonaislukuihin.               |

!!! tip
    Aiemmin mainitut vanhemmat muotoilutavat (format ja %-syntaksi) jätetään käsittelemättä tässä luvussa, mutta mikäli aihe kiinnostaa, tutustu vapaasti numeroiden tulostamiseen `"".format()` avulla. Toimiiko muoto `"{0:.2f}".format(42.00001)"` ?

Otetaan heksadesimaalimuunnos hyötykäyttöön, ja muokataan yllä olevaa Unicode plane -tulostinta. Alla sama koodi muokattuna siten, että se tulostaa numerot heksadesimaaleina. Luku vie aina vähintään 6 merkkiä; täytteenä toimii välilyöntimerkki:

```python
for section in range(17):
    start = (2 ** 16 * section)
    end = start + 2 ** 16 - 1
    
    print(f"{section:<2} {start:6x} {end:6x}")
```



!!! question "Tehtävä"
    Päättele yllä olevien avulla, kuinka käännät luvun binääriksi ja tulostat 8 merkkiä pitkänä. Luvusta 127 pitäisi tulostua `01111111`, mukaan lukien ensimmäinen nolla. Vihje: `b`.



## Numeroiden metodit

Toisin kuin merkkijonot, joihin liittyy useita hyödyllisiä metodeja kuten `.lower()`, numerot ovat merkillisen tylsiä. Kokeile tätä itse esimerkiksi Jupyter Notebookissa tai Visual Studio Codessa:

```python
# Luo muuttuja
num = 5
num.     # paina tabia (1)

# Kokeile myös floattia
other = 3.14
other.   # paina tabia

# Kokeile myös class methodeja eli ei olion vaan itse luokan funktioita
int().   # paina tabia
float(). # paina tabia
```

1. Tabulaattorin, eli Q-näppäimen vasemmalla puolella olevan näppäimen, klikkaaminen käynnistää IDE:n koodin täydennyksen (code completion), joka listaa kaikki kyseisen olion metodit (eli olion omat funktiot) ja ominaisuudet (propertyt), jotka eivät ala alaviivalla eli eivät ole yksityisiä. IDE:stä riipppuen mukaan saattaa tulostua ties mitä muuta, kuten tiedostopolkuja.



## Moduuli: datetime

Sinulla on nyt hallussa merkkijonojen ja numeroiden perusteet, joten voit alkaa käsitellä päivämääriä ja aikoja. Päivämääriä varten löytyy `datetime.date` ja aikoja varten `datetime.datetime`. Alla pari peruskomentoa, joilla pääset alkuun, mutta Internet on täynnä esimerkkejä aiheesta.

Huomaa, että päivämääriä ja aikoja voi tulostaa ANSI C -standardin mukaisilla koodeilla, joissa esimerkiksi `Y` edustaa nelinumeroista vuotta. Koko lista löytyy [Pythonin dokumentaatiosta](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes).

```python
import datetime

# Today hakee käyttöjärjestelmän kellolta päivämäärän
today = datetime.date.today()

# Vaihtoehto 1: muotoile merkkijono strftime funktiolla
today_str = today.strftime("%Y:%m:%d - %A")
print(today_str)

# Vaihtoehto 2: muotoile F-stringin muotoiluosassa
print(f"{today:%Y:%m:%d - %A}")

# P.S.
# Muista, että voit myös näin voi tehdä:
dt_format = "%Y:%m:%d - %A"
print(f"{today:{dt_format}}")
```

Kellonaikoja koskeva matematiikka on inha koodata käsin. Jos haluat lisätä aikaan `13:37` esimerkiksi `25` minuuttia, niin sinun pitää osata ottaa huomioon, että yksi tunti on 60 minuuttia. Tätä varten Pythonin datetime-moduuli tarjoaa onneksi timedeltan.

```python
import datetime

now = datetime.datetime.now()
delta = datetime.timedelta(hours=1, minutes=15)

# Suorita laskuoperaatio
past = now - delta

print(past.isoformat())
```



!!! warning
    Kellonaikojen käsittely on huomattavan vaikeaa, varsinkin jos mukaan sotketaan eri aikavyöhykkeet ja kesäajat tai kaukana historiassa olevat Juliaaniset sekä Gregoriaaniset kalenterit. Huomaa, että pyörää ei välttämättä kannata keksiä uudestaan. Datetimen ympärille on rakennettu kirjastoja, kuten [Arrow](https://arrow.readthedocs.io/en/latest/), jotka käsittelevät aikoja oletetusti aikavyöhykkeeseen sidottuna.



## Kymmenjärjestelmästä poikkeavat luvut

Bittien käsittely Pythonissa ei ehkä ole aivan jokapäiväistä työtä, mutta perusteet on silti hyvä tietää. Bittien, heksadesimaalin ja desimaalijärjestelmien perusteiden ymmärrys kuuluu tietojenkäsittelytieteiden perusteisiin, joten tämä on viimeistään hyvä vaihe ottaa aihe haltuun.

```python
# Literaali 0b-etuliitteellä
>>> 0b111
7

# Käännä kokonaisluku binäärin merkkijonopresentaatioksi
>>> bin(7)
'0b111'

# ...tai tee sama F-stringillä
>>> f"{7:08b}"
'00000111'
```

Jos sinulla on merkkijono, joka edustaa binääriä, käännä se numeroksi sisäänrakennettua `int()`-konstruktoria käyttäen.

```python
# Binääriä esittävä merkkijono numeroksi
>>> int("00000111", base=2)
7

# Desimaalilukua ...
>>> int("101")
101

# Heksadesimaalia ...
>>> int("65", base=16)
101
```



## Floatin ongelmat

On houkuttelevaa, ja usein käytännöllistä, kutsua float-lukuja suomeksi desimaaliluvuiksi. On tärkeää muistaa, että kyseessä on kuitenkin liukuluku, ja ero on ajoittain merkittävä. Liukulukuihin liittyvä matematiikka on tämän kurssin skoopin ulkopuolella, mutta sen vaikutukset käytännön ohjelmoinnissa on hyvä tuntea. Float-luku kääntyy suomeksi liukuluvuksi ja kyseessä on aina binäärimuotona tallennettu luku, joka esitetään käyttäjälle pyöristetyssä desimaalimuodossa. Siksi yllä Desimaalijärjestelmässä meidän kantaluku on 10, joten jos lisäät mihin tahansa lukuun nollan perään, kerrot sen kymmenellä. Binäärissä kertoisit luvun kahdella. Mikäli poistat nollan, jaat sen kymmenellä. Binäärissä jakaisit sen kahdella. Mikäli luvussa on desimaalierotin (suomessa pilkku, amerikassa piste), erottimen vasemmalla puolella on kokonaisluku, oikealle puolella sen desimaaliosa.

Mikäli desimaaliosan yrittäisi sanallistaa desimaali- ja binäärilukujen osalta, sen voisi tehdä näin:

```
# Kantaluku 10
0.1   = yksi kymmenesosa
0.01  = yksi sadasosa
0.001 = yksi tuhannesosa

# Kantaluku 2
0.1   = puolet
0.01  = neljäsosa
0.001 = kahdeksasosa
```

Koska tietokone tallentaa luvun binäärinä, siihen kohdistuvat binäärilukujärjestelmän rajoitteet. Huomaa, että murtoluku `yksi kolmasosa` on mahdoton esittää desimaalijärjestelmässä desimaalilukuna täydessä tarkkuudessaan. Se on päättymätön `0.33333...`. Kantaluvun kolme järjestelmässä tuo luku olisi yksinkertaisesti `0.1`. Kuinka tämä sitten näkyy käytännössä binäärijärjestelmän lukujen kanssa? Se näkyy pyöristysvirheinä:

```python
>>> 1/10 + 2/10 == 3/10
False

>>> 1/10 + 2/10
0.30000000000000004

>>> print(f"{3/10:.16f}")
0.3000000000000000

>>> print(f"{3/10:.17f}")
0.29999999999999999

>>> round(2.5)
3

>>> num = 0.1
>>> num.as_integer_ratio()
(3602879701896397, 36028797018963968) 
# Pythonin näkökulmasta 0.1 on suunnilleen sama kuin
# kokonaislukujen 3_602_879_701_896_397 ja 2**55 suhde 
```

Jos luot murtolukujen avulla liukulukuja **missä tahansa ohjelmointikielessä**, noudata äärimmäistä varovaisuutta! Suorita pyöristysoperaatio aina vasta viimeisenä, ja mielellään riittävällä tarkkuudella, kuten rahan kohdalla sentteinä. Mikäli tarvitset tieteellisen laskennan tarkkuutta, käytä avuksi kirjastoja kuten Pythonin built-in kirjastot `decimal` tai `franctions`.



## Harjoituksia

### Harjoittele: Nykyhetki Unix-ajassa

Selvitä, paljon jokin valitsemasi kellonaika on Unix-ajassa. Unix-ajalla tarkoitetaan sekunteja (tai joissakin tapauksissa milli-, mikro- tai nanosekunteja) 1970-luvun alusta alkaen. Luku voi olla myös negatiivinen. Voit unohtaa mahdolliset aikavyöhykkeiden tuomat ongelmat tässä harjoitteessa:

```python
import datetime

# Selvitä, mitä argumentteja datetime() kaipaa
event_time = datetime.datetime()

# Selvitä, mitä tämä palauttaa
event_time.timestamp()
```



### Harjoittele: Etsi edellinen maanantai

Kirjoita skripti, joka tulostaa, kuinka monta päivää sitten oli edellinen maanantai, ja mikä kyseinen päivä on kalenterissa (ISO 8601 formaatissa). Tulostuvan lauseen pitäisi olla (`"Last Monday was # days ago: YYYY-MM-DD"`). Jos osaat, tee koodiin muutos, joka tulostaa `"Today is Monday, you silly!"`, jos tänään on maanantai.

```python
import datetime

# Aloita tästä
today = datetime.date.today()
```

??? tip "Vihje"
    Vihje: `weekday()` tai `%w`.



### Harjoittele: Kommentoi IP-osoitefunktiot

Tutustu alla oleviin funktioihin. Kopioi koodi omaan Jupyter Notebookiin tai `.py`-tiedostoon ja kommentoi koodirivit parhaasi mukaan. Kaksi vaikeinta riviä, joissa käsitellään listoja, on kommentoitu jo valmiiksi. Yritä selvittää, mitä muut rivit tekevät: etenkin rivit, joissa tapahtuu bittioperaatiot `<<` ja `&` ja `>>`. Silmukkarakenne `for` käydään läpi myöhemmässä luvussa, joten voi olla, että osa koodista jää hämärän peittoon. Yritä kuitenkin!

Vinkki: `enumerate` numeroi silmukan iteraatiot, eli `index` saa ensimmäisellä kerralla arvon `0`, viimeisellä arvon `4`.

```python
def ip_to_integer(ip_address:str, verbose=False) -> int:
    """Convert IP address into an integer.
    
    Example: 
    >>> ip_to_integer("1.0.0.0")
    16_777_216
    """
    
    # Convert to list "1.2.3.4" => [1, 2, 3, 4]
    ip_parts = [int(x) for x in ip_address.split(".")]
    assert len(ip_parts) == 4, "IP must be in format x.x.x.x"
    total = 0
    
    for index, ip_part in enumerate(ip_parts[::-1]):
        ip_shifted = ip_part << (8 * index)
        total = total + ip_shifted
        if verbose:
            print(
                f"[INFO] {index+1}th from right ({ip}) " 
                f"is in bitshifted binary: {ip_shifted:32b}"
            )
    
    return total


def integer_to_ip(ip_integer: int) -> str:
    """Convert integer into an IP address
    
    Example: 
    >>> integer_to_ip(16_777_216)
    "1.0.0.0"
    """

    assert 0 <= ip_integer <= 2 ** 32 - 1, "Integer should be in range 0-4_294_967_295"
    
    ip_parts = []
    for _ in range(4):
        ip_part = ip_integer & 0b11111111
        
        # Add this part into the list ip_parts
        ip_parts.append(str(ip_part))
        
        ip_integer = ip_integer >> 8

    # Join parts with dot as separator, e.g. [4,3,2,1] -> "1.2.3.4"
    ip_address = ".".join(ip_parts[::-1])
    
    return ip_address
```

Funktioita voi käyttää nyt kääntämään IP-osoitteita ja aliverkon peitteitä kokonaisluvuiksi, ja näiden välillä voi suorittaa bittioperaatioita. Täten voimme tarkistaa, mikä on verkon osoite, jos tiedämme aliverkon peitteen ja IP-osoitteen:

```python
host = ip_to_integer("192.168.131.17")
mask = ip_to_integer("255.255.128.0")

network_address = integer_to_ip(host & mask)
print(network_address)
# Kokeile, mitä tämä tulostaa!
```

Huomaathan, että esimerkki on äärimmäisen naiivi. Se sallii epäkelpoja aliverkon peitteitä (esim. `255.128.255.0`). Pythonin `ipaddress`-kirjasto hoitaa saman tehtävän vähemmän naiivisti ja käyttää olio-ohjelmoinnin keinoja. Kirjaston dokumentaatio löytyy [Python Docs: ipaddress — IPv4/IPv6 manipulation library](https://docs.python.org/3/library/ipaddress.html).

!!! question "Tehtävä"
    Yritä kirjoittaa muutama rivi koodia, jotka varmistavat, että verkon peite (eli mask) kelpaa oikeasti peitteeksi. Sovitaan, että peitteen pitää sisältää `8-29` ykköstä ja loput nollia eli sallitaan CIDR:t `/8 - /29`. Jos CIDR ei ole tuttu käsite, käväise esimerkiksi [Wikipedia: Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#IPv4_CIDR_blocks). Vasemmalta alkavien ykkösten välissä ei saa siis olla yhtään nollaa, mikä tarkoittaa että `255.0.255.0` maskin pitäisi nostaa AssertionError! Käytä tähän `assert something_that_should_be_true` muotoa, kuten yllä olevissa esimerkeissä.
