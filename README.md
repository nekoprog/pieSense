pieSense
========

OPNSense Unofficial Build for Raspberry Pi 2 B+

Setting up a build system for RPI2
==================================

Install [FreeBSD 11.1-RELEASE (i386)](https://download.freebsd.org/ftp/releases/i386/i386/ISO-IMAGES/11.1/)
on a machine with at least 25GB of hard disk (UFS partition)
and at least 4GB of RAM to successfully build armv6 image.  All
tasks require a root user.  Do the following to grab the repositories
(overwriting standard ports and src) and make armv6 image for RPI2:

    # pkg install git
    # ln -sv /usr/local/bin/perl5.26.* /usr/local/bin/perl5.26.0
    # fetch https://raw.githubusercontent.com/nekoprog/pieSense/master/qemu-i368-makefile -o /usr/ports/emulators/qemu-sbruno/Makefile
    # cd /usr/ports/emulators/qemu-sbruno && make -DBATCH install clean
    # cd /usr && git clone https://github.com/opnsense/tools
    # cd tools
    # make update
    # make base kernel ARCH=arm:armv6 KERNEL=SMP-RPI2
    # make xtools ARCH=arm:armv6
    # make packages ARCH=arm:armv6
    # pkg install u-boot-rpi2
    # make arm-3G ARCH=arm:armv6
