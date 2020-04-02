---
layout: post
title: How to install GraspIt!
date: '2015-06-29T14:28:00.000-04:00'
author: Mahyar
tags:
- Linux
- Robotics
- Ubuntu
- Grasp
- GraspIt!
modified_time: '2016-12-11T20:28:29.347-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-3821387688220099921
blogger_orig_url: http://www.etedal.net/2015/06/how-to-install-graspit.html
---


GraspIt! was created to serve as a tool for grasping research. It is a simulator that can accommodate arbitrary hand and robot designs. It can also load objects and obstacles of arbitrary geometry to populate a complete simulation world. The GraspIt! engine includes a rapid collision detection and contact determination system that allows a user to interactively manipulate a robot or an object and create contacts between them. Once a grasp is created, one of the key features of the simulator is the set of grasp quality metrics. Each grasp is evaluated with numeric quality measures, and visualization methods allow the user to see the weak point of the grasp and create arbitrary 3D projections of the 6D grasp wrench space. Here is the website: [http://www.cs.columbia.edu/~cmatei/graspit/](http://www.cs.columbia.edu/~cmatei/graspit/)  
  
If you are running Ubuntu 12 you can use this precompiled version: [https://drive.google.com/file/d/0B7S255p3kFXNSmFLREd6dWdDOVk/view?pli=1](https://drive.google.com/file/d/0B7S255p3kFXNSmFLREd6dWdDOVk/view?pli=1)  
  
If you want to compile it on Ubuntu 12 use the following commands:  
```  
cd Graspit/qhull/ && make && sudo make install && exit  
cd /usr/local/include/  
sudo ln -s libqhullcpp/\* ./  
sudo ln -s libqhull/\*.h ./  
cd Graspit/ && qmake graspit.pro && make  
```  
You will of course first have to install the prerequisites,  
  
Using graspit :
```  
cd /usr/lib/  
sudo cp /usr/local/lib/libqhull.so.6.3.1 ./  
sudo ln -s libqhull.so.6.3.1 libqhull.so && exit  
cd Graspit/bin/ && ./graspit  
```  
  
  
 You cannot build GraspIt! on Ubuntu 14, however there is a patch that can be used before compiling that fixes the incompatibility issues. Here is the patch:  
[https://gist.github.com/potpath/03a96d3321e719fbae1c#file-graspit-patch](https://gist.github.com/potpath/03a96d3321e719fbae1c#file-graspit-patch)
