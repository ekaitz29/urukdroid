# Introduction #

Iptables is a user space application program that allows a system administrator to configure the tables provided by the Linux kernel firewall (implemented as different Netfilter modules) and the chains and rules it stores. [More...](http://en.wikipedia.org/wiki/Iptables)

This service just load necessary modules so iptables can work in UrukDroid. You just need to enable this service.

Application that can make use of this service is Android firewall manager - for example [DroidWall](http://code.google.com/p/droidwall/).

This implementation of iptables is missing "connection tracking" feature - that is also all NAT functionality.