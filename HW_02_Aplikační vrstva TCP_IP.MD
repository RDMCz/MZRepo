# HW 02 – Aplikační vrstva TCP/IP

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

## P2P – Peer-to-peer

* Počítačová síť, kde spolu přímo komunikují jednotliví klienti
* Sdílení prosředků prostřednictvím sítě bez dedikovaného serveru
* Všechna koncová zařízení (peers) si jsou rovna a mohou sloužit jako klient i jako server
* Napster, BitTorrent, Bitcoin, ...

## Klient-server

* Žadatel a poskytovatel
* Na serveru běží jedna nebo více serverových aplikací a prostředky se sdílí s klientem
* Klient inicializuje komunikační relaci se serverem čekajícím na příchozí požadavky
* E-mail (SMTP), WWW (HTTP), ...

## Aplikace

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

### 80 – HTTP – Hypertext Transfer Protocol

* Request-response protocol (klient-server)
* Přenos souborů, převážně HTML

1. Do webového prohlížeče je zadána URL nebo je kliknuto hypertextový odkaz
2. Prohlížeč jakožto klient odesílá GET request na adresu serveru (zjištěna pomocí DNS)
3. Server vrací požadovaná data a/nebo vrací zprávu s číselným označením (200/404/500/...)

* REST – GET, POST, PUT, PATCH, DELETE
* __443 – HTTPS__ – Pomocí asymetrické kryptografie je ověřena identita webového serveru
* Webový server je počítač vyřizující HTTP požadavky od klientů

### E-mail

* Klienti komunikují se serverem kvůli odesílání a přijímání e-mailů
* Servery komunikují mezi sebou kvůli odesílání mezi různými e-mailovými doménami
* __25 – SMTP – Simple Mail Transfer Protocol__
  * Pomocí mailového klienta je odeslán e-mail na mail server
  * Server přijme zprávu. Pokud je určena systému, na kterém běží, odešle ji lokálně. V opačném případě ji odešle na jiný příslušný mail server (spolupráce s DNS).
* __110 – POP3 – Post Office Protocol__
  * Načítání pošty z webového serveru
  * Server na vyžádání odešle zprávu klientovi, a pak ji ze serveru smaže
  * Žádné centralizované místo, kde jsou e-maily uchovány
* __143 – IMAP – Internet Message Access Protocol__
  * Narozdíl od POP3 si klient stahuje kopie zpráv a originál zůstane na serveru
  * Když klient zprávu smaže, server se sesynchronizuje a také ji smaže

### Sdílení souborů

* __20/21 – FTP – File Transfer Protocol__
  * Přenos souborů mezi klientem a serverem
  * 21 – konfigurace; 20 – přenos dat
  * Umožňuje autentifikaci login+heslo
  * __69 – TFTP – Trivial File Transfer Protocol__
    * UDP (oproti klasickému FTP, které je TCP)
    * Neumožňuje autentifikaci, žádná konfigurace
* __445 – SMB – Server Message Block__
  * Client-server, request-response
  * Sdílený přístup k souborům, tiskárnám a sériovým portům
  * Převážně Windows, s Linuxem se lze spojit pomocí softwaru Samba
* __111/2049 – NFS – Network File System__

### 23 – Telnet – Teletype Network

* Client-server
* Připojení ke vzdálenému PC pomocí textového UI – virtuální terminál
* Nešifrovaná komunikace – přechod na SSH

### 22 – SSH – Secure Shell

* Šifrovaná náhrada za Telnet

### 123 – NTP – Network Time Protocol

* Client-server, synchronizace vnitřních hodin počítačů

## 67/68 – DHCP – Dynamic Host Configuration Protocol

* Protokol, který koncovým zařízením v síti automaticky přiřazuje IP adresu, masku, default gateway a adresu DNS serveru

## 53 – DNS – Domain Name System

* Přiřazuje k IP adrese doménové jméno
* Pro překlad adresy se požádá DNS server (nejspíše ten, který nám byl přiřazen DHCP serverem)
  * Pokud server tuto adresu zná, tak odpoví
  * Pokud ne, obrátí se na kořenový DNS server
