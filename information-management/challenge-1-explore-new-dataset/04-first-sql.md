---
description: >-
  In this lesson, you'll write your first SQL statements and start querying some
  data.
---

# 06 - First SQL

## De facto standard for querying databases

SQL has been developed to query relational databases. This happened in the late seventies, when the first commercial relational databases came to market. Even today, more than thirty years later, SQL has sustained its dominant role as a de facto standard for querying databases.

With the arrival of new types of databases, such as document oriented databases, new ways to query them were required as well. And in fact, new languages were developed for these new types of databases. However, almost all databases today are designed to still understand SQL, even though they do not adhere to the relational model. Because of SQL's ubiquity, users are so familiar with SQL that it makes great sense from an acceptance perspective to implement an interface for SQL in any database product.

If a database does not rely on the relational model, this doesn't mean the data isn't in some way structured. In fact, there is no way to query unstructured data - what would you even be querying for? Even for unstructured \(or semi-structured\) data such as images, we must project some structure \(or schema\) onto the data when we want to query it. \(This is called [schema-on-read](../scenario-d-big-data-analysis/31-semi-structured-data.md)\). And once we a schema, we can use SQL.

## Date and time

Data and time values are important in many analytic scenarios. We often want to know when something happened, or how often an event occured happened during a particular time window. Some examples:

* How many item have we sold **today**?
* How many **yesterday**? Or the **same day the year before**?
* How many mentions on Twitter did we get in the **last hour**?
* **How long** since we last sold this product?

```sql
%sql
select 
    date
   ,to_date(CAST(UNIX_TIMESTAMP(date, 'MM/dd/yyyy hh:mm:ss a') AS TIMESTAMP))
   ,year(TO_DATE(CAST(UNIX_TIMESTAMP(date, 'MM/dd/yyyy hh:mm:ss a') AS TIMESTAMP)))
   ,hour(CAST(UNIX_TIMESTAMP(date, 'MM/dd/yyyy hh:mm:ss a') AS TIMESTAMP))
from crimes
```

## Quiz

Take the following quiz to check if you understand the basics of this lesson.

* [SQL Introduction Quiz](https://goo.gl/forms/xM9FjAZPkTaYiFLp2)

