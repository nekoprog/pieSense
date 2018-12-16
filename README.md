pieSense
========

OPNSense Unofficial Build for Raspberry Pi 2 B+

Setting up a build system for RPI2
==================================

Install [FreeBSD 11.2-RELEASE (i386)](https://download.freebsd.org/ftp/releases/i386/i386/ISO-IMAGES/11.2/)
on a machine with at least 25GB of hard disk (UFS partition)
and at least 4GB of RAM to successfully build armv6 image.  All
tasks require a root user.

Remove i386 BROKEN marks from qemu ports and install qemu-user-static

    # fetch https://raw.githubusercontent.com/nekoprog/pieSense/master/qemu-i368-makefile -o /usr/ports/emulators/qemu-sbruno/Makefile
    # cd /usr/ports/emulators/qemu-user-static && make -DBATCH install clean
    
Install git and u-boot

    # pkg install git u-boot-rpi2
    
Grab [OPNsense/tools](https://github.com/opnsense/tools) repositories
(overwriting standard ports and src) and make armv6 image for RPI2:

    # cd /usr && git clone https://github.com/opnsense/tools
    # cd tools
    # make update ARCH=arm:armv6
    # make base kernel ARCH=arm:armv6 KERNEL=SMP-RPI2
    # make xtools ARCH=arm:armv6
    # make packages ARCH=arm:armv6
    # make arm-3G ARCH=arm:armv6
