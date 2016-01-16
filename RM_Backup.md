# Introduction #

Backup menu is a easy way to backup your entire, vital partitions of UrukDroid. This is rootfs partition (hold operating system) and datafs (storing installed application and it's settings).

Backup files are stored on SDcard - thus it has to be present and should have enough free space to create backup.

# Why use backups? #

Well despite obvious ;) it's good to prepare backup before every major update/upgrade. This is also a good way of moving entire system between compatible devices, storing your system for service time etc. etc.
There are many ways you can utilise this almost "[bare metal](http://en.wikipedia.org/wiki/Bare-metal_restore)" backups.

# Details #

You should look for backup files on your SDcard in "UrukDroid\_backup" directory. File structure looks like this:

```
/sdcard/sdcard/UrukDroid_backup/
|-- 2011.06.15
|   |-- UrukDroid_rootfs_backup.md5
|   `-- UrukDroid_rootfs_backup.tgz
|-- 2011.06.16
|   |-- UrukDroid_datafs_backup.md5
|   |-- UrukDroid_datafs_backup.tgz
|   |-- UrukDroid_rootfs_backup.md5
|   `-- UrukDroid_rootfs_backup.tgz
`-- 2011.06.17
    |-- UrukDroid_rootfs_backup.md5
    `-- UrukDroid_rootfs_backup.tgz

3 directories, 8 files
```

Like you can see this are plain "tar" archives compressed with "gzip". There are also md5 checksum files for validating purpose.

# How to use Backup Menu #

You should boot to "Rescue Menu", choose "Backup Menu". Then you can create backup of _"rootfs"_ and _"datafs"_ or restore those backups.

## Creating backup ##

When you choose to create backup file, system will try to mount proper filesystems and will check if there is enough free space. If there is less free space then uncompressed size of future backup, you will be warned, but you can still proceed.

Then you will see backup progress, with estimated time to finish. After successfully created backup file, system will create md5 checksum and finish entire process.

## Restoring backup ##

Restoring backup should be as straight forward as doing it. So you choose to restore _"rootfs"_ or _"datafs"_, then you are able to choose from your backups found on SDCard. Later system will check backup file consistency and start restoring files.