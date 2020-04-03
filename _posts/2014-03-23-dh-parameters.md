---
layout: post
title: DH Parameters
date: '2014-03-23T13:19:00.000-04:00'
author: Mahyar
tags:
- Robotics
modified_time: '2015-05-28T10:44:53.791-04:00'
thumbnail: http://2.bp.blogspot.com/-yglwOzZ8SpA/VWcmXegu2JI/AAAAAAAAAm4/2gpN86nXwlA/s72-c/Classic-DHparameters.png
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-138544653334753054
blogger_orig_url: http://www.etedal.net/2014/03/dh-parameters.html
---

###   There are a few rules to consider in choosing the coordinate system:

1.  the $z$-axis is in the direction of the joint axis
2.  the $x$-axis is parallel to the [common normal](http://en.wikipedia.org/wiki/Common_normal_%28robotics%29 "Common normal (robotics)"): $x_n = z_n \times z_{n - 1}$ 
    If there is no unique common normal (parallel $z$ axes), then $d$ (below) is a free parameter.
3.  the $y$-axis follows from the $x$- and $z$-axis by choosing it to be a [right-handed coordinate system](http://en.wikipedia.org/wiki/Cartesian_coordinate_system#In_three_dimensions "Cartesian coordinate system").

Once the coordinate frames are determined, inter-link transformations are uniquely described by the following four parameters:  

*   $\theta$: angle about previous $z$, from old $x$ to new $x$
*  $d$: offset along previous $z$ to the common normal
* $r$: length of the common normal (aka $a$, but if using this notation, do not confuse with $\alpha$). Assuming a revolute joint, this is the radius about previous $z$.
* $\alpha$: angle about common normal, from old $z$ axis to new $z$ axis

"Standard" DH Parameters
------------------------

Following the DH standard you must provide 4 numbers that define the orientation of the $i_{th}$ link with respect to the  $i-1_{th}$ link. "Standard" DH convention assumes that the $i_{th}$ coordinate frame is at the $i+1_ {joint}$. (joint 1 axes 0, joint 2 axes 1 ...)

[![](http://2.bp.blogspot.com/-yglwOzZ8SpA/VWcmXegu2JI/AAAAAAAAAm4/2gpN86nXwlA/s320/Classic-DHparameters.png)](http://2.bp.blogspot.com/-yglwOzZ8SpA/VWcmXegu2JI/AAAAAAAAAm4/2gpN86nXwlA/s1600/Classic-DHparameters.png)

1.  (Link parameter)($\alpha$)The first number represents the angle (in radians) between $z_{i-1}$ and $z_i$ about $x_i$.
2.  (Link parameter)($a$)The second number represents the length (in meters) along $x_i$ of the common perpendicular between $z_{i-1}$ and $z_i$.
3.  (Joint parameter)($\theta$)The third number represents the angle (in radians) between $x_{i-1}$ and $x_i$ about $z_{i-1}$.
4.  (Joint parameter)($d$)The fourth number represents the distance (in meters) along axis $z_{i-1}$ between the origin of the $i-1_{th}$ coordinate frame and the point where the common perpendicular intersects axis $z_i$

  

"Modified" DH Parameters (also called Craig's convention)
---------------------------------------------------------

Following the modified DH standard, you must provide 4 numbers that define the orientation of the $i_{th}$ link with respect to the $i-1_{th}$ link. Unlike the "standard" DH convention, the "modified" DH convention assumes that the $i_{th}$ coordinate frame is at the $i_ {joint}$. (joint 1 axes 1,joint 2 axes 2 ...)

[![](http://3.bp.blogspot.com/-0vYqCXD3c0c/VWclrHl5wdI/AAAAAAAAAmw/nW3lYqA_WVM/s320/DHParameterModified.png)](http://3.bp.blogspot.com/-0vYqCXD3c0c/VWclrHl5wdI/AAAAAAAAAmw/nW3lYqA_WVM/s1600/DHParameterModified.png)

1.  (Link parameter)($\alpha$)The first number represents the angle (in radians) between $z_{i-1}$ and $z_i$ about $x_{i-1}$.
2.  (Link parameter)($a$)The second number represents the length (in meters) along $x_{i-1}$ of the common perpendicular between $z_{i-1}$ and $z_i$.
3.  (Joint parameter)($\theta$)The third number represents the angle (in radians) between $x_{i-1}$ and $x_i$ about $z_i$.
4.  (Joint parameter)($d$)The fourth number represents the distance (in meters) between $x_{i-1}$ and $x_i$ about $z_i$.  
      
      Many people in robotics are actually unaware that there are two different conventions in use. An advantage of Craig’s convention is the proximal placement of the origin for a link. Also the rotation  $\theta_i$ is about  $z_i$ and the joint number is the same as the coordinate number, which seem more natural. Torque exerted about joint $i$ is also at the same place as at link $i$’s coordinate system, to which inertial parameters such as center of mass are likely to be referenced. A disadvantage is that the transform mixes $i−1$ and $i$ parameters. Both Craig’s convention and the standard DH convention are equally valid. The choice of one over the other is merely a matter of taste or habit.
