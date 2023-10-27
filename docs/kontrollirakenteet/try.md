Pythonissa on tyypillistä "tehdä ensin ja pyytää tarpeen mukaan anteeksi". Tähän käytetään try-except-finally -lauseketta. Varsinkin ulkopuolisen rajapinnan, kuten jonkin palvelun REST API:n, käyttö on aina virheherkkää.

* Verkko voi olla alhaalla
* Palvelin voi olla nurin
* Sertifikaatti on voinut mennä vanhaksi
* Token on voinut mennä vanhaksi
* Palvelin saattaa olla kiireinen ja palauttaa HTTP status 503:n
* ...tai jotain muuta!

Sokkona luottamisen sijasta on turvallisempaa kääriä API-kutsu try-lausekkeen sisään ja käsitellä mahdolliset virheet except-lausekkeessa. Tämän jälkeen koodi jatkaa suoritusta normaalisti. Muutoin mahdollinen virhetilanne, josta syntyy jokin Exception, kaataa sinun Python-sovelluksen suorituksen.

## Peruskäyttö

Try-lauseketta käyttäessä vähintään yksi except-lauseke on pakollinen. Finally on valinnainen eikä sitä tarvitse läheskään aina. Finally-lausekkeen sisällä voi esimerkiksi sulkea tietokantayhteyden tai tiedoston, joka on avattu try-lausekkeen sisällä, tai suorittaa jotakin muuta puhdistusta.

```python
try:
    # Do something
    pass
except:
    # Handle exception
    pass
finally:
    # Do something after try-except
    pass
```

Alla yksinkertainen esimerkki, joka kaatuu tässä tapauksessa ZeroDivisionErroriin. Mikäli koodi kaatuisi mihin tahansa muuhun virheeseen, seuraava except-blokki ottaa sen vastaan, tulostaa viestin ruudulle, ja lopulta nostaa virheen. Virheiden tarkempi käsittely ja lokiin kirjoittaminen on seuraavien Python-kurssien aihe.

```python
try: 
    x = 10 / 0
except ZeroDivisionError:
    print("You can't divide by zero!")
except Exception as e:
    print("Something else went wrong! Error: " + str(e))
    raise
```

## Pidempi esimerkki

Jotta virheen synnyn ymmärtäisi, tulee kurkata sen kirjaston dokumentaatiota (tai lähdekoodia), jota olet käyttämässä. Pythonissa on täysin sallittua luoda omia virheitä, joten et voi lähtökohtaisesti tietää, mitä virheitä ajamasi kirjasto voi nostaa. Alla esimerkkikoodia, joka edustaa ovea, joka on ehkä lukossa, ehkä ei. Mikäli oven yrittää tiirikoida auki, voi tiirikka mennä rikki.

Käyttäjä saa itse asettaa oven lukossa olemisen mahdollisuuden sekä tiirikan rikkoutumisen mahdollisuuden.

```python
import random 

class DoorLockedException(Exception):
    pass

class LockpickBrokeException(Exception):
    pass

class Door:
    def __init__(self, locked_chance: float, lockpick_break_chance: float):
        self.locked = random.random() < locked_chance
        self.lockpick_break_chance = lockpick_break_chance
        self.closed = True

    def open(self):
        if self.locked:
            raise DoorLockedException()
        else:
            self.closed = False

    def lockpick(self):
        if random.random() < self.lockpick_break_chance:
            raise LockpickBrokeException()
        else:
            self.locked = False
    
    def is_closed(self) -> bool:
        return self.closed
```

Alla koodi, joka pyrkii avaamaan oven ensin ihan vain nykäisemällä. Tämän jälkeen oven tiedetään olevan lukossa, joten jatkossa pitää yrittää tiirikkaa.

```python
# Kokeile muuttaa locked_chace ja lockpick_break_chance arvoja
door = Door(locked_chance=0.95, lockpick_break_chance=0.80)

# Yritetään kerran ilman tiirikkaa, loput tiirikalla
retries = 6
we_know_it_is_locked = False


for retry in range(retries):
    try:
        if we_know_it_is_locked:
            print("Kokeillaan tiirikkaa")
            door.lockpick()
        door.open()
    except DoorLockedException:
        print("Ovi on lukossa. Kaivetaan tiirikat pussista.")
        we_know_it_is_locked = True
    except LockpickBrokeException:
        print("... murtovälineet meni rikki, yritetään uudestaan")
    except:
        print("Jotain meni pieleen, softassa on vikaa vikaa vikaa...")
        raise

    if not door.is_closed():
        print(f"[SUCCESS] Ovi on auki. Vaati {retry} tiirikkaa.")
        break
else:
    print(f"[FAILURE] Ovi ei auennut {retry} tiirikalla.")
```