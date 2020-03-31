---
layout: post
title: 'Raspberry Pi 4 as a HiFi Music Server '
date: '2019-09-29T00:05:00.001-04:00'
author: Mahyar
tags:
- Linux
- RaspberryPi
- debian
modified_time: '2019-11-22T09:19:42.765-05:00'
thumbnail: https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s72-c/JPEG%2Bimage-51AE4A518482-1.jpeg
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-1540079348099163230
blogger_orig_url: http://www.etedal.net/2019/09/raspberry-pi-4-as-hifi-music-server.html
---


I've bought Raspberry Pi 4 to use it as a DaaS (Desktop as a Service). I've needed a VPN server to securely connect to when I am traveling. I've needed a Cloud Server to replace Dropbox to have unlimited space. I've needed a NAS (Network-attached storage) to share files among my laptops and computers. I've also needed a Music Player Server to manage my music files and serve as a source for my amplifier. I've also needed a media player like Apple TV to play my movies, youtube etc.  
  
**Note: the sound quality was not satisfying for me.**  
  
In summary Raspberry Pi as:  
1. [Cloud server](http://www.etedal.net/2019/09/raspberry-pi-4-as-cloud-server.html)  
2. [VPN server](http://www.etedal.net/2019/09/raspberry-pi-4-as-vpn-server.html)  
3. [NAS](http://www.etedal.net/2019/09/raspberry-pi-4-as-nas.html)  
4. [Music server](http://www.etedal.net/2019/09/raspberry-pi-4-as-hifi-music-server.html) (this post) (not recommended)  
5. [Media Player](http://www.etedal.net/2019/09/raspberry-pi-4-as-media-player.html)  

[![](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s320/JPEG%2Bimage-51AE4A518482-1.jpeg)](https://1.bp.blogspot.com/-1ghALR1EWSw/XY_c62WOmQI/AAAAAAAAA7w/tAey5M4DmikDlIEq9jr5fF0_U6d7kwDowCEwYBhgL/s1600/JPEG%2Bimage-51AE4A518482-1.jpeg)[![](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7w/nqE1lWjRWqMRJKxm7D4ZlJaprZXIzjthwCEwYBhgL/s200/JPEG%2Bimage-233E2BAC51FD-1.jpeg)](https://1.bp.blogspot.com/-y0W5wo3PztY/XY_c6re4fTI/AAAAAAAAA7w/nqE1lWjRWqMRJKxm7D4ZlJaprZXIzjthwCEwYBhgL/s1600/JPEG%2Bimage-233E2BAC51FD-1.jpeg)

To be able to do all of the above, I think it is better to keep the original Raspbian distribution. I have not used [Volumio](https://volumio.org/) because I have needed a full OS for doing other stuff. But if you only care about the music quality Volumio is great and it is very light weight operating system for Raspberry Pi.  
  
I have bought Allo DigiOne HaT from [here](https://www.allo.com/sparky/digione.html).  

  
![](https://www.allo.com/shop/1719-large/digione.jpg)  
  
Why such boards are needed for enhancing the sound quality for feeding into the amplifier or DAC? When you want to transfer a digital file and you don't care about the timing, it is a fairly easy task and since sound files are all zeros and ones it's going to be transferred perfectly. However, when you want to play this file on your stereo system everything should happen in real-time. Every ones and zeros should be perfectly send in the perfect intervals. In this "real-time" situations everything matters even for a digital signal which consists of zeros and ones, from quality of wire, board connections etc. Even the noise produced by cpu can interfere with transferring signals. That is why it is claimed that RP 3 has a better sound quality compare to RP 4 using same ALLO Transport board and external linear power supply ([source](https://www.youtube.com/watch?v=cjqEPyMr1zI)).  
  
You only need to mount this HaT onto you RP and add `dtoverlay=allo-digione` to boot setting:  
`sudo emacs /boot/config.txt  `
reboot your RP.
From Menu in Raspbian open `Preferences>>Audio Device Settings`
Make sure that `snd\_allo\_digione (Alsa mixer)` is selected.
Click on `Select Controls` and check `Tx Source`
Select `AIF for Tx Source` and click on  `Make Default`
Until now you configured DigiOne sound hardware.

Since I have not used Volumio I had to install MPD from scratch. A typical setup for a home network:  
- A UPnP Media Server (e.g. MinimServer, Minidlna, Mediatomb, or some commercial product),  
- A UPnP Control Point (e.g. Bubble UPnP running on a tablet or phone, Linn Kazoo on a PC/MAC, or upplay for Linux or Windows).  
- upmpdcli and MPD running on some Linux device (e.g. a Raspberry Pi hooked up to your bedroom stereo).

[![upmpdcli](https://www.lesbonscomptes.com/upmpdcli/pics/upmpdcli.png)](https://www.lesbonscomptes.com/upmpdcli/pics/upmpdcli.png)

But I have only installed MPD:  
`sudo emacs /etc/mpd.conf`
Change the directory MPD looks for music and  set MPD config as follows:  
```
audio_output {
type "alsa"
name "Allo DigiOne"
# device        "hw:0,0" 
device "hw:sndallodigione"
#       device          "hw:0,0"        # optional 
#       mixer\_type      "hardware"      # optional 
#       mixer\_device    "default"       # optional 
#       mixer\_control   "PCM"           # optional 
#       mixer\_index     "0"             # optional 
}
```
and comment the following line:  
`# user                          "mpd" `
then:
`sudo systemctl enable mpd`
`sudo systemctl start mpd`
`sudo systemctl restart mpd `
For remotely controlling MPD I have used this project:
[https://github.com/Nyx0uf/shinobu](https://github.com/Nyx0uf/shinobu)
