# HW 27 – Paměti

## Paměť

* Fyzická zařízení umožňující ukládat data a následně s nimi pracovat

### Nevolatilní

* Data jsou zachována i po ztrátě napájení
* Flash, ROM, HDD, ...

### Volatilní

* Po ztrátě napájení jsou data ztracena
* Rychlejší ale dočasné
* RAM

## ROM – Read-Only Memory

* Nevolatilní
* Obsah určen při výrobě, poté již nelze měnit

### PROM – Programmable ROM

* Data lze zapsat až po výrobě, ale pouze jednou
* Kapacita v řádech KB

### EPROM – Erasable PROM

* Obsah lze vymazat pomocí UV záření

### EEPROM – Electrically EPROM

* Obsah lze vymazat pomocí vysokého napětí, nebo napětí na _Erase pinu_
* Paměť flash je založena na technologii EEPROM, je navržena pro vysoké rychlosti a hustotu, má však nižší životnost

## RAM – Random Access Memory

* Přístup ke všem buňkám trvá stejnou dobu
* Volatilní, rychlá
* Prakticky neomezený počet přepisů

### SRAM – Static RAM

* Základní princip je obvod D latch
* Realizace pomocí 6 tranzistorů (4 tranzistory a 2 odpory, které se většinou také realizují pomocí tranzistorů), které zachovávají data, dokud je k dispozici napájení
* ~~Rychlejší~~, dražší
* CPU cache, HDD buffer, router buffer

### DRAM – Dynamic RAM

* Každá paměťová buňka obsahuje 1 tranzistor a 1 kapacitor, pro uchování dat se vyžaduje periodický _memory refresh_
  * Přečtení dat a následný zápis na stejné místo, aby se data uchovala
* Čtení je destruktivní, přečtenou informaci je nutno bezprostředně zapsat zpět
* ~~Pomalejší~~, levnější, větší spotřeba v klidovém stavu
* Mýtus rychlosti – rychlost paměti závisí převážně na její velikosti (DRAM se vyrábějí ve výrazně větších kapacitách než paměti SRAM)

### SDRAM – Synchronous DRAM

* Všechny operace provádí synchronně s CPU clock
  * Snížení čekací doby CPU = zvýšení výkonu
* SDR SDRAM – Reaguje na náběžnou hranu
* DDR SDRAM:

### DDR – Double Data Rate

* Reaguje na náběžnou i sestupnou hranu
* DDR2, DDR3, DDR4 – Nejsou zpětně kompatibilní
* DDR5 standard byl zveřejněn v roce 2020

### Základní parametry

* Kapacita \[GB\]
* Formát – DIMM, SO-DIMM, (SIMM, SIPP)
* Typ – SDRAM DDR2/3/4/5
* Pracovní frekvence \[MHz\] – Počet instrukcí za vteřinu, také může být uvedeno v MT/s (Mega Transfers per second)

### GDDR – Graphics DDR

* DDR SDRAM přizpůsobená pro práci s GPU

### HBM – High Bandwidth Memory

* 3D paměť – DRAM čipy se skládají na sebe
* Díky tomu data putují kratší vzdálenost a je umožněna větší hustota, nižší spotřeba a širší sběrnice
* Drahé na výrobu, využito v některých kartách od AMD

## Cache

* Cache (mezipaměť) je relativně malá, ale rychlá paměť
* K datům uloženým do cache budou následující přístupy rychlejší
* Oproti bufferu (vyrovnávací paměti) může cache data poskytovat opakovaně

### CPU cache

* Mezipaměť, díky které nemusí CPU pokaždé sahat do operační paměti
* SRAM – rychlejší
* L1
  * Rozděleno na L1 Data Cache a L1 Instruction Cache
  * Nejrychlejší
  * Velikost: stovky KB, maximálně okolo 1 MB
* L2 – Několik MB
* L3 – Desítky MB
* Při zkopírování dat do cache se vytvoří _cache entry_ obsahující zkopírovaná data a umístění těchto dat zvané tag
* CPU před žádáním hlavní paměti zkontroluje cache, pokud je záznam nalezen (tag se shoduje s žádanou adresou) jedná o _cache hit_, při absenci dat v cache se jedná o _cache miss_
