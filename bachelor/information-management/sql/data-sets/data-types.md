# Data Types

## Data types

![](../../../.gitbook/assets/puzzle%20%281%29.jpg)

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

## References

| Title and Link | Type |
| :--- | :--- |
| [Float or double?](http://www.ilikebigbits.com/2017_06_01_float_or_double.html) | Additional information |
