# HW 01 – Vrstva síťového přístupu, Ethernet

## Referenční model ISO/OSI

<table>
    <thead>
        <tr>
            <th colspan=2>Vrstva</th>
            <th>Protokolová datová jednotka</th>
            <th>Funkce</th>
            <th>TCP/IP</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>7</strong></td>
            <td><strong>Aplikační</strong></td>
            <td rowspan=3>Zpráva</td>
            <td>Vrstva nejblíže k uživateli. Obsahuje jádro aplikací, které má smysl standardizovat (např. přenosové mechanismy elektronické pošty), zbylé části aplikace (UI) byly posunuty nad aplikační vrstvu. Poskytuje uživatelským programům ucelené služby.</td>
            <td rowspan=3><strong>Aplikační</strong></td>
        </tr>
        <tr>
            <td><strong>6</strong></td>
            <td><strong>Prezentační</strong></td>
            <td>Transformuje data do tvaru, který používají aplikace (šifrování, konvertování, komprimace). Zabývá se strukturou dat, nikoliv jejich významem.</td>
        </tr>
        <tr>
            <td><strong>5</strong></td>
            <td><strong>Relační</strong></td>
            <td>Udržuje relaci (session) – uchovává informace mezi jednotlivými spojeními na úrovni transportní vrstvy.</td>
        </tr>
        <tr>
            <td><strong>4</strong></td>
            <td><strong>Transportní</strong></td>
            <td>TCP segment / UDP datagram</td>
            <td>Přenos dat mezi koncovými uzly (end-to-end). Účelem je poskytnout takový přenos, který si vyžadují vyšší vrstvy. Řeší odeslání dat ze zdroje do cíle. (TCP/UDP)</td>
            <td><strong>Transportní</strong></td>
        </tr>
        <tr>
            <td><strong>3</strong></td>
            <td><strong>Síťová</strong></td>
            <td>Paket</td>
            <td>Propojuje nesousední systémy – komunikace dvou uzlů, které nejsou přímo spojeny (prostřednictvím jiných uzlů). Logická adresace – IP protokol – IP adresa. Směrování – určení cesty paketu; všechny směrovače pracují na této vrstvě.</td>
            <td><strong>Síťová</strong></td>
        </tr>
        <tr>
            <td><strong>2</strong></td>
            <td><strong>Linková</strong></td>
            <td>Rámec</td>
            <td>Přenáší data mezi dvěma přímo spojenými uzly. Uspořádání dat z fyzické vrstvy do rámců. Pracuje s rámci, hlásí chyby. Adresace MAC a LLC. Na této vrstvě fungují přepínače; propojení pouze místních zařízení. Ethernet, Wi-Fi, ZigBee.</td>
            <td rowspan=2><strong>Vrstva síťového rozhraní</strong></td>
        </tr>
        <tr>
            <td><strong>1</strong></td>
            <td><strong>Fyzická</strong></td>
            <td>Bit, symbol</td>
            <td>Přenáší data mezi zařízeními pomocí fyzického přenosového média. Převádí bity na elektrické/rádio/optické signály. Řeší fyzické poslání dat, neřeší jejich význam. Definuje např. hodnoty napětí, maximální přenosová vzdálenost, rozložení pinů u fyzických konektorů.</td>
        </tr>
    </tbody>
</table>

## Ethernet

* Protokol definující přenos dat na lokální síti
* Obsah rámce:
  * Preambule – Vzorek střídajících se bitů 0 a 1, aby zařízení snadno poznalo začátek přicházejícího rámce [7B]
  * SFD – Start Frame Delimiter – Značí konec preambule a začátek rámce [1B]
  * Cílová MAC adresa [6B]
  * Zdrojová MAC adresa [6B]
  * Délka paketu nebo indikátor protokolu [2B]
  * Vlastní obsah
  * Kontrolní součet CRC

### Lokální síť

* Dříve definováno vzdáleností mezi stroji, resp. časem přenosu mezi nimi
* Možné definice:
  * Síť pod jednou administrativní správou
  * Síť, která končí bránou

### IEEE 802.3

* Standard organizace Institute of Electrical and Electronics Engineers
* Určuje specifikace fyzické (HW) a linkové (MAC) vrstvy

<table>
    <tr><td>802.3i</td><td>Ethernet</td><td align="right">10 Mbit/s</td><td>10BASE-T</td></tr>
    <tr><td>802.3u</td><td>Fast Ethernet</td><td align="right">100 Mbit/s</td><td>100BASE-TX</td></tr>
    <tr><td>802.3ab</td><td>Gigabit Ethernet</td><td align="right">1000 Mbit/s</td><td>1000BASE-T</td></tr>
    <tr><td><td>10 Gigabit Ethernet</td><td align="right">10 000 Mbit/s</td><td></td></tr>
    <tr><td></td><td>100 Gigabit Ethernet</td><td align="right">100 000 Mbit/s</td><td></td></tr>
    <tr><td></td><td>Terabit Ethernet (200GbE a 400GbE)</td><td align="right">> 100 000 Mbit/s</td><td></td></tr>
</table>

* Baseband – Přenáší pouze jeden signál, data jdou v základním pásmu (v Ethernetu je vše baseband)
* Broadband – Přenáší několik signálů najednou (DSL modemy)
* 1000BASE-__T__ – Twisted – Kroucená dvojlinka
* 1000BASE-<b>L</b>X – Long – Single-mode fiber – Menší průměr vlákna, jeden paprsek, delší vzdálenost, dražší
* 1000BASE-<b>S</b>X – Short – Multi-mode fiber – Větší průměr vlákna, více paprsků, kratší vzdálenost, levnější

### MAC vrstva – Media Access Control

* Řízení přístupu k médiu
* Kontrola správnosti přenášených rámců
* Adresace – MAC adresy vázané na síťovou kartu (vrstva je hardwarově závislá)
* MAC adresa:
  * Šest dvouciferných hexadecimálních čísel (oddělené dvojtečkou, pomlčkou, nebo neoddělené)
  * 48 bitů, kontrola pomocí komparátoru
    * Sedmý bit – 0 = unikátní (OUI enforced), 1 = lokálně spravovaná
    * Osmý bit – 0 = unicast, 1 = multicast
    * První polovina – Organizationally Unique Identifier (OUI), výrobcům přiděluje IEEE
    * Druhá polovina – Přiděluje výrobce (náhodně)

### IEEE 802.2 – LLC vrstva – Logical Link Control

* LLC není obsahem standardu IEEE 802.3
* IEEE 802.2 definuje LLC jakožto horní podvrstvu linkové vrstvy, propojení mezi Ethernetem a síťovou vrstvou
* Zakrývá rozdíly mezi sítěmi 802, poskytuje společný formát a rozhraní pro síťovou vrstvu
* Error-control, flow-control (aby rychlý odesílatel nezahltil pomalého adresáta)

### Unicast

* Přímá komunikace mezi dvěma uzly v síti
* Cílová adresa – MAC adresa cílové síťové karty

### Broadcast

* Pro všechna zařízení v síti
* Cílová adresa – samé jedničky (FF:FF:FF:FF:FF:FF)

### Multicast

* Pro vybranou skupinu, musí být předem definována
* Výhoda – Zmenšení provozu na síti a hlavně na serveru
* Nevýhoda – Definovat skupinu může být problém

### Anycast

* Data přijdou nejbližšímu členovi skupiny (resp. nejvýhodnějšímu – počet skoků a latence)

## ARP – Address Resolution Protocol

* Objevování MAC adres na základě IP adres
* Situace, kdy je třeba odeslat IP datagram na adresu ležící ve stejné podsíti a odesílatel zná pouze IP adresu cíle
* Průběh:
  * ARP request – broadcast – obsahuje tázanou IP adresu + IP a MAC adresu zdroje
    * Všichni příjemci si tato data zapíší do ARP cache
  * ARP reply – tázané zařízení odesílá zpět svou IP a MAC adresu

## PPP – Point-to-Point Protocol

* Komunikační protokol linkové vrstvy – přímá komunikace mezi dvěma uzly
* Např. sériová linka RS-232

## Média

1. Měď
2. Optika
3. Bezdrát

* __Modulace__ – nosný signál měněn modulujícím signálem:
  * Kódování Manchester – Data XOR Hodiny
  * QAM – Kvadraturní amplitudová modulace – Kombinace amplitudové a fázové modulace
  * QPSK
* __Šířka pásma__: Maximální teoretické množství dat, které může protéct za jednotku času
* __Propustnost__: Opravdové množství dat, které proteče za jednotku času
* __Přenosová rychlost__: Závislá na propustnosti, ovlivněna vnějšími jevy

### Koaxiál

* Měděný vnitřní vodič pro přenos
* Vnější vodič – stínění před elektromagnetickým polem, oddělen od vnitřního nevodivou vrstvou
* Užití v počátcích Ethernetu, dnes se moc nepoužívá, existuje však rodina technologií Ethernet over Coax

### Kroucená dvojlinka

* Čtyři páry vodičů, které jsou v páru pravidelně zakroucené
* Kroucení má vliv na šířku pásma a na odolnost proti rušení
  * Magnetická pole kroucených vodičů jsou opačná a vyrušují se; vyrušují i vnější pole
* U/UTP – Unshielded Twisted Pair
  * Značení `<stínění kabelu>/<stínění páru>TP`, U – nestíněno, F – Fólie, S – Opletení (pouze kabel)
  * Např.: SF/FTP – Kabel stíněn fólií a opletením + páry stíněny fólií
* Různé kategorie Cat1 - Cat8, nejběžnější Cat6
* Koncovka RJ-45 (8P8C)

### Optika

* Skleněné nebo plastové vlákno přenašející signál pomocí světla
* Princip totálního odrazu
* Menší ztráty, větší vzdálenosti, imunní vůči elektromagnetickému rušení
* SMF – Single-mode fiber – Menší průměr vlákna, jeden paprsek, delší vzdálenost, dražší
* MMF – Multi-mode fiber – Větší průměr vlákna, více paprsků, kratší vzdálenost, levnější
* Vlnová délka cca 1 mikrometr, infračervený paprsek
* Konektory LC, SC, ST

### Bezdrát

* Signály na frekvencích 2,4 a 5 GHz – bezlicenční pásma
* Antény
