---
description: This lesson introduces expressions in SQL statements.
---

# Expressions

## Not just column names

The general syntax of the SQL statement suggests that we can only use column names for the first, and table names for the second placeholder. This is not the whole truth. We can also use expressions, which is a very powerful concept that we'll explore in this section.

An expression represents a value and can contain a combination of the following elements:

* Literal values
* Operators \(arithmetic, boolean\)
* Functions
* Columns

Moreover, an expression can also be a subquery that returns a \(single\) value. We'll cover subqueries [later](../../challenge-1-sales-data-analysis/advanced-queries/subqueries.md).

## Literal values

### Literal values for different data types

Instead of column names, we can select anything that represents a value. That means basically anything that we could fit into a column. Consider the example below:

```sql
SELECT 1 FROM person
```

What do you think the result would be? We are asking for a "1" from the table person. But when we run the query, we don't get only one "1", but instead we get 3! Why is that?

The explanation is simple: We get one "1" for every row in the table person. And as we have seen before, the table has three rows. Because there is no column with the name "1" in the table _person_, SQL interprets the "1" as a **literal value** and returns a new column with the value 1 for each row in the table.

In the example above, the new column does not have a name. We can assign a name easily:

```sql
SELECT 1 AS newCol FROM person
```

Now, the new column in the result set will be named `newCol`.

![](../../../.gitbook/assets/result_with_new_colum.png)

It doesn't have to be numbers, you can select literal values of any data type:

```sql
SELECT 'Hello World' as newStringCol FROM person;
SELECT true as newBooleanCol FROM person;
SELECT 0.5 as newDoubleCol FROM person;
```

{% hint style="success" %}
You can try the example above on [SQL Fiddle](http://sqlfiddle.com/#!18/8c7c4/2)!
{% endhint %}

{% hint style="info" %}
Note that the new columns won't be created in the source table when we select literal values. The new column will only exist in the result set, which is effectively also a table. A select statement can neither change the structure of an existing table, nor can it change the data in it.
{% endhint %}

### Literals values and columns mixed

We can also mix both literal values, expressions, and column names as we like:

```sql
SELECT 2018 as year, name FROM person
```

Imagine we want to save the result, and we want to add the `year` column to remember the year this report was created. This is the result:

![](../../../.gitbook/assets/result_mixed.png)

{% hint style="success" %}
You can try the example above on [SQL Fiddle](http://sqlfiddle.com/#!18/8c7c4/3)!
{% endhint %}

## Formulas

A literal value is a special case of an expression. Besides literal values, an expression be \(or contain\) a formula or a function. Any mix of the 3 types is possible as well.

### Arithmetic

Formulas are either arithmetic, i.e. they represent a number, or boolean, i.e. they represent a truth value. Look at the following line as an example for an arithmetic expression:

```sql
SELECT weight / height as relativeWeight FROM person
```

The expression `weight / height` calculates a mesaure that puts the two attributes into relation. The more you weigh, the bigger the number, the taller you are, the smaller the number. As with literal values, we can combine column names and expressions in a single statement:

```sql
SELECT name, weight / height as relativeWeight FROM person
```

This is the result:

![](../../../.gitbook/assets/result_expression.png)

{% hint style="success" %}
You can try the example above on [SQL Fiddle](http://sqlfiddle.com/#!18/8c7c4/4)!
{% endhint %}

Accordingly, we can use any other arithmetic operator to perform calculations. Try the following statements:

```sql
SELECT weight - 10 as reducedWeight FROM person;
SELECT weight + 10 as increasedWeight FROM person;
SELECT weight * 2 as doubledWeight FROM person;
SELECT weight % 10 as moduloTenWeight FROM person;
```

{% hint style="warning" %}
Arithmetic operators expect values of a numerical data type \(`integer`, `double`\). If you accidently specify the wrong column, i.e. one of the type `string`, you'll get unexpected results or even an error.
{% endhint %}

### Boolean

A booelan expression represents either `true` or `false`. Comparing two values \(or expressions\) is a typical scenario for a boolean expression. We can use the common operators:

```sql
SELECT 1 == 2 as alwaysFalse FROM person;
SELECT 1 == 1 as alwaysTrue FROM person;
SELECT weight > 60 as weighsMoreThan60 FROM person;
SELECT height <= 180 as isSmallerOrEqual180 FROM person;
SELECT name <> 'Horst' as notHorst FROM person;
```

## Functions

Functions can be invoked by their name and perform different tasks. In the end, every function represents a certain value. There are different types of functions in SQL, each type covers a set of scenarios:

* Math functions
* String functions
* Date & time functions
* Aggregation functions
* Window functions

Functions play a huge role in SQL, that's why we devote a separate section to date/time, aggregation and window functions. In the following, we'll introduce functions with simple math and string operations.

### Math

Much of the calculations we need are covered by the arithmetic operators. However, there are some math functions that we'll use quite often:

```sql
SELECT sqrt(weight) as squareRootOfWeight FROM person;
SELECT pow(weight, 3) as weightToThe3 FROM person;
SELECT pow(weight, 1/3) as thirdRootOfWeight FROM person;

SELECT 
  sin(height) as sinusHeight 
 ,cos(height) as cosinusHeight
 ,tan(height) as tanHeight
FROM person;
```

### String

When we are analyzing text, we need a special set of functions that deal with columns of the `string` data type. Here are some examples we might encounter:

```sql
SELECT length(name) as numberCharactersInName FROM person;
SELECT substr(0, 10, name) as first10Letters FROM person;
SELECT trim(name) as strippedSpaces FROM person;
```





