# HW 04 – Referenční model OSI/ISO

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

* International Organization for Standardization / Open System Interconnection
* Snaha o vytvoření jednotného standardu pro bezchybnou komunikaci v PC sítích napříč prvky od různých výrobců
* Dekompozice implementace sítě do sedmi vrstev umožňující snadnější pochopení a větší modularitu
* Každá vrstva využívá služeb vrstvy pod sebou a poskytuje svoje služby vrstvě nad sebou
* Vzájemně spolu komunikují prvky ze stejných vrstev pomocí protokolů

## 1. Fyzická vrstva

* Přenáší jednotlivé bity mezi zařízeními pomocí fyzického přenosového média
* Převádí bity na elektrické/rádio/optické signály (měď/bezdrát/optika)
* Řeší fyzické poslání dat, neřeší jejich význam
* Oznamuje chybové stavy linkové vrstvě
* Definuje např. hodnoty napětí, maximální přenosová vzdálenost, charakteristiky signálu (modulace/šířka pásma), rozložení pinů u fyzických konektorů a jejich tvar, ...
* Na této vrstvě pracuje opakovač a rozbočovač

## 2. Linková (spojová) vrstva

* Využívá spojení z fyzické vrstvy pro přenos větších bloků dat – rámců
  * Preambule – Vzorek střídajících se bitů 0 a 1, aby zařízení snadno poznalo začátek přicházejícího rámce [7B]
  * SFD – Start Frame Delimiter – Značí konec preambule a začátek rámce [1B]
  * Cílová MAC adresa [6B]
  * Zdrojová MAC adresa [6B]
  * Délka paketu nebo indikátor protokolu [2B]
  * Vlastní obsah
  * Kontrolní součet CRC
* Na této vrstvě pracuje most a přepínač
* Ethernet, Wi-Fi, ZigBee, ...
* Dolní podvrstva __MAC__
  * Adresace – MAC adresy vázané na síťovou kartu (vrstva je hardwarově závislá)
  * Šest dvouciferných hexadecimálních čísel (oddělené dvojtečkou, pomlčkou, nebo neoddělené)
  * 48 bitů, kontrola pomocí komparátoru
    * Sedmý bit – 0 = unikátní (OUI enforced), 1 = lokálně spravovaná
    * Osmý bit – 0 = unicast, 1 = multicast, (FF:FF:FF:FF:FF:FF = broadcast)
    * První polovina – Organizationally Unique Identifier (OUI), výrobcům přiděluje IEEE
    * Druhá polovina – Přiděluje výrobce (náhodně)
* Horní podvrstva __LLC__
  * Propojení mezi Ethernetem a síťovou vrstvou
  * Zakrývá rozdíly mezi sítěmi 802, poskytuje společný formát a rozhraní pro síťovou vrstvu
  * Error-control, flow-control (aby rychlý odesílatel nezahltil pomalého adresáta)

## 3. Síťová vrstva

* Propojuje nesousední systémy – komunikace dvou uzlů, které nejsou přímo spojeny, prostřednictvím jiných uzlů
* Logická adresace – IP protokol – IP adresa
* Směrování – určení cesty paketu
* Na této vrstvě pracuje směrovač a L3 switch

## 4. Transportní vrstva

* Řeší odeslání dat ze zdroje do cíle takovým způsobem, jaký si vyžadují vyšší vrstvy
* Nejnižší vrstva, kterou se nezabývají síťové prvky, ale pouze koncová zařízení (pokud nebereme v potaz Layer 4 switching)
* Přijímá data z relační vrstvy a rozkládá je na pakety pro síťovou vrstvu
* Stará se o (bezchybný) přenos zprávy (kontrola chyb, sestavení zprávy po přenosu)
* TCP – Transmission Control Protocol
  * Three-way handshake
  * Spolehlivost – zaručuje úplné správné odeslání
  * Potvrzuje přijatá data, znovu odesílá ztracená data
  * Pomalejší
  * WWW, e-mail, FTP, SSH
* UDP – User Datagram Protocol
  * Rychlejší, menší hlavička
  * Nezaručuje se úplné správné odeslání – ztráta, poškození, duplikace, špatné pořadí
  * VoIP, video stream, online hry

## 5. Relační vrstva

* Udržuje relaci (session) – uchovává informace mezi jednotlivými spojeními na úrovni transportní vrstvy
* Práva, hesla, omezení

## 6. Prezentační vrstva

* Transformuje data do tvaru, který používají aplikace (šifrování, konvertování, komprimace)
* Zabývá se strukturou dat, nikoliv jejich významem
* Kódování textu (ASCII), grafických dat (JPEG), ...

## 7. Aplikační vrstva

* Vrstva nejblíže k uživateli. Poskytuje uživatelským programům ucelené služby.
* Obsahuje jádro aplikací, které má smysl standardizovat (např. přenosové mechanismy elektronické pošty)
* Zbylé části aplikace (UI) byly posunuty nad aplikační vrstvu.
* FTP, Telnet, SMTP, ...

<table>
    <tr><td>Well-known</td><td>0 ÷ 1023</td><td>Vyhrazené pro nejběžnější služby</td></tr>
    <td>Registered</td><td>1024 ÷ 49151 (0xBFFF)</td><td>Určitý protokol či aplikace, IANA</td></tr>
    <td>Dynamic (private)</td><td>49152 ÷ 65535 (2**16)</td><td>Porty pro dočasnou krátkou komunikaci</td></tr>
</table>

Číslo portu | Aplikace | ...
:-: | :-: | :--
20, 21 | FTP | File Transfer Protocol
22 | SSH | Secure Shell
23 | Telnet | Teletype Network
25 | SMTP | Simple Mail Transfer Protocol
53 | DNS | Domain Name System
67, 68 | DHCP | Dynamic Host Configuration Protocol
69 | TFTP | Trivial File Transfer Protocol
80 | HTTP | Hypertext Transfer Protocol
110 | POP3 | Post Office Protocol
111 | NFS | Network File System
123 | NTP | Network Time Protocol
161 | SNMP | Simple Network Management Protocol
143 | IMAP | Internet Message Access Protocol
443 | HTTPS | HTTP Secure
445 | SMB | Server Message Block

## PDU – Protocol Data Unit

* Datová jednotka protokolů užívaná v konkrétní vrstvě, hlavička+data (PCI+SDU)
* Nižší vrstva bere jednotku (PDU) vyšší vrstvy jako svá data (SDU) a přidává k nim vlastní hlavičku (PCI) – zapouzdření

## TCP/IP – Transmission Control Protocol / Internet Protocol

* Vznikl původně jako komunikační protokol ministerstva obrany USA
