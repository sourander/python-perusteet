Useimmissa distribuutioissa on jokin Python-versio jo valmiiksi asennettuna. Sinulla on vaihtoehtoina joko käyttää valmiiksi asennettua versiota tai asentaa tuoreempi. Kummassakin on hyötynsä ja haittansa.

## Oletus Python3:n käyttäminen

Tämä ohje on kirjoitettu Ubuntussa, joka käyttää Debianista perittyä `APT`-paketinhallintaa. Mikäli sinulla on eri distribuutio, tutki, mikä on vastaava paketinhallinta ja vastaavat komennot.

```bash
# Tarkista versio
$ python3 --version
Python 3.10.12
```

Mikäli versio on kurssin puitteissa riittävän tuore, voit käyttää sitä. Tulet todennäköisesti tarvitsemaan myös muita paketteja, kuten `python3.10-venv`, mutta Python kyllä neuvoo tämän, kun ajat komentoja, joilta puuttuu tarvittavia riippuvuuksia. Huomaathan, että `python` ei ole symbolic link `python3`:een useimmissa distribuutioissa, joten joudut kirjoittamaan `python3` executablen nimeksi. Tämä usein korjautuu kun luot ensimmäisen virtuaaliympäristön `pip`:llä tai `poetry`:llä.

## Pyenv ja Ubuntu

Mikäli haluat käyttää toista Pythonia, on suositeltavaa ottaa käyttöön pyenv. Voit käyttää Homebrew:ta aivan kuten macOS:ssä tai pyenv:n omaa shell-skriptiä. Alla olevassa esimerkissä käytetään pyenv:n omaa asennusohjetta. Riippuvuudet listataan [pyenv:n dokumentaatiossa](https://github.com/pyenv/pyenv/wiki#suggested-build-environment), mutta listalle on lisätty varmuuden vuoksi git. Sen tarvitsee pyenv.run:n shelliskripti.

```bash
# Asenna riippuvuudet
$ sudo apt update
$ sudo apt install -y build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl git \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# Asenna shelli-skriptillä
$ curl https://pyenv.run | bash
```

Tee, kuten asennus ohjeistaa, eli lisää seuraavat rivit tiedostoon `.profile` tai `.bash_profile`, riippuen kumpi kotihakemistostasi löytyy, vakiona `.profile`:een:

```bash
# Initialize pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

Käynnistä shell uudestaan (login-tilassa) ajamalla seuraava komento:

```bash
# Käynnistä bash uudestaan (login shellinä)
$ exec $SHELL -l

# Tarkista, että pyenv toimii
$ pyenv --version
pyenv 2.3.27

# Asenna haluamasi Python
$ pyenv install 3.11

# Aseta global defaultiksi
$ pyenv global 3.11
```

