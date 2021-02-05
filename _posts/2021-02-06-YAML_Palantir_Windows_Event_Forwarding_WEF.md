---
layout: post
title: "YAML config for the Palantir Windows Event Forwarding recommendations"
description: "YAML config for the Palantir Windows Event Forwarding recommendations"
comments: true
keywords: "security, yaml, elk, elastic, database, servers, blueteam"
---

Duplicates from the ["Security Auditing and Monitoring Reference"](https://hannahsuarez.github.io/2021/Winlogbeat_NSAEventstoMonitor/) and ["Exploit Protection Events"](https://hannahsuarez.github.io/2021/ExploitProtectionEvents/) YAML configuration files are already taken out.

IDs are from the [Palantir WEF](https://github.com/palantir/windows-event-forwarding/) repo.

```
  #account management: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Account-Management.xml
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4765

  #active directory: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Active-Directory.xml
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 14080
        - equals.winlog.event_id: 4717

  #application crashes: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Application-Crashes.xml
  - name: Application
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1000
        - equals.winlog.event_id: 1002
    level: error
    provider:
      - Application Error
      - Application Hang
  - name: Application
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1001
    level: info
    provider:
      - Windows Error Reporting

  #applocker: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Applocker.xml
  - name: Microsoft-Windows-AppLocker/EXE and DLL
  - name: Microsoft-Windows-AppLocker/MSI and Script
  - name: Microsoft-Windows-AppLocker/Packaged app-Execution
  - name: Microsoft-Windows-AppLocker/Packaged app-Deployment

  #authentication: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Authentication.xml
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4624
        - equals.winlog.event_id: 4625
        - equals.winlog.event_id: 4626
        - equals.winlog.event_id: 4634
        - equals.winlog.event_id: 4647
        - equals.winlog.event_id: 4675
        - equals.winlog.event_id: 4800
        - equals.winlog.event_id: 4801
        - equals.winlog.event_id: 4802
        - equals.winlog.event_id: 4803
        - equals.winlog.event_id: 5378

  #autoruns: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Autoruns.xml
  #make sure to set up the scheduled autoruns service
  - name: Autoruns

  #bits: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Bits-Client.xml
  - name: Microsoft-Windows-Bits-Client/Operational

  #code integrity: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Code-Integrity.xml
  - name: Microsoft-Windows-CodeIntegrity/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 3001
        - equals.winlog.event_id: 3002
        - equals.winlog.event_id: 3003
        - equals.winlog.event_id: 3004
        - equals.winlog.event_id: 3010
        - equals.winlog.event_id: 3023
    level: error, warning
    provider:
      - Microsoft-Windows-CodeIntegrity

  #dns: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/DNS.xml
  - name: Microsoft-Windows-DNS-Client/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 3008
  - name: DNS Server
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 150
        - equals.winlog.event_id: 770
  #Check if DNS Server has audit enabled
  - name: Microsoft-Windows-DNSServer/Audit
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 541

  #device guard: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Device-Guard.xml
  - name: Microsoft-Windows-DeviceGuard/Operational

  #drivers: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Drivers.xml
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 219
    level: warning
    provider:
      - Microsoft-Windows-Kernel-PnP
  - name: Microsoft-Windows-DriverFrameworks-UserMode/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 2004

  #emet: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/EMET.xml
  - name: Application
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1
        - equals.winlog.event_id: 2
    level: warning, error
    provider:
      - EMET

  #event log diagnostics: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Event-Log-Diagnostics.xml
  - name: System
    provider:
      - Microsoft-Windows-Eventlog
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1100

  #external devices: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/External-Devices.xml
  - name: Microsoft-Windows-Kernel-PnP/Configuration
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 400
        - equals.winlog.event_id: 410
    level: info
    provider:
      - Microsoft-Windows-Kernel-PnP

  #firewall: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Firewall.xml
  - name: Microsoft-Windows-Windows Firewall With Advanced Security/Firewall
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 2004
        - equals.winlog.event_id: 2005
        - equals.winlog.event_id: 2006
        - equals.winlog.event_id: 2033
    level: info, error
    provider:
      - Microsoft-Windows-Windows Firewall With Advanced Security

  #gpo errors: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Group-Policy-Errors.xml
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1085
        - equals.winlog.event_id: 1125
        - equals.winlog.event_id: 1127
        - equals.winlog.event_id: 1129
    level: error
    provider:
      - Microsoft-Windows-GroupPolicy

  #kerberos: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Kerberos.xml
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4769
        - equals.winlog.event_id: 4770
        - equals.winlog.event_id: 4773

  #log deletion system: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Log-Deletion-System.xml
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 104
    level: info
    provider:
      - Microsoft-Windows-Eventlog

  #msi: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/MSI-Packages.xml
  - name: Application
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1022
        - equals.winlog.event_id: 1033
    provider:
      - MsiInstaller
  - name: Setup
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 2
        - equals.winlog.event_id: 0
    provider:
      - Microsoft-Windows-Servicing
  - name: Microsoft-Windows-Application-Experience/Program-Inventory
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 903
        - equals.winlog.event_id: 904
    provider:
      - Microsoft-Windows-Application-Experience
  - name: Microsoft-Windows-Application-Experience/Program-Inventory
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 905
        - equals.winlog.event_id: 906
    provider:
      - Microsoft-Windows-Application-Experience
  - name: Microsoft-Windows-Application-Experience/Program-Inventory
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 907
        - equals.winlog.event_id: 908
    provider:
      - Microsoft-Windows-Application-Experience
  - name: Microsoft-Windows-Application-Experience/Program-Inventory
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 800
    provider:
      - Microsoft-Windows-Application-Experience

  #office: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Microsoft-Office.xml
  - name: OAlerts

  #ntml: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/NTLM.xml
  - name: Microsoft-Windows-Authentication/AuthenticationPolicyFailures-DomainController
    provider:
      - Microsoft-Windows-NTLM
  - name: Microsoft-Windows-Authentication/ProtectedUserFailures-DomainController
    provider:
      - Microsoft-Windows-NTLM
  - name: Microsoft-Windows-NTLM/Operational
    provider:
      - Microsoft-Windows-NTLM

  #operating system: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Operating-System.xml
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 12
        - equals.winlog.event_id: 13
    provider:
      - Microsoft-Windows-Kernel-General
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4608
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1074
    provider:
      - USER32
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 16962
        - equals.winlog.event_id: 16965
        - equals.winlog.event_id: 16968
        - equals.winlog.event_id: 16969
  - name: Microsoft-Windows-SMBServer/Audit
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 3000
    provider:
      - Microsoft-Windows-SMBServer
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 41
        - equals.winlog.event_id: 1001
        - equals.winlog.event_id: 6008
        - equals.winlog.event_id: 4621

  #powershell: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Powershell.xml
  - name: Microsoft-Windows-PowerShell/Operational
  - name: Microsoft-Windows-PowerShell-DesiredStateConfiguration-FileDownloadManager/Operational
  - name: Windows PowerShell

  #print: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Print.xml
  - name: Microsoft-Windows-PrintService/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 307
    level: info
    provider:
      - Microsoft-Windows-PrintService

  #services: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Services.xml
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 7022
        - equals.winlog.event_id: 7023
        - equals.winlog.event_id: 7024
        - equals.winlog.event_id: 7026
        - equals.winlog.event_id: 7031
        - equals.winlog.event_id: 7032
        - equals.winlog.event_id: 7034
    level: info, critical, error, warning
    provider:
      - Service Control Manager
  - name: System
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 7045
        - equals.winlog.event_id: 7040
    level: info, critical, error, warning
    provider:
      - Service Control Manager

  #shares: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Shares.xml
  - name: Microsoft-Windows-SMBClient/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 30622
        - equals.winlog.event_id: 30624
  - name: Microsoft-Windows-SMBClient/Security
  - name: Microsoft-Windows-SMBServer/Security

  #smart card: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Smart-Card.xml
  - name: Microsoft-Windows-SmartCard-Audit/Authentication

  #software restrictions: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Software-Restriction-Policies.xml
  - name: Application
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 865
        - equals.winlog.event_id: 866
        - equals.winlog.event_id: 867
        - equals.winlog.event_id: 868
        - equals.winlog.event_id: 882
    provider:
      - Microsoft-Windows-SoftwareRestrictionPolicies

  #sysmon: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Sysmon.xml
  - name: Microsoft-Windows-Sysmon/Operational

  #system time change: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/System-Time-Change.xml
  - name: Security
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 4616

  #task scheduler: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Task-Scheduler.xml
  - name: Microsoft-Windows-TaskScheduler/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 106
        - equals.winlog.event_id: 129
        - equals.winlog.event_id: 141
        - equals.winlog.event_id: 142
        - equals.winlog.event_id: 200
        - equals.winlog.event_id: 201
    provider:
      - Microsoft-Windows-TaskScheduler

  #terminal services: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Terminal-Services.xml
  - name: Microsoft-Windows-TerminalServices-Gateway/Admin
  - name: Microsoft-Windows-TerminalServices-Gateway/Operational
  - name: Microsoft-Windows-TerminalServices-ClientUSBDevices/Admin
  - name: Microsoft-Windows-TerminalServices-ClientUSBDevices/Operational
  - name: Microsoft-Windows-TerminalServices-PnPDevices/Admin
  - name: Microsoft-Windows-TerminalServices-PnPDevices/Operational
  - name: Microsoft-Windows-TerminalServices-Printers/Admin
  - name: Microsoft-Windows-TerminalServices-Printers/Operational
  - name: Microsoft-Windows-TerminalServices-ServerUSBDevices/Admin
  - name: Microsoft-Windows-TerminalServices-ServerUSBDevices/

  #wmi: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/WMI.xml
  - name: Microsoft-Windows-WMI-Activity/Operational
  - name: Microsoft-Windows-TPM-WMI

  #windows defender: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Windows-Defender.xml
  - name: Microsoft-Windows-Windows Defender/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1006
        - equals.winlog.event_id: 1007
        - equals.winlog.event_id: 1008
        - equals.winlog.event_id: 1009
  - name: Microsoft-Windows-Windows Defender/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1116
        - equals.winlog.event_id: 1117
        - equals.winlog.event_id: 1118
        - equals.winlog.event_id: 1119

  #windows update: https://github.com/palantir/windows-event-forwarding/blob/master/wef-subscriptions/Windows-Updates.xml
  - name: Microsoft-Windows-WindowsUpdateClient/Operational
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 19
        - equals.winlog.event_id: 20
        - equals.winlog.event_id: 24
        - equals.winlog.event_id: 25
        - equals.winlog.event_id: 31
        - equals.winlog.event_id: 34
        - equals.winlog.event_id: 35
    level: error
    provider:
      - Microsoft-Windows-WindowsUpdateClient
  - name: Setup
    processors:
      - drop_event.when.not.or:
        - equals.winlog.event_id: 1009
    level: info
    provider:
      - Microsoft-Windows-Servicing
```

> Note: These are from 2019, so there may have been changes in terms of event ingestion.

> YMMV! Your mileage may vary.
