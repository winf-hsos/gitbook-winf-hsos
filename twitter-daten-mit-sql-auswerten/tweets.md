---
description: >-
  Let's see what kind of information a tweet is made of and how we can access it
  using SQL.
---

# Tweets

## What columns does a Tweet have?

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

