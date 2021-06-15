# SW 8 – Návrhové vzory I

## Návrhový vzor

* Popis/šablona pro řešení (častého) problému
* Svou aplikací zjednodušují daný problém
* Ověřená funkčnost = menší šance udělat chybu
* Kód je zpřehledněn a svým způsobem i standardizován

NV | — | —
:-: | :-: | :-:
__Vytvářející__ vzory | Mechanismy pro tvorbu objektů | Tovární metoda, Singleton, Bazén
__Strukturální__ vzory | Uspořádání objektů do efektivních struktur | Proxy, Adaptér, Fasáda, Muší váha, Composite
Vzory __chování__ | Interakce a responzibilita objektů | Command, Iterátor, Null, Služebník, State, Šablonová metoda

## Vytvářející vzory (Creational patterns)

### Tovární metoda (Factory Method)

* Časté využití u neměnných immutable objektů
* Implementace pomocí statické metody
* Nahrazuje konsktruktor, když potřebujeme např.:
  * Rozhodnout, zda se má instance opravdu vytvořit
  * Vracet instance různých typů
  * Provést nějakou akci před zavoláním konstrukce
  * Více implementací se stejnými parametry (tovární metody se mohou jmenovat různě)
* Metoda se používá ve třídě, ze které dědí objekty, které metoda vytváří

``` csharp
public static Osoba GetInstance(int age, string name)
{
    if (age < 0) return null;
    if (age <= 7) return new Predskolak(age, name);
    if (age <= 19) return new Skolak(age, name);
    if (age <= 65) return new Pracujici(age, name);
    return new Duchodce(age, name);
}
```

### Jedináček (Singleton)

* Může existovat pouze jedna instance dané třídy, která by měla být dostupná z více míst
* Existuje několik druhů implementace
* Instanci si lze vyžádat pomocí tovární metody (pokud instance neexistuje, je tovární metodou vytvořena)
* Samostatně se moc již nepoužívá, někteří jej považují za antipattern; je ale součástí jiných komplexnějších NV

``` csharp
class Jedinacek
{
    private Jedinacek() { }
    private static readonly Jedinacek instance = new Jedinacek();
    public static Jedinacek GetInstance() => instance;
}
```

### Fond / Bazén (Pool)

* Použití při potřebě omezit počet vytvořených instancí
* Místo vytváření nových instancí se znovupoužijí ty staré
* Dostupné instance jsou uloženy ve statické kolekci
* Metody pro získání volné instance a pro vrácení již nepotřebné instance
* Používá se, pokud potřebujeme větší množství instancí časově náročných na vytvoření, ale nepotřebjeme jich používat mnoho zároveň
* Omezená / Dynamická kapacita – při nedostatku instancí čekat, vyhodit výjimku / vytvořit novou
* Použití např. v bullet hell hrách

``` csharp
private const int ModulesCount = 5;
public static Module[] Modules = new Module[ModulesCount]
{
    new Module(Actions.BROUSENI),
    new Module(Actions.BROUSENI),
    new Module(Actions.REZANI),
    new Module(Actions.SVAROVANI),
    new Module(Actions.VRTANI)
};

public Module TakeModule(Actions a)
{
    if (Modules.Where(x => !x.InUse && x.Action == a).Count() > 0)
        return Modules.SingleOrDefault(x => !x.InUse && x.Action == a);
    else
        throw new Exception("Žádné dostupné moduly");
}
// InUse představuje dostupnost - jestli je modul používaný
```

## Vzory chování (Behavioral patterns)

### Příkaz (Command)

* Objekt je použit k zapouzdření všech informací potřebných ke zpožděnému spuštění události
* Zapouzdření příkazu do třídy a používání ho jako proměnné z důvodu
  * Přidání příkazu do fronty
  * Rekonstrukce historie příkazů – implementace undo/redo
* Použití ve WPF/UWP – `ICommand(Execute, CanExecute)`

### Iterátor (Iterator)

* Také známý jako Enumerator
* Samostatný objekt umožňující lineární procházení kolekcemi bez znalosti jejich vnitřní implementace
* V C# na kolekce implementující `IEnemuretor` lze použít `foreach` = __Implicitní iterátor__
* __Explicitní iterátor__ si musíme sami napsat, instance iterátoru na požádání vrací odkaz na další prvek v kolekci, dokud nedojede k prvku poslednímu
* __Externí iterátor__: průchod kolekcí řídí klient s využitím iterátoru; složitější, ale mocnější řešení
* __Interní iterátor__: průchod kolekcí řídí iterátor sám; klient specifikuje, co provádět s prvky kolekce (např pomocí LINQ + lambda)

### Prázdný (Null) objekt

* Použití, když se nehodí klasická hodnota `null`
* Null Object je plnohodnotný objekt, ale prázdný; zastupuje hodnotu `null`
* Odpadá testování hodnot, zdali jsou `null`

``` csharp
abstract class Animal : IAnimal
{
    public abstract void Sound();

    public static readonly IAnimal Null = new NullAnimal();
    private class NullAnimal : Animal
    {
        public override void Sound() { }
    }
}

class Dog : IAnimal
{
    public void Sound()
    {
        WriteLine("Woof");
    }
}

// Main:
IAnimal dog = new Dog();
IAnimal fox = Animal.Null;
```

### Služebník (Servant)

* Řeší, když je potřeba definovat společnou funkcionalitu pro více tříd současně
* Tyto třídy nemusí mít společného rodiče, kam bychom definici funkcionality umístili
* Implementují ale stejné rozhraní, které je vstupním parametrem v metodách služebníka

### Stav (State)

* Návrhový vzor stav (state) se podobá návrhovému vzoru konečný automat (finite-state machine)
  * Konečný automat se používá např. pro tvorbu AI u NPC
  * Objekt má konečný počet definovaných stavů a vždy se může nacházet pouze v jednom z nich
  * Zároveň má určeno, kdy a na základě jakých vstupů má přepínat mezi jednotlivými stavy
* Na rozdíl od konečného automatu jsou stavy více decentralizované = znovupoužitelnost ale horší optimalizace

### Šablonová metoda (Template method)

* Definuje kostru algoritmu, jeho jednotlivé kroky; potomci poté tyto kroky implementují a představují zaměnitelné algoritmy
* Potomci mohou předefinovat určité kroky algoritmu bez zásahu do jeho kostry
* Rodičovská třída deklaruje placeholdery algoritmu a potomci je implementují
* Použití:
  * Když chceme, aby se naše aplikace dala rozšířit, ale ne modifikovat
  * Když se nám v kódu objevují podobné algoritmy (lišicí se jen v pár krocích, kostra je stejná)
