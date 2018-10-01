# Anatomy of HTML

## Tags, attributes, and elements

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

## HTML template

There is a set of elements that make up the basic structure of every HTML document. The following code snippet shows the prototypical structure.

```markup
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My first page</title>
  </head>
  <body>
    <p>A paragraph with text.</p>
  </body>
</html>
```

{% embed data="{\"url\":\"https://codepen.io/winf-hsos/pen/EdjOga\",\"type\":\"rich\",\"title\":\"HTML Basic Structure\",\"description\":\"...\",\"icon\":{\"type\":\"icon\",\"url\":\"https://codepen.io/favicons/favicon-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://s3-us-west-2.amazonaws.com/m.cdpn.io/screenshot-coming-soon-small.png\",\"width\":400,\"height\":225,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"app\",\"url\":\"https://codepen.io/winf-hsos/embed/preview/EdjOga?height=300&slug-hash=EdjOga&default-tabs=html,result&host=https://codepen.io&embed-version=2\",\"html\":\"<iframe src=\\\"https://codepen.io/winf-hsos/embed/preview/EdjOga?height=300&amp;slug-hash=EdjOga&amp;default-tabs=html,result&amp;host=https://codepen.io&amp;embed-version=2\\\" style=\\\"border: 0; width: 100%; height: 300px;\\\" allowfullscreen></iframe>\",\"height\":300,\"aspectRatio\":null}}" %}

As you can see, an HTML document contains two sections: The head and the body. Both serve a special purpose and contain different types of elements.

## References

Read the following articles on MDN to get more information on elements, attributes, and the anatomy of an HTML document.

| Link |
| :--- |
| [Anatomy of an HTML Element \(MDN\)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started#Anatomy_of_an_HTML_element) |
| [HTML Attributes \(MDN\)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started#Attributes) |
| [Anatomy of an HTML Document \(MDN\)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started#Anatomy_of_a_HTML_document) |

