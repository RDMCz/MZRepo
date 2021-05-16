# SW 25 – Testování software, ošetření chyb

* Sémantická chyba, syntaktická chyba, chyba, debugging, ladění aplikace, výjimka, testování, jednotkové testy
* __Kompilovaný jazyk__ – Zdrojový kód nejprve přeložen pomocí překladače (kompilátoru) do strojového kódu a až poté je možné ho spustit (C#)
* __Interpretovaný jazyk__ – Program zvaný interpreter přímo spouští kód step-by-step bez nutnosti předběžného překladu (Python)

## Chyba

* Nedostatek v kódu
  * Buď porušuje pravidla zápisu programu
  * Nebo při svém běhu vyústí v nečekané/špatné chování programu

1. Hardwarové chyby – Chyby způsobené selháním hardwaru
2. Uživatelské chyby – Chyby způsobené nekorektními vstupy od uživatele
    * Některé může programátor snadno ošetřit, _např. když uživatel do kolonky hmotnost zadá textový řetězec namísto čísla_
    * Na jiné se reaguje složitěji, např. _když uživatel do kolonky hmotnost zadá hodnotu v librách namísto kilogramů_
3. Programátorské chyby – Chyby způsobené nesprávně napsaným kódem programu

## Programátorské chyby

// TODO
