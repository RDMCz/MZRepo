# SW 22 – AJAX, REST

## AJAX

* Asynchronous JavaScript and XML
  * Dnes se spíše používá JSON místo XML
* Technologie pro tvorbu interaktivních aplikací nejen v prostředí webu
* Základní myšlenka – Změna části stránky, aniž by se celá musela znovu načíst
* Vizuálně hezčí, šetří se data
* Využití např.:
  * React axios
  * Komplexní webové aplikace od (Office, Gmail)
  * Našeptávače, interaktivní formuláře, validace dat na straně klienta
  * Chat

### Použité technologie

1. HTML a CSS – vzhled a struktura stránky
2. DOM a JavaScript – modifikování obsahu na straně klienta
    * DOM – Document Object Model – jazykově nezávislé rohraní umožňující přístup a aktualizaci prvků v dokumentu
3. XMLHttpRequest (XHR) Object
    * Zajišťuje komunikaci mezi serverem a klientem, (nejen) protokol HTTP
    * Stěžejní prvek AJAXu
    * Vytváření dotazů na dodatečná data
4. XML, JSON, HTML, prostý text – formát dat pro výměnu informací
    * XML – "Abstraktní HTML", dnes nahrazeno JSONem (úspora místa)

### Komunikace

__Pomocí AJAXu__ (asynchronní komunikace):

* Uživatel chce vidět podrobnosti o nějaké věci na stránce, rozklikne ji v prohlížeči
* Klient (prohlížeč) žádá server o konkrétní data
* Server zpracuje požadavek, vrací pouze požadovaná formátovaná data
* Klient obdrží data a aktualizuje jen nutné části stránky

Výhoda:

* Přenos méně dat (ovšem tendence k častějšímu přenosu)
* Není potřeba sestavovat HTML stránku na straně serveru

Nevýhoda:

* Nutná podpora v prohlížečích
* Čtečky webových stránek mají s aktualizovaným obsahem problém
* Některé web crawlery nemusí spouštět JS – neindexuje se AJAX obsah (Google crawler JS podporuje)

__Bez AJAXu__ (klasická komunikace):

* Uživatel chce vidět podrobnosti o nějaké věci na stránce, rozklikne ji v prohlížeči
* Klient (prohlížeč) žádá server o celou stránku
* Server zpracuje požadavek, vrací celou novou stránku

Výhoda:

* Jednoduchá implementace

Nevýhoda:

* Náročné na data
  * Pokaždé se zpracovává a přenáší kompletní webová stránka
  * Přenos veškerých dat (i těch nezměněných) – HTML, CSS, JS, grafika, ...
* Náročné na výkon
  * Pokaždé je nutno stránku sestavit (server) a vyrenderovat (klient)

## JSON a XML

* Formáty pro výměnu dat

__XML__ – Extensible Markup Language:

* Myšlenka – Čitelný strojem i člověkem
* Aplikace – SVG, Česká státní správa

``` xml
<person gender="male">
    <firstname>John</firstname>
    <lastname>Doe</lastname>
</person> 
```

__JSON__ – JavaScript Object Notation:

* Zápis objektů v JS
* Název proměnné (klíče) ale musí být v uvozovkách
* Při serializaci složitějších dat může nastat problém

``` json
{
    "name": "John Doe",
    "phoneNumbers": [
        {
            "type": "home",
            "number": "777777777"
        },
        {
            "type": "office",
            "number": "666666666"
        }
    ]
}
```

## Odeslání a zpracování požadavku

``` javascript
fetch("example.com/profile", {
    method: "POST"
})
.then(function(response) {
    return response.json();
})
.catch(function(error) {
    console.log(error);
})
.then(function(data) {
    // Nastane v obou případech
    // Uklizení dat
});
```

* XMLHttpRequest dnes používán prostřednictvím axios nebo Fetch API

### Fetch API

* Nahrazuje XMLHttpRequest globálně přístupnou metodou `fetch`
* Vyžádání dat, asynchronní request
* Nefunkční v Internet Exploreru
* Vrací objekt `Promise`

### Promise

* Dva možné stavy – data přišla `successCallback` / data nepřišla, chyba `failureCallback`

## API

* Application Programming Interface
* Rozhraní pro programování aplikací
* Sbírka funkcí/tříd/protokolů/... nějaké knihovny/programu/kernelu/...
* Na serveru se používá webové API s endpointy

## Dotazovací Metody HTTP

__Representational State Transfer (REST)__:

* URL (Uniform Resource Locator) reprezentuje přímý přístup k datům
* `http://www.server.cz/knihy` vrací seznam knih
* `http://www.server.cz/knihy/4` vrací knihu s ID == 4
* REST metody:
  * `GET` – získat
  * `POST` – vytvořit
  * `DELETE` – smazat
  * `PUT` – klient zasílá data, která aktualizují celou entitu
  * `PATCH` – aktualizuje pouze část entity
  * `OPTIONS` – dotaz na server, jaké podporuje metody
