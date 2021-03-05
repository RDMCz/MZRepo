# SW 8 – Návrhové vzory I

* Návrhové vzory pro vytváření instancí, rozšiřování funkcionality.

## Návrhový vzor

* Popis / šablona pro řešení (častého) problému
* Svou aplikací zjednodušují daný problém
* Ověřená funkčnost = menší šance udělat chybu
* Kód je zpřehledněn a svým způsobem i standardizován

### Druhy NV

* Rozděleny podle toho, jaké problémy řeší
* __Vytvářející vzory (Creational patterns)__ řeší mechanismy pro tvorbu objektů, snaží se objekt vytvořit nejvhodněji vzhledem k aktuální situaci.
* __Strukturální vzory (Structural patterns)__ řeší strukturu vztahů mezi entitami.
* __Vzory chování (Behavioral patterns)__ řeší společnou komunikaci mezi objekty.

## Vytvářející vzory (Creational patterns)

### Tovární metoda (Factory Method)

* Časté využití u neměnných immutable objektů
* Implementace pomocí statické metody
* Nahrazuje konsktruktor, když potřebujeme např.:
  * Rozhodnout, zda se má instance opravdu vytvořit
  * Vracet instance různých typů
  * Provést nějakou akci před zavoláním konstruktoru
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
        return Modules.Where(x => !x.InUse && x.Action == a).ToArray()[0];
    else
        throw new Exception("Žádné dostupné moduly");
}
// InUse představuje dostupnost - jestli je modul používaný
```

### Knihovna (Utility)

* Skupina metod, které spolu nějak souvisí a využívají se společně
* Z knihovny by nemělo jít dědit a vytvářet instace, měla by být přístupná odkudkoliv – `public static`

### Originál

* Třída, jejíž instance jsou svými parametry unikátní
* Lze identifikovat přes klíč / seed

## Strukturální vzory (Structural patterns)

### Muší váha (Flyweight)

* Objekt rozdělen na vnitřní a vnější část
* Spočívá ve sdílení prstředků, vnitřní část je pro všechny instance společná
* Ušetření paměťové náročnosti
* Např. jednotky v RTS hrách

### Neměnné (Immutable) objekty

* Používánní proměnných objektů snižuje bezpečnost programu
* V C# `readonly`

### Přepravka (Crate, Data Transfer Object)

* Kontejner na předávání několika informací – např. podprogram může vracet více hodnot
* Atributy mohou být konstantní – zajištená neměnnost
* Např. souřadnice x y z

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

## Vzory chování (Behavioral patterns)

### Služebník (Servant)

* Řeší, když je potřeba definovat společnou funkcionalitu pro více tříd současně
* Tyto třídy nemusí mít společného rodiče, kam bychom definici funkcionality umístili
* Implementují ale stejné rozhraní, které je vstupním parametrem služebníka
