# SW 9 – Návrhové vzory II

* Návrhové vzory pro skrývání implementace, optimalizaci rozhraní.

## Zástupce (proxy)

* Umožňuje řídit přístup k celému/částečnému rozhraní objektu přes jiný zastupující objekt

### Vzdálený zástupce (remote proxy)

* Zastupuje objekt umístěný někde jinde
* Zařizuje (serverovou) komunikaci se vzdáleným objektem
* Měl by být připraven i na selhání spojení (vyhodit odpovídající výjimku)

### Virtuální zástupce (virtual proxy)

* Také zastupuje jiný objekt
* Vytvoření objektu se nechává na poslední chvíli (objekt ani být vytvořen nemusí) a chování objektu se předstírá
* Použití: lazy loading obrázků / dat z databáze

### Ochranný zástupce (protection proxy)

* Zakrývá identitu zastupovaného objektu
* nabízí jen podmnožinu metod zastupovaného objektu, lze implementovat kontrolu přístupových práv
* Implementace skrytím za rozhraní nebo za proxy třídu spravující instanci objektu

``` csharp
public class Zastupce
{
    private Zastupovany z;
    public void Metoda() => z.Metoda();
}
```

### Chytrý odkaz (smart reference)

* Návrhový vzor spadající pod zástupce
* Doplnění komunikace s objektem o další akce, typicky kvůli zrychlení a zefektivnění aplikace
* Virtuální zástupce je také chytrý odkaz – rozhoduje, kdy přistoupí k originálnímu objektu a kdy načte hodnoty z cache / metadata

## Příkaz (Command)

* Objekt je použit k zapouzdření všech informací potřebných ke zpožděnému spuštění události
* Zapouzdření příkazu do třídy a používání ho jako proměnné z důvodu
  * přidání příkazu do fronty
  * rekonstrukce historie příkazů – implementace undo/redo
* Použití ve WPF/UWP – `ICommand(Execute, CanExecute)`

## Iterátor (iterator)

* Také známý jako Enumerator
* Samostatný objekt umožňující lineární procházení kolekcemi bez znalosti jejich vnitřní implementace
* V C# na kolekce implementující `IEnemuretor` lze použít `foreach` = __Implicitní iterátor__
* __Explicitní iterátor__ si musíme sami napsat, instance iterátoru na požádání vrací odkaz na další prvek v kolekci, dokud nedojede k prvku poslednímu
* __Externí iterátor__: průchod kolekcí řídí klient s využitím iterátoru; složitější, ale mocnější řešení
* __Interní iterátor__: průchod kolekcí řídí iterátor sám; klient specifikuje , co provádět s prvky kolekce (např pomocí LINQ + lambda)

## Stav (state)

* Návrhový vzor Stav (state) se podobá návrhovému vzoru Konečný automat (finite-state machine)
  * konečný automat se používá např. pro tvorbu AI u NPC
  * objekt má konečný počet definovaných stavů a vždy se může nacházet pouze v jednom z nich
  * zároveň má určeno, kdy a na základě jakých vstupů má přepínat mezi jednotlivými stavy
* Na rozdíl od konečného automatu jsou stavy více decentralizované = znovupoužitelnost ale horší optimalizace

## Šablonová metoda (template method)

* Definuje kostru algoritmu, jeho jednotlivé kroky; potomci poté tyto kroky implementují a představují zaměnitelné algoritmy
* Potomci mohou předefinovat určité kroky algoritmu bez zásahu do jeho kostry
* Rodičovská třída deklaruje placeholdery algoritmu a potomci je implementují
* Použití:
  * když chceme, aby se naše aplikace dala rozšířit, ale ne modifikovat
  * když se nám v kódu objevují podobné algoritmy (lišicí se jen v pár krocích, kostra je stejná)

## Fasáda (facade)

* Zjednodušuje komunikaci mezi uživatelem a systémem
* Vytvoření jednotného rozhraní pro celou logickou skupinu tříd, které se tak sdruží do subsystému
* Zabalí komplikovaný subsystém do jednoduššího uceleného rozhraní

## Adaptér (adapter / wrapper)

* Převede zastaralé / nehodící se / chybné rozhraní třídy na rozhraní, které klient očekává
* Zabezpečuje spolupráci tříd a usnadňuje implementaci nových
* Může celou třídu zabalit do nové (object adaper), nebo z ní dědit (class adapter)

## Composite

* Doporučené řešení situace, kdy se pracuje se stromovou strukturou např. rekurzivně zanořené navigační menu
* Jednoduché a z nich složené (kompozitní) objekty – lze k nim přistupovat jednotným způsobem, implementují stejné rozhraní

![Composite](img/SW_09_01.png)
