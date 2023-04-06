---
title: "An adventure into profiling segments with Apache Druid's SYS tables"
datePublished: Wed Jul 06 2022 11:02:37 GMT+0000 (Coordinated Universal Time)
cuid: clg50ep6z000e09mnco6r9sln
slug: an-adventure-into-profiling-segments-with-apache-druids-sys-tables
tags: apachedruid

---

So I thought I’d share something I did a long while ago to profile segments in Druid using the `sys` tables!

All these can be executed in the console’s Sql interface:

#### What are the characteristics of segments inside each datasource?

I found this really useful for just getting a feel for what the segments are like in your Druid datastore. This query is focused on segments that have been pushed and published (ie, not real-time).

```sql
SELECT "datasource",
  COUNT(*) as segments,
  SUM("size") / 1048576 as totalSizeMb,
  MIN("size") / 1048576 as minSizeMb,
  AVG("size") / 1048576 as averageSizeMb,
  MAX("size") / 1048576 as maxSizeMb,
  SUM("num_rows") as totalRows,
  MIN("num_rows") as minRows,
  AVG("num_rows") as averageRows,
  MAX("num_rows") as maxRows,
  (AVG("size") / AVG("num_rows"))  as avgRowSizeB
FROM sys.segments
WHERE is_available = 1 AND is_overshadowed = 0 AND is_realtime = 0
GROUP BY 1
```

Focusing on one day can be useful for comparisons between lava data sources (filtered, few dimensions, rolled-up with approximations…) versus raw data sources.

Druid picks up all the data it has available for the period that you are asking about. It’s like picking up all the books in a library written between two dates. Druid then starts to read each one (in parallel) to find the relevant data (filter) and to compute statistics (sum, average, count, etc) in groups (group by).

Making the books smaller reduces how long it takes to read each book, and might also reduce the number of books overall. This is like giving Druid a section of a library that’s focused on answering one set of questions, instead of asking it to look through the entire library. It’s a useful technique to swing the balance towards maximum return on investment and is particularly useful when the same filters are almost always applied by end users.

Every “library book” needs to be read by someone when you ask Druid a question. If you have 100 people, it will be 100 x faster than if you only have 1 person. By adding more “people” (cores), Druid has more book-reading capacity, so for faster initial Dashboard draw times, more cores will be needed.

#### What bucket does each segment fall into?

I wanted to then bucket them so I could understand the variation in the size of my segments by giving stats in million-row buckets – so I did this:

```sql
SELECT "datasource", ABS("num_rows" /  1000000) as "bucket",
  COUNT(*) as segments,
  SUM("size") / 1048576 as totalSizeMb,
  MIN("size") / 1048576 as minSizeMb,
  AVG("size") / 1048576 as averageSizeMb,
  MAX("size") / 1048576 as maxSizeMb,
  SUM("num_rows") as totalRows,
  MIN("num_rows") as minRows,
  AVG("num_rows") as averageRows,
  MAX("num_rows") as maxRows,
  (AVG("size") / AVG("num_rows"))  as avgRowSizeB
FROM sys.segments
WHERE is_available = 1 AND is_overshadowed = 0 AND is_realtime = 0
GROUP BY 1,2
ORDER BY 1,2
```

#### What is segment balance like over time?

One of the reasons for doing all this was because I wanted to see what improvements I could make to query performance by doing compaction. Particularly, I wanted to know what `skipOffsetFromLatest` I’d need for auto-compaction so [more recent intervals](https://druid.apache.org/docs/latest/configuration/index.html#compaction-dynamic-configuration) are compacted. So I pumped data from this query below into a spreadsheet…

Notice that the query uses `LEFT` to string-extract the period, and the `WHERE` clause also uses `LEFT` to allow you to filter by datasource name. So you may need to adjust the `39`, for example, to make sure it extracts the right bit of text. Out the back you get a server-by-server count of the number of segments on each server over time.

You don’t have to use `COUNT` of course - some [other stat](https://druid.apache.org/docs/latest/querying/sql.html#segments-table) may be more useful to you like a sum of the number of rows on that server to get a view of how busy that server would be if someone queried a particular time period.

```sql
SELECT
  LEFT("segment_id",39) as "interval",
  server,
  COUNT(*)
FROM sys.server_segments
WHERE LEFT("segment_id",{length-of-datasource-name}) = '{datasource-name}'
   AND server LIKE '%:8283'
GROUP BY 1,2
ORDER BY 1,2
```

I even added conditional formatting to highlight differences in each interval’s location across the servers. Here’s a sheet I used when ramping up the auto-compaction on a very fragmented dataset: I could watch as the number of segments dropped, day by day, across the cluster.

![image](https://lc-imply-s3.b-cdn.net/optimized/2X/2/244cf58212e4d47626e9f0f6de6c8b277f3f55d1_2_535x500.jpeg align="left")