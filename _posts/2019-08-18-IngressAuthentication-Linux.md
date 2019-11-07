---
layout: post
title: "Collecting Linux Ingress Authentication Events using Rapid7 Universal Event Formats"
description: "Rapid7 released Universal Event Formats (UEF) as a way to allow event sources to make use of Rapid7 user behavior analytics (UBA) for DHCP, antivirus, ingress authentications, and VPN events. This post is on ingress authentication for Linux host sources."
comments: true
keywords: "logging, log collection, log management, SIEM, SIEM suite, Rapid7"
---

First..practical points on collecting ingress logs from Linux vs Windows

One obvious factor is how straight forward it is to set up log collection for a typical (authentication to a Windows Server with username/password via RDP from an outside network) Windows server ingress scenario. The structured XML data source that underpins EventLog already has existing fields to draw upon. In this case, just collecting EventIDs 4625 (An account has failed to log on) and 4624 (An account has successfully logged on) is enough to set up basic log collection.
Things change for Linux, because the same type of scenario (authentication to a Linux Server with PEM-formatted certificate via SSH) requires further steps. This is because the event is delivered in a semi-structured format where some of the data is structure in key-value pairs and the rest are in unstructured $Message field.

These are, in somewhat of an order:

* Locate what the raw fields are for the Syslog-formatted authentication event.

* In the raw data $Message field, locate which string to monitor to determine if the ingress activity was a failure or success.

* In the raw data $Message field, locate which string to monitor to obtain the account where access was attempted as well as the Source IP.

* Correct chown permissions for the /var/auth.log file.

However, these are only a few extra steps. While I only tested with one scenario, this should be adaptable for other semi-structured log sources, such as ingress authentication logs to Kubernetes resource, for example.

Thus the working (-not- final) sample (using NXLog xm_rewrite) to test out Rapid7 Universal Event Format for Linux Ingress Authentication is below:

```
<Extension rewrite>
Module xm_rewrite
# The syslog raw data needs to be parsed first
Exec parse_syslog();
Keep Hostname, account, version, user, custom_message, Message, event_type, EventReceivedTime, authentication_result, raw_event, authentication_target, source_ip
# These fields are generated from parse_syslog(); and should be dropped.
Delete SourceModuleName, SourceModuleType, Severity, SeverityValue, SyslogSeverityValue
Rename HostName, authentication_target
Rename EventReceivedTime, time
Rename Message, custom_message
</Extension>
# end::xm_rewrite_include[]
# tag::guide_include[]
<Input in_auth>
Module im_file
File “/var/log/auth.log”
<Exec>
# Convert the $EventReceivedTime string to ISO 8601 extended format.
$EventReceivedTime = strftime($EventReceivedTime, ‘%Y-%m-%dT%H:%M:%SZ’);
# Add the required input for $version
$version = “v1”;
# Add the required input for $event_type
$event_type = “INGRESS_AUTHENTICATION”;
# Use xm_rewrite module earlier in order to use the $source_ip and $account
fields
rewrite->process();
# Obtain the $source_ip and $account string data from $raw_event
if ($raw_event =~ /Accepted publickey for\ (\S+)\ from\ (\S+)/)
{
$account = $1;
$source_ip = $2;
}
# Success and Authentication messages based on the $raw_event field
if ($raw_event =~ /authentication failure/) { $authentication_result = “FAILURE”; } \
else if ($raw_event =~ /successfully authenticated/) { $authentication_result = “SUCCESS”; } \
# Ensure that only failure and success messages are logged
else drop();
# Convert to JSON
to_json();
</Exec>
</Input>
```

Which then yields the following output:

```
{
“time”:”2019–08–17T18:15:27Z”,
“version”:”v1",
“event_type”:”INGRESS_AUTHENTICATION”,
“account”:”admin”,
“source_ip”:”170.6.165.175",
“authentication_result”:”SUCCESS”,
“authentication_target”:”Not-My-Workstation”,
“custom_message”:”Accepted publickey for admin from 170.6.165.175 port 58790 ssh2: RSA SHA256:4kF2ePnGIDf2orwwph99pbMCgPs57FHHWBj7E”
}
```

Which is a lot nicer than dealing multiple log lines, that still needs other important metadata extracted from the raw field, like this line from another test run:

```
Aug 16 20:25:09 Not-My-Workstation sshd[9131]: Accepted publickey for admin from 170.6.165.175 port 58790 ssh2: RSA SHA256:4kF2ePnGIDf2orwwph99pbMCgPs57FHHWBj7E
```

This post is a continuation to another post written earlier which includes details for Windows. Read the original post [here](https://medium.com/@hannahsuarez/unifying-ingress-authentications-lessons-learnt-f12dde56a93b
).)

---

## What are your thoughts? Would UEF be a better way to ingest ingress authentication data or would the above Syslog format be enough?

Read the original post [here](https://medium.com/@hannahsuarez/unifying-ingress-authentications-lessons-learnt-f12dde56a93b
).
