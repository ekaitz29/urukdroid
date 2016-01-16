

# Introduction #

Since our Android/Linux is [multitasking](http://en.wikipedia.org/wiki/Computer_multitasking) capable, CPU needs to share it's cycles to more then one running task. This is a job for "CPU governor".

Linux has few default governors like performace, ondemand, powersafe. With UrukDroid there is one more called interactive - this CPU governor was made by people from CyanogenMOD.

To set desired governor you should use this service (this can be done by many more applications from market - but not with all available options).

# Special options #

With cpugovernor service you can see some low level CPU statistics. It's quite useful for performance/battery draining tuning - and debugging of course.
```
[root@urukdroid uruk.d]# ./cpugovernor stats
Uruk-CPUGovernor statistics:
	Current governor: interactive
	Overclock module: Enabled
		Current max vsel: 68
		Current max rate: 1100000
	CPU Max: 1100000
	CPU Min: 300000
	Available frequencies: 1100000 800000 600000 300000 
CPU statistics (tick spend in every frequency range): 
	1.1 GHz had 	5207 ticks 	(30.28%)
	800 MHz had 	317 ticks 	(1.84%)
	600 MHz had 	7090 ticks 	(41.23%)
	300 MHz had 	4584 ticks 	(26.66%)
```
You can see here current CPU governor, min/max CPU frequencies (used by governor - this are not hardware min/max), available CPU frequencies and table with CPU frequency and number of ticks CPU spend with this clock value.
In this case CPU mostly works on 300Mhz (56.49%), 600Mhz (28.65%), 800Mhz (0.93%) and 1Ghz (13.95%).

# Overclocking #

**Warning!** Although overclocking usually cannot harm your hardware it's really easy to make device unstable, and corrupt your data on disk drive. You should be also aware that overclocking may not work on your device AT ALL.

Since UrukDroid 1.6 (RC3 exactly) there is build in overclocking kernel module ([Milestone overclock](http://code.google.com/p/milestone-overclock/)). Basic settings are available through CPUGovernor service.

In configuration file, you can enable overclocking module and set max. CPU frequency.

## How to enable overclocking? ##

First, you should do rootfs backup (from Uruk RescueMenu) - in case if your device became unbootable or corrupted (see below), you can restore old config.

You may want to take a look at [overclocking topic on XDA](http://forum.xda-developers.com/showthread.php?t=1373354) (to see values, ask questions).

Then enable in CPUGovernor config file overclocking:
```
# Overclock
# 0 = disabled, 1 = enabled
enable_overclock=1
```
This will NOT overclock your CPU, it will just enable overclocking (it will load overclock.ko kernel module) - this step is quite safe, so you can enable it in configuration file (but remember - this is safe on kernel prepared for this module, if you use other kernel - see below).

If this steps fails, you can disable overclocking from RescueMenu.

Reboot your device and check if overclocking is running
```
[root@urukdroid root]# /etc/uruk.d/cpugovernor stats
Uruk-CPUGovernor statistics:
        Current governor: interactive
        Overclock module: Enabled
```

If its enabled - your are good to go to next step. Now you should check manually (without putting it to configuration file) what values are good for you. You need to specify MAX CPU frequency and voltage.

```
echo 66 > /proc/overclock/max_vsel
echo 1100000 > /proc/overclock/max_rate
```

First value is voltage, second on is CPU frequency in hz. If you find some stable values, you can set them up in configuration file:
```
# Overclock settings
max_vsel=68
max_rate=1100000
```

Higher vsel = higher voltage.

To calculate voltage: **max\_vsel\*12,5 + 600 = real mV**

Default value for 1Ghz is 60 (1,35V).

## How do I know if overclocking is working properly? ##

When you enable overclocking you device may became unstable (this means you should give bigger voltage or lower frequency). Device can be unstable on many ways:
  * freezes - when you device stops to respond after loading overclock, your values are wrong (for your device). Usually it also says your values are far from proper ones.
  * reboots - your device works for some time after applying overclock, but reboots without any reason after a while. You are closer then before - but far from ok.
  * force close apps. - your application are force closing from time to time - there are some memory/cpu errors, so you orverclocking settings are still not good enough - but you are close.
  * data corruption - when you download a movie and you see errors, or when you download application from market and it cannot install (says that file is corrupted) - like in force close errors, you have some memory/cpu problems.


## How to adjust overclock configuration for other kernels? ##

Overclock module options are configured for exact kernel. If you want to use older/newer/other kernel you need to reconfigure it.

Kernel module options settings are located in /etc/modprobe.d/ directory:
```
[root@urukdroid misc]# ls /etc/modprobe.d/
aliases.conf    dvb.conf        overclock.conf
```

First to need to find proper values for autoconfiguration (memory addresses)
```
[root@urukdroid uruk.d]# grep omap2_clk_init_cpufreq_table /proc/kallsyms
c005d2f0 T omap2_clk_init_cpufreq_table
[root@urukdroid root]# grep cpufreq_stats_update /proc/kallsyms
c02a6240 t cpufreq_stats_update
[root@urukdroid uruk.d]# cd /lib/modules/2.6.29-omap1/misc/
[root@urukdroid misc]# insmod overclock.ko omap2_clk_init_cpufreq_table_addr=0xc005d2f0 cpufreq_stats_update_addr=0xc02a6240
[root@urukdroid misc]# dmesg | tail -2
overclock: found mpu_opps_addr at 0xc04ab5bc
overclock: found cpufreq_stats_table_addr at 0xc04bfc68
```
First we search in kernel symbols for address of **omap2\_clk\_init\_cpufreq\_table** and **cpufreq\_stats\_update**. Then we load overclock kernel module with autodetect option and found memory address **0xc005d2f0** and **0xc02a6240**. As a result, in dmesg we can see (**0xc04ab5bc** and **0xc04bfc68**) proper memory address - so everything works ok. We could use this new address, but this is less safe - so we stick to auto-detect of overclock module, and use "grep" values.

The only line in overclock.conf (only uncommented) should look like this:
```
options overclock omap2_clk_init_cpufreq_table_addr=0xc005d2f0 cpufreq_stats_update_addr=0xc02a6240
```

Since UD 1.6RC6 there is an auto-generate option in cpugovernor:
```
[root@urukdroid root]# /etc/uruk.d/cpugovernor genconf
options overclock omap2_clk_init_cpufreq_table_addr=0xc005d2ec cpufreq_stats_update_addr=0xc02a76e0
```
Theoretically it should be enough to redirect it's output to modprobe config file like this:
```
[root@urukdroid root]# /etc/uruk.d/cpugovernor genconf >/etc/modprobe.d/overclock.conf
```
But it's not recommended to do it blindly - you should check if output parameters are reasonable.

# Configuration file #

**Location:** /etc/uruk.conf/cpugovernor

**Configuration options:**
  * cpu\_governor - name of CPU governor (can be any one from Linux available). _Default: interactive_
  * cpu\_governor\_default - name of CPU governor used when this service is disabled/stopped. _Default: ondemand_
  * cpu\_freq\_max/cpu\_freq\_min - if you want to narrow down range of frequencies that CPU governor will use - set this option. You can choose only values from "Available frequencies" (see ./cpugovernor stats). _Default: ""_ (not set)
  * enable\_overclock - enable overclock kernel module. _Default: 0_
  * max\_vsel - CPU maximum voltage, works only if overclock enabled. _Default: 68_
  * max\_rate - CPU maximum frequency rate (Hz), works only if overclock enabled. _Default: 1100000_