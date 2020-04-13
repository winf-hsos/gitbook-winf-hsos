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
select month(created_at)
      ,year(created_at)
      ,year(created_at) || '-' || month(created_at) as `Period`
      ,count(1)
from tweets
where year(created_at) IN (2019, 2020)
group by month(created_at), year(created_at)
order by year(created_at), month(created_at)
```

