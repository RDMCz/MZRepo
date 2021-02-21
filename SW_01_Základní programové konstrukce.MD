# SW 01 – Základní programové konstrukce

* proměnné, datové typy, reference a hodnota, programy a podprogramy, operátory, priorita operátorů
* if, switch, cyklus

## Proměnné

Proměnná je místo v paměti, kam se ukládají data. Je to označení pro identifikátor, který uchovává určitou hodnotu při běhu programu.

## Datové typy + reference a hodnota

__Hodnotové:__ Hodnota je v paměti uložena přímo a přímo se k ní přistupuje. Mají pevnou velikost.

* `int` a jiné celočíselné
* `float` a jiné desetinné
* `char`
* `bool`
* `enum`
* `struct`

__Referenční:__ Neuchovává přímo hodnotu samotnou, ale odkaz na místo v paměti (konkrétně na hromadu, kde je skutečný objekt uložen)

* `object` – alias třídy _`System.Object`_, všechny ostatní třídy z ní dědí
* `string`
* `class`
* `interface`
* `array`
* `delegate`

## Programy a podprogramy

__Program:__ Posloupnost instrukcí popisující realizaci dané úlohy počítačem.

__Podprogram:__ (subroutine) Část programu

* Lze opakovaně použít kdekoliv v programu (i v podprogramu)
* Může mít vstupní parametry
* Může mít návratovou hodnotu
* V C# metoda
* Obecně funkce vrací hodnotu, procedura ne

## Operátory + priorita operátorů

kategorie | operátor
--- | ---
__primární__ | závorky `(x)`, přístup ke členu `x.y`, invokace `f(x)`, indexer `a[x]`, `x++`, `x--`, `new`
__unární__| `+x`, `-x`, `!`, bitová negace `~`, `++x`, `--x`, přetypování `(T)x`, `true`, `false`
__rozsah__| `x..y`
__multiplikativní__| `*`, `/`, modulo `%`
__aditivní__| součet `+`, rozdíl `-`
__bitové posuny__| `<<`, `>>`
__relační__| `<`, `>`, `<=`, `>=`, `is`, `as`
__rovnost__| `==`, `!=`
__bit AND__| `&`
__bit XOR__| `^`
__bit OR__| `\|`
__AND__| `&&`
__OR__| `\|\|`
__ternární__| `? :`
__přiřazení a lambda__| `=`, `*=`, `/=`, `%=`, `+=`, `-=`, `<<=`, `>>=`, `&=`, `^=`, `\|=`, `=>`

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
