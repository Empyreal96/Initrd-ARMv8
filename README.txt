Initrd from Android x86 (Rewritten by @dk-zero-cool: https://github.com/dk-zero-cool/android-initrd)
With ARMv8 busybox. Other bins and libs were removed because it's x86 and unneeded.
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

The boot script offers several ways to identify a device (partition, image etc).

--> Device Identifiers <--
Dev Path: Regular dev path like /dev/sdb1.
File Path: Path to an image file relative to SRCDST. This can either be a gz compressed cpio file that will be extracted or a file system image that will be mounted. WARNING: Any gz compressed cpio file will be extracted to tmpfs filesystems, e.g. memory. This is fine for things like a ramdisk, but do not attempt this with a large system image. Despite the fact that it would take time to extract, it might also end up requiring all of your available memory.
UUID: Identify a partition based on it's uuid. This requires you to define the argument like DATA=UUID=<id>.
PARTUUID: Identify a partition based on it's partuuid. This requires you to define the argument like DATA=PARTUUID=<id>. WARNING: This is likely not supported by the kernel. Make sure of it's support before using it.
LABEL: Identify a partition based on it's label. This requires you to define the argument like DATA=LABEL=<id>.
PARTLABEL: Identify a partition based on it's partlabel. This requires you to define the argument like DATA=PARTLABEL=<id>. WARNING: This is likely not supported by the kernel. Make sure of it's support before using it.

You can edit my initrd image because it is not tested by me due to kernel does not load initrd.
