# HW 04 – Referenční model OSI/ISO

* Protokol, rozhraní, popis a funkce jednotlivých vrstev, PDU, zapouzdřování, porovnání s modelem TCP/IP, průchod dat přes síťové prvky, kategorie přepínačů pro jednotlivé vrstvy, nástroje pro zachycování dat v síti, testování a oprava problémů v síti

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
* Definuje např. hodnoty napětí, maximální přenosová vzdálenost, charakteristiky signálu (modulace/šířka psáma), rozložení pinů u fyzických konektorů a jejich tvar, ...
* Na této vrstvě pracuje opakovač a rozbočovač

## 2. Linková vrstva

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
  * Šest dvouciferných hexa čísel (oddělené dvojtečkou, pomlčkou, nebo neoddělené)
  * 48 bitů, kontrola pomocí komparátoru
* Horvní podvrstva __LLC__
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
* Nejnižší vrstva, kterou se nazbývají síťové prvky, ale pouze koncová zařízení
* Přijímá data z relační vrstvy a rozkládá je na pakety pro síťovou vrstvu
* Stará se o bezchybný přenos zprávy (kontrola chyb, sestavení zprávy po přenosu)
* TCP – Transmission Control Protocol
  * Three-way handshake
  * Spolehlivost – zaručuje úplné správné odeslání
  * Potvrzuje přijatá data, znovu odesílá ztracená data
  * Pomalejší
  * WWW, e-mail, SSH
* UDP – User Datagram Protocol
  * Rychlejší, menší hlavička
  * Nezaručuje se úplné správné odeslání
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

## PDU – Protocol Data Unit

* Datová jednotka protokolů užívaná v konkrétní vrstvě, hlavička+data (PCI+SDU)
* Nižší vrstva bere jednotku (PDU) vyšší vrstvy jako svá data (SDU) a přidává k nim vlastní hlavičku (PCI) – zapouzdření

## TCP/IP – Transmission Control Protocol / Internet Protocol

* Vznikl původně jako komunikační protokol ministerstva obrany USA
