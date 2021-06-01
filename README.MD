# 🥺👉👈

`[ HW ] [##############################]`

`[ SW ] [#########################]`

[Barth](https://drive.google.com/drive/folders/1D_n9iXheGX6-S03_GvbHD6FxsxruTHXG?usp=sharing),
[Běhálek](http://www.cs.vsb.cz/behalek/vyuka/pcsharp/text/index.html),
[Bouška](http://samuraj-cz.com)

## HW

1. Vrstva síťového přístupu, Ethernet
    * Protokol IEEE 802.3, MAC vrstva, IEEE 802.2, LLC vrstva, unicast, broadcast, multicast, anycast
    * ARP protokol, popis rámce Ethernet, PPP a WLAN (stručně, jen vybrané položky rámce)
    * Média, modulace, šířka pásma, propustnost
    * Druhy médií – kabely, optická vlákna, bezdrátové sítě - základní principy činnosti
    * Značení kabelů (koaxiál, UTP/STP, konektory - zapojení),
    * konektory optických vláken (SMF/MMF)

2. Aplikační vrstva TCP/IP
    * Sítě P2P a klient-server (pro porovnání), aplikace P2P a klient-server (model)
    * Popis aplikací a komunikace:
        * WEB server, email,
        * FTP, SMB, NFS, telnet, TFTP,
        * SSH, NTP a další síťové aplikace

3. Síťový operační systém – Linux
    * Výběr operačního systému (vhodné distribuce Linuxu)
    * Instalace operačního systému, připojení uživatelů
    * Druhy souborových systémů používaných v současných verzích OS
    * Koncepce souborového systému, stromová struktura, druhy souborů
    * Práva a oprávnění, nastavení oprávnění pro soubory (rwx), databáze uživatelů a hesel
    * Změna vlastníka a oprávnění

4. Referenční model OSI/ISO
    * Protokol, rozhraní, popis a funkce jednotlivých vrstev, PDU, zapouzdřování, porovnání s modelem TCP/IP, průchod dat přes síťové prvky, kategorie přepínačů pro jednotlivé vrstvy, nástroje pro zachycování dat v síti, testování a oprava problémů v síti

5. VLAN, návrh podnikové sítě
    * Koncepce VLAN, výhody nasazení VLAN, access VLAN, trunk VLAN, IEEE802.1Q, native VLAN, management VLAN, voice VLAN.
    * Redundance v podnikové síti (záložní cesty) – STP a PVST+ a výběr root bridge, blokované porty – určení
    * Zvýšení propustnosti sítě pomocí EtherChannel - princip, nastavení, protokoly

6. Přepínání sítí, Inter-VLAN
    * Tři způsoby propojení VLAN, porovnání metod z hlediska efektivity.
    * Switch L3, směrování a přepínání sítí – porovnání
    * Nastavení směrovače pro propojení VLAN (legacy, Router-on-a-Stick)
    * Nastavení přepínače L3 pro Inter-VLAN, možnost směrování přepínače L3
    * Připojení VLAN do internetu

7. Sítě standardu IEEE 802.11
    * Přenosová trasa, přístup k médiu, 802.11a/b/g/n/ac/ax Wi-Fi, AP,
    * fyzická vrstva – SS – AFH, DS, OFDM, QAM, MIMO (multiple input, multiple output),
    * Ad-hoc, Wi-Fi Direct, infrastrukturní sítě,
    * BSS, ESS, ESSID, MAC control, WEP, WPA, WPA2, WPA3, EAP, 802.1X, Radius, AAA

8. Protokol TCP, UDP
    * Přepínání datagramů vs. přepínání obvodů, TCP komunikace, segmentace, multiplexování segmentů, formát datagramu, řízení toku, omezení režie, navázání a ukončení spojení (tří a čtyřcestný handshake), plovoucí okno.
    * Porovnání komunikace s použitím TCP a UDP, příklady

9. Adresace v internetu IPv4, cesta datagramu sítí
    * Značení portů na aktivních propojovacích prvcích (př. CISCO), fyzické adresy (MAC)
    * třídy adres IPv4, rezervované (speciální adresy), veřejné a privátní adresy,
    * získání adresy, protokol ARP, vytváření podsítí (podsítě konstantní velikosti, VLSM)
    * porty (dobře známé, registrované, volné), popis přenosu dat od odesílatele (klient) k adresátovi (server), přechod paketu přes standardní bránu, ARP - získání MAC,
    * rozložení cesty z pohledu modelu TCP/IP – zapouzdření dat

10. Protokol IPv6
    * Specifikace, srovnání s IPv4, dual-stack, tunel, NAT64.
    * Prefix a délka prefixu, komprimace nul, názvosloví v IPv6
    * druhy vysílání (unicast, multicast, anycast),
    * druhy adres IPv6 včetně příkladů adres (GUA, LLA, ULA, multicast)
    * stanovení InterfaceID, ZoneID, použití adresy pro ping a web stránky
    * ND (NDP) – RS, RA, NS, NA, DAD, ICMPv6 – náhrada ARP

11. Síťové prvky, přiřazení k vrstvám OSI/ISO
    * Popis standardního chování opakovače, mostu, přepínače, směrovače, firewallu …
    * Možnosti nastavení přepínače a směrovače pomocí managementu – další funkce směrovače,
    * Domácí router a Wi-Fi router – možnosti nastavení, porovnání s podnikovým routerem
    * Možnosti škálování sítí (drátové i bezdrátové) – rozšíření množství portů

12. Zabezpečení komunikace, ACL
    * Kryptografie symetrická a asymetrická, hashování, certifikáty a certifikační autorita, elektronický podpis, VPN, příklad implementace (SSL)
    * ACL standardní a rozšířený, jmenný ACL, zabezpečení přístupu k managování switche a routeru,
    * Vytvoření ACL a nasazení ACL na porty směrovače (filtrace provozu dovnitř a ven – porovnání)

13. Směrování, směrovací tabulky, směrovací protokoly
    * Směrovací tabulky – záznamy, statické směrování, dynamické směrovací protokoly (RIP, RIPv2, RIPng, EIGRP, OSPF, BGP),
    * směrovací protokoly postavené na principu vzdáleného vektoru (distance-vector) v porovnání s link-state.
    * Výhody a nevýhody statického směrování oproti dynamického směrování.
    * Příklad vytvoření směrovacích tabulek staticky a pomocí směrovacího protokolu (např. RIP)

14. Problematika bezpečnosti počítačových sítí
    * Fyzická bezpečnost, sociální inženýrství, adware, spyware, malware, exploit, virus, červ, DoS, DDoS, Botnet (zombie), Man in the Middle (MITM), ransomware
    * Zabezpečení přepínače (flooding, snooping, starvation, port security)
    * Zabezpečení bezdrátových sítí (kontrola přístupu, šifrování)

15. DHCP, NAT, DNS
    * DHCPv4 komunikace s DHCP serverem, obsah zprávy DHCP serveru
    * Nastavení rozsahu přidělovaných adres, DHCP Relay (DHCP server za standardní bránou)
    * SLAAC, DHCPv6, nastavení serveru a klienta, ověření nastavení.
    * Koncepce NAT, důvody a výhody použití NAT, port forwarding, NAT v IPv6 (NAT64)
    * Inside, outside, local a global adresy,
    * statická NAT, dynamická NAT, portovaná NAT (PAT) - overloading
    * Konfigurace statické i dynamické NAT, PAT (NAT overload), ověření nastavení
    * Doménové jméno, FQDN, systém DNS – kořenové servery
    * TLD, SLD, přiřazení DN, překlad, autoritativní odpověď

16. Mikrokontroléry (mcu) – základní pojmy
    * Vysvětlení pojmu mikrokontrolér, harvardská a von Neumannova architektura, hlavní vlastnosti mikrokontrolérů Atmel AVR, popis blokového schématu.

17. Instrukční soubor mcu
    * Druhy instrukcí, popis. Struktura instrukce v paměti, CISC, RISC, architektura load-store, doba provádění instrukce. Popis příkladu zdrojového kódu programu v asm.

18. Paralelní porty mcu
    * Popis paralelních portů mikrokontrolérů řady Atmel AVR. Obvodový popis portu, elektrické vlastnosti. Příklady instrukcí pro práci s porty.

19. Připojování externích periferií k mcu
    * Tlačítka, klávesnice, LED, segmentové a inteligentní displeje.

20. Čítačové podsystémy mcu
    * Režim čítače/časovače, podrobný popis pro Atmel AVR. Režimy CAPTURE, COMPARE, PWM. Dohlížecí časovač WDT.

21. Internet věcí
    * Vysvětlení pojmu, architektura, sítě typu LPWAN, komunikační protokoly.

22. Přerušovací podsystém mcu
    * Přerušení, obsluha, vektor, povolení, příznak, priorita, kontext, zpracování, přerušovací systém Atmel AVR.

23. Vyšší programovací jazyky pro mcu
    * Požadavky vpj na architekturu mcu, omezení a rozdíly vůči programování pro osobní počítače, optimalizace kompilátoru.

24. Sériová rozhraní mcu
    * Popis sériových sběrnic USART, RS422/485, SPI/Microwire, I2C, 1Wire, CAN. Popis sériového portu Atmel AVR.

25. Procesory
    * Struktura současných procesorů (x86/64). Techniky optimalizace provádění instrukcí, snižování spotřeby. Rozšířené instrukční sady.

26. Základní desky
    * Základní deska (čipová sada, bios), interní sběrnice (PCI, PCIe), externí sběrnice (usb, firewire).

27. Paměti
    * Typy pamětí, struktura, základní parametry, optimalizace přístupu do paměti (cache)

28. Zařízení pro ukládání dat
    * Pevné disky (HDD/SSD), optická média (CD, DVD, BlueRay), rozhraní PATA, SATA, SCSI, SAS, M.2.

29. Grafické karty
    * Struktura, základní parametry, akcelerace, vytváření 3D scény, použití pro negrafické výpočty.

30. Výstupní zařízení PC
    * Displeje - LCD, LED, OLED, technologie zobrazení, základní parametry. Tiskárny – technologie tisku, základní parametry.

## SW

1. Základní programové konstrukce
    * Základní programové konstrukce, proměnné, datové typy, reference a hodnota, programy a podprogramy, operátory, priorita operátorů.

2. Algoritmus, algoritmická složitost
    * Algoritmus, algoritmická složitost, rekurze, náhodnost.

3. Strukturované datové typy
    * Strukturované datové typy, objekt, pole, kolekce, generické kolekce.

4. Spojové struktury
    * Spojové struktury, seznamy, stromy, procházení, vkládání a odstraňování prvků, výhody a nevýhody.

5. Objektové programování I
    * Strukturované a objektové programování, objekt, třída, základní objektové vlastnosti, třídy abstraktní, zapouzdřené a rozhraní.

6. Objektové programování II
    * Zapouzdření, dědičnost, polymorfismus, přepsání a překrytí (virtual, override, new), přetížení.

7. Podprogramy
    * Podprogramy, funkce, metody, delegáty, lambda operátory, návratové hodnoty, oblast platnosti proměnné.

8. Návrhové vzory I
    * Návrhové vzory pro vytváření instancí, rozšiřování funkcionality.

9. Návrhové vzory II
    * Návrhové vzory pro skrývání implementace, optimalizaci rozhraní.

10. Paralelní programování
    * Asynchronní a paralelní programování. Thread, Task, zámek, chráněná sekce, použití paralelismu, Async/await.

11. Architektury .NET
    * Prostředky architektury .NET pro cílové platformy, MVVM, Binding, Observer, událostmi řízené programování.

12. Verzovací systémy
    * Verzovací systémy, Git, repozitář, commit, větev.

13. Konceptuální návrh databáze
    * Entita, relace, entitní typ, klíč, kandidátní klíč, primární klíč, silná a slabá entity, kardinalita a parcialita, agregace, kompozice

14. Normalizace databáze
    * OLAP, OLTP, Normální formy, normalizace, optimalizace, 0. NF, 1. NF, 2. NF, 3. NF

15. Jazyk SQL
    * Dialekt, standard, DML, DDL, DCL, TCL, INSERT, UPDATE

16. Výběr dat v SQL
    * SELECT, projekce, restrikce, podmínky, seskupování, agregace, spojování tabulek

17. Prostředky pro návrh webových aplikací I.
    * HTML, CSS, Javascript, značka, atribut, sémantický význam značek

18. Možnosti pozicování na webových stránkách
    * Blokové a inline prvky, absolutní a relativní pozicování, obtékání, grid, flex, tabulka

19. Frameworky architektury MVC
    * MVC, MVP, MVVM, Model, View, Controller, Presenter, Page, PageModel, request, response, http

20. Ověřování identity v prostředí internetu
    * Jméno, heslo, dvoufázové ověřování, biometrické ověřování, OAuth2, resource, owner, authorization server, OpenID, poskytovatelé ověření, access_token

21. Návrh webové aplikace <span>ASP.NET</span>
    * Razor Pages, MVC, Page, PageModel, Razor syntaxe, Startup.cs, služba, databáze, Entity Framework, Identity

22. AJAX, REST
    * Klasická a asynchronní komunikace, AJAX, promise, fetch API, API, metody http, GET, POST, DELETE, PUT, PATCH, OPTION, REST

23. React
    * Component, DOM, Virtual DOM, událost, props, state, hook, propagace stavu

24. Prostředky pro návrh webových aplikací II.
    * Písmo v WWW, CSS, selektor, příklady selektorů, vlastnosti CSS, media query, CSS Frameworky, komponenty v CSS, možnosti pozicování prvků v Bootstrap

25. Testování software, ošetření chyb
    * Sémantická chyba, syntaktická chyba, chyba, debugging, ladění aplikace, výjimka, testování, jednotkové testy
