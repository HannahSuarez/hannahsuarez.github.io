---
layout: post
title: "Various Notes - Incidence Response on Attacker Tricks for EventLog"
description: ""
comments: true
keywords: "incident response, forensics, security"
---

> Here's a collection of incidence response notes, largely from YouTube videos. Make sure to see the link for the full videos. Will update when I find more to share. There are actually more notes around with other IR topics but these are largely EventLog notes.


[Video "What Event Logs? Part 1: Attacker Tricks to Remove Event Logs"](https://youtu.be/7JIftAw8wQY)

Go beyond Windows EventLog for monitoring and look into attacker techniques:
* Clear logs
* Resize logs
* Mimikatz
* Invoke-Phant0m
* Look into what processes handling event logs

Understanding the processes in the level of granularity - attackers know the different links in the chain, seeing what is weak etc.

Attacker Techniques (used late 2017) include TrustedSec PowerShell exploitation
Attackers look at red team side projects and weaponizing them.

Attacker technique is to clear out event logs - a key tactics in a group in the breach cycle is to clear event logs, used to be one time but it is repeated. Event logs are cleared out from command line or GUI. Can be cleared out on exit or cleared out intermittently.

Escalate privilege to clear event logs, get malware to clear event logs, etc

Process auditing - if you are able to get insights into command arguements being issued.

In the surface, there is proof of event logs ie event 'the event log was cleared' and pops an alert as it is not part of standard procedure. easy anomaly detection. some situations is normal, attackers take advantage of it ie scheduled clearances is know by attackers.

Another artifact event log is cleared, you now what user or account is used.

Detection/mitigtation tips include:
* Forwarding logs to a SIEM
* Forwarding logs should be standard but some ways not - ie dev logs, logs not sensitive or not protected

Attackers can clear logs but not all logs are cleared ie task scheduler, remote desktop, etc. Logs may be gone from disk but some rendered from memory.

Another technique is to meddle with event logo settings ie stop event log service but there is a lot of artifacts left.

Meddle with event log settings such as `HKLM\SYSTEM\CurrentControlSet\Services\EventLog`.

Inside registry are metadata like retention periods, displaynameid, file name, change the eventlog size maxsize ie knock down the size to the minimum then flood with events to the point the system cannot maintain 3 seconds worth of history.

---

[Video "Incident Response Process - CompTIA Security+ SY0-501 - 5.4"](https://www.youtube.com/watch?v=qGktAVJpTGE)

The Incident Response Life Cycle is comprised of:
* Preparation
* Detection and Analysis
* Containment, Eradication, Recovery
* Post-incident Activity

Use logs for finding baselines and also to find indicators (for example, of compromise).

Detection methods have different levels of detail or perception. The question is how to find a legitimate threat.

---

[DFIR summit presentation "The Audit Log Was Cleared - SANS Digital Forensics and Incident Response Summit 2017"](https://www.youtube.com/watch?v=00EwvDKaKyQ)

How to mitigate - have logs be forwarded in SIEM, look for gaps and stoppage. SIEM is not just log collector but something that can base rules around

Check registry and look for timestamps ie use Volatility to dump memory services https://youtu.be/7JIftAw8wQY?t=1719

Attacker technique - EventLog editing with Mimikatz https://youtu.be/7JIftAw8wQY?t=1754

When 'event clear' event was done, run mimikatz event drop. What it does is it patches the event log service and prevents service from writing event logs.
Now you can clear the event log message of the event log being cleared entry aka no evidence of it being cleared.

If you are doing event log clearing and no alerts then it does not work.

Thread disruption via Invoke-Phant0m - https://youtu.be/7JIftAw8wQY?t=2029
Attempt using in the wild

- How were logs disrupted?
- What accounts were used
- What are evidence of execution ie executable, script, etc
- Timeframe of service disruption

Logs are powerful. We tend to take event logs at face value, they don't think to themselves about trusting the user or eventID. You know that a system has been compromised but you know that the system logs belong to the user and have ability to mess around artifacts etc.

Tracking attacks against integrity of event logs is important. Have evidence of threat actors clearing event logs from basic to complicated. To manipulate trace they were there in first place.

Another mitigation is to correlate what happens at the disk at the time. Look at other artefacts before/after event. Look at SIEM and see what has been forwarded.
There are many great tools - ie recover Event Logs from memory and from disk. These areas are covered very well.
