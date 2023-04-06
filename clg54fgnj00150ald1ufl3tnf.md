---
title: "Converting a timestamp from ticks (Windows) to epoch (Linux) at ingestion time in Apache Druid"
datePublished: Thu Oct 07 2021 12:55:14 GMT+0000 (Coordinated Universal Time)
cuid: clg54fgnj00150ald1ufl3tnf
slug: converting-a-timestamp-from-ticks-windows-to-epoch-linux-at-ingestion-time-in-apache-druid
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/mGFHA_0TWnA/upload/2af9bf426ce27bd796e3bf8ceb68cee3.jpeg
tags: apachedruid

---

To convert from c# ticks to Unix Epoch-based time, we will ingest the ticks and then use a transform to apply a simple calculation.

## Design the transform expression

`f = (c#Ticks - epoch_offset) / granularityRequired`

c#Ticks

Whatever the `column` setting is in the `timestampSpec` , it will always store it as `__time` . We can then refer to `__time` in a [transform expression](https://druid.apache.org/docs/latest/ingestion/index.html#transforms) and overwrite it with a different value. So, in the ingestion spec, just set the timestamp field as usual - we’ll then refer to `__time` in a transform and overwrite it.

epoch\_offset

621355968000000000 is the difference between the base time of c# Epoch and the Unix Epoch - the number of nanoseconds between 1st Jan 0001 and 1st Jan 1970. We must subtract this from the incoming c# tick time value as the first step.

granularityRequired

As c# ticks are very granular ([there is one tick every 100 nanoseconds](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.ticks)) we can maintain good resolution inside Druid. Druid supports a number of levels of time accuracy, so first find out [which one](https://druid.apache.org/docs/latest/ingestion/index.html#timestampspec) your business needs.

We divide the result of the epoch differences by the appropriate 10th power in order to get the [accuracy that you want](https://druid.apache.org/docs/latest/ingestion/index.html#timestampspec). For each timestampSpec/format, the divisor is as follows:

```apache
nano = 100
millis = 10000
posix = 10000000
```

## Add to the Ingestion Spec

You must set the granularity you will achieve inside the `timestampSpec/format` value.

Then put your transform formula into the the list of transforms at `transformSpec/transforms` . We use a simple `expression` -based transform to do the calculation, noting that it reads from, and writes back to, the \_\_time field.

Here’s what the expression looks like to convert to milliseconds:

`"type": "expression", "name": "__time", "expression": "(__time - 621355968000000000) / 10000"`

## Example

Here’s an example of a conversion from c# ticks to Unix Epoch-based milliseconds in Druid.

```apache
    :
    "timestampSpec": {
      "column": "incomingTime_dimensionName",
      "format": "millis"
    },
    "transformSpec": {
        "transforms": [
            { "type": "expression", "name": "__time", "expression": "(__time - 621355968000000000) / 10000" }
          ]
    },
    :
```