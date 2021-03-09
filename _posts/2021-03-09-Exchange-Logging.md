---
layout: post
title: "Microsoft Exchange Logging - Hafnium and other Attack Scenarios"
description: "The importance of NTP (Network Time Protocol) in Logging and Auditing"
comments: true
keywords: "security, exchange, iis, hafnium, logging, log collection, blueteam"
---

## Exchange

Microsoft Exchange is a common attack surface, providing multiple entry points from the public/Internet facing to the enterprise network. Recently, Exchange hit the news due to the Hacker group known as #Hafnium doubled its hack count of Microsoft’s Exchange Servers up to nearly 60,000 globally.

There has been some previous reports of known attacks by Exchange. [FireEye Red Team in 2019 conducted a red team pentest](https://www.fireeye.com/blog/threat-research/2019/04/finding-weaknesses-before-the-attackers-do.html) where you can see that initial compromise happens on OWA (Outlook Web App). This was cloned by red team on a look-alike domain, technically it's a phishing attack but the compromise goes OWA.

Attackers persistence and domain escalation can happen as Microsoft Exchange binds to Active Directory. Attackers can harvest same credentials.

## Exchange Log Collection

In addition to the [Microsoft security update which included mitigation strategies](https://msrc-blog.microsoft.com/2021/03/02/multiple-security-updates-released-for-exchange-server/) here are also other items that one can look into securing Exchange:

* Find indication of redirection (ie from fake OWA to real OWA)

* Find signs of `privesc` ("being an Administrator on an Exchange server is enough to escalate to Domain Admin" from [Duo](https://duo.com/decipher/microsoft-exchange-users-get-admin-rights-in-privilege-escalation-attack))

* [Pentesting Microsoft Exchange](https://securityonline.info/exchange-ad-privesc-exchange-privilege-escalations-to-active-directory/)

* Writeup to [harden Exchange](https://pentestlaboratories.com/2019/09/23/microsoft-exchange-preventing-cyber-attacks/)

Of course the mitigation notes and security release updates are most important. They also mention going through IIS logs for 'files identified as malicious have been accessed.'


Example Filebeat (general Exchange):

```
type: log

#confirm the path to the Microsoft Exchange Transport Logs. See the Open Office document to find where
paths:
 - /path/to/logs
#example
 #- F:\Program Files\Microsoft\Exchange Server\V15\TransportRoles\Logs\MessageTracking\*.LOG

processors:
 - decode_csv_fields:
     fields:
        message: csv
     separator: ,
     ignore_missing: false
     overwrite_keys: true
     trim_leading_whitespace: false
     fail_on_error: true
```

Example Winlogbeat File (general Exchange):

```
winlogbeat.event_logs:

name: Application
ignore_older: 72h
name: Security
name: System
name: MSExchange Management
name: MSExchange ADAccess
name: MSExchange Message
name: MSExchange Antispam
#OWA is client only - not relevant to server
#name: MSExchange OWA
```
