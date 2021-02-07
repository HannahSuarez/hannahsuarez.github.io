---
layout: post
title: "YAML Config Snippet for HyperV Audit Logging Event Locations"
description: "YAML Config Snippet for HyperV Audit Logging Event Locations"
comments: true
keywords: "security, yaml, hyperv, logging, log collection, blueteam"
---

The following is an Auditbeat YML configuration snippet utilizing the `file_integrity` module of potential locations of interest to monitor changes on HyperV for auditing purposes.

```
- module: file_integrity
  paths:
#Individual files to monitor
  - C:\ProgramData\Microsoft\Event Viewer\Views\ServerRoles\Virtualization.Events.xml
  - C:\ProgramData\Microsoft\Microsoft\Windows\Hyper-V\InitialStore.xml
#may not exist
  - C:\Users\Public\Documents\Blank floppy disk\Blank.vfd
#Files in C:\Windows\System32\
  - C:\Windows\System32\wnetvsc.inf
  - C:\Windows\System32\ws3cap.inf
  - C:\Windows\System32\wstorflt.inf
  - C:\Windows\System32\wstorvsc.inf
  - C:\Windows\System32\wvid.inf
  - C:\Windows\System32\wvmbus.inf
  - C:\Windows\System32\wvmbusid.inf
  - C:\Windows\System32\wvmbusvideo.inf
  - C:\Windows\System32\wvmic.inf
  - C:\Windows\System32\wvms_mp.inf
  - C:\Windows\System32\wvms_pp.inf
  #Files in C:\Windows\System32\ - AMD Hyper-V only
  - C:\Windows\System32\hvac64.exe
  #Files in C:\Windows\System32\drivers\en-US
  - C:\Windows\System32\drivers\en-US\isoparser.sys.mui
  - C:\Windows\System32\drivers\en-US\hvboot.sys.mui
  - C:\Windows\System32\drivers\en-US\vmbus.sys.mui
  - C:\Windows\System32\drivers\en-US\netvsc50.sys.mui
  - C:\Windows\System32\drivers\en-US\netvsc60.sys.mui
  - C:\Windows\System32\drivers\en-US\passthruparser.sys.mui
  - C:\Windows\System32\drivers\en-US\storflt.sys.mui
  - C:\Windows\System32\drivers\en-US\vhdparser.sys.mui
  #Files in C:\Windows\System32\DriverStore\en-US\
  - C:\Windows\System32\DriverStore\en-US\wnetvsc.inf_loc
  - C:\Windows\System32\DriverStore\en-US\ws3cap.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wstorflt.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wstorvsp.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvid.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvmbus.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvmbushid.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvmbusvideo.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvmic.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvms_mp.inf_loc
  - C:\Windows\System32\DriverStore\en-US\wvms_pp.inf_loc
  #Files in C:\Windows\System32\en-US\
  - C:\Windows\System32\en-US\nvspwmi.dll.mui
  - C:\Windows\System32\en-US\RemoteFileBrowse.dll.mui
  - C:\Windows\System32\en-US\SynthNic.dll.mui
  - C:\Windows\System32\en-US\SynthStor.dll.mui
  - C:\Windows\System32\en-US\vhdsvc.dll.mui
  - C:\Windows\System32\en-US\vmclusex.dll.mui
  - C:\Windows\System32\en-US\vmclusrex.dll.mui
  - C:\Windows\System32\en-US\vmicheartbeat.dll.mui
  - C:\Windows\System32\en-US\vmickvpexchange.dll.mui
  - C:\Windows\System32\en-US\vmicshutdown.dll.mui
  - C:\Windows\System32\en-US\vmicshutdown.dll.mui
  - C:\Windows\System32\en-US\vmictimesync.dll.mui
  - C:\Windows\System32\en-US\vmicvss.dll.mui
  - C:\Windows\System32\en-US\vmms.exe.mui
  - C:\Windows\System32\en-US\vmswitch.sys.mui
  - C:\Windows\System32\en-US\vmwp.exe.mui
  - C:\Windows\System32\en-US\vsconfig.dll.mui
  - C:\Windows\System32\en-US\WindowsVirtualization.mfl
  - C:\Windows\System32\en-US\WindowsVirtualizationUninstall.mfl
  - C:\Windows\System32\en-US\SnapInAbout.dll.mui
  - C:\Windows\System32\en-US\virtmgmt.msc
  #Files in C:\Program Files\Hyper-V
  - C:\Program Files\Hyper-V\InspectVhdDialog.exe
  - C:\Program Files\Hyper-V\InspectVhdDialog.resources.exe
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.resources.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.Management.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.Management.resources.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.RdpClientAxHost.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.RdpClientInterop.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.Settings.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.Settings.resources.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.VMBrowser.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.VMBrowser.resources.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.Wizards.dll
  - C:\Program Files\Hyper-V\Microsoft.Virtualization.Client.Wizards.resources
  - C:\Program Files\Hyper-V\SnapInAbout.dll
  - C:\Program Files\Hyper-V\virtmgmt.msc
  - C:\Program Files\Hyper-V\vmconnect.exe
  - C:\Program Files\Hyper-V\vmbus.cat
  - C:\Program Files\Hyper-V\vmstorage.cat
  - C:\Program Files\Hyper-V\vmbusvideo.cat
  - C:\Program Files\Hyper-V\vmic.cat
  - C:\Program Files\Hyper-V\netvsc.cat
  - C:\Program Files\Hyper-V\vmbushid.cat
  - C:\Program Files\Hyper-V\vmginst.cat
  #exclude_files:
  #include_files: []
  scan_at_start: true
  scan_rate_per_sec: 50 MiB
  max_file_size: 100 MiB
  hash_types: [sha1]
  recursive: false
```

> YMMV! Your mileage may vary.
