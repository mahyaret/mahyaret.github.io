---
layout: post
title: Skype problem with Camera in Linux
date: '2018-10-21T23:53:00.000-04:00'
author: Mahyar
tags:
- Linux
- debian
modified_time: '2018-10-21T23:53:11.245-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-7570979352333025197
blogger_orig_url: http://www.etedal.net/2018/10/skype-problem-with-camera-in-linux.html
---


Suppose your webcam is in `/dev/video0`.  
  
  
1. `sudo apt-get install v4l2loopback-dkms`  
  
2. `sudo modprobe v4l2loopback`  
  
3. Finally, when you need your webcam on Skype, just run this command:  
  
  ```
    ffmpeg -i /dev/video0 -vcodec rawvideo -pix\_fmt yuv420p -threads 0 -f v4l2 /dev/video1
  ```  
