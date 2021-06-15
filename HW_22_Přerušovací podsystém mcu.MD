# HW 22 – Přerušovací podsystém mcu

## Přerušení

* Událost, na kterou chceme reagovat

* Pomocí přerušovacího systému reagujeme na události

* Události hardwarové a softwarové:

* HW (častější):

  * Změna hodnoty na I/O pinu – Externí přerušení

  * Přetečení čítače/časovače

  * Překročení hodnoty u komparátoru

  * Dokončení převodu u AD převodníku

  * Příjem nebo odeslání znaku u sériové komunikace

* SW:

  * Neplatná adresa

  * Neplatný operační znak

* Reakce na událost:

  * Přeruší se běžící program

  * Předá se řízení na nějakou speciální adresu

  * Na této adrese je přímo umístěný obslužný podprogram, nebo skok/adresa na skutečné umístění podprogramu (častější)

* U ATmega64 jsou přerušovací vektory (adresy vedoucí do paměti programu), kam se předává řízení

  * Jsou na začátku PM odstupňované po dvou (0x0000, 0x0002, ...), aby se zde vešel nepodmíněný skok na skutečné místo podprogramu

* Tři skupiny přerušovacích systémů:

  1. Každá událost má vlastní interrupt vector (ATmega64)

  2. Některé události mají vlastní IV, některé ho sdílí – režim kombinovaný/smíšený (Intel 8051)

  3. Pouze jeden interrupt vector – vždy se skáče na jednu adresu, kde se musí softwarově vyhodnotit, co událost vyvolalo; pomalejší, ale lze definovat prioritu (Microchip PIC)

* Každý interrupt (každá událost, na kterou lze reagovat přerušením) se musí povolit – _Interrupt Mask Register_

  * Každá událost má vlastní povolovací bit, po resetu jsou zakázané

  * Také musí být povolen _Global Interrupt Enable_ v registru status (bit č. 7, první zleva, písmeno I)

  * Tento bit se používá, pokud nechceme, aby obsluha přerušení byla přerušena jinou obsluhou přerušení

* Každý zdroj přerušení má také svůj interrupt flag (příznak) – _Interrupt Flag Register_

  * Nastavuje se na jedničku, pokud vzniklo dané přerušení

  * Softwarově lze vynulovat kdykoliv

  * Některé systémy umí hardwarově nulovat automaticky, jakmile se spustí obsluha

  * Pokud by se flag nevynuloval, volala by se obsluha přerušení stále dokola

* Problém při více aktivních událostech řeší priorita

  * HW – Některé systémy obsahují registry, ve kterých lze každému interruptu nastavit prioritu, pořád ale lze nastavit u některých stejnou prioritu

  * U ATmega64 pořadí umístění vectorů v PM zároveň určuje jejich prioritu (nižší adresa = vyšší priorita)

  * U systémů s jedním interrupt vectorem se priorita definuje softwarově

  * U některých systémů může obsluha s vyšší prioritou přerušit obsluhu s nižší prioritou

* Kontext

  * Obsluha přerušení může pracovat s nějakými registry, po jejím skončení by hlavní program mohl tyto registry také používat a nalézt v nich neočekávaná/nekorektní data

  * Korektní obsluha přerušení by měla zajistit, aby po jejím skončení obsah příznakových a pracovních registrů byl stejný, jako když byla obsluha vyvolána

  * Na začátku se uloží obsah registrů, jejichž obsah se bude modifikovat (např. na zásobník) a před návratem z přerušení se původní obsah (zvaný kontext) obnoví

* Zpracování

  * Během každého instrukčního cyklu se vyhodnocuje, zdali nevzniklo nějaké přerušení

  * Pokud vzniklo a je povolené, tak se obsah následující instrukce uloží na zásobník a do PC (Program Counter) se nahraje příslušný interrupt vector

  * Tím se způsobí skok na adresu obsluhy přerušení a zakáže se _Global Interrupt Enable_

  * Provede se obsluha přerušení

  * Součástí instrukce návrat z přerušení je povolení _Global Interrupt Enable_, ze zásobníku se vytáhne adresa, kam se máme vrátit a nahraje se do PC

  * Provede se minimálně jedna následující instrukce, během které se opět zkontrolují příznaky přerušení

* Instrukce zabírající více než jeden instrukční cyklus se nemohou přerušit v půlce, aktuální instrukce se vždy dokončí
