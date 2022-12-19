---
layout: post
title: Simulation Software
date: '2022-12-17T19:00:00.002-04:00'
author: Mahyar
tags:
- Robotics
- Python
---

# Physics Engine: Real-Time VS. High-Precision
The job of the robot controller is to convert the task specification to forces and torques at the actuators. Control strategies include motion control, force control, hybrid motion/force control, or impedance control. Which of these behaviors is appropriate depends on both the task and the environment. For carrying out any task in any environment, we need to control force or motion in the required direction. Please remember that this "or" is exclusive. In other words, if the robot imposes a motion then the environment will determine the force, and if the robot imposes a force then the environment will determine the motion. The following is the use cases according to the demands of typical robotic applications: 
# Physics Engine: Real-Time VS. High-Precision

| Opensource      | Proprietary |
| :---        |    :----:   |  
| Advanced Simulation Library      | Adams Multibody Dynamics Simulation        | 
| Blender   | Agx Dynamics        | 
