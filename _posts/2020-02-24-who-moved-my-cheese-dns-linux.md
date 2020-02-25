---
layout: post
title: "Who moved my DNS cheese? BIND 9 DNS Log Collection and DNS Auditing"
description: "Who moved my DNS cheese? The Linux edition"
comments: true
keywords: "dns,dhcp,bind9,bind,linux,rhel,nxlog"
---

If you setting up native DNS audit logging on MSAD DNS servers you may already be familiar with this 2013 blog post [Who moved the DNS Cheese? Auditing for AD Integrated DNS Zone and Record Deletions](https://blogs.technet.microsoft.com/askpfeplat/2013/10/12/who-moved-the-dns-cheese-auditing-for-ad-integrated-dns-zone-and-record-deletions/).

Over the past week, I have been spending a lot of time looking into DNS log collection and auditing both for Windows and, initially, Linux but then moved focus on to open source flavors of DNS server implementations. The world of DNS log collection is actually quiet immense, once you also include cloud infrastructure as well as some of the newer implementations of the DNS protocol (ie DoH). It's out of the scope of this post but there should hopefully be a longer article out (in another place) sometime in the next month or so.

During that time last week, I had looked into a few open source DNS servers/other implementations (ie DNS recursion), and also installed the latest [BIND 9 server](https://www.isc.org/bind/) to set up various forms of log collection on it including DNS auditing. Before that though, a couple of tips related to BIND 9 log collection for DNS:

* For each category (like `networking` or `queries`) you may want to set up a separate channel for this.  A channel is either a Syslog stream or it could be a file that will have logs written to it.

* When setting up log collection, make sure that the process has access to read the Syslog stream.

* When setting up file-based log collection, ensure that the process has write access to the file itself. Check the AppArmor rules for BIND.

* In fact you should read this post by ISC2 [BIND Logging - some basic recommendations](https://kb.isc.org/docs/aa-01526) because you can't go wrong with that.

---

## Setting up DNS Auditing

RHEL has a very good resource ["Understanding audit log files"](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sec-understanding_audit_log_files) which talks about some of the terms that get used and that you should know when it is time to read the DNS audit logs.

In my [Linux auditing input module configuration](https://nxlog.co/documentation/nxlog-user-guide/im_linuxaudit.html), I create a rule to watch any write and access to `/etc/bind/named.conf` and, as part of the log output there will also be a tag `conf-change-bind` which makes it useful for structured log data and event correlation:


```
-w /etc/bind/named.conf -p wa -k conf-change-bind
```
Results are then output to a log file written in JSON format, here are a few examples taken over a small period of time:

```
{
"type":"CONFIG_CHANGE",
"time":"2020-02-21T01:30:36.027000+01:00",
"seq":31,
"auid":4294967295,
"ses":"1234957866",
"subj":"=unconfined",
"op":0,
"key":"conf-change-bind",
"list":"4",
"res":"1",
"EventReceivedTime":"2020-02-21T01:30:36.034819+01:00",
"SourceModuleName":"audit",
"SourceModuleType":"im_linuxaudit"
}
```
```
{
"type":"CONFIG_CHANGE",
"time":"2020-02-21T01:30:36.027000+01:00",
"seq":31,"auid":4294967295,
"ses":"4294967295",
"subj":"=unconfined",
"op":0,"
key":"configuration-change-dns-server",
"list":"4",
"res":"1",
"EventReceivedTime":"2020-02-21T01:30:36.034819+01:00",
"SourceModuleName":"audit",
"SourceModuleType":"im_linuxaudit"
}
```
```
{
"type":"CONFIG_CHANGE",
"time":"2020-02-21T02:03:48.393000+01:00",
"seq":3,"auid":4294967295,
"ses":"4294967295",
"subj":"=unconfined",
"op":0,
"key":"conf-change-bind",
"list":"4",
"res":"1",
"EventReceivedTime":"2020-02-21T02:03:48.396916+01:00",
"SourceModuleName":"audit",
"SourceModuleType":"im_linuxaudit"
}
```
### Reading the Linux Audit Log for DNS Server Configuration Changes

The below log contains the same `configuration-change-dns-server` but has additional information. Go to [Audit Record Types](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sec-Audit_Record_Types) documentation by RHEL for the list of audit record types.

```
{
"type":"SYSCALL",
"time":"2020-02-21T02:20:32.365000+01:00",
"seq":165,
"arch":"c000003e",
"syscall":"257",
"success":"yes",
"exit":3,
"a0":"ffffff9c",
"a1":"563b82d382a0",
"a2":"441",
"a3":"1b6",
"items":2,
"ppid":1739,
"pid":1740,
"auid":2000,
"uid":0,
"gid":0,
"euid":0,
"suid":0,
"fsuid":0,
"egid":0,
"sgid":0,
"fsgid":0,
"tty":"pts2",
"ses":"2",
"comm":"nano",
"exe":"/bin/nano",
"subj":"=unconfined",
"key":"conf-change-bind",
"EventReceivedTime":"2020-02-21T02:20:32.373192+01:00",
"SourceModuleName":"audit",
"SourceModuleType":"im_linuxaudit"
}
```

**Some things of note:**

The `auid` records the Audit user ID and for any other logs you can also trace back to other events associated with this `auid`.

The `uid` and `gid` is 0 which indicates superuser account.

The `comm` indicates what command was used. In this case we know that `nano` was invoked to change the DNS configuration file and the path to the executable is `/bin/nano`

---

Read more about [DNS Monitoring](https://nxlog.co/documentation/nxlog-user-guide/dns-monitoring.html) and the [Linux Audit System](https://nxlog.co/documentation/nxlog-user-guide/linux-audit.html).
