# SW 14 – Normalizace databáze

## OLAP (Online Analytical Processing)

* Technologie uložení dat v databázi
* Umožňuje uspořádat velké množství dat tak, aby byla srozumitelná uživatelům zabývajícím se analýzou obchodních trendů a výsledků
* (business intelligence – souhrn prodejů, marketing, management, rozpočet, předpověď, účetní závěrka)
* ⇒ Analytické účely nad rozsáhlými databázemi
* Jednorázově nahraná data, nad kterými jsou prováděny složité dotazy
* Na rozdíl od relačních databází (tabulka, sloupec, řádek) pracuje s [datovou kostkou](https://office.lasakovi.com/excel/kontingencni-tabulka/OLAP-kostka-Excel-teorie/) (může být vícerozměrná)
* Jde především o flexibilní a rychlé získání souhrnných dat

## OLTP (Online Transaction Processing)

* Technologie uložení dat v databázi, používána ve většině databázových aplikací
* "protiklad OLAP"
* Data jsou průběžně často modifikována a přidávána mnoha uživateli zároveň
* ⇒ Umožňuje co nejsnadnější a nejbezpečnější modifikaci dat v mnohauživatelském prostředí

## Normalizace + optimalizace

* Přeorganizování dat v relační databázi tak, aby využívala výhody relačního modelu dat
* Normalizovaná databáze má efektivnější ukládnání, prohledávání, třídění, zpracování. Zabraňuje redundanci dat.
* Při normalizaci se mění sloupce jednotlivých tabulek a zavádí se mezi nimi výhodné vztahy
* V čím vyšší je databáze normální formě (stupeň doporučení pro ideální návrh databáze), tím je kvalitněji navržena – vzrůstá efektivita ale i zátěž na databázový stroj
* Kompromisem je dosáhnout co nejvyšší normy a pak úroveň snižovat na zvládnutelnou úroveň
* Obvykle je zbytečné uvažovat nad vyšší než třetí normou

## Normální formy

### __UNF__ – Nenormalizovaná forma

### __0NF__ – Nultá normální forma

* Lze říci, že tabulka (relace) se nachází v nulté formě, pokud obsahuje alespoň jeden neatomický atribut
* Tzn. Jeden sloupec v tabulce obsahuje více než jednu hodnotu (neatomický = lze rozdělit)
* Odstraněním neatomických hodnot se zabývá 1NF

ID (PK) | Name | Phone
--- | --- | ---
1 | Adam | 777111111, 778222222
2 | Eva | 779333333

### __1NF__ – První normální forma

* Všechna data jsou atomická
* Pro neatomické atributy se vytvoří nová tabulka s FK a vzniká vztah 1:N

ID (PK) | Name
:-: | :-:
1 | Adam
2 | Eva

ID (PK) | PersonID (FK) | Phone
:-: | :-: | :-:
101 | 1 | 777111111
102 | 1 | 778222222
103 | 2 | 779333333

### __2NF__ – Druhá normální forma

* Splňuje 1NF
* Všechny neklíčové atributy jsou funkčně závislé na celém PK
* Může být (ne)splněna u tabulek se složeným PK
* Klade důraz především na odstranění duplicit
* Částečně závislé atributy se dají do nové tabulky a vytvoří se jim PK (může být umělý), který se v původní tabulce použije jako PFK

StudentID (PK) | SubjectID (PK) | SubjectAcronym | FinalGrade
:-: | :-: | :-: | :-:
1 | 101 | CJL | F
1 | 102 | MAT | D
2 | 101 | CJL | A

* Zkratka předmětu není funkčně závislá na celém PK, ale jen na jeho části = Nesplňuje 2NF
* Při změně zkratky předmětu by se musel změnit záznam u všech oznámkovaných z tohoto předmětu
* Nelze přidat nový předmět, u kterého ještě nikdo nemá uzavřenou známku

StudentID (PK) | SubjectID (PFK) | FinalGrade
:-: | :-: | :-:
1 | 101 | F
1 | 102 | D
2 | 101 | A

SubjectID (PK) | SubjectAcronym
:-: | :-:
101 | CJL
102 | MAT

### __3NF__ – Třetí normální forma

* Splňuje 2NF
* Žádná tranzitivní závislost – všechny neklíčové atributy jsou závislé __pouze__ na PK
* Pokud X → Y && Y → Z, tak X → Z

MovieID (PK) | GenreID | GenreName | RunningTime
:-: | :-: | :-: | :-:
1 | 101 | Dokument | 1h20m
2 | 102 | Akce | 1h5m
3 | 102 | Akce | 2h
4 | 103 | Komedie | 1h35m

* Splňuje 2NF, ale ne 3NF
* MovieID → GenreID && GenreID → GenreName => MovieID → GenreName
* GenreName není určen pouze PK

MovieID (PK) | GenreID (FK) | RunningTime
:-: | :-: | :-:
1 | 101 | 1h20m
2 | 102 | 1h5m
3 | 102 | 2h
4 | 103 | 1h35m

GenreID (PK) | GenreName
:-: | :-:
101 | Dokument
102 | Akce
103 | Komedie

### Další normalizace

#### __EKNF__ – Elementary key normal form

#### __BCNF__ – Boyce-Coddova normální forma

* Splňuje 3NF a řeší anomálii, kdy některý z atributů, který je součástí složeného PK, je funkčně závislý na některém neklíčovém atributu
* Silnější varianta 3NF

#### __4NF__ – Čtvrtá normální forma

#### __ETNF__ – Essential tuple normal form

#### __5NF__ – Pátá normální forma

#### __DKNF__ – Domain-key normal form

#### __6NF__ – Šestá normální forma
