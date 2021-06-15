# SW 01 – Základní programové konstrukce

## Proměnné

* Proměnná je místo v paměti, kam se ukládají data
* Je to označení pro identifikátor, který uchovává určitou hodnotu při běhu programu
* Proměnnou deklarujeme specifikováním datového typu, názvu a popř. hodnoty

## Datové typy, reference a hodnota

* Zásobník a hromada (halda) se nacházejí v paměti RAM
* Tuto paměť přiděluje programu (vláknu) OS
* Zásobník je rychlý ale má omezenou velikost
* Hromada je ~neomezená paměť se složitějším (pomalejším) přístupem

### Hodnotové datové typy

* Hodnota je uložena v zásobníku a program s ní pracuje přímo
* Mají pevnou velikost
* Lze dělit na základní typy, struktury a výčtové typy
* V programu se jich vyskytuje mnoho a zabírají málo místa, chceme s nimi pracovat co nejrychleji
* `int` a jiné celočíselné (`byte`, `short`, `long`)
* `float` a jiné s plovoucí řádovou čárkou (`double`)
* `char`
* `bool`
* `struct`
* `enum`

### Referenční datové typy

* V zásobníku neuchovává přímo hodnotu samotnou, ale pouze odkaz (referenci) na místo v paměti
  * Konkrétně na hromadu, kde je skutečný objekt uložen
* Na jeden objekt může být více referencí a můžeme vytvářet objekty s dynamickou velikostí
* O to, aby na hromadě nebyla data s žádnou referencí, se stará garbage collector
* `object` – alias třídy _`System.Object`_, všechny ostatní třídy z ní dědí
* `string` – navenek se ale chová spíše jako hodnotový typ pro zpříjemnění práce programátora
* `class`
* `interface`
* `array`
* `delegate`

## Programy a podprogramy

__Program:__ Posloupnost instrukcí popisující realizaci dané úlohy počítačem

__Podprogram__ (subroutine): Část programu

* Lze opakovaně použít kdekoliv v programu (i v podprogramu)
* Může mít vstupní parametry
* Může mít návratovou hodnotu
* V C# metoda
* Obecně funkce vrací hodnotu, procedura ne

## Operátory + priorita operátorů

kategorie | operátor
--- | ---
__primární__ | závorky `(x)`, přístup ke členu `x.y`, invokace `f(x)`, indexer `a[x]`, `x++`, `x--`, `new`
__unární__ | `+x`, `-x`, `!`, bitová negace `~`, `++x`, `--x`, přetypování `(T)x`, `true`, `false`
rozsah | `x..y`
__multiplikativní__ | `*`, `/`, modulo `%`
__aditivní__ | součet `+`, rozdíl `-`
bitové posuny | `<<`, `>>`
__relační__ | `<`, `>`, `<=`, `>=`, `is`, `as`
__rovnost__ | `==`, `!=`
bit AND | `&`
bit XOR | `^`
bit OR | `\|`
__AND__ | `&&`
__OR__ | `\|\|`
__ternární__ | `? :`
__přiřazení a lambda__ | `=`, `*=`, `/=`, `%=`, `+=`, `-=`, `<<=`, `>>=`, `&=`, `^=`, `\|=`, `=>`

## Podmíněné příkazy

__úplný if__:

``` csharp
if (podmínka) {

}
else {

}
```

__neúplný if__:

``` csharp
if (podmínka) {

}
```

__switch__:

``` csharp
switch (výraz) {
    case hodnota0:
        break;
    case hodnota1:
        break;
    default:
        break;
}
```

## Cykly

__while__:

``` csharp
while (podmínka) {
    // nemusí se provést vůbec
}
```

__do while__:

``` csharp
do {
    // provede se alespoň jednou
} while (podmínka)
```

__for__:

``` csharp
for (inicializátor; podmínka; iterátor) {

}
```

__foreach__:

``` csharp
foreach (object obj in pole) {
    // pro každý prvek datového typu implementujícího IEnumerable
}
```

---
---

![typy](http://www.cs.vsb.cz/behalek/vyuka/pcsharp/text/resources/3.jpg)

![memory](https://www.itnetwork.cz/images/5/csp/pamet_zasobnik_halda.png)
