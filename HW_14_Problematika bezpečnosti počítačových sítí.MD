# HW 14 – Problematika bezpečnosti počítačových sítí

## Fyzická bezpečnost

* K serverům a jiným prvkům IT infrastruktury se nesmí dostat nepovalaná osoba – zamezení odcizení/poškození
* Autorizace pro vstup do určitých částí budovy
* Uzamčení serveroven, uzamčení racků, kamerové systémy, alarm, ochranka, ...
* Brát ohled přírodní vlivy, např.
  * Neumisťovat server do spodních pater v zátopových oblastech
  * Pod střechu kde praží slunce
* Klimatizace, přepěťové ochrany, záložní zdroje, ...
* Stínění kabelů – vést kabel např. kovovou trubkou u stropu

## Sociální inženýrství

* Manipulace lidí za účelem provedení určité akce nebo získání určité informace
* Pretexting – Vytvoření smyšleného scénaře a přesvědčení oběti o jeho legitimnosti, aby následně provedla akci nebo vyzradila informace
* Phishing – Získávání citlivých údajů na internetu pomocí zasílání falešných zpráv, které se tváří jako pravé

## Adware

* Adware není nijak škodlivý (nijak nesleduje nebo nemanipuluje s daty uživatele)
* Může být ale velmi otravný, uživateli zobrazuje nechtěné reklamy a autor malwaru může mít z reklam příjem
* Banner, pop-up, ...

## Spyware

* Malware se záměrem shromažďování (citlivých) informací o osobě nebo společnosti
* Shromážděná data pak odesílá autorovi škodlivého kódu
* Keylogger, sledování souborů, obrazovky, kamery, ...
* Není snadné určit přesnou hranici, co je v pořádku a co už je spyware (cookies, cílená reklama, ...)

## Malware

* Zastřešující název pro úmyslně škodlivý software
* Virus, červ, trojan, ransomware, spyware, adware, ...

## Exploit

* Zneužití díry v zabezpečení softwaru ve vlastní prospěch
* Díra nejčastěji vzniká neúmyslně (bug, přehlédnutá chyba v kódu) nebo se jedná o zadní vrátka
* Většinou se využívá k získání administrátorských práv nebo k instalaci dalšího malwaru

## Počítačový virus

* Pojem virus bývá často zaměňován s malwarem
* Vkládá svůj kód do spustitelných souborů, dokumentů, ...
* Replikuje se, potřebuje hostitele
* Zabírá místo na disku, snižuje výkon
* Může být vytvořen za účelem pobavení, pachání škody (poškození dat), poukázání na bezpečností díru, šíření propagandy, ...
* Může mít i znaky ostatního malwaru, hlavní ale je, že se množí a modifikuje ostatní software (určitá podobnost s biologickým virem)

## Červ

* Rozesílá kopie sebe sama na jiné počítače, nejčastěji po síti
* Oproti viru nepotřebuje hostitelský software
* Zatěžuje počítačovou síť
* Může se v něm vyskytovat kód navíc (nesloužící přímo pro jeho replikaci) – payload (náklad)
  * Payload je využit pro konání sekundární činnosti – manipulace se soubory (spy/ransom/...) nebo vytvoření zadních vrátek

## DoS – Denial of Service

* Útok na internetové služby a stránky
* Přehlcení požadavky – pád, nedostupnost pro ostatní uživatele
* DDoS – Distributed DoS
  * Více strojů provádí DoS, často bez vědomí majitelů počítačů (botnet)

## Botnet

* Síť infikovaných počítačů na internetu řízená centrálně z jednoho místa (počítač útočníka)
* Infikované počítače se nazývají zombies
* Útočník pak může využít zombies pro rozesílání spamů nebo pro DDoS útok

## MITM – Man-In-The-Middle

* Útočník odposlouchává komunikaci mezi dvěma konci – přesměrování síťového provozu
* Může také komunikaci upravovat, oboustranně se vydávat za toho na druhém konci
* Útočník může získat citlivá data nebo se za někoho vydávat

## Ransomware

* Zablokování a zašifrování dat oběti a znemožnění přístupu k PC, dokud není zaplaceno výkupné
* Vyhrožování, že budou zveřejněna citlivá data
* Placení výkupného často v kryptoměnách kvůli složitějšímu dohledání pachatele
* Nejčastěji se do PC dostane formou trojského koně, může se ale jednat i o červa

## Zabezpečení síťových prvků

### MAC Flooding

* Zaplavení MAC adresami, snaha vyčerpat paměť přepínače (CAM tabulka)
* Odesílání velkého množství rámců s unikátními zdrojovými MAC adresami
* Snaha útočníka, aby se legitimní MAC adresy dostaly pryč z CAM tabulky a rámce pro ně byly rozeslány jako broadcast

### Port Security

* Obrana proti MAC Flooding
* Vypnout nepoužívané porty
* Určit, které MAC adresy jsou povolené na kterém portu

### DHCP Starvation

* Útočník opakovaně odesílá DHCP request za účelem vyčerpání adresního prostoru
* Ostatní uživatelé pak nedostanou adresu, útočník se může pokusit o DHCP Spoofing

### DHCP Spoofing

* Útočník odpovídá na DHCP requesty (namísto opravdového DHCP serveru)
* Nastaví sebe jako výchozí bránu nebo DNS server
* Díky tomu může zachytávat provoz na síti – man-in-the-middle

### DHCP Snooping

* Obrana proti DHCP Spoofing
* Na přepínači lze nastavit _trusted_ a _untrusted_ porty
* U nedůvěryhodných portů lze omezit počet DHCP requestů, nebo je úplně zakázat

## Zabezpečení bezdrátových sítí

### WEP – Wired Equivalent Privacy

* Šifrování komunikace
* 10/26/58 hexadecimálních čísel dlouhý klíč
* Symetrická šifra, na obou koncích nastaven statický klíč
* Snadno prolomitelné

### WPA – Wi-Fi Protected Access

* __WPA__
  * Reakce na nedostatky WEP
  * Šifra RC4
  * TKIP – Temporal Key Integrity Protocol – Pro každý paket je používán jiný klíč
* __WPA2__
  * Šifra AES – Advanced Encryption Standard
  * Prolomeno 2016 – KRACK
* __WPA3__
* __WPA-Personal__ – Také _WPA-PSK (pre-shared key)_
  * Domácí použití, nevyžaduje autentifikační server
* __WPA-Enteprise__
  * Využití autentifikačního serveru RADIUS a EAP metod

### IEEE 802.1X

* Standard popisující zabezpečení přístupu do sítě
* Také popisuje odesílání EAP zpráv po místní síti
* Suplikant, autentifikátor a autentifikační server
* Suplikant (klient) se nemůže dostat do chráněné části sítě, dokud není jeho identita ověřena. Suplikant předá požadované údaje autentifikátoru. Ten je přepošle autentifikačnímu serveru, který rozhodne, zdali suplikant může přistoupit k síti či nikoliv.

### EAP – Extensible Authentication Protocol

* Autentifikační framework
* Umožňuje výrobcům snadno vyvíjet a nasazovat nové autentifikační metody (EAP metody)

### AAA – Authentication, Authorization, Accounting

* Autentifikace – identita uživatele – představení identity + ověření (heslo, certifikát, ...)
* Autorizace – udělelní/zakázání specifického typu služeb na základě uživatelovi autentifikace
* Účtování – sledování využívání síťových služeb uživateli

### RADIUS

* RADIUS je AAA client/server protokol
* Obvykle se používá jako back-end pro 802.1X autentifikaci

![802.1X](https://upload.wikimedia.org/wikipedia/commons/1/1f/802.1X_wired_protocols.png)
