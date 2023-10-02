Pythonin tyypillisimmin käytössä olevat numeraaliset tietotyypit ovat kokonaisluku eli integer (`int`) sekä desimaaliluku eli floating point number (`float`). Pythonissa on myös kompleksiluku (`complex`), mutta se jätetään tässä materiaalissa käsittelemättä.

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



## Numerot ja F-string

Numeroita voi muotoilla F-stringin avulla. Kokeile ajaa alla oleva koodi, joka tulostaa edellisestä luvusta tutut Unicode-planet.

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

!!! question "Tehtävä"
    Päättele yllä olevien avulla, kuinka käännät luvun binääriksi ja tulostat 8 merkkiä pitkänä. Luvusta 127 pitäisi tulostua `01111111`, mukaan lukien ensimmäinen nolla. Vihje: `b`.



## Kymmenjärjestelmästä poikkeavat luvut

TODO. Heksa-, binääri- ja desimaalimuunnokset tähän.