
Komentoriviargumenttien käsittely on tärkeä osa ohjelmointia. Tässä osiossa harjoitellaan komentoriviargumenttien käsittelyä Pythonissa. Pythonissa on sisäänrakennettu argparse-moduuli, joka on hyvä tapa aloittaa. Karvalakkimalli olisi parsia argumentit samalla tavalla kuin esimerkiksi Bash-skripteissä. Tämä tapa on esitelty alla:

```python
import sys
script_name = sys.argv[0]
arguments = sys.argv[1:]
```

!!! warning

    Ellei sinulla ole vahvaa syytä, älä parsi argumentteja käsin. Käytä mieluummin argparse-moduulia, joka esitellään alla.

## Positionaaliset argumentit

```python
# a.py
import argparse

parser = argparse.ArgumentParser(description="Kuvaus ohjelmalle")
parser.add_argument("argumentti", type=int, help="Kuvaus positionaaliselle argumentille")
args = parser.parse_args()

print(args.argumentti)
```

!!! question "Tehtävä"

    Yllä näkyy tiedoston `a.py` sisältö. Luo tiedosto ja kokeile seuraavia neljää komentoa:

    ```bash
    python a.py
    python a.py --help
    python a.py kissa
    python a.py 1
    ```

## Valinnaiset argumentit

Positionaalisten argumenttien sijasta (tai lisäksi) on mahdollista luoda valinnaisia argumentteja. Tämä onnistuu seuraavasti:

```python
# b.py
import argparse

parser = argparse.ArgumentParser(description="This program calculates the area or volume")
parser.add_argument("x", type=int, help="Width of the shape")
parser.add_argument("y", type=int, help="Height of the shape")
parser.add_argument("-t", "--type", type=str, help="The name of the shape", choices=["rectangle", "triangle"], default="rectangle")
args = parser.parse_args()

if args.type == 'triangle':
    print(f"The area of the triangle is {(args.x * args.y) / 2}")
else:
    print(f"The area of the rectangle is {args.x * args.y}")
```

!!! question "Tehtävä"

    Yllä näkyy tiedoston `a.py` sisältö. Luo tiedosto ja kokeile seuraavia komentoja:

        ```bash
        python b.py
        python b.py --help
        python b.py 1 2
        python b.py 1 2 -t triangle
        python b.py 1 2 --type triangle
        python b.py --type triangle 1 2
        python b.py 1 2 -t triangle -t rectangle
        python b.py 1 2 -t kissa
        ```
## Harjoituksia

### Harjoittele: Click

Argparse on näppärä Pythonin sisäänrakennettu moduuli, mutta se ei ole ainoa. Kokeile sen kilpailijaa `Click`, jonka dokumentaatio löytyy [täältä](https://click.palletsprojects.com/en/8.1.x/).

Asenna kirjasto ja kokeile sitä.

### Harjoittele: Typer

Click on näppärä, mutta tiangolo on luonut sen pohjalta vielä korkeamman tason abstraktion kirjaston. Sen nimi on `Typer`, ja sen dokumentaatio löytyy [täältä](https://typer.tiangolo.com/). 

Asenna kirjasto ja kokeile sitä.