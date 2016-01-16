

# Introduction #

EasyInstall is a code name for simple installation framework for UrukDroid. It was created as a successor of the previous installation method, involving Linux usage which was to harsh for most of our users.

# Usage #

EasyInstall consist of two files, initramfs and kernel image. Both need to be applied to Archos device with help of "Boot Menu" (see [installation process](http://code.google.com/p/urukdroid/wiki/Installation#Step_one)).

After boot up (use _"Boot Menu"_ and choose _"Developer edition"_) you should see screen with title "UrukDroid? 1.5 Installation framework" and simple menu tree:

  * Are you sure you want to proced with installation of UrukDroid?
    1. No
    1. [Install UrukDroid](#Install_UrukDroid.md)
      1. [Simple](#Simple_method.md)
        * Do you want UrukDroid to copy your existing /data partition (may cause trouble in future)?
      1. [Advanced](#Advanced_method.md)
        1. [Install to SDCard](#Install_to_SDCard.md)
          * You will be asked for partitions sizes here
          * Do you want UrukDroid to copy you existing /data partition (may cause trouble in future)?
        1. [Install to Internal storage](#Install_to_Internal_storage.md)
          1. Resize existing partition
          1. Format and create new partitions
            * You will be asked for partitions sizes here
            * Do you want UrukDroid to copy you existing /data partition (may cause trouble in future)?
    1. [ReInstall UrukDroid](#ReInstall_UrukDroid.md)
      1. ReInstall to SDCard (default for Simple installation)"
      1. ReInstall to Internal storage


## `Install UrukDroid` ##

  * What type of installation you want to use? (simple recommended)
    1. [Simple](#Simple_method.md)
    1. [Advanced](#Advanced_method.md)

**Simple method** will start installation on SDCard or HD (A70H) with predefined partition sizes - if you don't know what to choose, pick this one.

**Advanced method** will give you choice of where you want to install Uruk (except A70H) - whether it should be internal or SDCard installation. In some conditions you will also be able to choose partition sizes.

### Simple method ###

EI will partition your SDcard and format it, then you will be asked to transfer installation file (UrukDroid-install.tgz). After testing archive it will be prepared to next step.

If for some reason EI will report error - that install file is corrupted, please make sure that downloaded file is correct (check file md5sum or RAR installation package integrity).

Before reboot you will be asked if you want to copy "datafs" partition content from stock Archos OS. You can do it - but under some condition it may be a cause of future instability.

### Advanced method ###

On all devices, except A70H, you will have to choose:

  * Do you want to install UrukDroid on removable SD card, or internal storage. (SD card installation recommended)
    1. [Install to SDCard](#Install_to_SDCard.md)
    1. [Install to Internal storage](#Install_to_Internal_storage.md)

On A70H you will be moved already to partition size chooser - just like with "[Install to SDCard](#Install_to_SDCard.md)".

### Install to SDCard ###

You will be asked for partitions sizes here. Not much to write here :)

### Install to Internal storage ###

  * Do you want to resize existing internal partition or format and create new ones? (Resizing requires enough free space of /sdcard storage! - it will not be checked)
    1. Resize existing partition
    1. Format and create new partitions

You may choose to resize existing storage partition or format internal storage and create partition from scratch.
What is internal storage? Archos has 2 internal, virtual disks visible on system.
  1. /dev/block/mmcblk0
  1. /dev/block/mmcblk1

  1. This disk holds boot record, rawfs (with kernel and initramfs), system and data partitions
  1. This disk holds only one partition mounted by default as /mnt/storage (symlink to /sdcard)

So if you want to have custom sized _rootfs_ and _datafs_ (different then default - 512MiB i 1GiB) for UrukDroid and you are willing to loose all stuff on /mnt/storage partition you may choose _"Format and create new partitions"_.

If you will choose _"Resize existing partition"_ EI will shrink your /mnt/storage partition and create two new, required filesystem. Be aware that:
  * This operation is not entirely safe, it's done with _"parted"_ utility - it's good, tested tool but authors give a fair warning it may fail
  * You HAVE TO prepare /mnt/storage partition before this operation so there will be AT LEAST 1.7GiB free space. This condition is not checked during resizing procedure and if you fail to meet this condition - resizing will certainly also fail, and you may damage your /mnt/storage partition (called on Uruk _"storagefs"_)


## `ReInstall UrukDroid` ##

EI will help you to repair damaged UrukDroid installation by reformatting rootfs without touching datafs (stored apps and settings).

For all devices except A70H you will be asked for location of installed UrukDroid you want to repair (with A70H process will start automatically - since it can only be installed on HD).

  * Do you want to ReInstall/Repair UrukDroid on removable SD card, or internal storage?
    1. ReInstall to SDCard (default for Simple installation)"
    1. ReInstall to Internal storage

In both cases EI will try to format proper partition, will ask you to transfer installation file and will prepare device for later installation.

EI can't really check if what you have chosen is correct answer (about installation type) - so if you choose badly it may format wrong partition - so please be careful.