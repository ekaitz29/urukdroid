# Introduction #

Uruk services are special programs/scripts that enable certain functionality during boot process or on user demand. They are created to make some task easier and to save some memory for unused modules.


# General information #

Every UrukDroid service is build from it's configuration file and initializing script.
All configuration files are located in `/etc/uruk.conf` and all initializing scripts are in `/etc/uruk.d`. During boot process, `rcS` services tries to start all services located (in this case symlinked) in `/etc/init.d/`.

To enable service during boot you need to change in it's configuration file "service\_enabled" flag. For "sshd" service it looks like this:
```
root@urukdroid:/etc/uruk.conf# cat sshd
# Part of Uruk-Droid Android configuration system
#
# ver. 1.0 (14.01.2011) Adrian (Sauron) Siemieniak
#

# 1 to enable this service
# 0 to disable this service
service_enabled=1

# SSH password for root login
SSHD_PASS="UrukDroid"

# Port number for SSHd to listen on
SSHD_PORT=22

# Other configuration
CONFDIR=/etc/ssh/
SSHD_RSA_KEY=$CONFDIR"dropbear_rsa_key"
SSHD_DSS_KEY=$CONFDIR"dropbear_dss_key"
SSHD_BANNER=$CONFDIR"banner.txt"
SSHD_HOME="/root/"
```
Like you can see, this service is already enabled. To change it's behaviour during boot process use any text editor (like one from **RootExplorer**), use shell **nano** editor or simply install and use **UrukConfig** application.

For more information please read detailed documentation on every service (left menu).