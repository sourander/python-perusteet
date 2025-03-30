# uv

!!! warning

    Tämä materiaali on raakile. Se saa lisää täytettä, kunhan opettaja ehtii kirjoittaa.

Sinut neuvottiin asentamaan Python uv:n avulla, mutta toistaiseksi olet vasta asentanut uv:n, et Pythonia. Voit asentaa Pythonin näin:

```bash
# Install
uv python install 3.12
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
