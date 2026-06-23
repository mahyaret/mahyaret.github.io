---
layout: post
title: "QDD Actuators: Promising Technology, Selective Fit"
date: '2026-06-23T01:10:00.002-04:00'
author: Mahyar
tags:
- robotics
- Impedance Control
- harmonic-drive
- actuators
- controls
excerpt: "Quasi-Direct-Drive actuators trade gear reduction for transparency and impact tolerance, which moves the torque burden onto the motor and the thermal budget onto the system. A look at the physics, the system-level costs, and where each architecture genuinely belongs, drawn from published robotics literature."
---

Quasi-Direct-Drive (QDD) actuators have become the default choice for dynamic legged robots, while strain-wave (harmonic) drives still dominate industrial arms. Both are good answers to different questions. This post walks through why, starting from the physics and ending with a practical map of where each architecture fits. Everything here is drawn from public sources, listed at the end.

## What the two architectures are

A QDD actuator pairs a large-diameter, high-torque-density motor with a low gear reduction, typically in the range of 3:1 to 10:1. It sits between true direct drive (1:1) and conventional high-ratio drivetrains, aiming for backdrivability, low reflected inertia, and high torque transparency. The MIT Cheetah line popularized the approach, and it now appears across platforms such as Stanford Doggo, Unitree, and the KAIST Hound.

A harmonic drive is a strain-wave gearbox that achieves very high reduction, commonly 30:1 to 320:1, in a single compact stage with near-zero backlash. A thin-walled flexspline deforms under an elliptical wave generator so its teeth mesh with a rigid circular spline at two points, advancing a couple of teeth per input revolution. The result is high torque density, excellent repeatability, and low lost motion, which is why FANUC, ABB, and KUKA use these units throughout their robot wrists, and why they show up on the Mars rovers and in surgical systems like the da Vinci.

## The physics: where the heat comes from

The central trade is simple: a lower gear ratio shifts torque production back onto the motor. To produce the same output torque, a QDD motor must generate proportionally more torque at the rotor, which means more phase current. Because resistive losses scale with the square of current (I²R), the motor dissipates more heat for the same job. The exact magnitude depends on the motor torque constant, winding resistance, thermal path, and operating point, but the direction holds: for a comparable motor frame and thermal envelope, sustained QDD torque runs hotter.

This is also why "the planetary gearbox is more efficient" can be misleading. Planetary stages used in QDD do post high gearbox efficiency, often in the low-to-mid 90s percent, versus the more variable figures quoted for strain-wave units. But gearbox efficiency is not actuator efficiency. The efficiency QDD gains at the gears can be eaten back, and in some operating regimes more than eaten back, by the extra motor winding losses the low ratio forces. Measured at the same output torque, total electrical-to-mechanical efficiency of a QDD actuator can land comparable to or worse than a harmonic-drive actuator depending on the operating point.

## The system-level trade-off

To match a comparable harmonic-drive actuator's continuous output, a QDD design usually has to accept one or more of these:

- **Reduced continuous duty cycle.** The joint can hit a high peak torque briefly, but sustained full-torque operation is thermally limited.
- **Active cooling.** Liquid loops, phase-change materials, or forced air buy thermal headroom at the cost of mass, complexity, and new failure modes. Liquid-cooled proprioceptive actuators are an active research area precisely because of this constraint.
- **An upsized motor.** Larger magnets and current capacity, plus beefier power electronics, to sustain the I²R losses, which adds weight and cost.
- **Tighter load matching.** Low ratios reflect more load inertia back to the motor, which can shrink control margin in some regimes and demand extra sizing, damping, or sensing.

There is also a straightforward cost dimension. Per joint, a strain-wave unit typically runs several times the price of a comparable planetary set, so on price alone the planetary almost always wins. Harmonic drives earn their premium when positioning repeatability, hollow-shaft routing, or torque density in a tight envelope is non-negotiable. The premium for QDD, by contrast, tends to show up not at the actuator price line but at the system level, in cooling, motor sizing, and control margin.

## At a glance

| Dimension | QDD | Harmonic Drive |
| --- | --- | --- |
| **Gear ratio** | ~3:1 to 10:1 (single stage) | ~30:1 to 320:1 (single stage) |
| **Current / heat at same output torque** | Higher; more I²R loss for a given thermal envelope | Lower; the gearbox amplifies torque |
| **Continuous duty cycle** | Often a fraction of peak under sustained load | Generally well-suited to sustained operation |
| **Torque / force-control potential** | Higher, from hardware transparency and clean current-to-torque mapping | Good when paired with torque sensing, series elasticity, or compensation |
| **Impact tolerance** | High; low reflected inertia absorbs shocks | Lower under high shock unless protected by compliance or sensing |
| **Position precision** | Lower; backlash and compliance harder to suppress | High; near-zero backlash, often a few arc-minutes |
| **Backdrivability / power-off** | Naturally backdrivable; yields under contact but does not hold position passively, so it may need a stronger brake | Low backdrivability; largely self-holding, but transmits collision forces more rigidly |
| **Holding brake demand** | Higher; the joint will not hold position passively | Lower; high reduction is largely self-locking |
| **Manufacturing maturity** | Less mature, smaller supply base | Decades of industrial validation |
| **Relative cost per joint** | Lower at the gearbox | Higher, often several times a comparable planetary |

## Where each architecture fits

**Highly dynamic leg joints favor QDD.** When impact tolerance and torque transparency dominate, low reflected inertia is exactly what you want: it absorbs ground-contact shocks, and the intermittent duty cycle of locomotion makes the thermal ceiling easier to live with. The clean current-to-torque relationship also makes high-bandwidth force control and contact estimation tractable. This is why QDD became the standard for agile quadrupeds and humanoids.

**Manipulation and dexterous arms favor high-ratio drives.** When precision, compactness, and sustained torque density matter most, strain-wave gearing's near-zero backlash and self-holding behavior are hard to beat, and the continuous-duty thermal picture is friendlier. Achievable contact-force bandwidth is system-dependent in either case: loop rates can be high for both, but realized closed-loop bandwidth depends on inertia, sensing, structural modes, and tuning.

**Conventional industrial automation stays with harmonic drives.** For pick-and-place, welding, and assembly, the mature supply chain, repeatability, and continuous duty cycle keep strain-wave gearing the low-risk default.

The honest summary is that QDD is a specialized tool, not a general upgrade. The useful question for any given joint is where you actually need hardware transparency, and what cooling and motor-sizing budget you are willing to spend to get it.

## References and further reading

- [Proprioceptive Actuator Design in the MIT Cheetah](https://fab.cba.mit.edu/classes/865.18/motion/papers/mit-cheetah-actuator.pdf)
- [Stanford Doggo: An Open-Source, Quasi-Direct-Drive Quadruped (arXiv)](https://arxiv.org/pdf/1905.04254)
- [Design, Modeling, and Analysis of a Liquid Cooled Proprioceptive Actuator for Legged Robots (IEEE AIM 2019)](https://arxiv.org/pdf/2005.11134)
- [Review of Quadruped Robots for Dynamic Locomotion (arXiv)](https://arxiv.org/pdf/2005.11134)
- [Cycloidal Quasi-Direct Drive Actuator Designs with Learning-based Torque Estimation (arXiv)](https://arxiv.org/html/2410.16591v1)
- [Strain Wave Gearing technology overview, Harmonic Drive](https://www.harmonicdrive.net/technology)
- [Strain Wave / Harmonic Gearboxes explained, Sumitomo Drive](https://us.sumitomodrive.com/en-us/news/motion-control/how-strain-waveharmonic-gearboxes-work)

*This article is a general engineering explainer assembled from the public sources above. Figures are representative ranges, not specifications for any particular product.*
