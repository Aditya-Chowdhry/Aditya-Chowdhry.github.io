---
title: "Key Learnings - Maintaining Cloud Infrastructure"
layout: post
date: 2019-10-16 10:00
tag:
- infrastructure
- cloud
- gcp
- platform
- devops
- sre
- aws

headerImage: true
image: /assets/green-chameleon-s9CC2SKySJM-unsplash.jpg
hidden: false # don't count this post in blog pagination
description: "Some of my key learnings on maintaining cloud infrastructure"
jemoji: ""
category: blog
author: adityachowdhry
externalLink: false
---

Initial people, their habits and code have a dominant effect on the things that finally turnout for a startup and that too for a considerable amount of time.

Initial stage startups have the pressure to ship out product and new features ASAP which in turns affect the overall tech quality. Contrary to this aggressive focus on quality, may affect your startups business.

As your startup grows, the tech also evolves accordingly. There are continuous refactoring that keeps on happening along the journey which cannot be avoided as it is necessary for tech to adapt to the changes your startup is going through.

> Premature optimisations can do more harm than good ex. breaking a monolith into microservices.

These changes are bound to happen and usually take a lot of time and effort. There is always some uncertainty and lack of confidence around this process. This post brings out some of the key learnings that can help in reducing time-effort and increase confidence around refactoring from the perspective of the infrastructure side of things.

* * *

These are some of my key learnings

#### 1. Convention over configuration

Have a convention when you name your resources. Here a resource can be anything like projects, cloud instances, DNS, databases or anything.

This applies consistent naming throughout your infrastructure which allows to programmatically perform actions and ease management.

#### 2. Metadata

Whenever you provision something new, make a habit to add some metadata to it. This can also be automated but you can initially make a habit of adding it manually.

Cloud providers (AWS/GCP/Azure etc) give facility of tags that you can apply to different resources. *Example -  creating a Redis? Metadata can be: type: Redis, version: 5.0.3, team: ABC*

This comes in handy when you need to identify or categorise your resources.
> How many Redis are running for my team?
> How many databases are we using?
> What versions of Postgres are we using in production?

Queries like these can be easily answered when we have the metadata.

#### 3. Inventory

Store data of all things that are running, this helps in auditing and forms the basis of dependency matrix which can easily become complex as the company scale. This somehow depends on the previous point as well.

#### 4. Networking

Network design is important and one should follow the basic hygiene and precautions when designing the networking of your infra. It can be as simple as

- Separation of public-private subnets
- Separation of dev environments
- Assigning access, opening ports, whitelisting IPs — There should be some form of tracking on this as well. It can become really messy in no time.

Networking can become a big pain and hindrance to growth if not done cautiously. Complexity increases with an increase in the number of engineers and scale.

#### 5. Deployment

Deployment is something that is used very extensively throughout the journey of any tech company. One-click deployment and rollback are the two features that in my opinion should be present as soon as possible.

This helps in minimizing errors and downtime along with increasing efficiency and velocity of developers.

#### 6. Structured Logging

Logging plays a very important role and is used for different purposes like discovering errors, deriving metrics or tracking the health of the system. In the early stages, many engineers don’t pay attention to what and how the data is getting logged. A good logging platform enables confidence in developers to refactor things.

***What to log*** — Trackable and useful things should only be logged. Useful is subjective and depends on your use case. Just main catch is too much noise defeats the purpose of logging.

***Format of log*** — Be consistent with the formatting of logs. This can help in collating metrics and track things easily.

#### 7. Monitoring, metrics and alerts

Basic metrics should always be there that define your normal working of infrastructure. This gives an overview of how things behave and alerts developers when things go wrong. They can be also used for benchmarking purposes.

An alerting system can be as simple as sending an email or a Slack message. An effective alerting system can prevent or drastically reduce downtime. Basic health metrics can be:

- System metrics like CPU, memory, load average, disk space etc
- Specific metrics for components like cache, databases etc
- Service level metrics — API response time, throughput, Apdex etc

* * *

This post only highlights the points that need focus for an early-stage startup. The complexity of each point depends on your use case and the stage your startup is.

Will be happy to see any feedback or your learnings in the comments section below.

Thanks for reading.
