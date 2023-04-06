---
title: "Notes on roll-up effectiveness in Apache Druid"
datePublished: Thu Apr 06 2023 09:22:59 GMT+0000 (Coordinated Universal Time)
cuid: clg4wu2s2000i09lb0vqo7hai
slug: notes-on-roll-up-effectiveness-in-apache-druid
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/-sDWTQfqgFA/upload/1d6067e8646d680c5a97a61c74315e92.jpeg
tags: apachedruid

---

I thought I’d share some lessons I learned over the last few years about ingestion-time aggregation in Druid, and how cardinality affects it. This is kinda a little process I go through mentally that I thought would be helpful to share!

In case you don't know what roll-up is, it [takes incoming rows in Druid and then aggregates them](https://druid.apache.org/docs/latest/ingestion/rollup.html), spitting out metrics from the measures that you have. There's the native rollup, which you turn on with streaming ingestion, and then there's the modern Druid approach to roll-up, which – in plain English, a `GROUP BY` in the `INSERT` [statement](https://druid.apache.org/docs/latest/ingestion/rollup.html) for batch ingestion.

You might choose to emit your usual `MAX`, `MIN`, and so on metrics, or something more hÿpercool like a [data sketch](https://druid.apache.org/docs/latest/ingestion/index.html#metricsspec) to speed up approximation operations. In native, you put all that in the [`metricsSpec`](https://druid.apache.org/docs/latest/ingestion/rollup.html) section of your ingestion specification - with `INSERT` you just use the usual aggregates.

Awesome! Now you can reduce your 10m rows per second of people surfing TikTok on your office WiFi network (I will not enter into the debate as to whether TikTok connects to WiFi) to just 10 per second, giving you the aggregates ahead of time that you would otherwise have computed every time with each query.

In terms of efficiency of this operation, it's the same as it is for any `GROUP BY` operation: the cardinality of dimensions you have in your `SELECT`. In Druid’s case, that’s the source data columns that you list in your [ingestion specification](https://druid.apache.org/docs/latest/ingestion/index.html#dimensionsspec) or `INSERT` statement. So be cautious!

A discrete piece of functionality in Druid is to automatically truncate incoming timestamps. That’s done by specifying a `queryGranularity` in the ingestion spec or by using a suitable time function in your `INSERT`.

Here’s an example data set where `queryGranularity` processing is at `FIVE_MINUTE`. Druid has, for every incoming event, truncated the timestamp (like a [`TIME_FLOOR`](https://druid.apache.org/docs/latest/ingestion/rollup.html)).

| **Time** | **Name** | **Dance** |
| --- | --- | --- |
| 09:00 | Peter | Fandango |
| 09:00 | John | Fandango |
| 09:00 | Peter | Fandango |
| 09:05 | John | Fandango |
| 09:05 | John | Fandango |
| 09:05 | John | Fandango |
| 09:05 | Peter | Waltz |
| 09:05 | Peter | Waltz |

Now let’s use our eye-minds and think about the roll-up.

Imagine that we're going to add a `COUNT` Each column has low cardinality within that time period, so we get a nice aggregation: 8 went in, 4 came out.

| **Time** | **Name** | **Dance** | **Count** |
| --- | --- | --- | --- |
| 09:00 | Peter | Fandango | 2 |
| 09:00 | John | Fandango | 1 |
| 09:05 | John | Fandango | 3 |
| 09:05 | Peter | Waltz | 2 |

But what about this one:

| **Time** | **Name** | **Dance** |
| --- | --- | --- |
| 09:00 | Peter | Fandango |
| 09:00 | Mary | Fandango |
| 09:00 | Tom | Fandango |
| 09:05 | Brian | Fandango |
| 09:05 | Peter | Fandango |
| 09:05 | Mary | Fandango |
| 09:05 | Tom | Fandango |
| 09:05 | Terry | Fandango |

Notice that, within the 5 minutes buckets (our `queryGranularity` truncated timestamp) *every single event relates to a different dancer*. When the `GROUP BY` kicks in, those 8 incoming rows get emitted as 8 rows: the `GROUP BY` is **across all of the dimensions**.

| **Time** | **Name** | **Dance** | **Count** |
| --- | --- | --- | --- |
| 09:00 | Peter | Fandango | 1 |
| 09:00 | Mary | Fandango | 1 |
| 09:00 | Tom | Fandango | 1 |
| 09:05 | Brian | Fandango | 1 |
| 09:05 | Peter | Fandango | 1 |
| 09:05 | Mary | Fandango | 1 |
| 09:05 | Tom | Fandango | 1 |
| 09:05 | Terry | Fandango | 1 |

And there’s a second scenario: lots of **combinations** of values.

| **Time** | **Name** | **Dance** |
| --- | --- | --- |
| 09:00 | Peter | Fandango |
| 09:00 | Mary | Polka |
| 09:00 | Mary | Vogue |
| 09:05 | Brian | Fandango |
| 09:05 | Lucy | Waltz |
| 09:05 | Claire | Fandango |
| 09:05 | Sian | Waltz |
| 09:05 | Terry | Waltz |

Here there are just too many combinations of values in each five-minute interval. Every dancer dances a different dance.

| **Time** | **Name** | **Dance** | **Count** |
| --- | --- | --- | --- |
| 09:00 | Peter | Fandango | 1 |
| 09:00 | Mary | Polka | 1 |
| 09:00 | Mary | Vogue | 1 |
| 09:05 | Brian | Fandango | 1 |
| 09:05 | Lucy | Waltz | 1 |
| 09:05 | Claire | Fandango | 1 |
| 09:05 | Sian | Waltz | 1 |
| 09:05 | Terry | Waltz | 1 |

One cause for this combined cardinality problem could be data hierarchy. Let’s imagine that Peter is King of the Fandango and Voguing. (Well done, Peter). John, meanwhile, is King of the Foxtrot, Waltz, and Paso Doble. (Ie, parent-child).

| **Time** | **Teacher** | **Dance** |
| --- | --- | --- |
| 09:00 | Peter | Fandango |
| 09:00 | John | Foxtrot |
| 09:00 | Peter | Vogue |
| 09:05 | Peter | Fandango |
| 09:05 | John | Foxtrot |
| 09:05 | John | Waltz |
| 09:05 | Peter | Fandango |
| 09:05 | John | Paso Doble |

The roll-up ends up looking like this:

| **Time** | **Teacher** | **Dance** | **Count** |
| --- | --- | --- | --- |
| 09:00 | Peter | Fandango | 1 |
| 09:00 | John | Foxtrot | 1 |
| 09:00 | Peter | Vogue | 1 |
| 09:05 | Peter | Fandango | 2 |
| 09:05 | John | Foxtrot | 1 |
| 09:05 | John | Waltz | 1 |
| 09:05 | John | Paso Doble | 1 |

Here, the roll-up is less effective because each dancer (the root) knows a distinct set of dances (the leaves) and it’s very unlikely that they’d *repeat the same dance in the same roll-up period*.

You can look at data you have ingested already to get a feel for its profile.

If you've got your data in Druid already, find the number of rows in a one hour period simply by using the Druid console:

```sql
SELECT COUNT(*) AS rowCount
FROM "your-dataset"
WHERE "__time" >= CURRENT_TIMESTAMP - INTERVAL '1' HOUR
```

Finding cardinality is very easy as well:

```sql
SELECT COUNT (DISTINCT your-column) AS columnCardinality
FROM "your-dataset"
WHERE "__time" >= CURRENT_TIMESTAMP - INTERVAL '1' HOUR
```

Of course, you can do more than one at once, but just be cautious - on large datasets this can swamp your cluster…

```sql
SELECT COUNT (DISTINCT your-column-1) AS column1Cardinality,
   COUNT (DISTINCT your-column-2) AS column2Cardinality,
   :
   :
FROM "your-dataset"
WHERE "__time" >= CURRENT_TIMESTAMP - INTERVAL '1' HOUR
```

Even more useful is the ratio of rows to unique values of a column. If you have the *wikipedia* edits sample data loaded, try this query, which gives you the ratio for just a few of the columns in the data set. (Notice that the `__time` column `WHERE` clause is absent.)

```sql
SELECT CAST(COUNT (DISTINCT cityName) AS FLOAT) / COUNT(*) AS y,
   CAST(COUNT (DISTINCT channel) AS FLOAT) / COUNT(*) AS channelRowratio,
   CAST(COUNT (DISTINCT cityName) AS FLOAT) / COUNT(*) AS cityNameRowratio,
   CAST(COUNT (DISTINCT comment) AS FLOAT) / COUNT(*) AS commentRowratio,
   CAST(COUNT (DISTINCT countryIsoCode) AS FLOAT) / COUNT(*) AS countryIsoCodeRowratio,
   CAST(COUNT (DISTINCT countryName) AS FLOAT) / COUNT(*) AS countryNameRowratio,
   CAST(COUNT (DISTINCT diffUrl) AS FLOAT) / COUNT(*) AS diffUrlRowratio,
   CAST(COUNT (DISTINCT flags) AS FLOAT) / COUNT(*) AS flagsRowratio,
   CAST(COUNT (DISTINCT isAnonymous) AS FLOAT) / COUNT(*) AS isAnonymousRowratio,
   CAST(COUNT (DISTINCT isMinor) AS FLOAT) / COUNT(*) AS isMinorRowratio,
   CAST(COUNT (DISTINCT isNew) AS FLOAT) / COUNT(*) AS isNewRowratio,
   CAST(COUNT (DISTINCT isRobot) AS FLOAT) / COUNT(*) AS isRobotRowratio
FROM "wikipedia"
```

Those approaching 1 are the main cause of your low roll-up. In the `wikipedia` dataset, it’s clearly the `diffUrl` column. At the other of the scale are indicators of queries that are suffering because of the poor roll-up - like the `wikipedia` sample data columns that start with `is`.

The next step, whether the data has high compound cardinality, is more tricky. So I used the query above to create combinations of dimensions to assess, say, the dancer and the dance.

```sql
SELECT __time, COUNT(*) AS rowCount,
    COUNT (DISTINCT columnName) AS columnCardinality
FROM "datapipePMRawEvents"
WHERE "__time" >= CURRENT_TIMESTAMP - INTERVAL '1' HOUR
GROUP BY 1, 2
```

What I decided to do in my instance was to either shrink the number of dimensions (so maybe have two `tables`, one with all fields, and one with a commonly-used subset of fields designed to take advantage of rollup - then, I could query the appropriate dataset for a particular use case.). The other was to attack the cardinality problem. Maybe with a datasketch (if it is COUNT DISTINCT / set operation / Quantile) though I’ve heard some people using clever functions (from simple truncation to using if-then-else to create a new dimension).

In my instance I could then increase the `queryGranularity` to `HOUR` and I ended up with just one row instead of hundreds. It was particularly important as I was working in a clickstream project – and that has tonnes of data!

There was another option as well – which was to create different tables with some common filters already applied – that reduced the row count and had a big impact on cardinality as well.

So there you have it: remember to conceptualise and test your `GROUP BY` on the raw data, and remember cardinality and hierarchies.

Huzzah!