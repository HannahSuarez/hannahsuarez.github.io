---
layout: post
title: "NTP (Network Time Protocol) and Logging"
description: "The importance of NTP (Network Time Protocol) in Logging and Auditing"
comments: true
keywords: "security, ntp, time, network time protocol, logging, log collection, blueteam"
---

## About NTP

You may have services on your network that depend on [NTP](https://en.wikipedia.org/wiki/Network_Time_Protocol) and accurate timestamps in addition to using the standardized ISO8601 format. These include DNS servers, Cryptography (certificate/signature validity) like being able to connect to a https website as well as ensuring non-repudiation and integrity via maintaining accurate timestamps in logs and especially audit logs. Inaccurate timestamps offer an inaccurate view of a sequence of events, thus making it difficult to obtain a timeframe of events in an IR.

## Attack Example

From [Cloudflare](https://blog.cloudflare.com/secure-time/):

_Most cryptography uses timestamps to limit certificate and signature validity periods. When connecting to a website, knowledge of the correct time ensures that the certificate you see is current and is not compromised by an attacker. When looking at logs, time synchronization makes sure that events on different machines can be correlated accurately. Certificates and logging infrastructure can break with minutes, hours or months of time difference._

Logrythm also offers a data sheet on time normalization [here](https://logrhythm.com/pdfs/datasheets/lr-time-normalization-datasheet.pdf) (fyi: not affiliated with them!).

Read more about the attacks on the [wiki](https://en.wikipedia.org/wiki/NTP_server_misuse_and_abuse) and [Black Hat EU 14 paper](https://www.blackhat.com/docs/eu-14/materials/eu-14-Selvi-Bypassing-HTTP-Strict-Transport-Security-wp.pdf).

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

Cost of own NTP server varies. For example, 3600 euro + 800 for other features (Ultra high bandwidth, built in DOS detection, security hardening). Up to 1000 euro (ie TIMENET Pro, POE-powered NTP Master Time Server, incl. 5 metre antenna).

To build your own the cost with Arduino or Raspberry module using RTC (real time clock) module is needed.


**Own NTP server (Stratum 3) that obtain time from Stratum 2 servers**

* Uses “industry accepted time sources” - For example depending on the country there may be universities that host such servers, also there are more hosted privately and at other companies.
* Do not require expensive hardware
* Should be implemented with PKI infra, public key authentication, pre-shared key

**Own NTP server that uses the NTP pool**

* NTP.org uses round-robin DNS to allocate the IP address of a random time server in the pool. The geographically closer servers will provide the most accurate time
* NTP takes the time supplied from your 4 allocated time servers and uses that information collectively to calculate an accurate time. No one source is considered authoritative.
* Select at least 4 domain names from ntp.org
* More info at [http://support.ntp.org/bin/view/Servers/NTPPoolServers](athttp://support.ntp.org/bin/view/Servers/NTPPoolServers).

**Have NTP client already installed on Linux server?**

Check on these servers:

`timedatectl`

If `Network time on: yes` it is synced with NTP
If `NTP synchronized: no` the clock synced through another tool. May also mean
`systemd` didn't sync...

If `Network time on: no` run `sudo timedatectl set-ntp true`

Option:
`ntpdate Client` - suitable for those not connected to Internet

Use `timedatectl | grep "Time zone"`
Debian: `cat /etc/timezone`

## Collecting logs from NTP Server

`grep log /etc/ntp.conf` will show the location of where the logs are made.

Can change this location to another place otherwise logs normally go to `/var/messages` in `/opt/ntp/ntp.log`

## How to check NTP client sync logs

[Please see this Microsoft Technet support site](https://social.technet.microsoft.com/Forums/Lync/en-US/d36c9a2b-62f8-4a88-ab99-a3c899ced3c3/how-to-check-the-ntp-client-sync-logs) for the answer.

## NTP Authentication

[Please see Galsys](https://www.galsys.co.uk/news/ntp-authentication-explained/) to read more about NTP authentication.

Related: [NTP key-gen](http://doc.ntp.org/4.2.8/keygen.html)


## Collecting logs from Windows Time Server on ADDC

Audit changes to these registry keys
`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters\Type` (Values changed in the `'Value'` data box) – set to `NTP`

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config\AnnounceFlags`
(`DWORD` Value changes in the `'Value'` data box) – set to `5`

As usual, **the latest advice** comes from Microsoft's own [documentation](https://docs.microsoft.com/en-US/troubleshoot/windows-server/identity/configure-authoritative-time-server).

## Defending NTP Server Notes

* Considering configuring the firewall rules to provide exception for the 1 NTP server. Tighter ACL – ie enforce requests only from valid sources
* Traffic filtering
* Ensure no overprovisioning
* Block from the open Internet, closed only.
* Make sure it is upgraded
* Configure NTP authentication (ie [RedHat](https://access.redhat.com/solutions/393663)). Maybe needed for compliance reasons ie DoD, FIPS 140-2, etc.
* Disable `monlist`
* Check http://openntpproject.org/ to see if the NTP server is on the public list
* Extending semantics of a Reference Identifier field in an NTP packet when a Stratum field is 0.
