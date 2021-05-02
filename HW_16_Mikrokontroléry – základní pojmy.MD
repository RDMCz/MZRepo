# HW 16 – Mikrokontroléry (mcu) – základní pojmy

* Vysvětlení pojmu mikrokontrolér, harvardská a von Neumannova architektura, hlavní vlastnosti mikrokontrolérů Atmel AVR, popis blokového schématu.
* Dokumentace strana __1__, __3__, 10, 67, 171, 325

## Mikrokontrolér

* Elektronický integrovaný obvod
* Má integorvaný řadič, ALU a paměť
  * Řadič je v nákresech označen jako _INSTRUCTION DECODER_, jednou z jeho hlavních úloh je dekódování instrukcí
* Se svým okolím komunikuje pomocí univerzálních obousměrných vodičů sdružených do portů
* Obsahuje integrované periferie z důvodu většího programátorského pohodlí
  * Čítač / časovač
  * A/D převodník
  * Komunikační periferie
* Použití – Elektronická zařízení s digitálním řízením

## Von Neumannova architektura

![neumann](./img/HW_16_01.PNG)

* Architektura výpočetního systému, který je programován obsahem v paměti
* Nezávislá na typu řešené úlohy
* Paměť rozdělena na buňky stejné velikosti přístupné pomocí adres
  * RAM – přístup ke všem buňkám trvá stejnou dobu
* Instrukce se provádí v pořadí, v jakém jsou uloženy v paměti
  * Pořadí lze měnit pomocí instrukcí – (ne)podmíněné větvení
* __+__ Levnější výroba, rozdělení paměti pro data a kód si určuje programátor
* __-__ Možnost nechtěného přepsaní programu, jedna datová sběrnice – Neumannův bottleneck

## Harvardská architektura

![neumann](./img/HW_16_02.PNG)

* Rozdělení paměti na samostatnou _datovou_ a _programovou (instrukční)_
* Tyto dvě paměti mohou být vyrobeny odlišnými technologiemi
  * ATmega64 – SRAM pro data a nevolatilní Flash pro program
* Pokud je každá paměť připojena samostatnou sběrnicí, lze využít zřetězení
  * ATmega64 – 8bitová sběrnice pro data, 16bitová pro program
  * Single Level Pipelining – Zatímco je jedna instrukce zpracována, druhá je předběžně načtena z paměti programu

## Hlavní vlastnosti ATmega64

* Dokumentace strana 1
* Harvardská RISC architektura
  * Reduced Instruction Set Computer – jednoduchá a vysoce optimalizovaná sada instrukcí
* Většina instrukcí zabírá jeden hodinový cyklus
* 8bit
  * Osmibitová datová sběrnice
  * Osmibitová šířka registrů
  * Osmibitový implicitní datový typ pro ALU
* 32 osmibitových registrů
* Hardwarová násobička
* 64 KB Flash – velikost paměti programu
* 4 KB SRAM – velikost datové paměti (cache)
* 2 KB EEPROM – velikost datové paměti (firmware) – nevolatilní, lze elektricky vymazat
* Čítače, časovače
* _Byte-oriented Two-wire Serial Interface_ = I2C
* 2x USART
* SPI
* 53 vstupně-výstupních pinů

// TODO (?)
