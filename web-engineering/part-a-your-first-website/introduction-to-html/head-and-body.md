# Head and Body

## The head

The head contains metadata about the website. Nothing that is placed in the head is visible on the website. Among other elements, the `<head>` tag contains the `<title>` tag and at least one `<meta>` tag.

### The &lt;title&gt; tag

The value of the `<title>` tag defines the title of the website, which is displayed in the browser window bar \(or tab\).

### The &lt;meta&gt; tag

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

## The body

The body is where the visible part of your website lives. The following sections cover tags and their attributes that allow you to describe the structure and the visible elements of your website.



