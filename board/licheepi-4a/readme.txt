Intro
=====

This directory contains a buildroot configuration for building a
LicheePi 4A.

How to build it
===============

Configure Buildroot
-------------------

  $ make licheepi_4a_defconfig

Build the boot and rootfs
----------------

Note: you will need to have access to the network, since Buildroot
will download the packages' sources.

You may now build your rootfs with:

  $ make

(This may take a while, consider getting yourself a coffee ;-) )

Result of the build
-------------------

After building, you should obtain this tree:

    output/images/
    +-- boot.ext4
    +-- rootfs.ext2
    +-- rootfs.ext4 -> rootfs.ext2
    +-- rootfs.tar
    +-- u-boot.bin
    +-- u-boot-with-spl.bin
    +-- fw_dynamic.bin
    `-- Image

How to flash the board
========================

Once the build process is finished you will have 3 images corresponding
to the 3 partitions in the eMMC of LicheePi 4A.

# fastboot flash ram u-boot-with-spl.bin
# fastboot reboot
# sleep 10
# fastboot flash uboot u-boot-with-spl.bin
# fastboot flash boot boot.ext4
# fastboot flash root rootfs.ext2

Note that the init process is /sbin/init. You might need to change
the uboot environment variables to reflect that.

