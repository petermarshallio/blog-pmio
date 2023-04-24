---
title: "A capabilities map for Apache Druid®"
seoDescription: "Increase the chances of succeeding with real-time analytics projects using the SFIA framework to assess your team's capabilities."
datePublished: Mon Apr 24 2023 09:02:58 GMT+0000 (Coordinated Universal Time)
cuid: clgum1obd000f08l9cgsi0k7i
slug: a-capabilities-map-for-apache-druid
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/1K8pIbIrhkQ/upload/3283eedfa4d5f68861b7b655b6d9b136.jpeg
tags: apachedruid, sfia

---

**It's great that developers can freely use** [**Apache Druid**](https://druid.apache.org)**. If your solutions architect is interested in experimenting with this new type of database, you can create real-time analytics pipelines using anything from IoT data from bee hives to trading data. When you decide it's time for managers to be involved, be prepared with a list of capabilities you need for your idea to succeed ahead of time.**

As an ex-architect, this problem is very familiar: I've found some awesome new tech, but my Head of IT goes and asks me to check if it's feasible to implement it. What a party-pooper!

A while ago I discovered [The Skills for the Information Age](https://sfia-online.org/en). The SFIA is a not-for-profit skills framework in use in 180 countries around the world and translated into 10 languages, adopted by many organisations including the IEEE. It's a wonderful tool for capability maturity assessment and improvement.

Using SFIA you can proactively assess the feasibility of implementing any technology. You'll find people incorporating formal skill-level assessments it into formal project feasibility reports on some tech-or-other because it pre-arms managers to objectively assess capabilities needed. Once sold on needing to use something, you can make people ready to find gaps and plan for team development.

So let's get going with my findings for Apache Druid!

## Real-time analytics journey

I see the community of Apache Druid adopters – and I dare say all real-time analytics pipeline adopters – going through the activities below. This isn't earth-shattering – you'll recognise this list immediately because your PMO probably has one very similar. And you'll see how close this list is to the DevOps way of the world.

I'm presenting it this way purely as an abstraction. It helps aggregate the list of SFIA capabilities into something less like a massive spreadsheet! Align them with your local methodology.

| **Stage** | **Description** |
| --- | --- |
| **Design** | Defining the data pipeline, noting all the building blocks required, noting not only how they will be realised, but how and which data objects will flow through that pipeline and with what size, shape, and regularity. |
| **Deployment** | Manually or with automation, assigning Apache Druid components and configurations to the infrastructure - including network services, routing and firewall configuration, and encryption certificates - along with the three Druid dependencies: deep storage, Zookeeper, and a metadata database. |
| **Development** | Using the features of Apache Druid within the pipeline to achieve the desired design. |
| **Transition** | Hardening and additional tasks you would associate with good service transition, from defining OLAs / SLAs to training and educating your target audience. |
| **Operation** | Monitoring, support and maintenance of the transitioned production system to meet SLAs. |

Development is where the functionality of your real-time analytics database gets applied, which is why all the above become iterative, not sequential. As the dialogue between the user and the engineer evolves during the development stage, you'll pop in and out of each activity.

For this exercise, I've summarised the functionality of Apache Druid<sup>®</sup> into three areas.

| **Behaviour** | **Description** |
| --- | --- |
| **Ingestion** | Defining ingestion tasks that will bring statistics-ready data into Druid from storage and delivery services, (including schema, parsing rules, transformation, filtering, connectivity, and tuning options) and ensuring their distributed execution, led by the overlord, is performant and complete. |
| **Data Management** | Led by the coordinator, replication and distribution of the ingested data according to rules, while allowing for defragmenting (“compact”), reshaping, heating / cooling, and deleting that data. |
| **Querying** | Programming SQL / Druid Native code executed by the distributed processes that are led by the broker service (possibly via the router process) with security applied. |

## Capabilities

### Learn first

By whatever route Druid became your focus, from strategic [Innovation](https://sfia-online.org/en/sfia-7/skills/innovation), an IT department’s [Emerging Technology Monitoring](https://sfia-online.org/en/sfia-7/skills/emerging-technology-monitoring), a team’s [Business Process Improvement](https://sfia-online.org/en/sfia-7/skills/business-process-improvement) assessments, a desire for better [Knowledge Management](https://sfia-online.org/en/sfia-7/skills/knowledge-management), or failings identified through [Service Level Management](https://sfia-online.org/en/sfia-7/skills/service-level-management), there are some essential skill-holders you should try and find and work with throughout your process.

The [Knowledge Management](https://sfia-online.org/en/sfia-7/skills/knowledge-management) mission is a common goal for Apache Druid® deployments, whether that is opening up broad datasets to those who cannot current access them, or providing self-service analytics to alleviate the pressure on your analytics teams.

> “capturing, sharing, developing and exploiting the collective knowledge of the organisation to improve performance, support decision making and mitigate risks”

If you can find someone assigned this specific role in your organisation, they will become a pivotal member of your change coalition.

When developing apps on top of Druid, especially, take care to identify those with skills in [Product Management](https://sfia-online.org/en/sfia-7/skills/product-management), [Software Design](https://sfia-online.org/en/sfia-7/skills/software-design), [Systems Design](https://sfia-online.org/en/sfia-7/skills/systems-design), and [Systems Development Management](https://sfia-online.org/en/sfia-7/skills/systems-development-management).

Take advantage of [User Research](https://sfia-online.org/en/sfia-7/skills/user-research) and those with [User Experience Analysis](https://sfia-online.org/en/sfia-7/skills/user-experience-analysis) skills both to bolster your case for change and to design a vision that everyone can buy into. They are also very likely to give you an objective view of how your product needs to change to make life better for your users.

And if you’re handling a streaming telemetry data set - especially if it’s from your product - find that knowledgeable individual who is engaged in [Real-time / Embedded Systems Development](https://sfia-online.org/en/sfia-7/skills/real-time-embedded-systems-development) early, ensuring that you share their vision for Druid’s use.

As you move forward, the usual raft of [IT Management](https://sfia-online.org/en/sfia-7/skills/it-management), [Project Management](https://sfia-online.org/en/sfia-7/skills/project-management) and [Requirements Definition and Management](https://sfia-online.org/en/sfia-7/skills/requirements-definition-and-management) is going to be essential.

Remember to also look out for people who have [Change Implementation Planning and Management](https://sfia-online.org/en/sfia-7/skills/change-implementation-planning-and-management) skills: the greater your inspiration to create Apache Druid-inspired changes, the more this skill matters.

Finally, do not forget the people you’re trying to help. Polishing up on your team’s acuity in [Relationship Management](https://sfia-online.org/en/sfia-7/skills/relationship-management) can never be a bad thing.

### Design

Whether your designs for improvement are large or small, it’s always a good idea to engage with someone who has skills in [Solution Architecture](https://sfia-online.org/en/sfia-7/skills/solution-architecture). That person will hold a singular holistic view of how Apache Druid will be deployed, developed, operated, governed (strategies, policies, standards), secured, and put into production in a pipeline.

Often forgotten is the need for [Network Design](https://sfia-online.org/en/sfia-7/skills/network-design). In today’s cloud-connected world, you must find someone who can work out how data will be ingested into Druid, and how it will get back out again to your querying application - not in software, but along pieces of wire or some other networking media. They will have views on the use of network services to improve availability and ensure security and are positioned well to inform you about any costs associated with data movement of the scale that is associated with real-time analytics pipelines. Even the sketch of a [Network Plan](https://sfia-online.org/en/sfia-7/skills/network-planning) is an important communication tool for everyone.

Engage early with those people skilled in [Analytics](https://sfia-online.org/en/sfia-7/skills/analytics), [Data Visualisation](https://sfia-online.org/en/sfia-7/skills/data-visualisation) and [User Experience Design](https://sfia-online.org/en/sfia-7/skills/user-experience-design) to specify the result of your work. Having mock-ups of the output you need from Druid will define not only your ingestion and query requirements but the performance requirements of your underlying infrastructure.

It is always useful to have someone skilled in [Information Governance](https://sfia-online.org/en/sfia-7/skills/information-governance) at your side.

> “how all types of information, structured and unstructured, whether produced internally or externally, are used to support decision-making, business processes and digital services”

Someone with this skill will warn you when some data you’re going to open up or make available is subject to legislation or policy.

### Deploy

Deployment is the top “non-Druid” challenge for new adopters and long-standing users alike. Identify people that will not only create your infrastructure and network but also deploy the runtime and actual code to spin up the cluster.

Start by identifying those skilled in [IT Infrastructure](https://sfia-online.org/en/sfia-7/skills/it-infrastructure). They need to determine the “physical or virtual hardware, software, network services and data storage” required for Apache Druid - both itself and its dependencies. They need to become familiar with how to scale each constituent part horizontally and vertically, and how to [monitor](https://learn.imply.io/apache-druid-metrics) the load and performance of those components.

Druid is a Java-based [micro-services, shared-nothing database](https://youtu.be/2Ft-0CFkcgE?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR). Each process runs in a compatible JRE running in a compatible operating system. Beyond that, there are dependencies on [Zookeeper](https://druid.apache.org/docs/latest/dependencies/zookeeper.html), a compatible [metadata database](https://druid.apache.org/docs/latest/dependencies/metadata-storage.html), a suitable location for log files, (optionally) a [metrics](https://learn.imply.io/apache-druid-metrics) sink for your chosen [emitter](https://druid.apache.org/docs/latest/development/extensions.html) (essential for monitoring), as well as a compatible [deep storage](https://druid.apache.org/docs/latest/dependencies/deep-storage.html) system. This is all aside from your chosen infrastructure management system like Kubernetes, Ansible, or Terraform, and, of course, those services provided by your infrastructure provider.

That means you need someone with [specialist](https://sfia-online.org/en/sfia-7/skills/specialist-advice) knowledge in all these areas – not just Apache Druid. Many first-timers are caught off guard by the need to wisely configure and monitor the JRE for each process and to effectively monitor and resolve issues with Zookeeper - especially internode communication and memory allocation.

Find out who in your team is skilled in [Systems Installation & Decommissioning](https://sfia-online.org/en/sfia-7/skills/systems-installation-decommissioning) and [System Software](https://www.sfia-online.org/en/framework/sfia-7/en/framework/sfia-7/skills/service-management/service-operation/system-software). They'll need to understand and carry out all aspects of the deployment. They need to understand each moving part, especially in larger deployments, and [how performance is affected by infrastructure](https://youtu.be/chnZmngXMsQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR). And to that point, consider brushing up on your [Release & Deployment](https://sfia-online.org/en/sfia-7/skills/release-and-deployment) to guarantee complete, consistent, and safe deployments.

Remember to find the person who will be providing [Network Support](https://sfia-online.org/en/sfia-7/skills/network-support) to you as you go through your journey. They will quickly answer questions and resolve problems that you believe could be due to network communication issues into and out of the Druid cluster, as well as between processes. If you are using a containerised environment, make sure they know how to set up communication channels between the containers and each other as part of your overall design.

When it comes to the software itself, someone must know the [configuration options](https://druid.apache.org/docs/latest/configuration/index.html) for Druid, perhaps applying version control, comparing configurations to understand different performance profiles, and allowing you to standardise your environments. In other words, good [Configuration Management](https://sfia-online.org/en/sfia-7/skills/configuration-management). Runtime properties for Apache Druid and the JREs are all configurable. And in a mission-critical deployment, you might even consider a query, data management, and ingestion as individual configuration items.

And last but not least, think about pointing those with skills and opinions on [Availability Management](https://sfia-online.org/en/sfia-7/skills/availability-management) to the Apache Druid documentation. Measuring the availability of each component against targets (and establishing what those targets are) should start early, informing what you will deploy and use to monitor health and performance. Your team needs to know how much of Druid can be “unavailable” before it’s truly unavailable (e.g. redundancy and replication), to know where to collect state information about services, interfaces, and data, the tools they need to test and carry out disaster recovery, and building out a way to plan for maintenance in what will quickly become a Zero Downtime service.

### Development

First, a warning. Avoid becoming a [superhero](https://dzone.com/articles/recognizing-and-curing-superhero-syndrome) of Druid development. *Never* be the only person who owns *everything* in your Druid-powered real-time analytics pipeline! Take this opportunity to work out who will be in *your* close-knit team to work through issues together. And join the [community](https://druid.apache.org/community/) from the start, of course!

Using [Database Design](https://sfia-online.org/en/sfia-7/skills/database-design) and [Data Modelling & Design](https://sfia-online.org/en/sfia-7/skills/data-modelling-and-design) will help you work out how what may be quite complex [data sources](https://youtu.be/OpYDX4RYLV0?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) will be [ingested into, stored, and queried from within Druid](https://youtu.be/dmhbnJTlnt8?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR). And, importantly, how that data holds value for the business. Make sure they've understood the approach to [modeling](https://learn.imply.io/apache-druid-ingestion-and-data-modeling) in Druid to get the speed boost you're promising them.

And critically, make sure *everyone* understands that you're building an event-based analytics offering – not just a faster data warehousing solution. We're talking about OLAP on time-based data at super-fast speeds – not making OLTP better.

Together you can make informed decisions and recommendations about where your data in Druid will come from, how (and where) it needs to be prepared for statistical analysis (e.g. cleansing, filtering, transforming, enriching) and ultimately what it must look like when it’s made available for query. Prepare yourself by understanding what other UIs people have built on Druid, and [what makes them different](https://pmio.hashnode.dev/apache-druid-powered-analytics-applications).

It is dangerous, especially if your goal is self-service analytics, to leave this up to experimentation, hoping your users will get what they want because you’ve given them direct access to a self-service cheesecake much faster and with more filling. Knowing the intrinsic value of the data you’re going to make available will show that you are using Apache Druid for everyone’s benefit, and not just because you like cheesecake.

If your process of bringing data into Druid is complex or accuracy and transparency are essential, consider finding someone skilled in [Information Assurance](https://sfia-online.org/en/sfia-7/skills/information-assurance) to give your users confidence that the data they’re seeing is reliable and trustworthy. This can be essential if you decide to introduce [approximate aggregations](https://youtu.be/fSWwJs1gCvQ?list=PLDZysOZKycN7MZvNxQk_6RbwSJqjSrsNR) like HyperLogLog, Thetasketch, and Approximate Quantiles.

Much of the information about what Druid is doing is exposed in the main console. This will be of utmost interest to people skilled in [Database Administration](https://sfia-online.org/en/sfia-7/skills/database-administration). After all, Druid is a database - and to run a database you need DBA skills!

Knowing the moving parts of Apache Druid’s database, as well as the system schema tables, allows you to understand whether Druid is well-configured and operating well. As well as understanding functionality for data definition, manipulation, and control, it becomes important to know how to carry out the usual gamut of DBA operational jobs: interpreting the myriad of [log](https://learn.imply.io/apache-druid-logs) files from the distributed processes (perhaps the #1 skill of all!), how to apply information management policies, what conditions can lead to database-level locking, how to take backups, and so on.

As soon as you ingest data into Druid, you will start to think about effective [Storage Management](https://sfia-online.org/en/sfia-7/skills/storage-management). Druid’s tables must be designed to account for legal and policy compliance, availability requirements, and performance. It’s important to know how data can be isolated and protected, how tiering can be used, how disk traffic (initial load, rebalance, segment numbers, segment size) and disk types (DAS / NAS / SAN) affect throughput, what options there are for encryption at rest, and how datastores are made resilient and exactly what process will be followed to recover in face of disaster. This doesn’t mean just Deep Storage, but also the local segment caches on Historical processes, any log4j log stores, and so on.

There are three [Programming & Software Development](https://sfia-online.org/en/sfia-7/skills/programming-software-development) languages in Druid: SQL, Javascript, and Java, allowing querying, user-defined functions in a number of areas, and understanding / contributing to the underlying open source Java code. In particular, as regards Java, being able to look at - and contribute to - the code of Druid is always welcome by the community.

Understanding how you carry out [Security Administration](https://sfia-online.org/en/sfia-7/skills/security-administration) through Druid’s authentication, auditing, and authorisation capabilities could prove critical to your overall architectural design. Gain knowledge in these areas quickly and ensure you create a solution that complies with all manner of compliance requirements. You may find that you need extra components in your design to take care of things that your chosen database cannot do out-of-the-box.

### Transition

You need a team that's good at [Testing](https://sfia-online.org/en/sfia-7/skills/testing) in support of [Service Acceptance](https://sfia-online.org/en/sfia-7/skills/service-acceptance) activities. But have you worked out how you will do this testing in a Druid pipeline? What will their criteria be in all aspects of the design? What approach will you use? What tools (e.g. JMeter)? Herewith then a recommendation for good and well-prepared testing and service acceptance resources in your team.

As Druid is so awesome (!) the data you make available for analysis is bound to grow in depth and breadth. Good [Capacity Management](https://sfia-online.org/en/sfia-7/skills/capacity-management) ensures you can meet current and forecast needs in a cost-efficient manner, and can make evidence-based recommendations about future investment. To do this they need to understand the key measures of a cluster, including raw versus stored data sizes, query execution time, ingestion lag, data latency (especially for streaming ingestion), indexing throughput, real-time-to-historical query ratios, cache hit rates, and (of course) data quality indicators.

### Operate

Finally, you are ready to launch! Make sure that you have covered all your bases for support: [Application Support](https://sfia-online.org/en/sfia-7/skills/application-support), [Problem Management](https://sfia-online.org/en/sfia-7/skills/problem-management), and [Incident Management](https://sfia-online.org/en/sfia-7/skills/incident-management) - amongst others of course.

But don’t forget upgrades. Apache Druid releases are frequent, and each one brings with it performance and usability enhancements as well as fixes. Make sure you have a team around you that can identify whether that next release will bring value, and that they know exactly what they’re doing when they want to upgrade.

## Conclusion

The list of capabilities needed to build a real-time analytics pipeline may look massive, but in reality, you'll find them – or at least the desire to have them – already exists. Else you wouldn't be looking at real-time analytics databases in the first place!

The SFIA provides is an objective way of assessing your team's IT skills. When applied to real-time analytics projects, it pre-arms you with knowledge, and a starting point for negotiation.

Ultimately, it elevates you as an innovator.