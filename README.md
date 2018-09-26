# fpga-images-zcu102

First, prepare the SD card (https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_1/ug1157-petalinux-tools-command-line-guide.pdf)

An SD memory card with at least 4 GB of storage space. It is recommended to use a
card with speed-grade 6 or higher to achieve optimal file transfer performance.

Steps to prepare the SD card for PetaLinux SD card ext filesystem boot:

1. The SD card is formatted with two partitions using a partition editor such as gparted.

2. The first partition should be at least 60 MB in size and formatted as a FAT32 filesystem.
Ensure that there is 4 MB of free space preceding the partition. The first partition will
contain the bootloader, devicetree and kernel images. Label this partition as BOOT.

3. The second partition should be formatted as an ext4 filesystem and can take up the
remaining space on the SD card. This partition will store the system root filesystem.
Label this partition as rootfs.

Second, copy image files to SD card partitions (make load-sd).

1. Copy BOOT.BIN and image.ub to BOOT partition of SD card. The image.ub file will
have device tree and kernel image files.
$ cp images/linux/BOOT.BIN /media/BOOT/
$ cp images/linux/image.ub /media/BOOT/

2. Copy rootfs.cpio file to rootfs partition of SD card and extract the file system.
$ cp images/linux/rootfs.cpio /media/rootfs/
$ cd /media/rootfs
$ sudo pax -rvf rootfs.cpio
