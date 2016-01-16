# Introduction #

To move from one version of UrukDroid to another there are some updates and upgrades files prepared.

The main difference between update and upgrade is that upgrade overwrites almost entire rootfs (so its a bit simplified install) and updates only files that has really changed. In both cases be prepared that some configuration files (so entire /etc/) may be altered.

**IMPORTANT!**
Since UrukDroid 1.5 there is full [backup support](RM_Backup.md), so before doing any update/upgrade please do one - this way you will be always able to go back.

To update from UrukDroid 1.5+ (so 1.5.1 also) you should download special update package (UrukDroid-1.6-update.tbz2) from [Download](Download.md) section. You need to place this file in **"/data/UrukUpdate"** directory.


## Free space requirements for upgrade ##

UD version <1.6:
> Upgrade requires you to have at least as much as upgrade file free space on **rootfs** (/) and twice as much free space on **datafs** (/data). Without this it will fail!

UD versions 1.6+:
> Upgrade requires free space in size of about 110% of update package on datafs (/data), storage (/mnt/storage) and rootfs (/).

## Free space requirements for updates ##

UD version <1.6:
> Update will require twice free space on datafs (/data) as the size of update package.

UD version 1.6+:
> It will require free space on datafs (to put update package) in size of update package, same amount free space on storage (/mnt/storage) and:
  * if there is enough free space on rootfs (/) to put update file, update will be done during reboot - this is more clean way of doing updates
  * if there is not enough free space on rootfs (/) update will be done on living system - you will probably notice some "force close" errors etc. and device will reboot itself automatically

# How to apply updates/upgrades? #

## First method: ##
Put package file on your internal storage by any means - this is /mnt/storage (also visible as /sdcard/). Then use file manager (like [FileExpert](http://www.appbrain.com/app/file-expert/xcxin.filexpert) or RooteExplorer) to move file to proper directory or do as follow on terminal (or over [ssh](UrukService_sshd.md)).
Code:
```
su
cd /sdcard/
mv UrukDroid-1.5-upgrade.tbz2 /data/UrukUpdate/
```

## Second method: ##
Use [UrukConfig](UrukConfig.md) to enable [SSHD](UrukService_sshd.md) (if you don't have it started already), and use any SCP/SSH client (like WinSCP, or plain scp on Linux) to copy file (default username is "root", password is "UrukDroid") to "/data/UrukUpdate".

# Update process #

In both above cases upgrade will start automatically. You should see messages in top bar with important progress steps.

Some updates/upgrade may automatically reboot your devices.

You can also monitor _"/var/lib/urukdroid/update.log"_ file - to see upgrade progress.
```
root@urukdroid:/root# tail -f /var/lib/urukdroid/update.log 
UrukUpd: Waiting free lock ...Done
UrukUpd: Decompressing file.... Done
UrukUpd: Veryfing existance of signature file...
UrukUpd: Veryfing signature...
UrukUpd: Extracting package description...
UrukUpd: Checking file integrity...
UrukUpd: Found upgrade update package
UrukUpd: Processing upgrade...
  PreInst: Updating kernel...
UrukUpd: Extracting upgrade...
```

If upgrade or update will fail somehow, you should look for a reason in /var/lib/urukdroid/fail.log.