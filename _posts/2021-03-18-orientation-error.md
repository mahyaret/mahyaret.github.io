---
layout: post
title: Orientation Error
date: '2021-03-18T19:00:00.002-04:00'
author: Mahyar
tags:
- Robotics
- Python
---

# Robot Control
The job of the robot controller is to convert the task specification to forces and torques at the actuators. Control strategies include motion control, force control, hybrid motion/force control, or impedance control. Which of these behaviors is appropriate depends on both the task and the environment. For carrying out any task in any environment, we need to control force or motion in the required direction. Please remember that this "or" is exclusive. In other words, if the robot imposes a motion then the environment will determine the force, and if the robot imposes a force then the environment will determine the motion. The following is the use cases according to the demands of typical robotic applications: 

1) Standard industrial application: 
* pre-programmed task 
* external interface (if any) only necessary for synchronization

2) Advanced industrial application with non-continuous feedback control: 
    * pre-programmed task 
    * external sensors, but only discrete measurements 
    * no continuous feedback control (“look-then-move”) 
    * industrial controller does path planning, interpolation, inverse kinematics, etc.
    * simple interface sufficient (exchange of data without real-time requirements)
    * real-time / non-real-time vs. (non-)continuous are two different issues

3) Advanced industrial application with continuous feedback control: 
    * pre-programmed task 
    * external sensors used for feedback control 
    * examples: cameras, FT sensor, … 
    * major part of the application is programmed on an industrial controller
    * sensor data processing is programmed outside robot controller
    * low cycle time and minimal dead time of feedback control are important for sensor-based control? real-time interface: exchange of data in fixed time intervals (e.g., interpolation cycle time)

4) Research outside the robotics field: 
    * robot is used for research outside the field of robotics, e.g., the robot is used to automate measurements 
    * use cases 1-3 are applicable

5) Robotics research – system/application level: 
    * robot is used as part of a larger system to realize and evaluate new applications in the area of cognitive systems, service robotics, etc.
    * integration of robot controller in other systems should be easy
    * functionality of robot controller should be controllable from outside

6) Robotics research – control level: 
    * robot is used to implement and evaluate new robotics algorithms in the area of control, e.g., inverse kinematics, dynamics, force control, …
    * robot control at the low level (real-time constraints)

7) Robotics research – haptics: 
    * robot is used as a haptic input device (e.g., for virtual reality) or slave for telepresence systems; high sensitivity for force control (< 10 N)
    * control of robot systems at the lowest level possible (real-time constraints)

It is typically assumed in the robotics literature that there is direct control of the forces or torques at robot joints, and the robot's dynamics transforms those controls into joint accelerations. In some cases, however, we can assume that there is direct control of the joint velocities, for example when the actuators are stepper motors. There is an important property that states the mapping from joint (torque) control inputs to joint velocity is passive implying  that  passive  feedback τ=−p q, p >0, renders the robot stable in the sense of Lyapunov. Usually, robot-control engineers are not supposed to rely on the velocity-control modes of off-the-shelf amplifier for electric motors, because these velocity-control algorithms do not make use of a dynamic model of the robot. This allows the robot-control engineer to use a dynamic model of the robot in the design of the control law. It is important however that users educate themselves about the features of the system they have at hand so that they do not re-invent the wheel. One example of a very capable robot is the FrankaEmika robot which by using the open-source C++ interface, you can send real-time control values at 1 kHz with 5 different interfaces:
Gravity & friction compensated joint level torque commands.
Joint position or velocity commands.
Cartesian pose or velocity commands.

In a way, a position controller, a velocity controller, and an acceleration (torque) controller are all different implementations of each other because each is the integral of the next. Where these differ is how you apply the controller. This typically depends on what you're interested in. Keep in mind that second order effects are notoriously difficult to control. If you need Torque Control it's probably because you want to control Torque as a first order effect. You don't want your robot to start dropping things because someone decided that it should be able to run a bit faster. With a bit oversimplification, each mode uses the commanded method as its PRIMARY form of control, and it has control of the other parameters only by way of limitation. You can use a POSITION MOVE with LIMITS on the torque and velocity. the controller will do its best to get to that position within the limits provided but makes no effort to meet anything specified by the velocity or torque limits. Therefore, you could get to your commanded position with a speed of 10m/sec even though your limit was set at 40m/sec. Whatever mode you command in, the move will attempt to meet those criteria first and will ignore the other two (aside from limits). If VELOCITY is the most important thing you need to control, such as a conveyor then you use Velocity Mode. If Torque is important, such as not tearing a web or over-tensioning something, then use Torque Mode. 

The difference between VELOCITY mode and POSITION mode is a bit confusing. Arguably, you could control a conveyor using POSITION MOVES and simply setting limits on how much velocity the movement command can use. Eventually, after getting up to speed, your conveyor will be moving at the velocity specified in your POSITION MOVE. However, if you need to adjust your speed a bit, a POSITION MOVE makes this difficult. You now have to find a new position to move to and either increase or decrease the limit on your "speed max". This would be much easier if you are just using VELOCITY control, as the position of a conveyor is essentially cyclic and infinite. You can simply adjust up or adjust down the velocity of your velocity command, and you DON'T REALLY CARE where the position of the conveyor is. Namely, velocity is important but the position isn't. In another application, if you're interested in grasping an egg using a robot, your torque control cares about keeping the torque at a specific value, but it doesn't care where the position of the gripper is, or what the velocity is. 

That being said, traditional industrial robots are only able to be controlled by joint positions. Since the robotics market is still dominated by traditional robots, you should consider the available options for control commands and design your controller accordingly. The research/automation groups that are concerned with use cases 5-7 are the ones who want to control the robot at the lowest level possible. It is interesting to see that some users intend to improve or research algorithms that are already quite mature and integrated into the robot controllers, such as standard motion control algorithms or more advanced ones, such as vibration damping. Nevertheless, traditional industrial robots which are good sources of velocities due to their high gear ratios. They are not able to read the forces of the environment and are only able to be controlled by joint positions. Since the robotics market is still dominated by traditional robots, it is important to consider use case implementation for traditional ones.

One of the fundamental requirements for the success of a contact-rich task (use case 5-7) is the capacity to handle the interaction between manipulator and environment. The quantity that describes the state of interaction more effectively is the contact force at the manipulator’s end-effector. As mentioned before, most common industrial robots are joint-position-controlled. For this type of robot, compliance control is necessary to safely attempt contact-rich tasks, or the robot is prone to causing large unsafe assembly forces even with tiny pose (position and orientation) errors.

# Orientation Representation

To completely describe the pose of a rigid object in a 3-dimensional world we need 3 numbers for positions and 3 numbers for orientation. If we increase the value of one of the position dimensions the object will move continuously in a straight line, but if we increase the value of one of the orientation dimensions the object will rotate in some way and soon get back to its original orientation – this dimension is curved. We need to treat the position and orientation dimensions quite differently.

Euler’s rotation theorem requires successive rotation about three axes such that no two successive rotations are about the same axis. There are two classes of rotation sequence: Eulerian and Cardanian, named after Euler and Cardano respectively. The Eulerian type involves repetition, but not successive, of rotations about one particular axis: XYX, XZX, YXY, YZY, ZXZ, or ZYZ. The Cardanian type is characterized by rotations about all three axes: XYZ, XZY, YZX, YXZ, ZXY, or ZYX. It is common practice to refer to all 3-angle representations as Euler angles but this is underspecified since there are twelve different types to choose from. The particular angle sequence is often a convention within a particular technological field.

The ZYZ sequence is commonly used in aeronautics and mechanical dynamics. Another widely used convention is the Cardan angles: roll, pitch, and yaw. Confusingly there are two different versions in common use. Textbooks seem to define the roll-pitch-yaw sequence as ZYX or XYZ depending on whether they have a mobile robot or robot arm focus. When describing the attitude of vehicles such as ships, aircraft, and cars the convention is that the x-axis points in the forward direction and the z-axis points either up or down. It is intuitive to apply the rotations in the sequence: yaw (direction of travel), pitch (elevation of the front with respect to horizontal), and then finally roll (rotation about the forward axis of the vehicle). This leads to the ZYX angle sequence. When describing the attitude of a robot gripper, the convention is that the z-axis points forward and the x-axis is either up or down. This leads to the XYZ angle sequence. unit quaternions are also commonly used to represent rotations (or orientation of rigid bodies). 

In any case, rigid-body dynamics require integration of orientation over time. The advantages of unit quaternions are that they are compact, just 4 numbers. Additionally, mulltiplication involves fewer operations and is therefore faster. Also numerical errors build up when we multiply rotation matrices together many times, and they lose the structure (the columns are no longer unit length or orthogonal). Correcting this, the process of normalization is expensive. For unit quaternions errors will also compound, but normalization is simply a matter of dividing through by the norm.


# Orientation Error
