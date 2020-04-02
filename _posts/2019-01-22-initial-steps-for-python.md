---
layout: post
title: Initial Steps for Python
date: '2019-01-22T06:53:00.001-05:00'
author: Mahyar
tags:
- Jupyter
- Python
- debian
modified_time: '2019-01-22T06:55:31.652-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-5070432421912848701
blogger_orig_url: http://www.etedal.net/2019/01/initial-steps-for-python.html
---


Change python version system-wide
---------------------------------

This page has a great explanation for switching between Python and Python3:  
[https://linuxconfig.org/how-to-change-from-default-to-alternative-python-version-on-debian-linux](https://linuxconfig.org/how-to-change-from-default-to-alternative-python-version-on-debian-linux)  
  
```
sudo update-alternatives --config python
```

Installing Jupyter
------------------

Since in Python 3, ConfigParser has been renamed to configparser I switched to Python using:  
Then for installing and running a Notebook:
```
sudo apt-get install python-setuptools
sudo easy_install pip
sudo pip install notebook
jupyter notebook
```
