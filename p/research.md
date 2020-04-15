---
layout: page
title: Research
permalink: /p/research.html
---

Robotic Manipulation of Environmentally Constrained Objects Using Underactuated Hands (my PhD Project)
----------------------------

Robotics for agriculture represents the ultimate application of one of our society's latest and most advanced innovations to its most ancient and vital industry. Over the course of history, mechanization and automation have increased crop output several orders of magnitude, enabling a geometric growth in population and an increase in quality of life across the globe. As a challenging step, manipulating objects in harvesting automation is still under massive investigation in literature. Harvesting or the process of gathering ripe crops can be described as breaking environmentally constrained objects into two or more pieces at the desired locations. In this thesis, the problem of purposefully failing (breaking) or yielding objects by a robotic gripper is investigated. A failure task is first formulated using mechanical failure theories. Next, a grasp quality measure is presented to characterize a suitable grasp configuration and systematically control the failure behavior of the object. This approach combines information about the task's failure and the capability of the gripper for wrench insertion. The capability of the gripper for wrench insertion can be formulated using the friction between the object and the gripper. A new method inspired by the human pre-manipulation process is introduced to utilize the gripper itself as the measurement tool and obtain a friction model. The developed friction model is capable of capturing the anisotropic behavior of materials which is the case for most fruits and vegetables.

The limited operating space for harvesting process, the vulnerability of agricultural products and clusters of crops demand strict conditions for the manipulation process. This thesis presents a new sensorized underactuated self-adaptive finger to address the stringent conditions in the agricultural environment. This design incorporates link-driven underactuated mechanism with an embedded load cell for contact force measurement and a trimmer potentiometer for acquiring joint variables. The integration of these sensors results in tactile-like sensations in the finger without compromising the size and complexity of the proposed design. To obtain an optimum finger design, the placement of the load cell is analyzed using Finite Element Method (FEM). The design of the finger features a particular round shape of the distal phalanx and specific size ratio between the phalanxes to enable both precision and power grasps. A quantitative evaluation of the grasp efficiency by constructing a grasp wrench space is also provided.

The effectiveness of the proposed designs and theories are verified through real-time experiments. For conducting the massive experiments in real-time, a software/hardware platform capable of dataset management is crucial. In this thesis, a new comprehensive software interface for integration of industrial robots with peripheral tools and sensors is designed and developed. This software provides a real-time low-level access to the manipulator controller. Furthermore, Data Acquisition boards are integrated into the software which enables Rapid Prototyping methods. Additionally, Hardware-in-the-loop techniques can be implemented by adding the complexity of the plant under control to the test platform. The software is a collection of features developed and distributed under GPL V3.0. 

<div style="text-align: center;">
<iframe allowfullscreen="" frameborder="0" height="315" src="https://www.youtube.com/embed/yruMRA9iLS8" width="560"></iframe> <iframe allowfullscreen="" frameborder="0" height="315" src="https://www.youtube.com/embed/4XH8ZRJO_b8" width="560"></iframe>
</div>


Control Design for Grasping Convex Objects Using Cooperative Whole Arm Manipulator (my MSc project)
----------------------------------------------

This project presents a novel scale-dependent method for grasp evaluation based on so-called size ratio and the capability of the grasp to reject disturbance forces. Manipulating large objects, comparable to the robot size is considered. This is the case of a whole arm  manipulation (WAM) in which the robot arm can manipulate larger objects as the whole surface is used. In this way task-oriented information is incorporated in proposed grasp evaluation criterion. Examples are presented  to demonstrate the validity of the proposed approach.

Enveloping grasps are structured by wrapping the arms or fingers around the object. The main issue of the whole arm grasp (enveloping grasp) force analysis is that all contact forces are not actively controllable. It is also the case that there  are always sensory errors of magnitude and position of contact forces, since object can come into contact with any part of the limbs surface. Therefore, position uncertainty results to an uncertain Jacobian matrix. We derive a new optimal adaptive Jacobian controller for regulating internal forces. Optimal contact forces are shown to be regulated with the uncertain kinematical and dynamical parameters. They are updated online by parameter update law. Experimental results validate the proposed approach.

<div style="text-align: center;">
<iframe allowfullscreen="" frameborder="0" height="315" src="https://www.youtube.com/embed/VKypbjG0hBE" width="560"></iframe></div>

