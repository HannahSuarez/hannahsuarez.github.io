---
layout: post
title: "Collecting of Windows EventIDs tracking Lateral Movement based on JPCERT"
description: "This post hosts a collection of Windows Event IDs and paths"
comments: true
keywords: "logging, log collection, log management, SIEM, SIEM suite, malware, lateral movement"
---

## Introduction

JPCERT published a very thorough document, [Detecting Lateral Movement through Tracking Event Logs](https://www.jpcert.or.jp/english/pub/sr/20170612ac-ir_research_en.pdf), which is well worth a read itself to learn more about attacker tools and its movement through Windows environments.

**They also have a much better and interactive resource at [Github](https://jpcertcc.github.io/ToolAnalysisResultSheet/) where you can click through each of the tools**

The research they conducted provides basic information which for log collection and further log analysis. They investigated the evidence of tools used by many attackers.

They made the research more accessible to those outside the incident response industry and also to easily list out the following activities of note by the malware:

• Event log
• Execution history
• Registry entry

**Important to note**
Before applying these EventIDs to your log collection, the amount of logs that can be acquired in a default system is typically not enough to emit the requirements events.  Therefore, additional settings need to be made (ie enabling Windows audit policy) as well as installing Sysmong.

## List below

```
Security
4624, 4634, 4648, 4656, 4658, 4660, 4663, 4672, 4673, 4688, 4689, 4698, 4720, 4768, 4769, 4946, 5140, 5142, 5144, 5145, 5154, 5156, 5447, 8222

Event Log - Sysmon
1, 2, 5, 8, 9

Event Log - System
7036, 7045, 20001

Event Log - Application and Service
Microsoft\Windows\Windows Remote Management
80, 132, 143, 166

Event Log - Application and Service - Microsoft\Windows\Windows Remote Management\Operational
80

Event Log - Application and Service - \Microsoft\Windows\Windows Remote
81

Event Log - Application and Service Log - \Microsoft\Windows\TaskScheduler\Operational
106, 129, 200, 201

Event Log - Application and Service Log - \Microsoft\Windows\TerminalServices-LocalSessionManager\Operational
21, 24

Event Log - Application and Service Log - \Microsoft\Windows\Bits-Client
60

Event Log - Each Target Log
Event ID : 104 (The System log file was cleared)
```
