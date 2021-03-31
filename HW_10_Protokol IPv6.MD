# HW 10 – Protokol IPv6

* Specifikace, srovnání s IPv4, dual-stack, tunel, NAT64.
* Prefix a délka prefixu, komprimace nul, názvosloví v IPv6
* druhy vysílání (unicast, multicast, anycast),
* druhy adres IPv6 včetně příkladů adres (GUA, LLA, ULA, multicast)
* stanovení InterfaceID, ZoneID, použití adresy pro ping a web stránky
* ND (NDP) – RS, RA, NS, NA, DAD, ICMPv6 – náhrada ARP

## IPv6 – Internet Protocol Version 6

* Internet Protocol je zodpovědný za směrování (routování) paketů ze zdroje do cíle
* IP adresa jednoznačně identifikuje síťové rozhraní na třetí vrstvě OSI/ISO
* IPv6 adresy se skládají z osmi skupin po čtyřech hexa číslech (0-F) oddělených dvojtečkou = __osm hextetů__
* `0123:BB99:3210:FE00:58A0:4565:98AE:1245`
* Vznikla kvůli nedostatku IPv4 adres

IPv4 | IPv6
--- | ---
4 oktety | 8 hextetů
oktet = 8 bitů | hextet = 16 bitů
desítková soustava | šestnáctková soustava
0b11111111 = 255 | 0b1111111111111111 = 65535 = 0xFFFF
4 * 8 = 32 bitů | 8 * 16 = 128 bitů
2\*\*32 = 4,29 \* 10\*\*9 | 2\*\*128 = 340 \* 10\*\*36
4 miliardy adres | 340 sextiliónů adres (dlouhá šklála)
4 billiony adres | 340 undecillionů adres (krátká škála)

## Koexistence IPv4 a IPv6 – metody přechodu

### Dual stack (dvojí zásobník)

* Zařízení má hybridní zásobník pro IPv4 a IPv6
* Zařízení musí podporovat oba dva protokoly a mít IPv4 i IPv6 adresu
* Kooperace mezi dvěma protokoly (pokud je třeba) se obvykle odehrává až v aplikační vrstvě

### Tunneling (tunelování)

* Balení jednoho protokolu do druhého
* Tunelování IPv6 datagramů pro průchod IPv4 sítí
* Tunel má dva konce, každý má IPv4 adresu
* IPv6 datagram je zabalen do IPv4 datagramu, kde adresa odesílatele je zdejší konec tunelu a adresa příjemce druhý konec tunelu
* Datagram je odeslán běžnou IPv4 sítí, na druhém konci se rozbalí a je odeslán dále po IPv6 síti

![Tunelling](./img/HW_10_01.PNG)

### Translation (překlad)

* Nutné pro komunikaci IPv4-only zařízení se zařízením IPv6-only (dual stack ani tunel nelze použít)
* Obecná sada pravidel, jak překládat kterou položku v hlavičce, normalizováno
* IPv6 adresy s vloženým IPv4 (IPv4-embedded)
  * Část prostoru za prefixem u adresy IPv6 je vyhrazena pro reprezentaci IPv4 adresy
  * Převod IPv4 -> IPv6 snadný
  * Převod IPv6 -> IPv4 složitější, využívá se dynamického mapování (podobné jako NAT u IPv4 privatních sítí)
* Ujal se přechodový mechanismus __NAT64__

### Dual-Stack Lite (DS Lite)

* Příprava na situaci, kdy ISP budou mít páteřní síť IPv6-only
* Tunelovací mechanismus, tentokrát se ale posílá IPv4 datagram IPv6 sítí

## Prefix a délka prefixu

* Zařízení umístěná v jedné (pod)síti mají ve svých IP adresách shodné nejvýznamější bity (bity vlevo)
* Velikost části, která vyjadřuje číslo sítě je definována pomocí CIDR notace počtem bitů zleva = __prefix__
* V IPv4 lze zapsat jako délu prefixu `192.168.1.1/24` nebo pomocí masky `255.255.255.0`
* V IPv6 se zapisuje pouze délka prefixu
  * Doporučená velikost pro podsítě je `/64`, aby fungoval Neighbor Discovery Protocol (?)
* S délkou prefixu `/64` je tedy 64 bitů z leva __Prefix__ (adresa podsítě) a zbylých 64 bitů (128-64) je __Interface ID__ (adresa konkrétního zařízení v podsíti)

## Komprimace nul

* Úvodní nuly ve skupině se dají vynechat (až na jednu)
* Skupiny nulových hextetů lze zkrátit na `::`, ale pouze jen jednou, zpravidla na delší skupinu nul
* `0123:0000:0000:0000:00ab:0000:0000:0000` lze zapsat jako:
  * `123::ab:0:0:0`
  * `123:0:0:0:ab::`

## Druhy vysílání a adres

<table><tbody>
<tr><td><strong>Unicast</strong><td><td>Individuální</td><td>Identifikuje právě jedno zařízení.</td></tr>
<tr><td><strong>Multicast</strong><td><td>Skupinové</td><td>Adresování skupin zařízení, data přijdou všem členům skupiny.</td></tr>
<tr><td><strong>Anycast</strong><td><td>Výběrové</td><td>Adresování skupiny, data přijdou jen nejbližšímu členovi skupiny.</td></tr>
</tbody></table>

* Oproti IPv4 broadcast (všesměrové vysílání) není potřeba, používají se obecnější typy multicast adres

## Unicast

prefix | význam
--: | :--
`::/128` | nedefinovaná adresa
`::1/128` | loopback (pingem lze zjistit funkčnost IP služeb)
`64:FF9B::/96` | IPv4-embedded adress – adresy s vloženým IPv4
`2000::/3` | GUA – global unicast address – individuální globální
`FC00::/7` | ULA – unique local address – unikátní individuální lokální
`FE80::/10` | LLA – link-local address – individuální lokální linkové

### __GUA__ – global unicast address

* Podobné jako veřejné IPv4 adresy, globálně unikátní, směrovatelné
* Zatím byla definována a přiděluje se jen část z nich – prefix 0b001
* ISP dostává prefix, jehož části (delší prefix se stejným začátkem) rozděluje zákazníkům

![GUA](./img/HW_10_02.PNG)

* __Global Routing Prefix__ – Globální směrovací prefix – Síťová část adresy přidělená poskytovatelem, obvykle `/48`
* __Interface ID__ – Identifikátor rozhraní – Rozlišuje zařízení v rámci podsítě (podobné jako hostitelská část IPv4), doporučeno `/64`
* __Subnet ID__ – Identifikátor podsítě – Prostor mezi nimi; čím větší, tím větší možné množství podsítí
* `2000::/3` – `2000`-`3FFF`, např.: `2001:db8:3c4d:15::baba:deda`

### __ULA__ – unique local address

* Nástupce _site local_ adres
* Adresy směrovatelné v množině spolupracujících sítí, např. společnost s více pobočkami

![ULA](./img/HW_10_03.PNG)

* _Příznak L_ je zatím vždy `1` a proto zatím všechny ULA adresy začínají prefixem `FD00::/8` (celkem je vyhrazeno `FC00::/7`)
* 40bitový Global ID je náhodně vygenerované číslo, zbytek klasika
* např.: `fd12:3456:789a:1::1`

### __LLA__ – link-local address

* Komunikace na lince (v podsíti)
* Povinná pro každé IPv6 zařízení, nesměrovatelná, nastavuje ji OS
* prefix `FE80::/10` __+__ 54 nulových bitů __+__ 64bitový identifikátor rozhraní
* např.: `fe80::714b:9770:43d4:f8b2`

## Multicast

* Použití např. real-time distribuce obrazu a zvuku
* Adresy `FF00::/8`, např.: `ff35:30:2001:718:1c01:0:0:7`
  * 8 jedniček – `FF`
  * 4 bity – příznaky
  * 4 bity – dosah, jak daleko členové od sebe mohou být; např. `0b0010` (`2`) = linka
  * 112 bitů – identifikátor skupiny
* Well-known:
  * `FF02::1` – všichni hosté na lince ~"broadcast"
  * `FF02::2` – všechny routery na lince (musí mít zapnuté `ipv6 unicast-routing`)
  * aj.
* Solicited-Node Multicast Address:
  * Používá ji Neighbor Discovery Protocol, aby zjistil, zdali je určitá adresa unikátní na lince
  * Spojení prefixu `ff02::1:ff00:0/104` s posledními 24 bity testované uni/anycast adresy
  * Např. `ff02::1:ff00:0/104` + `fe80::2aa:ff:fe`__`28:9c5a`__ = `ff02::1:ff28:9c5a`

## Mrdka stanovení InterfaceID, ZoneID, použití adresy pro ping a web stránky

## mrdka 🤐 ND (NDP) – RS, RA, NS, NA, DAD, ICMPv6 – náhrada ARP

## Dynamické adresování

* Dynamicky se adresuje GUA a ULA (LLA generuje OS)
* Adresa = Prefix + Interface ID (síťová část + hostitelská část)
* Interface ID přiděluje OS:
  * Podle MAC adresy pomocí algoritmu EUI-64
    * Doporostřed MAC adresy vloží `FFFE` a sedmý bit zleva nastaví na jedničku (pokud není)
  * Nebo generováno OS, tzv. Privacy Extensions
* Zbývá vyřešit přidělení prefixu:
  * Stavové – DHCPv6 – zařízení odešle na obecnou adresu dotaz ohledně svých parametrů a server mu odpoví
  * Bezstavové – SLAAC – směrovače vedí vše potřebné a občas tyto informace rozešlou všem, nebo si o ně zařízení zažádá (RS – Router solicitation – Výzva směrovači)

### __RA__ – Router advertisement – Ohlášení směrovače

* Směrovače v náhodných intervalech zasílají do všech připojených sítí informace
* Odesláno pomocí ICMPv6

### __SLAAC__ – StateLess Address AutoConfiguration – Bezstavová konfigurace

* Přidělování adres, použití RA a RS
* Není potřeba DHCPv6 server
* Dříve RA zprávy neobsahovaly IPv6 adresy rekurzivních DNS serverů

### __Stateless DHCPv6__

* Nadstavba SLAAC
* RA obsahuje příznaky, které informují zařízení, zdali má požádat DHCPv6 server o dodatečné informace (které ve SLAAC chybí)

### __Stateful DHCPv6__

* DHCPv6 server přiděluje i adresu
* SLAAC ale nelze úplně vypnout, přiděluje totiž výchozí bránu
