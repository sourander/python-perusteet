## Käytä Z Shelliä

Z Shellin (`zsh`) pitäisi olla macOS:ssä nykyisin default, mutta voi myös olla, että Terminal käynnistää kilpailevan shellin eli `bash`:n. Mikäli näin on, macOS:n pitäisi neuvoa sinua ajamaan komento, joka näkyy alla. Aja komento ja käynnistä Terminal uusiksi.

```bash
$ chsh -s /bin/zsh
```

On suositeltavaa asentaa myös Oh My Zsh ja aktivoida ssh-agent plugin. Tämä neuvotaan [Linux Perusteet](https://sourander.github.io/linux-perusteet/)-kurssilla.

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

Gittiin kannattaa asettaa itselleen sopivat global konfiguraatiot. Nämä neuvotaan How to Git -materiaalissa, mutta alla todennäköisesti sinulle toimivat arvot. Vaihda nimen tilalle oma nimesi ja sähköpostiosoitteen tilalle koulun sähköpostiosoitteesi.

```bash
$ git config --global user.name "Etunimi Sukunimi"
$ git config --global user.email "etunimisukunimi@kamk.fi"
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

## Asenna uv

Uv-työkalun asennus on niin hyvin dokumentoitu (ja on vain yksi komento), joten viittaan suoraan alkuperäiseen ohjeeseen: [uv](https://docs.astral.sh/uv/)

Uv-työkalun käyttö neuvotaan [Ajaminen/uv](../ajaminen/uv.md) -sivulla.