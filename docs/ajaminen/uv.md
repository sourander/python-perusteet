# uv

!!! warning

    Tämä materiaali on raakile. Se saa lisää täytettä, kunhan opettaja ehtii kirjoittaa.

Sinut neuvottiin asentamaan Python uv:n avulla, mutta toistaiseksi olet vasta asentanut uv:n, et Pythonia. `uv` asentaa Pythonin tarpeen mukaan automaattisesti, tai voit asentaa sen käsin näin:

```bash
# Install
uv python install 3.12

# ... or upgrade
uv python install 3.12 --reinstall
```

Jatkossa kun ajat Pythonia, aloita rivi näin:

```
uv run python [tiedosto] [argumentit]
```

Esimerkiksi:

```bash
# Aja main.py
uv run python main.py

# Aja REPL
uv run python

# Aja REPL Git Bashissä winpty:n kanssa
winpty uv run python
```

Tätä pikaohjetta enempää en neuvo, koska [Python Developer Tooling Handbook](https://pydevtools.com/handbook/tutorial/)-sivuston Tutoriaali on niin kattava. Seuraa kyseisen sivuston ohjeita, ja opit tekemään `uv`:n avulla Python-kirjaston, puskemaan sen PyPi:iin ja tekemään sekä unit-testit että staattista koodianalyysiä ruffilla.