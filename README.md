# Running OpenBSD SPARC on QEMU (for Linux and FreeBSD)

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


1. **tar -Jxvf qemu-4.2.0.tar.xz**
2. **cd qemu-4.2.0**
3. **export PREFIX=/usr/local/wine-4.2.0/**
4. **./configure --prefix=$PREFIX --target-list=sparc-softmmu** if you see an 
   error here it's probably because your system is missing of some development packages
5. For *Linux* use make (**Add -jN where N is the number of cpu cores you have**) and
   for *FreeBSD* use **gmake** (this can be installed with **pkg install gmake**)
6. Then if the build was successful use *make install* (Linux) or *gmake install* (FreeBSD)


# Testing QEMU SPARC #

1. Execute: */usr/local/qemu-4.2.0/bin/qemu-system-sparc* 
   You should see the window and the *OpenBIOS* output


#  


