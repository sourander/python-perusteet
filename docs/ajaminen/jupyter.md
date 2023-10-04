Koodia voi ajaa myös Jupyter Notebookissa, joka on web-selainpohjainen interaktiivinen IDE. Projektin voi asentaa joko käyttäen tuoreempaa `JupyterLab`:ia tai klassista `Jupyter Notebookia`. Notebook on hieman karsitumpi ominaisuuksiltaan, mutta sillä pärjää yllättävän pitkälle.

JupyterLabin hyötyjä ovat muun muassa:

* Välilehdet. Jupyter Notebook vaatii yhden selainikkunan per notebook. JupyterLabissa voit avata monta yhteen.
* Tiedostoselain. 
* Tuki extensioneille (esim. [Jupyter Tabnine](https://github.com/codota/jupyter-tabnine))

Tiiviisti sanottuna: klassinen Jupyter Notebook, jos työskentelet yhden tiedoston koodin parissa.

!!! warning
   Ethän asenna Jupyter Notebookia järjestelmätason Pythoniin vaan virtuaaliympäristöön. Lue siis [pip](.../asennus/paketinhallinta/pip.md)-luku ennen seuraavien komentojen ajamista!

Pidemmät asennusohjeet löytyvät [Jupyter:n dokumentaatiosta](https://jupyter.org/install), mutta alkuun pääsee kahdella seuraavalla komennolla:

```bash
# Ajathan komennot VIRTUAALIYMPÄRISTÖSSÄ
(.venv) $ pip install notebook
(.venv) $ jupyter notebook
```

Komento joko avaa suoraan selaimeesi Jupyter Notebook -näkymän, tai tarjoaa linkin, jota klikkaamalla pääset siihen. Ethän sulje terminaalia tai palvelin kuolee pois. Kun haluat lopettaa työskentelyn, varmista että tiedosto on tallennettu ++ctrl+s++ näppäinyhdistelmällä ja valitse Jupyter Notebookista `File => Shut Down`.