# 🥺👉👈

* Sepsáno léta Páně 2021
* Použití na vlastní nebezpečí

`[ HW ] [##############################]`

`[ SW ] [#########################]`

## 🥵🥶

* SW 01:

kategorie | operátor
--- | ---
__primární__ | `(x)`, `x.y`, `f(x)`, `a[x]`
__unární__ | `+x`, `-x`, `!`, `(T)x`, `true`, `false`
__multiplikativní__ | `*`, `/`, `%`
__aditivní__ | `+`, `-`
__relační__ | `<`, `>`, `<=`, `>=`
__rovnost__ | `==`, `!=`
__AND__ | `&&`
__OR__ | `\|\|`
__ternární__ | `? :`
__přiřazení a lambda__ | `=`, `*=`, `/=`, `%=`, `+=`, `-=`, `=>`

* SW 02 – Algoritmus – __Elementárnost, Konečnost, Obecnost, Determinovanost, Výstup__

* SW 05/06 – OOP – __Dědičnost, Zapouzdření, Polymorfismus__

* SW 08/09:

NV | — | —
:-: | :-: | :-:
__Vytvářející__ vzory | Mechanismy pro tvorbu objektů | Tovární metoda, Singleton, Bazén
__Strukturální__ vzory | Uspořádání objektů do efektivních struktur | Proxy, Adaptér, Fasáda, Muší váha, Composite
Vzory __chování__ | Interakce a responzibilita objektů | Command, Iterátor, Null, Služebník, State, Šablonová metoda

* SW 08 – __Tovární mtd, Singleton, Bazén, Command, Iterator, Null, Servant, State, Template mtd__

* SW 09 – __Proxy – Remote/Virtual/Protection, Adapter, Fasáda, MušíVáha, Composite__

* SW 11
  * CLI – __Common Language Infrastrucure__ – specifikace, vyšší jazyky na různých platformách
  * CLR – __Common Language Runtime__ – Překlad CLI -> machine code, správa paměti, type/thread safety, garbage, výjimky
  * CIL – __Common Intermediate Language__
  * FCL – __Framework Class Library__ – hierarchie jmenných prostorů, práce se soubory/sítí/vlákny/..., ASP, LINQ

* SW 15:

``` sql
-- DML --
INSERT INTO animalsounds (animal, sound) VALUES ("Cat", "Meow"), ("Dog", "Woof"), ("Cow", "Moo");
INSERT INTO table2 SELECT * FROM table1 (WHERE condition);
UPDATE employees SET salary = 37000 WHERE name = "Hektor";

-- DDL --
CREATE TABLE employees (
    id          INTEGER         PRIMARY KEY,
    name        VARCHAR(50)     not null,    
);
ALTER TABLE employees ADD salary INTEGER;
TRUNCATE TABLE employees;
DROP TABLE employees;

-- DCL --
GRANT SELECT, INSERT, UPDATE, DELETE ON employees TO PUBLIC;
REVOKE ALL ON employees FROM username;

-- TCL --
BEGIN TRANSACTION; 
COMMIT; 
SAVEPOINT savename;
ROLLBACK TO savename;
```

## HW

1. Vrstva síťového přístupu, Ethernet
2. Aplikační vrstva TCP/IP
3. Síťový operační systém – Linux
4. Referenční model OSI/ISO
5. VLAN, návrh podnikové sítě
6. Přepínání sítí, Inter-VLAN
7. Sítě standardu IEEE 802.11
8. Protokol TCP, UDP
9. Adresace v internetu IPv4, cesta datagramu sítí
10. Protokol IPv6
11. Síťové prvky, přiřazení k vrstvám OSI/ISO
12. Zabezpečení komunikace, ACL
13. Směrování, směrovací tabulky, směrovací protokoly
14. Problematika bezpečnosti počítačových sítí
15. DHCP, NAT, DNS
16. Mikrokontroléry (mcu) – základní pojmy
17. Instrukční soubor mcu
18. Paralelní porty mcu
19. Připojování externích periferií k mcu
20. Čítačové podsystémy mcu
21. Internet věcí
22. Přerušovací podsystém mcu
23. Vyšší programovací jazyky pro mcu
24. Sériová rozhraní mcu
25. Procesory
26. Základní desky
27. Paměti
28. Zařízení pro ukládání dat
29. Grafické karty
30. Výstupní zařízení PC

## SW

1. Základní programové konstrukce
2. Algoritmus, algoritmická složitost
3. Strukturované datové typy
4. Spojové struktury
5. Objektové programování I
6. Objektové programování II
7. Podprogramy
8. Návrhové vzory I
9. Návrhové vzory II
10. Paralelní programování
11. Architektury .NET
12. Verzovací systémy
13. Konceptuální návrh databáze
14. Normalizace databáze
15. Jazyk SQL
16. Výběr dat v SQL
17. Prostředky pro návrh webových aplikací I.
18. Možnosti pozicování na webových stránkách
19. Frameworky architektury MVC
20. Ověřování identity v prostředí internetu
21. Návrh webové aplikace <span>ASP.NET</span>
22. AJAX, REST
23. React
24. Prostředky pro návrh webových aplikací II.
25. Testování software, ošetření chyb
