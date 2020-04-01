---
layout: post
title: Raspberry Pi 4 as a VPN Server
date: '2019-09-28T17:18:00.001-04:00'
author: Mahyar
tags:
- Linux
- RaspberryPi
- debian
modified_time: '2019-11-22T09:13:31.165-05:00'
thumbnail: https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s72-c/JPEG%2Bimage-51AE4A518482-1.jpeg
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-3938998714557574870
blogger_orig_url: http://www.etedal.net/2019/09/raspberry-pi-4-as-vpn-server.html
---


I've bought Raspberry Pi 4 to use it as a DaaS (Desktop as a Service). I've needed a VPN server to securely connect to when I am traveling. I've needed a Cloud Server to replace Dropbox to have unlimited space. I've needed a NAS (Network-attached storage) to share files among my laptops and computers. I've also needed a Music Player Server to manage my music files and serve as a source for my amplifier. I've also needed a media player like Apple TV to play my movies, youtube etc.  
  
In summary Raspberry Pi as:  
1. [Cloud server](http://www.etedal.net/2019/09/raspberry-pi-4-as-cloud-server.html)  
2. [VPN server](http://www.etedal.net/2019/09/raspberry-pi-4-as-vpn-server.html) (this post)  
3. [NAS](http://www.etedal.net/2019/09/raspberry-pi-4-as-nas.html)  
4. [Music server](http://www.etedal.net/2019/09/raspberry-pi-4-as-hifi-music-server.html)  
5. [Media Player](http://www.etedal.net/2019/09/raspberry-pi-4-as-media-player.html)  
  

[![](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s320/JPEG%2Bimage-51AE4A518482-1.jpeg)](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s1600/JPEG%2Bimage-51AE4A518482-1.jpeg)[![](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7w/nqE1lWjRWqMRJKxm7D4ZlJaprZXIzjthwCEwYBhgL/s200/JPEG%2Bimage-233E2BAC51FD-1.jpeg)](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7w/nqE1lWjRWqMRJKxm7D4ZlJaprZXIzjthwCEwYBhgL/s1600/JPEG%2Bimage-233E2BAC51FD-1.jpeg)

  
To be able to do all of the above, I think it is better to keep the original Raspbian distribution.  
  
Lots of limitations can be imposed on internet access that makes it impossible to use VPN. **(Warning You Are Responsible For How You Use VPN)** Organizations can close ports that are usually used for VPN access, therefore I've decided to use port 80 which is for webpages. If port 80 is not accessible it means that the internet access is down! Another limitation can be the protocol that your VPN app uses over port 80. The protocol that is used for webpage access is TCP so I've decided to use that. All in all, with these VPN settings from the admin perspective you're accessing a webpage. I have used dynamic DNS can be used for accessing your VPN sever globally. Remember to do Port Forwarding from your router to Raspberry Pi.  
  
Install PiVPN:  
```
curl -L https://install.pivpn.io | bash  
  ```
Add user:  
```
pivpn add  
  ```
Edit `USER.ovpn` to have your Dynamic DNS address  
Send the `USER.ovpn` to the user.  
Open `USER.ovpn` using OpenVPN app
