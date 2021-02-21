# SW 07 – Podprogramy

* Podprogramy, funkce, metody, delegáty, lambda operátory, návratové hodnoty, oblast platnosti proměnné.

## Podprogramy

__Program:__ Posloupnost instrukcí popisující realizaci dané úlohy počítačem.

__Podprogram:__ (subroutine) Část programu

* Lze opakovaně použít kdekoliv v programu (i v podprogramu)
* Může mít vstupní parametry
* Může mít návratovou hodnotu
* V C# metoda
* Obecně funkce vrací hodnotu, procedura ne

## Funkce + metody

* ~Obecně __funkce__ = podprogram; __metoda__ = funkce (podprogram) uvnitř objektu. Metoda je OOP ekvivalent pro funkci.
* V C# funkce nejsou, pouze metody
* Parametry metodě jsou předávány hodnotou. Metoda získá kopii parametrů a jakékoliv modifikace uvnitř metody se nepromítnou zpět. (Toto platí pro hodnotové datové typy, ne pro referenční)
  * Lze předat parametr odkazem pomocí klíčového slova `ref`, použité proměnné musí být předem inicializovány
  * Parametry lze definovat jako výstupní (klíčové slovo `out`)

    ``` csharp
    static void LowerUpperText(string input, out string low, out string up)
    {
        low = input.ToLower();
        up = input.ToUpper();
    }

    // Main:
    string s = "aHoJ";
    string sUp = "blabla";
    LowerUpperText(s, out string sLow, out sUp);    // Proměnnou lze deklarovat až při volání (sLow) nebo už před tím (sUp)
    
    WriteLine(s);       // aHoJ
    WriteLine(sLow);    // ahoj
    WriteLine(sUp);     // AHOJ
    ```

  * Metoda s proměnným počtem parametrů:
    * Klíčové slovo `params` před posledním z parametrů. Typ tohoto parametru musí být pole.

        ``` csharp
        public void SomeMethod(params object[] p) { } // Proměnný počet parametrů
        ```

## Delegáty

* "Typově bezpečný ukazatel na metodu"
* Nemusí být interně spojen s jednou metodou, podporuje množinou metod (lze přidat pomocí `+=` nebo `+`)
* Odděluje specifikaci od implementace

``` csharp
public delegate void NumberAction(int x);

public static void Double(int x) => WriteLine(x * 2);
public static void Triple(int x) => WriteLine(x * 3);

public static void DoNumberAction(int x, NumberAction del) // Delegát (~předpis pro metodu) jako vstupní parametr
{
    del(x); // Provede metody, na které delegát ukazuje
}

static void Main(string[] args)
{
    NumberAction del = new NumberAction(Double);
    del += Triple; // K delegátovy lze přidat Double a Triple, protože mají stejnou signaturu (návratový typ a vstupní parametry) 

    DoNumberAction(5, del);
}
// Output:
// 10
// 15
```

## Lambda operátory

* Vycházejí z anonymních delegátů – jakýkoliv lambda výraz lze přepsat na delegáta
  * výraz bez návratové hodnoty `Action`

    ``` csharp
    Action<string> greet = name => WriteLine($"Hello {name}!");
    greet("World"); // "Hello World!"
    ```

  * výraz s návratovou hodnotou `Func`

    ``` csharp
    Func<int, int> square = x => x * x; // Func<T,TResult>
    Console.WriteLine(square(5)); // 25
    ```

__Lambda + LINQ:__

``` csharp
int[] numbers = { 2, 3, 4, 5 };
foreach (var v in numbers.Select(x => x * x)) Write(v + " "); // 4 9 16 25
```

* Lambda lze použít i pro zkrácený zápis metod, switche apod.

__Upravený příklad z delegátů pomocí lambdy:__

``` csharp
public delegate void NumberAction(int x);

public static void DoNumberAction(int x, NumberAction del) => del(x);

static void Main(string[] args)
{
    NumberAction del = (int x) => WriteLine(x * 2); // (Double)
    del += (int x) => WriteLine(x * 3); // (Triple)

    DoNumberAction(5, del);
}
```

__nebo:__

``` csharp
    NumberAction del = (int x) => { WriteLine(x * 2); WriteLine(x * 3); };
    DoNumberAction(5, del);
```

__nebo:__

``` csharp
    DoNumberAction(5, (int x) => WriteLine(x * 2));
    DoNumberAction(5, (int x) => WriteLine(x * 3)); // Tady asi nejdou spojit do jednoho (?)
```

``` csharp
// Always the same output:
// 10
// 15
```

## Oblast platnosti proměnné

* Class Level Scope
* Method Level Scope
* Block Level Scope