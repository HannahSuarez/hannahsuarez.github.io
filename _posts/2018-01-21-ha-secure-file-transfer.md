---
layout: post
title: "Using secure file transfer software in high availability environments"
description: "An article on using secure file transfer software in HA environments"
comments: true
keywords: "file transfer protocols, security, resiliency, high availability, fault tolerance"
---

This was an article written for a secure file transfer product.

[Read more here](https://www.sftpplus.com/news/2018/sftpplus-ha-resiliency-intro.html)

---

# Full content below

## Where does SFTPPlus sit in your IT infrastructure

The SFTPPlus software stands at the OSI Layer 7 or the TCP Layer 4. In order to have a fully fault tolerant system, you need to implement resilience at all the other layers including the OS. SFTPPlus can be integrated with external tools in order to meet the requirements for a fault tolerant infrastructure.

For those not familiar with OSI and TCP please read on.


## SFTPPlus on the OSI 

The OSI model is a model that characterizes and standardizes communication functions. The layers range from layer 1 right through to layer 7. In the OSI, or Open Systems Interconnection model, SFTPPlus sits in the OSI Layer 7 or on the application layer.

The application layer sits at the top of the OSI model and is the software, hence the name application, layer between the end-user and the networking layers underneath.

In order to have a fault tolerant system, SFTPPlus on the upper layer 7 will need to be integrated with the bottom layers.


## SFTPPlus on the TCP

In addition to the OSI model, another way of understanding where SFTPPlus plays a role in your infrastructure is via the TCP layer. SFTPPlus sits in the TCP Layer 4 or the application layer. This is the topmost layer which defines the TCP/IP application protocols and how SFTPPlus interfaces with the Transport layer, the layer below the application layer, and other services that use the network.


## Installing SFTPPlus in high availability and resilient environments

The following are introductory information for this topic.


### About high availability

High availability means creating a system that is always available for use. It could be a percentage of 99.99% uptime guaranteed. In this case, you will be looking at a downtime of merely five minutes of time over the course of the year.

There are extra items that one can add to ensure that this system is available at the guaranteed uptime rate. In this case, one can look into active-active or active-passive scenarios. To build a system that is highly available means that there may be an additional cost associated with ensuring this.


### About resilience

The following can be deduced as a definition of a resilient control system:

*"A resilient control system is one that maintains state awareness and an accepted level of operational normalcy in response to disturbances, including threats of an unexpected and malicious nature"*

High availability and resilience tend to be used interchangeably. However, having a highly available system does not necessarily mean that all required functions are still in use and available. This is where having a resilient system come into action. Even if a system has high availability, can it still function to a required level of standard, operational normalcy?  You will still wish to utilize a system with the same users, storage and database as found in the usual system.


### About fault tolerance

On the event of failure, the system remains available in order to maintain the high uptime. There may be a performance break or slow down but the services are still available.

You may add additional devices or protocols for a fault tolerant system - RAID set up, multiple network paths for fault tolerance (on the event of a failed network path) and load balancers are such examples.


### About clustering

Clustering involves creating a cluster of two or more nodes or members that work together in order to perform an action. They can be grouped in the following major types; storage, high availability, load balancing and high performance clusters.

The main clusters that relates to SFTPPlus in a given system are high availability and load balancing types of clusters.

High availability clusters involve the provision of highly available services by ensuring that any single points of failure are eliminated. This is done by failing over services from one cluster node to another should that node be no longer in operation. This ensures the ability to maintain data integrity.

Load balancing clusters sends off network requests to a number of cluster nodes in order to balance the request load among the cluster nodes. This ensures scalability of a network since administrators can match the number of nodes according to load requirements through load balancing algorithms.


## Active-Active and Active-Passive Scenarios

Active-active and Active-passive are two types of cluster configurations in a high availability scenario.

The details between these two scenarios are laid out below from *Sybase*.


### Active-Passive configurations

Setup: A single Adaptive Server runs either on the primary node or on the secondary node. The Adaptive Server runs on the primary node before a fail over and the secondary node after fail over.

Failover: When a system fails over, the Adaptive Server and its associated resources are relocated to, and restarted on, the secondary node.

Failback: Failback is a planned fail over or relocation of the Adaptive Server and its resources to the primary node. Failback is not required, but can be done for administrative purposes.

Client Connection failover: During failover and failback, clients connect to the same Adaptive Server to resubmit uncommitted transactions. Clients with the failover property reestablish their connections automatically.


## How to set up SFTPPlus in active-passive scenarios

In this infrastructure scenario, the second system is offline and only commences when the main SFTPPlus system is down.

Since the server.ini configuration is stored in a single file, you can create a file copy task to keep the system configurations in sync. Make sure to also transfer additional files that are required - such as SSH keys, and SSL keys and certificates - to ensure a smooth transition. When it is time to use the secondary system, the SFTPPlus instance will then read the latest server.ini configuration file.


### Active-Active configurations

Setup: Two Adaptive Servers are configured as companion servers, each with independent workloads. These companions run on the primary and secondary nodes, respectively, as individual servers until one fails over.

Failover: When fail over occurs, the secondary companion takes over the devices, client connections, and so on from the primary companion. The secondary companion services the failed-over clients, as well as any new clients, until the primary companion fails back and resumes its activities.

Failback: Failback is a planned event during which the primary companion takes back its devices and client connections from the secondary companion to resume its services.

Client Connection failover: During failover, clients connect to the secondary companion to resubmit their uncommitted transactions. During failback, clients connect to the primary companion to resubmit their transactions. Clients with the failover property reestablish their connections automatically.


## How to set up SFTPPlus in active-active scenarios


In this infrastructure scenario, both SFTPPlus systems are receiving and processing requests. If one system goes down, the other will handle all the requests.

To implement SFTPPlus in this scenario, a simple file copy will not work. This is because running SFTPPlus instances will not check changes in the local file configuration (server.ini) in order to reconfigure. In addition, there are other files that are also required - such as all SSH keys in use and other related files, all SSL certificates required, any logs that need to be kept for auditing purposes, any externally referenced scripts used in pre- and post- transfer processing, and so on.

One method of achieving an active/active implementation is to manually set up the 2 nodes to rely on a single external authentication method (HTTP or LDAP). In this way, accounts are managed in the single external system, and those accounts will be automatically available for both SFTPPlus instances.


## Installing SFTPPlus for disaster recovery


Disaster recovery is part of business continuity plans (or business continuity and resiliency plans) which is the process of creating systems of prevention and recovery to deal with potential threats to a company. The use of the term “recovery” has also been used when talking about resiliency.

Providing that the server configuration and related configuration files are properly maintained and backed-up, you can integrate SFTPPlus as part of your disaster recovery plans.


## Conclusion and next steps

The application of these does not immediately guarantee results in achieving high availability or resiliency. Please consider these guides merely as a layer within multiple others when implementing a high available, resilient and secure managed file transfer solution.

Since features are constantly changed, we did not touch on any specifics within SFTPPlus. Please consult our documentation for the configuration and operations information, as well as practical users guides.
