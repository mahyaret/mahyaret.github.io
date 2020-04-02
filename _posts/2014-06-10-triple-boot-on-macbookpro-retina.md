---
layout: post
title: Triple Boot on MacBookPro Retina
date: '2014-06-10T19:28:00.002-04:00'
author: Mahyar
tags:
- Linux
modified_time: '2016-12-11T20:31:33.765-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-474577320440422048
blogger_orig_url: http://www.etedal.net/2014/06/triple-boot-on-macbookpro-retina.html
---


If you want to have Windows and Ubuntu alongside your Mac OS on your MacBookPro you should be aware of the followings:  
The only Linux distribution which has a built-in support for Mac hardware is Ubuntu. For example after installing Fedora in addition to resolution problem your wireless network card won't work initially.  
According to my experience you should **first install Windows and then Linux**. In order to install Windows it is better to use the Apple Boot Camp which automatically downloads and attache software and drivers to the Windows image and makes a bootable Windows USB for you.  
By using Disk Utility a exFAT partition for Windows and keep the remaining as free space for Linux.  
If you want just Windows alongside Mac you can restart your mac then press "option" key and then install Windows. However this doesn't work fork triple scenario then you need to install another program called `rEFInd`.  
  
  

1\. Partition the Hard Drive
----------------------------

Just launch Disk Utility, click on the laptop's hard drive and click on the Partition tab. From there the Mac OS X partition can be resized. Disk Utility allows you to create a new partition with the extra space I recommend building exFAT for Windows before intended Linux Partition, but I just left remaining as Free Space, so that it would be created by the Ubuntu installer.  
  

2\. Create the Ubuntu USB Installer
-----------------------------------

The latest stable release of Ubuntu is available at [http://www.ubuntu.com/download](http://www.ubuntu.com/download) - you'll need the 64-bit Mac (AMD64) desktop image.  
  
Instructions for creating a bootable USB stick are provided [http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/)  
  
  

3\. Install an EFI Boot Manager: rEFInd
---------------------------------------

Download the binary rEFInd zip file from [http://www.rodsbooks.com/refind/getting.html](http://www.rodsbooks.com/refind/getting.html) and unzip it by double-clicking the file in the Mac OS X Finder. You'll want to check out the [rEFInd installation instructions](http://www.rodsbooks.com/refind/installing.html), but I chose the simplest option of installing rEFInd in the Mac OS X partition. There are other possibilities, but this seemed the easiest for me to manage - especially if something went wrong.  
  
The installation needs to be done in the Terminal, by running the `install.sh` script:  
```
cd ~/Downloads/refind-bin-0.7.7   ./install.sh --alldrivers
```
  
The `--alldrivers` option installs the file system drivers for `rEFInd`, which allows the boot manager to be able to access the Ubuntu kernel files on the Linux file system. If you are upgrading from a previous installation of `rEFInd`, it will keep your existing `rEFInd` config file and copy the latest version with a different name.  
  
The script will prompt for your password so it can run with administrator privileges using sudo. Once the script has run, `rEFInd` is installed and you can see the configuration files at `/EFI/refind`.  
  
You'll need to reboot a couple of times before you can see the `rEFInd` menu appearing. We'll need to configure `rEFInd` later.  

4\. Installing Windows
----------------------
Connect your bootable USB drive that has been created by Apple Boot Camp and then install it on the partition that you previously made which is probably right after Recovery Partition (~640 mb).


5\. Installing Ubuntu
---------------------
Connect your bootable USB drive into the Macbook Pro and reboot - you should see the USB stick as an option in the rEFInd boot menu, so boot from that. In the Ubuntu installer, select the _Try Ubuntu_ option and it will take you to the Ubuntu desktop at a resolution of 2880x1800 -You're now ready to install Ubuntu. We want to do this without installing the Grub boot-loader, which would put us back into the old-world BIOS mode. To install without Grub, run the following in a terminal:  
```
ubiquity -b  
```
This will launch the installer and you can follow the instructions to install Ubuntu on the free space that we created earlier, alongside Mac OS X.

Once you are done, you can reboot into Mac OS X. You'll notice that the Ubuntu partition is not showing up in rEFInd as yet - that's what we need to fix next.
