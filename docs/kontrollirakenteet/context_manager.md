With-lause on Pythonin tapa käsitellä resursseja, jotka pitää sulkea käytön jälkeen. Sitä voi käyttää kaikkien sellaisten olioiden kanssa, jotka toteuttavat `__enter__` ja `__exit__` metodit. Termi tälle on `context manager`. Se on hyödyllinen muun muassa silloin, kun käsitellään tiedostoja, tietokantayhteyksiä tai muita resursseja, jotka pitää sulkea käytön jälkeen.

Useiden eri dokumentaatioiden kirjastot neuvovat käyttämään with-lauseketta, joten se on hyvä tuntea, vaikka sen sielunelämään ei perehtyisikään.

```python
# Vaihtoehto 1: Käytä with-lausetta
with open("file.txt", "r") as f:
    print(f.read())

# Vaihtoehto 2: Avaa ja sulje tiedosto itse
f = open("file.txt", "r")
try:
    file.write('Hola!')
finally:
    file.close()
```

## Harjoituksia

### Harjoittele: MyContextManager

Alla on esiteltynä luokka MyContextManager, joka toteuttaa with-lausekkeen vaatimat metodit `__enter__` ja `__exit__`. Käytä tätä context manageria with-lauseen kanssa. Mitä tapahtuu?

```python
class MyContextManager:
    def __init__(self):
        print("Init")

    def __enter__(self):
        print("Enter")

    def __exit__(self, exc_type, exc_value, traceback):
        print(f"Exit ({exc_type}, {exc_value}, {traceback})")
```

1. Kutsu context manageria with-lauseen kanssa siten, että tulostat lausekkeen keskellä "Hello from the with block". Missä järjestyksessä tulostuvat Init, Enter ja Exit sekä tulostamasi arvo?
2. Kutsu context manageria uusiksi siten, että teet with-lausekkeen sisällä jotain laitonta, kuten `x = 10 / 0`. Mitä arvoja exc_type, exc_value ja traceback saavat?