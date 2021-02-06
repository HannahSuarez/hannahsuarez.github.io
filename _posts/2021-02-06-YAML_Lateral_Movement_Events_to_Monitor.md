---
layout: post
title: "YAML Config Snippet of JPCERT Lateral Movement Events to Monitor (Windows)"
description: "YAML Config Snippet of JPCERT Lateral Movement Events to Monitor (Windows)"
comments: true
keywords: "security, yaml, elk, elastic, database, servers, blueteam, JPCERT"
---

The following are lateral movement events based on [JPCERT](https://jpcertcc.github.io/ToolAnalysisResultSheet/).

Follow the comments for the name of the source of lateral movement (ie command execution, remote login, etc).

These IDs are related to the following: PsExec, wmic, schtasks, wmiexec.vbs, BeginX, winrm, BITS, pwdump7, pwdumpx, quarks_pwdump, mimikatz, wce, gsecdump, lslass, acehash, find-gpo-passwr,ds get-gpppassword, invoke-mimikatz, out-minidump, powermemory, webbrowserpass, htran, fake_wpad, rdp_remote, wce_remote_login, mimikatz_remotelogin, ms14-058, ms15-078, sdb-uac-bypass, ms14-068, golden_ticket_mimikatz, silver_ticket_mimikatz, ntdsutil, vssadmin, csvde, ldifde, dsquery, dcdiag, nltest, nmap, net_user, net_use, sdelete, timestomp, klist_purse, wevutil

Double check that events can be collected in the first place, for example, ensure to enable Sysmton (though you may already know that!)

```
  - name: Microsoft-Windows-Sysmon/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1
        - equals.winlog.event_id: 2
        - equals.winlog.event_id: 3
        - equals.winlog.event_id: 5
        - equals.winlog.event_id: 8
        - equals.winlog.event_id: 9
        - equals.winlog.event_id: 10
        - equals.winlog.event_id: 11
        - equals.winlog.event_id: 12
        - equals.winlog.event_id: 13

  - name: Security
    event_id:  4611
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4624
        - equals.winlog.event_id: 4656
        - equals.winlog.event_id: 4658
        - equals.winlog.event_id: 4660
        - equals.winlog.event_id: 4661
        - equals.winlog.event_id: 4663
        - equals.winlog.event_id: 4670
        - equals.winlog.event_id: 4672
        - equals.winlog.event_id: 4673
        - equals.winlog.event_id: 4674
        - equals.winlog.event_id: 4674
        - equals.winlog.event_id: 4688
        - equals.winlog.event_id: 4689
        - equals.winlog.event_id: 4690
        - equals.winlog.event_id: 4703
        - equals.winlog.event_id: 4726
        - equals.winlog.event_id: 4728
        - equals.winlog.event_id: 4737
        - equals.winlog.event_id: 4768
        - equals.winlog.event_id: 4769
        - equals.winlog.event_id: 4771
        - equals.winlog.event_id: 4776
        - equals.winlog.event_id: 4779
        - equals.winlog.event_id: 4904
        - equals.winlog.event_id: 4905
        - equals.winlog.event_id: 5140
        - equals.winlog.event_id: 5152
        - equals.winlog.event_id: 5156
        - equals.winlog.event_id: 5158
        - equals.winlog.event_id: 5159
        - equals.winlog.event_id: 5447
        - equals.winlog.event_id: 8222

  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 104, 7036, 7045, 20001

  - name: Application
  processors:
    - drop_event.when.not.or:
      - equals.winlog.event_id: 102
      - equals.winlog.event_id: 105
      - equals.winlog.event_id: 300
      - equals.winlog.event_id: 216
      - equals.winlog.event_id: 302
      - equals.winlog.event_id: 2001
      - equals.winlog.event_id: 2003
      - equals.winlog.event_id: 2005
      - equals.winlog.event_id: 2006

  - name: Microsoft-Windows-Kernel-PnPConfig/Configuration
  processors:
    - drop_event.when.not.or:
      - equals.winlog.event_id: 1
      - equals.winlog.event_id: 4
      - equals.winlog.event_id: 400
      - equals.winlog.event_id: 410

  - name: Microsoft-Windows-WinRM/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4
        - equals.winlog.event_id: 6
        - equals.winlog.event_id: 8
        - equals.winlog.event_id: 10
        - equals.winlog.event_id: 11
        - equals.winlog.event_id: 13
        - equals.winlog.event_id: 15
        - equals.winlog.event_id: 16
        - equals.winlog.event_id: 29
        - equals.winlog.event_id: 30
        - equals.winlog.event_id: 31
        - equals.winlog.event_id: 33
        - equals.winlog.event_id: 80
        - equals.winlog.event_id: 81
        - equals.winlog.event_id: 82
        - equals.winlog.event_id: 83
        - equals.winlog.event_id: 132
        - equals.winlog.event_id: 134
        - equals.winlog.event_id: 143
        - equals.winlog.event_id: 166
        - equals.winlog.event_id: 169
        - equals.winlog.event_id: 192
        - equals.winlog.event_id: 193

  - name: Microsoft-Windows-TerminalServices-RDPClient/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1024
        - equals.winlog.event_id: 1026
        - equals.winlog.event_id: 1028
        - equals.winlog.event_id: 1029
        - equals.winlog.event_id: 1105

  - name: Microsoft-Windows-TerminalServices-RemoteConnectionManager/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 261
        - equals.winlog.event_id: 1149

  - name: Microsoft-Windows-WMI-Activity/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 5857

  - name: Microsoft-Windows-TaskScheduler/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 106
        - equals.winlog.event_id: 129
        - equals.winlog.event_id: 200
        - equals.winlog.event_id: 201

  - name: Microsoft-Windows-TerminalServices-LocalSessionManager/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 21
        - equals.winlog.event_id: 24
        - equals.winlog.event_id: 25

  - name: Microsoft-Windows-TaskScheduler/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 106
        - equals.winlog.event_id: 129
        - equals.winlog.event_id: 200
        - equals.winlog.event_id: 201

  - name: Microsoft-Windows-Bits-Client/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 3
        - equals.winlog.event_id: 4
        - equals.winlog.event_id: 59
        - equals.winlog.event_id: 60

  - name: Microsoft-Windows-Application-Experience/Program-Telemetry
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 500

  - name: Microsoft-Windows-PowerShell/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4104
        - equals.winlog.event_id: 8193
        - equals.winlog.event_id: 8194
        - equals.winlog.event_id: 8195
        - equals.winlog.event_id: 8196
        - equals.winlog.event_id: 8197
        - equals.winlog.event_id: 12039
        - equals.winlog.event_id: 40961
        - equals.winlog.event_id: 40962
        - equals.winlog.event_id: 53504
```

> YMMV! Your mileage may vary.
