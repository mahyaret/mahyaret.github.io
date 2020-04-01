---
layout: post
title: How to recover a shell after a disconnection?
date: '2019-04-07T16:45:00.000-04:00'
author: Mahyar
tags:
- ssh
- Linux
- shell
- tmux
modified_time: '2019-04-07T16:55:49.377-04:00'
thumbnail: https://4.bp.blogspot.com/-Jn2tg1dS8Ws/XKpjpYnJD-I/AAAAAAAAA5E/h6InT2rB0Z8E6mDUGSolyXE0kkZbcAIDQCLcBGAs/s72-c/Screen%2BShot%2B2019-04-07%2Bat%2B4.54.13%2BPM.png
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-6510283051212975132
blogger_orig_url: http://www.etedal.net/2019/04/how-to-recover-shell-after-disconnection.html
---


[![](https://4.bp.blogspot.com/-Jn2tg1dS8Ws/XKpjpYnJD-I/AAAAAAAAA5E/h6InT2rB0Z8E6mDUGSolyXE0kkZbcAIDQCLcBGAs/s320/Screen%2BShot%2B2019-04-07%2Bat%2B4.54.13%2BPM.png)](https://4.bp.blogspot.com/-Jn2tg1dS8Ws/XKpjpYnJD-I/AAAAAAAAA5E/h6InT2rB0Z8E6mDUGSolyXE0kkZbcAIDQCLcBGAs/s1600/Screen%2BShot%2B2019-04-07%2Bat%2B4.54.13%2BPM.png)
  

It is not possible! but the cure is `tmux`. I start tmux, start the operation and go on my way. If I return and find the connection has been broken, all I have to do is reconnect and type `tmux attach`  
  
For installing tmux on Mac:  
```
 brew install tmux  
```
`tmux` in the top image is running with [vtop](https://github.com/MrRio/vtop) on the top pane and [PM2](http://pm2.keymetrics.io/) on the bottom.  
Here is my `.tmux.conf`:
<script src="https://gist.github.com/mahyaret/f06d62ba4bb3f309b4187008c51343cf.js"></script>
