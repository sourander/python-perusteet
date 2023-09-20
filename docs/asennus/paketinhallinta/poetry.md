!!! warning
    Poetry on pip:iä hieman edistyneempi työkalu. Ellei opettaja ohjeista kurssin puitteissa, sinun ei ole millään tavoin pakko asentaa Poetryä.

Poetry käyttää Pythonin omia `venv` ja `pip` työkaluja konepellin alla, mutta tarjoaa käyttäjäystävällisen kokemuksen. Työkalu vaatii hieman opettelua alkuun, mutta pitkässä juoksussa sen käyttö on todella suositeltua. Sen kilpailija ja/tai edeltäjä on `pipenv`, johon voit myös halutessasi tutustua.

Poetryllä on oma, selkeä dokumentaatio, joten en turhaan toista suurta osaa ohjeista tässä dokumentissa. Alla on hyvin tiivistetty asennusohje, jossa on mainittuna pari pientä seikkaa, joita dokumentaatio ei tee selväksi.

## Asennus

!!! tip "Windows"

    Mikäli käytössäsi on Windows, ja dokumentaatiosta löytyvä rivi. Riippuen ympäristöstäsi, sinulla ehkä toimii komento `python3`, ehkä ei. Jos ei, aja alempi rivi.

    ```bash
    # Näin
    curl -sSL https://install.python-poetry.org | python3 -

    # Tai näin, jos python3 ei viittaa mihinkään
    curl -sSL https://install.python-poetry.org | python -
    ```

!!! tip "macOS"
    Asennetaan Python Poetry käyttäen pyenv:n globaalia Pythonia käyttäen. Huomaa, että `python3` viittaa yhä system-wide Pythoniin, joka ei salli virtual environmenttien luomista kopioiomalla - ja se on juuri mitä me ollaan tekemässä. Siispä sinun pitää ajaa komento nimenomaan siten, että ajat skriptin `python`:ssa, ETKÄ `python3`:ssa.

    ```bash
    # Asenna käyttäen pyenvin globaalia Pythonia
    curl -sSL https://install.python-poetry.org | python -
    ```


## Poetryn lisääminen PATH:iin

### Windows

Lisätään PATH:iin `%APPDATA%\Python\Scripts`.

TODO: tarkemmat ohjeet.

### macOS

Asioiden lisäämistä PATH:iin ja `.zshrc`:ään on harrastettu tässä dokumentaatiossa jo aiemmin. Tehdään se taas kerran. Lisää seuraavat rivit `.zshrc`-tiedostoon.

```bash
# Python Poetry
export PATH="$HOME/.local/bin:$PATH"
```

Jatkossa, kunhan olet ajanut komennon `source .zshrc` tai käynnistänyt Terminaalin uusiksi, komennon `poetry --version` pitäisi palauttaa Python Poetryn versionumero.

## Pyenv ja Poetry

Jos sinulla on sekä pyenv että Python Poetry asennettuna, eli todennäköisesti olet joko macOS- tai Linux-käyttäjä, niin aktivoi myös seuraava konfiguraatio:

```bash
poetry config virtualenvs.prefer-active-python true
```