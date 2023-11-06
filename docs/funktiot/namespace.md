Pythonissa on useita nestattuja namespace skooppeja, muistisäännöltään LEGB, jotka ovat:

* L: Local
* E: Enclosing
* G: Global
* B: Built-in

Alla näkyvässä koodissa on moduulin `__main__` lokaali funktio nimeltään `outer_func`. Tuon funktion lokaaliin scopeen kuuluu funktio nimeltään `inner_func`. Tämän funktion lokaaliin skopeen kuuluu taas yhden tason sisäkkäisempi funktio `innermost_function`. Kaikista sisimmän funktion näkökulmasta muuttuja `x` on määritetty kolmessa eri scopessa: local, enclosing, global.

```python
def outer_func():

    def inner_func():
        def innermost_func():
            # Innermost func scope
            x = 4
            print("Innermost func sees: ", x)
        
        # Inner func scope
        x = 3
        innermost_func()
        
    # Outer func scope
    x = 2
    inner_func()

# Global scope
x = 1

outer_func()
```

!!! question "Tehtävä"

    Kommentoi rivit seuraavassa järjestyksessä:

    * `x = 4`
    * `x = 3`
    * `x = 2`

    Mitä tulostuu ja miksi?

## Globaalin funktion muuttaminen

Alla oleva koodin funktio tulostaa x:n, joka löytyy sen globaalista skoopista. Tämän jälkeen se yrittää sijoittaa kokonaisluvun kaksi tuohon globaaliin muuttujaan.

```python
def problematic_func():
    print(x)
    x = 2

x = 1
problematic_func()
```

!!! warning

    Yllä oleva nostaa UnboundLocalError virheen. Ylemmän tason muuttujien ei onnistu sisemmässä skoopissa.

On mahdollista, mutta ei missään nimessä suositeltua, muuttaa globaalia muuttujaa sisemmässä skoopissa. Tämä onnistuu `global` avainsanalla.

```python
def problematic_func():
    global x
    print(x)
    x = 2

x = 1
problematic_func()
```

!!! tip

    Muistutus: tämä EI ole suositeltua. Syötä muuttuja x mieluummin argumenttina funktiolle ja palauta uusi arvo. Tämä esitellään myöhemmin kurssilla.

## Moduulien skooppi

Ota huomioon, että kullakin moduulilla on oma skooppinsa. Alla esimerkki kahden tiedoston Python-ohjelmasta:

```python
# b.py
x = 'B'

def func():
    print(x)
```

```python
# a.py
from b import func

x = 'A'
func()
```

!!! question "Tehtävä"

    Mitä yllä oleva koodi tulostaa? Aja shellissä `python a.py` ja tarkista.

    Kokeile myös kommentoida rivi `x = 'B'` ja selvitä, mitä tapahtuu. Tulostuuko kutsuvan moduulin `x` eli ("A") vai tuleeko error?

## Harjoituksia

### Harjoittele: Globals ja Locals

Selvitä, mitä sisäänrakennetut funktiot globals() ja locals() tulostavat. Kokeile ajaa niitä eri namespace skoopeissa.

```python
# Mikä tämä on?
globals()

# Entä tämä?
locals()
```

