---
layout: post
title: How to Setup a VPN (PPTP) Server on Debian Linux
date: '2015-12-22T00:54:00.000-05:00'
author: Mahyar
tags:
- Linux
- Network
- debian
modified_time: '2016-12-11T20:25:53.477-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-7981563241840025737
blogger_orig_url: http://www.etedal.net/2015/12/how-to-setup-vpn-pptp-server-on-debian.html
---


1. `sudo apt-get install pptpd`

2. `sudo nano /etc/pptpd.conf`

3. Add server IP and client IP at the end of the file. You can add like below:  
```
localip 192.168.2.100  
remoteip 192.168.2.101-200
```
localip is the ip address of the server in the network and remoteip is the range you specify for vpn clients to join your network.  

4.  `sudo nano /etc/ppp/pptpd-options`

5. Uncomment the `ms-dns` and add google like below or OpenDNS  
```
ms-dns 8.8.8.8  
ms-dns 8.8.4.4
```
6. `sudo nano /etc/ppp/chap-secrets `
```
# client        server  secret                  IP addresses  
username * myPassword *
```
7. `sudo /etc/init.d/pptpd restart` 

If you are setting your iphone to use this server set the "Encryption Level" to "Auto".

If your modem has `DMZ` setting you don't have to forward any port but in case you can forward `1723/TCP` and `47/UDP` to the server.
