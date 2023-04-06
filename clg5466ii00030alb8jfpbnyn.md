---
title: "Thinking about schemas in Apache Druid"
datePublished: Sun Nov 01 2020 13:47:55 GMT+0000 (Coordinated Universal Time)
cuid: clg5466ii00030alb8jfpbnyn
slug: thinking-about-schemas-in-apache-druid
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Wpnoqo2plFA/upload/4b4e81519cd814e947ac0d8a99720c96.jpeg
tags: apachedruid

---

[*Mike\_McLaughlin*](https://www.linkedin.com/in/mikermclaughlin/) *and I used to spend a LOT of time talking about schema design in Apache Druid. The schema of your datasource has a massive impact not just on the ability to deliver the data people want from a Druid-powered application, but on the performance of the queries that power that application. Let’s look at a matrix that can help in designing that perfect schema in Druid.*

First, let’s not forget that the Druid documentation is a great place to start. If you haven’t already, take a look at the [Schema Guidance](https://druid.apache.org/docs/latest/ingestion/schema-design.html) in the core documentation.

# Understanding Usage

Start a new sheet, and add a row for each dimension of incoming data.

Next, we’re going to add check-box columns that cover three usage characteristics:

1. Data you’ll be using at ingestion time - (red)
    
2. Data you’ll use at query time - (orange)
    
3. Data you’ll generate at ingestion time (yellow)
    

Third step, for each dimension, put an X into the appropriate column.

* Tick red any time you are going to use this column at ingestion time for filtering and transformation (`transformSpec`), in-Druid enrichment (a `LOOKUP`), or which will get flattened
    
* Amber column is all about the query - filtering, sorting, [calculations](https://druid.apache.org/docs/latest/querying/sql.html#numeric-functions), and statistical [aggregations](https://druid.apache.org/docs/latest/querying/sql.html#aggregation-functions). Amber also covers columns you’re going to `GROUP BY` or use for bucketing results.
    
* Finally, yellow means you’re going to create windowed aggregations using roll-up - whether that’s accurate or [approximate](https://druid.apache.org/docs/latest/querying/aggregations.html#approximate-aggregations) (including set, quantile, and cardinality estimation)
    

Your final sheet might look something like this. Notice how in this example, our hero actually split the columns out further.

![2020-10-07_12-36-51](https://lc-imply-s3.b-cdn.net/optimized/2X/9/9ee4d86094196f8c62ec84f8c1e64a02e109b4f9_2_517x183.png align="left")

They also added another column to record the [type](https://druid.apache.org/docs/latest/querying/sql.html#data-types-and-casts) you’ve chosen for the dimension: `STRING`, `DOUBLE`, `FLOAT`, `LONG` or `COMPLEX`. This reminded them that they had some incoming “numeric” fields (like an account Id) they were actually going to store as a `STRING` to take advantage of better indexing.

# Applying the Table

## Red columns

### Consider on-ingestion Lookups for enrichment

If you’re going to use the data as a *Foreign Key*, you have a choice. Either use this to `JOIN` data at query time, or do it beforehand at ingestion time. If your data must represent the state at the time of ingestion (e.g. recording an Account Hierarchy parent or a person’s surname) you’ll want to do a `lookup` on ingestion. If you want the current state, you’ll want to `JOIN` or `lookup` at query time. In the former, the enrichment happens once on ingestion, in the latter it happens every time and impacts your query. Choose wisely!

### Think carefully about transforming data as it arrives

If you’re going to use the column for new dimension values, just think in your mind whether it’s better tio use expressions at ingestion time in the `transformSpec` or to just do it at query time? it’s the same question as Lookups, really: performance and state.

Don’t forget this question also applies to your timestamp, which can also be transformed at ingestion time.

## Amber columns

### Use the most popular time column

If you have multiple time columns in your incoming data, remember that the primary time column is used to shard data. Therefore, choose a timestamp that will be used to sort and filter the most when you set up your spec. Store other timestamps as longs in milliseconds with `transformSpec`.

### Filter fast

Are you *almost always* applying the same filter to you queries? I mean, *exactly* the same query? I’m talking:

`WHERE state = "valid"`

or

`WHERE colourOfFruit = "orange" AND fruitType = "orange"`

Or maybe your users will always filter on that dimension: in which case, think about the number of times people will actually filter by each value - is there a general rule (everyone always uses “orange”) and a set of weird edge cases (Brian in Sales looks for “tomato” every twenty-fifth September but only in a leap year)?

Think carefully about whether you could use `transformSpec` filters to completely filter the rows out (Brian will be made happy in other ways), to split your incoming data into multiple datastores (Brian gets a special one *all of his own*) or to use it as a sub-partition key (great for a row distribution of `maxRowsPerSegment` per `segmentGranularity`).

### Use strings for numbers…

When an incoming column is *never* going to be used for calculations or to make numerical stats, but is *only* going to be used for filtering and sorting, it should be a string *even if it’s numeric*. This takes advantage of all the column optimisations to speed up those operations. Some examples might be:

* Application Identifier
    
* Product Number
    
* Customer Reference Number
    
* NAICS Code
    

Imagine: you will never add together or find the average Application Identifier - but you are pretty much guaranteed to filter or sort by it.

### …except for GROUP BY

Reportedly `GROUP BY` often performs better on numerical values than string values in Druid. So if you’re going to group results using this dimension, you may want to store it as a number - maybe as an additional dimension just for grouping.

## Yellow columns

As a general rule, if the raw data isn’t needed - ie you’ve not ticked *any* red or amber columns at all for a given dimensions, either exclude it or use it to create a statistic or datasketch.

> Fred is a network manager, and he is pushing all his network monitoring events into Kafka. Feeding into Druid are 2.5 kazillion events per minute. Yet Fred is unhappy. His queries are taking 3 days to run.
> 
> Using The Matrix of Supreme Schema Design, Fred realises that he never, ever, *ever* sorts of filters by IP address. Moreover, he never *ever* needs an absolutely accurate count of IP addresses - he’s using this data mainly for trends and anomaly detection anyway. So Fred turns on roll-up, sets his `queryGranularity` to `MINUTE`, and removes his `ip_addr` field and instead creates a `HLL` sketch. Now he gets a fantastic level of accuracy for his counts.
> 
> Then, like a wave of brains, Fred realises he’s also bringing individual temperature readings for each device. “What a fool I have been!” exclaims Fred. Fred removes the temperature readings and replaces it with a SUM (so he can divide it by count to get an average) and a MAX (because he has a friend called Max).
> 
> Suddenly, Fred’s 2.5 kazillion events per second are represented in just *four rows*. Yes, you heard us right: **four rows**! The increase in query performance is meteoric. He wins awards. His cat even loves him again. Fred is happy.

Technically, these are metrics in Druid - not dimensions. So if you do go down this path for your incoming column, you will leave this row’s data type in the matrix blank, and probably add another row that is a Metric where you record the type of aggregation you’ll use - MAX, MIN, FIRST, LAST, HLL, etc.