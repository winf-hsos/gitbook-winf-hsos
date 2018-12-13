# JavaScript fürs Web

## HTML mit JavaScript verändern

JavaScript erlaubt es uns, den HTML-Baum und all seine Attribute nach dem Laden der Webseite zu verändern. Damit kann z.B. das Hinzufügen oder Löschen von HTML-Elementen gemeint sein. Aber auch das bloße Ändern des \(Text-\) Inhalts oder Attributwerten.

Das Vorgehen ist dabei immer gleich:

1. Zugriff auf das HTML-Element, am einfachsten über eine eindeutige ID. Wir speichern das Element auf einer Variable, um anschließend damit arbeiten zu können.
2. Durchführen der gewünschten Veränderungen \(z.B. neue Kind-Elemente anfügen im Fall einer Liste, Textinhalt verändern etc.\)

Es folgen Beispiele für die häufigsten DOM-Manipulationen, die ihr benötigen werdet.

### Textinhalt verändern

#### HTML

Vergebt im HTML eine ID für ein HTML Element, das ihr mit JavaScript manipulieren wollt.

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
<p id="one"></p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### JavaScript

Verwendet die Funktion `document.querySelector()`, um euch mit JavaScript Zugriff auf das Element zu verschaffen. Nutzt anschließend `textContent` oder `innerHTML`, um den Inhalt des Elements zu setzen.

{% code-tabs %}
{% code-tabs-item title="script.js" %}
```javascript
var pElement = document.querySelector("#one");
pElement.textContent = "This text is set with JS";

// Instead of text use HTML like this
pElement.innerHTML = "This <tt>text</tt> is set with <b>JS</b>";
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Arrays

Sortierte Listen - oder Arrays - begegnen uns häufig im Zusammenhang mit dem Lesen von Daten aus der Firestore-Datenbank. Deshalb ist es wichtig, dass wir die gängigsten Operationen mit Arrays in JavaScript kennen und anwenden können.

### Alle Elemente eines Arrays durchlaufen

{% code-tabs %}
{% code-tabs-item title="script.js" %}
```javascript
// Reading a Firestore collection like this results in an array with 
// all documents.
firebasetools.getContentItems("todos", todosReady);

// This callback-function is called with the todos
function todosReady(todosArray) {
    
    // We can use a FOR-loop to iterate all todos
    for(var i = 0; i < todosArray.length; i++) {
        console.dir(todosArray[i]);
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Data-Attribute

#### HTML

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
<p id="one" data-id="1" data-author="Michael"></p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### JavaScript

{% code-tabs %}
{% code-tabs-item title="script.js" %}
```javascript
// Access data attributes via the .dataset collection
var elementId = document.querySelector("#one").dataset.id;

// Change the value of an existing data attribute
document.querySelector("#one").dataset.author= "Gordon";

// Set new data attributes
document.querySelector("#one").dataset.title = "Introduction to JavaScript";
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Mehr zu Data-Attributen findet ihr u.a. auf der MDN Dokumentationsseite:

{% embed url="https://developer.mozilla.org/en-US/docs/Web/HTML/Global\_attributes/data-\*" %}

