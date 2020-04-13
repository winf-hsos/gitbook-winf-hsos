---
description: >-
  Let's see what kind of information a tweet is made of and how we can access it
  using SQL.
---

# Tweets

## What columns does a tweet have?

We can quickly get an overview of all available columns using the following SQL statement:

```sql
describe tweets
```

The result is a table with the name and data type of each column:

| Column Name | Data Type |
| :--- | :--- |
| id | String |
| screen\_name | String |
| created\_at | Timestamp |
| lang | String |
| text | String |
| hashtags | Array of Strings |
| is\_retweet | Boolean |
| is\_quote\_status | Boolean |
| in\_reply\_to\_screen\_name | String |
| in\_reply\_to\_status\_id | String |
| favorite\_count | Integer |
| quote\_count | Integer |
| retweet\_count | Integer |
| retweeted\_status\_id | String |
| retweeted\_user | String |
| urls | Array of Structs |
| photos | Array of Structs |
| user\_mentions | Array of Strings |
| source | String |
| insert\_timestamp | Timestamp |

## How many tweets are there?

If we want to know how many tweets we have in our data set, we can do a simple count of all rows:

```sql
select count(*) from tweets
```

## How many tweets are there by user?

The same question, but now we want to know the number per user. For that, we apply grouping tweets by `screen_name`. In addition, we sort the result by the number of tweets in descending order \(`desc`\) so that the user with the most tweets shows on top:

```sql
select count(*) as `Number Tweets`
      ,screen_name as `User`
from tweets
group by screen_name
order by count(*) desc
```

## How many tweets are there over time?

To see if there any abnormalities or trends in our data, lets aggregate the number of tweets by time period. In the example below, we use months, and we add an extra field `Period` that contains the year and month value concatenated by a hyphen. This field proofs useful for visualization and sorting: 

```sql
select month(created_at) as `Month`
      ,year(created_at) as `Year`
      ,year(created_at) || '-' || month(created_at) as `Period`
      ,count(1)
from tweets
where year(created_at) IN (2019, 2020)
group by month(created_at), year(created_at)
order by year(created_at), month(created_at)
```

## How many tweets are there per hour of the day?

It might be interesting to get a feeling for when the users tweet during the day. Let's create a query that groups by the hour of the day and visualize the result:

```sql
select hour(created_at) as `Hour`
      ,count(*) as `Number Tweets`
from tweets
group by hour(created_at)
order by hour(created_at) asc
```

The result visualized in Databricks as a bar chart:

![Number of tweets in every hour of the day in the example data set.](../../../.gitbook/assets/image%20%2834%29.png)

