---
title: "Support models in tech communities"
datePublished: Fri Apr 21 2023 10:25:30 GMT+0000 (Coordinated Universal Time)
cuid: clgqeo93p000g09mqfebmhu5u
slug: support-models-in-tech-communities
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/-2vD8lIhdnw/upload/3751aa421d70d947c2548d8787321609.jpeg
tags: devrel, apachedruid

---

My team is passionate about supporting the Apache Druid community. We are driven to improve the overall community support experience. In 2022, a group of community members got together to assess what it was like, and to think about how things could be better. In this post, I share our story.

## Step 1: Defining what "support" means

I'm a stickler for defining what words mean. And yes, I'm also a bit of a grammar fiend, I'm afraid! I personally wanted everyone to be clear about what the term "support" really meant. [Taz Chaudhry](https://www.linkedin.com/in/tahira-c-989a0642/) and [Caroline Harris](https://www.linkedin.com/in/caroline-harris-04783550/) (awesome support leaders I've worked with for many years) helped develop an answer to that fundamental question.

Being fans of [ITIL](https://en.wikipedia.org/wiki/ITIL), we didn't re-invent the wheel. We quickly worked up a table of what we felt support was - and how it is different depending on the circumstances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682065318253/7bc9ec53-df4c-4de5-9bcf-a7d18b7a0558.png align="center")

Now we could ask *who*, in the community, was involved in each tier of support. What kinds of community members are likely to be in demand? Where are they? What are their motivations? What barriers are there to them being in on the action?

I'm happy to say that when we had those conversations inside our own company, it rallied everyone around one of our company's core mission statements:

> "Make it as easy as possible for people to use Druid and build awesome data applications on top of it".

## Step 2: Understanding where it happens

Each Apache [PMC](https://projects.apache.org/projects.html) states its preferred channels of communication on its project website. This sets an expectation, especially for people involved in or using Apache projects like Druid.

> ...to coordinate the development of their software and administer their organization \[and\] as a primary support channel where users can help each other learn to use the software. … If you have a technical question of any kind, the best place to ask is the user@ or dev@ list for the relevant project.

These [mailing lists](https://www.apache.org/foundation/mailinglists.html) are [public](https://www.apache.org/foundation/public-archives.html) – and people should expect them to be so - because:

> ...they serve as both a public historical record and a searchable repository of our activities and decisions.

The Apache Druid PMC [published lists of channels](https://druid.apache.org/community/) for Druid, starting with the *developer* mailing list “for discussion about project development” and the *user* mailing list “for general discussion, questions, and announcements”. In that respect, the demands and expectations from Druid community members is the same as every Apache project:

> I need somewhere to get solutions when I'm stuck, and I need to be able to suggest / propose changes to the code.

There are additional channels for the Druid community too, including a Slack channel and Github to “report issues and problems, or suggest new features”.

Thanks to the group's model of tiered support, we could categorise the channel based on the type of questions and problems they were raising.

The clarity this brought can't be understimated!

We reached a consensus that the Druid Slack troubleshooting channel was *at least* Tier 2. And we found that Google Groups conversations (the main user mailing list) were usually Tier 1. And while people were expecting Github issues to be Tier 3, we found a lot of Tier 1 issues, with people just wanting some tutoring.

But we didn't just want to stop there. The Druid community had been through a period of rapid growth, and we wanted to find out whether the community as a whole needed to be in better places at a better time.

## Step 3: Learn from peers

We peeked out of the window and looked at what other communities were doing to create an "environment of goodwill" where people felt able to ask questions and help one another be successful.

Of course, communities don't always just stick to the user and dev mailing lists. Amongst the projects we checked at the time, Stack Overflow was the most prevalent "additional" channel, followed by Slack.

* Apache Airflow’s PMC use [Github Discussions](https://github.com/apache/airflow/discussions/) and [StackOverflow](https://stackoverflow.com/questions/tagged/airflow) with the usual user lists
    
* Apache Beam also uses [user](https://lists.apache.org/list.html?user@beam.apache.org) lists along with [StackOverflow](https://stackoverflow.com/questions/tagged/apache-beam) and [Slack](https://s.apache.org/beam-slack-channel)
    
* Apache Drill has [Slack](https://join.slack.com/t/apache-drill/shared_invite/enQtNTQ4MjM1MDA3MzQ2LTJlYmUxMTRkMmUwYmQ2NTllYmFmMjU4MDk0NjYwZjBmYjg0MDZmOTE2ZDg0ZjBlYmI3Yjc4Y2I2NTQyNGVlZTc) and [user](http://mail-archives.apache.org/mod_mbox/drill-user/) lists
    
* Apache OpenOffice has a [forum](https://forum.openoffice.org/en/forum/) in addition to user lists.
    
* Solr has [user](https://lists.apache.org/list.html?users@solr.apache.org) lists, [IRC](https://solr.apache.org/community.html) (IRC, I miss you!!), and a dev-only [Slack](https://the-asf.slack.com/messages/CE70MDPMF) channel.
    
* Apache Arrow use [user](https://lists.apache.org/list.html?user@atlas.apache.org) lists only
    

And then open-core companies often sponsor channels themselves. And some of those channels also have open-source support under their umbrella.

* For Cassandra, we found that their PMC have [user](mailto:user-subscribe@cassandra.apache.org) lists as well as [StackOverflow](http://stackoverflow.com/questions/tagged/cassandra) and [Slack](https://s.apache.org/slack-invite) – DataStax itself have a separate public [forum](https://community.datastax.com/index.html) covering both Cassandra and Datastax
    
* Apache Kafka has [user](https://lists.apache.org/list.html?users@kafka.apache.org) lists, [IRC](https://botbot.me/freenode/apache-kafka/) (inactive?), and [Google User Groups](http://groups.google.com/group/kafka-dev) (inactive?), with [Confluent](https://www.confluent.io/community/ask-the-community/) running a [forum](https://forum.confluent.io/?src=dp&_ga=2.65008044.263246500.1655880213-1529595238.1655277929) and [Slack](https://launchpass.com/confluentcommunity) channel in addition that covers both Kafka and Confluent
    

Some separate open-source support from their own product support:

* Apache Spark recommends [StackOverflow](https://stackoverflow.com/questions/tagged/apache-spark) as first port-of-call, and also has a [user](https://lists.apache.org/list.html?user@spark.apache.org) list - and Databricks has its own public [forum](https://community.databricks.com/) very much focused on Databricks
    
* Apache CouchDB’s PMC has both [IRC](https://web.libera.chat/#couchdb) and Slack, as well as the usual [user](https://lists.apache.org/list.html?user@couchdb.apache.org) lists – with Couchbase adding a public [forum](https://forums.couchbase.com/), focused on Couchbase.
    

And we found that some third parties keep their sponsored support forums private:

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

Now we had a sense of what tooling people were using. What things were common. What they were using them for. And we could come up with some ideas of what might (and might not!) work. Not just as a "standard" set, but also with our joint knowledge of geo-specific needs our own community might have.

## Step 4: Planning for action

We started by thinking about usage in each tier. And not just the community's own channels, but any that our company was sponsoring. We got involved in the conversations, yes, but we also stepped back. We wanted to know what value the community members themselves felt that they added. We wondered whether people even *knew* about the channels – and what they were for. How did people get there? Was it easy to register? (At the time, the answer when it came to the Slack channel was "no"!)

(Cue a Channel Access Strategy!)

The working group put a lot of effort into collecting and analysing data. We assessed traffic levels per channel, reply rates and response times, channel join and drop-off rates, even did a 3-month analysis of 5 years worth of conversations to find key categories of issue!

We were able to arm the community itself with a tome of data so that together we could come up with rational, actionable ideas of how to make the experience better for everyone.

Now we were ready to share what we'd learned.

## Step 5: Inspire change

Led by one of the team's advocates, [Mark Herrera](https://www.linkedin.com/in/mark-anthony-herrera-337259225/), we started talking to key community stakeholders and influencers.

For tier 0, for example, we spoke with a Druid docs committer [Charles Smith](https://www.linkedin.com/in/charlesosmith/). We talked about how we, as community members, could all help improve the docs to better support a user's journey. And what activity might improve rates of contribution.

For tier 1, we engaged with curriculum engineer [Steve Halladay](https://www.linkedin.com/in/steve-halladay-63b1441/) about the kinds of [training courses](https://learn.imply.io) that people might be able to refer to on a topical basis. That inspired a huge amount of work in common themes in Tier 1 support.

And armed with our knowledge that Slack was a Tier 3 channel, we engaged with the project's own committers and contributors. We wanted them to increase their involvement in Slack. And let me tell ya, that change has been critical! Having those highly experienced people in Slack has turned it into a place where even the most complex questions can be answered.

Yes, all of this we were able to do in a data-driven way. But it would **not** have happened had people not believed in the importance of helping one another. As Mark put it, of "generating goodwill". This is such an inspiring part of working in the Apache Way. When you see people wanting to hold one another's hand, spending their own time to be there for one another – well, it's just cool as hell :)

But let me just be a bit selfish and personal here about what I got out of all this.

As a team invested in people's success with Druid, this project and the action plans and coalitions it created continues to help me as a DevRel Director. As a community member myself, managing a team of advocates and content writers, I know how I can help the community. How I can personally participate in improving people's support experience. And I feel now like the importance of checking and continually improving the support experience in our own community has been elevated.

And again – what an inspiring journey I've been on with this group. Woohoo for the Apache Druid Community!