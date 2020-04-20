# Clean & Process Data

{% hint style="info" %}
This page is a placeholder until I finish the article of the script.
{% endhint %}

## Remove duplicate records

Due to errors or even built-in safety mechanisms in the Twitter API as well as potential errors in the [Twitter Collector Tool](https://big-data-analytics-helper.web.app/), it can happen that we have duplicate tweets in our database. Before we analyze the data, it is a good idea to remove them.

Learn how to check for duplicates and remove them in this article:

{% page-ref page="../sql-for-twitter/clean-twitter-data.md" %}

## Filter data beforehand

Depending on your question, filtering the data can be part of the preparation process. Filtering can be useful on different attributes. 

{% page-ref page="../sql-basics/filter-rows-with-sql.md" %}

In any case, you should make sure you store the result of the filtering process on a temporary view or even a permanent table. This way, you can always access the filtered data for analysis and the queries are likely to run faster with less data to process.

{% page-ref page="../sql-advanced/views.md" %}

### By user

For some questions, you might only be interested in the tweets by one user or a group of users. You can then easily filter tweets using the `screen_name` attribute.

### By date

### By topic / hashtag

