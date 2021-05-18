---
title: "Avoid These Pitfalls While Configuring Your GKE"
layout: post
date: 2018-09-01 16:00
tag:
- sre
- kubernetes
- gke
- google-kubernetes-engine
- devops
image: /assets/redis.png
headerImage: true
projects: false
hidden: false # don't count this post in blog pagination
description: ""
jemoji: ""
category: blog
author: adityachowdhry
externalLink: false
---

## Intro
I have been playing around with GKEs for more than a year at Gojek. This post ellaborates some of the common pitfalls that teams get into while maintaining their GKE clusters because of less thought out configurations. Treat these points as a point of discussion within your team to arrive at an appropriate configuration. 

## Pitfall 1 - Downtime due to zone degradation, upgrade or other maintainence activities

### Choosing a correct cluster type - Zonal or Regional
Zonal clusters have single control plane and are of two types - one with single zone node pools and second with multi-zone node pools.
Recommendation - Avoid using zonal cluster with single zone node pools for production

Regional clusters involves replicated control planes in each zone which gives higher availability.

This ![doc](https://cloud.google.com/kubernetes-engine/docs/best-practices/scalability#choosing_a_regional_or_zonal_control_plane) acts as a good guide for choosing between zonal and regional.

Since, you would need to upgrade or do maintenance activities often on a GKE cluster, spend some time on the trade-offs and select a type that suits well with your use case. This is **immutable** once created. 

In future, if you need to change the type, only way is to create a new cluster and migrate workloads, which is a tedious task.


## Pitfall 2 - Scaling issues
One day, while enjoying your coffee, you recieve a pager(insert horror face here). You notice high throughput on one of your services and your autoscaled pods are failing to get scheduled. Digging further you notice, even nodes are unable to autoscale. While checking Pod IP address range, it appears a lot more pods can be created, then what is the issue? After a while you find out that the number of nodes have hit a threshold.

We'll come to the why part later, but lets see what options do we have here to scale our cluster

A cluster can be scaled in two ways
1. Increasing number of nodes
2. Increasing node size (choosing higher machine type configuration)

Increasing node size seems to be easy, let us check what is the maximum number of pods that can be scheduled on a node.
The configuration `max_pods_per_node` seems to be a default one with value 110. Pods on the cluster are distributed evenly on all nodes, and seems like the actual number of pods getting scheduled is much lower than the 110 value. 

Cool, lets change the machine type to higher configuration which can accomodate more pods.

Uh oh! Machine type cannot be changed, you would need to create a new node pool with your target machine type and migrate your workloads there. This [doc](https://cloud.google.com/kubernetes-engine/docs/tutorials/migrating-node-pool) explains on how to do it without downtime.

This is only possible if we are able to create a new node pool in the same cluster. But, in this scenario we can't even create another node. 

Okay then maybe lets try the first option

Sure, the number of nodes in a cluster depends on node IP address range and max pods per node configuration. 

From GKE docs, you figure out that node IP range depends on underlying subnet primary IP range. There is this [doc](https://cloud.google.com/vpc/docs/using-vpc#expand-subnet) which talks about how you can expand your subnet. Hence, one can increase the number of nodes by increasing the primary range. 

another blocker -  seems like if we try to expand our subnet, we violate one of the subnet rules that are mentioned in the doc. Okay but what about max number of pods?

Sad news, You can configure the maximum number of Pods per node at cluster creation time and at node pool creation time. And now we are back to zero.

*cries in a corner*

This incident brings our attention to three configurations that are very crucial while creating a cluster
1. Node IP address range
2. Pod IP address range
3. Max pods per node
 
Now, coming to why
Assuming we have sufficient pod IP range. We use the default settings as
- `/20` as default node IP range
- `110` as max pods per node

`/20` allows us to create 4092 nodes (2^12 = 4092 + 4 reserved IP addresses)
As we have, 110 as max pods per node, GKE allocates double the addresses to one node i.e 256 in this case (checkout this [table](https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr#cidr_ranges_for_clusters))



### VPC-native subnet IP address ranges
I'll be talking only about VPC native clusters, since these have become default and are recommended. 