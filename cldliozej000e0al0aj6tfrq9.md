# Notes from Apache Druid POCs

"It's clear out time," says my ever-patient husband. "Why have you got all this paper hanging around? I need this space to put my brand new PS5 that you bought me." (Yes, the PS5 is so huge, it requires an entire room.)

And what did I find amongst the dusty, somewhat crusty A5 notepads but a tonne of notes from my days helping people through their very first POC with Apache Druid® - the real-time analytics database that's setting fire to the world of personal, high-speed analytics UIs.

What should app developers think about before they start? Who should data engineers talk to when they're setting things up? What's a hit list?

Herewith, then, a jumble of notes that I hope any of you about to start a POC with Apache Druid will find useful.

And as always, if you've got questions about anything here, come ask the [community](https://druid.apache.org/community). We're a friendly bunch!

## Start at the end

**Work with your end users to sketch out what your Druid-powered user interface is going to look like.**

As soon as you feel the early tingling magic of Druid, speak to Product Owners

* What dimensions will you need?
    
* Will there be common filters?
    
* What level of summarisation could be used?
    
* Do performance requirements on one visual differ from another one?
    
* Will there be interactive elements?
    

Why? To better inform your ingestion. That’s the dimensions you’ll need, the transformations and filters, and any metrics you can generate with a `GROUP BY` (aka roll-up) at ingestion time, and whether you could use data tiering.

And never forget to test the water with them about [approximations](https://youtu.be/fSWwJs1gCvQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) - ask them directly whether an approximation based on data rolled-up to a second or a minute is good enough for the analysis they want to do - it probably is!

Further back in the pipeline, it also helps your design - it’ll open up questions of whether you need to continue enriching [before data hits Druid](https://youtu.be/dmhbnJTlnt8?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) or whether you can do it inside Druid - whether by lookup on ingestion or at query time.

The message here is to work together on the ingestion specification with your end user. Avoid just chucking everything in and hoping for the best!

## Create magic

**Druid apps can be super special! Don’t miss the opportunity to modernise your application and how your end users will interact with it.**

You can be the person who shows the UI team what's actually possible by looking at what other people have built with Druid. Stuff that's different to how it's usually done.

Take a look at my other post where I ramble on about t[ha](https://pmio.hashnode.dev/apache-druid-powered-analytics-applications)t.

## Know thy queries

**Take time to familiarise yourself with how you construct Druid queries - especially the full gamut of options available in** [**Druid SQL**](https://druid.apache.org/docs/latest/querying/sql.html)**.**

Check out the full range of functions that are available to you, from approximation to array processing. Know the dialect's limitations and possibilities first.

Be aware of the functions you want to use and integrate these into your testing - not just that they work, but that they work at a sufficient level of performance given your infrastructure and your schema.

## Druid is not an Island

**Think about *how* and *what* you will deploy onto your** [**infrastructure**](https://youtu.be/CgB-unmWGOs?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)**, especially Druid’s dependencies.**

Druid has to exist in an ecosystem. It has service and infrastructure dependencies, and you should speak to your infrastructure people about how that might be done in a compliant and robust way.

That could be network ports connecting to your HDFS cluster on GCP when Druid will be on AWS. Or it could be AWS Security Groups to allow you to connect to Kinesis from account X when Druid will be account Y.

More and more Kubernetes is used to deploy everything from Druid to potato salad. If you’re hot on K8s, remember that your network engineer may not be. That point when you can’t figure out why Kafka won’t ingest or you can’t write segments to the deep store - if it’s a network issue you could be on your own.

Druid itself has [dependencies](https://druid.apache.org/docs/latest/design/architecture.html): a BLOB store, a relational database, and Zookeeper - take care to know their performance and capacity, but also longevity and supportability inside your organisation.

## Do not forget the JRE

**Configure JRE properties well - especially heaps - and choose the right hardware - so take time to read the tuning guide**

Yes, quickstart is great. It’s lovely! Some work has been done for you! Especially the configuration of the JREs that all the Druid processes run in.

I see people having issues because they haven’t provided enough Heap, for example. Or because they’ve specified loads of heap but run it on a server with three tiny mice for memory.

Heap sizing is particularly important if you’re going to use Lookups.

Take a look at the [tuning guide](https://druid.apache.org/docs/latest/operations/basic-cluster-tuning.html) in the official documentation - the calculations there will help you work out the right heap sizes, as well as some recommended JRE options – especially if you're not using the standard node configs.

## Go configure

There are some critical configuration properties that you should read up on and - as you work more with Druid - keep an eye on, tuning them for your precise ingestion volume and velocity and the query execution pattern on your underlying data.

This need for ongoing maintenance of the configuration files may prompt you to use something more formal to deploy your configs other than just `nano` and `rsync`…

At a minimum, make sure you have these set and know what they do:

| **What** | **Settings** |
| --- | --- |
| [`common.runtime.properties`](http://common.runtime.properties) | [`druid.metadata.storage`](http://druid.metadata.storage)`.type`  
`druid.metadata.storage.connector.*`  
`druid.storage.*`  
`druid.indexer.logs.*`  
`druid.zk.service.host`  
`druid.zk.paths.base` |
| Historical [`runtime.properties`](http://runtime.properties) | `druid.server.http.numThreads`  
`druid.processing.buffer.sizeBytes`  
`druid.processing.numMergeBuffers`  
`druid.processing.numThreads`  
`druid.segmentCache.locations`  
`druid.cache.sizeInBytes` |
| Historical `jvm.config` | XMS, XMX, and MaxDirectMemorySize |
| MiddleManager [`runtime.properties`](http://runtime.properties) | `druid.worker.capacity`  
`druid.indexer.runner.javaOpts` → `Xms`, `Xmx`, and `MaxDirectMemorySize` |
| Coordinator-Overlord `jvm.config` | XMS, XMX, and MaxDirectMemorySize |
| Broker `jvm.config` | XMS, XMX, and MaxDirectMemorySize |
| Router `jvm.config` | XMS, XMX, and MaxDirectMemorySize |

Sometimes, people miss that, when ingesting streaming data, Middle Manager Tasks (aka Peons) also respond to queries. Just like the Historical process, then, they receive lookups (unless you say otherwise) that need to go into heap, and they also have their own equivalent settings for the `druid.processing.*` you see above, but all prefixed with [`druid.indexer.fork.property`](http://druid.indexer.fork.property) in the MiddleManager [`runtime.properties`](http://runtime.properties).

The HTTP settings are also very often missed - these limit the number of queries that the Broker can receive and the size of the fan-out to Middle Manager Tasks and Historicals. There are a number of [dials](https://druid.apache.org/docs/latest/operations/basic-cluster-tuning.html#sizing-the-connection-pool-for-queries) around [`druid.broker`](http://druid.broker)`.http.numConnections`, `druid.server.http.numThreads`. You might even delve into [`druid.broker`](http://druid.broker)`.http.maxQueuedBytes`.

Then there are the settings for the caches - `druid.historical.cache.useCache` / [`druid.broker`](http://druid.broker)`.cache.useCache` and `druid.historical.cache.populateCache` / [`druid.broker`](http://druid.broker)`.cache.populateCache`.

## Stay connected

**Druid is a highly** [**distributed**](https://youtu.be/2Ft-0CFkcgE?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)**, loosely coupled system on purpose. Care for your interprocess communication systems and paths: especially Zookeeper and Http**

Query, data management, and ingestion are all distributed functions. They rely on good interprocess communication. Monitor your traffic and your network and try to keep the network and the processes healthy.

What you don’t want is to run into an issue where Zookeeper is running out of memory and crashes, but nobody is there to help you fix it - or even to tell you that it happened. Familiarise yourself with your Zookeeper configuration and why it matters.

## Love your logs

**Get to know the** [**logs**](https://learn.imply.io/apache-druid-logs)**. For ingestion, particularly the overlord, middle manager and its tasks. For everything else, particularly the coordinator and historicals.**

Anyone who spends time in the channels will see that people *look at their logs*.

This isn’t because we are all Ren and Stimpy fans. No, that’s because the logging in Druid is extremely detailed. From the start to the finish of every ingestion job is a detailed audit of process activity. Remember that Wikipedia sample data in quickstart? Like me, you probably didn’t look at the ingestions logs or the process logs and use them to learn what happened!

Take a different road. When you go back to your Druid cluster tomorrow, or if you’re just starting with Druid, open up that log folder. Go on! Take a look. Read through the logs and spend time understanding what Druid is doing for you. Then when you have an issue in the future, you’re much more likely to be able to understand what could have caused a blip.

## K.I.S.S.

**Be agile: set up a lab, start simple and start small, working up to perfection**

Druid is a sports car. If we did buy a Nissan GTR each, it would be foolish to drive it to the shops at 9.5 bn miles an hour. And it could be such a disappointment if you hop behind the wheel and think you’re going to get the most out of it only to crash out because you didn’t go out on the track first and learn all you could about it and your car.

When working with Druid **KEEP IT SIMPLE**: start small, with a discrete, well-known data set that’s nice and simple. Then you can watch the dance of the different parts of Druid, honing and tuning each one as needed. ITERATIVELY. Working up to a goal. We get EXCITED - and we want to use new toys. But Druid is unique as a database, it’s combining OLAP, time series, and search technologies so wherever you’re starting from, there are going to be things you need to do differently than you have before.

Maybe don’t do transformations first, maybe don’t do roll-up first.

You WILL get there - and you will have a much less stressful journey along the way.

## Understand segments

**Historicals serve all used** [**segments**](https://youtu.be/kHH3oPqPGCw?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)**, and deep storage stores them. Query time relates directly to segment size: lots of small segments means lots of small query tasks. Segments are tracked in master nodes and registered in the metadata DB**

Ingestion is where data is partitioned. It is worth checking that the ingestion specification you have written is creating segments of optimal size and content, clearly understanding those levers that you have.

First, we need to take care of the cost associated with Historicals. We need to scale out the Historicals with the right balance of storage and compute power according to our performance needs for the data we have in Druid.

Second, we mustn’t let the Druid Deep storage grow and grow for no reason. We need to keep careful control of the infrastructure costs that come with this critical storage area in Druid.

Third, we must remember that each parallel query task that Druid runs reads ONE segment each. If one segment is too big, or worse, if all of them are too big, queries will take too long to run.

But on the other end of the scale, if they’re too small, the processors and memory on the Historical servers become consumed with lots of tasks, each processing only very small amounts of data.

Finally, the Druid cluster has a database of all the segments with its own compute and storage overhead. It’s just good administrative practice to ensure this database doesn’t get overloaded, perhaps by keeping records for thousands of segments with data in them that we don’t care about any more.

All in all, that means you need to control the `COUNT` of segments as that affects the memory overhead and processing power we need to run queries.

Yes, don’t underestimate the importance of compaction, but *do not* leave it to compaction to tidy up a mess that you've made because of an insane ingestion config.

You also need to control the *size* of segments not just to control storage costs but because size also affects query performance.

* Filter rows and think carefully about what dimensions you need
    
* Use different segment granularities and row maximums to control the number of segments generated
    
* Apply time bucketing with query granularity and roll-up
    
* Think about tiering your historicals using drop and load rules
    
* Consider not just initial ingestion but ongoing re-indexing
    
* Never forget compaction!
    
* Check local (`maxBytesInMemory`, `maxRowsInMemory`, `intermediatePersistPeriod`) and deep storage (`maxRowsPerSegment`, `maxTotalRows`, `intermediateHandoffPeriod`, `taskDuration`) persists
    

## Get meta

**Collect metrics and understand how your work affects them**

Druid emits all kinds of event data in its metrics. It’s time-series data - use it like time-series data! Surface it and use it to make better decisions, faster decisions, about how you’re using Druid.

For ingestion, some key metrics are Kafka lag and - of course - GC collections. But also think about metrics that are affected by your ingestion: segment scan times and the number of segments scanned during a query. When you’re iterating through that ingestion specification, use these metrics to measure yourself as you approach full stability.

Some people even go as far as having JMeter watch query performance as each Ingestion Specification changes, and others even go so far as to use Flame Graphs (using Swiss Java Knife) to find exactly what is happening at the lowest of levels.

Important metrics include:

* 98th PERCENTILE QUERY TIME (most people are getting this)
    
* QUERY ID - very useful for over-time comparisons of similar queries (set programmatically)
    
* GC Time and Total GCs → Heap issues
    
* KAFKA LAG
    
* SUBQUERY COUNT + SEGMENTS SCANNED + SEGMENT SCAN TIME → optimising segments