---
layout: post
title: 'GCC: Linux gnu/XXX.h: No such file or directory'
date: '2014-04-30T09:19:00.001-04:00'
author: Mahyar
tags:
- Linux
- fedora 20
modified_time: '2014-04-30T09:19:30.928-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-5979077301422923808
blogger_orig_url: http://www.etedal.net/2014/04/gcc-linux-gnuxxxh-no-such-file-or.html
---


It can happen a lot when you receive a compiler error alerting for instance: `gnu/stubs-32.h: No such file`  
The best you can do is just:  
```
yum whatprovides *stubs-32.h  
yum install $RESULT
```
