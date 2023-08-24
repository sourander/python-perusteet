## Windows

Aloita asentamalla Python. Mene [Python.org](https://www.python.org/) sivustolle ja lataa etusivulla mainostettu tuorein Python 3 versio (esim. ``).

Käynnistä komentokehote (Command Prompt, cmd). Jos käytät PowerShelliä, komennot ovat eri. Jos alla olevan listan komento alkaa `>>` merkeillä, se edustaa edellisen komennon tulostetta ruudulle. Sen sijaan `$`-merkki edustaa nykyistä kansiota, jonka tilalla lukee esimerkiksi todennäköisesti `C:\Users\<username>`. Lyhenne `%cd%` tarkoittaa kansiota (current directory).

Lyhyesti sama:

1. Asenna Python
2. Avaa komentokehote ja suorita:

```bash
# Mene valitsemaasi projektikansioon, esimerkiksi:
$ cd %userprofile%\Code\

# Kloonaa git repo
$ git clone <repo-url>

# Varmista että python executable löytyy ja viittaa oikeaan versioon
# Ensimmäisen itemin PATH:ssa pitäisi olla Python 3.X:n executable.
$ py -0p
>> -V:3.11 *        %localappdata%\Programs\Python\Python311\python.exe
>> -V:3.10          %localappdata%\Programs\Python\Python310\python.exe
>> ...

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

Asenna seuraavaksi tehtävien tarkistamiseen käytetyt Python-moduulit:

# Tehtävien testaaminen

```sh
# Asenna pytest ja mypy
pip install pytest
pip install mypy

# Varmista että seuraava testi menee läpi
pytest tests/test_helloworld.py::test_hello_world --verbose
>> configfile: pytest.ini
>> collected 1 item
>> 
>> tests\test_helloworld.py PASSED                      [100%] 
>> 
>> ==================== 1 passed in 0.01s ====================
```