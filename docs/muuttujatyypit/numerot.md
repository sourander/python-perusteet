Pythonin tyypillisimmin käytössä olevat numeraaliset tietotyypit ovat kokonaisluku eli integer (`int`) sekä desimaaliluku eli floating point number (`float`). Pythonissa on myös kompleksiluku (`complex`), mutta se jätetään tässä materiaalissa käsittelemättä. Vahvasti tyypitetyissä kielissä, kuten C ja Java, on eri kokoisille luvuille omat muuttujatyyppinsä. Esimerkiksi pieniä lukuja varten, jotka mahtuvat välille `-128...127`, on oma muuttujatyyppintä byte. 1, 2, 3 ja 4-tavuisia numeroita varten ovat erikseen byte, short, int ja long. Pythonissa kaikkia näitä varten käytetään samaa tyyppiä: `int`. Myös `float` aina aina float, eikä eriksee 4- tai 8-tavuinen `float` tai `double`.

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

## Operaatiot

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
| >, <, >=, <= | `"2.51 > 2`  |

### Loogiset

| Operaattori | Esimerkki |
| ----------- | --------- |
| and         | `2 and 3` |
| or          | `0 or 42` |
| not         | `not 0`   |

!!! question "Tehtävä"
    Kokeile kaikki yllä olevat operaattorit läpi. Selvitä, mitä ne tekevät. Loogiset operaattorit, saattavat tuntua lukujen kanssa epäloogisilta. Ota selvää!

### Bitti

| Operaatio |                   |              |
| --------- | ----------------- | ------------ |
| &         | AND               | `0b1 % 0b1`  |
| \|        | OR                | `0b0 OR 0b1` |
| ^         | XOR               | `0b1 ^ 0b0`  |
| ~         | NOT               | `~ 0b0111`   |
| <<        | Siirto vasemmalle | `0b1 << 1`   |
| >>        | Siirto oikealle   | `0b10 >> 1`  |

!!! tip
    Näistä on esimerkkejä alempana tässä samassa luvussa. 



## Numerot ja F-string

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

Otetaan heksadesimaalimuunnos hyötykäyttöön, ja muokataan yllä olevaa Unicode plane -tulostinta. Alla sama koodi muokattuna siten, että se tulostaa numerot heksadesimaaleina. Luku vie aina vähintään 6 merkkiä; täytteenä toimii välilyöntimerkki:

```python
for section in range(17):
    start = (2 ** 16 * section)
    end = start + 2 ** 16 - 1
    
    print(f"{section:<2} {start:6x} {end:6x}")
```



!!! question "Tehtävä"
    Päättele yllä olevien avulla, kuinka käännät luvun binääriksi ja tulostat 8 merkkiä pitkänä. Luvusta 127 pitäisi tulostua `01111111`, mukaan lukien ensimmäinen nolla. Vihje: `b`.

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

Jos sinulla on merkkijono, joka edustaa binääriä, käännä se numeroksi sisäänrakennettua `int()`-funktiota.

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



## Harjoituksia

### Kommentoi IP-osoitefunktiot

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
