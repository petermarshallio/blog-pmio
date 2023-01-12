# Apache Druid® - an enterprise architect's overview

[Apache Druid](https://druid.apache.org/) is part of the [modern data architecture]((https://a16z.com/2020/10/15/emerging-architectures-for-modern-data-infrastructure/)). It uses a special data format designed for analytical workloads, using extreme parallelisation to get data in and get data out. A shared-nothing, microservices architecture helps you to build highly-available, extreme scale analytics features into your applications.

## Modern data architecture

Druid is a real-time analytics database that can [ingest data](https://druid.apache.org/docs/latest/ingestion/index.html#ingestion-methods) from file stores and data lakes (for batch ingestion), and event streams (for immediate query). It’s used [globally](https://druid.apache.org/druid-powered) to build analytical interface elements in applications “whenever someone is sat there, waiting for the results” via a [SQL API](https://druid.apache.org/docs/latest/querying/sql.html) or JDBC interface.

## Storage system

Druid has its own [data format](https://druid.apache.org/docs/latest/design/segments.html). Source data is [sharded](https://druid.apache.org/docs/latest/ingestion/partitioning.html) at ingestion time into “segments” that enable planning for massively parallelized operations. The “Druid segment” is paired with Java code, crafted over many years by engineers from AirBnB to Yahoo, so that each one can be scanned and statistics extracted extremely quickly. Druid front-loads data distribution and replication, balancing it [automatically](https://druid.apache.org/docs/latest/design/coordinator.html#overview) to make it ready as soon as it’s needed for queries, and it uses metadata from each segment to intelligently prune query execution plans based on time periods and, optionally, [clusters](https://druid.apache.org/docs/latest/ingestion/partitioning.html#secondary-partitioning) of dimension values.

## Parallel execution

Dedicated leader [processes](https://druid.apache.org/docs/latest/design/processes.html) for each of ingestion, query, and on-going data management each generate highly parallelised execution plans. The plans are executed by independent follower processes, and there are facilities to target those workloads at particular groups of followers to account for different [query](https://druid.apache.org/docs/latest/operations/mixed-workloads.html#service-tiering) and [ingestion](https://druid.apache.org/docs/latest/configuration/index.html#worker-select-strategy) throughput requirements.

## Availability and elasticity

Druid has a shared-nothing, loosely-coupled microservices design, making use of cloud-era [dependencies](https://druid.apache.org/docs/latest/dependencies/deep-storage.html). The leading processes that each perform critical functions use proven leadership election techniques, while multiple follower processes add workload redundancy. A Druid cluster remains aware of the resources you make available to it and will distribute tasks to microservices automatically, allowing for on-the-fly adjustments to cluster size and shape. Together, this helps users create deployments with [high availability](https://druid.apache.org/docs/latest/operations/high-availability.html) that can adapt to the query concurrency and data scales that you have.

## Learn more…

* Take a look at the [design](https://druid.apache.org/docs/latest/design/architecture.html) section of the official Apache Druid documentation.
    
* Watch videos from Imply’s developer relations team’s “[adoption tips](https://www.youtube.com/playlist?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)” playlist.
    
* Meet members of the [Druid community](https://druid.apache.org/community/)