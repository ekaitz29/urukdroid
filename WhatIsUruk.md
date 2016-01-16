# Introduction #

UrukDroid is an Android distribution for Archos GEN8 devices. It's mix of Android 2.2.1, original Archos OS with different Linux/GNU utilities, kernel patches and all kinds of modifications.

Goal of this system is to allow users to do most of the operations they are allowed to do on normal Linux distributions. It's aimed for more advanced users, but tries to be useful on basic level of all people if they don't need special features.

## Key Features: ##
  * Easy install method for external (SDcard) and Internal storage
  * EXT4 ([much faster than ext3](http://forum.xda-developers.com/showpost.php?p=10239762&postcount=2), can store files >4GB comparing to FAT32)
  * Full read/write access to every part of the system
  * root (su + superuser.apk) out of the box
  * new services like: samba, sshd, vpnc, openvpn, dvbt, nfs4, wpa
  * full iptables support (firewall), power tuning support
  * on the fly [overclocking support](UrukService_cpugovernor.md)
  * [3G/usb tether support](http://forum.xda-developers.com/showthread.php?t=940470)
  * Possibility to remove some google/Archos apps
  * Swap memory in RAM (CompCache) or on disk - when and where you need it
  * No 300MB limit for apps (and no faulty app2sd required)
  * Many new new kernel modules (usbserial, ntfs, [3G modems](http://forum.xda-developers.com/showthread.php?t=940470), nfs4, cifs, hfs, iptables etc.)
  * DVB-T support for selected tuners
  * updated modules, firmware (like WiFi)
  * User friendly [UrukConfig](UrukConfig.md) application
  * [RescueMenu](RescueMenu.md) on early system boot level for UrukDroid healing, full [backup/restore](RM_Backup.md) feature and [AlternativeOS](RM_AlternativeOS.md) subsystem
  * You can have much more space on SD card - it that can be also faster than internal flash - but usually not (check [this thread](http://forum.xda-developers.com/showthread.php?t=934087))
  * ... and much, much more - too much to mention all here - please read [Changelog](Changelog.md)

## How Android/UrukDroid is build ##

It's quite essential to understand that all operating systems (including this one) have layers. It's more visible on system like Linux - and less on Windows - but it's a common truth for all of them.

In this case we have a **kernel layer**, witch is a slightly modified Linux kernel (2.6.29) by Android project. This is a place where all hardware drivers reside. This is also a place where Uruk Droid, comparing to other Android/Archos OS, have some important modification.

Next level is a **system layer**. These are applications compiled for the exact CPU and run on it natively. All Uruk services run on this layer - this is a place where most of Uruk Droid modification are made.

And third one is **Dalvik/UI layer**. With Android we are given the Java Runtime Environment called Dalvik - this is a place where all Android applications (from Market etc.) reside and work. This is a place where Uruk is just like every other Android - no modifications are made here.
Most of the things you can actually see are from this layer.

## What is "Uruk"? ##

Isn't it obvious? :) You can read more about [Uruk-hai](http://en.wikipedia.org/wiki/Uruk-hai) on Wikipedia, long story short - this are more advance Orcs from Tolkien fiction.