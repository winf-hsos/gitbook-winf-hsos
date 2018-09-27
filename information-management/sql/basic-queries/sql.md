# SQL

## Why SQL?

### Empower the normal user

The following is an excerpt from the [Microsoft SQL Server Reference](https://docs.microsoft.com/en-us/sql/odbc/reference/structured-query-language-sql?view=sql-server-2017) and gives a great introduction to the topic:

> A typical DBMS allows users to store, access, and modify data in an organized, efficient way. Originally, the users of DBMSs were programmers. Accessing the stored data required writing a program in a programming language such as COBOL. While these programs were often written to present a friendly interface to a nontechnical user, access to the data itself required the services of a knowledgeable programmer. Casual access to the data was not practical.
>
> Users were not entirely happy with this situation. While they could access data, it often required convincing a DBMS programmer to write special software. For example, if a sales department wanted to see the total sales in the previous month by each of its salespeople and wanted this information ranked in order by each salesperson's length of service in the company, it had two choices: Either a program already existed that allowed the information to be accessed in exactly this way, or the department had to ask a programmer to write such a program. In many cases, this was more work than it was worth, and it was always an expensive solution for one-time, or ad hoc, inquiries. As more and more users wanted easy access, this problem grew larger and larger.
>
> Allowing users to access data on an ad hoc basis required giving them **a language in which to express their requests**. A single request to a database is defined as a query; such a language is called a query language. Many query languages were developed for this purpose, **but one of these became the most popular: Structured Query Language**, invented at IBM in the 1970s. It is more commonly known by its acronym, SQL, and is pronounced both as "ess-cue-ell" and as "sequel". SQL became an ANSI standard in 1986 and an ISO standard in 1987; it is used today in a great many database management systems.

There are many key points made in the excerpt. An important one is that SQL is designed for the normal _users_, and not the programmers. Its original goal was to enable users to access databases and thereby satisfy their information requirements more easily, without the need for the IT department's resources. 

Donald Chamberlin underlines this view on SQL in his paper [Early History of SQL](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6359709&tag=1):

> \[..\] we believed that it should be possible to design a relational language that would be more accessible to users without formal training in mathematics or computer programming.

### No structure, no query

SQL is most strongly associated with relational databases. Unsurprisingly, as it was originally developed for them. In fact, SQL requires structured data \([as does any data you want to analyze](https://medium.com/@hjalli/there-is-no-unstructured-data-in-analytics-8c5d06944b23)\), and the relational database is the best example for a highly structured database. 

However, if a database does not rely on the relational model, it doesn't mean the data in it isn't structured. In fact, there is no way at all to query unstructured data. What would you even be querying for? Even for unstructured \(or semi-structured\) data such as images, we must project some structure \(or schema\) onto the data when we want to query it. And once we have a schema, we can use SQL again.

### Lingua franca for data analysis

> We believe that SQL has become the universal interface for data analysis. \([source](https://blog.timescale.com/why-sql-beating-nosql-what-this-means-for-future-of-data-time-series-database-348b777b847a)\)

## The power of SQL

### Query data

SQL is popular for its power to _query_ structured data. The means to do that is the popular _select_ command. Selecting data with this command is at the core of what we do with SQL in our courses. For most scenarios, we assume the structure and content of the data is given. We only want to _get_ the data we need from the given data set \(or table\). This can be tricky, but it requires only the select command.

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

* [Why SQL is beating NoSQL, and what this means for the future of data](https://blog.timescale.com/why-sql-beating-nosql-what-this-means-for-future-of-data-time-series-database-348b777b847a)
* [There is no unstructured data in analytics](https://medium.com/@hjalli/there-is-no-unstructured-data-in-analytics-8c5d06944b23)
* [Early History of SQL](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6359709&tag=1) in  the IEEE Annals of the History of Computing 2012

### Videos

Watch the following video from 00:28:54 until 00:45:32 to get a vivid introduction to why we need databases and what SQL is:

{% embed data="{\"url\":\"https://www.youtube.com/watch?v=MaqfxpCBMJI&t=1736s\",\"type\":\"video\",\"title\":\"CS50 2017 - Lecture 10 - SQL\",\"description\":\"00:00:00 - Muppet Teaser\\n00:03:02 - eprint\\n00:05:07 - Facebook Login Walkthrough\\n00:14:34 - Flask Sessions\\n00:28:56 - SQL\\n00:29:44 - Databases\\n00:36:55 - SQLite\\n00:39:01 - Database Operations\\n00:45:32 - SQL Data Types\\n00:54:33 - Optimizing the Database\\n01:06:13 - phpLiteAdmin\\n01:12:42 - Constraints\\n01:18:01 - Creating a Database\\n01:21:58 - sqlite3\\n01:25:14 - SQL in Python\\n01:33:15 - SQL Injection Attacks\\n01:38:50 - Adding SQL to Flask\\n01:43:31 - C$50 Finance\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.youtube.com/yts/img/favicon\_144-vfliLAfaB.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://i.ytimg.com/vi/MaqfxpCBMJI/maxresdefault.jpg\",\"width\":1280,\"height\":720,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"player\",\"url\":\"https://www.youtube.com/embed/MaqfxpCBMJI?rel=0&showinfo=0&start=1736\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://www.youtube.com/embed/MaqfxpCBMJI?rel=0&amp;showinfo=0&amp;start=1736\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778},\"caption\":\"David J. Malan from Harvard on Databases & SQL\"}" %}

