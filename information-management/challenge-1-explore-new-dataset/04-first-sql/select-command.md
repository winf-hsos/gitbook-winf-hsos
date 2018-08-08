---
description: This lesson introduces the select statement for querying data.
---

# Select

## Close to how we speak

If you could talk to a database and ask for specific data, how would you formulate your reuqest? Engineers at IBM in the 1970s have probably asked themselves the very same question. And the result was the SQL select statement.

One idea behind the select statement is that users should write queries similar to how they would formulate the query in the English language. Consider we have a data set \(or table\) called _person_ with 3 columns and 5 rows:

![](../../../.gitbook/assets/person_table%20%281%29.png)

Given this simple table, how would you formulate a request to get only the name and height of each person \(not the weight\)? You would probably say something like _"_**Give me only the name and height of each person, please"**_,_ right?

Let's consider the table more as set with elements \(rows\) and properties which we can choose _from_. We could then formulate it as "**I'd like to choose the name and the height from the person set**". That's very close to what it would look like in SQL. We only have to replace the verb "choose" with "select" and remove some fill words: "~~I'd like to~~ **select** ~~the~~ **name** ~~and the~~ **height from** ~~the~~ **person** ~~set~~". Instead of "and" we put a comma, and we have our first working select statement:

```sql
SELECT name, height FROM person
```

If we execute this statement against the database, the result looks like this:

![](../../../.gitbook/assets/result_simple_select.png)

That was easy, right? And so far quite intuitive and close to how we naturally speak. The good news is: The rest of the select statement's vocabulary follows the same rule of staying close to how we speak. That makes small and less complex queries very easy to read. The bad news: Once we arrive at certain complexity, SQL statements can become large and very hard to read, despite the fact that it is at its core close to how we naturally speak. We'll find ways to deal with that later when we get there.

{% hint style="info" %}
Note that the example above is oversimplified, but serves the purpose of showing the concepts of the select statement. The exercise of selecting 2 out of 3 columns may seem pointless in this scenario. But keep in mind that in a real world data set, the number of columns can span between 10 - 100 or even more. Here, selecting only what you need becomes essential.
{% endhint %}

