Generaattorit on hyvä tunnistaa, vaikka niitä ei vielä itse kirjoittaisikaan. Generaattorilla voi tyypillisesti korvata luokkana kirjoitetun iteraattorin, ja syntaksi on lyhyempi. Kumpaakin yhdistää se, että iteroitavien asioiden listaa ei tarvitse koskaan luoda kokonaan muistiin, vaan niitä voi käsitellä yksi kerrallaan. Tätä kutsutaan *lazy evaluationiksi*.

## Generaattorin syntaksi

Generaattorin syntaksi on hyvin samanlainen kuin funktioiden. Ainoa ero syntaksissa on, että funktioiden `return`-lauseke korvataan `yield`-lausekkeella.

```python
def my_generator():
    yield 1
    yield 2
    yield 3
```

Tätä generaattoria voi käyttää kuten iteraattoria, eli kutsua `my_generator().__next__()`, kunnes funktio nostaa StopIteration-exceptionin. Tämä tapahtuu automaattisesti, jos funktion ajo menee läpi siten, että `yield`-lauseke ei tule vastaan. Nextin kutsumista ei tietenkään tehdä käsin, vaan luotetaan, että for-silmukka osaa käyttää sitä:

```python
for i in my_generator():
    print(i)
```

## Iteraattorista Generaattoriin

Tehdään aluksi edellisten esimerkkien mukainen iteraattori luokan avulla:

```python
class MyIterator:
    def __init__(self, start, end):
        self.start = start
        self.end = end

    def __iter__(self):
        return self

    def __next__(self):
        if self.start >= self.end:
            raise StopIteration
        value = self.start
        self.start += 1
        return value
```

Ja lopulta sama generaattorina:

```python
def my_generator(start, end):
    while start < end:
        yield start
        start += 1
```