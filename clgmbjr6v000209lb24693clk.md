---
title: "Getting to know Apache Druid®"
datePublished: Tue Apr 18 2023 13:46:56 GMT+0000 (Coordinated Universal Time)
cuid: clgmbjr6v000209lb24693clk
slug: getting-to-know-apache-druid
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/3MYvgsH1uK0/upload/80edcd104cf0e1fe7bf07575b006c402.jpeg
tags: apachedruid

---

I've been working with Druid now for four-and-a-bit years, joining Imply as its first pre-sales engineer in Europe, and now proud to be working with the open-source community full time as Imply's Director of Developer Relations!

This workaversary gave me a chance to think back on the people and things that helped me learn about Druid, and to compile a list of things that I would recommend anyone goes and checks out Druid.

## Get to know the Why

Take a listen to Eric Tschetter, the person who [made the first commit](https://github.com/apache/druid/commit/70e993806e48fbd35ac597a4075d046a98c5b6ae) to the [apache/druid](https://www.github.com/apache/druid) repository. You'll learn *why* Druid got built in the first place - and therefore what technical issues those originators were trying to fix.

* [https://softwareengineeringdaily.com/2021/08/16/druid-event-driven-data-with-eric-tschetter/](https://softwareengineeringdaily.com/2021/08/16/druid-event-driven-data-with-eric-tschetter/)
    

For a deep dive, check out the official Druid whitepaper, written way back when to give the findings of their research into the real-time analytics landscape as it was, and why the team decided to do the mad thing of creating a new database.

* [http://static.druid.io/docs/druid.pdf](http://static.druid.io/docs/druid.pdf)
    

It's also worth checking out the following to see how other people are using Druid:

* [Druid | Use Cases (](https://druid.apache.org/use-cases)[apache.org](http://apache.org)[)](https://druid.apache.org/use-cases)
    
* [Druid | Powered by Apache Druid](https://druid.apache.org/druid-powered)
    
* [Druid Summit](https://druidsummit.org)
    

## Try it now

Get straight into it and run through the Quickstart tutorials. Some people prefer a hands-on lab (like the Druid Basics course on Druid Faculty by Imply), some just `wget` Druid and run it in the JRE on their laptops, some prefer Docker. Some mad people like me [put it onto Raspberry Pis](https://pmio.hashnode.dev/a-raspberry-pi-apache-druid-cluster-well-why-not)! But either way, get an environment up and see what it looks like.

* [Druid Faculty](https://learn.imply.io) - Druid Basics
    
* [Druid Downloads](https://druid.apache.org/downloads.html)
    
* [Druid Quickstart Tutorial](https://druid.apache.org/docs/latest/tutorials/index.html)
    

I'd recommend resisting the temptation to go all out and deploy Druid in clustered mode. Be selfish and try out Druid on your own laptop for now.

## Learn what it's made of

Now you can start to pull back the onion skin. If you took Druid basics you'll have had a peek - but now get into it and find out what the Druid architecture is like. You need to know this especially if (like me!!!) Druid is the first database you've used that has a microservices, shared-nothing architecture.

* Video - [Remember! Druid's distributed](https://www.youtube.com/watch?v=2Ft-0CFkcgE&list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR&index=1&pp=iAQB)
    

I've also put together a post on the qualities of UIs built on top of Druid that might help you think about what kind of UI Druid is great for.

* [Apache Druid®-powered analytics applications](https://pmio.hashnode.dev/apache-druid-powered-analytics-applications)
    

Here's some key Druid Docs pages for you to look at:

* [Druid | Technology (](https://druid.apache.org/technology)[apache.org](http://apache.org)[)](https://druid.apache.org/technology)
    
* [Processes and servers · Apache Druid](https://druid.apache.org/docs/latest/design/processes.html)
    
* [Clustered deployment · Apache Druid](https://druid.apache.org/docs/latest/tutorials/cluster.html)
    
* [Metadata storage · Apache Druid](https://druid.apache.org/docs/latest/dependencies/metadata-storage.html)
    
* [ZooKeeper · Apache Druid](https://druid.apache.org/docs/latest/dependencies/zookeeper.html)
    
* [Deep storage · Apache Druid](https://druid.apache.org/docs/latest/dependencies/deep-storage.html)
    

## Find out what it's for

Take a look at these videos, where you can learn a little more about other technologies that are often used alongside Druid and why.

* Video - [Incoming Data](https://youtu.be/dmhbnJTlnt8?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)
    
* Video - [Druid Ecosystem](https://youtu.be/CgB-unmWGOs?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)
    

If you're already tired of my voice (!!) look at this, where there are tonnes of cool videos from people in the community that use Druid. It's nearly carved up into aligned technologies so you can find something you're using in your real-time analytics pipeline (like Apache Kafka) and see what they're doing with it.

* Imply's Druid [developer resource center](https://docs.imply.io/latest/developer/dev-resources/)
    

As well as videos you'll find on the resource center, the docs also have some pages on how Druid differs from other database technologies. Start your reading by looking at Druid versus Elastic.

* [Druid versus...](https://druid.apache.org/docs/latest/comparisons/druid-vs-elasticsearch.html)
    

## Learn what Druid ingestion does

Segments are a fundamental concept in Druid. You need to know how they're created, where they go, and how they're used at query time.

This recording of a talk by Gian Merlino will help you understand how this special data format ends up being so important at query time.

* Video: [Inside Apache Druid's Storage and Query Engine](https://www.youtube.com/watch?v=qSJ8_Lc1oAY)
    

This series of videos from Sergio Ferragut goes into detail on how source data will get split up by Druid at ingestion time, and the different options that you have.

* Video: [Notebooks on Apache Druid partitioning](https://www.youtube.com/playlist?list=PLDZysOZKycN4wNrNUpUhfXLP8Q___5omG)
    

You can't escape me, either! Here's my video on segment optimization.

* Video: [Optimize your segments](https://youtu.be/kHH3oPqPGCw?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)
    

Here are some key docs for you to look at:

* [Segments · Apache Druid](https://druid.apache.org/docs/latest/design/segments.html)
    
* [Native ingestion](https://druid.apache.org/docs/latest/ingestion/ingestion-spec.html) / [SQL-based ingestion](https://druid.apache.org/docs/latest/multi-stage-query/index.html)
    
* [Partitioning · Apache Druid](https://druid.apache.org/docs/latest/ingestion/partitioning.html)
    
* [Segment size optimization · Apache Druid](https://druid.apache.org/docs/latest/operations/segment-optimization.html)
    

## Now fold in query wisdom

At the time of writing, by default, Druid has a fan-out / fan-in approach to parallelising `SELECT` query execution. That makes certain queries *very* fast.

Learn what a good query pattern looks like in Druid. You'll begin to understand why data layout and data modelling is so important to query execution speeds - let alone providing enough infrastructure.

* Video: [Aim for sub-second queries](https://youtu.be/chnZmngXMsQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)
    

Many people might also skip understanding how approximation works in Druid, and how you can use it to your advantage. But [Apache Datasketches](https://datasketches.apache.org/) are a really important Computer Science technique to evaluate and to employ. As well as checking out "datasketches"-tagged videos in the Developer Resource Center, check out this video:

* Video [Approximation](https://youtu.be/fSWwJs1gCvQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)
    

It's also now a good time to think about how many `TABLE`s you may want to have in Druid, and how they get created.

* Video [Plan your Druid table datasources](https://youtu.be/OpYDX4RYLV0?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR)
    

Here's some useful docs links:

* [Configuration reference - Task Affinity · Apache Druid](https://druid.apache.org/docs/latest/configuration/index.html#worker-select-strategy)
    
* [Tutorial: Configuring data retention · Apache Druid](https://druid.apache.org/docs/latest/tutorials/tutorial-retention.html)
    
* [Druid SQL overview – UNION · Apache Druid](https://druid.apache.org/docs/latest/querying/sql.html#union-all)
    
* [TopN queries · Apache Druid](https://druid.apache.org/docs/latest/querying/topnquery.html)
    
* [Data rollup · Apache Druid](https://druid.apache.org/docs/latest/ingestion/rollup.html)
    
* [SQL scalar functions · Apache Druid](https://druid.apache.org/docs/latest/querying/sql-scalar.html#sketch-functions)
    

## Set yourself up to debug and monitor

Over on the Druid Faculty you'll find two courses that will help you understand how to configure, store, and use Druid monitoring information – logs and metrics.

* [Druid Faculty](https://learn.imply.io) - Logs / Metrics courses
    

## Join the community

The Apache Druid community welcomes you! The Slack channel is particularly active, and it's got not just other users, but actual code and docs committers present. Go over to the main Community page to get links to all the things...

* [Druid Community](https://druid.apache.org/community)
    

Whether you've got a question about an error or just want to know whether your idea for using Druid is a fit, people there will be super happy to help you.

The main website for Druid also lists upcoming meetup events - and you can also find them by searching meetup.com for events tagged with Apache Druid.

## Get a little bit of data in

It can be quite tempting to just take the plunge and ingest a tonne of data into Druid. But I'd suggest taking just a sample of your own data, or generating some sample data, to get you through a modelling exercise. The best place to understand the process is the Druid Faculty course on Data Modelling and Ingestion:

* [Druid Faculty](https://learn.impy.io) - Data Modelling and Ingestion
    

Now you're set for getting into the Slack channel and starting to build out your tables and your cluster!

And on starting the next part of the journey, take a detour onto my blog article on [Druid POCs](https://pmio.hashnode.dev/notes-from-apache-druid-pocs).