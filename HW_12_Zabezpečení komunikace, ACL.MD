# HW 12 – Zabezpečení komunikace, ACL

## Kryptografie

* Zabývá se šifrováním dat

### Symetrická

* K šifrování i dešifrování se používá stejný tajný klíč
* Obě strany musí mít ke klíči přístup a použít ho
* Oproti asymetrickým šifrám o dost menší výpočetní náročnost

### Asymetrická

* Oproti symetrické není potřeba výměny klíčů
* Veřejný šifrovací klíč
  * Majitel ho uveřejní a kdokoliv jím může šifrovat jemu určené zprávy
* Soukromý dešifrovací klíč
  * Majitel jej drží v tajnosti a může jemu určené zprávy dešifrovat
* Klíče jsou matematicky svázány, z šifrovacího klíče nesmí být možno vypočítat ten dešifrovací
* Využívá se jednocestných funkcí – ze vstupu se snadno vypočítá výstup, opačný směr je velmi obtížný
* Používá se také pro elektronický podpis – možnost prokázat u dat jejich autora

## Hashování

* Funkce, která z libovolně dlouhého vstupu vytvoří vždy stejně dlouhý výstup
* Malá změna u vstupních dat vyvolá velkou změnu na výstupu
* Z hashe (otisku) je velmi obtížné zrekonstruovat původní zprávu
* Není zaručena jedinečnost hashe (množina vstupů je větší než množina výstupů)
* Použití:
  * Rychlejší prohledávání tabulek v databázi
  * Kontrola správnosti dat
  * Skladování hesel v databázi

## Elektronický podpis

* Zašifrování pomocí soukromého klíče a dešifrování pomocí veřejného
* Pokud dokážeme zprávu dešifrovat, znamená to, že ji zašifroval vlastník soukromého klíče
* Aby se nemusela šifrovat celá zpráva (náročné), šifruje se pouze otisk (hash)
* Aby byl podpis skutečně důvěryhodný, musí být potvrzeno, že subjekt je majitelem páru klíčů, k tomu slouží certifikáty

## Digitální certifikát

* Vydáván certifikační autoritou
* Obsahuje údaje o subjektu, jeho veřejný klíč, podpis certifikační autority, dobu platnosti, ...

## Certifikační autorita

* Autorita vydávající digitální certifikáty
* Důvěryhodná třetí strana

## VPN – Virtual Private Network

* Propojení počítačů do soukromé sítě, i když jsou na různých místech v internetu
* Veškerá komunikace přes šifrovaný tunel
* Při komunikaci se serverem vidí poskytovatel i server pouze adresu VPN serveru
* Důvěra mezi uživatelem a poskytovatelem VPN

![vpn](./img/HW_12_01.PNG)

* VPN se také používá pro vzdálený přístup do místní sítě nějaké firmy

## SSL – Secure Sockets Layer

* Jeho nástupce je TLS – Transport Layer Security
* Nejčastěji se používá pro šifrovanou HTTPS komunikaci

## ACL – Access Control List

* Seznam pravidel které řídí přístup k nějakému objektu
* Zařízení sloužící pouze pro provoz ACL = firewall
* Cisco:

### Standardní ACL

* Filtrace paketů podle zdrojové IP adresy
* Adresu lze přidat na whitelist nebo blacklist
* Omezuje, co vstupuje do cíle, na kterém je ACL implementován
* Identifikace dle čísel 1–99
* Optimálně nasazujeme nejblíže k cíli

### Rozšířené ACL

* Kontroluje zdrojovou i cílovou adresu
* Umožňuje filtrovat i čísla portů
* Nevýhodou je větší náročnost na výkon
* Identifikace dle čísel 100–199
* Optimálně nasazujeme nejblíže ke zdroji

### Jmenné ACL

* Místo identifikačního čísla je použito jméno
* Proto je potřeba dodefinovat, zdali se jedná o standard nebo extended (to je normálně určeno číslem)

### Příkazy

``` txt
Switch(config)# access-list 5 deny host 10.5.1.10
Switch(config)# access-list 5 permit 10.5.1.10 0.0.0.255
Switch(config)# access-list 5 deny any
```

* Povoluje přístup subnetu 10.5.1.0/24 mimo adresy 10.5.1.10, všechny ostatní adresy jsou zakázány

``` txt
Switch(config-if)# ip access-group {číslo|jméno ACL} {in|out} 
```

* Aplikuje pravidla na vybraném interfacu
* `in` – filtrace příchozích, méně náročné na hardware
* `out` – filtrace odchozích
