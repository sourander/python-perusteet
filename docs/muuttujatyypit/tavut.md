Kaikki maailman data ei tietenkään koostu ihmiselle merkityksellisestä UTF-8 enkoodatusta Unicode-merkistöstä. Osa datasta on binääridataa eli peräkkäin kirjoitettuna tavuja tiedostossa. Tämän datan käsittelyyn Pythonista löytyy tyypit `bytes` ja `bytearray`.

Tietotyypin bytes muuttujia voi luoda muun muassa seuraavin tavoin:

```python
>>> b"Hello"
b'Hello'

>>> bytes([ord("H"), ord("e"), ord("l"), ord("l"), ord("o")])
b'Hello'

>>> bytes([72, 101, 108, 108, 111])
b'Hello'

>>> bytes("Hello", encoding="utf-8")
b'Hello'

>>> "Hello".encode()
b'Hello'
```

Tietotyypin bytearray muuttujia voi luoda muun muassa seuraavin tavoin:

```python
>>> bytearray(b"Hello")
bytearray(b'Hello')

>>> bytearray([72, 101, 108, 108, 111])
bytearray(b'Hello')

>>> bytearray.fromhex("48 65 6c 6c 6f")
bytearray(b'Hello')
```



## Immutability

Tietotyypit `bytes` ja `bytearray` eroavat toisistaan siten, että bytes on muuttumaton - aivan kuten aiemmin tutut sekvenssit merkkijono ja tuple, ja `bytearray` on muuttuva, aivan kuten lista. Jos tietoa ei ole tarve muuttaa luomisen jälkeen, käytä bytesiä.

```python
# Tämä ei onnistu vaan nostaa TypeErrorin
>>> bytes([72, 101, 108, 108, 111])[0] = 0x59

# Tämä sen sijaan onnistuu
bytearray([72, 101, 108, 108, 111])[0] = 0x59
```



## Harjoittele



### Harjoitus: Häshäys ja salaus

Kokeile sekä häshätä että salata jokin merkkijono. Alla on esitelty SHA-256 häshäys. Kokeile salata ja purkaa valitsemasi merkkijono. Käytä tähän symmetrista salausalgoritmia Fernet. Teethän tarvittavat `pip`-asennukset virtuaaliympäristössä!

```python
>>> import hashlib
>>> hashlib.sha256(b"Hello").hexdigest()
'185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969'
```



### Harjoitus: Luku ja kirjoitus

Kokeile lukea ja kirjoittaa binääritiedostoja. Luo MS Paintilla, [JSPaintilla](https://jspaint.app/) tai vastaavalla grafiikkatyökalulla **pieni** 24-bit Bitmap BMP-kuva. Käytä mieluiten kuvaa, joka on alle 100x100 pikseliä. Mikäli käytit JS Paintia ja tallensit kuvan käsketyssä muodossa, kuvan pikselidata alkaa bytestä `image_data[54]`. Kolme peräkkäistä byteä edustavat aina yhden pikselin RGB-arvoja käänteisessä järjestyksessä eli BRG.

```python
# Reading a binary file into bytes
with open("image.bmp", "rb") as file:
    image_data = file.read()
    
# Do something to the image here
processed_image_data = process(image_data)

# Writing binary data to a file
with open("output.bin", "wb") as file:
    file.write(processed_image_data)
```

Toteuta oma prosessorisi haluamallasi tavalla. Alla on esimerkki, joka korvaa kaikki punaiset pikselit mustilla pikseleillä. Ensimmäisten 54 tavun oletetaan edustavan metadataa. Kaiken lopun oletetaan noudattavan kaavaa bytes[blue, green, red, ...] ja jokaisen kuvan pikselirivin olevan neljällä jaollisia. BMP-formaatissa ei-4-jaolliset rivit täytetään nollatavuilla.

```python
def process(image:bytes, 
            pattern_to_replace=bytes.fromhex("00 00 ff"), 
            replacement_pattern=bytes.fromhex("00 00 00")
           ) -> bytes:
    """ I see a red door and I want it to turn black."""

    # Leave pixels that are part of the header untouched.
    HEADER_INDEX, PIXEL_SIZE = 54, 3
    
    # Split to header and pixel data
    header = image[0:HEADER_INDEX]
    pixel_data = image[HEADER_INDEX:]

    # Reveal the naiveness of this function
    assert header[18] % 4 == 0, ("This function only works with images "
                                 "with width that is divisible with 4.")

    # Create pixel indicies 0, 3, 6, ... n-3
    strides = range(0, len(pixel_data), 3)
    output_bytes = bytearray()

    # Loop and append
    for i in strides:
        chunk = pixel_data[i:i + PIXEL_SIZE]
        if chunk == pattern_to_replace:
            output_bytes.extend(replacement_pattern)
        else:
            output_bytes.extend(chunk)

    return header + output_bytes
```



## Harjoitus: Käytä kirjastoa kuvien käsittelyyn

Binääridataa, kuten kuvia, käsitellään useimmissa tapauksissa eri kirjastojen avulla. Kuvia voi käsitellä esimerkiksi kirjastoilla opencv ja Pillow. Kokeile jälkimmäistä. Huomaa, että Pillow on fork vanhemmasta kirjastosta PIL. Tästä johtuu se, että paketti on pypissä eri nimellä kuin millä se importattaan.

Asenna kirjasto virtuaaliympäristöösi:

```bash
# Bashissä
$ pip install Pillow

# ...tai luo ja aja Jupyter Notebookissa magic cell
%pip install Pillow
```

Jos haluat listata kaikki tiedostoformaatit, jotka voit Pillow:lla tällä hetkellä avata ja/tai kirjoittaa, aja komento:

```python
>>> from PIL import features
>>> PIL.features.pilinfo()
```

Kirjoita koodi:

```python
from PIL import Image

# Lataa kuva ja tarkista sen tietotyyppi
img = Image.open("image.bmp")
print(type(img))

# Suurenna kuva tasan 4x suuremmaksi käyttämättä interpolointia, jotta
# kaunis pixel art pysyy pixel arttina eikä mössönä.
resized = img.resize((img.width * 4, img.height * 4), resample=Image.NEAREST)

# Hae pikselit listana tupleja. Huomaa type hint.
pixels: list[tuple[int, int, int]] = list(resized.getdata())

# Prosessoi pikselit funktiolla, joka sinun tulee luoda
pixels = process(pixels)

# Laita muokatut pikselit paikoilleen
resized.putdata(new_pixels)
```

Pillow ja Jupyter Notebookin käyttämä IPython tarjoavat mahdollisuuksia myös kuvan näyttämiseen. Jupyter Notebookissa kuvan voi katsoa ajamalla solun, jonka viimeinen rivi on kuvan sisältävä muuttuja, kuten `resized`, tai vaihtoehtoisesti `display()` funktion sisältä esimerkiksi solun keskeltä:

```python
# GUI pop-up. Toimii myös Python-skripteistä laukaistuna:
resized.show()

# IPythonin display. Toimii Jupyter Notebookissa:
from IPython.display import display
display(resized)
```

