# Introduction #

Since UrukDroid 1.0 there is a boot menu called "Rescue Menu". It's operating during early boot process - before any Android specific features are run. It's designed to allow boot other operating systems, restore "bare metal" backups etc.


# Entering menu #

To enter Rescue Menu, you need to press any volume button after "Archos" logo is gone (there is few seconds window to do that). To be precise, best moment to do that is during "Waiting for external devices" message. You can push volume button multiple times of course (it won't harm). If you succeed you should see message "Rescue menu initialized...", and shortly after you should see menu itself.

You can also create file "/rescue-boot.lock" - next reboot will end in Rescue Menu.

Last (but not least) you can use UrukConfig option "Reboot to rescue menu" (requires UrukConfig 1.1 later then 16.06.2011) and UrukDroid 1.1RC1+