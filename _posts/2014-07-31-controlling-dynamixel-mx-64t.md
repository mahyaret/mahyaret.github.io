---
layout: post
title: Controlling Dynamixel MX-64T using Arduino
date: '2014-07-31T19:29:00.000-04:00'
author: Mahyar
tags:
- Arduino
- Servo Motors
modified_time: '2016-12-11T20:30:48.775-05:00'
thumbnail: https://3.bp.blogspot.com/-P9KIeplRJmc/U-Krl_NASZI/AAAAAAAAAiM/x1B7h_dyWQ8/s72-c/g4084.png
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-2900153567104176047
blogger_orig_url: http://www.etedal.net/2014/07/controlling-dynamixel-mx-64t.html
---

**MX-28T, MX-64T, MX-106T**

**Connection to UART**

To control the Dynamixel actuators, the main controller needs to convert its UART signals to the half duplex type. The recommended circuit diagrams for this are shown below.

  

[![](https://3.bp.blogspot.com/-P9KIeplRJmc/U-Krl_NASZI/AAAAAAAAAiM/x1B7h_dyWQ8/s1600/g4084.png)](http://3.bp.blogspot.com/-P9KIeplRJmc/U-Krl_NASZI/AAAAAAAAAiM/x1B7h_dyWQ8/s1600/g4084.png)

[  
](http://1.bp.blogspot.com/-hxd1kYNo4YI/U-Kp_0bSyQI/AAAAAAAAAiA/nTVtsx7Vkkw/s1600/g4084.png)

[![](https://3.bp.blogspot.com/-UbTbGF1URME/U9rRCdLDR4I/AAAAAAAAAhw/Wux0acm6Bek/s1600/Half+Duplex+UART.png)](http://3.bp.blogspot.com/-UbTbGF1URME/U9rRCdLDR4I/AAAAAAAAAhw/Wux0acm6Bek/s1600/Half+Duplex+UART.png)

  
 **Program in Arduino Uno**  
Download the latest version of Dynamixel\_Serial from [here](https://code.google.com/p/slide-33/downloads/list). Extract it to the Arduino library folder which is usually: C:\\Program Files\\Arduino\\libraries  
  
`GND` to `GND` 
`port #2` to `Data Control`  
`port #1(Tx)` to `Tx`  
`Port #0(Rx)` to `Rx`  
  
You can now run one of the example to see how it works.
