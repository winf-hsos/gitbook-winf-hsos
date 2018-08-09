# Expressions

## More than column names

The general syntax above suggests that we can only put in column names for the first and table names for the second placeholder. This is not the whole truth.

### Literal values

Instead of column names, we can select anything that represents a value. That means basically anything that we could fit into a column. Consider the example below:

```sql
SELECT 1 FROM person
```

What do you think the result would be? We are asking for a "1" from the table person. But when we run the query, we don't get only one "1", but instead we get 3! Why is that?

The explanation is simple: We get one "1" for every row in the table person. And as we have seen before, the table has three rows. Because there is no column with the name "1" in the table _person_, SQL interprets the "1" as a  **literal value** and returns a new column with the value 1 for each row in the table. 

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

We can also mix both literal values \(or expressions\) and column names as we like:

```sql
SELECT 2018 as year, name FROM person
```

Imagine we want to save the result, and we want to add the `year` column to remember the year this report was created. This is the result:

![](../../../.gitbook/assets/result_mixed.png)

{% hint style="success" %}
You can try the example above on [SQL Fiddle](http://sqlfiddle.com/#!18/8c7c4/3)!
{% endhint %}

### Expressions

Another type of value we can select is an **expression**. An expression can be a function or a formula, anything that represents a value. A literal value is therefore a special case of an expression.

Typical expressions include arithmetic operations:

```sql
SELECT weight / height as relativeWeight FROM person
```

The above expression `weight / height` calculates a mesaure that puts the two attributes into relation. The more you weigh, the bigger the number, the taller you are, the smaller the number. As with literal values, we can combine column names and expressions in a single select statement:

```sql
SELECT name, weight / height as relativeWeight FROM person
```

This is the result:

![](../../../.gitbook/assets/result_expression.png)

{% hint style="success" %}
You can try the example above on [SQL Fiddle](http://sqlfiddle.com/#!18/8c7c4/4)!
{% endhint %}

