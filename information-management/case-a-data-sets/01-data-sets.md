# Data Sets

## Data formats

### Comma Separated Values \(CSV\)

## Data granularity or level of aggregation

### What does a record represent?

### Single values

## Data types

### A standard format for dates

Imagine the following situation: You are on the phone with your insurance company, and to make you sure you are actually who you claim to be, the clerk asks for your birthdate. Given you are in Germany, you wouldn't have to think long about what information the clerk expects to receive \(day, month, year\), and in which order. In Germany, we always write down birthdates in this form: day of month as a two digit number, followed by a dot, month of the year as a two digit number, followed by dot, and finally, the year as a four digit number. For example: **13.09.1981**, which is my birthdate in this format. More general, we can describe the format as **dd.mm.yyyy.** If you were in the United States, you'd write the same date as **09/13/1981**, and the general format would be **mm/dd/yyyy**.

Your birthdate is actually a special case of a more general class of information: A date. We do not just write down birthdates using this agreed upon format, we use it for any date we write down anywhere. The same is true for the IT context, and especially for databases. Here, we store dates in an agreed upon format, and we assign it the data type `date`.

### Less specific data types

A date is one of many data types. It is actually quite specific, and it is composed of less specific data types. For example, a date can also be viewed as a series of characters \(**"13.09.1981"** = numbers and punctuation marks\). For a date, these characters just happen to follow a certain syntax, and that makes it fit the data type `date`. We can also store a series of characters that don't follow a specific syntax, and we call this data type a `string`. In a string, we can store any number of arbitrary characters, no syntax required. However, most often we use the `string` data type to store things that _do_ follow a syntax: words, sentences, or whole texts.



\*\*\*\*



## Representations of data

