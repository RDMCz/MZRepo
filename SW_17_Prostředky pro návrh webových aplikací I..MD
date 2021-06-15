# SW 17 – Prostředky pro návrh webových aplikací I

## HTML (Hypertext Markup Language)

* Značkovací jazyk pro tvorbu webových stránek propojených hypertextovými odkazy

``` html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <link rel="stylesheet" href="styles.css" />
        <title>Titulek stránky</title>
    </head>
    <body>
        <!-- komentář -->
    </body>
</html>
```

## CSS (Cascading Style Sheets)

* Style sheet language pro popis způsobu zobrazení elementů na stránkách napsaných v HTML (také XHTML, XML, SVG, XUL)
* Navržen pro oddělení prezentace (vizuálu – barvy, layout, fonty) od obsahu
* Více stránek může čerpat z jednoho .css souboru – zbavení se redundance + soubor zůstance v cache = rychlejší načítání
* Podpora Media Queries – jiné zobrazení na PC / Mobilu / vytisknuté / přečteno čtečkou / ...
* Priorita:
  1. Inline (uvnitř html elementu) `<p style="color: red">Červený text</p>`
  2. Externí a interní (v hlavičce html) `<head><style>p {color: red;}</style></head>`
  3. Browser default

### Selektory

* `*` – vybere všechny elementy
* `p` – vybere všechny elemety `<p>`
* `p, div` – vybere všechny elemety `<p>` a `<div>`
* `.class` – vybere elementy s `class="class"`
* `p.class` – vybere všechny elemety `<p>` s `class="class"`
* `#id` – vybere elementy s id="id"

## JavaScript

* Multiparadigmatický vyšší programovací jazyk
* Dynamické přiřazení typů, funkce první třídy (funkce jsou také objekty – mají atributy a lze je předat dále)
* Společně s html a css tvoří základ www
* Většina stránek ho používá pro definici chování na straně klienta (může ale běžet i na serveru)
* Dokáže upravovat atributy html i css prvků
* Frameworky:
  * Frontend: React, Angular, Vue
  * Backend: Express, Next, Meteor

``` html
<p id="demo">Text</p>
<button type="button" onclick="changeText()">Změnit</button>
```

``` javascript
function changeText() {
    document.getElementById("demo").innerHTML = "Změněný text";
}
```

## Značka (Tag)

* HTML element je zapsán počáteční (a koncovou) značkou, mezi nimiž může být text (obsah)
* Počáteční značka může obsahovat atributy s hodnotami
* Párové `<p></p>` a nepárové `<br>`
* `<tag atribut="hodnota">obsah</tag>`

## Atribut

* Dodávají elementům dodatečné informace
* Všechny html elementy mohou mít atributy
* Umožňují nastavit `id`, `class`, `style`

``` html
<img src="cesta_k_obrázku" width="šířka" height="výška" alt="placeholder">
<a href="adresa">Odkaz</a>
<html lang="cs"></html>
<p title="tooltip">Text</p> 
```

## Sémantický význam značek

* Obsah dokumentu se značí podle toho, o jaký druh informace se jedná
* Značky implikují význam, nikoliv instrukce pro vzhled
* `<!DOCTYPE>` – Definuje typ dokumentu
* `<html>` – Definuje html dokument
* `<head>` – Obsahuje metadata + informace pro dokument
* `<title>` – Titulek dokumentu
* `<body>` – Tělo dokumentu
* `<h1-6>` – Nadpis
* `<p>` – Odstavec
* `<br>` – Zalomení řádku
* `<hr>` – Horizontální oddělovací čára
* `<blockquote>` – Bloková citace
* `<code>` – Zdrojový kód
* `<em>` – Zvýrazněné písmo – kurzíva
* `<strong>` – Důležité písmo – tučně
* `<form>` – Formulář – `<input>`, `<textarea>`, `<button>`, `<select>`, `<label>`
* `<img>` – Obrázek
* `<svg>` – Kontejner pro SVG (vektor) grafiku
* `<a>` – Hypertextový odkaz
* `<nav>` – Navigační odkaz
* `<li>` – Prvek v bullet (`<ul>`) nebo číslovaném (`<ol>`) seznamu
* `<table>` – Tabulka – `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>`
* `<div>` – Rozdělelní na sekce, kontejner
* `<span>` – Inline kontejner
* `<header>`, `<main>`, `<footer>`
