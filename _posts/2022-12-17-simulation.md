---
layout: post
title: Simulation
date: '2022-12-17T19:00:00.002-04:00'
author: Mahyar
tags:
- Robotics
- Python
---


In this post, I am going to present the different physics engines that are available for engineering applications. I'll talk about what are different simulation types and applications. I'll introduce the rigid-body simulation techniques. I'll mention what simulations are suitable for Reinforcement Learning (RL). Additionally, I'll mention issues with most Physics Engines and what kind of experimental verification can be done to quantify these issues.

# Physics engine: Real-Time VS. High-Precision
Here is a list of different types of simulation engines:


|Real-time | |High-Precision |
| :-     |    :-   |  :- |
| **Opensource**      | **Proprietary** | Solidworks |
| Advanced Simulation Library      | Adams Multibody Dynamics Simulation        |  ANSYS |
| Blender   | Agx Dynamics        | ABAQUS |
|Box2D|NovodeX|VisSim|
|Bullet (AMD)|Renderware Physics|Working Model|
|MuJoCo|SIMPACK|COMSOL|
|Chipmunk physics engine|Vortex Dynamics||
|DART|Havoc (Intel)|||
|FleX (Nvidia only on GPU)|||
|Newton Game Dynamics|||
|Open Dynamics Engine|||
|PAL (Physics Abstraction Layer) |||
|PhysX (Nvidia)|||
|Project Chrono |||
|Siconos|||
|SOFA (Simulation Open Framework Architecture)|||
|Tokamak|||



# Simulation types and applications
- Frequency-domain analyses, (slippage detection) 
- Finite element modeling of compliant structures, (bone sanding)
- Rigid-body simulation
- Engineering (visualizing planetary rover behavior or studying separation dynamics for launch vehicles) (example: ADAMS)
- Video games (contact dynamics of large numbers of rigid/soft-bodies in real-time) (example: Bullet)
- Etc.

# Rigid-body simulation
- **Collision detection**
It uses the position and geometric data of bodies to detect contact and penetration.
- **Simulator**
It computes contact forces and integrates the motion of the bodies.
    1. **The time control module** calls other modules and defines the integration time-step size. 
        1. **Fixed time-step** which is the simplest method is to use, where the size of the time-step is set at the beginning of a simulation and does not vary. (**Bullet**)
        2. **Adaptive time-stepping** algorithms vary the size of the time-step during the simulation, depending on the relative error of the state of the system. This can prevent penetrations between bodies, but increases computational expense. (**ADAMS**)
    2. **The constraint solver** computes all reaction forces acting on the bodies due to contact behavior or other constraints (e.g. joints, motors). 
        1. **Penalty based** which adds a non-linear, unidirectional spring between the two bodies. (**ADAMS**)
        2. **Constrained based** which the reaction forces are defined such that they enforce a constraint on either the position or the velocity of the objects, preventing penetration. 
            1. **Direct** methods can provide very accurate solutions, but at a very high computational expense. 𝒪(𝑛^3 )
            2. **Iterative** fixed point schemes which approximate a solution iteratively, until certain convergence criteria are met.  𝒪(𝑛) (**Bullet**)
            3. **Newton** methods also solve the system iteratively, achieving higher accuracy than iterative fixed point, but at a higher convergence time. 𝒪(𝑛^2 )  
    3. **The motion solver** uses all forces acting on the bodies to update the velocities and positions.
    
# Rigid-body simulaiton for RL
- Video Game Simulators
    - Real-time or faster
    - Scales with relatively less computational intensity using CPU threads or GPU (FleX)

<p align="center">
<img src="/img/simulation/bullet.png" height="200">
<img src="/img/simulation/flex.png" height="200">
</p>

- Engineering Simulators
    - Real-time or slower
    - More complex physics interactions
    - More functionality (e.g. frequency-domain analyses, FEM of compliant structures, optimization of cost functions)

<p align="center">
<img src="/img/simulation/atv_excavator_0.gif" height="100">
<img src="/img/simulation/dynamics.gif" height="100">
<img src="/img/simulation/flexible_body_1_0.gif" height="100">
</p>
<p align="center">
<img src="/img/simulation/viewflex_0.gif" height="100">
<img src="/img/simulation/ftire_sportscar.gif" height="100">
<img src="/img/simulation/flexible_body_2.gif" height="100">
</p>

# Issues of video game simulators
- Time-Integration
Oscillatory behavior, and instability (energy increase.)
- Friction
Acceptable sliding friction, but no static friction simulation.
- Elastic Collisions
Some collisions create more energy than others, depending on the amount of penetration at the time-step where the collision is detected.
- Constraint-Based Contact Model (Stewart-Trinkle method)
Game engines chosen to set a fixed number of iterations as a convergence criterion, rather than some tolerance on the error.
The Stewart-Trinkle method always has a solution, however, uniqueness is not guaranteed.
- Other
Fluid simulation (still rigid-body, COMSOL vs FleX)
Mechanically applied forces (motors, etc.) 
Breakable objects.

# Experimental verification
Here are important resources on this topic:
- [Benchmarking Simulated Robotic Manipulation through a Real World Dataset.](https://arxiv.org/abs/1911.01557)
<p align="center">
<img src="/img/simulation/table.png" height="300">
</p>
- [Rigid-body Simulation using Gaming Engines: A Study on the Usability of Gaming Industry Software for Simulating Engineering Problems
Title.](https://repository.tudelft.nl/islandora/object/uuid%3Ad6381efc-b79f-4d6a-92c6-20ced2968efe)
<p align="center">
<img src="/img/simulation/net.png" height="300">
</p>

# Conclusion

- MuJoCo is a popular CPU-based physics simulator, Bullet and others can be possible alternatives, but MuJoCo remains by far the most popular physics simulator in the Deep RL community. 
- FleX is also gaining momentum in Deep RL community. While GPU-accelerated physics simulations have been  applied in scientific computing and healthcare, FleX remains the only GPU-based physics simulator in gaming and robotics.
- Established engineering software packages such as SIMPACK, Adams, Vortex, and Agx also allow engineers to visualize and study the motion of mechanical systems. However, the big difference between them and gaming engines is that the latter only need to provide plausible simulation in real-time (or even faster), and thus have been developed with less stringent constraints on accuracy in mind. 


