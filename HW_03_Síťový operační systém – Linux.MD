# HW 03 – Síťový operační systém – Linux

* Výběr operačního systému (vhodné distribuce Linuxu)
* Instalace operačního systému, připojení uživatelů
* Druhy souborových systémů používaných v současných verzích OS
* Koncepce souborového systému, stromová struktura, druhy souborů
* Práva a oprávnění, nastavení oprávnění pro soubory (rwx), databáze uživatelů a hesel
* Změna vlastníka a oprávnění

## Linux

* Open-source unix-like operační systém založený na linuxovém jádře (Linus Torvalds)
* Linux je typicky zabalen v linuxové distribuci

## Výběr distribuce

* Aplikace:
  * Desktop – Mint, Ubuntu, Fedora, Arch
  * Server – Red Hat, CentOS, Ubuntu Server, SUSE
  * Embedded systems – IoT, routery
  * Smartphone – Android
  * Superpočítače

* Základní distribuce – Slackware, Debian, Red Hat, ...

### Distribuce

* Všechny distribuce mají stejné základní jádro
* Liší se v:
  * Doplňující software
  * Package manager
  * GUI – grafická nadstavba
    * GNOME
    * KDE Plasma
    * Cinnamon
    * MATE
    * Xfce

## Instalace a systém

### ISO soubor

* Obsahuje Live CD + instalátor
* Jedná se o obraz CD/DVD
* Rufus – vytvoření bootovatelné flashky

### Instalátor

* Jazyk
* Rozložení klávesnice
* Typ instalace – vymazat disk a nainstalovat nebo vytvářet a upravovat oddíly
* Časové pásmo
* Vytvoření uživatele

<img src="./img/HW_03_01.PNG" width="777" />

* Prvním krokem po instalaci by měli být aktualizace
* Linux lze také spustit ve Windows pomocí WSL (Windows Subsystem for Linux)
* Přístup k systému přes terminál
* V systému běží několik virtuálních terminálů
  * Přistupuje se k nim `Ctrl` + `Alt` + funkční klávesa
  * Např. na Mint běží GUI na virtuálním terminálu `Ctrl` + `Alt` + `F7`

## Soubory

### ext4

//TODO 16:40
