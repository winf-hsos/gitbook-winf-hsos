---
description: This lesson introduces the where clause to filter data sets.
---

# Filter

## Less is sometimes more

We learned how we can control the result set in terms of columns when we introduced the [select statement](select.md). To do that, we simply specify the columns or [expressions ](expressions.md)we want in the result set. But what if we want to narrow down the results in terms of rows? Let's look at how we can achieve that!

### A first cut

When we select columns and expressions fom a table, we answer the question: _What information \[about the records\] should the result set contain?_ 

Let's imagine we want the columns `name` , `abv` and `style`, but not for all beers in the data set. Only for those, which contain more than 9% alcohol. In natural language, we could formulate this request as: "Give me the **name,** the **alcohol by volume** and ****the **style** of all beers **that contain more than 9% alcohol**". We have already learned how to express the first part in SQL: 

{% code-tabs %}
{% code-tabs-item title="\#1" %}
```sql
SELECT name, abv, style FROM beers
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We can express the last part "**that contain more than 9% alcohol**" with the _WHERE clause_. In natural language, we would say: "Give me \[...\] **where the alcohol by volume is more than 9%**." SQL is more efficient. It knows no fill words and uses a single character to represent "**more than**": "**where** ~~the~~ **alcohol by volume** ~~is more than~~ **&gt; 60** ~~kilograms~~:

{% code-tabs %}
{% code-tabs-item title="\#2" %}
```sql
-- All craft beers with more than 9% alcohol
SELECT name, abv, style FROM beers
WHERE abv > 0.09
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Analogous to the question _What information should the result set contain?_, the WHERE clause answers the question: _Which records should the result set contain?_

In the example above, we use a WHERE clause with a single condition `abv > 0.09`. However, in most cases, we need more than one filter on more than one column.

### Slice as you like

The previous SQL returns a result set with 84 records. That is, 84 beers in the data set contain more than 9% alcohol. Because we like IPAs, we are only interested in this particular brewing style. From a quick scroll through the result set, we see that the data set distinguishes between different kinds of IPAs. But it seems that all of the styles contain the word "IPA".

We could manually pick all the records from the result set where the style contains "IPA". For 84 rows that is a feasible task. Howevery, query results can often be much bigger, and fortunately, we can do this much easier with SQL:

{% code-tabs %}
{% code-tabs-item title="\#3" %}
```sql
SELECT name, abv, style FROM beers
WHERE abv > 0.09
AND style LIKE '%IPA%'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The first two lines are equal to the statement before, but we added a third line and thereby extended the WHERE clause's set of conditions. Because we used the `AND` keyword, both conditions `abv > 0.09` and `style LIKE '%IPA%'` must be true for any record in the result set. But what does this strange `LIKE` operator do?

As the name suggest, it looks for string values that are _like_ a specific search term. Using the `LIKE` operator, we can look for strings...

* ...at the beginning of a string
* ...at the end of a string
* ...anywhere within a string

In the example above, the `LIKE` condition looks for the word "IPA" anyhwere in the value of the `style` column. This is because we used the `%` symbol, which is a wildcard for any characters. So in natural language, the condition would read: "**Look for the term 'IPA' within the style column. It doesn't matter what comes before or after the term 'IPA'**".

To contrast this, look at this slightly modified statement:

{% code-tabs %}
{% code-tabs-item title="\#4" %}
```sql
SELECT name, abv, style FROM beers
WHERE abv > 0.09
AND style LIKE '%IPA'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

It differs by one character, the `%` after the "IPA". This finds the term "IPA" only at the _end_ of the `style` column. Accordingly, removing the `%` before the "IPA" finds the term only at the _beginning_ of the `style` column.

The `LIKE` operator, in combination with the `%` wildcard character, is a powerful tool for query filters based on string columns. You can combine search terms and wildcards as you need:

{% code-tabs %}
{% code-tabs-item title="\#5" %}
```sql
SELECT name, abv, style FROM beers
WHERE abv > 0.09
AND style LIKE '%American%IPA'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The result includes only beers where the style contains the terms "American" and "IPA", where the latter may only occur at the end of the string. The result will include "American Double / Imperial IPA" and "American IPA", but not "Belgium IPA".

| name | abv | style |
| :--- | :--- | :--- |
| Hop Crisis | 0.09699999999999999 | American Double / Imperial IPA |
| Hemlock Double IPA | 0.095 | American Double / Imperial IPA |
| Bad Axe Imperial IPA | 0.098 | American Double / Imperial IPA |
| ... | ... | ... |
| Better Weather IPA | 0.094 | American IPA |

### Equality 

```sql
SELECT name, abv, style FROM beers
WHERE abv > 0.09
AND style = 'American Double / Imperial IPA'
```

