# Introduction #

Android OS has a multimedia files SQL database. To be useful it has to be up-to-date, so every time you change something (mount Archos over usb, download something etc.) mediascanner is starting to work. This can be time a CPU consuming task and often people don't want it to run. There is no options to turn it off, that's why there is MediaScanner service.

# How mediascanner works? #

Original mediascanner can work in two ways, full media rescan (you can do it from "Settings->Repair & formating->Reset multimedia library" menu) and update scan. When doing full media scan system should use Android build in scanner, when doing update it start system level scripts to prepare list of changed files and then just re-index new/deleted files.

Update scans are much more often and this scans can be disabled by disabling UrukDroid Mediascanner service. This service won't affects full scans.

# Warning #

It is know that under some conditions mediascanner can erase some multimedia files, it happens more often when you disable Mediascanner service (people claim it has something to do with ".nomedia" files in directories). If it happens to you - enable Mediascanner service (so it should no influence on Android mediascanner)

# How to use Mediascanner service? #

If Mediascanner service is enabled (default state since UrukDroid 1.0) - scanning of your multimedia files is working as usual. If you disable this service, every update scan will end just after initial run (you will be able to see in notification area, information about updating multimedia library, but it will end without doing anything).

If you will need temporary multimedia library update, run just once (do not enable it during boot) Mediascanner service (in UrukConfig for example). Now service will allow for one update scan during next 5 minutes. You need to trigger it manually (Settings->Storage->Update multimedia library) or copy some files to trigger automatic update scan.