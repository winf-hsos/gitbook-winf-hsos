---
description: >-
  Mit HTML beschreiben wir die Struktur der Webseite und bestimmen, welche
  Elemente wie Überschriften, Absätze, Bilder oder Tabellen vorhanden sein
  sollen.
---

# HTML

## Das Grundgerüst

Jede Seite beinhaltet eine Menge an Elementen, die auch das HTML-Grundgerüst genannt werden:

```markup
<html>
    <head>
        <title>Titel der Webseite</title>
        <meta name="author" content="Nicolas Meseth" />
    </head>
   
    <body>
        <h1>Das ist eine Überschrift</h1>
        <p>Das ist ein Absatz</p>    
    </body>
</html>
```

## Begriffe rund um HTML

### Tags, attributes, and elements

A website is written in HTML, which is a so called markup language. A markup language differs from a programming language in an important way: You cannot write a program and run it, you can only _describe_ the elements and the structure of a document, in this case a website. A program requires commands, if-then-else structures, and loops. HTML has none of that.

In HTML, we use _tags_ to describe our website. A tag is a keyword enclosed by brackets. Most tags come in two versions: An opening tag and a closing tag. The closing tag differs from the opening tag by one symbol, the forward slash `/`:

```markup
<!-- Opening tag looks like this -->
<body>
...
<!-- Closing tag has an additional slash -->
</body>
```

We call a combination of opening and closing tag an HTML _element_.

HTML elements can have one or more attributes. Attributes add more information to an element. For example, the hyperlink element `<a>` has an attribute to define the destination of the hyperlink:

```markup
<a href="https://google.com">This link takes you to Google</a>
```

Attribute values are not visible in the browser.

