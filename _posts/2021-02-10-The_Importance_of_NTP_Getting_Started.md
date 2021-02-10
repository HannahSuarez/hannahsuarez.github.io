---
layout: post
title: "The Importance of NTP (Network Time Protocol) in Logging and Auditing"
description: "The importance of NTP (Network Time Protocol) in Logging and Auditing"
comments: true
keywords: "security, ntp, time, network time protocol, logging, log collection, blueteam"
---

## About

You may have services on your network that depend on [NTP](https://en.wikipedia.org/wiki/Network_Time_Protocol) and accurate timestamps. These include DNS servers, Cryptography (certificate/signature validity) like being able to connect to a https website as well as ensuring non-repudiation and integrity via maintaining accurate timestamps in logs and especially audit logs. Inaccurate timestamps offer an inaccurate view of a sequence of events, thus making it difficult to obtain a timeframe of events in an IR.

## Attack Example

From [Cloudflare](https://blog.cloudflare.com/secure-time/):

_Most cryptography uses timestamps to limit certificate and signature validity periods. When connecting to a website, knowledge of the correct time ensures that the certificate you see is current and is not compromised by an attacker. When looking at logs, time synchronization makes sure that events on different machines can be correlated accurately. Certificates and logging infrastructure can break with minutes, hours or months of time difference._

Logrythm also offers a data sheet on time normalization [here](https://logrhythm.com/pdfs/datasheets/lr-time-normalization-datasheet.pdf) (fyi: not affiliated with them!).

## Ways to set up or configure own NTP Servers

Windows servers utilize `time.windows.com`. For others, or to maintain your own there are a few options, depending on your own resources as well as criticality.

If seeking your own, the first step is to learn more about NTP [Stratum model](https://en.wikipedia.org/wiki/Network_Time_Protocol#Clock_strata) and the [NTP Pool](https://en.wikipedia.org/wiki/NTP_pool).

**Own on-site Stratum 1 NTP Server**

* Is independent of other instances
* Is independent of other sources
* Good for secure networks
* Attached to time-keeping device (Stratum 0)
* Need to build or purchase as it requires special modules

You can buy your own NTP server, or even build one off hardware like Raspberry Pi.

**Own NTP server (Stratum 3) that obtain time from Stratum 2 servers**

* Uses “industry accepted time sources” - For example depending on the country there may be universities that host such servers, also there are more hosted privately and at other companies.
* Do not require expensive hardware
* Should be implemented with PKI infra, public key authentication, pre-shared key

**Own NTP server that uses the NTP pool**
* NTP.org uses round-robin DNS to allocate the IP address of a random time server in the pool. The geographically closer servers will provide the most accurate time
* NTP takes the time supplied from your 4 allocated time servers and uses that information collectively to calculate an accurate time. No one source is considered authoritative.
* Select at least 4 domain names from ntp.org
* More info athttp://support.ntp.org/bin/view/Servers/NTPPoolServers
