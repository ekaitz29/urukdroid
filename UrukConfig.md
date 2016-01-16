

# Introduction #

UrukConfig is and Android application created by "[solune](http://forum.xda-developers.com/member.php?u=874424)" to control UrukDroid features from User Interface level.

# Installation #

This application should be already installed on your Uruk. If not - you can [download](Download.md) it and install manually.

# Usage #

With first run of UrukConfig you will be prompted to allow SuperUser access to this application. Please grant this privileges - otherwise application will be unable to function properly.

UrukConfig is divided in three screens. First one is a place where you can managed (in a bit restricted manner) your Uruk Services. Second one gives some additional configuration options and third one is for information purpose.

## Services Tab ##

![http://urukdroid.googlecode.com/files/UrukConfig_0.7_services.png](http://urukdroid.googlecode.com/files/UrukConfig_0.7_services.png)

You can see here list of services, with it's Cfg (configuration) button, service name, bootup status (Enabled/Disabled), current status (running/down) and some key parameters for every service.


## Options Tab ##

![http://urukdroid.googlecode.com/files/UrukConfig_0.7_options.png](http://urukdroid.googlecode.com/files/UrukConfig_0.7_options.png)

Like for now you will find here only two options.

  * SoftButtons - allows to enable/disable soft buttons from right part of Archos screen (search,home,menu,back). When you disable this buttons, they will appear on the top of the screen (after reboot) - now they can be hidden by games, movie players etc. If you find yourself in a need of doing some work with "hidden" buttons (while they are hidden by some application) you can show extended button menu by pressing "long power button" (>1s) and choosing "Button mode".

  * Force Update - this options will force Uruk update service to check for new files in /data/UrukUpdate folder.



## Informations Tab ##

![http://urukdroid.googlecode.com/files/UrukConfig_0.7_informations.png](http://urukdroid.googlecode.com/files/UrukConfig_0.7_informations.png)

Here you can find some usefull informations about your device like:
  * UrukDroid release, and date of release
  * Current IP address
  * Free space on rootfs (/) and datafs (/data)
  * Free space on SDcard

# Change Log #

## `UrukConfig 1.0` ##
  * two new services cifs, wpa
  * UrukConfig should not show _"unknown"_ state to services and should update it's state much faster

## `UrukConfig 0.7` ##
  * now a button give acces to service description and will give access to it configuration for those who need it.
  * you don't change service settings in Options tab now. There will be buttons in the new setting windows to start/stop state and startup too soon.
  * In options tab for now you'll just find "force update" and "hide buttons".

## `UrukConfig 0.6` ##
  * new icons to fit with new UrukDroid design
  * new tab : Informations who give fews infos (more to come) and 2 tools : force update and possibility to hide/show softs buttons (thanks to jerry101 in this thread)
  * change in tab "options" now refresh tab "Services" when come back to it
  * new tab "Backup" but nothing inside for now, still in todo list.