# HW 11 – Síťové prvky, přiřazení k vrstvám OSI/ISO

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
            <td>Vrstva nejblíže k uživateli. Obsahuje jádro aplikací, které má smysl standardizovat (např. přenosové mechanismy elektronické pošty), zbylé části aplikace (UI) byly posunuty nad aplikační vrstvu. Poskytuje uživatelským programům ucelené služby.</td>
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

* __Pasivní síťový prvek__ – Pouze přenáší data a nijak do nich nezasahuje: konektor, kabel, spojka, ...
* __Aktivní síťový prvek__ – S datovým signálem vykonává určitou aktivní činnost:

## Opakovač (Repeater)

* Fyzická vrstva – Pracuje přímo s elektrickým signálem
* Přijímá degradovaný (zkreslený, zašuměný, poškozený) signál
* Vysílá opravený a zesílený signál
* Zvýšení dosahu média (Ethernet kabel 100 m) bez ztráty kvality signálu
* Využití hlavně u podmořských kabelů

## Rozbočovač (Hub)

* Fyzická vrstva – Větvení sítě
* Umožňuje větvení sítě do hvězdicové topologie
* Obnovuje data jako opakovač
* Obnovená data rozešle na všechny svoje porty (kromě portu, z kterého data přišla)
* U větších sítí zatěžuje uzly, kterým data nebyla určena
* Nižší latence než switch, ovšem nulová bezpečnost (broadcast storm, na hubu lze sledovat veškerý provoz sítě)
* Nemá žádnou "inteligenci" (VLAN, STP, ...)

## Most (Bridge)

* Linková vrstva – Spojuje dvě lokální sítě – Dva porty
* Je neviditelný pro protokoly vyšších vrstev
* Rozděluje provoz sítě a tím zmenšuje její zatížení
* Ve své paměti má uloženo, k jakému portu patří jaká MAC adresa
* Pokud se příjemce nachází ve stejné části sítě (na stejném břehu), jako odesílatel, bridge rámce do druhé části sítě neodešle
* Rozsah broadcastu se neomezuje

## Přepínač (Switch)

* Linková vrstva
* Počet portů obvykle v rozmezí 5-52 (Cisco), propojuje prvky do hvězdicové topologie
* Narozdíl od hubu přeposílá provoz pouze tam, kde je potřeba
* V podstatě bridge s více porty
* CAM – Content Adressable Memory
  * Tabulka, kde jsou přiřazené adresy k portům
  * Pokud cílovou adresu v tabulce nenajde, použije broadcast
* Rozšíření množství portů:
  1. Propojit více switchů – pomalejší
  2. Modulární switche
  3. Propojit switche speciální paralelní sběrnicí

## Směrovač (Router)

* Síťová vrstva – Propojení dvou cizích sítí
* Přeposílá pakety směrem k jejich cíli – Cílem je cizí síť
* Směrovací tabulka (routing table) obsahuje adresu sítě, masku a port (interface), na kterém se nachází
* Routování:
  * Statické – routy nastavuje správce
  * Dynamické – routy nastavuje směrovač pomocí protokolů
* Pakety mají omezenou životnost TTL (time to live)

## Firewall

* Dá se chápat jako brána, která rozhoduje, zdali se přes ní dostanou nějaká data, resp. zdali spolu dvě sítě mohou navázat spojení
* Základní proměnnou je adresa a port zdroje a cíle
* ACL – Access Control List – Seznam pravidel řídících přístup k nějakému objektu
* IDS – Intrusion Detection System – Monitorování provozu a snaha odhalit podezřelé aktivity
  * Senzor obsahující mechanismy pro detekci nebezpečných kódů
* IPS – Intrusion Prevention System

## Wi-Fi Router

* Router + switch + access point
* Zapnutá NAT (občas i natvrdo)
* Dva druhy Ethernet portů:
  * Obvykle 1 modrý – pro připojení WAN
  * Obvykle 4 žluté – slouží jako switch
* Nastavení routeru přes prohlížeč, user friendly UI
* Lze si nastavit DHCP, QoS, VPN, ...
* Existují také Wi-Fi DSL Modem Routery (do WAN je připojen přes RJ-11 namísto RJ-45)
