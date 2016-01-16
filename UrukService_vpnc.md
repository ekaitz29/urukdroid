# Introduction #

CISCO developed it's own standard for VPN. Because of it, we have to use separate VPN tool. Luckily there is a open source "[vpnc](http://www.unix-ag.uni-kl.de/~massar/vpnc/)".

vpnc is supposed to work with:

  * Cisco VPN concentrator 3000 Series
  * Cisco IOS routers
  * Cisco PIX / ASA Zecurity Appliances
  * Juniper/Netscreen

  * Supported Authentications: Hybrid, Pre-Shared-Key + XAUTH, Pre-Shared-Key
  * Supported IKE DH-Groups: dh1 dh2 dh5
  * Supported Hash Algo (IKE/IPSEC): md5 sha1
  * Supported Encryptions (IKE/IPSEC): (null) (1des) 3des aes128 aes192 aes256
  * Perfect Forward Secrecy: nopfs dh1 dh2 dh5

# How to use VPNC service? #

Like with every service you can enable it for boot time, or run every time you need it with UrukConfig. In both cases you should edit VPNC profile configuration file, called _"archos.conf"_. Profiles are located in _"/etc/vpnc/"_ directory. You can find there an example called "example.conf"
```
#IPSec gateway <gateway>
#IPSec ID <group-id>
#IPSec secret <group-psk>
#IKE Authmode hybrid
#Xauth username <username>
#Xauth password <password>
```

This are the same configuration options like in Cisco vpn client.

If you want to use different profile, you can change it's name in _"/etc/uruk.conf/vpnc"_.

# Configuration file #

**Location:** /etc/uruk.conf/vpnc

**Configuration options:**
  * VPNC\_PATH - path to directory where VPNC profiles are stored. _Default: "/etc/vpnc"_
  * VPNC\_PROFILE - name of the default profiles used by vpnc. _Default: "archos"_