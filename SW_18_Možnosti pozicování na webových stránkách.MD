# SW 18 – Možnosti pozicování na webových stránkách

## Statické pozicování

* Výchozí pozicování prvků v HTML je _`static`_
* Prvky jsou za sebou (block) nebo vedle sebe (inline)

__Blokový prvek:__

* Vždy začíná na novém řádku
* Využívá plnou šířku, kterou má k dispozici
* Na rozdíl od inline prvků má __`margin-top`__ a __`margin-bottom`__
* `<div>`, `<h1>`, ...

__Inline prvek:__

* Nezačíná na novém řádku, může jich být víc vedle sebe
* Zabírá jen tolik šířky, kolik potřebuje
* `<span>`, `<a>`, ...

## Obtékání (Float)

* Stará metoda pozicování, dříve používáná na návrh celého layoutu
* Dnes se používá pouze pro obrázek obtékaný textem
* __`float:`__ _`left;`_ / _`right;`_ / _`none;`_ (default) / _`inherit;`_
* Pokud má více prvků stejnou hodnotu float, jsou vedle sebe

## Relativní pozicování

* Posunutí prvku o určité souřadnice (pozice je relativní k výchozí pozici)
* __`position:`__ _`relative;`_
* __`left:`__ / __`right:`__ / __`top:`__ / __`bottom:`__ _`30px;`_

## Absolutní pozicování

* Prvek je relativně pozicován ke svému pozicovanému rodiči (pozicovaný prvek je jakýkoliv prvek, co není statický)
* Levý horní roh rodiče jsou souřadnice 0,0 – U umístění vnitřních prvků se nemusí dopočítávat souřadnice relativně k celé stránce

## Fixní pozicování

* Prvek je pozicován relativně k viewportu
* Vždy zůstane na tom stejném místě

## Sticky

* __`position:`__ _`sticky;`_ má relativní pozici, pokud se ale dostane mimo zobrazení (např. kvůli skrolování), přepne se na fixní pozici

## Flexbox

* Definuje kontejner a prvky v něm umístěné
* __`display:`__ _`flex;`_
* U prvků ve flexboxu lze určovat směr, pořadí, zarovnání, mezery mezi nimi, zalomení na nový řádek ...
* Galerie, navbary

## Grid

* Rozděluje stránku na síť zarážek – řádky a sloupce
* Definuje se počet a velikost sloupců / řádků
* Prvky se umisťují do jednoho nebo několika sloupců / řádků
* __`display:`__ _`grid;`_
* Použití: Hlavní vnější kostra webu pomocí Grid, detaily pomocí Flex, super detaily pomocí pozicování

Flex a Grid fungují velmi dobře pro Media Queries (zobrazení na mobilu / tabletu / PC / TV / ...)

## Tabulka (Table)

* Nejstarší způsob pozicování, dnes se používá především na výpis tabulkových dat
* Také se používá na pozicování v e-mailech – e-mailoví klienti mohou ignorovat moderní pozicovací techniky
* `colspan`, `rowspan`
* Jednoduché na použití, ale neresponzivní, nemá tolik možností, hlasové čtečky pak web čtou jako tabulku

```html
<table>
    <thead>
        <tr>
            <th></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td></td>
        </tr>
    </tbody>
</table>
```
