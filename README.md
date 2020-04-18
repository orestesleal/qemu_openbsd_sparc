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

1. Execute: */usr/local/qemu-4.2.0/bin/qemu-system-sparc -nographic* 

You should see the *OpenBIOS* output, like the following:

Configuration device id QEMU version 1 machine id 32
Probing SBus slot 0 offset 0
Probing SBus slot 1 offset 0
Probing SBus slot 2 offset 0
Probing SBus slot 3 offset 0
Probing SBus slot 4 offset 0
Probing SBus slot 5 offset 0
Invalid FCode start byte
CPUs: 1 x FMI,MB86904
UUID: 00000000-0000-0000-0000-000000000000
Welcome to OpenBIOS v1.1 built on Oct 28 2019 17:08
  Type 'help' for detailed information
Trying disk:a...
Trying disk...
No valid state has been set by load or init-program

0 > 

Now type: *power-off*  on the *OpenBIOS* prompt to shutdown.


# Creating the virtual disk  

1. */usr/local/qemu-4.2.0/bin/qemu-img  create -f qcow2 openbsd-sparc.disk 4G*

# Creating a configuration file to run qemu

*run-sparc.sh*

/usr/local/qemu-4.2.0/bin/qemu-system-sparc \
        -drive file=openbsd-sparc.disk,if=scsi,bus=0,unit=0,media=disk \
        -nographic \
        -drive file=install58.iso,format=raw,if=scsi,bus=0,unit=2,media=cdrom,readonly=on

Save it, make it executable (*chmod u+x run-sparc.sh*), and run the script to begin the installation.
When finish, remove the last line from the script and run your *OpenBSD* *SPARC* VM.

By default *QEMU* creates an internal network, with his own *DHCP* server, etc. and your *VM*
will have networking by using the *le* driver internally.

Output from a running vm:

# uname -a 
OpenBSD sparcfoobar.my.domain 5.8 GENERIC#0 sparc

# cc -v
Reading specs from /usr/lib/gcc-lib/sparc-unknown-openbsd5.8/4.2.1/specs
Target: sparc-unknown-openbsd5.8
Configured with: OpenBSD/sparc system compiler
Thread model: posix
gcc version 4.2.1 20070719 

# perl -v
This is perl 5, version 20, subversion 2 (v5.20.2) built for sparc-openbsd


NOTE: This will not use kernel acceleration, since on *AMD64* architectures
      anything that is not the same arch will use full emulation. With that said,
      with a normal *CPU* you will be able to use the VM without issues, install
      packages, etc.


Orestes,
April, 2020.




