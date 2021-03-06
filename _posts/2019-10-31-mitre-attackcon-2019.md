---
layout: post
title: "MITRE ATT&CKCon 2019 - Recap"
description: "Recap of livestreaming the MITRE ATTACKcon"
comments: true
keywords: "conference, events, meetups, mitre attack"
---

Spending in total about 11 hours (7 hours on the first day, 6 hours on the second) listening to and watching the livestream of [MITRE ATT&CKcon](https://www.mitre.org/attackcon) was definitely a real pleasure. Not only were the presentations very interesting and informative, but the livestream quality was really amazing and it really felt like I was sitting there in the conference area, though minus the lobby talks.

I certainly learnt a lot over the two days. Now is the time for implementation!

---

## Resources and project links of note

> If I missed a link, please let me know so that I can add your project!

* Check out [Mordor](http://mordor.readthedocs.io)  - The Mordor project provides pre-recorded security events generated by simulated adversarial techniques. The pre-recorded data is categorized by platforms, adversary groups, tactics and techniques defined by the Mitre ATT&CK Framework.

* Check out **CALDERA** automated adversary emulation system [here](https://github.com/mitre/caldera). Briefly trialed them out some time back but will do so again.

* Check out the [Linux Forensics Workshop](https://github.com/ashemery/LinuxForensics) which is used to map to MITRE ATT&CK techniques, also [@ForensicITGuy](https://twitter.com/ForensicITGuy) for more Linux info.

* SoK: ATT&CK Techniques and Trends in Windows Malware [PDF](https://krisk.io/post/sok-attack-securecomm19.pdf)

* "Just because a technique says that it can be detected with a data source in ATT&CK, it might not really be practical due to limitations in the tool" [source](https://twitter.com/MITREattack/status/1189282437098020865)

* attckr tool in R - Analyze Adversary Tactics and Techniques Using the MITRE ATT&CK CTI Corpus. See the project page [here](https://cinc.rud.is/web/packages/attckr/)

* STIX (Structured Threat Information Expression makes ingesting CTI a lot easier - [project page here](https://oasis-open.github.io/cti-documentation/stix/intro). Here's the [Cyber Threat Intelligence Repository expressed in STIX 2.0](https://github.com/mitre/cti).

* Watch out for the [TRAM project](https://twitter.com/MITREattack/status/1189233353255460866) by Sarah Yoder and Jackie Lasky, to be made available publicly in the MITRE repository..

* See the [Adversary Playbook Viewer](https://github.com/pan-unit42/playbook_viewer). The goal of the Playbook is to organize the tools, techniques, and procedures that an adversary uses into a structured format, which can be shared with others, and built upon.

* [Misinfosec - where misinformation meets information security](https://misinfosecproject.github.io/)

---

See some screenshots below of a few of the presentations.

> It would be great to add all screenshots but it was hard to follow all content that I want to keep track during the day, so I only used the same screenshots that I sent out online.

![Mitre ATTACKcon](/assets/images/mitre.png)

Above image note: John Wunder, Principal Cybersecurity Engineer, MITRE at #ATTACKcon on having security monitoring and telemetry in order to update the MITRE ATT&CK Framework of what adversaries are doing.  (Screenshot from his presentation)

![Mitre ATTACKcon](/assets/images/mitre 1.png)

![Mitre ATTACKcon](/assets/images/mitre 2.png)

By Valentina Palacin, Threat Intelligence Analyst, Deloitte and Ruth Esmeralda Barbacil, Threat Intelligence Analyst, Deloitte

Above image notes: Loving the theme! "Raiders of the MITRE Framework: How to Build Your Own Threat Library" by the Argentinian team involved in creating their own Threat Library. Also shared some useful notes that you can see from the stream.

* Keep a specific format ie Have a formula for data sources

* These will be added and encouraged to be shared to ATT&CK people

* Create your own technique. ie A lot of DNS tunneling was encountered and new techniques added.

* When being a CTI analyst, jumping through a lot of data is required.

* Practice in an attack way to improve defences in company

They use a lot of sources, and there are some challenges found, mainly with China, usually overlaps threat actors.

One challenge is in using multiple sources, not knowing everyone that writes those reports.

![Mitre ATTACKcon](/assets/images/mitre 3.png)

![Mitre ATTACKcon](/assets/images/mitre 4.png)

![Mitre ATTACKcon](/assets/images/mitre 5.png)

Above image note: Relationship between #ATTACK data sources to Windows Event Log #ATTACKcon  -- they then started documenting every single Event Log, finding out what is triggering the data sources.  Heaps of great projects from [Hunters Forge](https://github.com/hunters-forge) also.

![Mitre ATTACKcon](/assets/images/mitre 6.png)

Above image note: Check out [https://github.com/hunters-forge/api-to-event](https://github.com/hunters-forge/api-to-event)

A repo focused primarily on documenting the relationships between API functions and security events that get generated when using such functions. #windows #eventlog

![Mitre ATTACKcon](/assets/images/mitre 7.png)

![Mitre ATTACKcon](/assets/images/mitre 8.png)

Above image note: Focus on a single TTP.  Rapid emulation and validation allows for more rapid response against high threat activity. Instead of a large engagement, determine if it's an event trigger/s make sure you are covered. (Emma MacMullan, Federal Reserve)

![Mitre ATTACKcon](/assets/images/mitre9.png)

From [this user](https://twitter.com/bodaceacat): Late addition to today's #attackcon talk: first image of a misinformation incident in STIG.  It's not perfect, What this means is that we can now create graph views of misinformation campaigns and store them in STIX format ready for further processing.

## My own thoughts..

* Automating, having a better workflow, using a template, using a common language >> all of these to take the burden off the laborious and manual process to build up data.

* Another good visualization is to think of the MITRE ATT&CK Framework as a periodic table of elements, where a mixture of particular elements (ie tactics, techniques, etc) provide a chemical reaction

* I really like the idea have a threat/attack framework , and you visualize it like a board game. You land on a 'square' and you can do X, Y, Z..  I mean, not an actual -game board- but more like a visualization technique #ATTACKcon

* Decision loop (part of keynote): We actually change the game for the adversary, maybe it's not tomorrow, maybe it's not next year, but we can get to the point where we're inside the adversary's decision loop.

* There will no longer be ATT&CK and PRE-ATT&CK, just ATT&CK - this is a relief.

## ATT&CK for Cloud - watch for this release!

When you move to a cloud workload, you become a consumer and less an admin. Threat hunting becomes an interesting challenge. Consuming logs in a cloud environment is important. >> Agreed! Similar sentiment that I heard from MITRE ATT&CK EU community group.

ATT&CK for Cloud version 1 released (last week) #ATTACKcon
See list at [https://attack.mitre.org/resources/updates/updates-october-2019/index.html](https://attack.mitre.org/resources/updates/updates-october-2019/index.html)

DNC hack was a notable incident for use case of adversary in this page. They need to build this out and looking for contributions (majority of how framework is built from community)

---

Overall, a great community! I got a shoutout from Katie Nickels, ATT&CK Threat Intelligence Lead, MITRE.

> Check out the recap from the [MITRE ATT&CK EU Community Workshop 2019 here](https://hannahsuarez.github.io/2019/bsides-luxembourg-mitre-attack-community-group-conference/).
