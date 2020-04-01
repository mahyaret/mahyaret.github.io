---
layout: post
title: Windows Subsystem for Debian
date: '2019-03-13T11:10:00.003-04:00'
author: Mahyar
tags:
- Linux
- debian
modified_time: '2019-03-13T12:41:39.814-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-6998449994862777586
blogger_orig_url: http://www.etedal.net/2019/03/windows-subsystem-for-debian.html
---


If you're frustrated using Windows and there is no way around not using it use the following:  
[https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)  
  
Open PowerShell as Administrator:  
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Install Debian:  
[https://www.microsoft.com/en-ca/p/debian/9msvkqc78pk6?rtc=1&activetab=pivot:overviewtab](https://www.microsoft.com/en-ca/p/debian/9msvkqc78pk6?rtc=1&activetab=pivot:overviewtab)  
 ```
sudo apt update
```
