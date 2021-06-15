# SW 13 – Konceptuální návrh databáze

## Relace

* V relační databázi se tabulkám říká _relace_
* Vztahy mezi tabulkami se také nazývají _relace_

## Entita

* Jednoznačně odlišitelný objekt reálného světa zachycený v datovém modelu
* Objekt schopen nezávislé existence (fyzické / konceptuální)
* Instance entitního typu
* "Řádek (záznam) v tabulce (relaci)"

## Entitní typ

* Množina entit stejného typu
* Charakterizováno názvem typu a popsáno pomocí atributů
* "Tabulka"

## Atribut

* Definuje entitní typ
* "Sloupec v tabulce"

## Klíč

* Klíčový atribut, obecně identifikuje entitu
* Každý záznam (řádek) v tabulce musí být jednoznačně identifikován. Měl by být unikátní díky souhrnu svých atributů. Souhrn všech hodnot atributů = __Superklíč__
* Superklíč není vhodný pro jednoznačné adresování (uživatelem nebo navázanou tabulkou). Proto je potřeba vybrat jeden atribut, který jednoznačně identifikuje celý záznam (řádek) = __Primární klíč__
* Všechny atributy, které mohou být použity jako PK = __Kandidátní klíče__
* K propojení tabulek se používá __Cizí klíč__ – Sloupec, který se shoduje (váže) na PK v jiné tabulce, musí obsahovat hodnotu PK druhé tabulky nebo null.
* Složený primární klíč – Více atributů
* PFK – Primární cizí klíč – Součást složeného PK "převzatá" z jiné tabulky

## Silná a slabá entita

__Silná entita:__

* Není závislá na jakékoliv jiné entitě ve schématu, vždy má svůj PK

__Slabá entita:__

* Existenčně závislá na silné entitě
* Diskriminátor (parciální klíč) od sebe odlišuje slabé entity
* PK slabé entity __=__ PK silné entity (na které je slabá závislá) __+__ parciální klíč

## Kardinalita a parcialita

__Kardinalita:__

* Vyjadřuje, kolik entit se na relaci (vztahu) podílí nebo může podílet
* __1:1__ – Řádku v jedné tabulce odpovídá právě jeden řádek v druhé tabulce a naopak. Moc se nepoužívá, protože lze zapsat jako jedna tabulka. Využitím je zpřehlednění rozsáhlých tabulek.
  * Např. řidič a automobil – v jednu chvíli řidič řídí právě jeden automobil a ten je zároveň řízen právě tím jedním řidičem.
* __1:N__ – K jednomu řádku z jedné tabulky patří více řádků z druhé tabulky. Nejpoužívanější typ relace.
  * Např. autobus a pasažéři – v jednu chvíli pasažér jede právě jedním autobusem a v jednom autobuse může zároveň být více pasažérů.
* __N:M__ – K řádku z jedné tabulky lze přiřadit více řádků z druhé tabulky s tím, že přiřazený řádek v druhé tabulce lze přiřadit k více řádkům v první tabulce ("nevyčerpá svou možnost přiřazení"). Často bývá relizován pomocí dvou vztahů 1:N a 1:M ukazujících do pomocné tabulky, ve které jsou kombinace obou použitých klíčů (tzv. vazební tabulka).
  * Např. herec a filmy – Herec hrál ve více filmech a ve filmu hraje více herců.
  * Používá se také při potřebě zachovat historii vztahů – řidič v minulosti řídil několik automobilů a za volantem jednoho automobilu se vystřídalo více řidičů.

__Parcialita:__

* Povinnost účasti v relaci
* __0__ – nemandatorní (nepovinná) relace
* __1__ – mandatorní (povinná) relace
* Např. řidič a automobil – řidič musel řídit alespoň jeden automobil (je to řidič), automobil ještě nemusel být nikým řízen.

## Agregace

* Vztah celek-část
* Část může existovat bez celku
* Tiskárna může existovat bez počítače
* Volná vazba se graficky značí prázdným kosočtvercem na straně celku

## Kompozice

* Vztah celek-část, jen mezi silnou a slabou entitou
* Část nemůže existovat bez celku
* Kniha a její výpujčky – při odstranění knihy zaniknou výpůjčky
* Součást patří minimálně i maximálně jednomu celku
* Značení plným kosočtvercem na straně celku
