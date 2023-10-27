Ehtolause on lause, joka suoritetaan vain jos jokin ehto on tosi. Ehtolauseet kuuluvat käytännössä kaikkiin ohjelmointikieliin. Pythonissa ehtolauseet ovat `if`, `elif` ja `else`-lauseita. Näistä viimeisin eli `elif` on lyhenne sanoista `else if`. 

Tuoreemmissa Python-versioissa (3.10+) on myös match-lause, joka on käytännössä sama asia kuin switch-case muissa kielissä.

## Lausekkeet

### If

If-ehtoa voi käyttää yksistään ilman elif tai else-lauseita. Tällöin if-lause suoritetaan vain jos ehto on tosi. Esimerkkejä:

```python
if True:
    print("Tämä suoritetaan")

something_that_returns_true = True
if something_that_returns_true:
    print("Tämäkin suoritetaan")

pets = ["cat", "dog", "fish"]
if "cat" in pets:
    print("Kissa löytyy")
```

Ajoittain on hyödyllistä käyttää `not`-avainsanaa, joka kääntää ehtolauseen tuloksen. Esimerkki:

```python
if not user.get_login_status():
    user.login()
```

### Elif ja else

Elif-lause suoritetaan vain jos if-lauseen ehto on epätosi ja elif-lauseen ehto on tosi. Else-lause suoritetaan vain jos if- ja elif-lauseiden ehdot ovat epätosia. Esimerkki:

```python
pets = ["cat", "dog", "fish"]

if "cat" in pets:
    print("Kissa löytyy")
elif "dog" in pets:
    print("Koira löytyy")
else:
    print("Ei löytynyt")
```



### Match

Match-lause on uusi Python 3.10:ssä. Se on käytännössä sama asia kuin switch-case muissa kielissä. Esimerkki:

```python
response = requests.get("http://example.com")

match response.status_code:
    case 200:
        do_something(response.data)
    case 404:
        logging.error("Not found")
    case _:
        return logging.critical("Unknown error")
```

!!! warning

    Muistathan, että match vaatii Pythonin versiota 3.10 tai uudempaa. Tämä on riski käyttää esimerkiksi automaatiskriptissä, joka ajetaan eri koneilla.


## Hyviä käytänteitä

### Vältä vaikeita ehtoja

Vältä `and` ja `or` sanojen liiallista käyttöä if-lausekkeessa, varsinkin yhdistettynä monimutkaisiin, sulkuja vaativiin ehtoihin. Yleensä logiikan voi purkaa helpommaksi.

```python
if a or b or c or d or e:
    do_this()

if a and b and c and d and e:
    do_that()
```

Ajoittain tämän voi ratkaista `any` tai `all` funktioiden avulla.

```python
reasons = (a, b, c, d, e)

# Any
if any(reasons):
    do_this()

if all(reasons):
    do_that()
```

### Vältä sisäkkäisyyttä

Alla esimerkki sisäikkäisistä if-lausekkeista, joka on kohtalaisen vaikea lukea:

```python
def drink_milk(person, fridge):
    if person.is_thirsty():
        if fridge.has_milk():
            person.stomache.add(fridge.get_milk())
        else:
            raise NoMilkError("No milk in fridge")
    else:
        raise NotThirstyError("Person is not thirsty")
```

Tämän sisäkkäisen if-lausekkeen voi purkaa 1-ulotteisiksi if-lauseiksi:

```python
def drink_milk(person, fridge):
    if not person.is_thirsty():
        raise NotThirstyError("Person is not thirsty")

    if not fridge.has_milk():
        raise NoMilkError("No milk in fridge")

    person.stomache.add(fridge.get_milk())
```

## Harjoituksia

### Harjoittele: With

Alla on Python-luokka, joka toteuttaa context manager -yhteensopivan interacen eli `__enter__` ja `__exit__` metodit.

```python
class MyContextManager:
    def __init__(self):
        print("Init")

    def __enter__(self):
        print("Enter")

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exit")
```

Käytä tätä context manageria with-lauseen kanssa. Mitä tapahtuu?

```python
my_manager = MyContextManager()

with my_manager:
    print("Doing something with My Manager")
```