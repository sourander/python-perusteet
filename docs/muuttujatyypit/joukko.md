Pythonin built-in tyyppi joukko eli `set` on järjestämätön kokoelma. Joukon entiteeteillä ei siis ole indeksiä, toisin kuin aiemmin tututuiksi tulleilla listalla ja tuplella. Lisäksi joukko voi sisältää vain uniikkeja arvoja. 

## Joukon luonti

```python
# Parittomien <=10 lukujen joukko
>>> {1, 3, 5, 7, 9}
{1, 3, 5, 7, 9}

# Parillisten "0 < x < 11" lukujen joukko
>>> set(range(2, 11, 2))
{2, 4, 6, 8, 10}

# Merkkijonoista koostuva joukko
>>> commons_pets = {"cat", "dog", "parrot", "python"}
>>> "parrot" in commons_pets
True

# Huomaa, että joukon jäsenet voivat olla keskenään eri tyyppiä
>>> {"meaning", 42, .5}
{0.5, 42, 'meaning'}
```

Joukkoon lisättävän entiteetin tulee olla häshättävää tyyppiä. Duplikaatit tunnistetaan häshin avulla ja ne poistetaan. Tämän takia listasta, joka sisältää duplikaatteja, voi luoda helposti uniikkien arvojen setin:

```python
>>> set([1, 1, 1, 2, 2, 3])
{1, 2, 3}
```

!!! tip
    Aiempi muistisääntö LSD, jolla tunnistaa mutable eli muutettavat tietotyypit, pätee myös tähän. Häshäämättömät tietotyypit ovat LSD eli: list, set, dictionary.

Joukkoa ei voi indeksoida, slicettää tai käyttää LIFO-tyylisenä (List In, First Out) jonona. Juokko on kuitenkin huomattavan hyödyllinen, kun haluat tutkia, millaisista alkioista jokin populaatio koostuu, tai miten kaksi eri populaatiota vertautuvat toisiinsa.



## Operaatiot

### Aritmeettiset ja Vertailu

Nämä voi unohtaa joukkojen kanssa. Esimerkiksi `{1, 2, 3} + {4, 5}` ei toimi. Valtaosa vertailuoperaattoreista on siirretty uuteen, joukko-operaatioiden käyttöön. Yhteläisyys eli `a == b` toimii kuitenkin yhä arvattavalla tavalla: se tarkistaa, että kaksi joukkoa ovat täysin samat.

### Loogiset

Nämä käyttäytyvät samalla tavalla kuin sekvenssien kanssa. `set_a or set_b or set_c` palauttaa ensimmäisen joukon, jonka pituus eli `len()` ei ole 0.

### Joukko

Joukko tukee aivan omanlaisiaan operaatioita, jotka saattavat olla sinulle ennestään tuttuja matematiikasta. Mikäli olet jo opiskellut SQL:ää, saatat tunnistaa yhtenäisyyttä näissä JOIN-operaatioihin sekä SQL-komentoon DISTINCT.

| Operaatio                   | Vaihtoehto         | Selite                                                       |
| --------------------------- | ------------------ | ------------------------------------------------------------ |
|                             | `a == b`           | Joukot a ja b ovat täysin samat. Ei varsinaisesti joukko-operaatio, mutta on hyvä esitellä tässä yhteydessä. |
| `a.isdisjoint(b)`           |                    | Palauttaa True, jos joukoilla ei ole yhteisiä jäseniä.       |
| `a.issubset(b)`             | `a < b`            | Palauttaa True, jos joukko a kuuluu kokonaisudessaan joukkoon b |
| `a.issuperset(b)`           | `a > b`            | Palauttaa True, jos joukko b kuuluu kokonaisudessaan joukkoon a |
| `a.union(b, c, ...)`        | `a | b | c  | ...` | Palauttaa joukkojen unionin eli yhdisteen eli joukon, johon kuuluvat kaikkien joukkojen uniikit alkiot. |
| `a.intersection(b, c, ...)` | `a & b & c & ...`  | Palauttaa joukon alkioista, jotka kuuluvat kaikkiin joukkoihin. |
| `a.difference(b, c, ...)`   | `a - b - c - ...`  | Palauttaa joukkoerotuksen eli alkiot, jotka kuuluvat joukkoon a, mutta eivät muihin joukkoihin. |
| `a.symmetric_difference(b)` | `a ^ b`            | Palauttaa ne alkiot, jotka ovat a:ssa mutta eivät b:ssä, ja ne, jotka ovat b:ssä mutta eivät a:ssa. |



## Harjoittele



### Harjoittele: Joukko-operaatiot

Sinulla on jo valmiiksi `requests`-kirjasto, koska se asentuu Jupyter Notebookin riippuvuutena. Kokeillaan käyttää sitä. Aloitetaan noutamalla 10 käyttäjää ja 100 postausta JSON Placeholder -sivustolta, joka tarjoilee dummy-dataa REST-rajapinnan yli.

```python
import requests

users_url = "https://jsonplaceholder.typicode.com/users"
posts_url = "https://jsonplaceholder.typicode.com/posts"
comments_url = "https://jsonplaceholder.typicode.com/comments"

users = requests.get(users_url).json()
posts = requests.get(posts_url).json()
comments = requests.get(comments_url).json()
```

Tutki, mitä kysyiset muuttujat sisältävät. Ne ovat tyyppiä `List[dictionary]`, ja dictionary joka esitellään seuraavassa luvussa. Käännetään se muotoon `List[int]`, jossa kokonaisluku on käyttäjän id.

```python
user_ids = [x["id"] for x in users]
post_user_ids = [x["userId"] for x in posts]

user_emails = [x["email"].lower() for x in users]
comment_user_email = [x["email"].lower() for x in comments]
```

Todista joukko-operaatioita käyttäen seuraavat väitteet:

1. Kaikki rekisteröityneet käyttäjät ovat luoneet vähintään yhden postauksen
2. Kukaan rekisteröitynyt käyttäjä ei ole kirjoittanut kommenttia omalla sähköpostillaan.



### Harjoitus: Frozenset

Joukko eli set kuuluu yllä mainittuun muistisääntöön LSD. Joukko ei siis voi kuulua joukkoon. Jos kuitenkin haluat luoda joukon joka koostuu useista joukoista, tulee sinun käyttää joukon muuttumatonta (immutable) varianttia nimeltään `frozenset`.

```python
odds = frozenset(range(1, 11, 2))
evens = frozenset(range(2, 11, 2))
odds_and_evens = {odds, evens}
```

Keksi jokin populaatio, joka koostuu pienemmistä populaatioista, ja toteuta se joukkona jäädytettyjä settejä. Yksi kuvitteellinen esimerkki, josta voi olla hyötyä, on pizza. Alla esimerkki, joka sallii käyttäjän valita pizza-aineksia. Tutki, mitä ohjelma tekee.

```python
# Define the constant, available ingredients
INGREDIENTS = [ "Egg", "Ham", "Pineapple"]

def print_menu():
    for i, ingredient in enumerate(INGREDIENTS, start=1):
        print(f"{i:>3}  {ingredient}")

def prompt_pizza() -> frozenset:
    
    # Default pizza.
    pizza_combination = {"Tomato sauce", "Cheese"}

    # Prompt
    print("Enter comma-seprated ingredients (e.g. 1,2,4) or press enter to finish: ")
    user_input = input()
    print(user_input)
    wanted_ingredients = [int(x) for x in user_input.split(",") if x]

    for index in wanted_ingredients:
        index = index - 1  # list if zero-indexed
        
        if index in range(len(INGREDIENTS)):
            pizza_combination.add(INGREDIENTS[index])
        else:
            print(f"Sorry, do not have ingredient #{index + 1}. Decided to add spam instead.")
            pizza_combination.add("Spam")
        
    return frozenset(pizza_combination)

def user_wants_to_continue() -> bool:
    print("Do you want to order another pizza? (yes/no)")
    another_pizza = input().lower()
    return another_pizza == "yes"
  
  
# Initialize
unique_pizzas_ordered = set()
print_menu()

while True:
    pizza = prompt_pizza()
    
    print("Adding pizza to unique orders:", pizza)
    unique_pizzas_ordered.add(frozenset(pizza))

    if not user_wants_to_continue():
        break

print("\nAll pizza combinations ever ordered:")
for combination in unique_pizzas_ordered:
    print(", ".join([x for x in combination]))
```

