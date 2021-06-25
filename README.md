# Ressourcen, Fragen & Antworten
Fragen und Antworten rund um Front- und Backend Webentwicklung. 

# Inhaltsverzeichnis

## 1. Ressourcen

* ### Linksammlungen

  * ![image](react.png)[React Resources](https://reactresources.com/)
  * ![image](react.png)[Awesome React](https://github.com/enaqx/awesome-react)

* ### Artikel und Tutorials
  * ![image](javascript.png)[Implementing a simple Promise in Javascript](https://medium.com/swlh/implement-a-simple-promise-in-javascript-20c9705f197a)

* ### Nützliche Helfer
  * ![image](layout.png)[Iconscout](https://iconscout.com/) - SVG, Icons, Grafiken etc.

## 2. Fragen und Antworten

* ### Javascript
  <a name="this_in_javascript"></a>
  * [This in Javascript](#this-in-javascript)

* ### React

* ### CSS


<br>
<hr>

### This in Javascript  
***This*** ist in Javascript eine Referenz auf den Execution Context. Der Wert von ***This*** hängt also nicht davon ab **wo** das Keyword benutzt wird, sondern **wie**, in welchem Kontext es aufgerufen wird!<br><br>
Im ***globalen Ausführungskontext*** (das heisst ausserhalb jeder Funktions) verweist ***this*** auf das globale Objekt, im Webbrowser ist das **window** Objekt das globale Objekt

Im Funktionskontext hängt der Wert von this davon ab, wie diese Funktion aufgerufen wird:

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



<br><br>:arrow_up:[Nach oben](#this_in_javascript)
