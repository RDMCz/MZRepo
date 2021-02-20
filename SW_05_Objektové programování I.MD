# SW 05 – Objektové programování I

* Strukturované a objektové programování, objekt, třída, základní objektové vlastnosti, třídy abstraktní, zapouzdřené a rozhraní.
* Příkladem budiž zvířata a jejich zvuky

## Strukturované a objektové programování

= paradigmata (programovací styly)

__Strukturované__: Využívá bloků (`{}`), podmínek (`if`/`else`), cyklů (`for`/`while`), podprogramů ad. namísto skoků (`GOTO` vede ke špagetovému kódu)

__Objektové__:

* Založeno na objektech obsahující data (atributy/vlastnosti) a kód (metody)
* Obsahuje praktiky ze strukturovaného paradigmatu (podmínky/cykly)

## Objekt

* neboli instance
* V podstatě místo v paměti alokované a nakonfigurované třídou / strukturou.
* Program může vytvořit několik objektů stejné třídy / struktury.
* Může být uložen v proměnné / kolekci.
* V C# je třída _Object_ nejvyšší základní třída.

### Dědičnost (Inheritance)

* Tvoření nových datových struktur na základě starých
* Dědící třída používá (dědí), rozšiřuje nebo modifikuje chování rodičovské třídy.
* V C# lze mít pouze jednoho rodiče (single inheritance only)
* Konstruktory a destruktory se nedědí, každá třída si musí definovat svůj vlastní

#### Zapouzdření (Encapsulation)

* = Zabalení dat a metod a restrikce přístupu k nim. Používá se pro skrytí dat ve třídě.
* `private` – Ke členům třídy mají přístup třídy, které z ní dědí a jsou v ní "nested" (`public class A { public class B : A { } }`)
* `protected` – Ke členům třídy mají přístup třídy, které z ní dědí
* `internal` – Ke členům třídy mají přístup třídy, které z ní dědí a nachází se ve stejném "[sestavení](https://docs.microsoft.com/cs-cz/dotnet/standard/assembly/)"
* `public` – Ke členům třídy mají přístup ~všichni

### Polymorfismus (Polymorphism)

* Podstatou jsou metody, které mají všichni potomci definované se stejnou hlavičkou, ale jiným tělem
* V C# `virtual` + `override`

## Třída

* Referenční datový typ
* Vzor pro tvorbu objektů

### Abstraktní třída

* Abstrakce = skrytí určitých detailů a zobrazení jen nejdůležitějších informací
* Modifikátor `abstract` může používat třída, metoda, vlastnost, indexer, událost
* Abstraktní třída je myšlena pouze jako základ pro ostatní třídy, nelze z ní vytvořit instanci
* Abstraktní členy lze použít pouze v abstraktní třídě, mají pouze hlavičku, tělo je definováno v dědících třídách (pomocí `override` protože Abstraktní člen je automaticky virtuální)

## Rozhraní

* Neboli jak je objekt viditelný zvenku
* Obsahuje výčet metod, vlastností, indexerů, událostí (pouze hlavička bez těla ([od C# 8.0 může mít i tělo ?](https://www.infoq.com/articles/default-interface-methods-cs8/)))
* Všechny členy jsou automaticky veřejné
* Třída implementující rozhraní musí obsahovat všechny jeho členy
* Nelze z něj vytvořit instanci
* V C# může třída dědit jen z jedné třídy, může ale implementovat více rozhraní. Rozhraní také mohou implementovat rozhraní.
