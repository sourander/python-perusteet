## Asennus Windowsille

!!! warning
   Huomaa, että Git Bash emuloi Linux-maailmasta tuttua Bash-shelliä. Tämän takia esimerkiksi hakemistojen välissä käytetty erotin on ajoittain komentojen tuloisteissa POSIX- eli Linux-suuntaan (`/`) ja ajoittain Windows-suuntaan (`\`). Git Bash on outo sekoitus Windowsia ja Linuxia: sen kanssa pitää vain oppia tulemaan toimeen, mikäli käyttää Windowsia kehitysympäristönä.

Windowsissa pip asentuu Pythonin mukana. Se asentuu lokaatioon `$LOCALAPPDATA/Programs/Python/Python311/Scripts/pip.exe`. Komento ei välttämättä ole $PATH:ssa eikä sitä täten voi ajaa suoraan komentokehotteesta, mutta tällä ei ole väliä. Meille riittää, että komento toimii virtuaaliympäristöissä.

!!! tip
    Lukuohje ympäristömuuttujiin. Bashissä, kuten myös Windowsissa, on olemassa ympäristömuuttujia. Linuxissa näihin viitataan syntaksilla `$MUUTTUJA` ja Windowsissa `%MUUTTUJA%`. Osa näistä on aina olemassa, kuten `$PATH`, joka sisältää puolipisteellä erotellun listan hakemistoista, joista ajettavia komentoja etsitään. Tutustu olemassa oleviin ympäristömuuttujiin ajamalla Git Bash:ssä komento `printenv`. Niitä on huomattavan paljon. Käytän paria näistä alla olevissa komennoissa lyhentämään muutoin kammottavan pitkiä tiedosto- tai hakemistopolkuja.

Avaa Git Bash ja siirry johonkin kansioon, jossa uskallat kokeilla virtuaaliympäristöjä.

```bash
# Jos yllä oleva python.exe löytyy AppData kansion alta, niin jatka ohjetta.
# Luo virtuaaliympäristö hakemistoon .venv
$ python -m venv .venv

# PS. Lue lisää python executablen optionseista täällä:
# https://docs.python.org/3/using/cmdline.html

# Aktivoi virtuaaliympäristö
source .venv/Scripts/activate

# Virtuaaliympäristö on aktivoitu jos komentokehotteen rivi alkaa `(.venv)`-tekstillä.
# Tämä ei valitettavasti aina toimi Git Bash:ssä, vaan se saattaa tulostua oudosti vasta
# seuraavalle riville.
(.venv) $

# Varmista vielä, että ensimmäinen Python listalla on nimenomaan projektin alla oleva 
# paikallinen python.exe eli virtuaaliympäristö.
$ py -0p
  *               $PWD\.venv\Scripts\python.exe
 -V:3.11          %LOCALAPPDATA\Programs\Python\Python311\python.exe


Mikäli vahingossa deaktivoit virtuaaliympäristön, aktivoi se uusiksi komennolla `.venv\Scripts\activate.bat`. Sinun tulee ajaa tämä **aina** kun suljet ja käynnistät
```

## TODO

Selitä myös `python -m venv --copies` vs. default eli symbolic link.