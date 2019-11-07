---
layout: post
title: "Chromebook on dev mode; list of --crossystem parameters"
description: "Parameters for Chromebook (Samsung 550 released in 2012) on Google Lumpy 2.111.0"
comments: true
keywords: "chromeos, chromebook"
---

## First look around Chromebook

![Chromebook (Samsung 550 released in 2012)](/assets/images/chromebook-600px.png)

I have been putting off putting the Chromebook which is a Samsung 550 version released in 2012. I've been planning to get it on dev mode and tinkering around the internals and putting another OS or some other system for a few years. For some reason, I decided to make a start of it this year. It's been sitting on the shelf, unused.  I've been thinking of one or two potential OS, or I may just keep it as is and poke around the internals.  I've found the limitations both frustrating and interesting to work around, being new to working around these systems headless.

The first item that was done was to open the Chromebook.  I've found the fan a bit too loud and wanted to check if there was anything that should be cleaned out with the fan.

I took out the battery because originally, I thought that the physical dev mode switch is residing beneath the battery.  This is because the model that I have must have the physical dev mode switch turned on.  I really could not find it at all based on the 2012 model photos provided on the [Developer Information for Chrome OS Devices page](https://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices) and I did read that it resided underneath the battery.  So, off I went looking.  Until I came across a very helpful post of the image [here](https://greenido.files.wordpress.com/2013/08/photo3.jpg) which showed where the dev mode switch was located.

As other posters have described, after the dev mode reboot (`Esc` + `refresh` + `power` button) you see some sort of warning screen. This is already described in a number of posts (please see the links below).  One item I found out is that you can press `Ctrl` + `I` and it will show a text description of the 'not-nice' warning screen.

Since there is no git, wget, etc it was not straight forward following through with some of the details already published about putting Crouton on Chromebook, etc.  To git clone, I needed to generate ssh keys, then install git and find a way to transfer keys to my profile. I looked at maybe using sftp/scp through some packages. You can also go through and access/exchange files downloaded from the browser version or files created from dev mode. Whichever mode, I think this is a nice type of setup but currently it's not really at a stage that's currently much use to me other than to poke around.

## --crossystem Parameters

One item you will come across first is `--crossystem`.
So, I've decided to list the `--crossystem` parameters available to me for Samsung Chromebook on Google Lumpy 2.111.0.

```
sage:
  crossystem [--all]
    Prints all parameters with descriptions and current values.
    If --all is specified, prints even normally hidden fields.
  crossystem [param1 [param2 [...]]]
    Prints the current value(s) of the parameter(s).
  crossystem [param1=value1] [param2=value2 [...]]]
    Sets the parameter(s) to the specified value(s).
  crossystem [param1?value1] [param2?value2 [...]]]
    Checks if the parameter(s) all contain the specified value(s).
Stops at the first error.
Valid parameters:
  arch                    Platform architecture
  backup_nvram_request    Backup the nvram somewhere at the next boot. Cleared on success.
  battery_cutoff_request  Cut off battery and shutdown on next boot.
  block_devmode           Block all use of developer mode
  clear_tpm_owner_request  Clear TPM owner on next boot
  clear_tpm_owner_done    Clear TPM owner done
  cros_debug              OS should allow debug features
  dbg_reset               Debug reset mode request (writable)
  debug_build             OS image built for debug features
  dev_boot_usb            Enable developer mode boot from USB/SD (writable)
  dev_boot_legacy         Enable developer mode boot Legacy OSes (writable)
  dev_boot_signed_only    Enable developer mode boot only from official kernels (writable)
  dev_default_boot        default boot from legacy or usb (writable)
  devsw_boot              Developer switch position at boot
  devsw_cur               Developer switch current position
  disable_dev_request     Disable virtual dev-mode on next boot
  ecfw_act                Active EC firmware
  fmap_base               Main firmware flashmap physical address
  fwb_tries               Try firmware B count (writable)
  fw_vboot2               1 if firmware was selected by vboot2 or 0 otherwise
  fwid                    Active firmware ID
  fwupdate_tries          Times to try OS firmware update (writable, inside kern_nv)
  fw_tried                Firmware tried this boot (vboot2)
  fw_try_count            Number of times to try fw_try_next (writable)
  fw_try_next             Firmware to try next (vboot2,writable)
  fw_result               Firmware result this boot (vboot2,writable)
  fw_prev_tried           Firmware tried on previous boot (vboot2)
  fw_prev_result          Firmware result of previous boot (vboot2)
  hwid                    Hardware ID
  inside_vm               Running in a VM?
  kern_nv                 Non-volatile field for kernel use
  kernel_max_rollforward  Max kernel version to store into TPM
  kernkey_vfy             Type of verification done on kernel key block
  loc_idx                 Localization index for firmware screens (writable)
  mainfw_act              Active main firmware
  mainfw_type             Active main firmware type
  nvram_cleared           Have NV settings been lost?  Write 0 to clear
  oprom_needed            Should we load the VGA Option ROM at boot?
  phase_enforcement       Board should have full security settings applied
  recovery_reason         Recovery mode reason for current boot
  recovery_request        Recovery mode request (writable)
  recovery_subcode        Recovery reason subcode (writable)
  recoverysw_boot         Recovery switch position at boot
  recoverysw_cur          Recovery switch current position
  recoverysw_ec_boot      Recovery switch position at EC boot
  ro_fwid                 Read-only firmware ID
  tpm_attack              TPM was interrupted since this flag was cleared
  tpm_fwver               Firmware version stored in TPM
  tpm_kernver             Kernel version stored in TPM
  tpm_rebooted            TPM requesting repeated reboot (vboot2)
  try_ro_sync             try read only software sync
  tried_fwb               Tried firmware B before A this boot
  vdat_flags              Flags from VbSharedData
  vdat_lfdebug            LoadFirmware() debug data (not in print-all)
  vdat_lkdebug            LoadKernel() debug data (not in print-all)
  vdat_timers             Timer values from VbSharedData
  wipeout_request         Firmware requested factory reset (wipeout)
  wpsw_boot               Firmware write protect hardware switch position at boot
  wpsw_cur                Firmware write protect hardware switch current position

```

## What's in the /bin/?

```
arping
attr
basename
bash
brltty
brltty-atb
brltty-config
brltty-ctb
brltty-ktb
brltty-trtxt
brltty-ttb
brltty-tune
bunzip2
bzcat
bzip2
cat
chacl
chgrp
chmod
chown
chroot
cp
cut
dash
date
dd
df
dir
dirname
dmesg
dnsdomainname
du
echo
egrep
env
eutp
expr
false
fgrep
findmnt
getfacl
getfattr
grep
groups
gunzip
gzip
head
hostname
ifconfig
ip
keyctl
kill
kmod
ln
login
ls
lsblk
lsmod
mkdir
mkfifo
mknod
mktemp
modinfo
more
mount
mountpoint
mv
netstat
passwd
ping
ping6
ps
pwd
rbash
readlink
rm
rmdir
route
sed
seq
setfacl
setfattr
sh
sleep
sort
stty
su
sync
tail
tar
touch
tr
true
tty
udevadm
umount
uname
uncompress
vdir
vstp
wc
wdctl
yes
zcat
```

## What next after ChromeOS?

Not being a big user of ChromeOS products, there was no point in me continuing to run ChromeOS.  I am looking at a couple of options to run instead.

**What about Crouton?**

There is [Crouton](https://github.com/dnschneid/crouton) which I did manage to download and unzip from dev mode. I initially converted to a `tar` so that I can use `/bin/gzip` to unzip it.  Followed the instructions in trying to run it but no luck.  It may be due to location since it was downloaded to `home/user/CHROME_ID/Downloads` as I was using the browser version. Anyway, I only wanted to see how it looks but I can imagine that I'd want to go ahead and not use ChromeOS anymore and something else.

## Other posts that you may find useful when reading about running Chromebook in dev mode

[OpenBSD on the Chromebook Pixel](https://jcs.org/notaweblog/2016/08/26/openbsd_chromebook)

[CNet - how to enable developer mode](https://www.cnet.com/how-to/how-to-enable-developer-mode-on-a-chromebook/)

[Developer Mode - Chrome OS wiki](https://sites.google.com/site/chromeoswikisite/home/what-s-new-in-dev-and-beta/developer-mode)

[Crouton](https://github.com/dnschneid/crouton)

