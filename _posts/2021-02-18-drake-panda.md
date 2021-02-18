---
layout: post
title: OpenAI Gym Environments with Drake (Part 1)
date: '2021-02-18T19:00:00.002-04:00'
author: Mahyar
tags:
- Drake
- OpenAI Gym
- Robotics
- Python
- Reinforcement Learning
---

# This post is a work-in-progress

# Why Drake?
Because it is claimed that this simulator is designed with contact-rich manipulation in mind. Since I've been always interested in Robotic Grasping, I really wanted to test this simulation out.

Drake can be run natively in C++, or by using its MATLAB, python, or Julia bindings. This manual will be focusing on using Drake in python. From the Drake Website ([https://drake.mit.edu/](https://drake.mit.edu/)):

"Drake (“dragon” in Middle English) is a C++ toolbox started by the Robot Locomotion Group at the MIT Computer Science and Artificial Intelligence Lab (CSAIL). The development team has now grown significantly, with core development led by the Toyota Research Institute. It is a collection of tools for analyzing the dynamics of our robots and building control systems for them, with a heavy emphasis on optimization-based design/analysis.

While there are an increasing number of simulation tools available for robotics, most of them function like a black box: commands go in, sensors come out. Drake aims to simulate even very complex dynamics of robots (e.g. including friction, contact, aerodynamics, …), but always with an emphasis on exposing the structure in the governing equations (sparsity, analytical gradients, polynomial structure, uncertainty quantification, …) and making this information available for advanced planning, control, and analysis algorithms. Drake provides interfaces to high-level languages (MATLAB, Python, …) to enable rapid-prototyping of new algorithms, and also aims to provide solid open-source implementations for many state-of-the-art algorithms. Finally, we hope Drake provides many compelling examples that can help people get started and provide much needed benchmarks. We are excited to accept user contributions to improve the coverage."

# Getting Started

## Getting Drake

Drake may be installed from binaries or source. Both may be gotten here:

[https://drake.mit.edu/installation.html](https://drake.mit.edu/installation.html)

## Installation

### Using source

Drake uses Bazel as a build tool under the hood. [Bazel](https://bazel.build/) is an open-source build and test tool. For compiling with the Python Bindings:

```
git clone https://github.com/RobotLocomotion/drake.git
mkdir drake-build
cd drake-build
cmake ../drake
make -j
```
By default pydrake will not be in the path. You can add the following to your `~/.bashrc`:
```
export PYTHONPATH=path/to/drake-build/install/lib/python3.6/site-packages:${PYTHONPATH}
```


### Using binary 

Instead of building from source you may want to simply use the binary files:

```
curl -o drake.tar.gz https://drake-packages.csail.mit.edu/drake/nightly/drake-latest-<platform>.tar.gz
rm -rf /opt/drake
sudo tar -xvzf drake.tar.gz -C /opt
```
Ensure that you have the system dependencies:

```
sudo ./opt/drake/share/srake/setup/ubuntu/install_prereqs
```

By default pydrake will not be in the path. You can add the following to your `~/.bashrc`:
```
export PYTHONPATH=/opt/drake/lib/python3.6/site-packages:${PYTHONPATH}
```

# Using Pydrake

Pydrake itself has generated documentation available here:
[http://drake.mit.edu/pydrake/index.html](http://drake.mit.edu/pydrake/index.html)

## Drake Concepts
### Simulation



## Drake resources

### Doxygen

Besides the source code itself, the most accurate and up to date information is available in searchable form on the Doxygen page. This is a useful reference, but can be overwhelming.

[https://drake.mit.edu/doxygen_cxx/index.html](https://drake.mit.edu/doxygen_cxx/index.html)

### Underactuated Robotics textbook and examples

Drake has a textbook being built alongside it by Russ Tedrake.

[http://underactuated.mit.edu/underactuated.html](http://underactuated.mit.edu/underactuated.html)

In particular the python source used to generate some of the examples in the book is worth examining.

[https://github.com/RussTedrake/underactuated/tree/master/src](https://github.com/RussTedrake/underactuated/tree/master/src)

The full course is available online both on Edx and more recent versions on Youtube.

[http://underactuated.csail.mit.edu/Spring2018/](http://underactuated.csail.mit.edu/Spring2018/)
