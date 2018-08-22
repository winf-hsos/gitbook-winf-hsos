---
description: This lesson introduces the where clause to filter data sets.
---

# Filter

## Less is sometimes more

We learned how we can control the result set in terms of columns when we introduced the [select statement](select.md). To do that, we simply specify the columns or [expressions ](expressions.md)we want to result set to contain. But what if we want to narrow down the results in terms of rows? Let's look at how we can achieve that!

### A first cut

When we select columns and expressions fom a table, we asked the question: _What information \[about the records\] should the result set contain?_ 

Let's imagine we want the columns `name` , `abv` and `style`, but not for all beers in the data set. Only for those, which contain more than 9% alcohol. In natural language, we could formulate this request as: "Give me the **name,** the **alcohol by volume** and ****the **style** of all beers **that contain more than 9% alcohol**". We have already learned how to express the first part in SQL: 

```sql
SELECT name, abv, style FROM beers
```

We can express the last part "**that contain more than 9% alcohol**" with the _WHERE clause_. In natural language, we would say: "Give me \[...\] **where the alcohol by volume is more than 9%**." SQL is more efficient. It knows no fill words and uses a single character to represent "**more than**": "**where** ~~the~~ **alcohol by volume** ~~is more than~~ **&gt; 60** ~~kilograms~~:

```sql
-- All craft beers with more than 9% alcohol
SELECT name, abv, style FROM beers
WHERE abv > 0.09
```

Analogous to the question _What information should the result set contain?_, the WHERE clause answers the question: _Which records should the result set contain?_

In the example above, we use a WHERE clause with a single condition `abv > 0.09`. However, in most cases, we need more than one filter on more than one column.

### Slice as you like

The previous SQL returns a result set with 84 records. That is, 84 beers in the data set contain more than 9% alcohol. Because we like IPAs, we are only interested in this particular brewing style. We could manually pick all the records from the result set where the style indicates that is an IPA. But fortunately, we can do this much easier with SQL:

```sql
SELECT name, abv, style FROM beers
WHERE abv > 0.09
AND style = 'American Double / Imperial IPA'
```

The first two lines are equal to the statement before, but we added a third line and thereby extended the WHERE clause's set of conditions. Because we used the AND keyword, both conditions `abv > 0.09` and `style = 'American Double / Imperial IPA'` must be true for any record in the result set. It turns out that of the 84 beers with more than 9% alcohol, 33 are IPAs.

### The LIKE operator



