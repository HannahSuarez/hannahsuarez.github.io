---
layout: post
title: "DNS Log Collection - More on DNS Queries"
description: "A series on DNS"
comments: true
keywords: "dns, domain name system"
---

> Prerequisite: Please see this post [Why understanding of DNS monitoring is useful for securing and hardening infrastructure](https://hannahsuarez.github.io/2019/DNS-Monitoring/) published earlier in 2019

Logging DNS queries are a valuable data source used in networks in order to help incident response, and discover for indicators of compromise (intrusion discovery).  However, these transactions are noisy and can take up significant space. Log collection and log centralization will funnel these valuable logs into a processing and analytics system to enable specialists to gain insights into valuable security scenarios.  Beyond that, log centralization protects the integrity of the data should the DNS server be compromised as part of counter incident-response efforts.

## Finding Queries on DNS Debug Logs

The DNS debug file contains information on DNS queries and activity that informs of any signs of malicious traffic. The message logging key (for packets - other items use a subset of these fields) for DNS debug logging will provide information of the following:

```
	Field #  Information         Values
	-------  -----------         ------
	   1     Date
	   2     Time
	   3     Thread ID
	   4     Context
	   5     Internal packet identifier
	   6     UDP/TCP indicator
	   7     Send/Receive indicator
	   8     Remote IP
	   9     Xid (hex)
	  10     Query/Response      R = Response
	                             blank = Query
	  11     Opcode              Q = Standard Query
	                             N = Notify
	                             U = Update
	                             ? = Unknown
	  12     [ Flags (hex)
	  13     Flags (char codes)  A = Authoritative Answer
	                             T = Truncated Response
	                             D = Recursion Desired
	                             R = Recursion Available
	  14     ResponseCode ]
	  15     Question Type
	  16     Question Name
```

Once DNS log collection is set up, administrators must write configurations to parse these logs in order to extract the fields from each record. Since original data will be in a single-line log format, parsing allows for additional consumption in other software.

## Finding DNS Queries with Sysmon Event ID 22

See my previous post [here](https://hannahsuarez.github.io/2019/Sysmon-eventID22/) for more information.

> This series is from some of the braindump and notes that I have collected while researching DNS back in 2019. I have decided to share these notes out. Of course, the RFC series and implementations are the source of information of these notes.
