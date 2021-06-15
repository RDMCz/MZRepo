# HW 23 – Vyšší programovací jazyky pro mcu

## Programování pro MCU x PC

* ~Absence OS a osekané architektury u MCU

### Jazyk C pro MCU

* Podporována norma jazyka C, některé odlišnosti:
* __+__ Přímý přístup k HW
* __+__ Instrukce přímo manipulující s jednotlivými bity (Set, Clear, Test) (u PC nutno řešit softwarově)
* __-__ Omezené HW prostředky – redukovaná velikost paměti, hloubka implementace zásobníku a podpora ze strany ALU
* __-__ Absence služeb OS (přidělování procesoru, správa paměti)
  * Absence dynamické alokace paměti – kontrola rozsahu polí, adres, ...
  * Vlastní řešení multitaskingu a ukládání kontextu při přerušení
* Někdy je nutná softwarová implementace zásobníku
* Omezené nebo zakázané rekurzivní volání

#### Datové typy

* Většina podporována
* Velikost integeru závislá na platformě (16/32 bit) (nemá fixní velikost jazyka C)
* Float a double většinou nejsou podporovány hardwarově, nutnost softwarové emulace
  * Výkonnější ARMy (Cortex M4) mají hw podporu pro plovoucí řádovou čárku

## ASM x VPJ

* Assembler:
  * Složitější
  * Je možné dosáhnout vyšší úrovně optimalizace
  * Výrazně delší doba tvorby programu
  * Nepřenosnost
* C:
  * Rychlejší, čitelnější, ...
  * Přenosnost mezi platformami, pokud neodkazujeme na konkrétní HW dané architektury
    * Lze použít HAL – Hardware Abstraction Layer

## Požadavky VPJ na MCU

* Jaké vlastnosti by měl mít HW, aby kódová nadbytečnost byla co nejmenší (vybrat si několik)

1. Více pracovních registrů (akumulátorů)
    * Charakteristika architektur RISC
    * 32 osmibitových pracovních registrů (strana 1)
2. Krátký instrukční cyklus (Single Cycle Instruction)
    * Charakteristika architektur RISC (strana 395 poslední sloupec)
    * Pipelining
3. Rozšířená podpora ukazatelů
    * Registry X,Y,Z; lze adresovat celou paměť; post-increment/pre-decrement
4. Indexování polí
    * Instrukce obsahuje adresu začátku pole + posun vůči začátku (relativní displacement)
5. Paměťové ukazatele – minimálně 4
    * Zdroj, cíl, stack pointer, datový segment
    * Datový segment – je výhodné mít proměnné v paměti u sebe v souvislém úseku, kde jsou adresy proměnných relativní vůči umístění segmentu v paměti
6. Šíření příznaku nuly
    * Instrukce zahrnující výsledek předchozí operace
    * Strana 395 instrukce _with Carry_ / _Through Carry_
    * Např. _Compare with Carry_ u porovnání vícebajtových čísel – pokud předchozí část rovna nebyla, ani následující nebudou rovny
7. Bitové proměnné
    * Zjištění hodnoty na portech
    * Reprezentace true/false
    * Set, Clear, Test (Skip if Bit ...)
8. Instrukce včetně operandů uložena v paměti na jedné adrese
    * Charakteristika architektur RISC
    * Není nutno do paměti přistupovat opakovaně
9. Hardwarový stack pointer
10. Podpora aritmeticko-logických instrukcí s vyšší šířkou, než je ta nativní
    * ATmega64 _Word_ – Zdvojené registry

## Optimalizace kompilátoru

* Kompilátor volí, jak bude implementovat kód napsaný ve VPJ
* Cílem je minimální velikost nebo co největší rychlost programu (zpravidla tyto požadavky jdou proti sobě)

1. Optimalizace závislé na HW – Podpora ze strany architektury
2. Optimalizace nezávsilé na HW – Aplikovatelné vždy

* Měli bychom programy psát tak, abychom optimalizaci kompilátoru co nejvíce usnadnili

### Optimalizace závislé na HW

* Registrové proměnné – Klíčové slovo, kompilátor se pokusí proměnnou uložit do registrů
* Optimalizace jednoduchým přístupem – Pokud možno, kompilátor využívá bitové operace
* Změna typu/směru smyčky – Pro procesory bývá efektivnější číslovat sestupně a testovat na nulu

### Optimalizace nezávislé na HW

* Zpracování konstant (constant folding) – Výpočty obsahující konstanty předpočítány v době kompilace
* Vyloučení opakovaných výpočtů (výrazů) – Opakující se výpočty se vypočítají jen jednou a výsledek se ukládá do registru
  * Klíčovým slovem `volatile` říkáme kompilátoru, aby tuto optimalizaci neprováděl, protože se hodnota proměnné může změnit asynchronně
  * Výsledkem výpočtu je číslo a výsledkem výrazu je true/false
* Optimalizace skokových příkazů
  * Vícenásobné skoky (vnořené ify) možné nahradit přímým skokem
  * Volba absolutního/relativního skoku
* Vyloučení mrtvého kódu
* Náhrada opakujících se úseků programu skoky
  * Opakující se sekvence kódu nahrazeny za podprogram
  * Šetří paměť ale zpomaluje program
* Negace skoků – Znegování podmínky
* Překrývání dat – Sdílení statických proměnných v rámci několika funkcí, pokud to neovlivní správný běh programu
* Optimalizace plnění – Redundantní příkazy plnění (zavádění) se odstraňují
  * Např. deklarace proměnné, do které se posléze uloží výsledek výpočtu
* Optimalizace jednoduchých smyček
  * Rozbalení cyklů
  * Rychlejší, zabírá více místa
* Rotace smyček
  * Záměna pořadí provedení instrukcí, ty na sobě nesmí být závislé z hlediska výsledku
* Optimalizace řídícího toku – Optimalizace výrazů switch-case
