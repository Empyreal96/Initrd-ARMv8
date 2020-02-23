Initrd from Android x86 (Rewritten by @dk-zero-cool: https://github.com/dk-zero-cool/android-initrd)
With ARMv7 busybox. Other bins and libs were removed because it's x86 and unneeded.
Used for Grub2Lumia.
https://github.com/RedGreenBlue09/Grub2Lumia
------------------------------
What can this Initrd do?
According to the author:
- Manage partitions by letting Android deal with it. The script's job is locating the partitions and inform Android which ones to use for what purpose. It supports defining partitions using dev paths, image paths, uuid, label and possibly partlabel and partuuid whenever it is supported by the kernel being used.

So how can I manage partitions using this script?
According to the author:
- Add the following arguments to kernel parameter:

* ROOT: Partition where you store Android files. Default is auto-search for the partition that store booted kernel.
* CHRDST: Defines the path where Android's ramdisk will be mounted to. Default is /chroot. (that will become the root of Android when Initrd ends)
* SRCDST: Defines the path where the source of the partitions. Defaults to /mnt.
* RAMDISK: The ramdisk device that should be mounted to CHRDST. See Device Identifiers. Default to SRCDST/ramdisk.img.
* SYSTEM: The system device that should be mounted to CHRDST/system. See Device Identifiers. Default to SRCDST/system.img.
* DATA: The data device that should be mounted to CHRDST/data. See Device Identifiers. Defaults to tmpfs.
* CACHE: The cache device that should be mounted to CHRDST/cache. See Device Identifiers. Defaults to tmpfs.
* AUTOMOUNT: True/False (1/0). If true (1) all partitions like system, data and cache will be mounted by the boot script. Otherwise the fstab file contained within the ramdisk will be updated to match selected options.
* DEBUG: True/False (1/0). If true (1) the boot script will run in debug mode. This enables TTY support with access to the main file system (initrd) even after Android has booted. It also starts a debug terminal before Android is started.
