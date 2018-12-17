pieSense 19.1
========

OPNSense 19.1 Unofficial Build for Raspberry Pi 2 B+

Setting up a build system for RPI2
==================================

Install [FreeBSD 11.2-RELEASE (i386)](https://download.freebsd.org/ftp/releases/i386/i386/ISO-IMAGES/11.2/)
on a machine with at least 25GB of hard disk (UFS partition)
and at least 4GB of RAM to successfully build armv6 image.  All
tasks require a root user.

Install git and u-boot

    # pkg install git u-boot-rpi2

Grab [OPNsense/tools](https://github.com/opnsense/tools) repositories
(overwriting standard ports and src)

    # cd /usr && git clone https://github.com/opnsense/tools
    # cd tools
    # make update ARCH=arm:armv6 SETTINGS=19.1

Remove i386 BROKEN marks from qemu ports and install qemu-user-static

    # sed -i -e 's/amd64 powerpc/i386 amd64 powerpc/1' /usr/ports/emulators/qemu-sbruno/Makefile
    # sed -i -e '/BROKEN_i386/d' /usr/ports/emulators/qemu-sbruno/Makefile
    # sed -i -e '/i386 host/d' /usr/ports/emulators/qemu-sbruno/Makefile
    # cd /usr/ports/emulators/qemu-user-static && make -DBATCH install clean
    
Make armv6 image for RPI2:

    # make base kernel ARCH=arm:armv6 KERNEL=SMP-RPI2 SETTINGS=19.1
    # make xtools ARCH=arm:armv6 SETTINGS=19.1
    # make packages ARCH=arm:armv6 SETTINGS=19.1
    # make arm-3G ARCH=arm:armv6 SETTINGS=19.1
