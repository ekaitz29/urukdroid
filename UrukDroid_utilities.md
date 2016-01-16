

# Introduction #

There are plenty of utilities installed with UrukDroid. Most of them are OS level binary tools and scripts, so they can be used over SSH and/or terminal. They can be also used by some rare Android programs. Here you can find list of most common GNU tools available on Uruk and more detailed information about native Uruk scripts and tools.


# Installed GNU tools #

**List of tools installed with UrukDroid:** awk, azap, bash, bc, bz(cat,cmp,diff,egrep,exe,fgrep,grep,less,more), bzip2, bzip2recover, cifsiostat, cpio, dash, date, dd, dmesg, dnsdomainname, egrep, fgrep, file, find, ionice, iostat, ldd, less, lessecho, lessfile, lesskey, lesspipe, lsmod, lsof, lsusb, mawk, md5sum, md5sum.textutils, mknod, mktemp, mount, mountpoint, mpstat, mt, mt-gnu, nano, nc, ncftp, netstat, nfsiostat, nisdomainname, nmap, nohup, pgrep, pidstat, ping, pkill, rbash, readlink, renice, rnano, rpcinfo, rsync, run-parts, scp, screen, sed, sftp, sh, sh.distrib, smbpasswd, sort, sqlite3, ssh, ssh-add, ssh-agent, ssh-argv0, ssh-copy-id, ssh-keygen, ssh-keyscan, ssh-vulnkey, sshfs, stat, strace, stty, sudo, sync, tail, tailf, tar, tee, telnet, telnet.netkit, tempfile, test, top, traceroute, tzap, umount, uname, uncompress, unzip, uptime, vdir, vi, vim, vim.tiny, vmstat, w, w\_scan, watch, whereis, which, who, ypdomainname, z(cat,cmp,diff,egrep,fgrep,force,grep), zip, zipinfo, zless, zmore, znew,

**Root specific:** badblocks, bonnie, bonnie++, cachefilesd, cfdisk, chroot, depmod, dosfsck, dropbear, dropbearkey, dumpe2fs, e2fsck, e2image, e2label, e2undo, fdisk, fsck, fsck.ext2, fsck.ext3, fsck.ext4, fsck.msdos, fsck.nfs, fsck.vfat, ifconfig, incrond, insmod, iptables, iptables-multi, iptables-restore, iptables-save, kd\_flasher, logsave, losetup, lsmod, mkdosfs, mke2fs, mkfs, mkfs.ext2, mkfs.ext3, mkfs.ext4, mkfs.msdos, mkfs.vfat, mkswap, modinfo, modprobe, mount, mount.nfs, mount.nfs4, mountpoint, parted, partprobe, portmap, reboot\_into, resize2fs, rmmod, route, rpc.idmapd, rzscontrol, sftp-server, showmount, smbd, start-stop-daemon, sudoedit, swapoff, swapon, sysctl, thttpd, tune2fs, update-usbids, usb\_modeswitch, visudo, vpnc, vpnc-connect, vpnc-disconnect

# UrukDroid specific tools #

## iobench.sh ##

This script was created for sdcard speed test purpose. You can find more information and results in this [XDA thread](http://forum.xda-developers.com/showthread.php?t=934087). Basicly this is script with some io tests (based on bonnie++) - it should check both raw r/w performance and small files operations speed. It should be more precise that "dd" speed test (witch is of course also good ;) - but can be not fully true if some sd cards prefer some specific block sizes)

Since UrukDroid 0.6 this script is installed by default. But with Uruk 0.7 it's output has changed so it's not compatible (comparable) with previous results.

### How to run test? ###
To run the test, connect archos to power supply and run from shell
```
su
iobench.sh
```

Test run looks like this:
```
[root@localhost tst]# iobench.sh 
Turning on max CPU frequency: 1000000 hz
Performing disk (/data) IO test. Test make take about 1h on slower systems - please connect device to power supply!
Done: 0%...12%...20%...28%...36%...44%...52%...60%...68%...76%...84%...92%...100%
------------------- Please report this data ---------------------
Your throughput score is: 4847.8
Your metadata score is: 2328.3
localhost,128M,2242,78,6313,6,5014,5,2984,98,17486,9,20.3,0,16,93,1,+++++,+++,73,0,94,1,+++++,+++,68,0
SDCard by LEXAR (0x1:) manufacture date 10/2010, oemid 0x4245
-----------------------------------------------------------------
Restoring previous cpu setting....
```

### What does tests do? ###
Script creates files with different method (per char, per block, in sequential or random order) - this is throughput part.
Second tests check how fast we can create/access/remove files. More you can read about tool called [bonnie++](http://www.coker.com.au/bonnie++/readme.html) on Internet.

So called score is just for you - it may be not precise, full exact data are in line below score.

This are charts created with help of people from XDA - they compare performance of some selected SDCards.

Pre 0.7 results
![http://adrian.siemieniak.net/UrukDroid/SDCard-results.png](http://adrian.siemieniak.net/UrukDroid/SDCard-results.png)

0.7+ results
![http://adrian.siemieniak.net/UrukDroid/SDCard-resultsV2.png](http://adrian.siemieniak.net/UrukDroid/SDCard-resultsV2.png)


## copy\_from\_sd\_to\_internal.sh ##
## copy\_from\_internal\_to\_sd.sh ##

This is simple script that I use to copy (kind of backup for me) my UrukDroid installation from SDcard to Internal storage (and vice-versa). This way whenever I would broke something on me development platform (SDcard) I could easily boot to internal (just remove SDcard and reboot) and fix problem.

It's recommended to run this script on "[screen](http://en.wikipedia.org/wiki/GNU_Screen)" - since it's quite CPU consuming operation and sometimes it brakes WiFi connection (of course if you run it over ssh).

This script can be also used to migrate from external Uruk Droid installation to internal one.

Below is an example of use:
```
root@urukdroid:/root# copy_from_sd_to_internal.sh
Mounting rootfs partitions...
Erasing old filesystem...
Copying rootfs...
Mounting datafs partitions...
Erasing old filesystem...
Copying datafs...
You can poweroff device, remove SDcard and boot to internal...
```

## mount\_sdcard.sh ##

This script is used to mount SDCard storage partition when it is formatted as EXT4 filesystem (vold will fail to do that).