# Data Formats

## Comma Separated Values \(CSV\)

### A questionable offer

Punctuation matters. Omitting a comma here or there can completely change the meaning of what we write. There are many funny instances on the web, simply [google](http://bfy.tw/JVRe) "punctuation matters". The picture below shows one I find particularly funny.

![Do you want to join this party?](../../../.gitbook/assets/eat_the_pastor.png)

The church is known for many [unsettling acts](https://www.bbc.com/news/world-44209971), but usually they don't make it that public. Or was it just a punctuation error this time?

The example illustrates the role punctuation marks play in separating words and sentences, so that they reflect the intended meaning. Let's cut the church some slack and assume this is what they meant: "**Best sausage supper in St. Louis, come and eat. Pastor Thomas Ressler.**" That sounds better, and we don't have to subscribe to cannibalism to join this party. 

### You gotta keep 'em separated

But what does it have to do with data sets? The answer is simple: When we store data in a file, separating the single parts of a data record is as crucial to understanding the data as proper punctuation is for understanding written prose.

Consider this sample from a craft beer data set, where I removed the comma as the separator symbol, which we will call _delimiter_ \(the original data set is posted on [Kaggle](https://www.kaggle.com/nickhould/craft-cans#beers.csv)\):

{% code-tabs %}
{% code-tabs-item title="craftbeers.csv" %}
```text
1 0.066 2265 Devil's Cup American Pale Ale (APA) 177 12.0
36 0.083 35.0 11 Monk's Blood Belgian Dark Ale 368 12.0
246 0.08 54.0 2639 Dark Star American Stout 8 16.0
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Even if we didn't know the name or anything else about the data set, a quick glance tells us this data has something to do with beer. But what _exactly_ does all the information in one line mean? 

We can guess that the words "**Devil's Cup American Pale Ale \(APA\)**", "**Monk's Blood Belgian Dark Ale**", and "**Dark Star American Stout**" are the names of each beer. But what about all the weird numbers before and after that? With only the information above, there is no way we can understand the meaning all the numbers. Luckily, the original file provides more information in its first row:

{% code-tabs %}
{% code-tabs-item title="craftbeers.csv" %}
```text
rownum,abv,ibu,id,name,style,brewery_id,ounces
1 0.066 2265 Devil's Cup American Pale Ale (APA) 177 12.0
36 0.083 35.0 11 Monk's Blood Belgian Dark Ale 368 12.0
246 0.08 54.0 2639 Dark Star American Stout 8 16.0
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We added an extra line at the beginning of the file, which contains a comma separated list of words. We call the type of information in the first line _meta data_**.** Meta data is data about the actual data, i.e. meta data describes the actual data. In this case, it describes the names of the data fields for all the rows in the file.

We now know that each line contains 8 separate data fields, because there are 8 names provided in the first line. Is this enough information to fully understand the data set? Let's find out!

We'll start with the first record, which is now in line 2. With the meta data from the top line, we can try to split the data record into the 8 data fields:

1. `rownum` is **1**.
2. `abv`, which is the alcohol by volume, is **0.066**.
3. `ibu`, which stands for international bitter units, is **2265**. \(_Wait, isn't IBU supposed to be between 0 and 100?_\)
4. `id` is "**Devil's Cup American Pale Ale \(APA\)**". \(_Weird, shouldn't that be an integer number?_\)
5. `name` is "**177**". \(_WTF? That can't be right!\)_
6. `style` is "**12.0**". \(_Ok, something is wrong!_\)
7. `brewery_id` is .... _Ahhh, no more values!_

There are four values that don't seem to fit their field name. Moreover, we are two values short: We can't assign values to the fields `brewery_id` and `ounces`. What's are we missing?

The answer is _delimiters_. In the approach above, we implicitly applied delimiters. We _assumed_ that a space between two numbers indicates that these numbers belong to different fields. When we encountered a text value, we _assumed_ that the spaces belong to the text and that the whole text belongs to one data field. It looks like our assumptions were wrong after all. So let's re-introduce the original delimiter, in this case the comma:

{% code-tabs %}
{% code-tabs-item title="craftbeers.csv" %}
```text
rownum,abv,ibu,id,name,style,brewery_id,ounces
1,0.066,,2265,Devil's Cup,American Pale Ale (APA),177,12.0
36,0.083,35.0,11,Monk's Blood,Belgian Dark Ale,368,12.0
246,0.08,54.0,2639,Dark Star,American Stout,8,16.0
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We now see two problems with missing delimiters:

* Empty values get lost. In the case of the first beer, the value for the field `ibu` is absent. This becomes apparent only if we have a designated delimiter.
* The end of a text is not properly defined. What we assumed to be the name was actually more than that: The last part "**American Pale Ale \(APA\)**" belongs to the field `style`. Because we use spaces also to separate words in sentences, the space character is not a good choice for a delimiter. Unless we put the text in quotes.

{% hint style="info" %}
CSV stands for comma separated values. Although the comma is often the first choice for a delimiter, other symbols are just as good. You'll often see a semicolon or a pipe instead of a comma. Invisible characters, such as TAB, are also quite popular. \(There is even a file extension `.tsv`\). As long as we know which symbol separates two data fields, any symbol will do.
{% endhint %}

### Quotation marks

Take the following line from a CSV file and see if you can spot the problem:

{% code-tabs %}
{% code-tabs-item title="wine.csv" %}
```text
id,description,country
1,This is ripe and fruity, a wine that is smooth while still structured.,Portugal
```
{% endcode-tabs-item %}
{% endcode-tabs %}

What happens when we tro to match the data fields in line 2 with the meta data in the first row? The `id` is 1, no problem here. But when we go on to the `description`, we would have interpret the comma after "**This is ripe an fruity**" as a delimiter, which makes the `country` " **a wine that is smooth while still structured**". Obviously, the `country` should have been "**Portugal**".

The problem is clear: For sentences that contain one or more commas, as in the case of the description above, we need to use an extra marker to indicate the beginning and the end of the text. To solve this issue, we put double quotation marks around the text. Any symbols, including commas, are treated as part of the text. \(Except quotation marks\).

{% code-tabs %}
{% code-tabs-item title="wine.csv" %}
```text
id,description,country
1,"This is ripe and fruity, a wine that is smooth while still structured.",Portugal
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
Some texts may contain quotation marks themselves, which breaks the solution to mark the beginning and end using quotation marks. To solve this, we must precede the quotation marks inside the text with another quotation mark \([RFC-4180](https://tools.ietf.org/html/rfc4180), paragraph 2.7\). We call this _escaping_ the double quote.
{% endhint %}

## JSON

## References

* [Common Format and MIME Type for CSV Files \(RFC 4180\)](https://tools.ietf.org/html/rfc4180)

