## Asenna

Mikäli sinulla on jo Visual Studio Code asennettuna, hyppää seuraavaan aliotsikkoon.

- Windowsille Visual Studio Code asennetaan [Visual Studio Code](https://code.visualstudio.com/download):n sivuilta.
- macOS:lle voit asentaa sen joko lataamalla asennuspaketin samalta sivustolta, tai, käyttämällä Homebrew:ta. Homebrew:n asennus ja peruskäyttö on neuvottu tämän saitin [macOS](macOS.md)-ohjeessa, jonka toivon mukaan olet jo lukenut, jos olet macOS-käyttäjä.
- Linuxissa asennus riippuu distrosta. Etsi työpöytäympäristöstäsi `GNOME Software` tai lataa käyttöjärjestelmääsi sopiva paketti [Visual Studio Code Downloads](https://code.visualstudio.com/download)-sivulta.

Jos asennat macOS:ssä Homebrew:tä käyttäen, aja komento:

```bash
$ brew install --cask visual-studio-code
```

## Asetukset

Visual Studio Codessa useimmat asetukset päätyvät JSON-tiedostoon. Pääset tiedostoon käsiksi näin:

1. Avaa Command Palette. Pikanäppäin on Windowsissa ++ctrl++shift+p++ ja macOS:ssä ++shift++command++p++.
2. Etsi sanaa "Settings"

Listalta pitäisi löytyä seuraavat vaihtoehdot:

- Preferences: Open User Settings (JSON)
- Preferences: Open User Settings
- Preferences: Open Default Settings (JSON)
- Preferences: Open Default Settings
- Preferences: Open Workspace Settings (JSON)
- Preferences: Open Workspace Settings

Huomaat, että lähes kaikkia asetuksia voi säätää joko menujen kautta tai kirjoittamalla käsin JSON-konfiguraatiotiedostoon rivejä. Osa asetuksista vaatii, että kirjoitat ne käsin, osalle löytyy menuista mukava, valmis nappi.

Jos valitsit VS Coden käynnistymisen yhteydessä väriteeman "Default Dark Modern" ja laitat menuista (Preferences: Open User Setttings) asetuksen "Git: Autofetch" tilaan `false`, ja asetat Git Bashin oletusterminaaliksi, niin JSON näyttää tältä:

```json
{
  "workbench.colorTheme": "Default Dark Modern",
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "git.autofetch": false
}
```

Jos olet **macOS-käyttäjä**, sinulla ei ole Git Bashiä laisinkaan vaan oletusshell on `zsh`:n. Vastaava JSON näyttää tältä:

```json
{
  "workbench.colorTheme": "Default Dark Modern",
  "terminal.integrated.defaultProfile.osx": "zsh",
  "git.autofetch": false
}
```

Asetuksiin kannattaa tutustua ajan kanssa. VSCodessa voi, ja ajoittain joutuu, säätämään hyvinkin pikkutarkkoja asetuksia, kuten asetuksia, jotka kohdistuvat vain tiettyjen tiedostopäätteiden tiedostoihin.

## Extensions

### Extension: Markdown All in One

Asennetaan dokumentaatiota helpottava extension **Markdown All in One**.

1. Klikkaa VS Coden vasemmassa toolbarissa näkyvää Extensions-ikonia.
2. Etsi hakusanalla "markdown all"
3. Valitse haluttu extension ja klikkaa sinistä Install-nappia.

Voit lukea extensionin ohjeet Visual Studio Marketplacesta [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one):n omalta sivulta.

!!! question "Tehtävä"

    Noudata Marketplacesta löytyvää dokumentaatiota ja kokeile seuraavia asioita:

    1. Luo muutama otsikko ja Table of Contents
    2. Luo Markdown-taulukko. Kokeile Table formatter -ominaisuutta.

### Extension: Prettier - Code Formatter

Asenna Prettier yllä neuvotulla tavalla.

```json
{
  // Pretty
  "workbench.colorTheme": "Default Dark Modern",

  // Terminal
  "terminal.integrated.defaultProfile.osx": "zsh",

  // Editor
  "editor.detectIndentation": false,
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  // Git
  "git.autofetch": false,

  // File specific
  // Markdown file format settings
  "[markdown]": {
    "editor.formatOnSave": true,
    "editor.wordWrap": "on",
    "editor.tabSize": 4,
    "editor.insertSpaces": true
  },

  // Markdown All in One extension
  "markdown.extension.list.indentationSize": "inherit"
}
```

### Extension: Python

Asenna kuten aiemmat tai asenna kun Code kysyy sitä. Tyypillisesti Code tarjoaa tämän Extensionin asenatamista, kun luot tai avaat ensimmäisen `.py`-päätteisen tiedoston.

Anna tämän extensionin olla vakioasetuksilla.

### Extension: Jupyter

Asenna kuten aiemmat tai asenna kun Code kysyy sitä. Tyypillisesti Code tarjoaa muutaman Jupyteriin liittyvän extensionin asentamista, kun luot tai avaat ensimmäisen `.ipynb`-päätteisen tiedoston.
