
## Syntaksi

Pythonissa funktio määritellään `def`-sanan avulla. Mikäli funktio on määritelty luokan (Class) sisällä, siitä käytetään nimeä metodi. Funktio voi palauttaa arvon `return`-sanan avulla. Mikäli funktio ei palauta mitään, palauttaa se automaattisesti `None`-arvon eli NoneTypen.

```python
def my_function():
    return 1
```

!!! tip

    Funktiot ovat tapa modularisoida koodia ja vähentää toistoa. Pyri pilkkomaan koodisi pieniin, toiminallisiin kokonaisuuksiin. Tämä helpottaa koodin ylläpitoa ja testaamista.

## Parametrit ja Argumentit

### Perusteet

Argumenttien ja parametrien terminologia menee herkästi sekaisin: yleensä kuulija kuitenkin ymmärtää, mitä tarkoitat, jos käytät näitä ristiin. Argumentti on funktiolle syötettävä arvo funktion näkökulmasta. Kun funktiota kutsutaan, sille syötetään parametreja.

Funktion määrittelyrivillä on mahdollista luoda kahdenlaisia argumentteja: sellaisia, joilla ei ole oletusarvoa, ja sellaisia, joilla on.

* Pakolliset, positionaaliset argumentit
    * Tunnetaan yleensä nimellä: args
    * Ei oletusarvoa
* Valinnaiset argumentit
    * Tunnetaan yleensä nimellä: kwargs
    * Oletusarvo

```python
def my_function(a:int, b:float, name="kissa", age=42):
    print(f"{a=}")
    print(f"{b=}")
    print(f"{name=}")
    print(f"{age=}")
```

Huomaa, että kaikki positionaaliset argumentit on pakko antaa, tai funktio nostaa TypeErrorin.

```python
>>> my_function()
TypeError: my_function() missing 2 required positional arguments: 'a' and 'b'

>>> my_function(42)
TypeError: my_function() missing 1 required positional argument: 'b'

>>> my_function(42, 3.14)
a=42
b=3.14
name='kissa'
age=42

>>> my_function("42", 3, name="Bond", age="Double-oh-seven") # (1)
a='42'
b=3
name='Bond'
age='Double-oh-seven'
```

1. HUOM! Python ei tarkista argumenttien tyyppejä, vaan antaa niiden olla mitä tahansa. Käyttämäsi IDE saattaa varoittaa tästä, mikäli type hintsit ovat paikoillaan, mutta Python ei itse tarkista niitä.

### N-kappaletta parametreja

Tämä syntaksi vaatii hieman muistinvirkistystä tupleista. Mikäli et muista miten sekvenssien pakkaus ja purku (packing, unpacking) käyttäytyvät, käy lukemassa seuraava artikkeli: [Sekvenssit](../muuttujatyypit/sekvenssit.md)

```python
def sum_all_args(*args: int):
    print(args)
    total = sum(args)
    print(total)
```

```python
>>> sum_all_args(1, 2, 3, 4, 5)
(1, 2, 3, 4, 5)
15
```

### N-kappaletta nimettyjä parametreja

Myös dictionaryyn ja keyword argumentteihin liittyy samanlainen unpack-syntaksi. Tosin, toisin kuin sekvenssien purku, tätä ei juuri tarvitse muualla kuin funktioiden argumenteissa. Purku avaa sanakirjan avaimet ja arvot keyword argumenteiksi.

Katsotaan ensin, kuinka tätä voi käyttää syöttämään funktiokutsussa käytetyt parametrit sanakirjasta.

```python
# Funktio, joka ottaa 3 oletusarvollista argumenttia
def my_function(a=1, b=2, c=3):
    print(f"{a=}")
    print(f"{b=}")
    print(f"{c=}")
```

```python
>>> data = {"a": 10, "b": 20, "c": 30}
>>> my_function(**data)
a=10
b=20
c=30
```

Kun yllä olevan toiminnan hyväksyy, on helppo hyväksyä, että myös seuraava toimii:

```python
def print_all_kwargs(**kwargs):
    for key, value in kwargs.items():
        print(f"{key} = {value}")
```

```python
>>> print_all_kwargs(z=1, x=2, y="Kissa")
z = 1
x = 2
y = Kissa
```

## Palautusarvo

Hyvin tyypillisesti, mutta ei suinkaan aina, funktio palauttaa jonkin arvon tai joitakin arvoja. Tämä hoituu return-sanalla. Kun return-lauseke suoritetaan, funktio lopettaa välittömästi suorituksensa ja palauttaa arvon.

```python
def my_function():
    return 1
    print("This will never be printed")
```

Aivan kuten argumenttien kanssa, myös palautusarvojen kanssa voi käyttää tyyppivihjeitä.

```python
def my_function() -> int:
    return 1
```

Mikäli palautat monta asiaa kerralla, ne tulevat tuplena funktion kutsujalle.

```python
def my_function() -> tuple[int, int, int]:
    return 1, 2, 3
```

Palautuva arvo voi olla myös montaa eri tyyppiä riippuen käyttäjän syötteestä tai jostakin muusta tekijästä riippuen. Yksi tyypillinen case on se, että funktio palauttaa joko jonkin etukäteen päätetyn tietotyypin mukaisen aron tai `None`-arvon - eli NoneTypen.

```python
# Python 3.10 ja uudemmat
def my_function() -> int | None:
    if random.randint(0, 1):
        return None
    else:
        return 1

# Vanhemmat Pythonit
def my_function() -> Union[int, None]:
    if random.randint(0, 1):
        return None
    else:
        return 1
```

## Harjoituksia

### Harjoittele: Tulosta kaikki argumentit

Alla on funktio, joka ottaa vastaansa huiman määrän erilaisia argumentteja. Toteuta sille sisältö, joka tulostaa kaikki argumentit.

```python
def print_all_args(a, b, *args, n="abc", m="def", **kwargs):
    # Toteuta sisältö tähän

# Kutsu sitä seuraavilla argumenteilla
print_all_args(1, 2, 3, 4, 5, 6, m="1", n="2", o="2", y="4")

# Varmista, että se toimii myös vain pakollisilla
print_all_args(1, 2)
```