# Ressourcen, Fragen & Antworten
Fragen und Antworten rund um Front- und Backend Webentwicklung. 

# Inhaltsverzeichnis

## 1. Ressourcen

* ### Linksammlungen

  * [React Resources](https://reactresources.com/)
  * [Awesome React](https://github.com/enaqx/awesome-react)

* ### 🦊Artikel, 🔥Tutorials , 🌸 Blogs
  * 🔥[Implementing a simple Promise in Javascript](https://medium.com/swlh/implement-a-simple-promise-in-javascript-20c9705f197a)
  * 🌸[How Javascript works](https://blog.sessionstack.com/how-javascript-works/home) Eine Serie über die Bausteine und Internals von Javascript
  * 🌸[Dmitri Pavlutiin](https://dmitripavlutin.com/) I help developers understand JavaScript and React
  * 🔥[Flat File CMS](https://cmsstash.de/empfehlungen/flat-file-cms)
  * 🔥[React Micro Frontend](https://tsh.io/blog/micro-frontend-tutorial/) Ein Formular mit React erstellt in eine Webseite einbetten
  * 🔥[How NOT to build micro frontends](https://tsh.io/blog/how-not-to-build-micro-frontends/)
  * 🔥[Micro Front End Integration](https://martinfowler.com/articles/micro-frontends.html#Run-timeIntegrationViaJavascript) Run tine Integration Beispiel
  * 🌸[The software house blog](https://tsh.io/blog/) Interessant rund um React, Node etc.
  * 🔥[Building a react container query hook](https://non-traditional.dev/building-a-react-container-query-hook-for-dom-elements-ee25cd208740) 
  * 🦊[CSS font-display](https://css-tricks.com/almanac/properties/f/font-display/) Wie lädt man Fonts am besten, FOIT und FOUT
  * 🔥[Application-state-management-with-react](https://kentcdodds.com/blog/application-state-management-with-react) Top Artikel von Kent C. Dodds
  * 🌸[Logrocket Blog](https://blog.logrocket.com//) Interessant rund um React, Node etc.





* ### Nützliche Helfer
  * [Iconscout](https://iconscout.com/) - SVG, Icons, Grafiken etc.

* ### Allerlei
  * [ericlo.dev](https://ericlo.dev/) - Visualisierungen mit d3js.



## 2. Fragen und Antworten

* ### Javascript
  <a name="this_in_javascript"></a>
  * [Destrukturieren von Funktionsparametern](destrukturieren-von-funktionsparametern)<a name="destrukturieren_von_funktionsparametern"></a>
  * [Die Scope Chain](die-scope-chain)<a name="die_scope_chain"></a>
  * [use strict](#use-strict)<a name="use_strict"></a>
  * [This in Javascript](#this-in-javascript)<a name="this_in_javascript"></a>
  * [This in Arrow Funktionen](#this-in-arrow-funktionen)<a name="this_in_arrow_funktionen"></a>
  * [Die verschiedenen Scopes in Javascript](#die-verschiedenen-scopes-in-javascript)<a name="die_verschiedenen_scopes_in_javascript"></a>
  * [Closure](#closure)<a name="closure_link"></a>
  * [React in bestehenden Seite einbetten](#react-einbetten)

* ### React

* ### CSS


<br>
<hr>

### Destrukturieren von Funktionsparametern
 
⬆️ [Nach oben](#destrukturieren_von_funktionsparametern)

<hr>




### Use strict

Der strict mode erzeugt einen Fehler wenn eine Variable nicht deklariert wurde. Im folgenden Beispiel ohne strict mode wird nicht erkannt, dass die Variable meineVar bei der erneuten Zuweisung falsch geschrieben wurde - dies produziert schwer zu findende Fehler.

```javascript
var meineVar = 0
console.log(meineVar),
meinVar = 1  // Neuer Wert wird zugewiesen, ABER mit Schrreibfelher.

if(meineVar > 0) {
 console.log("Hallo);
}
```

Ausserdem verhindert der srict mode:
* Benutzen von für zukünftige JS Versionen **reservierte Keywords**
* Löschen von Funktionen und Variablen mit **delete**
* Die **eval** Funktion wird sicherer, da Zuweisungen an nicht deklarierte oder bereits deklarierte Variablen verhindert werden


⬆️ [Nach oben](#use_strict)

<hr>

### This in Javascript  
***This*** ist in Javascript eine Referenz auf den Execution Context. Der Wert von ***This*** hängt also nicht davon ab **wo** das Keyword benutzt wird, sondern **wie**, in welchem Kontext es aufgerufen wird!<br><br>
Im ***globalen Ausführungskontext*** (das heisst ausserhalb einer Funktion) verweist ***this*** auf das globale Objekt, im Webbrowser ist das **window** Objekt das globale Objekt

Im **Funktionskontext** hängt der Wert von this davon ab, wie diese Funktion aufgerufen wird:

```javascript

function f1(){
  return this;
}

// In einem Browser:
f1() === window; // true

```

Der Execution Context von f1() ist also das window Objekt, man kann auch schrieben window.f1() - dann wird dies deutlicher.

Anders sieht es hier aus:

```javascript

const myObject = {
  name: "Markus",
  myFunction: function () {
    console.log(this.name);
  }
};

myObject.myFunction(); // --> Markus

```

Nun ist der Execution Context das Objekt myObject, welches direkt links neben dem Aufruf der Funktion myFunction steht.

Erstellen wir ein weiteres Objekt ***value*** und nehmen die Eigenschaft ***name*** aus diesem Objekt heraus und definieren diese in dem Objekt ***myObject***, dann ist der Execution Context der Funktion ***myFunction*** das Objekt ***value***. Entsprechend ist this.name undefined : 

```javascript
const myObject = {
  name: "Markus",
  value: {
    myFunction: function () {
      console.log(this.name);
    }
  }
};

myObject.value.myFunction(); // --> undefined
```

Mit ***call***, ***apply*** oder ***bind*** kann man den Wert von this setzen:

```
myObject.value.myFunction.call(myObject); // --> Markus
myObject.value.myFunction.apply(myObject); // --> Markus
myObject.value.myFunction.bind(myObject)(); // --> Markus

```


⬆️ [Nach oben](#this_in_javascript)

<hr>

### This in Arrow Funktionen  

:bulb:Arrow Funktionen kennen das Konzept von ***this*** nicht. Eine Arrow Funktion hat kein eigenes ***this***. ***This*** wird wie eine normale Variable behandelt. 

Es wird das ***this*** des umschliessenden **Lexical Scope** benutzt! Arrow Funktionen folgen also den normalen Regeln für Variablen. Ist eine Variable im aktuellen Scope nicht definiert, wird sie im umschliessenden Scope gesucht. Eine Arrow Funktion wird also immer ***this*** im umschliessenden Scope suchen - und zwar im **lexikalischen Scope**!

```javascript

const myFunction = () => {
  console.log(this);
};

myFunction();  // --> window

console.log(this); // --> window

```
Das ist das gleiche Resultat wie bei einer normalen Funktion - aber aus einem anderen Grund. Bei der normalen Funktion zeigt this auf das ausführende Objekt, also das window Objekt. Die Arrow Funktions kennt kein this und sucht deshalb im umgebenden lexikalischen Scope, und dies ist der globale Scope und dort ist this das window Objekt.

Arrow Funktion als Methode eines Objekts:

```javascript
const myObject = {
  myMethod: () => {
    console.log(this);
  }
};

myObject.myMethod() // ---> window !!!

```

Die arrow Funktion verhält sich nicht wie eine normale Funktion. Auch hier gilt: Arrow Funktionen verfügen nicht über ein ***this***, sie erben es von ihrem umschliessenden Objekt- In diesem Fall ist es das Objekt ***myObject*** in welchem ***this*** per Definition auf das globale Objekt zeigt, also window.

**Call, apply und bind funktionieren nicht mit Arrow Funktionen. Ebenso funktioniert der new Operator nicht mit Arrow Funktionen.**



🔗 [Understanding this in arrow functions](https://www.codementor.io/@dariogarciamoya/understanding-this-in-javascript-with-arrow-functions-gcpjwfyuc)

⬆️ [Nach oben](#this_in_arrow_funktionen)

<hr>

### Die verschiedenen Scopes in Javascript

Es gibt 3 Scopes in Javascript :
* Global Scope
* Function Scope
* Block Scope

Wird eine Variable ausserhalb einer Funktion mit ***var*** definiert, so ist sie überall sichtbar. Dies ist der **Global Scope**.

Wird eine Variable innerhalb einer Funktion mit ***var*** definiert, so ist sie nur innerhalb dieser Funktion sichtbar, das ist der **Function Scope**.

Wird eine Variable mit ***let*** oder ***const*** innerhalb eines Blocks ( {} ) definiert, so ist sie nur innerhalb dieses Blocks sichtbar, dies ist der **Block Scope**

⬆️ [Nach oben](#die_verschiedenen_scopes_in_javascript)
<hr>


### Closure

Eine **Closure** gibt einer inneren Funktion ***sayHello*** Zugriff auf den Scope einer äusseren Funktion ***factoryMachHallo***.

```javascript
    var factoryMachHallo = function(sprache) {

        var gruss;    

        if( sprache === "de") {
            gruss = "Guten Tag ";    
        }    

        if ( sprache === "en") {
            gruss = "Good day "
        }
        

        var sayHello = function(name) {
            console.log(gruss + name);
        }   

        return sayHello     

    }

    sagHalloEnglisch = factoryMachHallo("en");
    sagHalloDeutsch  = factoryMachHallo("de");
    sagHalloDeutsch("Markus");
    sagHalloEnglisch("Markus");
    
    // In dev Tools bei Aufrunf von sagHalloEnglisch :
    Closure (factory)
      gruss: "Good day "
    
```   

Closures werden von JS automatisch erstellt wenn sie benötigt werden. Ohne eine Closure hätte im obigen Beispiel die Funktion **sagHalloDeutsch** keinen Zugriff auf den local Scope der Funktion **factoryMachHallo** da diese ja bereits ausgeführt wurde. Durch die Closure wird die lokale Variable ***gruss*** erhalten und ist für die innere Funktions ***sayHello*** zugänglich. Es wird für jeden Aufruf der Funktion ***sayHello*** eine neue Closure erstellt ( Bei Aufruf der Funktions ***sagHalloDeutsch*** ist der Wert von ***gruss*** = "Guten Tag").

⬆️ [Nach oben](#closure_link)


<hr>


### React einbetten

so habe ich es auch immer gemacht:

https://betterprogramming.pub/how-to-embed-a-react-application-on-any-website-1bee1d15617f

Es geht auch anders:

While all this is doable, it is not easy to make robust, and doing it inside NextJS makes it more cumbersome. My advice would be to structure the code of your NextJS app in such a way that the parts you need in the widget are components that you can use both in the NextJS main app and in a separate embeddable widget using plain CRA.

Some further reading:

https://selleo.com/blog/how-to-create-embedded-react-widget (not the iFrame parts though)

https://meda.io/embed-react-into-an-html-web-page/

So sollte es doch auch gehen....
https://maferland.com/blog/publishing-library-minimal-config

⬆️ [Nach oben](#closure_link)


<hr>


### Ein div so hoch machen wie der verbleibende Raum auf der Seite


```html
<body>
    <header>Header with an arbitrary height</header>
    <main>
        This container will grow so as to take the remaining height
    </main>
</body>
```

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;       /* body takes whole viewport's height */
}

main {
  flex: 1;                 /* this will make the container take the free space */
}
```

⬆️ [Nach oben](#closure_link)


<hr>




