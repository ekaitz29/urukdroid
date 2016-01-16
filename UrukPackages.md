# Introduction #

UrukDroid has it's own package system for doing various type of modification. We have three types of packages:
  * update
  * upgrade
  * kernel

# Details #

For doing all type of already installed system I've prepared packaging system. It's easy and flexible way of modifying Uruk.

## Type of packages ##

Like you already know, we have three types of UrukDroid packages

### Update ###

This is most common type of packages, it brings all those small changes and fixes to system. This packages usually works in "overwrite" mode - so nothing is erased.
Proper update can made on system level (so device restart is not required) and on boot time level (during boot up process you will see message about update being applied)

### Upgrade ###

This type is used mostly during major system upgrades. All work is done during bootup process and inflicts erasing most of **rootfs** data. So probably all you service configurations will be overwritten.

### Kernel ###

This are kernel packages, their task is to update kernel and initramfs images. They install without reboot, but of course to see changes reboot is required.

## Installation ##

To install package you need to simply copy/move it to **/data/UrukUpdate** folder. During install process (since UrukDroid 1.1) you should see communicates on top bar.

# Trouble shooting #

If you see that package installation failed, read error message. You should see it in top bar (prior to UrukDroid 1.1 you should look for it in text, log file /var/lib/urukdroid/fail.log - this file is also present in later realises).

Most common errors are:
  * **Wrong file**: This means system did not recognize package, probably it's not an UrukDroid package or it's corrupted
  * **No package description file**: System was unable to extract package description file. This means that file is probably corrupted (and can't be extracted), but it could also mean that this is proper type of archive, but it's not UrukDroid package.
  * **Veryfing signature failed**: This means package was somehow altered. At this level it's weak protection against unskilled package modification, later it may became strong private/public key protection.
  * **Pre/Post installation script failed**: Package can have some scripts inside to modify more complex updates/upgrades - this is information that one of them failed to complete