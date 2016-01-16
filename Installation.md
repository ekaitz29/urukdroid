

# Introduction #

This is installation procedure for UrukDroid 1.0+ with [EasyInstall](EasyInstall.md) method. You can also do it [manually](http://forum.xda-developers.com/showpost.php?p=10249905&postcount=7).


# Some useful information #

## Warning ##
  * UrukDroid is known to work on A70S and H, A101 (8/16GB) and A43. However on A70H it may be installed only on HD.
  * Be aware that this modification requires SDE and probably some Linux knowledge.
  * By doing the steps described below you probably can't brick your Archos - but do it on your own risk.
  * Root access on your device makes it less secure for malicious software (use more head - less fingers ;) )


## Known problems: ##
  * Sometimes WiFi can't be turned on - restart fix the problem
  * If you can't connect to WiFi, please try build in WiFi Manager utility/widget or disable WPA service
  * Some people reported unable to see device info from preferences/settings menu


## Before you start: ##
  * Read about SDE on forum, read SDE warning on Archos page before install
  * All operations described here, are done on Linux or Android and should be done from `root` user (you can switch to that user in terminal by typing "su" or "sudo su" command)
  * If you don't have Linux on your PC - you can find any recent [Rescue CD](http://www.sysresccd.org/Download), Live CD or Virtual disk (VirtualBox or VMware) - distribution does not matter. If you don't know what to choose - get Rescue CD from above link.
  * This method REQUIRES 2GB+[SDHC (SD)](http://en.wikipedia.org/wiki/SDHC#SDHC) by default, or resizing/formatting internal storage.


Since UrukDroid 0.6 there is new automated install method. It puts some restriction on flexibility of installation - but it should satisfy most of users; for more experienced ones - you can do it in old (manual) way.

# Installation #

## Location of buttons and sockets on A70 ##
![http://urukdroid.googlecode.com/files/A70_desc.png](http://urukdroid.googlecode.com/files/A70_desc.png)
Use numbers from above picture to find corresponding buttons/sockets in text below.

## Step one ##

**Important notice**: Because of performance reason it is recommended to install UrukDroid internally (on internal storage). In most cases all so called "Force Close" errors, poor performance etc. are because of slow SDCard (10x SDCard does not have to be "good" for operating system - it's a bit more complex work to find "good" SDCard). However because of easiness default "Simple" method is still external.

Assuming you have already installed [SDE from Archos](http://www.archos.com/support/support_tech/updates.html?country=us&lang=en):

Download and extract installation files from archive **UrukDroid\_1.5-EasyInstall.rar**. Inside you should find three files: **initramfs.cpio.gz**, **zImage** and **UrukDroid-install.tgz**

Flash initramfs.cpio.gz and zImage from SDE boot menu:
  * power on (2) Archos device, hold up/+ volume key (1) until you see _"Archos AXXXX - Boot Menu"_,
  * choose with Volume +/- (1) _"Recovery System"_->_"Developer Edition Menu"_->_"Flash Kernel and Initramfs"_,
  * connect Archos to PC (5) and copy zImage and initramfs.cpio.gz
  * press power button (2) shortly, you should see Archos flashing new kernel
  * if flashed properly, press power button (2) shortly to reboot...

Boot to SDE:
  * power on (2) Archos, hold up/+ volume key (1) until you see _"Archos AXXXX - Boot Menu"_,
  * choose "Developer edition"


You should see **"UrukDroid 1.5 Installation framework"** title. Please choose simple install method. When asked to, connect Archos to PC (5) once again and copy UrukDroid-install.tgz, disconnect Archos from PC **_properly_** (umount, safely remove device etc.) and press power button (2) shortly. Now [EI](EasyInstall.md) will check installation file and prepare it for next step.

Later, you will be also able to choose whether you want to copy /data partition. It's recommended not to - but you have this option.
For advanced install method - look below.

After reboot you should see UrukDroid 1.5 boot up screen (if it happens to boot to stock OS, reboot once again and go to _"Boot menu"_, choose _"Developer edition"_).

You should see some progress information on bottom of the screen.
For few minutes you will see installation message with progress bar.
Few minutes later, after some postinstallation procedures you should see UrukDroid boot animation and shortly after Archos setup wizard.

If with first run "Archos configuration wizard" creates "Force close" errors, please reboot device (hold power button shortly for more than 1 second, this will bring "Power menu" and press power button long until "Reboot" message will appear).

**Congratulations!** you have just installed UrukDroid

Here you can watch video created by [ArcTablet](http://www.arctablet.com/blog/) with Easy Installation of UrukDroid 0.6
<a href='http://www.youtube.com/watch?feature=player_embedded&v=LbqKwl6ggFo' target='_blank'><img src='http://img.youtube.com/vi/LbqKwl6ggFo/0.jpg' width='425' height=344 /></a><br>
It's a bit old but gives a good insight how it should look like.<br>
<br>
<h2>Step two: optional</h2>

If you want <b>GoogleMarket</b> (and required component to make it work) it's recomended to use (more up to date) <a href='http://www.arctablet.com/blog/archos-tablet/arctools-google-apps-and-market-installer-for-archos-gen8-youtube-fixed/'>ArcTools</a> from AppStore.<br>
<br>
You can also install <a href='UrukPackages.md'>UrukDroid package</a> (thus you will have no WiFi location enabled) - UrukDroid-GoogleMarket_1.0.tbz2. (files inside this package are base on kenyu73 work).<br>
<font color='darkred' size='+1'>If you copied your old /data, you cannot have installed any other version of Market. If you apply this update, on previously installed market/vending etc. - it won't work.</font> This packaged is tested with fresh install of Uruk - where it works.<br>
Download archive and put it in UrukUpdate directory located on /data partition<br>
(so path is /data/UrukUpdate/). You should do it directly from internet browser on Archos Tablet, file manager like Astro or terminal - you shouldn't do it over USB.<br>
Installation process will start automatically and silently, file will disappear from that folder after it's done. To run Market, restart is required when you'll be ready.<br>
<br>
<h2>Advanced EasyInstall</h2>
Since UrukDroid 0.7 you are able to choose, during install process, method called "Advanced". This option will give you possibility to:<br>
<ul><li>choose partition sizes (from defined list of choices) when installing to SDCard or formatting Internal storage,<br>
</li><li>you are also able to choose Internal installation method with "resize" option. This method will try to reduce size of your current internal storage (visible on stock OS under /mnt/storage) and create additional filesystems. You cannot choose filesystem sizes here (it will use default/simple one 512MB for rootfs and 1GB for datafs) and YOU MUST assure enough free space on shrinked filesystem. So <font color='darkred'>MAKE SURE</font> your /mnt/storage has <font color='darkred'>AT LEAST 1.7GB free space</font> - preferably more - otherwise this method will fail. This condition is not checked during install process.</li></ul>

<h1>Installation of additional package</h1>

There are few additional <a href='UrukPackages.md'>UrukDroid packages</a> you can install, this are usually files with extension ".tbz2".