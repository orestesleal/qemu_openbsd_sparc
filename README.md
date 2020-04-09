# Running OpenBSD SPARC on qemu (Linux, FreeBSD)

This will document how to run OpenBSD *SPARC* (sun4m) on [QEMU](https://www.qemu.org/ "QEMU")


**NOTE: OpenBSD's SPARC 32bit port is discontinued (latest release was 5.9). This 
document will show you in a few simple steps how to build qemu to generate the 
SPARC emulator (just that, we're not doing a full build here), get the neccesary 
files, etc. to get this port up and running. In this way you will have a OpenBSD 
SPARC VM, fun!**


# Requirements #

* [OpenBSD 5.8](https://mirror.transip.net/openbsd/5.8/sparc/install58.iso "OpenBSD 5.8/SPARC - install cd")
* [Wine sources](https://download.qemu.org/qemu-4.2.0.tar.xz "Wine 4.2.0 source")
* [FreeBSD](https://www.freebsd.org/ "FreeBSD")
* [Linux](https://distrowatch.com/ "Pick your distro as a service (PYDAAS)")

Pick *Linux* or *FreeBSD*, it's up to you.


# Getting Wine #

 * FreeBSD: $ fetch https://download.qemu.org/qemu-4.2.0.tar.xz
 * Linux: $ wget https://download.qemu.org/qemu-4.2.0.tar.xz or curl https://download.qemu.org/qemu-4.2.0.tar.xz -O

# Building Wine #

1.  For *FreeBSD*

