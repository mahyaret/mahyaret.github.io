---
layout: post
title: Raspberry Pi 4 as a Media Player
date: '2019-09-28T18:25:00.001-04:00'
author: Mahyar
tags:
- Linux
- RaspberryPi
- debian
modified_time: '2019-12-26T20:27:47.212-05:00'
thumbnail: https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7s/G5-5gDPzFfAweo9-_B3LX6L1gc-C725ugCLcBGAsYHQ/s72-c/JPEG%2Bimage-51AE4A518482-1.jpeg
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-9183604248065051502
blogger_orig_url: http://www.etedal.net/2019/09/raspberry-pi-4-as-media-player.html
---


I've bought Raspberry Pi 4 to use it as a DaaS (Desktop as a Service). I've needed a VPN server to securely connect to when I am traveling. I've needed a Cloud Server to replace Dropbox to have unlimited space. I've needed a NAS (Network-attached storage) to share files among my laptops and computers. I've also needed a Music Player Server to manage my music files and serve as a source for my amplifier. I've also needed a media player like Apple TV to play my movies, youtube etc.  
  
In summary Raspberry Pi as:  
1. [Cloud server](http://www.etedal.net/2019/09/raspberry-pi-4-as-cloud-server.html)  
2. [VPN server](http://www.etedal.net/2019/09/raspberry-pi-4-as-vpn-server.html)  
3. [NAS](http://www.etedal.net/2019/09/raspberry-pi-4-as-nas.html)  
4. [Music server](http://www.etedal.net/2019/09/raspberry-pi-4-as-hifi-music-server.html)  
5. [Media Player](http://www.etedal.net/2019/09/raspberry-pi-4-as-media-player.html) (current post)  
  
 
[![](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7s/G5-5gDPzFfAweo9-_B3LX6L1gc-C725ugCLcBGAsYHQ/s320/JPEG%2Bimage-51AE4A518482-1.jpeg)](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7s/G5-5gDPzFfAweo9-_B3LX6L1gc-C725ugCLcBGAsYHQ/s1600/JPEG%2Bimage-51AE4A518482-1.jpeg)[![](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7o/db_7TCe7UoQYVQ6QFmzFyQZE1qH2H4tlgCLcBGAsYHQ/s200/JPEG%2Bimage-233E2BAC51FD-1.jpeg)](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7o/db_7TCe7UoQYVQ6QFmzFyQZE1qH2H4tlgCLcBGAsYHQ/s1600/JPEG%2Bimage-233E2BAC51FD-1.jpeg)

  
  
To be able to do all of the above, I think it is better to keep the original Raspbian distribution. RP 4 is much faster than other RPs however it is still too slow for playing videos in 4K. I found Kodi very slow on RP 4. VLC is performing well if you overclock CPU and GPU and set the memory for GPU higher than default. RP 4 CPU gets hot easily so in order to overclock it I bought a [small fan](https://shop.pimoroni.com/products/fan-shim) for it and since I wanted to mount ALLO DigiOne HaT on top of it I bought [pin header](https://shop.pimoroni.com/products/booster-header).  
 ```
sudo emacs /boot/config.txt  
  ```
Add the following (**warning overclocking is never recommended!**)  
  
```
over_voltage=4

arm_freq=2000

gpu_freq=600

gpu_mem=512  
```  
  
reduce your screen resolution.  
  
if you want to play a file using ssh remotely use the following:  

```  
export DISPLAY=:0  
vlc -f file.mp4  
 ``` 
to be able to control VLC remotely in preferences>>show all>>Main interfaces check Web and set a password for Lua HTTP  
  
best remote app for VLC can be found here:  
[https://hobbyistsoftware.com/VLC-more](https://hobbyistsoftware.com/VLC-more)  
  
  
If you want to control your TV using HDMI cable:  
```  
sudo apt install cec-utils  
echo 'scan' | cec-client -s -d 1  
  ```
  
for turning on the TV:  
```
echo 'on DEVICE\_NUMBER' | cec-client -s -d 1  
  ```
  
for more info: [https://www.linuxuprising.com/2019/07/raspberry-pi-power-on-off-tv-connected.html](https://www.linuxuprising.com/2019/07/raspberry-pi-power-on-off-tv-connected.html)
