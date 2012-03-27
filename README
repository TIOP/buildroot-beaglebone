Buildroot for the BeagleBone
============================

This README contains basic instructions for creating a system image
for the BeagleBone using Buildroot. The image created is minimal, boots
quickly, is fairly small, but doesn't do much. Packages can easily be
added using Buildroot's "make menuconfig" configuration editor. 

Project status
--------------

March 26, 2012 - I'm in the process of sending the patches to add
BeagleBone support to buildroot upstream. As a result, I've been
negligent in keeping this project up-to-date. It works fine, but does
not have the Linux 3.2 kernel that many people are using now on the
BeagleBone. The patches that I am sending upstream do support Linux 3.2.

If you would like a version of buildroot that supports Linux 3.2, please
see [bbone-erlang-buildroot](https://github.com/nerves-project/bbone-erlang-buildroot).
It is a fairly bare-bones image with the exception that the Erlang runtime
is turned on by default. Just turn it off in "make menuconfig".

I will be posting to the beagleboard email list as soon as the upstream
buildroot project fully supports the BeagleBone.

Preparing your system
---------------------

Buildroot requires several packages to be installed on the system 
before it can work. On Ubuntu, the following apt-get line is sufficient:

sudo apt-get install git-core bison flex g++ gettext texinfo libncurses5-dev

Building
--------

Select the Buildroot configuration. Two BeagleBone configurations are
available depending on the desired C library. The uclibc system is
self-contained and builds host-side tools such as the cross-compiler. 
The glibc system requires the TI AM335x SDK to be installed and is a
work in progress. 

To select the uclibc system, run:

make beaglebone_uclibc_defconfig

To build everything, run:

make

The initial build takes a while since many packages need to be downloaded and 
built. The downloads are cached in the dl directory. Subsequent builds are
faster.

The build output is stored in the output/images directory.

Creating a BeagleBone MicroSD card
----------------------------------

The MicroSD card that comes with the BeagleBone is partitioned properly for
the BuildRoot image. To format a new MicroSD card, the following will work:

sudo sfdisk -H 255 -S 63 /dev/XXXXXX << EOF
0,9,c,*
,124
EOF
 
sudo mkfs.vfat /dev/XXXXXX -n boot

Then copy the built images to the SD Card:

# Copy the bootloads and the Linux kernel
cp MLO u-boot.img uImage /media/boot

# Copy the root file system (replace sdd2 with the second partition of right
# device)
sudo dd if=rootfs.ext2 of=/dev/sdd2 bs=128k

Notes
-----

Bring up the ethernet interface: 

# udhcp
 
