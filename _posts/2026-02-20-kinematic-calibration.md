---
layout: post
title: "Choosing a Metrology System for Robot Kinematic Calibration"
date: '2026-01-03T01:10:00.002-04:00'
author: Mahyar
categories: [robotics, controls, metrology]
tags: [kinematic-calibration, metrology, motion-capture, laser-tracker]
---

Kinematic calibration is the process of refining a robot's kinematic model so that the pose it *thinks* it is at matches the pose it is *actually* at. The catch is right there in that sentence: the robot's own encoders cannot tell you the truth about where the tool center point (TCP) ended up, because the encoders are exactly what you are trying to validate. You need an independent, external measurement of pose. That external sensor, the ground truth, is your metrology system, and choosing the right one drives the quality of every calibration result that follows.

There is no single best answer. The right system depends on what you are measuring and under what conditions. This post walks through the questions worth answering first, the three technology families you are realistically choosing between, and a way to reason about the tradeoffs.

## Start with the requirements, not the catalog

It is tempting to start by browsing vendor datasheets. Resist that. The requirements are what eliminate options, and most of them are easy to write down once you ask the right questions.

**Working volume.** A benchtop arm and a large gantry are completely different problems. Some technologies have a fixed, well characterized accuracy inside a modest volume and degrade once you try to extend beyond it. Others scale to very large volumes but trade away other things to get there.

**Accuracy target.** Be honest about what you actually need. The useful number is the volumetric accuracy across the whole workspace, not the headline figure at the sweet spot. A system that is excellent at one meter and mediocre at the edges of a large cell may not be good enough where it counts.

**Static or dynamic.** Two very different questions hide here. If you only care about the *shape* of a path, a purely spatial measurement is enough. If you need the robot's pose *at a specific instant* so you can compare it against synchronized encoder telemetry, you now have a time alignment problem on top of a spatial one. More on that below, because it is the part people underestimate.

**One body or many.** Measuring TCP pose is one thing. Measuring the pose of each link, so you can observe individual joint contributions directly, is another. Some systems happily track many rigid bodies at once. Others track exactly one point and nothing else, which closes the door on per link observation.

**Line of sight and occlusion.** Robots fold over themselves. Any optical method needs to see its targets, and a trajectory that hides a target behind the arm will drop tracking. The question is how gracefully a given architecture handles that: can you add viewpoints, can you move the sensor, or are you simply stuck.

**Setup robustness.** How much does the measurement degrade if someone bumps the rig, if the room warms up over the day, or if you have to relocate the sensor between tests? A system that needs frequent recalibration adds friction to every session.

**Synchronization.** If you are comparing external pose against the robot's internal telemetry, the two data streams have to line up in time. Whether the metrology system can accept an external trigger, and how much latency and jitter sit between that trigger and the actual measurement instant, matters enormously once the robot is moving.

## The three families

Most commercially available options fall into one of three buckets.

### Multi-camera motion capture

These are the systems familiar from film and biomechanics labs (Vicon, OptiTrack, Qualisys and similar). You mount several cameras around the cell, each looking at the working volume from a different angle, and the software triangulates the 3D position of reflective or active markers by combining the views. A calibration step, usually waving a known wand through the volume, teaches the system where the cameras are relative to each other.

Strengths: the volume is whatever you make it, because you can add and reposition cameras. Frame rates are high, which is genuinely useful for fast motion, and multiple bodies are tracked easily so per link observation is straightforward.

Weaknesses: accuracy is tied to the camera geometry and the quality of that wand calibration, so it is less tightly bounded and more sensitive to setup than a factory calibrated instrument. The cameras must stay put; vibration, thermal drift, or a knock can degrade accuracy until you recalibrate. Passive reflective markers can also pick up spurious reflections off shiny robot surfaces, which you then have to manage by masking surfaces or switching to active markers, both of which add setup burden.

### Stereo camera trackers

A stereo tracker (Creaform's C-Track is the well known example) uses a single rigid assembly with two cameras at a precisely known, fixed baseline. Because that baseline is controlled at the factory and compensated for temperature and inclination, the system can state a strong, repeatable accuracy figure out of the box without a user calibration of camera geometry.

Strengths: trustworthy datasheet accuracy without the per session calibration dance, and notable robustness to being moved or bumped. As long as it can see enough fixed reference markers to anchor its coordinate frame, you can relocate the unit and keep tracking. It tracks multiple bodies, and in practice it tends to cope better with reflective backgrounds than passive multi-camera setups.

Weaknesses: frame rate is modest compared to dedicated mocap, so very high speed dynamics are less of a strength. Extending beyond a single unit's volume means either chaining a limited number of units or moving one unit around, and accuracy gradually softens as you stitch a larger frame of reference together. It still needs line of sight, though you have more freedom to reposition than a fixed camera array.

### Laser trackers

A laser tracker (Leica/Hexagon, API and others) points an interferometric rangefinder at a single retroreflector on a motorized mount, getting range from the laser and angles from the mount encoders. A camera on the head can resolve full 6DoF pose if the target carries an appropriate marker arrangement.

Strengths: outstanding absolute accuracy, and it holds that accuracy across very large volumes that the camera based systems cannot reach. For sheer metrological precision over distance, nothing else here competes.

Weaknesses: it tracks one target. That makes direct per link or joint angle measurement essentially impossible, and tracking TCP pose relative to the base is awkward. Line of sight is strict, and a single retroreflector is easy to occlude during realistic robot motion, after which you may need a manual reacquisition. Dynamic performance is also more constrained than mocap.

## A rough comparison

The table below is qualitative and uses ballpark, datasheet level generalizations. Exact figures depend heavily on configuration, volume, and vendor, so treat it as a starting point for your own evaluation rather than a spec.

| Criterion | Multi-camera mocap | Stereo tracker | Laser tracker |
|---|---|---|---|
| Track multiple bodies | Yes | Yes | No (single target) |
| Volume scaling | Add cameras, flexible | Limited chaining or relocate | Very large by nature |
| Accuracy character | Setup dependent | Strong out of the box | Best, holds over distance |
| Robust to bumps and drift | Recalibration likely | High | Moderate |
| Dynamic / frame rate | High | Moderate | Constrained |
| Occlusion handling | Add viewpoints | Reposition unit | Strict line of sight |
| Reflective backgrounds | Can be troublesome | Generally tolerant | Not applicable |

## The synchronization trap

If your goal is comparing external pose against internal encoder telemetry while the robot moves, the hardest part is often not spatial accuracy at all. It is time alignment.

The two data sources sample on their own clocks. Even when you trigger the metrology shutter from the robot controller, there is a fixed latency between the trigger edge and the moment the measurement is actually taken, plus some jitter around it. At speed, a small timing offset turns straight into an apparent position error, because the target has moved between the instant you wanted and the instant you got. The fixed part of that latency is deterministic, so you can compensate for it by interpolating one stream forward to the other's effective sample instant. The jitter is what is left over, and it scales with velocity.

Interpolation has its own assumptions. Fitting a smooth spline between samples works well only if the underlying motion is smooth relative to your sample rate. If the robot oscillates near or above the Nyquist frequency of your telemetry, the interpolated estimate breaks down and you see error that is really just aliasing in disguise. The practical mitigations are to use smooth trajectories, to damp out high frequency oscillation, and where possible to sample the encoders faster than the metrology system so the interpolation has more to work with. None of this is exotic, but it is the kind of thing that quietly poisons a calibration data set if you ignore it.

## How I would decide

A few heuristics that tend to hold:

- If you need per link or joint level observation, you need multiple tracked bodies, which rules out a laser tracker regardless of how good its accuracy is.
- If your workspace is genuinely large and you mainly need TCP accuracy at high precision, a laser tracker is hard to beat, as long as you can live with occlusion and single target tracking.
- If you want trustworthy accuracy with minimal calibration ceremony and tolerance for an imperfect environment, a stereo tracker is a strong default for medium volumes.
- If you need very high speed dynamics, a fully flexible volume, or dense multi body capture and you are willing to invest in setup and recalibration discipline, multi-camera mocap earns its keep.
- Whatever you pick, settle the synchronization story before you trust a single moving measurement.

The honest summary is that this is a requirements problem wearing a hardware costume. Write down the volume, the accuracy you truly need, whether you are measuring statically or dynamically, how many bodies you need to see, and how you will align time. Once those are on paper, the field usually narrows itself.
