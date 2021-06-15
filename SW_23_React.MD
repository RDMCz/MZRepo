# SW 23 – React

## React

* Open-source frontend JavaScript knihovna pro návrh UI a UI komponent
* Vyvíjen mj. Facebookem
* První veřejná verze 0.3.0 (2013)
* Existuje také framework React Native umožňující vývoj aplikací pro Android, iOS, Windows, ...

## DOM – Document Object Model

* Jazykově nezávislé rohraní umožňující přístup a aktualizaci prvků v dokumentu
* Reprezentuje dokument tak, aby program mohl měnit jeho strukturu a obsah
* Prohlížeč si stránku po jejím stažení převede na DOM
  * Všechny prvky stránky jsou díky tomu v paměti uloženy jako objekty a uspořádány do stromu
  * Díky DOM může JavaScript přistupovat ke všem HTML prvkům na stránce

### Virtual DOM

* Používá ho např. React nebo Vue.js
* VDOM je abstraktnější, rychlejší a odlehčená reprezentace pravého DOMu
  * Struktura pravého DOMu u SPA může být komplexní a operace v ní tedy pomalé
* Eliminuje zbytečné překreslování neměnných komponent
  1. Vytvořit VDOM s novým stavem aplikace
  2. Porovnat s předchozím VDOM
  3. V pravém DOM aktualizovat pouze ty komponenty, které se změnily

## Component

* Rozdělují UI aplikace do nezávislých, znovupoužitelných částí – enkapsulace
* Lze je zapsat jako třídu nebo jako funkci

``` jsx
const Welcome = ({name}) => {
    return (
        <>
            <h1>Hello, {name}!</h1>
        </>
    );
}

export default Welcome;
```

``` jsx
import Welcome from "./Components/Welcome";

const App = () => {
  return (
    <>
        <Welcome name={"John Doe"} />
    </>
  );
}

export default App;
```

## Props

* Props si lze "vyzvednout" dvěma způsoby

``` jsx
const Welcome = ({name, surname}) => { return (<><h1>Hello, {name} {surname}!</h1></>); }
const Welcome = (props) => { return (<><h1>Hello, {props.name} {props.surname}!</h1></>); }
```

## Hook

* Háky byly přidány ve verzi 16.8.0 (2019)
* Umožňují používat funkce Reactu bez použití třídy
  * Nefungují uvnitř tříd, pouze uvnitř React funkcí
* Musí se volat na nejvyšší úrovni, vždy ve stejném pořadí
  * Nelze je tedy volat ze smyček, podmínek apod.

## useState

* Každá class komponenta má vestavěný state
* Funkcionální komponenta může také mít svůj state díky háku useState
* Do statu se ukládají data (proměnné) komponenty
* Tato data "přežijí" překreslení komponenty – deklarace se znovu nezavolá (refresh stránky nepřežijí)
* Při změně těchto dat se komponenta překreslí

``` jsx
{/*const [<název proměnné>, <název metody pro změnu proměnné>] = useState(<iniciální hodnota>);*/}
const [name, setName] = useState("");
```

## useEffect

``` jsx
useEffect(() => {
    {/*Kód, který se má spustit*/}        
}, []);
```

* Druhým parametrem háku useEffect je pole prvků – pokud jakýkoliv z nich změní svou hodnotu, je spuštěn kód uvnitř háku
  * Pokud je pole prázdné, slouží hák jako konstruktor

## useContext

* Umožňuje mít společná globální data, která nemusíme všem komponentám tunelovat pomocí props
* V kombinaci s hákem `useReducer` lze mít i globální logiku

## Událost

Oproti klasickému JavaScriptu:

* Názvy událostí jsou camelCase, nikoliv lowercase
* Funkce se předává jako event handler, nikoliv string
* Nelze vracet false
* Není potřeba volat `addEventListener`

## Ukázka kódu

``` jsx
import { createContext } from "react";

export const ListContext = createContext(null);
```

``` jsx
import { useState } from 'react';
import { Route, Router, Switch } from "react-router-dom"; {/*Je třeba doinstalovat balíček react-router-dom*/}
import { createBrowserHistory } from "history";

import Home from "./Components/Home";
import { ListContext } from "./Providers/ListContext";

const App = () => {

    const [context, setContext] = useState([]);

    return (
        <>
            <ListContext.Provider value={{context, setContext}}> {/*Všechny child komponenty mají přístup ke contextu*/}
                <Router history={history}>
                    <Switch>
                        {/*Router Switch zobrazuje komponenty na základě adresy v adresním řádku*/}
                        <Route exact path="/" component={Home}></Route>
                    </Switch>
                </Router>
            </ListContext.Provider>
        </>
    );
}

const history = createBrowserHistory();

export default App;
```

``` jsx
import { useContext, useState } from 'react';

import { ListContext } from "../Providers/ListContext";

const Home = () => {

    {/*Hák nahrazuje komponentu <ListContext.Consumer>*/}
    const {context, setContext} = useContext(ListContext);

    const [text, setText] = useState("");

    const AddItem = (item) => {
        setContext([...context, item]);
    }

    return (
        <>
            {
                context.map((item, index) => (
                    <div key={index}>{item}</div>
                ))
            }

            {/*Použití událostí:*/}
            <input value={text} onChange={e => {setText(e.target.value)}}></input>
            <button onClick={() => AddItem(text)}>Přidat položku</button>
        </>
    );
}
```

## Propagace stavu

* Pokud v potomkovi chceme změnit hodnotu rodiče, předáme mu v props metodu na změnu této hodnoty

## npm

``` npm
npx create-react-app nazev-aplikace
npm install --save bootstrap reactstrap axios react-router-dom formik
npm start
```
