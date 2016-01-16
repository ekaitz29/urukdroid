# Changelog: #

**UrukDroid 1.6.2** (31.01.2012) (this is crypt update)
  * `[`NEW`]` Added cyptsetup util, library and modules - to enable disk encryption. More [here](http://forum.xda-developers.com/showpost.php?p=22025706&postcount=2415) and [here](http://forum.xda-developers.com/showpost.php?p=21613545&postcount=2411)

**UrukDroid 1.6.1** (13.01.2012) (this is just fix release)
  * `[`FIX`]` Fixed samba issue (running samba service could cause reboot loop)
  * `[`FIX`]` Fixed iptables REDIRECT filter (for transparent proxy)
  * `[`CHANGE`]` Added some missing modules joydev, ec168
  * `[`CHANGE`]` Restored default settings for mediascanner (on) and wpa (off)
  * `[`NEW`]` Added /etc/rc.local file for user "on boot" settings
  * `[`CHANGE`]` Failed updates will now be deleted (to prevent update on every reboot)
  * `[`CHANGE`]` Updated xtables (iptables) libraries/binaries
  * `[`NEW`]` Added AlternativeOS Ubuntu script

**UrukDroid 1.6** (02.01.2012) "DOV FUS LOS Wahl ko Daar Sivaas!"
  * `[`CHANGE`]` Incorporated changes from Archos firmware 2.4.19, 2.4.65, 2.4.80 and 2.4.81
  * `[`CHANGE`]` Updated superuser apk and binaries
  * `[`FIX`]` Fixed some library linking
  * `[`NEW`]` Changed top bar button size to 32px permanently
  * `[`NEW`]` **New overclock module** from [milestone-overclock](http://code.google.com/p/milestone-overclock/) to change CPU voltage and max frequencies on the fly
  * `[`CHANGE`]` Added [overclock support to CPUGovernor](UrukService_cpugovernor.md) service
  * `[`FIX`]` Restored proper busybox binary
  * `[`NEW`]` New patches on kernel from December update from Archos git
  * `[`NEW`]` **Full iptables support** (with NAT, conntrack etc) - so everything is now possible (redirect, proxies etc)
  * `[`NEW`]` **Full kernel timing for power consumption monitoring**
  * `[`NEW`]` **Recompiled WiFi and HDMI drivers**
  * `[`NEW`]` Added python 2.7, [iotop](http://guichaz.free.fr/iotop/) (for watching i/o operations), [PowerTOP](http://www.linuxpowertop.org/) (for power consumption monitoring - but it's not as useful as on x86)
  * `[`NEW`]` Added ntfs-3g support - **full read/write support for NTFS** file systems (need to be used manually, vold does not use it)
  * `[`CHANGE`]` Added UrukDroid Rescue Menu - [Repair submenu](RM_Repair.md) with disabling overclocking (for those who made their device unbootable with overclocking) and Dalvik cache cleaner
  * `[`NEW`]` New feature in cpugovernor script (genconf, current)
  * `[`CHANGE`]` **New features in update subsystem**
    * scripts now tries to keep /data/.tmp directory cleaner,
    * for those with disk shortage /data/.tmp can be now symlink to directory on sdcard
    * updater now checks if you have enough free space in /data/.tmp before it begin installation
    * update process now can be during bootup (better one) if you have enough free space on rootfs, or on running system (not so nice - this is default behavior until UD 1.6 release)
  * `[`CHANGE`]` restoring backup in Rescue Menu now erases partition before restore (until now it was just overwriting)
  * `[`FIX`]` added (again ;)) xbox pad kernel support (was missed out in new kernel compilation)
  * `[`FIX`]` fixes scp/sftp-server (on some configuration refused to start child processes)

**UrukDroid 1.5.1** (20.08.2011) (this is just fix release)
  * `[`CHANGE`]` Swap now can use both file and partition at the same time, added simple stats, added default Archos swap partition
  * `[`CHANGE`]` Disabled Archos swap manager (forgot in 1.5)
  * `[`FIX`]` Fixed WPA service (did not switch properly)
  * `[`FIX`]` NFS4 service don't report failed umount of CIFS/SMB share
  * `[`NEW`]` Fix for remounting to RW mode rootfs (sometimes it happens it starts in RO)
  * `[`CHANGE`]` Alternative OS boot now produces more messages (for easier debug), new Debian boot script (as an example)
  * `[`NEW`]` Added unrar binary
  * `[`CHANGE`]` When there exists mmcblk0p3 swap partition - it's used by default

**UrukDroid 1.5** (15.08.2011) [Manamana!](http://www.youtube.com/watch?v=8N_tupPBtWQ)
  * `[`CHANGE`]` Since UrukDroid 1.1 (both beta1/2/3 and release candidate 1/2/3) had stability and compatibility issues - that I was unable to trace down (too many changes on changes etc.) - I've decided to implement all stuff from beginning on fresh OS. Since all "reverse engineering" stuff was already made and I already have required knowledge - It should be the fastest method. So entire system is cleaned up, updated to latest binaries - and so far looks good :). That's why I've bumped version to 1.5 - just to make it a bit more visible it's not a straight continuation of 1.0/1.1.
  * `[`FIX`]` No more "soft reboots" (system reloaded it's graphics UI part)
  * `[`FIX`]` No more turning off WiFi issue (but it happens that WiFi can't pop in after full reboot - another reboot is required)
  * `[`FIX`]` CIFS startup on boot ([Issue 57](http://code.google.com/p/urukdroid/issues/detail?id=57))
  * `[`CHANGE`]` Update process should be now more chatty and report more errors
  * `[`CHANGE`]` Reverted back WPA service (which enable UrukDroid WPA supplicant with AdHoc support) - since some people reported problems with adding new networks with Uruk version of WPA supplicant.
  * `[`CHANGE`]` Merged changes from Archos 2.3.28 OS

**UrukDroid 1.1** _Won't be released (since I was unable to make it stable enough)_
  * `[`CHANGE`]` Removed "wpa" service - since wpa\_supplicant now can work with standard wifi manager and adhoc networks
  * `[`NEW`]` New wpa\_supplicant - hopefully with all features and without most of known problems (sometimes it still refuses to start)
  * `[`CHANGE`]` Updated modules and kernel
  * `[`FIX`]` Fix camera support for A43
  * `[`CHANGE`]` Merged changes from Archos 2.3.26 OS
  * `[`CHANGE`]` Redesigned services to output more reliable status
  * `[`FIX`]` Mediascanner fixes (did not rescan data sometimes)
  * `[`CHANGE`]` Changed file browser app to "File Expert" (with root access feature)
  * `[`NEW`]` Introduced in 1.0 "Rescue Menu" now fully functional (RM)
  * `[`NEW`]` RM now have [Alternative OS](AlternativeOS.md) boot feature
  * `[`NEW`]` RM now have "bare metal" backup/restore functionality
  * `[`NEW`]` Update process will now communicate with user with help of UrukConfig
  * `[`NEW`]` Enabled cgroups
  * `[`FIX`]` "Moved" boot image on A101
  * `[`FIX`]` 3Gmodem\_init.sh fixes
  * `[`NEW`]` You can dissable boot from SDCard by naming any of it's partition "noboot" ('root@urukdroid:/root# e2label /dev/block/mmcblk2p1 noboot')
  * `[`NEW`]` patch (by Sibere) increasing USB current in Host mode

**UrukDroid 1.0** (30.04.2011) "[For he is the Kwisatz﻿ Haderach](http://www.youtube.com/watch?v=DVx6bXoCnC0)"
  * `[`FIX`]` sshfs missing files fix
  * `[`FIX`]` EasyInstall: changed datafs max size from 2GB to 1.95GB (for market to work), fixed partition sizes for A101 16GB when doing internal install with resize, fixed installation for A70H devices
  * `[`NEW`]` small script to copy UrukDroid files from SDCard (external) to Internall (copy\_from\_sd\_to\_internal.sh)
  * `[`CHANGE`]` Changed behaviour of dvb service (device configuration)
  * `[`FIX`]` Added some missing modules for DVB support
  * `[`CHANGE`]` New kernel modules for more dvb devices (but it requires manual loading and testing)
  * `[`NEW`]` rsync tool
  * `[`CHANGE`]` swap service now can work on swap partition (or like before on swap file), also after mounting sdcard ext4 partition
  * `[`NEW`]` Ad-Hoc WiFi connection support by [WPA service](UrukService_wpa.md) (networks are visible with "`*`" on beginning of it's SSID)
  * `[`CHANGE`]` Some new progress indicators during install/upgrade
  * `[`NEW`]` Simple Animation during late phase of bootup
  * `[`NEW`]` New services: cifs (to load cifs modules), wpa (ad-hoc wifi)
  * `[`NEW`]` Added cgroups kernel setting
  * `[`NEW`]` Moved some modules dependencies (cifs,ntfs,dvb) to /etc/modprobe.d
  * `[`NEW`]` EasyInstall has now simple "Repair" option to reformat rootfs, and install from scratch (this operation preserves all application data from datafs)
  * `[`NEW`]` Installation package brings [WiFi manager](http://www.appbrain.com/app/wifi-manager/org.kman.WifiManager), [File Manager](http://www.appbrain.com/app/file-manager/com.rhmsoft.fm) and [Terminal](http://www.appbrain.com/app/android-terminal-emulator/jackpal.androidterm) application
  * `[`CHANGE`]` New [UrukConfig](UrukConfig.md) application


**UrukDroid 0.7** (28.02.2011) [you're? damn right it's a gift!!](http://www.dailymotion.pl/video/x1fvlh_mtv-lord-of-the-rings-parody_fun)
  * `[`NEW`]` NFSv4 client support
  * `[`NEW`]` FS-Cache (cachefilesd) support for NFS (local disk cache for NFS files)
  * `[`NEW`]` sshfs support
  * `[`FIX`]` OpenVPN fix - thanks to **nenadr**
  * `[`FIX`]` PPtP fix - thanks to **nenadr**
  * `[`NEW`]` vpnc tool for using Cisco VPN connections
  * `[`NEW`]` vpnc UrukDroid service
  * `[`CHANGE`]` Updated to libc6 2.11 (and all binaries recompiled/changed because of it - big change)
  * `[`NEW`]` new gnu tools: nmap
  * `[`NEW`]` EasyInstall now allows installing UrukDroid on internal (mmcblk1) storage in A70 and A101
  * `[`NEW`]` Integrated 3G USB modem and RNDIS USB tethering  [service by nenadr](http://forum.xda-developers.com/showthread.php?t=940470)
  * `[`CHANGE`]` New iobench.sh (with new bonnie++ test)
  * `[`CHANGE`]` Changed device fingerprint to work better with google market (enable download some missing apps)
  * `[`CHANGE`]` Merged Archos 2.1.8 firmware changes
  * `[`CHANGE`]` Changed DVB subsystem support and kernel/modules dependencies to work with new v4l2 modules (it will brake compatibility with most other kernels probably)
  * `[`FIX`]` Changes it UrukUpdate mechanism to work every time when file is moved to "/data/UrukUpdate"
  * `[`NEW`]` Added required modules and iptables service configuration for [DroidWall](http://www.appbrain.com/app/droidwall-android-firewall/com.googlecode.droidwall.free) (firewall) application
  * `[`NEW`]` sudo subsystem for launching properly some root tasks


**UrukDroid 0.6** (11.02.2011) Eye of the Uruk... in new logo :)
  * `[`CHANGE`]` Merged changes from Archos firmware 2.1.2/2.1.3/2.1.4
  * `[`CHANGE`]` DVB support with [LiveTV.apk](http://code.google.com/p/archos-gen8-dvb/downloads/list?q=label:Featured") from [chulri](http://forum.xda-developers.com/member.php?u=3282332) (for selected cards, there are more modules then listed in /etc/uruk.conf/dvb - but it requires to do some experiment and report it back)
  * `[`CHANGE`]` Changed Uruk service to work better with new UrukConfig
  * `[`NEW`]` New services: openvpn, mediascanner
  * `[`NEW`]` IO Benchmark tool: iobench.sh
  * `[`NEW`]` Possibility to turn off mediascanner and use it on demand only
  * `[`FIX`]` Fixed mount\_sdcard.sh script to work with 2.1.2 ext3 partitions
  * `[`NEW`]` Updated boot sequence with progress during upgrade/install
  * `[`NEW`]` You can hide soft buttons (Archos buttons) with UrukConfig
  * `[`NEW`]` Easy Install method - no need to know anything about Linux - just plug and wait...
  * `[`NEW`]` Kernel modules for 3g dongle


**UrukDroid 0.5** (27.01.2011) Tom Bombadil... in red
  * `[`NEW`]` [CompCache](http://code.google.com/p/compcache/) (aka ramzswap) support
  * `[`NEW`]` New CPU governor - interactive. Ported from XDA CyanogenMOD
  * `[`NEW`]` DVB: applied patches by chulri, Siano SMS1XXX USB support
  * `[`NEW`]` DVB: modules from outside kernel tree
  * `[`NEW`]` Some more GNU tools: gzip utils, zip utils, unzip utils, nc (NetCut for DVB streaming)
  * `[`CHANGE`]` New services model - so they can be easily run/configured with help of UI
  * `[`NEW`]` New kernel modules: usbnet, lzo
  * `[`NEW`]` Mediascanner modification - it should has much, much smaller impact on system performance
  * `[`NEW`]` sqlite3 (3.5.9) installed, for easy database file manipulation
  * `[`NEW`]` after restart of UrukDroid it will boot once again to Uruk without need of pressing any buttons, to boot on stock OS please use boot menu
  * `[`FIX`]` mount\_sdcard.sh fixed so it will mount first ext4 partition on sdcard if exist, and will not interfere with Vold if its vfat
  * `[`CHANGE`]` New update/upgrade/flash model - everything done on UrukDroid - no boot menu required
  * `[`NEW`]` New application to configure UrukDroid - UrukConfig.apk. Installed with this release. Can be uninstalled in default way.
  * `[`FIX`]` Fixed corrupted logo in A101
  * `[`NEW`]` Unified kernel for UrukDroid on SDCard and internal storage (A70S/A101)
  * `[`CHANGE`]` Services ENABLED with this release: CpuGovernor, CompCache


**UrukDroid 0.4.2** (21.01.2011)
  * Just extracted as a separate update file GoogleMarket


**UrukDroid 0.4.1** (15.01.2011) Myyy preciousssss...
  * Some more tools like: bc, proc utils, vim, tcpdump, bzip2, tar etc.
  * Android apps (Market, Maps, Talk, Calendar, Contact, Feedback, Locator, Updater) by default
  * Samba (3.2.5) support for sharing /mnt/storage (internal and sdcard storage) from Archos
  * Dropbear SSH server
  * Backported modprobe, depmod etc. tools for modules management
  * WiFI driver recompiled, WiFi HW firmware update (from 6.1.0.0.335 to 6.1.5.44.7)
  * Initial DVB-T support (Afatech AF9005, Afatech AF9015, DiBcom DiB0700, Terratec CinergyT2/qanu)
  * Bootlogo with progress steps
  * Cleanups of initramfs and rootfs
  * EXT4 drivers backported from 2.6.30 - some mount changes (to prevent config files corruption)
  * Initial A70H support
  * SDCard/HD layout changed
  * Autoupgrade service and installation helper
  * ADB fixes
  * Removed two apps. TelephonyProvider.apk, Phone.apk
  * <font>Since 0.4 all services are DISABLED by default, to enable it edit proper config file in /etc/uruk.conf/</font>

**UrukDroid 0.3** (9.01.2011) Rise my Uruk... not yet Hai :P
  * iptables, ntfs support
  * some more USB modules: usbserial, pl2303
  * fixed bluetooth problem (not working in Uruk 0.2)
  * automounting improvements (much more bulletproof)
  * new configuration files (/etc/uruk.conf/) to enable/disable features
  * new Uruk services (/etc/uruk.d/)
  * some more GNU utils openssh-client, coreutils
  * USB charging enabled (NOT tested!!!) - It would required much more power then standard USB in PC can give, use USB wall/car charges or double/triple USB cables

**UrukDroid 0.2** (5.01.2011) Go GNU release ;)
  * "smart" automounting script (that will mount ext4/vfat third partition from sdcard in RIGHT place, AFTER internal storage is mount)
  * plenty of useful GNU tools: whole e2fstools (mkfs, fsck for ext2/ext3/ext4), parted (for partition resize, format etc.), vfat tools, new toolbox, mtr, top, strace, bash - and much more (look in /usr/local/bin and /usr/local/sbin)
  * swap memory ON by default (50MIB file /swap01.file)
  * required compiled libraries libparted, libncurses, libe2fs... etc. (look in /usr/local/lib)
  * new text editor in text mode: nano (my favourite)
  * some init.rc cleanups
  * kernel changes (mostly toward console output)
  * fixed small (but problematic) misconfiguration in Archos (yep original one) Android in linking /etc/mtab

**UrukDroid 0.1** (30.12.2010) Initial "release"
  * recompiled kernel with ext4, nfs4, fb console
  * added su and superuser.apk
  * bootup changes (to make it work)