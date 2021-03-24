# HW 01 – Vrstva síťového přístupu, Ethernet

* Protokol IEEE 802.3, MAC vrstva, IEEE 802.2, LLC vrstva, unicast, broadcast, multicast, anycast
* ARP protokol, popis rámce Ethernet, PPP a WLAN (stručně, jen vybrané položky rámce)
* Média, modulace, šířka pásma, propustnost
* Druhy médií – kabely, optická vlákna, bezdrátové sítě - základní principy činnosti
* Značení kabelů (koaxiál, UTP/STP, konektory - zapojení),
* konektory optických vláken (SMF/MMF)

## Referenční model ISO/OSI

<table>
    <thead>
        <tr>
            <th colspan=2>Vrstva</th>
            <th>Protokolová datová jednotka</th>
            <th>Funkce</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>7</strong></td>
            <td><strong>Aplikační</strong></td>
            <td rowspan=3>Zpráva</td>
            <td>Vrstva nejblíže k uživateli. Obsahuje jádro aplikací, které ma smysl standardizovat (např. přenosové mechanismy elektronické pošty), zbylé části aplikace (UI) byly posunuty nad aplikační vrstvu. Poskytuje uživatelským programům ucelené služby.</td>
        </tr>
        <tr>
            <td><strong>6</strong></td>
            <td><strong>Prezentační</strong></td>
            <td>Transformuje data do tvaru, který používají aplikace (šifrování, konvertování, komprimace). Zabývá se strukturou dat, nikoliv jejich významem. Úkolem je, aby odeslaná data dorazila ve stejné podobě.</td>
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
        </tr>
        <tr>
            <td><strong>3</strong></td>
            <td><strong>Síťová</strong></td>
            <td>Paket</td>
            <td>Propojuje nesousední systémy – komunikace dvou uzlů, které nejsou přímo spojeny (prostřednictvím jiných uzlů). Logická adresace – IP protokol – IP adresa. Směrování – určení cesty paketu; všechny směrovače pracují na této vrstvě.</td>
        </tr>
        <tr>
            <td><strong>2</strong></td>
            <td><strong>Linková</strong></td>
            <td>Rámec</td>
            <td>Přenáší data mezi dvěma přímo spojenými uzly. Uspořádání dat z fyzické vrstvy do rámců. Pracuje s rámci, hlásí chyby. Adresace MAC a LLC. Na této vrstvě fungují přepínače; propojení pouze místních zařízení. Ethernet, Wi-Fi, ZigBee.</td>
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
