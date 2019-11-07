---
layout: post
title: "List of HKEY_* / Windows Registry keys and subkeys to audit based on MITRE ATT&CK (and more)"
description: "List of HKEY_* / Windows Registry keys and subkeys to audit based on MITRE ATT&CK, JPCert Lateral Movements 2017 research and more"
comments: true
keywords: "infosec, information security, windows, registry monitoring, mitre, mitre att&ck framework, defence, cyber security, offsec, powershell"
---

# What is the MITRE ATT&CK Framework and JPCert Detecting Lateral Movements?

I have mentioned MITRE resources previously - see my post on [OWASP zaproxy](https://hannahsuarez.github.io/2018/owasp-zap/), and [setting up zaproxy to pentest web apps](https://hannahsuarez.github.io/2018/securityscanners/) for example. This post uses one of their resources, [MITRE ATT&CK™](https://attack.mitre.org/). _"It is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations. The ATT&CK knowledge base is used as a foundation for the development of specific threat models and methodologies."_

There is also a tool called the ATT&CK Matrix for Enterprise. It is a visual and interactive tool that will allow you to drill down into tactics and techniques, eventually leading right down to the details of such attacks.

Which then leads me to writing this post. Actually, the idea of this post came about when I was reading through two other resources - JPCERT's Lateral Movements research in 2017 (["Detecting Lateral Movement through Tracking Event Logs"](https://www.jpcert.or.jp/english/pub/sr/20170612ac-ir_research_en.pdf)) being one of them. There are numerous others and I recommend reading through the research around lateral movements. Alongside the long list of Windows Event IDs being emitted were several paths to associated Windows Registry keys in relation to an attack tool.

# Why monitor Windows Registry Keys*?

The Windows Registry is a hierarchical database that stores low-level settings for the Microsoft Windows operating SYSTEM and for applications that opt to use the registry. You can read more [here](https://docs.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry).

Windows Registry is a rich source of forensic evidence for malware. Malware typically will want to touch / read the Registry. For example, a malware will write some string values to the following registry key `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` allowing the malcode to be executed on SYSTEM startup.

Malware (such as Puzlpman30 and Mozipowp31) accidentally leak information into the Registry by creating values under `HKEY_CURRENT_USER\Identities` (source page 389 Malware Analyst Cookbook). These values are binary data disguised as strings.

There are also other uses for Windows Registry, such as why reading registry contents from memory is important, but this is not covered in this post (Malware Analyst Cookbook is one such resource though for more reading)

# List of HKEY_* Windows Registry subkeys to audit

> Based on the [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/) that is current to this publication.

The following are the list of Windows Registry subkeys to audit or indicators of paths to subkeys. **Please do not use this as the exhaustive list.**

The context (ie what attack it pertains to, what group, etc) are not included in this post though.

```
HKEY_CURRENT_USER\SOFTWARE\Classes\
HKEY_CURRENT_USER\SOFTWARE\Bitcoin\Bitcoin-Qt.
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Terminal Server Client\Default
HKEY_USERS\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\Micromedia
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WMI\Security
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Pniumj
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\ShellCompatibility\Applications\laxhost.dll
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\PrintConfigs
HKEY_CURRENT_USER\SOFTWARE\Microsoft\WABE\DataPath
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\SYSTEM Enable LUA=”0”
HKEY_CURRENT_USER\SOFTWARE\DC3_FEXEC
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Windows
HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Run\
HKEY_CURRENT_USER\SOFTWARE\Classes\CLSID\
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ControlPanel\NameSpace
HKEY_CLASSES_ROOT\CLSID{GUID}
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\
HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\PreviousVersions\DisableLocalPage
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\ShellCompatibility\Applications\laxhost.dll
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\BootExecute
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\Micromedia
HKEY_CURRENT_USER\SOFTWARE\Classes\mscfile\shell\open\command
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ControlPanel\NameSpace
HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\PreviousVersions\DisableLocalPage
```

> Additions based on [JPCert Lateral Movements analysis](https://jpcertcc.github.io/ToolAnalysisResultSheet/).

For the list below, it is worthwhile to look at the full online resource. In some cases, they have added the Windows Registry changes at the time of malware execution. They also differentiated if the changes were at the source or destination host.

```
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2\CPC\Volume\{[GUID]}
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\DeviceClasses\{53f5630d-b6bf-11d0-94f2-00a0c91efb8b}\##?#STORAGE#VolumeSnapshot#HarddiskVolumeSnapshot[Number]#{53f5630d-b6bf-11d0-94f2-00a0c91efb8b}\DeviceInstance
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Enum\STORAGE\VolumeSnapshot
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\VSS
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\{533c5b84-ec70-11d2-9505-00c04f79deaf}\0000
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Terminal Server Client\Default\MRU0
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Terminal Server Client\Servers\[Target Host]\UsernameHint
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Search\JumplistData\Microsoft.Windows.RemoteDesktop
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count\Zvpebfbsg.Jvaqbjf.ErzbgrQrfxgbc
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Wpad\WpadLastNetwork
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tree\[Task Name]
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tasks\{[GUID]}
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tree\[Task Name]
HKEY_USERS\[User SID]\SOFTWARE\Sysinternals\Sdelete
HKEY_USERS\[User SID]\SOFTWARE\Sysinternals\SDelete\EulaAccepted
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{[GUID]}\Count\[ROT13 of Path to Tool]\[ROT13 of Tool Executable File Name]
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\{[GUID]}.sdb\DisplayName
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\services\SharedAccess\Parameters\FirewallPolicy\FirewallRules\TCP Query User{[GUID]}[Path to Tool]
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\VSS\Diag\BITS Writer
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count\{1NP14R77-02R7-4R5Q-O744-2RO1NR5198O7}\JvaqbjfCbjreFuryy\i1.0\cbjrefuryy.rkr
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Reliability Analysis\RAC\WmiLastTime
HKEY_USERS\[User SID]\SOFTWARE\Sysinternals\PsExec\EulaAccepted
HKEY_USERS\[User SID]\SOFTWARE\Microsoft\Windows Script Host
```

## Other notes

`HKLM\SOFTWARE` and `HKEY_USERS\.DEFAULT\SOFTWARE` is where most installed applications reside.

Additions to `HKEY_USERS\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` is typically made for persistence.

To obtain a list of subkeys, use either Windows Registry or [one can work with Registry Keys via PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/samples/working-with-registry-keys?view=powershell-6).

# Monitoring for Registry Changes via Windows Event Log

Since this post is largely about the list, I won't cover the steps on mitigating.

One of the ways to mitigate is through monitoring for Windows Registry Changes. Enable auditing on the Windows Registry root keys and centralize logs from any Windows Event Log events that will fire off depending on the event. Below are associated events:

| Event ID      | Title           |
| ------------- |:-------------:|
| 4656      | A handle to an object was requested |
| 4657      | A registry value was modified      |
| 4658 | The handle to an object was closed      |
| 4660 | An object was deleted      |
| 4663 | An attempt was made to access an object      |

Another way to mitigate is through hardening. CSO Online, in this [May 2019 post](https://www.csoonline.com/article/3393268/how-to-outwit-attackers-using-two-windows-registry-settings.html) has some pointers alongside other resources online. Specific to the MITRE ATT&CK framework, they also include mitigations (see [here](https://attack.mitre.org/mitigations/M1026/) for instance).

# Other resources

[Windows Registry Auditing Cheatsheet by Malware Archaelogy](https://static1.squarespace.com/static/552092d5e4b0661088167e5c/t/5d497aefe58b7e00011f6947/1565096688890/Windows+Registry+Auditing+Cheat+Sheet+ver+Aug+2019.pdf)

> Your mileage will vary.
