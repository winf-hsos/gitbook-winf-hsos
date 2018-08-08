# Date and Time

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

