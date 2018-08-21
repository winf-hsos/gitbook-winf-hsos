# Data Sets

## Data formats

### Comma Separated Values \(CSV\)

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
* We can easily derive the sum of cars per hour from the data set with the rows per car  through **aggregation**. It does not work the other way around.

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

Imagine the following situation: You are on the phone with your insurance company, and to make you sure you are actually who you claim to be, the clerk asks for your day of birth. Given you are in Germany, you wouldn't have to think long about what information the clerk expects to receive \(day, month, year\), and in which order. In Germany, we always write down the day of birth in this form: day of month as a two digit number, followed by a period, month of the year as a two digit number, followed by period, and finally, the year as a four digit number. For example: **13.09.1981**, which is my day of birth in this format. More general, we can describe the format as **dd.mm.yyyy.** If you were in the United States, you'd write the same date as **09/13/1981**, and the general format would be **mm/dd/yyyy**.

Your day of birth is actually a special case of a more general class of information: A date. We use this agreed upon format not only for birthdays, but for any date when we write it down. The same is true for the IT context, and especially for databases. Here, we store dates in an agreed upon format, and we assign it the data type `date`.

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



