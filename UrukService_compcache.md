# Introduction #

This service enables use of another type of [SWAP memory](UrukService_SWAP.md). This may sounds weird, but this type of SWAP is located in RAM.
As a matter of facts [CompCache](http://code.google.com/p/compcache/) creates compressed part of RAM and address it as a SWAP memory. It makes sense since quite good compression (zlib) method is still much faster then writing to disk. The compression ratio is about 1:3 (so storing 32MB of CompCache SWAP will use in real RAM only 8MB). Since CompCache does not reserve any memory in advance, you don't loose RAM until it's required to be use for swapping.

So enabling 64MiB of CompCache SWAP memory will add 66MiB of SWAP memory to system, but at very worst case scenario consume about 22MiB of RAM. So we still "gain" 44MiB. I wrote "gain" because it is not RAM and can't be addressed directly. So it's only solution for small memory shortage, or can be used together with SWAP to disk memory (this two services can be enabled simultaneously). In this case, faster CompCache will be used as a first sort of SWAP memory, when totally used, system will try to use slower SWAP disk memory.

# How to enable CompCache service #

You need only enable it like every UrukService. You may want to although change it size in configuration file.

# How to use it with SWAP service #

You can use CompCache service with [SWAP service](UrukService_SWAP.md). In this method system will use all CompCache memory, and later (it there will be such a need) slower SWAP (file of partition) memory. This can be quite smart way of using this both services.

# Special options #

This service has build in some statistics subsystem. To see how CompCache memory is used you can use "stats" argument.

```
root@urukdroid:/etc/uruk.d# ./compcache stats
DiskSize:	   32768 kB
NumReads:	     468
NumWrites:	    4726
FailedReads:	       0
FailedWrites:	       0
InvalidIO:	       0
NotifyFree:	     470
ZeroPages:	     260
GoodCompress:	      63 %
NoCompress:	      18 %
PagesStored:	    3997
PagesUsed:	    1735
OrigDataSize:	   15988 kB
ComprDataSize:	    6864 kB
MemUsedTotal:	    6940 kB
```


# Configuration file #

**Location:** /etc/uruk.conf/compcache

**Configuration options:**
  * compcache\_memkb - size of CompCache SWAP memory in KiB. _Default: 32768_ (32Mib)
  * compcache\_swappiness - this value controls how eagerly Linux kernel will try to swap RAM objects to SWAP memory. Bigger value - more swapping, more free RAM. _Default: 50_ (min:0, max:100). When used together with [SWAP service](UrukService_SWAP.md) - this value will be overwritten.