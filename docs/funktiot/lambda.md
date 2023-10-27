Lambda-funktiot ovat "one-liner"-ihmeitä. Lambda-funktioita voi kutsua myös termillä *anonymous functions*. Niiden käytön kanssa kannattaa olla maltillinen. Lambda-funktiot ovat helposti melko vaikealukuisia.

## Syntaksi

Lambda-funktion syntaksi on seuraava:

```python
lambda arguments: expression
```

## Funktiosta lambdaksi

```python
# Tämä funktio
def add(x, y):
    return x + y

# vastaa tätä lambda-funktiota
add = lambda (x, y): x + y
```

## Lambda kertakäyttöisenä funktiona

Lambda on usein hyötykäytössä listan sorttaamisessa tai muussa vastaavassa käyttötarkoituksessa, jossa simppeli funktio syötetään jonkin toisen funktion tai metodin parametriksi (eli ikään kuin callback funktiona). 

Alla esimerkki, jossa lista sortataan sen sisältämien sanakirjojen avaimen mukaan. Huomaa, että kyseistä lambda-fuktiota ei ole koskaan sijoitettu muuttujaan, eikä sitä tarvitsekaan.

```python
my_list = [
    {"name": "John", "age": 25},
    {"name": "Jane", "age": 24},
    {"name": "Bob", "age": 27},
]

my_list.sort(key=lambda x: x["name"])
```

