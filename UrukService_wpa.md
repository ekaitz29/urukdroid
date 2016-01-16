# Introduction #

Encrypted WiFi connection requires some kind of WPA supplicant. This is done by the tool called exactly the same _"wpa\_supplicant"_ (located in /system/bin directory).

To enable connecting to Ad-Hoc WiFi networks, one of the ways is to use [patched](http://szym.net/2010/12/adhoc-wifi-in-android/) and recompiled "wpa\_supplicant". With this modifications ad-hoc networks are visible like every other network but with "`*`" prefix. Since this kind of change made wpa\_supplicant not compatible with build in configuration user interface it's disabled by default.

If you would like to use Ad-Hoc WiFi networks please enable "wpa" service (this will exchange wpa\_supplicants) and from now on you should use "[WiFi Manager](http://www.appbrain.com/app/wifi-manager/org.kman.WifiManager)" instead of Android/Archos default WiFi configuration wizard (anyway - it's much better tool and I use it all the time). Since Uruk Droid 1.0 this tool (and widget) is installed by default.


# How to use WPA service #

You should use WPA service if:
  * you use Ad-Hoc WiFi networks

To use service you should:
  * Enable WPA service
  * Use [WiFi Manager](http://www.appbrain.com/app/wifi-manager/org.kman.WifiManager) to configure WiFi networks and enable/disable WiFi support
  * Ignore signal strength on upper bar of the system (it's always zero)