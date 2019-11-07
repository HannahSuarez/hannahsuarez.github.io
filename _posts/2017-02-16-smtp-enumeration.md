---
layout: post
title: "Mail server / SMTP Enumeration"
description: "How mail servers can help the enumeration process"
comments: true
keywords: "smtp, enumeration, nmap, nse, scanning"
---

> Page is currently a work in progress.


# What is SMTP
SMTP stands for Simple Mail Transfer Protocol and is used for email delivery
from an email client to an email server.

# What is enumeration
There are a few different definitions of enumeration.  In network security, this
is performed as a discovery process of hosts and devices within a network.

# Enumeration tools

## Scan

Conduct a scan using tools such as Nmap to determine state of the ports
servicing SMTP and any other details that you may ascertain.

## Nmap and NSE scripts

The Nmap Scripting Engine (NSE) contains a library of scripts including scripts
for SMTP enumeration.

The following are some examples that can be gleaned from use of these scripts.

A couple of things:

* The output has been edited/sanitised

* I've added a -d (debug) and -v (verbose) for stdout.  

### smtp-enum-users

```
nmap -v -p [port] --script=smtp-enum-users [target] -d
```
```
Starting Nmap 7.25BETA2 ( https://nmap.org ) at 2017-02-15 23:37 GMT
--------------- Timing report ---------------
  hostgroups: min 1, max 100000
  rtt-timeouts: init 1000, min 100, max 10000
  max-scan-delay: TCP 1000, UDP 1000, SCTP 1000
  parallelism: min 0, max 0
  max-retries: 10, host-timeout: 0
  min-rate: 0, max-rate: 0
---------------------------------------------
NSE: Using Lua 5.3.
NSE: Arguments from CLI: 
NSE: Loaded 1 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 1) scan.
Initiating NSE at 23:37
Completed NSE at 23:37, 0.00s elapsed

Scanning [target] [1 port]

Discovered open port [port] on [target]
Completed SYN Stealth Scan at 23:55, 0.15s elapsed (1 total ports)
Overall sending rates: 6.75 packets / s, 297.20 bytes / s.
NSE: Script scanning [target].
NSE: Starting runlevel 1 (of 1) scan.
Initiating NSE at 23:37
NSE: Starting smtp-enum-users against [target].
NSE: Finished smtp-enum-users against [target].
Completed NSE at 23:37, 1.86s elapsed
Nmap scan report for [target]
Host is up, received arp-response (0.15s latency).
Scanned at 2017-02-15 23:37:06 GMT for 3s

PORT   STATE SERVICE REASON
[port] open  smtp    syn-ack ttl 128
| smtp-enum-users: 
|   RCPT, root
|   Method VRFY returned a unhandled status code.
|_  Method EXPN returned a unhandled status code.
MAC Address: [MAC Address]
Final times for host: srtt: 145105 rttvar: 109245  to: 582085

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 1) scan.
Initiating NSE at 23:37
Completed NSE at 23:37, 0.00s elapsed
Read from /usr/bin/../share/nmap: nmap-mac-prefixes nmap-payloads nmap-services.
Nmap done: 1 IP address (1 host up) scanned in 2.62 seconds
           Raw packets sent: 2 (72B) | Rcvd: 2 (72B)
```

### smtp-commands

```
nmap -v -p [ports] --script=smtp-commands [target]
```
```
Starting Nmap 7.25BETA2 ( https://nmap.org ) at 2017-02-15 23:37 GMT
NSE: Loaded 1 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 23:37
Completed NSE at 23:37, 0.00s elapsed
Initiating ARP Ping Scan at 23:37
Scanning [target] [1 port]
Completed ARP Ping Scan at 23:37, 0.14s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 23:37
Completed Parallel DNS resolution of 1 host. at 23:37, 0.04s elapsed
Initiating SYN Stealth Scan at 23:37
Scanning [target] [1 port]
Discovered open port [port] on [target]
Completed SYN Stealth Scan at 23:37, 0.15s elapsed (1 total ports)
NSE: Script scanning [target].
Initiating NSE at 23:37
Completed NSE at 23:37, 0.58s elapsed
Nmap scan report for [target]
Host is up (0.14s latency).

PORT   STATE SERVICE
[port] open  smtp
|_smtp-commands: localhost Hello nmap.scanme.org; ESMTPs are:, TIME, 
MAC Address: [MAC Address]

NSE: Script Post-scanning.
Initiating NSE at 23:37
Completed NSE at 23:37, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 1.34 seconds
           Raw packets sent: 2 (72B) | Rcvd: 2 (72B)
```

### smtp-open-relay
```
nmap -v -p [port] --script=smtp-open-relay [target]
```
```
Starting Nmap 7.25BETA2 ( https://nmap.org ) at 2017-02-15 23:37 GMT
NSE: Loaded 1 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 23:37
Completed NSE at 23:37, 0.00s elapsed
Initiating ARP Ping Scan at 23:37
Scanning [target] [1 port]
Completed ARP Ping Scan at 23:37, 0.14s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 23:37
Completed Parallel DNS resolution of 1 host. at 23:37, 0.03s elapsed
Initiating SYN Stealth Scan at 23:37
Scanning [target] [1 port]
Discovered open port [port] on [target]
Completed SYN Stealth Scan at 23:37, 0.14s elapsed (1 total ports)
NSE: Script scanning [target].
Initiating NSE at 23:37
Completed NSE at 23:37, 1.06s elapsed
Nmap scan report for [target]
Host is up (0.14s latency).

PORT   STATE SERVICE
[port] open  smtp
| smtp-open-relay: Server is an open relay (2/16 tests)
|  MAIL FROM:<> -> RCPT TO:<relaytest@nmap.scanme.org>
|_ SMTP: RSET 553 We do not relay non-local mail, sorry.
MAC Address: [MAC address]

NSE: Script Post-scanning.
Initiating NSE at 23:37
Completed NSE at 23:37, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 1.98 seconds
           Raw packets sent: 2 (72B) | Rcvd: 2 (72B)
```

> Your mileage may vary.  This content is constantly under development and may change at any time.