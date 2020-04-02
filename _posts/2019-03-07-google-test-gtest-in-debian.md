---
layout: post
title: Google Test (gtest) on Debian
date: '2019-03-07T07:18:00.000-05:00'
author: Mahyar
tags:
- Linux
- C++
- debian
modified_time: '2019-03-07T07:21:02.248-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-6903558940979679450
blogger_orig_url: http://www.etedal.net/2019/03/google-test-gtest-in-debian.html
---


Here is the link to the project source [https://github.com/google/googletest](https://github.com/google/googletest)  
  
  
Here is the code for installing Google Test (gtest)
```
sudo apt-get install libgtest-dev
```

Install `cmake`
```
sudo apt-get install cmake
```
compiling `gtest`
```
cd /usr/src/gtest
sudo cmake CMakeLists.txt
sudo make
sudo cp *.a /usr/lib
sudo mkdir /usr/local/lib/googletest
```
linking `gtest`
```
sudo ln -s /usr/lib/libgtest.a /usr/local/lib/gtest/libgtest.a
sudo ln -s /usr/lib/libgtest_main.a /usr/local/lib/gtest/libgtest_main.a
```
