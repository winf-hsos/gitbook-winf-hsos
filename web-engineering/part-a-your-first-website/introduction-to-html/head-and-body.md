# Head and Body

## Tags and elements

A website is written in HTML, which is a so called markup language. A markup language differes from a programming language in an important way: You cannot write a program and run it, you can only _describe_ the elements and the structure of a document, in this case a website. A program requires commands, if-then-else structures, and loops. HTML has none of that.

In HTML, we use _tags_ to describe our website. A tag is a keyword enclosed by brackets. Most tags come in two versions: An opening tag and a closing tag. The closing tag differs from the opening tag by one symbol, the forward slash `/`:

```markup
<!-- Opening tag looks like this -->
<body>
...
<!-- Closing tag has an additional slash -->
</body>
```

We call a combination of opening and closing tag an HTML _element_.

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

### The head

The head contains metadata about the website. Nothing that is placed in the head is visible on the website. Among other elements, the `<head>` tag contains the `<title>` tag and at least one `<meta>` tag.

#### &lt;title&gt;

The value of the `<title>` tag defines the title of the website, which is displayed in the browser window bar \(or tab\).

#### &lt;meta&gt;

Usually, a `<meta>` tag has two attributes:

1. `name` : Attribute to describe the type of metadata
2. `content` : Attribute the define the value of that metadata

The listing provides examples for common metadata tags:

```markup
<head>
    <meta name="author" content="Elon Musk">
    <meta name="description" content="Simple website for illustration">
    <meta name="keywords" content="rockets,tesla,universe">
    <meta charset="utf-8">   
</head>
```

The metadata serves several purposes. For example, search engines like Google can use it to better understand the website's content and thereby improve the search results. Moreover, some metatags like the ones defined by the [Open Graph Protocol](http://ogp.me/) allow for an illustrative link preview when shared on Facebook or Slack.

Read more about the head and its elements at the following links:

{% embed data="{\"url\":\"https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction\_to\_HTML/The\_head\_metadata\_in\_HTML\",\"type\":\"link\",\"title\":\"What’s in the head? Metadata in HTML\",\"description\":\"That marks the end of our quickfire tour of the HTML head — there\'s a lot more you can do in here, but an exhaustive tour would be boring and confusing at this stage, and we just wanted to give you an idea of the most common things you\'ll find in there for now! In the next article we\'ll be looking at HTML text fundamentals.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://developer.mozilla.org/static/img/favicon144.e7e21ca263ca.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://developer.mozilla.org/static/img/opengraph-logo.72382e605ce3.png\",\"width\":600,\"height\":600,\"aspectRatio\":1}}" %}

{% embed data="{\"url\":\"https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title\",\"type\":\"link\",\"title\":\"<title>: The Document Title element\",\"description\":\"The HTML Title element \(title\) defines the document\'s title that is shown in a browser\'s title bar or a page\'s tab.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://developer.mozilla.org/static/img/favicon144.e7e21ca263ca.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://developer.mozilla.org/static/img/opengraph-logo.72382e605ce3.png\",\"width\":600,\"height\":600,\"aspectRatio\":1}}" %}

{% embed data="{\"url\":\"https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta\",\"type\":\"link\",\"title\":\"<meta>: The Document-level Metadata element\",\"description\":\"The HTML meta element represents metadata that cannot be represented by other HTML meta-related elements, like base, link, script, style or title.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://developer.mozilla.org/static/img/favicon144.e7e21ca263ca.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://developer.mozilla.org/static/img/opengraph-logo.72382e605ce3.png\",\"width\":600,\"height\":600,\"aspectRatio\":1}}" %}

### The body

| Link |  |
| :--- | :--- |
| [Anatomy of an HTML Document \(MDN\)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started#Anatomy_of_a_HTML_document) |  |

