---
layout: post
title: "How DNS request information is used in IT security - Attacks, Mitigations"
description: "A series on DNS"
comments: true
keywords: "dns, domain name system"
---

> This series is from some of the braindump and notes that I have collected while researching DNS back in 2019. I have decided to share these notes out. Of course, the RFC series and implementations are the source of information of these notes.

### Prerequisite: Please see this post [Why understanding of DNS monitoring is useful for securing and hardening infrastructure](https://hannahsuarez.github.io/2019/DNS-Monitoring/) published earlier in 2019

# How DNS request information is used in IT security.

A strong grasp of DNS is the foundation for secure networks and systems. Knowledge of what is in DNS request information, as covered in the previous post, in IT security leads to hardening network engineering practices.

## SANS CSC recommendations for DNS security

Ensuring illegal connections are not being made from the outside through hardening network helps prevent network footprinting where the adversary enumerates information about the target network to learn the resources in the network - domain names, computer names, IP addresses and more. This information is used as part of the enumeration exercises to learn more about the network prior to a compromise and attack.

Recommended on SANS CSC 19-3 is to deploy DNS servers in a hierarchical and structured way, ensuring that internal network client machines are configured to send requests to internal DNS servers, not to public Internet facing DNS servers. These internal DNS servers should then be configured to forward requests that cannot be resolved to DNS servers that are located within a protected demilitarized zone (DMZ). In turn these DMZ servers are then allowed to send requests to the Internet. The function of a DNS DMZ is to provide external or Internet DNS services to corporate users while also protecting them from external network threats like those trying to illegally connect to the internal network.

Knowledge of DNS request information in IT security can also lead to determining if there are communications to bad servers, such as an unwanted C2 (Command and Control) server.

According to SANS CSC 5-11, and in many other network security engineering standards, the recommendation is to enable DNS query logging to detect hostname lookup for known malicious C2 domains. These abused domains initiate Command and Control (C2) communications by communicating with a C2 server.

When periodic DNS requests are made by a host in the target network to a compromised domain controlled by the adversary, these responses contain exploits used to perform unauthorized and unwanted actions in the target host or even target network. These actions include data theft where data is transferred from the target network to a C2 server via protocols such as SSH through DNS queries and responses. Finding DNS request information is needed, since in order to tunnel the data, the compromised host must make DNS queries to the malicious domain. DNS tunneling can also be used for executing shellcode or machine code that is used within an exploit which is then executed.

## Other DNS malware attacks

Administrators monitoring the network for traffic, either from sandboxed networks, honeypots, or actual intrusions, need sufficient log collection to be effective. Compromised clients with APT malware communicating to  command-and-control servers, DNS hijacking trojan horse attacks and other DNS anomalies are just an example of attacks using DNS.

Below is an example of a DNS query leading to a malicious site `hacked.site.com`. With DNS (Domain Name Server) monitoring where administrators monitor and proactively analyze DNS  queries and responses has become a standard security practice for networks of all sizes. The efficiency of DNS monitoring is reliant on the sufficient logging and log collection in order to catch potential issues:

```
2020-09-06
Time (GMT)      Source                Destination           Protocol-Info
12:42:42.112898 xxx.xx.xxx.xxx        xxx.xx.xx.x           DNS      Standard query 0x1de7  A hacked.site.com
```

# Examples of DNS Attacks

## Honeypot taking advantage of vulnerabilities

For this case, the administrator could set up a honeypot to monitor from log collection. Monitoring these, especially the vulnerable URL, would help mitigate potential attacks to more valuable network resources. The following are indicators of attackers exploiting a BroadCom UPnP vulnerability.

For port scans, the administrator would set up log collection to monitor for destination scans to TCP port 5431 and scans to target’s UDP port 1900.

A vulnerable URL should also be monitored, once known. Administrators can also set up automated alerts for known vulnerable URLs gleaned from a database.

## DNS Spoofing Attack

For this case, the administrator would set up logging to capture DNS traffic where there is a a source port of 53 (attacker's) destined to an unprivileged port (above 1024) for a DNS resolver (attack target).

## DNS Cache Poisoning Attack

For this case, the administrator would set up logging to capture indicators that show high rate of DNS traffic where there is a source port of 53 (attacker) destined to a DNS server on the network (the attack target).

## DNS Amplification or Reflection Attack

For this case, the administrator would set up logging to monitor for high rate of DNS response traffic, coming in from various sources, where there is a source port of 53 (attacker's) which is destined to the target network. Typically the source addresses of the servers used in this scenario are typically DNS resolvers. This type of attacks are likely to use large DNS packets to increase efficiency.

## DNS Amplification or Reflection Attack Source

Monitor for high rate of DNS traffic from your DNS server with a source port of 53 (attacker) destined to other networks (attack targets).  These are likely to use large DNS packets to increase their efficiency; however large packets are not a requirement.

## Router DOS related to DNS sending multiple '\0' characters

Vulnerable [versions of MikroTik RouterBOARD](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-17537) allows an unauthenticated remote attacker to cause a DOS by connecting to port 53 and sending data that begins with multiple '\0' characters, possibly related to DNS. This will show up in DNS log monitoring activities.

## MITM attacks spoofing DNS responses

Vulnerable versions of [IBM DataPower Gateways](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1773) (IBM X-Force ID: 136817) could allow MITM attacks via spoofing DNS responses to perform DNS cache poisoning and redirect Internet traffic. In this case, it is also useful to be kept up to date with vendor updates.

# DNS Logging - Going Beyond

In addition to DNS log collection, be informed of other concepts including:

* Retention
* Format –  collect, parse, convert, and generate log data in various formats
* Integrity – sending and receiving various types of encrypted log data, with checksumming generation and validation, write events to append-only database tables
* Dashboard Monitoring
* Alerting

## Other Monitoring Strategies

Monitor DNS resolutions on every endpoint
DNS query and response, process

Monitor Netflow (IP) traffic to outbound DNS port 53
Process, remote IP address and port, count of bytes

Monitor DNS data on internal DNS servers
DNS query and response, client and nameserver IP address

Monitoring of the user (user and process) that is made pssible through setting up other log collection endpoints but not covered in the paper.

## Mitigations

### SANS CSC-5

The followng are notes _captured_ directly from SANS CSC-5.

#### CSC 5-11
Enable domain name system (DNS) query logging to detect hostname lookup for known malicious C2 domains.

#### CSC 11: Limitation and Control of Network Ports, Protocols, and Services
Manage (track/control/correct) the ongoing operational use of ports, protocols, and services on networked devices in order to minimize windows of vulnerability available to attackers.

Why Is This Control Critical?
Attackers search for remotely accessible network services that are vulnerable to exploitation. Common examples include poorly configured web servers, mail servers, file and print services, and domain name system (DNS) servers installed by default on a variety of different device types, often without a business need for the given service.

#### CSC 11-6
Operate critical services on separate physical or logical host machines, such as DNS, file, mail, web, and database servers.

#### CSC 13-3
To lower the chance of spoofed e-mail messages, implement the Sender Policy Framework (SPF) by deploying SPF records in DNS and enabling receiver-side verification in mail servers.

#### CSC 19: Secure Network Engineering
7Make security an inherent attribute of the enterprise by specifying, designing, and building-in features that allow high confidence systems operations while denying or minimizing opportunities for attackers.

#### CSC 19-3
4Deploy domain name systems (DNS) in a hierarchical, structured fashion, with all internal network client machines configured to send requests to intranet DNS servers, not to DNS servers located on the Internet. These internal DNS servers should be configured to forward requests they cannot resolve to DNS servers located on a protected DMZ. These DMZ servers, in turn, should be the only DNS servers allowed to send requests to the Internet.
