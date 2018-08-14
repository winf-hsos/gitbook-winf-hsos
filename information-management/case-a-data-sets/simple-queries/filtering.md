---
description: This lesson introduces the where clause to filter data sets.
---

# Filter

## It's all about less rows in the result

We have learned how we can narrow down the result in terms of columns when we introduced the [select statement](select.md). To do that, we simply specify the columns or [expressions ](expressions.md)we want to result set to contain. But what if we want to narrow down the results in terms of rows? Let's look at how we can achieve that!

### What and where

When we selected the columns and expressions fom a table, we asked the question: _What?_ Let's imagine we want the name and the weight, but not for all persons in the data set, but only for those who weigh more than 60 kilograms.  In natural language, we could formulate that request as: "Give me the **name** and the **weight** of a person **who weighs more than 60 kilograms**". We have already learned how to express the first part in SQL: 

```sql
SELECT name, weight FROM person
```

The last part "who weighs more than 60 kilograms" is expressed through the WHERE clause in SQL. In natural language, that would be: "Give me the name \[...\] **where the weight is more than 60 kilograms**." In SQL, we are much more efficient. We eliminate fill words and replace "more than" with the corresponding comparison operator: "**where** ~~the~~ **weight** ~~is more than~~ **&gt; 60** ~~kilograms~~:

```sql
SELECT name, weight FROM person 
WHERE weight > 60
```

It still amazes me how much simpler we can express things in SQL than if we use our natural language.

