# Introduction #

SSH is a network protocol that allows data to be exchanged using a secure channel between two networked devices. The two major versions of the protocol are referred to as SSH1 or SSH-1 and SSH2 or SSH-2. Used primarily on Linux and Unix based systems to access shell accounts, SSH was designed as a replacement for Telnet and other insecure remote shells, which send information, notably passwords, in plaintext, rendering them susceptible to packet analysis. The encryption used by SSH is intended to provide confidentiality and integrity of data over an unsecured network, such as the Internet. (description from [wikipedia](http://en.wikipedia.org/wiki/Secure_Shell))

SSHd service start SSH server on Uruk powered device. When this service is enabled you can:
  * connect over network to your device and work on shell like on every other Linux device. This is a best way of testing, doing low level system modification and for all error reporting
  * you can easily transfer your files to and from Uruk device without any restrictions

# How to use SSHd service #

To enable SSH server you only need to enable this service. You don't need to do anything else, but I encourage you to set some unique password (by default it's "UrukDroid") - see below.

When you enable ssh service and your device is visible in local network you can connect to it with some ssh client (for Windows machines it can be [putty.exe](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) for example).

You can also use some sftp/scp clients to transfer files to and from your Uruk device. For Windows it can be [WinSCP](http://winscp.net/eng/index.php) for example.
In both cases you need to know your Archos device current IP and use user name "root" and pre-set password "UrukDroid".

# Configuration file #
**Location:** /etc/uruk.conf/sshd

**Configuration options:**
  * SSHD\_PASS - this is field where you can set your desired ssh password. It's clear text field. _Default: "UrukDroid"_
  * SSHD\_PORT - TCP port number on which SSH daemon will listen for incoming connections. _Default: 22_
  * SSHD\_BANNER - location of text file that will be shown user after his successful login. _Default: $CONFDIR"banner.txt"_
  * SSHD\_HOME - path to user home directory (all initial script like .profilerc should be put there). _Default: "/root/"_