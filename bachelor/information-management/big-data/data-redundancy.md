# Data Redundancy

## The more the better \(or safer\)

Bob is a hobby photographer. He stores his photos on his laptop, but he is afraid to loose his work in case his laptop dies. So he came up with a strategy: He stores 3 versions of his photos. One on his laptop, one on an external hard drive in his living room drawer, and a third copy on a set of CDs that he deposits 50 miles away at his mother's house.

Having multiple copies on different media and keeping them in different physical locations is in fact a good strategy against loss of data, and it was recommended by many professionals from IT and photography. They call this _data redundancy_. If you loose one, you still have the other two, and you can restore the lost backup.

Keeping three redundant copies that way is also a cumbersome task. You must keep all copies in sync, and for most phyiscal media, you will need to frequently check whether they are still working. If not, you need to revocer your data, and to prevent this in the future, you must come up with a strategy that replaces for example CDs before they loose data. This is time consuming.

Fortunately, we no longer have to do all that work ourselves. We recently entered the cloud era, and cloud vendors nearly perfected data storage services in the past years. Most vendors guarantee you unlimited data retention. In other words, they promise they'll never loose your data as long as you don't delete it. They can promise this because they keep your data redundantly.

Cloud vendors use a similar technique as Bob does with his photos. When you upload a photo to the cloud service, they store that photo not just on one server, but on three or more at the same time. To make your photo even safer, these servers sit in different data centers around the world. And because the data centers are connected via a fast network, they can keep the data in sync in almost no time.

{% hint style="info" %}
Besides safety, storing data redundantly in data centers around the world has another benefit. It reduces latency when accessing the data. It takes longer to tranfer a file from at data center in Los Angeles to a latop in Berlin than from a data center in Frankfurt. This is the underlying principle of _Content Delivery Networks \(CDN\)_. Websites delivered via a CDN load faster.
{% endhint %}

Data redundancy is not merely useful for photos, but for any kind of data that you want to store permanently.

{% embed url="https://www.youtube.com/watch?v=LV1ncV1MO\_g" %}

