---
description: >-
  Mit HTML beschreiben wir die Struktur der Webseite und bestimmen, welche
  Elemente wie Überschriften, Absätze, Bilder oder Tabellen vorhanden sein
  sollen.
---

# HTML

## 💡 Was ist HTML?

HTML steht für _Hypertext Markup Language_. Wie der Name suggeriert ist HTML eine _Beschreibungs_sprache und keine Programmiersprache.

HTML verwendet so genannte **Tags**, um Bestandteile einer Webseite zu beschreiben. Ein Tag ist besteht aus einem definierten Schlüsselwort, das von einem Kleiner- und einem Größerzeichen eingeschlossen ist. Ein HTML **Element** besteht aus einem öffnenden und einem schließenden Tag. Der schließende Tag sieht genau so aus wie der öffnende, bis auf den Slash vor dem Schlüsselwort:

```markup
<h1>Das ist eine Überschrift</h1>
```

HTML kennt eine Reihe von Tags, die wir entweder kennen müssen oder [nachschlagen können](https://developer.mozilla.org/de/docs/Web/HTML/Element), um sie zu verwenden. Um wie oben gezeigt eine Überschrift auf unserer Webseite anzuzeigen, können wir den `<h1>` Tag nutzen. Mit dem `<p>` Tag erzeugen wir einen Abschnitt, und der `<img>` Tag bindet ein Bild auf der Webseite ein.

Der `<img>` Tag ist ein Beispiel für ein Element mit einem **Attribut**. Um anzugeben, wo sich das Bild befindet, verwenden wir das `src` Attribut:

```markup
<img scr="https://bilder.de/image.jpg">
```

Mit Attributen geben wir einem Element zusätzliche Informationen, die es genauer beschreiben. Ein Element kann auch mehr als ein Attribut haben, wie im Beispiel eines Links:

```markup
<a href="https://google.de" target="_blank">Link zu Google in neuem Tab</a>
```

{% hint style="info" %}
HTML ist **keine Programmiersprache**. Mit HTML lassen sich Dokumente **beschreiben**, wir können aber keine ausführbaren Programme damit erstellen. Dazu bräuchten wir Konzepte wie Variablen und Kontrollstrukturen wie Schleifen oder Wenn-Dann-Verzweigungen. Nichts davon existiert in HTML.
{% endhint %}

## 💡 Wie sieht eine HTML Seite aus?

Jede Seite beinhaltet eine Menge an Elementen, die auch das HTML-Grundgerüst genannt werden:

```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Titel der Webseite</title>
        
        <!-- You can use meta tags to describe your site -->
        <meta charset="utf-8">
        <meta name="author" content="Nicolas Meseth" />
        
        <!-- You can link to files, such as CSS -->
        <link rel="stylesheet" href="style.css">
    </head>
   
    <body>
        <h1>Das ist eine Überschrift</h1>
        <p>Das ist ein Absatz</p>    
    </body>
</html>
```

