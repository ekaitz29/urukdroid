# Introduction #

SMB is a network protocol used mainly by Microsoft Windows systems to share files. With this service you will be able to create SMB share from Archos disks and managed all it's storage/sdcard data on your Windows PC.

# How to use SMB service #

In most cases it's enough to enable it like all other services. But you may want to change exported directory or password. Default user name is "storage" and password "UrukDroid".

You can also change password for user "storage" by using "smbpasswd" command.
```
root@urukdroid:/root# smbpasswd storage
New SMB password:
Retype new SMB password:
```

# Configuration file #
**Location:** /etc/uruk.conf/samba

There are not special parameters in Uruk Service Samba configuration file. Although you may want to edit smb.conf file

**Location:** /etc/samba/smb.conf
```
[storage]
        comment = Archos storage
        path = /mnt/storage/
        guest ok = no
        writable = yes
#       share modes = yes
        create mode = 0775
        create mask = 0775
        directory mask = 0775
        valid users = storage
        invalid users = root daemon bin sys sync mail proxy www-data backup operator sshd nobody media default
```
This is part of configuration file describing Archos share. You may want to change file path, name or user.