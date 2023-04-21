---
title: "Support models in tech communities"
datePublished: Fri Apr 21 2023 10:25:30 GMT+0000 (Coordinated Universal Time)
cuid: clgqeo93p000g09mqfebmhu5u
slug: support-models-in-tech-communities
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/-2vD8lIhdnw/upload/3751aa421d70d947c2548d8787321609.jpeg
tags: devrel, apachedruid

---

My team is passionate about supporting the Apache Druid community. We are driven to improve your overall experience. In this post, I share a story of understanding and honing community support in the hope that it will provide some useful resources in your own DevRel journey.

## Step 1: Defining what "support" means

I'm a stickler for defining what words mean. And yes, I'm also a bit of a grammar fiend, I'm afraid! I wanted everyone to be clear what the term "support" really meant to us as a group. [Taz Chaudhry](https://www.linkedin.com/in/tahira-c-989a0642/) and [Caroline Harris](https://www.linkedin.com/in/caroline-harris-04783550/) (awesome support leaders I've worked with for many years) helped develop an answer to that fundamental question: "what does support for our open source community look like?"

I'm a bit of a fan of [ITIL](https://en.wikipedia.org/wiki/ITIL), so for better or for worse (!) we didn't re-invent the wheel. Using a number of awesome resources (like this [blog from BMC Software](https://www.bmc.com/blogs/support-levels-level-1-level-2-level-3/)) we quickly worked up a table of what we felt support was - and more than that, how it is different depending on the circumstances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682065318253/7bc9ec53-df4c-4de5-9bcf-a7d18b7a0558.png align="center")

Now we could start to clear up what people meant by "open source support", and ask *who* was involved in each of the levels of support. I'm happy to say that the outcome of those conversations re-affirmed to all of us that Imply's mission remains the same:

> "Make it as easy as possible for people to use Druid and build awesome data applications on top of it".

## Step 2: Understanding the demand

Each Apache [PMC](https://projects.apache.org/projects.html) states its preferred channels of communication on its project website. This sets an expectation, especially for people involved in or using Apache projects like Druid.

> ...to coordinate the development of their software and administer their organization \[and\] as a primary support channel where users can help each other learn to use the software. … If you have a technical question of any kind, the best place to ask is the user@ or dev@ list for the relevant project.

These [mailing lists](https://www.apache.org/foundation/mailinglists.html) are [public](https://www.apache.org/foundation/public-archives.html) – and people should expect them to be so - because:

> ...they serve as both a public historical record and a searchable repository of our activities and decisions.

The Apache Druid PMC [published lists of channels](https://druid.apache.org/community/), starting with the *developer* mailing list “for discussion about project development” and the *user* mailing list “for general discussion, questions, and announcements”. In that respect, the demands and expectations from Druid community members is the same as every Apache project: "I need somewhere to get solutions when I'm stuck, and I need to be able to suggest / propose changes to the code".

There are additional channels for the Druid community too, including a Slack channel and Github to “report issues and problems, or suggest new features”.

Thanks to our model of tiered support, we could then try and categorise the levels of support people were asking for and expecting, based on the channel that they used.

The clarity that brought can't be understimated!

We reached a consensus that Slack was *at least* Tier 2. And we found that Google Groups conversations (the main user mailing list) were usually Tier 1. Github issues on the other hand, were expected to be Tier 3, but sometimes were more like Tier 1 (people wanting expert help).

Next, we wanted to find out what channels other open core companies had. We'd been through a period of creativity (go startups!) and of rapid growth. We needed to be focused and to use our resources wisely. So we put our heads above the parapet and researched what other open-core companies were doing to create an "environment of goodwill" where people felt able to ask questions and to help one another be successful.

## Step 3: Learn from peers

Amongst the projects we checked at the time, Stack Overflow was most prevalent, followed by Slack. The added bit of schmungle (new word) to this is that open-core companies often sponsor other channels, aside from the "official" ones.

* Apache Airflow’s PMC use [Github Discussions](https://github.com/apache/airflow/discussions/) and [StackOverflow](https://stackoverflow.com/questions/tagged/airflow) with the usual user lists
    
* Apache Beam also uses [user](https://lists.apache.org/list.html?user@beam.apache.org) lists along with [StackOverflow](https://stackoverflow.com/questions/tagged/apache-beam) and [Slack](https://s.apache.org/beam-slack-channel)
    
* Apache Drill has [Slack](https://join.slack.com/t/apache-drill/shared_invite/enQtNTQ4MjM1MDA3MzQ2LTJlYmUxMTRkMmUwYmQ2NTllYmFmMjU4MDk0NjYwZjBmYjg0MDZmOTE2ZDg0ZjBlYmI3Yjc4Y2I2NTQyNGVlZTc) and [user](http://mail-archives.apache.org/mod_mbox/drill-user/) lists
    
* Apache OpenOffice has a [forum](https://forum.openoffice.org/en/forum/) in addition to user lists – but it only covers Open Office.  3rd parties do their own thing.
    
* Solr has [user](https://lists.apache.org/list.html?users@solr.apache.org) lists, [IRC](https://solr.apache.org/community.html) (IRC, I miss you!!), and a dev-only [Slack](https://the-asf.slack.com/messages/CE70MDPMF) channel.
    
* Apache Arrow use [user](https://lists.apache.org/list.html?user@atlas.apache.org) lists only
    

Talking of third-party sponsored support channels, some have open-source support under their umbrella.

* For Cassandra, we found that their PMC have [user](mailto:user-subscribe@cassandra.apache.org) lists as well as [StackOverflow](http://stackoverflow.com/questions/tagged/cassandra) and [Slack](https://s.apache.org/slack-invite) – DataStax itself have a separate public [forum](https://community.datastax.com/index.html) covering both Cassandra and Datastax
    
* Apache Kafka has [user](https://lists.apache.org/list.html?users@kafka.apache.org) lists, [IRC](https://botbot.me/freenode/apache-kafka/) (inactive?), and [Google User Groups](http://groups.google.com/group/kafka-dev) (inactive?), with [Confluent](https://www.confluent.io/community/ask-the-community/) running a [forum](https://forum.confluent.io/?src=dp&_ga=2.65008044.263246500.1655880213-1529595238.1655277929) and [Slack](https://launchpass.com/confluentcommunity) channel in addition that covers both Kafka and Confluent
    

Yet others fully separate open-source support from their own product support:

* Apache Spark recommends [StackOverflow](https://stackoverflow.com/questions/tagged/apache-spark) as first port-of-call, and also has a [user](https://lists.apache.org/list.html?user@spark.apache.org) list - and Databricks has its own public [forum](https://community.databricks.com/) very much focused on Databricks
    
* Apache CouchDB’s PMC has both [IRC](https://web.libera.chat/#couchdb) and Slack, as well as the usual [user](https://lists.apache.org/list.html?user@couchdb.apache.org) lists – with Couchbase adding a public [forum](https://forums.couchbase.com/), focused on Couchbase.
    

We found that some keep their support forums entirely private:

* Apache Superset has the usual user [list](https://lists.apache.org/list.html?dev@superset.apache.org) plus [Slack](https://join.slack.com/t/apache-superset/shared_invite/zt-16jvzmoi8-sI7jKWp~xc2zYRe~NqiY9Q) and [StackOverflow](https://stackoverflow.com/questions/tagged/superset+apache-superset), with Preset adding a private area on their website.
    
* Apache Pulsar has [user](https://lists.apache.org/list.html?users@pulsar.apache.org) lists and [Slack](https://apache-pulsar.slack.com/) and WeChat, but for technical help recommends [StackOverflow](https://stackoverflow.com/tags/apache-pulsar).  StreamNative a private login [area](https://auth.streamnative.cloud/u/login/identifier?state=hKFo2SBFMTlBbGxDc1lwMzNIZWhkOUVzUmhYSEhMcG9qSlYxOKFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIHlLSE1zSHY1ZlpIVTVuNTlwVDYzU2otbm4zRVdwX1VZo2NpZNkgNmVyNzNxS3E0MnFCMHdic3IxU09NYVliYXU3S2hsZXc) on their site.
    

* Veverica have a private login area [for customers](https://www.ververica.com/support), in addition to Apache Flink’s [user](https://lists.apache.org/list.html?user@flink.apache.org) list, [Slack](https://flink.apache.org/community.html#slack), and [StackOverflow](https://flink.apache.org/community.html#stack-overflow)
    
* Apache Ignite have a user list and [StackOverflow](https://stackoverflow.com/questions/tagged/ignite) with the site having a particular focus on developer vs user interactions, and then GridGain have a [private forum](https://support.gridgain.com/) for customers
    

In our space, Pinot and Clickhouse are key community partners. We're all trying to offer the world databases that smash the problems associated with real-time analytics pipelines.

Clickhouse's community support spaces, included Github [Discussions](https://github.com/ClickHouse/ClickHouse/discussions) and [Issues](https://github.com/ClickHouse/ClickHouse/issues), [Slack](https://clickhousedb.slack.com/join/shared_invite/zt-rxm3rdrk-lIUmhLC3V8WTaL0TGxsOmg#/shared-invite/email), [StackOverflow](https://stackoverflow.com/questions/tagged/clickhouse), and [Google User Groups](https://groups.google.com/g/clickhouse). Apache Pinot has the standard [mailing lists](https://docs.pinot.apache.org/community-1/community#mailing-lists) you'd associate with an Apache project, and add [Slack](https://communityinviter.com/apps/apache-pinot/apache-pinot). Startree additionally includes links to Pinot in [StackOverflow](https://stackoverflow.com/questions/tagged/pinot) – but there is no specific forum.

We also took a look at Presto – which we all know has a rather ... complex ... open-source community!

* PrestoDB is aligned with the Presto Foundation (part of the Linux Foundation) and has a [user](https://lists.prestodb.io/g/presto-users) mailing list (but prefers [Slack](https://prestodb.slack.com/)) along with [GitHub Discussions](https://github.com/prestodb/presto/discussions) and, for bugs, [GitHub Issues](https://github.com/prestodb/presto/issues).  (Ahana didn't appear to have any additional community presence at the time.)
    
* Trino is aligned with the Trino Software Foundation and heavily promotes its [Slack](https://join.slack.com/t/trinodb/shared_invite/zt-14ukl212d-98J09w~zC3vAQCgm6I2IxQ) channel.  It has also enabled [Github Discussions](https://github.com/trinodb/trino/discussions). To that, Starburst sponsored a [Trino Forum](https://www.trinoforum.org/) using Discourse and also had a private [portal](https://starburstsupport.force.com/s/login/).
    

And who could ignore Kubernetes?! When we checked, they had a Discourse-powered [forum](https://discuss.kubernetes.io/) along with [ServerFault](https://serverfault.com/questions/tagged/kubernetes) (versus StackOverflow) and a broad (invite-only) [Slack](https://kubernetes.slack.com/) channel.

As community members ourselves, we started to think about the purpose of support channels. What tier did they best suit? Not just the community channels, but also those channels that our company was sponsoring. What value did they add? Did people have access to them? What were the barriers to entry? Did people even *know* about the channels? (Cue a Channel Access Strategy!)

## Step 4: Planning for action

We'd looked at the channels that the [Apache Druid community](https://druid.apache.org/community) promoted, and the places people actually were. We could look at the conversations and work out what level people *thought* they were getting, and what the community itself was offering.

A key tool in the DevRel arsenal was [Common Room](https://www.commonroom.io/). We could assess traffic levels, join and drop-off rates, and overall sentiment. Even do a degree of topical analysis. We were armed with a tonne of data that let the working group recommend how to make the user experience better across all support tiers.

Led by one of the team's advocates, [Mark Herrera](https://www.linkedin.com/in/mark-anthony-herrera-337259225/), we started talking to internal stakeholders.

For tier 0, for example, we spoke with our docs leader [Charles Smith](https://www.linkedin.com/in/charlesosmith/). We planned out how to improve the docs to support a user's journey, and to improve rates of contribution to the docs from across the community.

For tier 1, we engaged our curriculum engineer [Steve Halladay](https://www.linkedin.com/in/steve-halladay-63b1441/) about Imply's [training courses](https://learn.imply.io) on Druid to provide hands-on labs that people could refer on a topical basis.

Armed with our new knowledge that Slack was Tier 3, we engaged with engineering leaders about their involvement in Slack support to tackle the most complex questions that the community of users were throwing up.

And all of this we could do this in a data-driven way, understanding people's experience in each tier, and with a fresh and clear understanding of the channel on which those improvements needed to be made.

As a team invested in people's success with Druid, this project and the action plans and coalitions it created continues to help us make *everyone's* journey with Druid ever-more frictionless.