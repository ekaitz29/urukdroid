# Introduction #

Since UrukDroid 1.1 (some hardly working features were introduced in 1.0) there is [Rescue Menu](RescueMenu.md) with Alternative OS boot functionality. Now you can store and boot more operating systems on your tablet.


# Details #

If you want to boot other then UrukDroid (Android) operating system, like plain Linux (Debian, Armstrong) or try MeeGo - you can now do it with UrukDroid rescue menu. Limitation is to the same kernel (modules are separate).

To do so you need to create proper boot file in /AlternativeOS directory called "name.boot". Rescue menu will automatically search for this type of files and ask user to choose one of them.
This file has to be a valid shell script with execution rights for root.

# Boot files structure #

Every boot file is a simple shell script with header. In header there should be name and description (for future use).
Body of the script is usually a mount option (to mount proper root file system) and chroot operation with launching init process.

debian.boot example
```
#!/bin/sh

#
# Script to boot alternative OS: Debian
#
# OS_Name: Debian
# OS_Desc: Debian armel
#
# Ver: 1.1 (14.06.2011) Adrian (Sauron) Siemieniak
#

set -xv

/bin/mount -t ext4 /dev/mmcblk2p1 /AlternativeOS/
exec /sbin/switch_root /AlternativeOS/ /sbin/init

# IF it fails - we can do some clean ups
/bin/umount /AlternativeOS/
```

Output of boot script is stored in /AlternativeOS/debug.txt file. So you can check why it failed to boot ;)