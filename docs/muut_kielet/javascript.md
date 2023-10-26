JavaScript on kielen rakenteeltaan ja jopa syntaksiltaan yllättävän lähellä Pythonia. JavaScriptin opiskelu on siten luontevaa Pythonin jälkeen. Tämä mahdollistaa, että voit muun muassa luoda:

* Web-serverin, joka tarjoaa REST-rajapinnan avulla JSON-muotoista dataa.
    * Kieli: Python
    * Kirjastot: FastAPI, Uvicorn
* Http-sivuston, joka käyttää REST-rajapintaa ja näyttää datan käyttäjälle.
    * Kielet: HTML, Vanilla JavaScript
    * Kirjastot: Fetch API

## Kielten samankaltaisuus

Samankaltaisuudet:

* Kumpikin on dynaamisesti tyypitetty
* Kumpikin on tulkattu
* Kumpaakin voi kehittää tavallisella tekstieditorilla
* Kummassakin on REPL (tavallaan)

Eroavaisuudet:

* Syntaksi pienissä määrin
    * JS:ssä on aaltosulkeita kaikkialla
    * JS:ssä on puolipiste komentojen lopussa
    * Python on snake_case, JavaScript on camelCase
* JS toimii selaimessa
* JS:llä ei lähtökohtaisesti käsitellä tiedostoja

## REPL

Saat REPL:n käyntiin kahdella tavalla.

1. Nettiselaimella millä tahansa sivulla
2. Nettiselaimella omassa sandboxissa
3. Komennolla `node`

### Vaihtoehto 1:

Avaa valitsemasi nettiselain (esim. Chrome). Paina F12. Valitse Console-välilehti. Kirjoita koodia ja paina Enter.

### Vaihtoehto 2:

Luo uusi tiedosto `index.html` ja `script.js`.

```html
<!-- index.html -->
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>JavaScript Sandbox</title>
</head>
<body>
    <!-- type=module is required for ES6 modules -->
    <script type="module" src="script.js"></script>
</body>
</html>
```

Aja tämän jälkeen kansiossa http-serveri esimerkiksi Pythonilla `python -m http.server`. Alla hyvin yksinkertainen Hello World -esimerkki.

```js
// script.js
// Luo funktio, joka tekee jotakin. Tämä palauttaa muuttujat siten kuten se sille annettiin.
function echo(input) {
    return input;
}

// Kutsu funktiota ja tulosta konsoliin
let result = echo("Hello World!");
console.log(result);

// Voit poistaa tämän, mikäli sinulla ei ole tarvetta kutsua funktiota Consolessa.
// Window on globaali objekti, joten siihen kiinnitetty echo on globaali funktio.
window.echo = echo;
```

Nyt voit avata palvelimen osoitteen selaimessa ja näet tuloksen Consolessa. Voit kehittää koodia REPL-hengessä Consolessa ja kopioida toimivaa koodia script.js-tiedostoon. Tämä on hieman purkkaviritelmä, mutta toimii.

### Vaihtoehto 3:

Asenna joko node.js paikallisesti tai Docker-konttiin. Nodessa ei ole yhtä näppärää virtuaaliympäristöjen hallintaa kuin Pythonissa, joten suosittelen Dockeria.

Esimerkki `Dockerfile` ja `docker-compose.yml` löytyvät [Javascript-perusteet-code reposta](https://github.com/sourander/javascript-perusteet-code).

```bash
# Luo Docker-kontti
$ docker image build -t kamk/tietolo-js .

# Aja kontti
# ks. parametrien selitykset: https://docs.docker.com/engine/reference/commandline/container_run/
docker container run -it --rm kamk/tietolo-js node
```

## Python to JavaScript

### Muuttujan luominen

```python
# Pythonissa ei ole constia, mutta käytäntö 
# on kirjoittaa sitä vastaava muuttuja isolla
WIDTH = 1024

# Muut muuttujat ovat snake_casea
user_input = "Blank"
```

```js
// Const on immutable
const width = 1024;

// Let on mutable
let userInput = "Blank";

// Var on vanha tapa tehdä muuttujia
// var x = "Älä käytä tätä";
```

### Muuttujatyypit

```python
my_string = "Hello World!"
my_other_string = 'Hello World!'
my_int = 1
my_float = 1.0
my_bool = True
my_list = [1, 2, 3]
my_dict = {"name": "John", "age": 30}

# Tulostaa tyypin
print(type(my_dict)
```

```js
// let tai const
let myString = "Hello World!";
let myOtherString = 'Hello World!';
let myNumber = 1;   // JavaScriptissä ei ole erillistä int-tyyppiä
let myNumber = 1.0; // vaan nämä kumpikin ovat float.
let myBool = true;
let myMutableArray = [1, 2, 3];
const myImmutableArray = [1, 2, 3];
let myObject = {"name": "John", "age": 30};

// Tulostaa tyypin
console.log(typeof(myObject));
```

### Listan arvon muokkaaminen

```python
my_list = [1, 2, 3]
my_list[0] = 4
```

```js
let myArray = [1, 2, 3];
myArray[0] = 4;
```

### Listan metodit

```python
len(my_list)
my_list.append(4)
my_list.pop()
my_list[start:end]
my_list[::-1]
my_list + my_list
```

```js
myArray.length;
myArray.push(4);
myArray.pop();
myArray.slice(start, end);
myArray.reverse();
myArray.concat(myArray);
```

### Konsoliin tulostaminen

```python
print("Hello World!")
```

```js
console.log("Hello World!");
```


### Stringin muotoilu

```python
# F-string
name, age = "John", 30
print(f"Hello, my name is {name} and I am {age} years old.")

# String-metodit
name_upper = name.upper()
```

```js
// Template literal
const name = "John";
const age = 30;
console.log(`Hello, my name is ${name} and I am ${age} years old.`);

// String-metodit
const nameUpper = name.toUpperCase();
```

### Perus loop

```python
for i in range(10):
    print(i)
```

```js
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

### Objektien käsittely loopissa
    
```python
# Pythonissa JS-objektia vastaa sanakirja
my_data = [
    {"name": "John", "age": 30},
    {"name": "Jane", "age": 25}
]

for person in my_data:
    print(person["name"])
```

```js
const myData = [
    {"name": "John", "age": 30},
    {"name": "Jane", "age": 25}
];

for (const person of myData) {
    console.log(person.name);
}
```

### Funktiot

```python
# Argumentit a ja b sekä keyword-argumentit c ja d
def my_function(a, b, c=1, d=42):
    pass
```

```js
// Vaihtoehto 1: Perintinen code block
function myFunction(a, b, c=1, d=42) {
    // ...
}

// Vaihtoehto 2: Arrow function
let myFunction = (a, b, c=1, d=42) => { return d }
```

### Import

```python
# main.py
from my_package.my_module import my_function

# ./my_package/my_module.py
def my_function():
    return "Hello World!"
```

```js
// script.js
// ES6 modules
import { myFunction } from "./modules/mmodule.js";

// modules/functions.js
function myFunction() {
    return "Hello World!";
}

export { myFunction };
```

### Käyttäjän syöte

Pythonissa käyttäjän syöte otetaan yleensä vastaan joko `python mun_skripti.py --parametri parametrin_arvo` tai luetaan konfiguraatiotiedostosta. 

JavaScriptissä, nimenomaan Http-frontin kannalta, käyttäjän syöte poimitaan eventeistä. Tätä varten sinun tulee tutustua DOM-tapahtumiin. Tässä yksinkertainen esimerkki.

```js
const echoButton = document.querySelector("#echo-button");
echoButton.addEventListener("click", myFunction);
```

DOM on pahasti tämän pikakatsauksen skoopin ulkopuolella. Tutustu Mozillan dokumentaation [A first splash into JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/A_first_splash)-artikkeliin sekä saman sivuston [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)-dokumentaatioon.