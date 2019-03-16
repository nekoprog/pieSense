![pieSense](https://github.com/nekoprog/pieSense/raw/master/opnsense-rpi2.jpg)

Current pieSense image status: ![ci_status](https://api.cirrus-ci.com/github/nekoprog/pieSense.svg)

Setting up a build system for RPI2
==================================

Install [FreeBSD 11.2-RELEASE (amd64)](https://download.freebsd.org/ftp/releases/amd64/amd64/ISO-IMAGES/11.2/)
on a machine with at least 25GB of hard disk (UFS partition)
and at least 4GB of RAM to successfully build armv6 image.
All tasks require a root user.

Install git, qemu-user-static, arm-gnueabi-binutils and u-boot-rpi2

    # pkg install git qemu-user-static arm-gnueabi-binutils u-boot-rpi2

Grab [OPNsense/tools](https://github.com/opnsense/tools) repositories
(overwriting standard ports and src)

    # cd /usr && git clone https://github.com/opnsense/tools
    # cd tools
    # make update
    # sed -i -e 's/${_ARCH}/arm:armv6/1' Makefile
    # sed -i -e 's/a10/rpi2/1' Makefile
    
Make armv6 image for RPI2

    # make base 
    # make kernel
    # make xtools
    # make packages
    # make arm-3G
    
Your pieSense is there if successfully built

    # make print-IMAGESDIR
