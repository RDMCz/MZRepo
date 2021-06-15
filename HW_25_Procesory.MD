# HW 25 – Procesory

## Central Processing Unit

* Integrovaný obvod, provádí strojové instrukce
* Řadič, ALU, registry

## Architektura CPU

* Dělí se na architekturu instrukční sady a mikroarchitekturu

### Architektura instrukční sady

* Definuje např. počet registrů, syntax strojového kódu, seznam instrukcí, způsob ukládání čísel do paměti, ...
* Nemá příliš vliv na celkový výkon CPU
* x86, ARM (Acorn RISC Machine), RISC-V, Sunway, ...

### Mikroarchitektura

* Logická a fyzická implementace instrukční sady
* Haswell, Skylake, Zen, ...
  * Spadají pod x86 – liší se výkonem, ale jsou navzájem kompatibilní

### x86

* Architektura instrukční sady pro 16/32/64bitové CPU
  * Všechny moderní CPU v osobních počítačích používají rozšíření x86-64 (_AMD64_ a _Intel 64_)
* Vznikla již v sedmdesátých letech, od té doby byla vylepšena, ale zachovala si téměř plnou zpětnou kompatibilitu
* Ve vestavěných systémech se příliš nepoužívá (zde dominuje ARM), existuje ale např. Intel Atom
* __Variabilní délka instrukce__
  * Někde v prvním bytu musí být zmíněna délka instrukce
  * Primitivní instrukce zabírají méně místa (oproti architekturám s fixní délkou instrukce)
* __CISC – Complex Instruction Set Computer__
  * Navrženo, když paměť byla drahá
  * Jedna instrukce dokáže provádět komplexní operace – rozkládá se na posloupnost mikroinstrukcí
  * Variabilní délka instrukce (základní instrukce jsou krátké)
  * Velký počet instrukcí a adresačních režimů
* __Zpětná kompatibilita__
* __Bajtové adresování__
  * Byte je nejmenší adresovatelná jednotka (ve většině případů)
  * Každý bajt má svou adresu
  * Opakem je word addressing (velikost slova závisí na architektuře)
* __SIMD – Single Instruction Multiple Data__
  * Jedna instrukce pracuje paralelně s více daty
* __Harvardská architektura__
  * L1 je dělena na Data Cache a Instruction Cache

## Techniky optimalizace provádění instrukcí

### Fronta instrukcí

* Fronta, do které se vkládají operační kódy instrukcí z operační paměti
* Z druhé strany fronty si řadič odebírá instrukce
* (Během provádění složitějších instrukcí se do fronty mohou paralelně vkládat další operační kódy, jakmile se provádí jednodušší instrukce, nemusí procesor čekat na operační paměť)
* Fronta se musí vyprázdnit, pokud dojde ke změně běhu programu – přerušení, instrukce skoku, návrat z podprogramu, ...

### Pipelining – Zřetězené zpracování instrukcí

* Instrukce se většinou dělí na několik kroků (řezů) – fetch, decode, execute, ...
* Tyto kroky se většinou provádí v jiné části mikroprocesoru
* Pipelining znamená zpracování více instrukcí současně s tím, že každá se nachází v jiné části zpracování
* Např. při ukladání výsledku operace1 se na ALU může provádět operace2 a z paměti načítat kód operace3
* Všechny části procesoru jsou činné; nečeká se na kompletní dokončení operace1, než se začne provádět operace2

### VLIW – Very Long Instruction Word – Explicitní paralelní zpracování instrukcí

* Všechny výkonné jednotky jsou umístěny paralelně vedle sebe
  * Pokud nenastane kolize v použitých registrech, mohou pracovat nezávisle na sobě
  * Např. paralelně: dvě ALU, jedna násobička, jedna dělička, ...
* V jedné instrukci jsou uloženy operační kódy pro všechny jednotky (jinak by se žádný čas neušetřil)
  * Díky tomu není potřeba komplexního řadiče, instrukce mají ale velkou délku
* Překladač se stará o kolize v registrech a skládá instrukce tak, aby bylo instrukční slovo co nejvíce zaplněno
* Závislé na konfiguraci procesoru – změna výkonných jednotek znamená změnu zápisu slova a celý program musí být znovu přeložen
* Nefunguje s intepretovanými jazyky

### Superskalární architektura

* Procesor má více modulů pro zpracování instrukcí, nemusí být ale symetrické (např. má dvě ALU ale jen jednu násobičku)
* Instrukce jou načteny z paměti a řadič rozhoduje, zdali je možné je provést paralelně
* __+__ Zpětná kompatibilita; __-__ Složitější řadič

### Eliminace skoků

1. Inline funkce – Na místo volání funkce se napíše přímo její kód
2. Loop unrolling – Rozbalování smyček
3. Predikce skoků

## Techniky snižování spotřeby

1. Zmenšení výrobní technologie
    * Vzdálenost mezi tranzistory (např. 7 nm)
    * Kratší vzdálenost znamená kratší cesta pro elektrony a díky tomu nižší spotřeba
2. Snížení napájecího napětí
3. Intel Turbo Boost nebo AMD Turbo Core
    * "Dynamické přetaktování" – frekvence (a spotřeba) se zvýší, pouze pokud je výkon potřeba
    * Existují další technologie jako AMD PowerNow!, AMD Cool'n'Quiet, Intel SpeedStep, ...

## Rozšířené instrukční sady

* Skalár – Hodnota proměnné plně určena jediným číselným údajem
* Vektor – Obsahuje několik hodnot stejného typu

### x87

* Dnes se již považuje za standardní součást x86
* Přidává operace pro práci s čísly s plovoucí řádovou čárkou
* Registry ST(0) až ST(7) pro čísla s plovoucí řádovou čárkou
  * Uloženo ve formátu `platnéČíslice * (základ ** exponent)`, přesnost je double extended

### MMX

* První rozšiřující sada obsahující SIMD operace pro x86
* Zaměření na multimédia, neoficiální zkratka MultiMedia eXtensions
* 57 nových instrukcí, 4 nové datové typy
* 8 nových registrů MM0 až MM7
  * Ve skutečnosti se jedná o aliasy na x87 registry, tudíž bylo komplikované provádět zároveň MMX a FPU (floating-point unit) operace

### 3DNow<span>!</span>

* Odpověď na MMX od AMD
* V podstatě MMX pracující s plovoucí řádovou čárkou

### SSE – Streaming SIMD Extensions

* Přidává spoustu nových instrukcí a nové 128bitové registry
* AVX – Advanced Vector Extensions – vylepšení SSE, 256bitové registry

### x86-64

* 64bitový režim a režim kompatibility
