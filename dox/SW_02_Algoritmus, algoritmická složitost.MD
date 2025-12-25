# SW 02 – Algoritmus, algoritmická složitost

## Algoritmus

Algoritmus je přesný postup, kterým lze vyřešit určitý problém.

Vlastnosti / požadavky:

### Elementárnost

* Skládá se z konečného počtu jednoduchých a srozumitelných kroků (příkazů)

### Konečnost

* Musí mít konečný počet kroků pro libovolný vstup

### Obecnost

* Neřeší konkrétní problém (kolik je 3\*7), ale obecnou třídu problémů (kolik je x\*y)
* Má širokou množinu možných vstupů

### Determinovanost

* Za stejných podmínek pro stejné vstupy poskytuje stejný výstup
* Každý krok algoritmu musí být jednoznačně definován

### Výstup

* Má alespoň jeden výstup v požadovaném vztahu ke vstupům → odpověď na problém, který algoritmus řeší

## Algoritmická složitost

Složitost algoritmu je jeho náročnost na „zdroje“: čas, paměť atd.

### Časová složitost

Zjištění časové složitosti pomocí měření času vykonání programu není dobrý přístup: je závislý na HW, OS atd. Dobrý přístup, pokud možno, je analýza algoritmu. Ta pracuje s tzv. elementární operací, jejíž čas pro vykonání definujeme jako 1 (jedna jednotka času). Při analýze algoritmu zjistíme počet provedených operací, který je závislý na velikosti vstupu 𝑛. Dostaneme funkci, kde nás zajímá nejrychleji rostoucí člen – zanedbáme pomaleji rostoucí členy a multiplikativní konstanty. Funkce nejrychleji roustoucího členu je hledaná časová složitost.

* Značí se `O()`, "omikron notace" – složitost algoritmu je asymptoticky ohraničena shora funkcí v&nbsp;závorce
* Zajímá nás kvalita algoritmu – časová složitost rozděluje algoritmy do kvalitativních kategorií

#### Příklad

```csharp
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

Selection sort najde v poli minimum (projede všech n prvků), dá ho na začátek a hledá nové minimum v dosud neseřazené části (takhle nkrát). Při zanedbání pomaleji rostoucích členů a konstant nám vyjde složitost `O(n**2)`.

Algoritmus, který náhodně zkouší všechny možnosti, dokud nenajde tu seřazenou, má složitost `O(n * n!)`. Pro každou permutaci (`n!`) je nutné zkontrolovat, zdali už je seřazeno (`n`).

## Rekurze

* Rekurzivní algoritmy volají samy sebe
* Určitá funkce je znovu volána dříve, než je dokončeno její předchozí volání
* Výhodou je usnadnění zápisu, čitelnost
* Nevýhodou je náročnost na paměť a procesor

__Přímá__: Podprogram volá přímo sám sebe

__Nepřímá__: Více podprogramů se volá navzájem a tvoří "kruh"

__Lineární__: Podprogram volá sám sebe vždy jednou

__Stromová__: Podprogram se volá více jak jednou v rámci jednoho svého úkolu (počet volání nemusí být nutně konstantní)

```csharp
uint Factorial(uint N) => (N == 0) ? 1 : Factorial(N - 1) * N;
```

```csharp
// Počítání prvků v binárním stromu od určité Node směrem dolů (třída Node obsahuje mj. Node left a Node right)
int Count(Node node)
{
    int result = 1;
    if (node.left != null) result += Count(node.left);
    if (node.right != null) result += Count(node.right);
    return result;
}
```

## Náhoda

* Šifrování, loterie, generace úrovní ve hrách, ...

__Pravá náhodná čísla__:

* Hardwarový generátor náhodných čísel
* Často založeno na mikroskopických jevech, které generují teoreticky zcela nepředvídatelné signály (např. tepelný šum)
* HW generátor má typicky převodník aspektu fyzikálního jevu na elektrický signál

__Pseudonáhodná čísla__:

* Zdánlivě náhodná čísla, později se sekvence opakují
* Jako základ (seed) použity např. hodiny v PC, které měří čas v ms

---

[>>>](./SW_03_Strukturované%20datové%20typy.MD)
