# SW 02 – Algoritmus, algoritmická složitost

## Algoritmus

Algoritmus je přesný postup, kterým lze vyřešit určitý problém.

Vlastnosti / požadavky:

### Elementárnost

* Skládá se z konečného počtu jednoduchých a snadno srozumitelných kroků (příkazů)

### Konečnost

* Musí mít konečný počet kroků – pro každý jednotlivý vstup musí být konečný

### Obecnost

* Neřeší konkrétní problém (kolik je 3\*7), ale obecnou třídu problémů (kolik je x\*y)
* Má širokou množinu možných vstupů

### Determinovanost

* Za stejných podmínek pro stejné vstupy poskytuje stejný výstup
* Toto je vyžadováno pokud není vyžadován náhodný výstup
* Každý krok algoritmu musí být jednoznačně definován

### Výstup

* Má alespoň jeden výstup v požadovaném vztahu ke vstupům = odpověď na problém, který algoritmus řeší

## Algoritmická složitost

### Časová složitost

* Doba, jak dlouho algoritmus běží
* Počítají se provedené příkazy (elementární operace) v závislosti na velikosti vstupu
* Značí se `O()`, na konstantách v závorce nezáleží (lze je zanedbat)
* "Omikron notace":  složitost algoritmu je asymptoticky menší nebo rovna hodnotě v závorce
* Zajímá nás kvalita algoritmu – časová složitost rozděluje algortimy do kvalitativních kategorií

#### Příklad

``` csharp
int minIndex;
int temp;
// Pro každý prvek
for (int i = 0; i < pole.Length; i++) {
    // Najít minimum (od aktuálního prvku do konce)
    minIndex = i;
    for (int j = i; j < pole.Length; j++) {
        if (pole[j] < pole[minIndex]) {
            minIndex = j;
        }
    }
    // Dát minimum na začátek (prohodit minimum za aktuální prvek)
    temp = pole[minIndex];
    pole[minIndex] = pole[i];
    pole[i] = temp;
}
```

Selection sort najde v poli minimum (projede všech n prvků, to trvá n), dá ho na začátek a hledá nové minimum (takhle nkrát). Náročnost je tedy `O(n**2)`, stejně jako u bubble sortu.

Algoritmus, který by zkoušel všechny možnosti, dokud nenajde tu seřazenou (permutace), by měl náročnost `O(n!)`.

## Rekurze

* Rekurzivní algoritmy volají samy sebe
* Určitá funkce je znovu volána dříve, než je dokončeno její předchozí volání
* Výhodou je usnadnění zápisu, čitelnost
* Nevýhodou je náročnost na paměť a procesor

__Přímá__: Podprogram volá přímo sám sebe

__Nepřímá__: Více podprogramů se volá navzájem a tvoří "kruh"

__Lineární__: Podprogram volá sám sebe vždy jednou

__Stromová__: Podprogram se volá více jak jednou v rámci jednoho svého úkolu (nemusí být konstantní počet volání)

``` csharp
uint Factorial(uint N) => (N == 0) ? 1 : Factorial(N - 1) * N;
```

``` csharp
// Počítání prvků v binárním stromu od určité Node směrem dolů (třída Node obsahuje mj. Node left a Node right)
int Count(Node temp)
{
    int rtrn = 1;
    if (temp.left != null) rtrn += Count(temp.left);
    if (temp.right != null) rtrn += Count(temp.right);
    return rtrn;
}
```

## Náhodnost

* Šifrování, simulace, generace úrovní ve hrách, ...

__Pravá náhodná čísla__:

* Hardwarový generátor náhodných čísel
* Často založeno na mikroskopických jevech, které generují teoreticky zcela nepředvídatelné signály (např. tepelný šum)
* HW generátor má typicky převodník aspektu fyzikálního jevu na elektrický signál

__Pseudonáhodná čísla__:

* Zdánlivě náhodná čísla, později se sekvence opakují
* Jako základ (seed) použity např. hodiny v PC, které měří čas v ms
