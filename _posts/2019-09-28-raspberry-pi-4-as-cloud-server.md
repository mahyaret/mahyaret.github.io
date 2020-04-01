---
layout: post
title: Raspberry Pi 4 as a Cloud Server
date: '2019-09-28T17:05:00.000-04:00'
author: Mahyar
tags:
- Linux
- RaspberryPi
- debian
modified_time: '2019-12-26T20:29:25.453-05:00'
thumbnail: https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s72-c/JPEG%2Bimage-51AE4A518482-1.jpeg
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-5851391133646323102
blogger_orig_url: http://www.etedal.net/2019/09/raspberry-pi-4-as-cloud-server.html
---


I've bought Raspberry Pi 4 to use it as a DaaS (Desktop as a Service). I've needed a VPN server to securely connect to when I am traveling. I've needed a Cloud Server to replace Dropbox to have unlimited space. I've needed a NAS (Network-attached storage) to share files among my laptops and computers. I've also needed a Music Player Server to manage my music files and serve as a source for my amplifier. I've also needed a media player like Apple TV to play my movies, youtube etc.  
  
In summary Raspberry Pi as:  
1. [Cloud server](http://www.etedal.net/2019/09/raspberry-pi-4-as-cloud-server.html) (this post)  
2. [VPN server](http://www.etedal.net/2019/09/raspberry-pi-4-as-vpn-server.html)  
3. [NAS](http://www.etedal.net/2019/09/raspberry-pi-4-as-nas.html)  
4. [Music server](http://www.etedal.net/2019/09/raspberry-pi-4-as-hifi-music-server.html)  
5. [Media Player](http://www.etedal.net/2019/09/raspberry-pi-4-as-media-player.html)  
  

[![](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s320/JPEG%2Bimage-51AE4A518482-1.jpeg)](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s1600/JPEG%2Bimage-51AE4A518482-1.jpeg)[![](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7w/nqE1lWjRWqMRJKxm7D4ZlJaprZXIzjthwCEwYBhgL/s200/JPEG%2Bimage-233E2BAC51FD-1.jpeg)](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7w/nqE1lWjRWqMRJKxm7D4ZlJaprZXIzjthwCEwYBhgL/s1600/JPEG%2Bimage-233E2BAC51FD-1.jpeg)

To be able to do all of the above, I think it is better to keep the original Raspbian distribution.  

I have used Nextcloud:  
I have used an external hard drive to the Raspberry Pi (rp). Since there is a chance that when you restart your rp it automatically mount external hard drive to different place it is a good idea to configure `fstab` to make sure that it always mounted on the right place. I also set static ip for rp (192.168.0.101)  
  
Installing Nextcloud:  
```
sudo apt install snapd  
sudo snap install nextcloud  
```  
Setting up the external hard drive:  
```
sudo mkdir /media/pi/cloud  
``` 
select UUID of your external hard drive:    
```
sudo blkid  
sudo emacs /etc/fstab  
```  
Use tab for each column when you add the following:  
```
UUID=YOURS /media/pi/cloud       auto    nosuid,nodev,nofail     0       0
```
  
Now reboot to see it mounts the external drive properly at the right place.  
  
Now edit the configuration file:  
```
sudo emacs /var/snap/nextcloud/current/nextcloud/config/autoconfig.php
```
  
change the data directory as:  
```
'directory' => '/media/pi/cloud'  
```
Start nextcloud:  
```
sudo snap restart nextcloud.php-fpm  
  ```

To install a Let's Encrypt SSL certificate, type:
```
cd /snap/bin  
sudo ./nextcloud.enable-https lets-encrypt  
 ``` 

If you use public dynamic dns services like noip remember to add it to config:
```
sudo emacs /var/snap/nextcloud/current/nextcloud/config/config.php
```
```
'trusted_domains' =>

 array (

 0 => '192.168.0.101',

 1 => '192.168.0.*',

 2 => 'YOURS.ddns.net',

 ),
```
  
check the directory file in the config if it is set to the right place  
```  
'datadirectory' => '/media/pi/cloud',
```
