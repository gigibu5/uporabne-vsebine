# RAO JS povzetek

Izpis: console.log(vrednost);

## Spremenljivke
### Deklaracija
```js
let a = 5; // Spremenljivka ustvarjena znotraj scopa (se ne vidi npr. iz funkcije, if-a, ipd.)
var a = 5; // Globalna spremneljivka, se ne priporoča
const a = 5; // Konstantna spremenljivka, se ne more spreminjat
```

### Operacije
+, -, *, /, %, ++, --, +=, -=, *=, /=, %=, ...

## Funkcije
### Obične funkcije
```js
// primer
function ime_funkcije(arg1, arg2) {
	return arg1 * arg2;
}
```

### Puščične funkcije (pretvorba zgornje v puščično)
1. Function nadomestiš s `let` (deklaracija spremenljivke), med ime_funkcije in argumente vstaviš `=`, med argumente in `{` vstaviš `=>`
```js
let ime_funkcije = (arg1, arg2) => {
	return arg1 * arg2;
}
```
2. Če ima funkcija samo en ukaz, lahko izpustiš `{}`
```js
let ime_funkcije = (arg1, arg2) => return arg1 * arg2;
```
3. Če ima funkcija samo `return`, ga lahko izpustimo
```js
let ime_funkcije = (arg1, arg2) => arg1 * arg2;
```

## Objekti
### Osnovni objekti
Objekt je deklariran samo s lastnostmi
```js
let avto = {znamka: "Volvo", model: "V60", letnik: 2013};
```

### Objekti s konstruktorji
```js
function Avto(znamka, model, letnik){
	this.znamka = znamka;
	this.model = model;
	this.letnik = letnik;
}

let x = new Avto("Volvo", "V60", 2013);
```

### Metode
#### Metode kot funkcije (osebno mi ni všeč)
```js
function izpisZnamke(){ // funkcija je globalna in se lahko uporablja na katerem koli objektu
	console.log(this.znamka)
}

avto.izpisZnamke();
```

#### Metode kot atributi (osebno priporočam)
```js
function Avto(znamka, model, letnik){
	this.znamka = znamka;
	this.model = model;
	this.letnik = letnik;

	// definicija metode
	this.izpisZnamke = () => {
		console.log(this.znamka)
	}
}

let x = new Avto("Volvo", "V60", 2013);
x.izpisZnamke();
```

## Tabele
### Deklaracija
```js
let a = []; // prazna tabela
let b = [1, 3, 5, 7, 8, 66, 3]; // Polna tabela
```

### Pomenbne metode tabel
```js
a = b.pop() // Izbriše zadnji element in ga vrne v a
b.push(20) // Doda element 20 na konec tabele
a = b.shift() // Izbriše prvi element in ga vrne v a
b.unshift(20) // Doda element 20 na začetek tabele

b.sort() // sortira tabelo
b.reverse() // sortira od uzad

b.length // "vrne" dolžino tabele
```

## HTML DOM (Document Object Model)
### Pridobivanje elementov
```js
document.getElementById("ajdi"); // Vrne 1 element, ki ima id="ajdi"
document.getElementsByClassName("klas"); // Vrne tabelo vseh elementov, ki imajo class="klas"
document.getElementsByTagName("znacka"); // Vrne tabelo vseh elementov, ki so značka znacka npr. p
```

### Atributi elementov
```js
element.innerHTML; // besedilo v elementu
element.style.atribut; // nastavljanje stilskih atributov (color = color, font-family = fontFamily)

element.setAttribute("atribut", "vrednost"); // nastavi atribut "atribut" na vrednost "vrednost"
```

### Dodajanje in brisanje elementov
```js
let gumb = document.createElement("button"); // ustvari element button
document.body.appendChild(gumb); // Doda element gumb v body (med pikama)
document.body.removeChild(gumb); // Odstrani element gumb iz bodya

let gumb2 = document.createElement("button"); // ustvari nov element button
document.body.replaceChild(gumb2, gumb); // nadomesti gumb z gumb2
```

### Atributi DOM elementov
```js
gumb.parentElement // Starševski element (element v katerem se nahaja)
gumb.childElementCount // Število otrok (elementov, ki se nahajajo v njem)
gumb.childNodes // Tabela vseh otrok (elementov, ki se nahajajo v njem)
```

### Dodajanje stimulantov (zna bit napačn izraz)
Ko kliknemo gumb, se bo na zaslonu pojavilo obvestilo "Kliknil si gumb [besedilo]"
```js
gumb.addEventListener("click", () => {
	alert("Kliknil si gumb " + this.innerHTML);
});
```

Nastavljive akcije
- click
- mouseover
- mousedown
- mouseup
- https://www.w3schools.com/js/js_events_examples.asp

### Primer: izpis tabele velikosti x * y v JS-u z vsebino
```js
let x = 10;
let y = 10;
let vsebina = "Nek tekst";

let tabela = document.getElementById("tabela"); // Vzamemo element iz HTML-ja

for(let i = 0; i < x; i++){ // vse vrstice
	let vrstica = document.createElement("tr"); // ustvarimo vrstico
	for(let j = 0; j < y; j++){ // vsi stolpci
		let celica = document.createElement("td"); // ustvarimo posamezno celico
		celica.innerHTML = vsebina; // nastavimo ji vsebino
		vrstica.appendChild(celica); // dodamo celico v vrstico
	}
	tabela.appendChild(vrstica); // dodamo vrstico v tabelo
}
``` 

## Knjižnjica Math
```js
Math.random(); // vrne naključno vrednost v intervalu [0, 1)
Math.floor(3.2); // zaokroži navzdol - 3
Math.ceil(3.2); // zaokroži navzgor - 4
Math.trunc(3.2); // vrne samo celi del - 3
Math.abs(3.2); // vrne absolutno vrednost - 3.2
```

## Try in Catch
```js
try {
	// neka koda, se izvede, če pride do napake, skoči na catch
}
catch(err){
	console.log(err); // izpiše napako
}
```
Lahko dodamo svoje napake
```js
throw "Poljubno besedilo"; // ko bo koda izvedena, bo to izpis napake ko pride do te vrstice
```
