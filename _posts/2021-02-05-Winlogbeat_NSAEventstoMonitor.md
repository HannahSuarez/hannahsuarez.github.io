---
layout: post
title: "YAML config for NSA Events to Monitor List"
description: "YAML file for NSA Events to Monitor List"
comments: true
keywords: "security, yaml, elk, elastic, database, servers, blueteam"
---

Read more at [Spotting the Adversary with Windows Event Log Monitoring (version 2)](https://apps.nsa.gov/iaarchive/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm).

```
  - name: Security

  - name: Application

  - name: System

  # define Account Usage events in the Security channel
  - name: Security
    event_id: 4740, 4648, 4781, 4733, 4776, 5376, 5377, 4625, 300, 4634, 4672, 4720, 4722, 4782, 4793, 4731, 4735, 4766, 4765, 4624, 4726, 4725, 4767, 4728, 4732, 4756, 4704

  # define Account Usage events in the Application channel
  - name: Application
    event_id: 1518, 1511

  # define Account Usage events in LSA channel
  - name: Microsoft-Windows-LSA/Operational
    event_id: 300

  # define Application Crashes event in the Application channel
  - name: Application
    event_id: 1000, 1002, 1001

  # define Application Crashes event in the System channel
  - name: Microsoft-Windows-WER-SystemErrorReporting
    event_id: 1001

  # define Application Whitelisting events in AppLocker
  - name: Microsoft-Windows-AppLocker/Packaged app-Deployment, Microsoft-Windows-AppLocker/Packaged app-Execution, Microsoft-Windows-AppLocker/EXE and DLL, Microsoft-Windows-AppLocker/MSI and Script
    event_id: 8023, 8020, 8002, 8003, 8004, 8006, 8007, 8005

  # define Application Whitelisting events in Security Channel
  - name: Security
    event_id: 4688, 4689

  # define Application Whitelisting events
  - name: Microsoft-Windows-SoftwareRestrictionPolicies
    event_id: 865, 866, 867, 868, 882

  # define Boot Events in the System channel
  - name: System
    event_id: 13, 12

  # define Boot Events in the User32 channel
  - name: User32
    event_id: 1074

  # define Certificate Services events in the Application channel
  - name: Application
    event_id:  95

  # define Certificate Services events in the Security channel
  - name: Security
    event_id: 4886, 4890, 4874, 4873, 4870, 4887, 4885, 4899, 4896

  # define Certificate Services events in the WindowsCertificateServices channel
  - name: Microsoft-Windows-CertificateServicesClientLifecycle-System
    event_id: 1006, 1004, 1007, 1003, 1001, 1002

  # define Clearing EventLogs events in the Security channel
  - name: Security
    event_id: 1100, 1102

  # define Clearing EventLogs events in the System channel
  - name: Security
    event_id: 104

  # define DNS and Directory Services events in the Security channel
  - name: Security
    event_id: 5137, 5141, 5136, 5139, 5138

  # define DNS and Directory Services events in the DNS Client channel
  - name: Microsoft-Windows-DNS-Client/Operational
    event_id: 3008, 3020

  # define External Media Detection events
  - name: Microsoft-Windows-Kernel-PnP/Device Configuration
    event_id: 400, 410

  # define Group Policy Errors events
  - name: Microsoft-Windows-GroupPolicy
    event_id: 1126, 1129, 112

  # define Kernel Driver Signing events in the System channel
  - name: System
    event_id: 219

  # define Kernel Driver Signing events in the Security channel
  - name: Security
    event_id: 5038, 6281

  # define Kernel Driver Signing events in the CodeIntegrity channel
  - name: Microsoft-Windows-CodeIntegrity/Operational
    event_id: 3001, 3002, 3003, 3004, 3010, 3023

  # define Microsoft Cryptography API events
  - name: Microsoft-Windows-CAPI2/Operational
    event_id: 11, 70, 90

  # define Mobile Device Activities events in NetworkProfile
  - name: Microsoft-Windows-NetworkProfile/Operational
    event_id: 10000, 10001

  # define Mobile Device Activities events in WLAN AutoConfig
  - name: Microsoft-Windows-WLAN-AutoConfig/Operational
    event_id: 8003, 8000, 8011, 8001, 11000, 11001, 11002, 12011, 12012, 12013, 8002, 11004, 11005, 11010, 11006

  # define Network Host Activities events in the Security channel
  - name: Security
    event_id: 4714, 4713, 4769, 6273, 6275, 6274, 6272, 6278, 6277, 6279, 6276, 6280, 5140, 5145, 5142, 5144, 4706, 4897, 4719, 4716, 4779, 4778, 5632

  # define Network Host Activities events in RDP Operational channel
  - name: Microsoft-Windows-TerminalServices-RDPClient/Operational
    event_id: 1024

  # define Network Host Activities events in RemoteAccess channel
  - name: Microsoft-Windows-MPRMSG
    event_id: 20250, 20274, 20275

  # define PowerShell Activities events in PS Operational Channel
  - name: Microsoft-Windows-Powershell/Operational
    event_id: 4103, 4104, 4105, 4106

  # define PowerShell Activities events
  - name: Powershell
    event_id: 800, 169

  # define Printing Services events
  - name: Microsoft-Windows-PrintService/Operational
    event_id: 307

  # define Software Service Installation events in Program-Inventory
  - name: Microsoft-Windows-Application-Experience/Program-Inventory
    event_id: 903, 904, 907, 908, 800, 905, 906

  # define Software Service Installation events in Application channel
  - name: Microsoft-Windows-Application-Experience/Program-Inventory
    event_id: 1022, 1033

  # define Software Service Installation events in System channel
  - name: System
    event_id: 6, 7045, 7000, 19

  # define System Integrity events in Security channel
  - name: Security
    event_id: 4657, 4616

  # define System Integrity events in System channel
  - name: System
    event_id: 1

  # define System Or Service Failures events
  - name: System
    event_id: 7022, 7023, 7024, 7026, 7031, 7032, 7034

  # define Task Scheduler Activities events
  - name: Microsoft-Windows-TaskScheduler/Operational
    event_id: 106, 141, 142, 200

  # define WindowsDefenderActivities events
  - name: Microsoft-Windows-Windows Defender/Operational
    event_id: 1008, 1006, 1116, 1010, 2003, 2001, 1009, 1118, 1119, 1007, 1117, 3002, 2004, 1005, 5008

  # define Windows Firewall events
  - name: Microsoft-Windows-Windows Firewall With Advanced Security/Firewall
    event_id: 2009, 2004, 2005, 2006, 2033

  # define Windows Update Errors in Setup channel
  - name: Microsoft-Windows-Servicing
    event_id: 1009

  # define Windows Update Errors events
  - name: Microsoft-Windows-WindowsUpdateClient/Operational
    event_id:  20, 24, 25, 31, 34, 35
```

> YMMV! Your mileage may vary.
