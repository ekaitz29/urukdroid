

# Introduction #

DVB service for Uruk Droid should make a bit easier initializing your USB DVB-T dongle with Archos devices. Only few devices are already tested to work, so if you try it with different hardware - please let us know if it works.

This manual is for UrukDroid 1.0+ only (older releases worked in a bit different way).

You will also need some application to stream data from DVB to mediasystem. This kind of application is LiveTV made by chulri. You can download it from [project page](http://code.google.com/p/archos-gen8-dvb/downloads/list).

# DVB devices that are known to work #

  * [WinTV-HVR-950Q](http://www.linuxtv.org/wiki/index.php/Hauppauge_WinTV-HVR-950Q) xc5000 chipset
  * [EzTV DUTV009 USB DVB-T Receiver](http://www.linuxtv.org/wiki/index.php/E3C_EC168) EC168 chipset
  * DiBcom DiB0700 USB DVB devices dib0700 chipset

# How to use DVB service #

If your device is on above list - you need only to uncomment proper line in configuration (/etc/uruk.conf/dvb) file.
```
# Part of Uruk-Droid Android configuration system
#
# ver. 1.2 (26.04.2011) Adrian (Sauron) Siemieniak
#

# 1 to enable this service
# 0 to disable this service
service_enabled=0

# Where to store device information
dvb_devices_conf="/etc/uruk.conf/dvb-devices"

# DVB card type
# Working USB DVB devices
# 1. (dvb-usb-af9005) Afatech AF9005 DVB-T USB1.1 support
# 2. (dvb-usb-dib0700) DiBcom DiB0700 USB DVB devices (see help for supported devices)
#dvb_driver='dvb-usb-dib0700'
# 3. (dvb-usb-af9015) Afatech AF9015 DVB-T USB2.0 support
# 4. (dvb-usb-cinergyT2) Terratec CinergyT2/qanu USB 2.0 DVB-T receiver
# 5. (smsusb) Siano SMS1XXX USB dongle support
# 6. (dvb-usb-ec168) EC168 USB dongle support
#dvb_driver='dvb-usb-ec168'
# 7. (xc5000) WinTV-HVR-950Q dongle support
dvb_driver="xc5000"
```
And restart DVB service with USB DVB device connected to Archos. Above  you can see an example for Haupage 950Q DVB device.

To test if device is configured properly you can use command:
```
root@urukdroid:/root# cd /etc/uruk.d/
root@urukdroid:/etc/uruk.d# ./dvb devstatus
Uruk-DVB: device configured
```
If you will see message "device not found" you may wan to try "./dvb fixdev" command. This will try to generate proper configuration file for your device.

# How does DVB service works #

This knowledge may be required to run your device.

First of all, like every other device DVB-T dongles requires driver and probably firmware. Driver is a Linux kernel part shipped with UrukDroid. There is quite a big bunch of those drivers - but they need to be tested and configured properly.
```
root@urukdroid:/etc/uruk.d# cd /lib/modules/2.6.29-omap1/kernel/drivers/media/dvb/dvb-usb/
root@urukdroid:/lib/modules/2.6.29-omap1/kernel/drivers/media/dvb/dvb-usb# ls
dvb-usb-a800.ko           dvb-usb-au6610.ko     dvb-usb-dib0700.ko        dvb-usb-dtt200u.ko  dvb-usb-gl861.ko        dvb-usb-ttusb2.ko
dvb-usb-af9005-remote.ko  dvb-usb-az6027.ko     dvb-usb-dibusb-common.ko  dvb-usb-dtv5100.ko  dvb-usb-gp8psk.ko       dvb-usb-umt-010.ko
dvb-usb-af9005.ko         dvb-usb-ce6230.ko     dvb-usb-dibusb-mb.ko      dvb-usb-dw2102.ko   dvb-usb-m920x.ko        dvb-usb-vp702x.ko
dvb-usb-af9015.ko         dvb-usb-cinergyT2.ko  dvb-usb-dibusb-mc.ko      dvb-usb-ec168.ko    dvb-usb-nova-t-usb2.ko  dvb-usb-vp7045.ko
dvb-usb-anysee.ko         dvb-usb-cxusb.ko      dvb-usb-digitv.ko         dvb-usb-friio.ko    dvb-usb-opera.ko        dvb-usb.ko
```

Some of this drivers requires proper firmware
```
root@urukdroid:/root# ls /lib/firmware/
TIInit_7.2.31.bts  af9005.fw  dvb-fe-xc5000-1.6.114.fw  dvb-usb-af9015.fw  dvb-usb-dib0700-1.20.fw  dvb-usb-ec168.fw
```
If it's not there already - you have to find it on net (and if working - report back to us).

When DVB service is started:
  * it loads some default, required modules and modules configured in _/etc/uruk.conf/dvb_
  * if device is present, and driver will report back it existence by creating _/dev/dvb0.`*`_ devices,
  * service will create/update dvb configuration file in _/etc/uruk.conf/dvb-devices_.

This is how it should work and since now you should be able to use your dvb freely.

Sometimes devices like WinTV-HVR-950Q don't want to configure properly while plugged in (modules are reporting errors). You will need to load service first and then connect USB. But in this case we will miss some required information to create _/etc/uruk.conf/dvb-devices_ - that's why there is "./dvb fixdev"

## More detailed steps ##

  * ./dvb start (or during system start)
  * dvb checks if it's not already started and loads dvb core and usb modules
  * dvb loads modules from /etc/uruk.conf/dvb file
    * before this, "modprobe" will check for module dependencies and try to load all required modules before - you can see all soft dependencies in _/etc/modprobe.d/dvb.conf_
  * dvb will check if /dev/dvb0.`*` devices are present (this are driver reported working dvb devices)
    * if device is present, dvb will try to update _/etc/uruk.conf/dvb-devices_ with proper MIN/MAJ values and create devices in /dev/dvb/
    * if device is NOT present, dvb will try to create devices in /dev/dvb/ based on configuration from _/etc/uruk.conf/dvb-devices_

## What for is _/etc/uruk.conf/dvb-devices_ file? ##

DVB driver creates proper device in /dev/dvb0.`*`. LiveTV application requires devices to be created in /dev/dvb/frontend0/`*`.  So we need to create those devices in different place (this stuff is usually made with mknod tool). We could do this with a simple symlink (ln -s /dev/dvb0.demux /dev/dvb/frontend0/dvb.demux) but this will not solve one more problem - file access permissions. Devices to be readable/writeable by Android apps requires (long story short) 0777 permission.

So in this file we have stored information how to recreate device in /dev/dvb/frontend0/ directory, even when our DVB device is not plugged in (so we can start Archos, later plug DVB device and it should work instantly).

# DVB Service special options #
DVB service has two special options, to help you configure it properly.

  * ./dvb devstatus - this will show you if your device IS or ISN'T visible to system. Even if this option shows that device is configured, you may need still use "fixdev" to make it work with LiveTV app.
  * ./dvb fixdev - this option fill force creating dvb configuration file _/etc/uruk.conf/dvb-devices_. This file is updated automatically on every dvb service start, but with some devices it may not work. This option should be required to be called just once - later dvb service will use already created dvb configuration.

# Configuration file #

**Location:** /etc/uruk.conf/dvb

**Configuration options:**
  * dvb\_devices\_conf - file name, where DVB service should store information about DVB devices. _Default: "/etc/uruk.conf/dvb-devices"_
  * dvb\_driver - name of DVB driver that suits your DVB usb dongle. Please choose one from listen in configuration file, or add new. _Default: none_


# Example #

Here is small example of working DVBT with Uruk Droid 0.7 and LiveDVB app.
<a href='http://www.youtube.com/watch?feature=player_embedded&v=sJjoiP4fAt4' target='_blank'><img src='http://img.youtube.com/vi/sJjoiP4fAt4/0.jpg' width='425' height=344 /></a>

# How to configure DVB service for new DVB devices #

## Gather information ##

Please find all required information about this device. [LinuxTV wiki](http://www.linuxtv.org/vdrwiki/index.php/Main_Page) page is a good place to start. If you will find name for proper Linux kernel module, and it's present in Uruk - your are ready to go. If this modules is not present - you can try in this [XDA thread](http://forum.xda-developers.com/showthread.php?t=871391) to find help.

Check if this chip requires any firmware, if this firmware is present in Uruk. If not - find it and put in /lib/firmware directory of your Archos device.

## Find module dependencies ##

SSH to your Uruk device, became root (su) and load required module
```
root@urukdroid:/root# modprobe -a dvb-core dvb-usb
root@urukdroid:/root# lsmod | grep dvb
dvb_usb                19996  0
dvb_core               89240  1 dvb_usb,[permanent]
```

The task now is to find all modules that driver depends on - this is example for "dvb-usb-af9015" module. You will need to try load module and check in "dmesg" if it's missing something. Then look where missing stuff is, load new modules - and try again.

```
root@urukdroid:/etc/uruk.conf# modprobe dvb-usb-af9015
root@urukdroid:/etc/uruk.conf# dmesg | tail -5
Configure McBSP TX FIFO threshold to 1260
init: sys_prop: mis-match msg size recieved: -1 expected: 128
Configure McBSP for 1 phase
Configure McBSP TX FIFO threshold to 1260
usbcore: registered new interface driver dvb_usb_af9015
```
In this case we can see that "dvb-usb-af9015" loaded properly and does not requires any additional modules. So work is done :)

In some cases you will find here lines like "missing symbol xxxaaabbb" - then you need to find module with the missing symbol. Crude but working way of doing this is using "grep" command.
```
root@urukdroid:/etc/uruk.conf# cd /lib/modules/2.6.29-omap1/kernel/drivers/media/
root@urukdroid:/lib/modules/2.6.29-omap1/kernel/drivers/media# ls
common  dvb  video
root@urukdroid:/lib/modules/2.6.29-omap1/kernel/drivers/media# grep -ri 950q *
Binary file video/au0828/au0828.ko matches
```

## Create configuration ##

When you will gather all dependency information, you can edit "/etc/modprobe.d/dvb.conf" to add some missing modules dependencies (it's quite simple). And modify DVB service config file. Then reboot device, start dvb service manually and check if it's working properly.