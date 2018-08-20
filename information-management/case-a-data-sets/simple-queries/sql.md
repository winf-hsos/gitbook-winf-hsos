# SQL

## Why SQL?

### SQL was designed to empower the normal user

The following is an excerpt from the [Microsoft SQL Server Reference](https://docs.microsoft.com/en-us/sql/odbc/reference/structured-query-language-sql?view=sql-server-2017) and gives a great introduction to the topic:

> A typical DBMS allows users to store, access, and modify data in an organized, efficient way. Originally, the users of DBMSs were programmers. Accessing the stored data required writing a program in a programming language such as COBOL. While these programs were often written to present a friendly interface to a nontechnical user, access to the data itself required the services of a knowledgeable programmer. Casual access to the data was not practical.
>
> Users were not entirely happy with this situation. While they could access data, it often required convincing a DBMS programmer to write special software. For example, if a sales department wanted to see the total sales in the previous month by each of its salespeople and wanted this information ranked in order by each salesperson's length of service in the company, it had two choices: Either a program already existed that allowed the information to be accessed in exactly this way, or the department had to ask a programmer to write such a program. In many cases, this was more work than it was worth, and it was always an expensive solution for one-time, or ad hoc, inquiries. As more and more users wanted easy access, this problem grew larger and larger.
>
> Allowing users to access data on an ad hoc basis required giving them **a language in which to express their requests**. A single request to a database is defined as a query; such a language is called a query language. Many query languages were developed for this purpose, **but one of these became the most popular: Structured Query Language**, invented at IBM in the 1970s. It is more commonly known by its acronym, SQL, and is pronounced both as "ess-cue-ell" and as "sequel". SQL became an ANSI standard in 1986 and an ISO standard in 1987; it is used today in a great many database management systems.

There are many key points made in the excerpt. An important one is that SQL is designed for the normal _users_, and not the programmers. Its original goal was to enable users to access databases and thereby satisfy their information requirements more easily, without the need for the IT department's resources.

### SQL requires structured data

SQL is most strongly associated with relational databases. This what is was orinally developed for. In fact, SQL requires structured data \([as does any data you want to analyze](https://medium.com/@hjalli/there-is-no-unstructured-data-in-analytics-8c5d06944b23)\), and the relational database is the best example for a highly structured database. However, if a database does not rely on the relational model, it doesn't mean the data in it isn't structured. In fact, there is no way at all to query unstructured data. What would you even be querying for? Even for unstructured \(or semi-structured\) data such as images, we must project some structure \(or schema\) onto the data when we want to query it. And once we have a schema, we can use SQL again.

## The power of SQL

### Query data

SQL is most famous for its power to _query_ strucutred data. The means to do that is the popular _select_ command. Selecting data with this command is at the core of what we do with SQL in our courses. For most scenarios, we assume the structure and content of the data is given. We only want to _get_ the data we need from the given data set. This can be tricky, but it requires only the select command.

### Manipulate data

To change a data set's content, we can use a specific set of SQL's commands. This part of SQL is referred to as the SQL _Data Manipulation Language \(DML\)._ It allows us to perform operations that manipulate the data:

* Delete data records
* Update data records, such as specific column \(or fields\) values
* Add new data records

### Define data

Before we can do anything useful with data, we must define a structure for it. That is especially true for relational databases, where the upfront definition of a static schema is a requirement. A typical description of the data structure includes the tables, the relationships among them, the table's columns as well as the column's data types. SQL's _Data Definition Language \(DDL\)_ allows us to do that. With DDL, we can \(among other operations\):

* Define and create databases
* Create tables
* Define a table's columns \(name, key constraints, data type\)
* Manifest relationships between tables
* Invoke constraints, such as _non-null_ or a maximum length of strings

### Run procedures

We do not consider this part of the core SQL standard, but in most databases, it is possible to write procedures that can be executed either manually or based on triggers. For the definition of such procedures, the SQL language is usually extended to the functionality of a full programming language. Popular examples include [Microsoft's T-SQL](https://docs.microsoft.com/de-de/sql/t-sql/language-reference) or [Oracle's PL/SQL](http://www.oracle.com/technetwork/database/features/plsql/index.html).

{% hint style="info" %}
Note that **SQL is not a programming language**, despite the fact that many database vendors have extended SQL to include the functionality of a programming language \(e.g. T-SQL, PL/SQL\).
{% endhint %}

## References

* "[Why SQL is beating NoSQL, and what this means for the future of data](https://blog.timescale.com/why-sql-beating-nosql-what-this-means-for-future-of-data-time-series-database-348b777b847a)" 
* "[Early History of SQL](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6359709&tag=1)" in  the IEEE Annals of the History of Computing 2012

