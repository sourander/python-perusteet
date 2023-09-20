## Asennus Windowsille

Windowsissa pip asentuu Pythonin mukana. Se asentuu lokaatioon `%localappdata%\Programs\Python\Python311\Scripts\pip.exe`. Komento ei välttämättä ole $PATH:ssa eikä sitä täten voi ajaa suoraan komentokehotteesta, mutta tällä ei ole väliä. Meille riittää, että komento toimii virtuaaliympäristöissä.

Avaa Git Bash ja siirry johonkin kansioon, jossa uskallat kokeilla virtuaaliympäristöjä.

```bash
# Jos yllä oleva python.exe löytyy AppData kansion alta, niin jatka ohjetta.
# Luo virtuaaliympäristö alikansioon .venv
$ python -m venv .venv

# PS. Lue lisää python executablen optionseista täällä:
# https://docs.python.org/3/using/cmdline.html

# Aktivoi virtuaaliympäristö
.venv\Scripts\activate.bat

## Virtuaaliympäristö on aktivoitu jos komentokehotteen rivi alkaa `(.venv)`-tekstillä.
(.venv) $

# Jatkossa python executable löytyy lähimmillään tuosta alikansiosta
$ py -0p
>>  *             %cd%\.venv\Scripts\python.exe
>> -V:3.11        %localappdata%\Programs\Python\Python311\python.exe
>> -V:3.10        %localappdata%\Programs\Python\Python310\python.exe
>> ...

Mikäli vahingossa deaktivoit virtuaaliympäristön, aktivoi se uusiksi komennolla `.venv\Scripts\activate.bat`. Sinun tulee ajaa tämä **aina** kun suljet ja käynnistät
```

## TODO

Selitä myös `python -m venv --copies` vs. default eli symbolic link.