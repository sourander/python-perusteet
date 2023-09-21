!!! tip
    Lukuohje alla oleviin koodisnippetteihin: mikäli rivi alkaa `$`-merkillä, kyseinen rivi on ajettava komento. Kyseinen merkki ei kuulu komentoon, vaan on yksinkertaisesti dokumentaatiossa indikoimassa, että kyseessä on command promptiin syötetty käsky. Mikäli rivistä puuttuu tuo merkki, on kyseessä komennon palauttama tuloste. Mikäli tulosteessa on rivi `...`, tulostetta on lyhennetty luettavuuden parantamisen vuoksi. Oikea tuloste on tällöin pidempi.

## Käytä Z Shelliä

Z Shellin (`zsh`) pitäisi olla macOS:ssä nykyisin default, mutta voi myös olla, että Terminal käynnistää kilpailevan shellin eli `bash`:n. Mikäli näin on, macOS:n pitäisi neuvoa sinua ajamaan komento, joka näkyy alla. Aja komento ja käynnistä Terminal uusiksi.

```bash
$ chsh -s /bin/zsh
```

## Asenna Homebrew

Homebrew on vastaavanlainen paketinhallinta kuin Snap, Flatpak, Chocolatey tai jopa Ubuntusta tuttu ATP tai Red Hatistä tuttu DNF. Valitettavasti macOS:ssä ei ole valmiina omaa, joten avoimen lähdekoodin yhteisö on luonut puutteen tilalle Homebrew:n. Sitä käytetään asentamaan, päivittämään, hallinnoimaan ja poistamaan sovelluksia. Useimpia ohjelmistonkehitykseen tai shell-komentoihin liittyviä sovelluksia et löydä AppStoresta vaan ne tulee asentaa Homebrew:n tai vastaavan avulla. Jos haluat tarkat asennusohjeet, lue mac.install.guide-sivuston: [Install Homebrew Complete Guide](https://mac.install.guide/homebrew/3.html). Jos olet pelkkää asennuskomentoa vailla, aja [Homebrew:n kotisivuilta](https://brew.sh/) löytyvä komento:

```bash
# Homebrew:n asennuskomento on bashillä ajettava shell-skripti. Tämä komento lataa ja ajaa sen.
# Tuloste sisältää ohjeistusta ja tietoja asennuksesta. Lue se! Alla lyhennelmä:
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
==> This script will install:
/opt/homebrew/bin/brew
...
==> The following new directories will be created:
/opt/homebrew/bin
/opt/homebrew/etc
...
```

HUOM! Jos olet joskus ajanut komennon `xcode-select --install`, joka asentaa Linux-maailmasta tuttuja komentoriviltä ajettavia sovelluksia kuten `gcc` sekä `clang`. Mikäli et, Homebrew:n asennus käynnistää XCode Command Line Tools:n asennuksen. Homebrew tarvitsee näitä ohjelmia.

Lue asennuksen tarjoamat ohjeet tarkkaan. Asennus pyytää sinua lisäämään yhden rivin .zprofile-tiedostoon, joka voi olla tai voi olla olematta käytössä vakiona. Rivi näyttää muutoin samalta kuin alla oleva, mutta alla olevassa on mukana kommentti. Suosittelen pitämään `.zprofile` ja `.zshrc` tiedostot kommentoituina, jotta tiedät mitä mikäkin rivi tekee, ja miksi olet sen sinne lisännyt.

```bash
# .zprofile sisältö alla:

# Add Homebrew-related env variables
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Jatkossa ympäristömuuttujan `$PATH` pitäisi sisältää Homebrew:n asennuskansio. Voit tarkistaa tämän seuraavalla komennolla. Tulosteen pitäisi sisältää kansio `/opt/homebrew/bin` jos sinulla on ARM-sirullinen Apple. Vanhemmissa Intel-pohjaisissa koneissa asennuskansio on `/usr/local`. Asennuskansion pitäisi olla sinulle tuttu, mikäli luit aiempien komentojen tulosteen.

```bash
$ echo $PATH | tr ":" "\n"
/opt/homebrew/bin
/opt/homebrew/sbin
/usr/local/bin
...
```

# Asenna git

Python-koodi kannattaa pistää lähes poikkeuksetta gittiin, ja tämä on usein myös eri kursseilla tehtävänantojen oletus. Xcode:n mukana tulee Applen oma höyste `git`-työkalusta, mutta suosittelen asentamaan Homebrew:n hallinnoiman version.

```bash
# Asenna
$ brew install git

# Tarkista että on asentunut
$ git --version
git version 2.42.0

# Varmista, että lokaationa on nimenomaan Homebrew:n asennuskansio
# EI SIIS /usr/bin/git vaan alla näkyvä tuloste
$ type git
git is /opt/homebrew/bin/git

# Mikäli yllä oleva tuloste viittaa /usr/bin-kansion executableen, aja seuraava
# komento ja kokeile uusiksi
rehash
```

# Konfiguroi git

Gittiin kannattaa asettaa itselleen sopivat global konfiguraatiot. Nämä neuvotaan How to Git -kurssilla, mutta alla todennäköisesti sinulle toimivat arvot. Vaihda nimen tilalle oma nimesi ja sähköpostiosoitteen tilalle koulun sähköpostiosoitteesi.

```bash
$ git config --global user.name "Etunimi Sukunimi"
$ git config --global user.email "etunimisukunimi@kamk.fi"
$ git config --global core.autocrlf input
$ git config --global pull.ff only
$ git config --global init.defaultBranch main
```

# Git Credential Manager

Jos käytät pelkästään ssh-avaimia, tämä vaihe ei ole välttämättä tarpeen. Jos haluat kirjautua Githubiin tai GitLabiin ilman ssh-avainta, Git Credential Manager (GCM) on tällä hetkellä suositeltu tapa.

Se asentuu näin:

```bash
$ brew install --cask git-credential-manager
```

Seuraavalla kerralla kun kloonaat HTTPS-urlilla repositorion, git avaa ikkunan, jossa se pyytää sinua kirjautumaan sisään Oauth-tyylisesti palveluun. Tämä luo tokenin, joka oikeuttaa kyseisen repositorion kloonaamisen. Mikäli 2FA on päällä, kysyy se myös sitä.

# Asenna pyenv

Asenna pyenv Homebrew:lla ja lue sen [käyttöohjeet GitHubista](https://github.com/pyenv/pyenv#usage). Työkalulla voi hallita useita eri Python-asennuksia samalla koneella, esimerkiksi kansio/projektikohtaisesti.

```bash
$ brew install pyenv
```

Lisää seuraavat rivit `.zshrc`-tiedostoon, aivan kuten dokumentaatiossa neuvotaan:

```bash
# Set up pyenv related environment variables
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

Käynnistä terminaali uusiksi tai aja komento `source ~/.zshrc`. Jos haluat varmistaa, että komennot ovat ajettuna oikein, tarkista löytyykö jokin pyenvin tarvitsemista ympäristömuuttujista. Alla yksi esimerkeistä:

```bash
# Tämän pitää tulostaa zsh eikä tyhjää merkkijonoa
$ echo $PYENV_SHELL 
zsh
```

## Asenna Pythonin riippuvuudet

Pyenv:n ajama Python-asennus voi vaatia joitakin riippuvuuksia, joista Homebrew ei tiedä. Pelkän `xs`:n pitäisi riittää, mutta [pyenv:n dokumentaatio](https://github.com/pyenv/pyenv/wiki#suggested-build-environment) suosittelee seuraavia:

```bash
$ brew install openssl readline sqlite3 xz zlib tcl-tk
```

## Asenna Python pyenvillä

Mikäli kaikki vaiheet yllä on suoritettu onnistuneesti, voit alkaa asentaa useita eri Python-versioita ja hallinnoimaan niitä kuten pyenvin dokumentaatiossa neuvotaan. Ensimmäiseksi sinun pitää päättää, minkä Python-version haluat. Suosittelen asentamaan Pythonin, joka on sillä hetkellä tuorein `bugfix` tai `security` maintenance statuksella oleva Python-versio. Tämän voit käydä tarkistamassa [Pythonin sivuilta](https://www.python.org/downloads/). Kirjoitushetkellä `bugfix`-tilassa on 3.11, joten haluan asentaa 3.11.x version. Versionumeron kolme pisteellä erotettua versionumeroa ovat `major.minor.patch`. Python on saman major (3.x.x) version sisällä taaksepäin yhteensopiva, mutta uudemmissa Pythoneissa on toimintoja, jotka eivät toimi vanhemmissa versioissa. Vanha 2.x Python on virallisesti kuollut ja kuopattu. Sitä ei pitäisi käyttää tuotannossa.

Tämän dokumentaation kirjoitushetkellä tuorein bugfix-vaiheessa oleva Python patch on `3.11.5`. Sen voi asentaa alla olevalla komennolla. Komento täydentää itse tuoreimman patch-numeron.

```bash
# Asenna Python
$ pyenv install 3.11
python-build: use openssl from homebrew
python-build: use readline from homebrew
Downloading Python-3.11.5.tar.xz...
...
Installing Python-3.11.5...
...
```

Huomaa, että pyenv asentaa Pythonin sinun kotikansioosi. Asennuslokaatio on yllä asetettu `$PYENV_ROOT` eli esimerkiksi `/home/jani/.pyenv/versions/3.11.5/`.

Asetetaan vielä tuorein versio globaaliksi oletukseksi. Näin pyenv käyttää valittua versiota globaalina oletuksena, jonka tosin voi jyrätä lokaalilla versiolla. Tutustu dokumentaatiosta, kuinka lokaali versio asetetaan. Globaalin voi vaihtaa näin:

```bash
# Tarkistetaan ensin vanha oletusarvo
$ pyenv global
system

# Asetetaan uusi
$ pyenv global 3.11

# Tarkistetaan uusi
$ pyenv global
3.11
```


## Kuinka päivittää jatkossa?

Jos haluat myöhemmin päivittää Pythonia, asenna uusi ja vaihda global siihen.

```bash
pyenv install 3.x
pyenv global 3.x
```
