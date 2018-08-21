# Data Sets

## Comma Separated Values \(CSV\)

### A questionable offer

Punctuation matters. Omitting a comma here or there can completely change the meaning of what we are trying to say or write. There are many funny instances on the web, simply [google](http://bfy.tw/JVRe) "punctuation matters". The picture below shows one I find particularly funny.

![Do you want to join this party?](../../.gitbook/assets/eat_the_pastor.png)

The church is known for many [unsettling acts](https://www.bbc.com/news/world-44209971), but usually they don't make it that public. Or was it just a punctuation error this time?

The example illustrates the role punctuation marks play in separating words and sentences, so that they reflect the intended meaning. Let's cut the church some slack and assume this is what they meant: "**Best sausage supper in St. Louis, come and eat. Pastor Thomas Ressler.**" That sounds better, and we don't have to subscribe to cannibalism to join this party. 

### You gotta keep 'em separated

But what does it have to do with data sets? The answer is simple: When we store data in a file, separating the single parts of a data record is as crucial to understanding the data as proper punctuation is for understanding written prose.

Consider this sample from a craft beer data set, where I removed the comma as the separator symbol \(the original data set is posted on [Kaggle](https://www.kaggle.com/nickhould/craft-cans#beers.csv)\):

{% code-tabs %}
{% code-tabs-item title="craftbeers.csv" %}
```text
1 0.066 2265 Devil's Cup American Pale Ale (APA) 177 12.0
36 0.083 35.0 11 Monk's Blood Belgian Dark Ale 368 12.0
246 0.08 54.0 2639 Dark Star American Stout 8 16.0
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Even if we didn't know the name or anything about the data set, a quick glance tells us this data has something to do with beer. But what _exactly_ does all the information in one line mean? 

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

We added an extra line at the beginning of the file, which contains a comma separated list of words. We call the type of information in the first line **meta data.** Meta data is data about the actual data. Thus, meta data describes the actual data. In this case, it describes the names of the data fields for all the rows in the file.

We now know that each line contains 8 separate data fields, because there are 8 names provided in the first line. Is this enough information to fully understand the data set? Let's find out!

We'll start with the first record, which is now in line 2. With the meta data from the top line, we can try to split the data record into the 8 data fields:

1. `rownum` is **1**.
2. `abv`, which is the alcohol by volume, is **0.066**.
3. `ibu`, which stands for international bitter units, is **2265**. \(_Wait, isn't IBU supposed to be between 0 and 100?_\)
4. `id` is "**Devil's Cup American Pale Ale \(APA\)**". \(_Weird, shouldn't that be an integer number?_\)
5. `name` is "**177**". \(_WTF? That can't be right!\)_
6. `style` is "**12.0**". \(_Ok, something is wrong!_\)
7. `brewery_id` is .... _Ahhh, no more values!_

There are a lot of values that don't seem to fit their field name. Moreover, we are two values short: We can't assign values to the fields `brewery_id` and `ounces`. What's are we missing?

The answer is _separators_. In the approach above, we implicitly applied separators. We _assumed_ that a space between two numbers indicates that these numbers belong to different fields. When we encountered a text value, we _assumed_ that the spaces belong to the text and that the whole text belongs to one data field. It looks like our assumptions were wrong. So let's re-introduce the original separator symbol, in this case the comma:

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

We now see two problems with missing separators:

* Empty values get lost. In the case of the first beer, the value for the field `ibu` is absent. This becomes apparent only if we have a designated separator.
* The end of a text is not properly defined. What we assumed to be the name was actually more than that: The last part "**American Pale Ale \(APA\)**" belongs to the field `style`. Because we use spaces also to separate words in sentences, the space character is not a good choice for a separator symbol. Unless we put text in quotes.

{% hint style="info" %}
CSV stands for comma separated values. Although the comma is often the first choice for a separator symbol, many other symbol are just as good. You'll often see a semicolon or a pipe instead of a comma. As long as we know which symbol separates two data fields, any symbol will do.
{% endhint %}

### Quotation marks

Take the following line from a CSV file and see if you find a problem with it:

{% code-tabs %}
{% code-tabs-item title="wine.csv" %}
```text
id,description,country
1,This is ripe and fruity, a wine that is smooth while still structured.,Portugal
```
{% endcode-tabs-item %}
{% endcode-tabs %}

What happens when we tro to match the data fields in line 2 to the meta data in the first row? The `id` is 1, no problem here. But when we go on to the `description`, we would have interpret the comma after "**This is ripe an fruity**" as a separator symbol, which makes the `country` " **a wine that is smooth while still structured**". Obviously, the `country` should have been "**Portugal**".

The problem is clear: Sentences that contain one or more commas, as in the case of the description above, we need to use an extra marker to indicate the beginning and the end of the text. To solve this issue, we put double quotation marks around the text. Any symbols, including commas, are treated as part of the text. \(Except quotation marks\).

{% code-tabs %}
{% code-tabs-item title="wine.csv" %}
```text
id,description,country
1,"This is ripe and fruity, a wine that is smooth while still structured.",Portugal
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
Some texts may contain quotation marks themselves, which breaks the solution to mark the beginning and end using quotation marks. To solve this, we must precede the quotation marks inside the text with another double quote \([RFC-4180](https://tools.ietf.org/html/rfc4180), paragraph 2.7\). We call this _escaping_ the double quote.
{% endhint %}

## Data granularity

### What does a record represent?

Imagine this scenario: To decide whether to install a traffic light, the city wants to count the number of cars that pass through by an intersection in every hour of the day. They hire students to count and write down the number of cars passed. An example from one day looks like this:

| Day | Starting Hour | Cars |
| :--- | :--- | :--- |
| 2018/01/10 | 9 am | 78 |
| 2018/01/10 | 10 am | 99 |
| 2018/01/10 | 11 am | 81 |
| 2018/01/10 | 12 am | 145 |
| 2018/01/10 | 1 pm | 131 |

Now ask this simple question: Does this data contain all the information we could have gotten about the subject "cars at the intersection"? The answer is no, and to find out why, we can look at what a record represents: One record \(or row\) represents the **sum of cars** that passed through in one hour. The key here is the word "**sum**".

When counting the cars, the students could have noted every single car as its own record. That would mean, instead of only one record for the hour from 9 - 10 am, we'd have 78 records. In that case, the students should have recorded the exact time of the car's passing, and maybe even some more features \(car make, color, type\). The first records could then have looked like this:

| Day | Time | Make | Color |
| :--- | :--- | :--- | :--- |
| 2018/01/10 | 09:01:23 AM | BMW | black |
| 2018/01/10 | 09:01:55 AM | Opel | green |
| 2018/01/10 | 09:03:12 AM | BMW | white |
| 2018/01/10 | 09:03:20 AM | Volkswagen | black |

If we look at both data sets, we can conclude the following:

* A row per car provides us with more information than the one with the sum of cars per hour.
* The data set with a row per car is much bigger than the one with the sum of cars per hour.
* We can easily derive the sum of cars per hour from the data set with the rows per car through **aggregation**. It does not work the other way around.

### Aggregation

Having the data at it finest granularity gives you flexibility of what types of analysis you can do with the data. Take the car count example from above: What if the city found out they needed not the sum per hour, but the sum for every minute in order to decide on the length of the green phases? With the data set containing one row per hour, this would be impossible to do. The city would need to start counting all over again, this time using the finest granularity possible: one row per car. From there, they could aggregate and count the cars for any time interval they needed.

And not just that. Having more attributes in the data set \(car make, color\), aggregations along any combination of these dimensions become possible \(e.g. cars per hour per car make\).

{% hint style="info" %}
Aggregating data always results in less or an equal number of rows.
{% endhint %}

### Single values

## Data types

![](../../.gitbook/assets/puzzle%20%281%29.jpg)

### A standard format for dates

Imagine the following situation: You are on the phone with your insurance company, and to make sure you are who you claim to be, the clerk asks for your day of birth. Given you are in Germany, you don't have to think long about what pieces of information the clerk expects to hear \(day, month, year\), and in which order. In Germany, we always write down the day of birth in this form: day of month as a two digit number, followed by a period, month of the year as a two digit number, followed by period, and finally, the year as a four digit number. For example: **13.09.1981**, which is my day of birth in this format. More general, we can describe the format as **dd.mm.yyyy.** 

This is not the case for all countries. If you were in the United States, you'd write the same date as **09/13/1981**, and the general format would be **mm/dd/yyyy**. Other countries may have even different formats.

Your day of birth is actually a special case of a more general class of information: A date. We use this agreed upon format not only for birthdays, but for any date we write down. The same is true for the context of IT systems, and especially for databases. Here, we store dates in an agreed upon format, and we assign it the data type `date`.

### Less specific data types

#### Strings

A date is _one_ of many data types. It is quite specific, and it is composed of more general data types. For example, a date can also be viewed as a series of characters \(**"13.09.1981"** = numbers plus punctuation marks\). For a date, these characters just happen to follow a certain syntax, and that makes it fit the data type `date`. We can also store a series of characters that don't follow a specific syntax, then we call this data type a `string`. In a `string`, we can store any number of arbitrary characters, no syntax required. However, most often we use the `string` data type to store things that _do_ follow a syntax: words, sentences, or whole texts.

#### Numbers

We could also choose this view on the structure of the date: It is composed of 3 numbers, connected by two periods. We know that the day, month and year cannot be any arbitrary sequence of characters, but it can only be a subset of it: integer numbers, i.e. numbers without a decimal place. There we have our next data type: `integer`. And in case we need decimal places, the right data types are `float` or `double`.

{% hint style="info" %}
A `double` value is more precise, that is, it can store more decimal places. Read [here ](http://www.ilikebigbits.com/2017_06_01_float_or_double.html)for a nice comparison between `float` and `double`.
{% endhint %}

The following table gives some typical examples of numbers and their data types:

| Number | Type | Precision |
| :--- | :--- | :--- |
| Age in years | `integer` | - |
| Day of year | `integer` | - |
| Running ID in a table | `integer` | - |
| Salary, price, turnover \(anything money related\) | `float` | 2 decimal places for cents |
| Pi | `double` | As many as possible |
| Temperature, humidity \(any sensor values\) | `double` | As many as needed for application |

**Truth values**

Consider another scenario: You are at your physician's waiting room. In order make a good diagnosis, the physician requested you to fill out a short survery about your diet and habits. One question is: "Do you smoke?". There are only two possible answers to this question: "Yes" or "No". You either smoke, or you don't. In other words, the statement "Mr. XYZ smokes!" is either **true** or **false.** A value that can either be true or false is called a **boolean value**. We can store theses kinds of values using the data type `boolean`.

We can combine truth values with boolean operators. The result of such an operation is also a boolean value. For example, consider the statement "Mr. XYZ smokes **AND** drinks alcolhol at least once a day". Depending on the truth value of each single statement and the operator we apply, we get different results:

| Smokes | Drinks | Boolean Operator | Result |
| :--- | :--- | :--- | :--- |
| true | true | AND | true |
| true | false | AND | false |
| true | false | OR | true |
| true | true | XOR | false |

The AND operator requires both sides to be true, otherwise the result is false \(lines 1 and 2\). The OR operator requires at least one side to be true, but both are also possible \(line 3\). In contrast, the XOR requires one, and only one, side to be true. When both are true, the result of an XOR operation is false \(last line\).

### **Compatibility**

## Representations of data

## References

* [Float or double?](http://www.ilikebigbits.com/2017_06_01_float_or_double.html)
* [Common Format and MIME Type for CSV Files \(RFC 4180\)](https://tools.ietf.org/html/rfc4180)



