# FAQ #



## My HDMI connection does not work ##
Please make sure you did not uninstall/removed system application LiveWallpapers. This is somehow required for Archos interface to switch to other display.
```
[root@urukdroid root]# ls -l /system/app/Live*
-rw-r--r--    1 root     root       3270738 Dec 29 18:57 /system/app/LiveWallpapers.apk
-rw-r--r--    1 root     root         48469 Dec 29 18:57 /system/app/LiveWallpapersPicker.apk
```

## Battery does not charge to 100% ##
You can recalibrate battery charge level by:
  * charge Archos battery to full level (when you see it won't charge any more for 15-20 minutes - it's probably at 100%, even if it shows something different). I use [Battery Widget](http://www.appbrain.com/app/battery-widget/personal.jhjeong.app.batterylite) to control charge level and see how it discharge/charge.
  * erase **/data/system/batterystats.bin** file (from terminal, or with [File Expert](http://www.appbrain.com/app/file-expert/xcxin.filexpert) in root mode)
  * unplug charging cable - you should now see it's 100% charged.

## My UrukDroid fails to hibernate (deep sleep) ##

In most cases this is because there is some background connection or task that won't brake for deep sleep - check for running applications smb/nfs shares etc. Do tests with disabled WiFi.

## How to prevent Uruk from booting SDcard ##

UrukDroid loader always tries to boot from SDCard on the first place, then from Internal storage. Loader checks how many partitions is on SDCard (if present) - if there are 3 or more, it assumes it's Uruk installation and will try to boot from it.

So if (for example) you have:
  * old installation of Uruk on SDCard and you moved internal
  * full bootable UrukDroid backup on SDCard

And you want permanently force Uruk to boot from Internal, label first SDCard partition as "noboot".
You can do it on any other PC, on Uruk it should look like this
```
su
e2label /dev/block/mmcblkp2p1 noboot
```
You may change it back with giving partition any other name (for example "boot").
This "trick" will work on UrukDroid 1.1+

## I've tried to use OC kernel - but it does not work ##

OC (OverClocked) kernel may work only on some CPUs (it's just luck - not something you can determine). It may also work partially - even if device booted up, it does not have to mean it works fully correctly (there can be some calculation errors, corruptions etc).

Anyway if you have tried OC kernel and it failed to boot completely, you need to power off device, go to Developer Menu (just like during installation process) and flash proper zImage and initramfs.cpio.gz  (this are not the files used for EasyInstall!) which can be found in Uruk Droid repository (go to proper version folder): http://sauron.pourix.com/UrukDroid/

If device get unstable or has some errors - you may try to revert to normal kernel with UrukDroid package - you can also find this packaged in repository (there name is something like: UrukDroid-1.5-kernel.tbz2).

## My UrukDroid (1.0+) fails to boot ##

Most common reason is corrupted filesystem. Even so Uruk will try to repair every partitions during bootup process, it may sometimes fail to do so. This should not happened during normal usage process. But when rootfs (system partition) get badly corrupted, easiest solution to fix it is to "[ReInstall](EasyInstall#ReInstall_UrukDroid.md)" it with [EasyInstall](EasyInstall.md). This will format and install Uruk on your tablet, without touching your datafs (application) or storagefs.

Of course you can also connect (if it's SDCard) media to Linux machine and try to fsck it manually. It is also possible (if you have Uruk internal and SDCard) to boot from another Uruk and do fsck of other partition from it's shell.

## How to migrate from SDCard to Internal installation method ? ##

If you have already installed Uruk Droid on SDCard, please do an internal installation with EasyInstall. Boot again from SDCard and use "[copy\_from\_sd\_to\_internal.sh](http://code.google.com/p/urukdroid/wiki/UrukDroid_utilities#copy_from_sd_to_internal.sh)".

## How to migrate from Internal installation method to SDCard? ##

If you have already installed Uruk Droid in internal space, please do an SDCard installation with EasyInstall. Boot again from internal and use "[copy\_from\_internal\_to\_sd.sh](http://code.google.com/p/urukdroid/wiki/UrukDroid_utilities#copy_from_internal_to_sd.sh)".

## What files need to be removed to install the UrukDroid Market? ##

If you have already installed Market, and you don't want to reinstall your applications (do fresh install without copying /data (datafs)). You can try with removing this files before installation of UrukDroid Market package.
```
system/lib/libzxing.so
system/lib/libinterstitial.so
system/lib/libspeech.so
system/lib/libvoicesearch.so
system/lib/libimageutils.so
system/framework/com.google.android.maps.jar
system/app/Talk.apk
system/app/GoogleCalendarSyncAdapter.apk
system/app/GenieWidget.apk
system/app/GoogleContactsSyncAdapter.apk
system/app/NetworkLocation.apk
system/app/GoogleFeedback.apk
system/app/MarketUpdater.apk
system/app/GoogleServicesFramework.apk
system/app/Vending.apk
system/app/MediaUploader.apk
system/app/GoogleBackupTransport.apk
```


## How to gather data from UrukDroid for reports purpose ? ##

The best way is to use [SSH](http://en.wikipedia.org/wiki/Secure_Shell). To do this, please start "[sshd service](UrukService_sshd.md) on UrukDroid by using [UrukConfig](UrukConfig.md) application or by editing /etc/uruk.conf/sshd file.
First start can take up to one minute - since sshd has to generate unique encryption keys.
If you use Windows download [putty.exe](http://the.earth.li/~sgtatham/putty/latest/x86/putty.exe) (ssh client) and run it. Write your Archos IP (it has to be visible in local WiFi network) and connect.
Use
```
Login: root
Password: UrukDroid
```
Now you can write Linux commands and cut/paste results for help/debug purpose.


## What is current directory/disk layout? ##
```
/ -> rootfs partition (default 512M) - for root filesystem
/data -> datafs partition (default 1GB) - for installed apps
/mnt/storage -> internal storage partition - for data used by installed apps
/mnt/storage/sdcard -> SDCard third partition - anything you want, nothing by default
```

And there is something called symbolic links (symlinks) - witch are kind of Win shortcuts used on UN\*X extensively.
```
/sdcard -> /mnt/storage
/storage -> /mnt/storage
/mnt/sdcard -> /mnt/storage
```
So you can enter /sdcard - and you are be using files from /mnt/storage. You can also create symlinks by yourself
```
su
ln -s /source destinations
```


## How to mount ext4 under Windows? ##

There is project called "ext2read" that claims to work also with ext4  (I've only tested it with ext2 long time ago - it worked) http://sourceforge.net/projects/ext2read/ - please write some comments if you use it.

## I'm getting "Firmware Update Available" notification, what should I do? ##

This is notification of Archos updater, you should ignore it and if you want to get rid of this message - remove "Daos.apk". This application is required only during initial run, later it can be safely removed. Use file manager or from shell:
```
root@urukdroid:$ su
root@urukdroid:/root# cd /system/app
root@urukdroid:/system/app# ls -l Daos.apk 
-rw-r--r-- 1 root root 79043 Feb  1 23:32 Daos.apk
root@urukdroid:/system/app# mv Daos.apk ../app.old/
```