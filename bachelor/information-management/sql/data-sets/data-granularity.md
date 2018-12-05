# Data Granularity

## Data granularity

### What does a record represent?

Imagine this scenario: To decide whether to install a traffic light, the city wants to count the number of cars that pass through by an intersection in every hour of the day. They hire students to count and write down the number of cars passed. An example from one day looks like this:

| Day | Starting Hour | Cars |
| :--- | :--- | :--- |
| 2018/01/10 | 9 am | 78 |
| 2018/01/10 | 10 am | 99 |
| 2018/01/10 | 11 am | 81 |
| 2018/01/10 | 12 am | 145 |
| 2018/01/10 | 1 pm | 131 |

Now ask this simple question: Does this data contain all the information we could have gotten about the subject "cars at the intersection"? The answer is no, and to find out why, we can look at what a record represents: One record \(or row\) represents the **sum of cars** that passed through in one hour. The key here is the word "**sum**".

When counting the cars, the students could have noted every single car as its own record. That would mean, instead of only one record for the hour from 9 - 10 am, we'd have 78 records. In that case, the students should have recorded the exact time of the car's passing, and maybe even some more features \(car make, color, type\). The first records could then have looked like this:

| Day | Time | Make | Color |
| :--- | :--- | :--- | :--- |
| 2018/01/10 | 09:01:23 AM | BMW | black |
| 2018/01/10 | 09:01:55 AM | Opel | green |
| 2018/01/10 | 09:03:12 AM | BMW | white |
| 2018/01/10 | 09:03:20 AM | Volkswagen | black |

If we look at both data sets, we can conclude the following:

* A row per car provides us with more information than the one with the sum of cars per hour.
* The data set with a row per car is much bigger than the one with the sum of cars per hour.
* We can easily derive the sum of cars per hour from the data set with the rows per car through **aggregation**. It does not work the other way around.

### Aggregation

Having the data at it finest granularity gives you flexibility of what types of analysis you can do with the data. Take the car count example from above: What if the city found out they needed not the sum per hour, but the sum for every minute in order to decide on the length of the green phases? With the data set containing one row per hour, this would be impossible to do. The city would need to start counting all over again, this time using the finest granularity possible: one row per car. From there, they could aggregate and count the cars for any time interval they needed.

And not just that. Having more attributes in the data set \(car make, color\), aggregations along any combination of these dimensions become possible \(e.g. cars per hour per car make\).

{% hint style="info" %}
Aggregating data always results in less or an equal number of rows.
{% endhint %}

### Flattening

### Single values

