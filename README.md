BeagleBoardxM-Ubuntu-doc
========================

A reference guide to installing ubuntu 12.04 on Beagle Board xM

LINKS USED: 

1) http://elinux.org/BeagleBoardUbuntu
2) https://github.com/lzap/dancepill
   [For extracting .xz files (normally not included by default in the distro)]
   extract the package. 

=======================================================================================
METHOD>>
=======================================================================================
Download the image through "wget http://rcn-ee.net/deb/rootfs/precise/ubuntu-12.04-r1-minimal-armhf.tar.xz"


On terminal:
------------
> sudo ~/.bashrc

//add these lines 

extract () {
   if [ -f $1 ] ; then
       case $1 in
       *.tar.bz2)  tar xvjf $1 && cd $(basename "$1" .tar.bz2) ;;
       *.tar.gz)	tar xvzf $1 && cd $(basename "$1" .tar.gz) ;;
       *.tar.xz)	tar Jxvf $1 && cd $(basename "$1" .tar.xz) ;;
       *.bz2)		    bunzip2 $1 && cd $(basename "$1" /bz2) ;;
       *.rar)		    	    unrar x $1 && cd $(basename "$1" .rar) ;;
       *.gz)			    	  gunzip $1 && cd $(basename "$1" .gz) ;;
       *.tar)				  	 tar xvf $1 && cd $(basename "$1" .tar) ;;
       *.tbz2)					     tar xvjf $1 && cd $(basename "$1" .tbz2) ;;
       *.tgz)					     	 tar xvzf $1 && cd $(basename "$1" .tgz) ;;
       *.zip)						     unzip $1 && cd $(basename "$1" .zip) ;;
       *.Z)						     	   uncompress $1 && cd $(basename "$1" .Z) ;;
       *.7z)							   	      7z x $1 && cd $(basename "$1" .7z) ;;
       *)								      	 echo "don't know how to extract '$1'..." ;;
       esac
   else
       echo "'$1' is not a valid file!"
   fi
 }
source path/to/your/git/clone/e (i.e, where you extracted the package)

//now exit the file 
---------------------------
Extract image of ubuntu

insert the memorycard into PC and then through df,notedown the/dev/sdX path to media (Also format it so its freed of memory)

follow directions on link 1st (refer to line 0 of this doc)

> sudo ./setup_sdcard.sh --mmc /dev/sdX --uboot beagle_xm
(where sdX denotes your path of sd card)
 
when getting an error like : 
-----------
Are you sure? I Don't see [/dev/idontknow], here is what I do see...

fdisk -l:
Disk /dev/sda: 500.1 GB, 500107862016 bytes <- x86 Root Drive
Disk /dev/mmcblk0: 3957 MB, 3957325824 bytes <- MMC/SD card

mount:
/dev/sda1 on / type ext4 (rw,errors=remount-ro,commit=0) <- x86 Root Partition
-----------

now replace /dev/sdX in above command with /dev/sdb or whatever is shown in 2nd line after "fdisk -l" in above shown error..

>>Another error then might creep in like> missing the so and so dependencies.. then just do a simple apt-get install XYZ on on all of 'em..
For example: 

"vinay@vinay-laptop:~/ubuntu-precise-beta2-minimal-armhf$ sudo ./setup_sdcard.sh --mmc /dev/sdb --uboot beagle_xm

I see...
fdisk -l:
Disk /dev/sda: 320.1 GB, 320072933376 bytes
Disk /dev/sdb: 7948 MB, 7948206080 bytes

mount:
/dev/sda8 on / type ext4 (rw,errors=remount-ro)
/dev/sda7 on /media/b1ef4913-ae2a-4289-8860-a062dbd87ccf type ext4 (rw,nosuid,nodev,uhelper=udisks)
/dev/sdb1 on /media/beagle type vfat (rw,nosuid,nodev,uhelper=udisks,uid=1000,gid=1000,shortname=mixed,dmask=0077,utf8=1,flush)

Are you 100% sure, on selecting [/dev/sdb] (y/n)? y

Debug: ARM rootfs: armel-rootfs-201203291757.tar
Debug: image has initrd.img: HAS_INITRD=1
You're missing command mkimage (consider installing package uboot-mkimage)
You're missing command mkfs.btrfs (consider installing package btrfs-tools)
You're missing command pv (consider installing package pv)

Your system is missing some dependencies
Ubuntu/Debian: sudo apt-get install uboot-mkimage wget pv dosfstools btrfs-tools parted
Fedora: as root: yum install uboot-tools wget pv dosfstools btrfs-progs parted
Gentoo: emerge u-boot-tools wget pv dosfstools btrfs-progs parted"

=====================================================
For a full gui install run this on your beagle (make sure network is setup):

Ethernet: "sudo ifconfig -a" and "sudo dhclient usb1" or "sudo dhclient eth0"
Wireless: http://elinux.org/BeagleBoardUbuntu#Wifi_Networking_.28command_line.29

>sudo apt-get update
>sudo apt-get install xfce4 gdm xubuntu-gdm-theme xubuntu-artwork xserver-xorg-video-omap3 network-manager


=====================================================

