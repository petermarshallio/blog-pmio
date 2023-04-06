---
title: "Apache Druid® adoption essentials"
datePublished: Thu Apr 06 2023 08:03:11 GMT+0000 (Coordinated Universal Time)
cuid: clg4tzguj000d09l67hac13t8
slug: apache-druid-adoption-essentials
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/wpOa2i3MUrY/upload/1c75d4544eeef06781101838c73d409c.jpeg
tags: apachedruid

---

There are some things that our brains needs to dwell on when it comes to Druid. Things we need to think about before we even start our POC or pilot. Druid is different to warehouses, datalakes + query engines, timeseries database, search system - or any other type of NoSql DB you can shake a Metacritic rating at. There's just some things you gotta know...

## 1 – Druid is distributed

Apache Druid has a shared-nothing, microservices architecture. That's what helps us make robust, scalable deployments.

* Check [this video](https://youtu.be/2Ft-0CFkcgE?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) where I speak and have pretty slides on this very topic.
    
* Take [this course](https://learn.imply.io/apache-druid-basics) where you get your hands on a cluster irl
    
* Read about Druid’s [processes](https://druid.apache.org/docs/latest/design/processes.html), [clustered deployments](https://druid.apache.org/docs/latest/tutorials/cluster.html), use of [Apache Zookeeper](https://druid.apache.org/docs/latest/dependencies/zookeeper.html), the [Metadata Database](https://druid.apache.org/docs/latest/dependencies/metadata-storage.html), and [Deep Storage](https://druid.apache.org/docs/latest/dependencies/deep-storage.html)
    
* Check docs on [ingestion](https://druid.apache.org/docs/latest/ingestion/) (and [Apache Kafka ingestion](https://druid.apache.org/docs/latest/development/extensions-core/kafka-ingestion.html)) and the [load rules](https://druid.apache.org/docs/latest/operations/rule-configuration.html) that actually get the data pre-loaded onto Druid's processes to be queried. Also worth reading a little about [memory mapping](https://druid.apache.org/docs/latest/design/historical.html#loading-and-serving-segments-from-cache) in Druid.
    
* And for extra beans, check the docs on [task affinity](https://druid.apache.org/docs/latest/configuration/index.html#worker-select-strategy)
    

## 2 - Some queries just work better

Druid's fan-out, fan-in (aka scatter / gather) query engine (notwithstanding anything that happens with MSQ) means you need to know how queries execute. When you do, you'll get why some queries are awesomely fast, and some are ... tricky.

* I've got [a video](https://youtu.be/chnZmngXMsQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) on it that's based on one from Gian Merlino (PMC Chair) - checkit
    
* Read the detail on the query engines in Druid: [Native scan queries](https://druid.apache.org/docs/latest/querying/scan-query.html), [search queries](https://druid.apache.org/docs/latest/querying/searchquery.html) and [GROUP BY queries](https://druid.apache.org/docs/latest/querying/groupbyquery.html)
    
* Read more about the role of the [Broker](https://druid.apache.org/docs/latest/design/broker.html#overview)
    
* Check out more about [JOIN](https://druid.apache.org/docs/latest/querying/joins.html) operations in Druid in the docs, too.
    
* On the segment side, there's a great page on [segment optimisation](https://druid.apache.org/docs/latest/operations/segment-optimization.html) in the docs and [another video from me](https://youtu.be/kHH3oPqPGCw?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR), walking through that
    

## 3 - Know if you gotta approximate, mate.

At speed on big data sets, a UI will thank you for using approximation. Druid does some of it out of the box, so it's good to know what it is. And how you can help it out.

* Guess what - I've got a [video](https://youtu.be/fSWwJs1gCvQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) on it!
    
* Get to know how to use Sketches by looking at the docs on the [SQL functions](https://druid.apache.org/docs/latest/querying/sql-scalar.html#sketch-functions), and get the super-technical lowdown from the [Apache Datasketches](https://datasketches.apache.org/) project
    
* Don't forget you can use [rollup](https://druid.apache.org/docs/latest/ingestion/rollup.html) / `GROUP BY` to generate sketches at ingestion time and give those functions a speed boost
    
* Check out some videos on Datasketches being used with Druid – visit the Imply [developer resource center](https://docs.imply.io/latest/developer/dev-resources/) and hit "datasketches", like:
    
    * [Not Exactly! Approximate Algorithms For Big Data](https://files.speakerdeck.com/presentations/4d79125022d3013121837aec47472c60/Not_Exactly__Approximate_Algorithms_for_Big_Data.pdf) by Fangjin Yang and Nelson Ray
        
    * [Combining Druid and DataSketches for Real-time, Robust Behavioral Analytics](https://yahooeng.tumblr.com/post/147711922956/combining-druid-and-datasketches-for-real-time) by Himanshu Gupta and Mike Sefanov
        
    * [Fast Approximate Counting Using Druid and DataSketch](https://medium.com/expedia-group-tech/fast-approximate-counting-using-druid-and-datasketch-f5f163131acd), Elan Helfin and Aravind Sethurathnam
        
* Read about the approximate [TopN](https://druid.apache.org/docs/latest/querying/topnquery.html) native query in the docs
    

## 4 - Design each Druid `TABLE`

A `TABLE` in Druid has gotta be thought about – you'll want to consider how fast it needs to be, what the level of detail is, where it'll be stored, retention periods...

(Side note: there are other types of Druid [Datasource](https://druid.apache.org/docs/latest/querying/datasource.html) too - not just tables.)

* Here's [my video](https://youtu.be/OpYDX4RYLV0?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) on it
    
* There are some real important principles of data modelling for Druid - you can run through all of them in the Ingestion and Data Modeling [course](https://learn.imply.io/apache-druid-ingestion-and-data-modeling)
    
* Get to know the detail of [segments](https://druid.apache.org/docs/0.23.0/design/segments.html#segment-components) in the docs
    
* Watch [this notebook series](https://www.youtube.com/watch?v=7caGijktulo&list=PLDZysOZKycN4wNrNUpUhfXLP8Q___5omG) from the awesome Sergio Ferragut about how Druid shards incoming data into segments through the `PARTITIONED` and `CLUSTERED`
    
* You can read more on changing data through [reindexing](https://druid.apache.org/docs/latest/ingestion/faq.html#how-can-i-reindex-existing-data-in-druid-with-schema-changes) in the docs
    
* For info about retention and tiering, check [Load and Drop rules](https://druid.apache.org/docs/latest/operations/rule-configuration.html) - there's even a [retention tutorial](https://druid.apache.org/docs/latest/tutorials/tutorial-retention.html)
    
* Read about [UNION ALL](https://druid.apache.org/docs/latest/querying/sql.html#union-all) in SQL
    
* There's a cool doc on considerations for [multi-tenancy](https://druid.apache.org/docs/latest/querying/multitenancy.html) in Druid
    
* Also remember to read about how Druid [updates data](https://druid.apache.org/docs/latest/ingestion/data-management.html#updating-existing-data)
    

## 5 - Some fish upstream

Yep you can twist and turn your data at ingestion time in Druid. But some stuff you may want to think about doing upstream.

* Check out [my video](https://youtu.be/dmhbnJTlnt8?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) on this very topic.
    
* Read about using native [DimensionsSpec](https://druid.apache.org/docs/latest/ingestion/ingestion-spec.html#dimensionsspec) for inclusions, exclusions, and schemaless ingestion, and to enable indexes.
    
* Check native [TransformsSpec](https://druid.apache.org/docs/latest/ingestion/ingestion-spec.html#transformspec) for expressions and filtering - and obvs in MSQ that's just your usual SQL functions in `INSERT`
    
* Read about how Druid can aggregate at ingestion time using [rollup](https://druid.apache.org/docs/latest/ingestion/rollup.html) - the equivalent being `GROUP BY` with MSQ `INSERT`
    

## 6 - Druid's not an island

There might be other things that you need to put around Druid to successfully integrate it into your pipeline.

* Here's [my video](https://youtu.be/CgB-unmWGOs?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) (you should have known this was coming by now)
    
* And there's a tonne of videos on the Druid ecosystem over on the [developer resource center](https://docs.imply.io/latest/developer/dev-resources/) from other people, cooler than me! Here's a selection:
    
    * [Automating CI/CD for Druid Clusters at Athena Health](https://www.youtube.com/watch?v=XGzMJBM8xeg), Shyam Mudambi / Ramesh Kempanna / Karthik Urs
        
    * [Druid and Spot Instances at SuperAwesome](https://youtu.be/XoX-0IblxiQ), Nicolas Trésegnie
        
    * [Building an Enterprise-Scale Dashboarding/Analytics Platform at Target](https://youtu.be/h1FaIbGt_NE), Jeremy Woelfel
        
    * [Building a Real-Time Gaming Analytics Service with Apache Druid at Game Analytics](https://youtu.be/iE_pJwOl3_U), Ramón Latres Guerrero
        
    * [Interactive time-series analysis with Apache Druid, Apache Superset, and Facebook Prophet](https://preset.io/blog/2021-3-16-druid-prophet-pt2/) by Robert Stolz
        
    * [One event to rule them all at Outbrain](https://youtu.be/v_1L-aYY2YU), Daria Litvinov
        
    * Simon Späti’s [Open-source data warehousing](https://www.sspaeti.com/blog/open-source-data-warehousing-druid-airflow-superset/) article
        
* In the docs, check out:
    
    * [Druid configuration reference](https://druid.apache.org/docs/latest/configuration/index.html)
        
    * [Druid security overview](https://druid.apache.org/docs/latest/operations/security-overview.html)
        
    * [Task logs](https://druid.apache.org/docs/latest/ingestion/tasks.html#task-logs), the [general logging overview](https://druid.apache.org/docs/latest/configuration/logging.html), and [Druid metrics and emitters](https://druid.apache.org/docs/latest/operations/metrics.html) - and check out the [learn.imply.io](https://learn.imply.io) course on Logs and Metrics, too