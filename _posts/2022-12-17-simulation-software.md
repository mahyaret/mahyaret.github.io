---
layout: post
title: Simulation Software
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
| :-       |    :--   |  :-- |
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
- Collision detection
It uses the position and geometric data of bodies to detect contact and penetration.
- Simulator
It computes contact forces and integrates the motion of the bodies.
1. **The time control module** calls other modules and defines the integration time-step size. 
1. **Fixed time-step** which is the simplest method is to use, where the size of the time-step is set at the beginning of a simulation and does not vary. (Bullet)
2. **Adaptive time-stepping** algorithms vary the size of the time-step during the simulation, depending on the relative error of the state of the system. This can prevent penetrations between bodies, but increases computational expense. (ADAMS)
2. **The constraint solver** computes all reaction forces acting on the bodies due to contact behavior or other constraints (e.g. joints, motors). 
1. **Penalty based** which adds a non-linear, unidirectional spring between the two bodies. (ADAMS)
2. **Constrained based** which the reaction forces are defined such that they enforce a constraint on either the position or the velocity of the objects, preventing penetration. 
1. **Direct** methods can provide very accurate solutions, but at a very high computational expense. 𝒪(𝑛^3 )
2. **Iterative** fixed point schemes which approximate a solution iteratively, until certain convergence criteria are met.  𝒪(𝑛) (Bullet)
3. **Newton** methods also solve the system iteratively, achieving higher accuracy than iterative fixed point, but at a higher convergence time. 𝒪(𝑛^2 )  
3. **The motion solver** uses all forces acting on the bodies to update the velocities and positions.
