---
layout: post
title: "Collecting Windows Ingress Authentication Events using Rapid7 Universal Event Formats"
description: "Rapid7 released Universal Event Formats (UEF) as a way to allow event sources to make use of Rapid7 user behavior analytics (UBA) for DHCP, antivirus, ingress authentications, and VPN events. This post is on ingress authentication for Windows host sources."
comments: true
keywords: "logging, log collection, log management, SIEM, SIEM suite, Rapid7"
---

In October 2018, Rapid7 released Universal Event Formats (UEF) as a way to allow event sources to make use of Rapid7 [user behavior analytics (UBA)](https://www.rapid7.com/solutions/user-behavior-analytics/) for DHCP, antivirus, ingress authentications, and virtual private network events.

UEF is not a log or data source but rather it is more like a ‘contract’. For UEF to work, the data will need to be transformed to meet these fields. The specific fields will depend on what type of [Universal Event Source](https://insightidr.help.rapid7.com/docs/rapid7-universal-event-sources) is used although some fields typically share the same attributes such as time (must be a valid ISO 8601 format), event type, version, and additional field for any custom data.

## Why ingress authentication?

In networking, you typically have both ingress (inbound) and egress (outbound) points. Such points can be situated at the perimeter or as part of network segmentation (ie to enforce access control policies). Ingress authentication are events which involve authentication (also, authentication attempts) inbound into a network resource. For instance, a firewall is set up to defend a network ingress and ingress filtering is used as a way to defend a resource against DoS/DDoS attacks. Expected ingress authentication activity would be a staff member accessing an internal network resource through their VPN with all of these access points being right for that staff member (ie they have the right clearances for that resource for example). Events that are not expected would be a recently fired employee attempting to access such resource or authentication activity from an account that is not enabled.

## ATT&CK Matrix for Enterprise

The MITRE ATT&CK Matrix resource as another way to build potential adversary scenarios and understand as to why collecting log data points of ingress authentication events is important from an incident management point of view. Ingress events are like the heartbeat to finding indicators of initial access with the adversary attempting to get into your network through vectors such as public facing servers and through means such as the use of valid accounts.

## Collecting Windows Ingress Authentication and rewriting them to the Universal Event Format

While Rapid7 published a [post](https://blog.rapid7.com/2018/10/16/universal-event-formats-in-insightidr-a-step-by-step-nxlog-guide/) utilizing the KVP module and other modules available as free/open source community software NXLog Community Edition, there is also another method but utilizes the rewrite module, the [xm_rewrite](https://nxlog.co/documentation/nxlog-user-guide/xm_rewrite.html), which allows fields to be renamed, kept (whitelisted), or deleted (blacklisted).

Being able to configure which fields to keep, delete, and rewrite is required to write the log data in the UEF contract. For example, the raw data field for time needs to be written in the ISO 8601 format, for example.

## Finding which fields to write

To find which fields are available, inspect the raw data of that log source. In this case the source is Windows EventLog so the raw XML data is inspected to locate which fields are pertinent for two authentication EventLog IDs — 4625 (An account has failed to log on) and 4624 (An account has successfully logged on).

## Check the logs are indexed on Rapid7

Log collection validation happens in two stages. The first stage is to check that the raw logs are actually being collected for that log data source input.

The second, and most important stage, is to confirm that the logs are indexed on the Rapid7 Log Search section. Without indexing, the raw data is pretty much useless. Lack of index can indicate that the Universal Event Format contract has not been met. Make sure that the fields are all lowercase (since the field names are case sensitive), that the fields being chosen to rewrite are correct, that the timestamps are in ISO 8601 format.

##Example log entry of an ingress authentication attempt to an EC2 resource

Since the endpoint in which log collection has taken place is on an EC2 instance, there were some interesting IPs already knocking on the door.

![Photo](/assets/images/belarus_insightidr.png)

## Creating a test dashboard for UEF Ingress Authentication sample events

![Photo](/assets/images/insightidr_dashboard.png)

Overall, there are at least two methods (or modules offered by NXLog) to write fields to meet the UEF contract for setting up a data source utilizing the Rapid7 Universal Event Format. There are already other ways to collect security events on Windows EventLog including their [Generic Windows EventLog](https://insightidr.help.rapid7.com/docs/generic-windows-event-log) data source and you can even convert EventLog to a Syslog format (Syslog Snare) for the [Generic Syslog](https://insightidr.help.rapid7.com/docs/generic-syslog) data source, or if these are converted to JSON or some other KVP format, one can the use [Raw Data](https://insightidr.help.rapid7.com/docs/raw-data) option as the data source input. UEF was, of course, the only option that automatically allocates some further details to aid in user attribution.

## Universal Event Format versus EventLog in Structured Log (JSON, in this case) or going beyond Structured Log Collection.

Another case is that even while the EventID being collected is the same (4625, 4624 events) there is no additional processing from the Rapid7 InsightIDR end. Below is a log sample in JSON format from Security event in Snare Syslog format which does show failed log in attempt for ‘Administrator’ from a another attempt, this time from a Netherlands-based IP. The fields have not been rewritten, for example, ip_address should be source_ip.

```
01 Aug 2019 17:46:45.291{
“timestamp”: “2019–08–01T21:46:43.000Z”,
“hostname”: “Collector_HOST”,
“event_code”: “4625”,
“description”: “An account failed to log on.”,
“subject_user_sid”: “S-1–0–0”,
“subject_user_name”: “-”,
“subject_domain_name”: “-”,
“subject_logon_id”: “0x0”,
“logon_type”: “Network”,
“target_user_sid”: “S-1–0–0”,
“target_user_name”: “ADMINISTRATOR”,
“target_domain_name”: “”,
“failure_reason”: “Unknown user name or bad password.”,
“status”: “username or password incorrect”,
“sub_status”: “user name is correct but the password is wrong”,
“process_id”: “0x0”,
“process_name”: “-”,
“workstation_name”: “-”,
“ip_address”: “212.92.116.56”,
“ip_port”: “0”,
“logon_process_name”: “NtLmSsp”,
“authentication_package_name”: “NTLM”,
“transmitted_services”: “-”,
“lm_package_name”: “-”,
“key_length”: “0”,
“source_data”: “<11>Aug 1 17:46:43 NXLog.ec2–18–222–186–72.us-east-2.compute.amazonaws.com MSWinEventLog\t3\tSecurity\t77\tThu Aug 01 17:46:43 2019\t4625\tMicrosoft-Windows-Security-Auditing\tN/A\tN/A\tFailure Audit\tCollector_HOST\tLogon\t\tAn account failed to log on. Subject: Security ID: S-1–0–0 Account Name: — Account Domain: — Logon ID: 0x0 Logon Type: 3 Account For Which Logon Failed: Security ID: S-1–0–0 Account Name: ADMINISTRATOR Account Domain: Failure Information: Failure Reason: Unknown user name or bad password. Status: 0xC000006D Sub Status: 0xC000006A Process Information: Caller Process ID: 0x0 Caller Process Name: — Network Information: Workstation Name: — Source Network Address: 212.92.116.56 Source Port: 0 Detailed Authentication Information: Logon Process: NtLmSsp Authentication Package: NTLM Transited Services: — Package Name (NTLM only): — Key Length: 0 This event is generated when a logon request fails. It is generated on the computer where access was attempted. The Subject fields indicate the account on the local system which requested the logon. This is most commonly a service such as the Server service, or a local process such as Winlogon.exe or Services.exe. The Logon Type field indicates the kind of logon that was requested. The most common types are 2 (interactive) and 3 (network). The Process Information fields indicate which account and process on the system requested the logon. The Network Information fields indicate where a remote logon request originated. Workstation name is not always available and may be left blank in some cases. The authentication information fields provide detailed information about this specific logon request. — Transited services indicate which intermediate services have participated in this logon request. — Package name indicates which sub-protocol was used among the NTLM protocols. — Key length indicates the length of the generated session key. This will be 0 if no session key was requested.\t223050”
}
```

---

## What are your thoughts? Would UEF be a better way to ingest ingress authentication data or would the above Syslog format be enough?

Read the original post [here](https://medium.com/@hannahsuarez/collecting-windows-ingress-authentication-events-using-rapid7-universal-event-formats-283c4dc61f56
).
