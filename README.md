Setting up a build system for RPI2
==================================

Install [FreeBSD 11.2-RELEASE (i386)](https://download.freebsd.org/ftp/releases/i386/i386/ISO-IMAGES/11.2/)
on a machine with at least 25GB of hard disk (UFS partition)
and at least 4GB of RAM to successfully build armv6 image.  All
tasks require a root user.

Install git, gcc, gmake, python, pkgconf, pixman, bison, glib and u-boot

    # pkg install git gcc gmake python pkgconf pixman bison glib u-boot-rpi2

Grab [OPNsense/tools](https://github.com/opnsense/tools) repositories
(overwriting standard ports and src)

    # cd /usr && git clone https://github.com/opnsense/tools
    # cd tools
    # sed -i -e 's/18.7/19.1/1' Makefile
    # sed -i -e 's/SMP/SMP-RPI2/1' Makefile
    # sed -i -e 's/${_ARCH}/arm:armv6/1' Makefile
    # make update

Remove i386 BROKEN marks from qemu ports and install qemu-user-static

    # sed -i -e 's/amd64 powerpc/i386 amd64 powerpc/1' /usr/ports/emulators/qemu-sbruno/Makefile
    # sed -i -e '/BROKEN_i386/d' /usr/ports/emulators/qemu-sbruno/Makefile
    # sed -i -e '/i386 host/d' /usr/ports/emulators/qemu-sbruno/Makefile
    # cd /usr/ports/emulators/qemu-user-static && make -DBATCH install clean
    
Make armv6 image for RPI2

    # make base kernel
    # make xtools
    # make packages
    # make arm-3G
    
Your pieSense is there if successfully built.

    # make print-IMAGESDIR
