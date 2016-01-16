# Introduction #

Most of operating systems are able to use slower swap memory, when there is a lack of real RAM. Since GEN8 Archos devices has only 256MB of RAM, it's quite essential to use some swap memory.
Android system uses dedicated subsystem to manage running application and dispose unused ones if more RAM memory is needed. Sadly with 256MB of RAM it means that most of the time only one application can be running (one big - like web browser, pdf reader etc).

# When to use SWAP service #

If you are fed up with applications being killed all the time, when you run any new one - you should enable SWAP memory. Drawback of using this type of memory is less snappy device. You will experience some few seconds freezes of user interface while changing applications - during this few seconds system will swap memory from RAM to disk and vice-versa.

# How to use SWAP service #

You can choose between three ways of using SWAP memory. Two of them do not need any system changes. That is [CompCache](UrukService_compcache.md) (witch is another Uruk service) or SWAP memory in file. Third method involves creating separate swap partition - but it's considered faster then "SWAP in file" way.

If you are unsure what type is the best for you, I would recommend to start with [CompCache](UrukService_compcache.md) (at about 64MBs of cache for example). If it won't be enough for you - then use SWAP in file and perhaps later (when you'll be sure that's SWAP memory suits you) - SWAP memory on separate partition - for better performance.

# How to enable SWAP service #

Like in every Uruk service, enable it by editing configuration file and changing "service\_enabled" from 0 to 1.

## SWAP in file ##

By default, when this service is enabled, it tries to use SWAP file on rootfs.
Those two parameters control size (in MiB) and location of SWAP file.
```
 swap_mem_size=50
 swap_mem_file=/swap01.file
```

## SWAP on partition ##

You need to edit partition location (make sure device exist, and is swap initialized with "mkswap" command line utility).
```
 swap_mem_partition=/dev/block/mmcblk1p4
```

# Configuration file #
**Location:** /etc/uruk.conf/swap

**Configuration options:**
  * swap\_mem\_size - size of SWAP file in [Mebibytes](http://en.wikipedia.org/wiki/Mebibyte). _Default: 50_
  * swap\_mem\_file - location of SWAP file. Please make sure there is enough free space to create new file of size "swap\_mem\_size". Swap file will be created and initialized automatically. _Default: "/swap01.file"_
  * swap\_mem\_partition - device that should be used as SWAP memory. This device will not be initialized (you have to do it manually - use "mkswap /dev/device") for safety reason. When this value is set, service will ignore SWAP file settings. _Default: not set_
  * swap\_mem\_swappiness - this value controls how eagerly Linux kernel will try to swap RAM objects to SWAP memory. Bigger value - more swapping, more free RAM. _Default: 50_ (min:0, max:100)