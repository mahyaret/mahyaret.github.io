---
layout: post
title: How to settup HTTP Proxy server in Ubuntu
date: '2015-12-21T11:47:00.000-05:00'
author: Mahyar
tags:
- Linux
- Network
- Ubuntu
modified_time: '2016-12-11T20:26:10.794-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-5613456245898559298
blogger_orig_url: http://www.etedal.net/2015/12/how-to-settup-http-proxy-server-in.html
---


Squid - Proxy Server
====================

Squid is a full-featured web proxy cache server application which provides proxy and cache services for Hyper Text Transport Protocol (HTTP), File Transfer Protocol (FTP), and other popular network protocols. Squid can implement caching and proxying of Secure Sockets Layer (SSL) requests and caching of Domain Name Server (DNS) lookups, and perform transparent caching. Squid also supports a wide variety of caching protocols, such as Internet Cache Protocol (ICP), the Hyper Text Caching Protocol (HTCP), the Cache Array Routing Protocol (CARP), and the Web Cache Coordination Protocol (WCCP).

The Squid proxy cache server is an excellent solution to a variety of proxy and caching server needs, and scales from the branch office to enterprise level networks while providing extensive, granular access control mechanisms, and monitoring of critical parameters via the Simple Network Management Protocol (SNMP). When selecting a computer system for use as a dedicated Squid caching proxy server for many users ensure it is configured with a large amount of physical memory as Squid maintains an in-memory cache for increased performance. 

1. `sudo apt-get install squid3` 

2. `sudo nano /etc/squid3/squid.conf`

3. simply find the following line and change `deny` to `allow`. This not the best way to allow accesses so if you are curious for better ways of doing it use this url: [https://www.digitalocean.com/community/tutorials/how-to-install-squid-proxy-on-ubuntu-12-10-x64](https://www.digitalocean.com/community/tutorials/how-to-install-squid-proxy-on-ubuntu-12-10-x64)
```
 http_access deny all  
```
4. `sudo service squid3 restart`

remember to forward the `port 3128` in your router to the server ip address.
