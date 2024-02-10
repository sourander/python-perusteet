!!! warning

    Poetry on pip:iä hieman edistyneempi työkalu. Ellei opettaja ohjeista kurssin puitteissa, sinun ei ole millään tavoin pakko asentaa Poetryä.

Poetry käyttää Pythonin omia `venv` ja `pip` työkaluja konepellin alla, mutta tarjoaa käyttäjäystävällisen kokemuksen. Työkalu vaatii hieman opettelua alkuun, mutta pitkässä juoksussa sen käyttö on todella suositeltua. Sen kilpailija ja/tai edeltäjä on `pipenv`, johon voit myös halutessasi tutustua.

Poetryllä on oma, selkeä dokumentaatio, joten en turhaan toista suurta osaa ohjeista tässä dokumentissa. Alla on hyvin tiivistetty asennusohje, jossa on mainittuna pari pientä seikkaa, joita dokumentaatio ei tee selväksi.

## Nykyinen tapa asentaa:

Mikäli sinulla ei ole Poetryä asennettuna, voit asentaa sen suoraan uudella tavalla. Jos se on asennettuna, mutta käyttämättä tätä `pipx`-tapaa, suosittelen poistamaan sen ja asentamaan uudelleen. Tähän on ohjeet alla "Wanha tapa asentaa" -otsikon alla.

Asenna Poetry pipx:ää käyttäen. Katso ohje tämän materiaalin [pipx](pipx.md) -ohjeesta. Lyhyimmillään se hoituu näin:

```bash
pipx install poetry
```

## Wanha tapa? Päivitä!

Ethän seuraa tätä ohjetta asentamiseen, vaan nimenomaan poistoon ja uudelleen asentamiseen.

```bash
# Jos sinulla on jo Poetry entuudestaan, eikä pipx tunne sitä, olet saattanut 
# asentaa sen vanhalla tavalla. Eli tällä komennolla:
curl -sSL https://install.python-poetry.org | python -

# Jos olet asentanut wanhalla tavalla, poista se näin:
curl -sSL https://install.python-poetry.org | python - --uninstall
```

!!! tip

    Saatat joutua valitsemaan python:n tai python3:n käyttöjärjestelmäsi mukaan. Kokeile ensin `python -V` ja `python3 -V` ja katso kumpi niistä palauttaa Pythonin versionumeron. Käytä sitä komennossa.


## Pyenv ja Poetry

Jos sinulla on sekä pyenv että Python Poetry asennettuna, eli todennäköisesti olet joko macOS- tai Linux-käyttäjä, niin aktivoi myös seuraava konfiguraatio:

```bash
poetry config virtualenvs.prefer-active-python true
```
