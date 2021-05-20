---
title: "Avoid These Pitfalls While Configuring Your GKE"
layout: post
date: 2021-05-21 00:50
tag:
- sre
- kubernetes
- gke
- google-kubernetes-engine
- devops
image: /assets/gke.png
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
I have been playing around with GKEs for more than a year at [Gojek](https://www.gojek.io/). This post elaborates on some common pitfalls that teams get into while maintaining their GKE clusters because of less thought out configurations. Treat these points as a point of discussion within your team to arrive at an appropriate configuration. 

## Pitfall 1 - Downtime due to zone degradation, upgrade or other maintenance activities

### Choosing a correct cluster type - Zonal or Regional
Zonal clusters have a single control plane and are of two types - one with single-zone node pools and the second with multi-zone node pools.
Recommendation - Avoid using a zonal cluster with single-zone node pools for production

Regional clusters involve replicated control planes in each zone which gives higher availability.

This [doc](https://cloud.google.com/kubernetes-engine/docs/best-practices/scalability#choosing_a_regional_or_zonal_control_plane) acts as a good guide for choosing between zonal and regional.

Since, you would need to upgrade or do maintenance activities often on a GKE cluster, spend some time on the trade-offs and select a type that suits well with your use case. This is **immutable** once created. 

In future, if you need to change the type, the only way is to create a new cluster and migrate workloads, which is a tedious task.


## Pitfall 2 - Scaling issues
One day, while enjoying your coffee, you receive a pager(insert horror face here). You notice high throughput on one of your services and your autoscaled pods are failing to get scheduled. Digging further you notice, there is insufficient CPU and nodes are unable to scale further. 

You immediately go check the Node IP address range. With this, you get the max number of nodes that can be created. This number seems to be way higher than the current number of nodes. Then why is it unable to create more nodes?

We'll come to the why part later, but let us see what options do we have here to scale our cluster

A cluster can be scaled in two ways
1. Increasing number of nodes
2. Increasing node size

Increasing node size seems to be easy, you quickly check what is the maximum number of pods that can be scheduled on a node.

The configuration **`max_pods_per_node`** seems to be a default one with value **110**. Pods on the cluster are distributed evenly on all nodes, and seems like the actual number of pods getting scheduled is much lower than the 110 value. 

Cool, let us change the machine type to a higher configuration that can accommodate more pods.

Uh oh! Machine type cannot be changed, you would need to create a new node pool with your target machine type and migrate your workloads there. This [migration doc](https://cloud.google.com/kubernetes-engine/docs/tutorials/migrating-node-pool) explains how to do it without downtime.

But but ..  this is only possible if we can create a new node pool in the same cluster. In this scenario, we can't even create another node. **meanwhile in the background you get a slack popup - hey how much time will it take to solve the issue?** 

Sweating, you decide okay then maybe let us try the first option

Sure, the number of nodes in a cluster also depends on Pod IP address range and max pods per-node configuration. 

Okay then maybe increase the Pod IP address range? GKE docs reveal Pod IP address range is actually taken from VPC-native cluster's subnet secondary IP range. The doc further reveals that doing so is not supported as it has the potential to put the cluster in an unstable state. 

Okay okay, calm down! But what about the max number of pods?

Sad news, You can only configure the maximum number of Pods per node at cluster creation time and at node pool creation time. And now we are back to zero.

<center><i>cries in a corner</i></center>

This incident brings our attention to three configurations that are very crucial while creating a cluster
1. Node IP address range
2. Pod IP address range
3. Max pods per node
 
Now, coming to the why part. Let us try to work this through an example to understand the calculation of the number of nodes

Assume Node IP range (primary range) as `/23` and Pod IP range (secondary range) as `/20`
This roughly translates to 
- **/23** to `2^9 = 512`, in which 4 addresses are reserved. Hence, a total of *508 nodes* are possible
- **/20** to  `2^12 = 4096`, in which 4 addresses are reserved. Hence, a total of *4092 pods* can be scheduled. 

Taking max pods per node default value as 110, GKE allocates addresses to each node with at least twice the number of max pods per node i.e 256 in this case. (checkout this [table](https://cloud.google.com/kubernetes-engine/docs/how-to/flexible-pod-cidr#cidr_ranges_for_clusters))

Now we can calculate the number of nodes as  `Number of pod IP addresses/Number of IP addresses assigned to each node` which is `4092/256` ~ **15 nodes**  

So as you see, though 512 nodes are possible, the number of nodes can vary depending on pod IP address range and max pods per node.


## Pitfall 3 - Frequent upgrades

Kubernetes follows a periodic release cycle, which is propagated via GKE releases. GKE releases more often than the open-source Kubernetes, it becomes difficult to keep up manually with the upgrades. Depending upon your *nature of workloads*, you can enrol to a release channel, in which Google automatically manages the version and upgrade cadence for the cluster and its node pools. You can read more about [release channels here](https://cloud.google.com/kubernetes-engine/docs/concepts/release-channels)


There is a catch here, Google upgrades the control plane of a cluster automatically even if you are not enrolled in a release channel. So be sure to assign a maintenance window that is least disruptive to your business.


Let me know if these points are helpful.