# SW 05 – Objektové programování I

## Strukturované a objektové programování

= paradigmata (programovací styly)

__Strukturované__: Využívá bloků (`{}`), podmínek (`if`/`else`), cyklů (`for`/`while`), podprogramů ad. namísto skoků (`GOTO` vede ke špagetovému kódu)

__Objektové__:

* Založeno na objektech obsahující data (atributy/vlastnosti) a kód (metody)
* Obsahuje praktiky ze strukturovaného paradigmatu (podmínky/cykly)

## Objekt

* neboli instance
* V podstatě místo v paměti alokované a nakonfigurované třídou/strukturou
* Program může vytvořit několik objektů stejné třídy/struktury
* Může být uložen v proměnné/kolekci
* V C# je třída _Object_ nejvyšší základní třída

### Dědičnost (Inheritance)

* Tvoření nových datových struktur na základě starých
* Dědící třída používá (dědí), rozšiřuje nebo modifikuje chování rodičovské třídy
* V C# lze mít pouze jednoho rodiče (single inheritance only)
* Konstruktory a destruktory se nedědí, každá třída si musí definovat svůj vlastní (spuštění původního pomocí `: base()`)
* Podporuje koncept znovupoužitelnosti, méně redundantního kódu
* Rodič = super/base/parent class; Potomek = sub/derived/extended/child class
* Ze `sealed` třídy nelze dědit

### Zapouzdření (Encapsulation)

* = Zabalení dat a metod a restrikce přístupu k nim. Používá se pro skrytí dat ve třídě.
* `private` – Ke členům třídy mají přístup třídy, které z ní dědí a jsou v ní "nested" (`public class A { public class B : A { } }`)
* `private protected` – Ke členům třídy mají přístup třídy, které z ní dědí a nachází se ve stejném sestavení (stejné dll/exe)
* `protected` – Ke členům třídy mají přístup třídy, které z ní dědí
* `internal` – Ke členům třídy mají přístup všechny třídy ve stejném sestavení
* `protected internal` – Ke členům třídy mají přístup všechny třídy ve stejném sestavení nebo třídy, které z ní dědí
* `public` – Ke členům třídy mají přístup všechny třídy

### Polymorfismus (Polymorphism)

* Podstatou jsou metody, které mají všichni potomci definované se stejnou hlavičkou, ale jiným tělem (jiná implementace "stejných" metod)
* V C# `virtual` + `override`

### Abstrakce (Abstraction)

* Obecně skrytí určitých detailů a zobrazení jen nejdůležitějších informací

## Třída

* Referenční datový typ
* Vzor pro tvorbu objektů

### Abstraktní třída

* Modifikátor `abstract` může používat třída, metoda, vlastnost, indexer, událost
* Abstraktní třída je myšlena pouze jako základ pro ostatní třídy, nelze z ní vytvořit instanci
* Abstraktní členy lze použít pouze v abstraktní třídě, mají pouze hlavičku, tělo je definováno v dědících třídách (pomocí `override` protože abstraktní člen je automaticky virtuální)

### Statická třída

* Nemohou z ní být tvořeny instance, nelze z ní dědit
* Modifikátor `static` u třídy vyžaduje, aby měla všechny členy také statické
* U této třídy nelze tedy použít klíčové slovo `new`, ke členům třídy se přistupuje přes jméno třídy samotné

### Statický konstruktor

* Jakákoliv třída může mít statický konstruktor (i vedle "normálního" konstruktoru)
* Nemůže mít vstupní parametry
* Volá se automaticky (před vytvořením první instance nebo použitím statického členu), aby inicializoval statické atributy (nebo vlastnosti) dané třídy; k nestatickým atributům přístup nemá

### Zapečetěná třída

* Modifikátor `sealed`
* Z třídy nelze dědit
* Modifikátor také lze použít na přepsané (override) metody, aby již nešly přepisovat v dalších potomcích

### Částečná třída

* Modifikátor `partial`
* Definice tříd, struktur a rozhraní lze rozdělit do více zdrojových souborů
* Všechny části se zkombinují při kompilaci

### Privátní konstruktor

* Pokud má třída privátní konstruktor, nemohou z ní ostatní třídy (kromě nested potomků) vytvářet instance
* Použití, pokud má třída metodu, která vrací její instanci
* Nebo pokud třída nemá žádné _instance methods_ (~metody vyžadující vytvoření instance pro své volání), příkladem je knihovna Math
* (Pokud má třída všechny členy statické, doporučuje se i třídu samotnou udělat statickou)

## Rozhraní

* Neboli jak je objekt viditelný zvenku
* Obsahuje výčet metod, vlastností, indexerů, událostí (pouze hlavička bez těla ([od C# 8.0 může mít i tělo ?](https://www.infoq.com/articles/default-interface-methods-cs8/)))
* Všechny členy jsou automaticky veřejné
* Třída implementující rozhraní musí obsahovat všechny jeho členy
* Nelze z něj vytvořit instanci
* V C# může třída dědit jen z jedné třídy, může ale implementovat více rozhraní. Rozhraní také mohou implementovat rozhraní.
