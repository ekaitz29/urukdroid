# Introduction #

NFS is another network file sharing protocol (like [smb](UrukService_smb.md), [cifs](UrukService_cifs.md)), but this one is most efficient and robust. It's usable probably only for Linux/UN\*X users (they can easily create shares) - but there are some Windows implementation of NFS servers.
NFS4 is a most recent NFS implementation that is easier to maintain on firewall, and requires less daemons to work on both client and server side.

UrukDroid implementation of NFS4 has also one more feature - it can use EXT4 filesystem as a local cache. This may help streaming video on WiFi network.

# How to use NFS4 service #

Most simple configuration requires you to have NFS4 server visible in local network. Then you need to setup share option in configuration file "/etc/uruk.conf/nfs4"
```
nfs4_source="10.8.10.1:/data/"
```
and of course start NFS4 service.

In configuration above I use [OpenVPN](UrukService_openvpn.md) server so it works from (almost) every place I have internet.

# Configuration file #

**Location: /etc/uruk.conf/nfs4**

**Configuration options:**
  * nfs4\_disable\_smbc - if enabled, NFS4 service will disable smb fuse client before mounting share. Since default place to mount nfs4 on Archos is in place of SMB share - it's wise to disable it. _Default: 1_ (disable smb client)
  * nfs4\_disable\_ndmp - if enabled, NFS4 service will disable NDMP client before mounting share. This is just for memory consumption limitation. _Default: 1_ (disable ndmp client)
  * nfs4\_source - NFS4 share in form of IP/path value. For example "192.168.1.200:/export". _Default: none_
  * nfs4\_mpoint - this is local NFS4 mount point. Place where all mounted files will be visible. By default it points to place where smb files are mounted "/mnt/storage/network/smb/" - with this "trick" MediaPlayer will be able to play all files from NFS4 share. Of course it can by any location, like usual Linux place in "/mnt" directory. _Default: "/mnt/storage/network/smb/"_
  * nfs4\_cache\_enable - should NFS4 service use local cache for remote files. It may greatly increase NFS4 file streaming "feel" - but requires some additional work (see below). _Default: 0_

# How to enable caching #

Cache system requires ext4/ext3 storage with enabled extended attributes and running "cachefilesd" daemon.

By default, if your SDcard storage partition (/sdcard/sdcard or /mnt/storage/sdcard) is EXT4 partition, you don't need to do nothing - just set _"nfs4\_cache\_enable=0"_ and restart NFS4 service. With _"ps -ef |grep cache"_ you should see "cachefilesd" process, and cache files in "
```
root@urukdroid:/root# ps -ef |grep cache
root     13165     1  0 17:42 ?        00:00:00 /usr/local/sbin/cachefilesd
root     13176 12144  0 17:42 pts/5    00:00:00 grep cache
root@urukdroid:/root# ls -l /sdcard/sdcard/cache/fscache/
total 8
drwx------ 3 root root 4096 Feb 23 20:43 cache
drwx------ 2 root root 4096 Feb 23 20:36 graveyard
```

If your storage is FAT/VFAT you can do it this way:
  * create file (size of your desire - should be big enough to storage file you are streaming)
  * make it ext4
  * mount it
  * use as cache device
```
root@urukdroid:/root# dd if=/dev/zero of=/sdcard/sdcard/nfs4.cache bs=1M count=100
100+0 records in
100+0 records out
104857600 bytes (105 MB) copied, 17.7757 s, 5.9 MB/s
root@urukdroid:/root# mkfs.ext4 -O ^huge_file /sdcard/sdcard/nfs4.cache 
mke2fs 1.41.12 (17-May-2010)
/sdcard/sdcard/nfs4.cache is not a block special device.
Proceed anyway? (y,n) y
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=0 blocks, Stripe width=0 blocks
25688 inodes, 102400 blocks
5120 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=67371008
13 block groups
8192 blocks per group, 8192 fragments per group
1976 inodes per group
Superblock backups stored on blocks: 
	8193, 24577, 40961, 57345, 73729

Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 28 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
root@urukdroid:/root# mkdir /mnt/cache
root@urukdroid:/root# mount -o loop=/dev/block/loop1,noatime,nodiratime,nosuid,user_xattr /sdcard/sdcard/nfs4.cache /mnt/cache/
```
After this you need to edit "/etc/cachefilesd.conf" and change it to point to "/mnt/cache/fscache" instead of "dir /mnt/storage/sdcard/cache/fscache/".

I know it's a bit harsh (I use all the time the first way) - but if there will be a single person who will use second method (use - not test) - let me know, I'll add it to service.