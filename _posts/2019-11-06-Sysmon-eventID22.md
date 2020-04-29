---
layout: post
title: "DNS Event Query Monitoring with Sysmon with Metadata Sample and link to Example Rules"
description: "sysmon, windows"
comments: true
keywords: "sysmon, windows, dns"
---

I came across a post by a sysadmin who created a macro in Word document which dials into a C2 server that they themselves run on a port. They were disappointed that the firewall did not catch this and no alerts came up.

It interested me because there are a few different ways, other than looking into the ACLs, there is also DNS monitoring.

There are more than a few different ways for DNS log collection on Windows.These include:

* DNS logging via latest Sysmon (version released June 2019) which includes Event DI 22.

* DNS monitoring via ETW Provider (DNS Client and DNS Server Providers respectively)

* Windows Event Log EventIDs related to DNS

* DNS file-based logging turning on the DNS Analytical and Debug channels. These channels are not included in the Event Log (above).

Sysmon Event ID 22 (for DNSEvent (DNS query)) is "generated when a process executes a DNS query, whether the result is successful or fails, cached or not. The telemetry for this event was added for Windows 8.1 so it is not available on Windows 7 and earlier."

See below for an example output from the metadata using NXLog `im_msvistalog` module that is available in the Community Edition:

```
"Message":"Dns query:\r\nRuleName: \r\nUtcTime: 2019-11-06
08:40:13.321\r\nProcessGuid: {b3c285a4-5f1e-5db8-0000-0010c24d1d00}\r\nProcessId:
5696\r\nQueryName: hannahsuarez.me\r\nQueryStatus: 0\r\nQueryResults:
::ffff:88.180.312.23;\r\nImage: C:\\Windows\\System32\\PING.EXE"
```
You can see that not only is the domain included, but the executable (in this case, ping.exe) is also included.

One of the trickiest think about utilizing Sysmon for DNS monitoring is going to be in the ruleset. DNS log collection is very noisy and also challenging due to factors like:

* Client-side lookups (ie via ads)
* If on an EC2 instance, you will notice lookups to the instance IP address
* Legitimate domains can also be used to host malware/C2 but including these will be very noisy. In this case it will be about making sure that the Sysmon rule schema is being done properly.
* Google Chrome has a built-in DNS pre-fetching mechanism (used to improve on page loading), also Firefox
* From Windows Server 2016, there is an addition of a new feature called [DNS Policy](https://docs.microsoft.com/en-us/windows-server/networking/dns/deploy/dns-policy-scenario-guide) and to reduce noise, administrators may want to add some [filtering](https://docs.microsoft.com/en-us/windows-server/networking/dns/deploy/apply-filters-on-dns-queries) related policies for it.

There is an excellent resource by [SwiftonSecurity for a Sysmon configuration file](https://github.com/SwiftOnSecurity/sysmon-config/) which also includes DNS as well as other Sysmon rules.
