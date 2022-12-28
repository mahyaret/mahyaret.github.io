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

