# SQL

## Why SQL?

The following is an excerpt from the [Microsoft SQL Server Reference](https://docs.microsoft.com/en-us/sql/odbc/reference/structured-query-language-sql?view=sql-server-2017) and gives a great introduction to the topic:

> A typical DBMS allows users to store, access, and modify data in an organized, efficient way. Originally, the users of DBMSs were programmers. Accessing the stored data required writing a program in a programming language such as COBOL. While these programs were often written to present a friendly interface to a nontechnical user, access to the data itself required the services of a knowledgeable programmer. Casual access to the data was not practical.
>
> Users were not entirely happy with this situation. While they could access data, it often required convincing a DBMS programmer to write special software. For example, if a sales department wanted to see the total sales in the previous month by each of its salespeople and wanted this information ranked in order by each salesperson's length of service in the company, it had two choices: Either a program already existed that allowed the information to be accessed in exactly this way, or the department had to ask a programmer to write such a program. In many cases, this was more work than it was worth, and it was always an expensive solution for one-time, or ad hoc, inquiries. As more and more users wanted easy access, this problem grew larger and larger.
>
> Allowing users to access data on an ad hoc basis required giving them **a language in which to express their requests**. A single request to a database is defined as a query; such a language is called a query language. Many query languages were developed for this purpose, **but one of these became the most popular: Structured Query Language**, invented at IBM in the 1970s. It is more commonly known by its acronym, SQL, and is pronounced both as "ess-cue-ell" and as "sequel". SQL became an ANSI standard in 1986 and an ISO standard in 1987; it is used today in a great many database management systems.

There are many key points made in the excerpt. An important one is that SQL is designed for the normal _users_, and not the programmers. Its original goal was to enable users to satisfy their information requirements more easily, without the need for the IT department's resources.

SQL is most strongly associated with realtional databases. This what is was orinally developed for. In fact, SQL requires structured data, and the relational database is the best example for a highly structured database. However, if a database does not rely on the relational model, it doesn't mean the data in it isn't structured. In fact, there is no way at all to query unstructured data. What would you even be querying for? Even for unstructured \(or semi-structured\) data such as images, we must project some structure \(or schema\) onto the data when we want to query it. And once we have a schema, we can use SQL again.

## The power of SQL

### Query data

SQL is most famous for its ability to _query_ strucutred data. The means to do that is the popular select command. Selecting data with this commandis at the core of what we do with SQL. For most of our scenarios, we assume the structure and content of the data is given. We only want to _get_ the data we need from the given data set. This can be tricky, but it requires only the select command.

### Manipulate data

To change a data set's content, we can use a specific set of SQL's commands. This part of SQL is referred to as the SQL _Data Manipulation Language \(DML\)._ It allows us to perform operations that manipulate the data:

* Delete data records
* Update data records, such as specific column \(or fields\) values
* Add new data records

### Define data

