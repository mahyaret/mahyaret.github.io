---
layout: post
title: Create a Bootable Windows 7 or 10 USB Drive in Linux
date: '2019-09-20T20:44:00.000-04:00'
author: Mahyar
tags:
- Linux
- debian
modified_time: '2019-09-21T20:13:05.204-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-2302701000234579711
blogger_orig_url: http://www.etedal.net/2019/09/create-bootable-windows-7-or-10-usb.html
---


source: [https://thornelabs.net/posts/create-a-bootable-windows-7-or-10-usb-drive-in-linux.html](https://thornelabs.net/posts/create-a-bootable-windows-7-or-10-usb-drive-in-linux.html)  
  
```  
# fdisk /dev/sdY  
``` 
create single partition type **7** plus the bootable partition  
```  
# mkfs.ntfs -f /dev/sdY1  
# ms-sys -7 /dev/sdY  
```
Finally, copy the contents of the mounted Windows 7 ISO to the mounted USB drive
```  
# mount -o loop win7.iso /mnt/iso  
# mount /dev/sdY1 /mnt/usb  
# cp -r /mnt/iso/* /mnt/usb/
```
