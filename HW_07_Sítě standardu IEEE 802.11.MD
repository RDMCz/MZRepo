# HW 07 – Sítě standardu IEEE 802.11

## Bezdrát podle dosahu

* NFC – Near Field Communication
  * Vzdálenost pár centimetrů – bezpečné
  * Bezkontaktní placení, ...
* WPAN (Personal)
  * Malá vzdálenost, 10 metrů
  * IEEE 802.15:
    * Bluetooth
    * ZigBee – ovládání zásuvek, žárovek, ...
* WLAN
  * IEEE 802.11
* WWAN
  * Mobilní sítě – LTE, ...

## IEEE 802.11

* Standard pro bezdrátové sítě WLAN
* Využívá se bezlicenčních pásem – 2,4/5/(6) GHz – za jejich použití není nutno platit
* První verze 802.11 "legacy" byla pomalá a drahá

Standard | Alias | Pásmo | Max. rychlost | Modulace
--- | :-- | :-: | --: | :--
802.11a | Wi-Fi 2 | 5 GHz | 54 Mbit/s | OFDM
802.11b | Wi-Fi 1 | 2,4 GHz | 11 Mbit/s | DSSS
802.11g | Wi-Fi 3 | 2,4 GHz | 54 Mbit/s | OFDM
802.11n | Wi-Fi 4 | 2,4/5 GHz | 600 Mbit/s | MIMO OFDM
802.11ac | Wi-Fi 5 | ~2,4/5 GHz | 3,5 Gbit/s | MU-MIMO OFDM
802.11ax | Wi-Fi 6 | 2,4/5/6 GHz | 10,5 Gbit/s | MU-MIMO OFDMA

### 802.11a

* Narozdíl od Legacy pracuje na 5 GHz a nabízí o dost větší rychlost

### 802.11b

* Vyšlo ve stejný rok jako 802.11a a má horší vlastnosti – "krok zpět"
* Výrazně levnější – dostupné pro běžné uživatele (802.11a spíše pro firmy)

### 802.11g

* V podstatě stejné parametry jako 802.11a, ale na frekvenci 2,4 GHz

### 802.11n

* Max. rychlost 600 Mbit/s díky 4x4 MIMO
* Jedna anténa – max. 150 Mbit/s (600÷4)
* První technologie (z těch běžně dostupných), která začala používat i 5 GHz
* Umožňuje dvojnásobnou šířku pásma 40 MHz

### 802.11ac

* Definováno na 5 GHz, je ale zpětně kompatibilní se všemi předchozími standardy (funguje i na 2,4 GHz)
* 433 Mbit/s na jednu anténu, max. 8 antén
* Šířka pásma 80 MHz
* MU-MIMO – Multi User – Funkční pouze při downloadu na 5 GHz, max 4 spojení

### 802.11ax

* Funkční MU-MIMO pro download i upload, max 8 spojení pro 5 GHz a 4 spojení pro 2,4 GHz
* OFDMA – Efektivnější obsluha více uživatelů
* Wi-Fi 6E – Marketingový název pro zařízení operující na 6 GHz

## Wi-Fi Alliance

* Konsorcium, nezisková organizace
* Certifikace produktů – zaručuje kompatibilitu mezi certifikovanými produkty
* Postupem času krom certifikování začali vyvíjet i vlastní technologie:
  * Miracast
  * WPA, WPA2
  * Wi-Fi Direct
  * Wi-Fi 6E
  * ...

## AP – Access Point

* Zařízení pracující na druhé vrstvě
* Zařizují přechod mezi 802.11 WLAN a 802.3 Ethernet
* Součást domácích Wi-Fi routerů

## Fyzická vrstva

* modulační signál (vstupní signál) + nosný signál = modulovaný signál (vhodný pro přenos)

### AFH – Adaptive Frequency Hopping Spread Spectrum

* Hopping = rapidní měnění nosné frekvence (změny musí znát vysílač i přijímač)
  * Odolnost proti rušení a odposlechu
* AFH = Mechanismus pro zjištění "dobrých a špatných" kanálů (špatný kanál může být např. rušen nebo právě využíván)
  * Přeskakuje (hopping) pouze mezi "dobrými" nosnými frekvencemi, aby zmírnil rušení
  * Využíváno technologií __Bluetooth__

### DSSS – Direct-Sequence Spread Spectrum

* Umělé zavedení redundance – bity určené k přenosu jsou prokládané pseudonáhodnými bity
* Díky tomu je signál méně citlivý vůči rušení
* Pro zařízení bez znalosti mechanismu vytvoření pseudonáhodných sekvencí se signál jeví jako šum
* Využíván __802.11b__ (a novější zpětně kompatibilní standardy)

### OFDM – Orthogonal Frequency-Division Multiplexing

* Kódování signálu na více nosných frekvencích pomocí různých modulací, které jsou ortogonální
  * ~Jsou blízko sebe, dokonce se překrývají, ale jsou nezávislé/oddělitelné
* Využíván __802.11a/g/n/ac__

### OFDMA – Orthogonal Frequency-Division Multiple Access

* OFDM při obsluze více uživatelů používá point-to-point a rychle mezi nimi přepíná
* OFDMA využívá point-to-multipoint – více uživatelů v jednom okamžiku
* Využíván __802.11ax__, LTE, 5G

### QAM – Quadrature Amplitude Modulation

* Kombinuje amplitudovou a fázovou modulaci – dokáže přenášet více informací

### MIMO – Multiple-Input Multiple-Output

* Využívá více antén pro paralelní přenos signálů
* Zařízení příjemce musí také podporovat MIMO a paralelní signály si převede do signálu původního
* Značení např. _4x4_ znamená 4 spojení na 4 anténách

### MU-MIMO – Multi-User MIMO

* Dokáže v jeden okamžik komunikovat s více zařízeními najednou
* Např. 4 antény se rozdělí mezi 4 zařízení

## Ad hoc

* WLAN, kde jsou zařízení propojena přímo, nekomunikují tedy přes prostředníka (jako je access point)
* Opakem je _infrastrukturní síť_ – centralizované, zařízení připojena k AP
* Převážně se jedná o dočasná spojení
* Příkladem je Bluetooth

## Wi-Fi Direct

* Wi-Fi standard umožňující P2P bezdrátové spojení více zařízení bez použití AP, routeru, nebo připojení k internetu
* Sdílení souborů, ovládání tiskárny, ...

## Service Set

* BSS – Basic Service Set
  * Dělí se na – infrastrukturní síť / ad hoc / mesh
* ESS – Extended Service Set
  * Více AP se tváří jako jedno AP

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
