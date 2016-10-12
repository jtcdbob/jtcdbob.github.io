---
title:  "CS4410/11: Operating Systems"
excerpt: "Lecture Notes for CS 4410"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---

# 08/23/2016 Introduction

## Course information
Lecturer: Rachit Agarwal/Anne Bracy.

Course Objectives:

* Learn about operating system design and principles.
* Today:
    * What is an operating systems?
    * Why study operating systems?
    * Course organization.

### Example 1 - Mars Rover

* 200MHz processor, 128MB of DRAM, 256MB Flash
* Cameras, sensors, batteries, Solar Panels, Antennas, ...
* Unpredictable environment
    * How to share resources while multi-tasking?
    * How to store files of types audio, images, logs, ...?
    * How to send/receive data?
    * How to avoid/overcome failures?
* An operating system designed in a principled manner.

### Example 2 - Self driving cars

* 150 MacBook Pros in one car.
* Cameras, sensors, GPS, image recognition, ...
* Unpredictable environment
    * Same questions.

### Example 3 - Smart phones

* A8 chipset, 16GB DRAM, ...
* Camera, sensors, fingerprint device, image recognition, ...
* Evolving ecosystem of heterogeneous applications.
    * Same questions.
    * How to run new applications w/o reprogramming?
    * How to secure data (e.g., Apple pay)?

### Example 4 - Web services (Google, Facebook, ...)

* A lot of servers. Billions of users.
* Search, maps, messaging, images, videos,...
* Heterogeneous applications and heterogeneous users.
    * Same questions.

## What is an operating system?
Software to manage hardware resources.

Applications <-> OS <-> Hardware

* Virtual machine interface.
* Physical machine interface.

### Virtual machine
Software emulation of an "abstract machine"

* Illusion of hardware having features one wants
    * E.g., networking (files vs. packets)
    * E.g., storage (files vs. registers)
* Simplicity of programming
    * Each application has "all" of the resources
    * Each application doesn't care how the data is stored
* More powerful than hardware interface
    * E.g., network failures masked

## What makes an operating system good?
Two criteria:

* Principles
    * Does the design conform to a set of principles?
* Performance
    * Does the design meet certain objectives

Some principles:

* Reliability - Does the system operate as per its specification?
* Availability - What portion of the time is the system working?
* Security - Can the system be compromised by an attacker?
* Privacy - Is the data accessible only to authorized users?
* Portability - Across hardware, applications, ...
* Fairness - Do applications receive their fair share of resources?

### Performance

* Latency - how long does an operation take to complete?
* Throughput - #operations per unit time.
* Utilization - fraction of resources used over time.
* Scalability - how does the performance change with size?
* Predictabiliity - consistency of an objective over a period of time.

## Why study operating systems?

* Most widely used OS today are designed in the last decade.
* Ever-evolving applications
   * Self-driving cars
   * Internet of things
   * smart homes
* Ever-evolving technologies
   * Hardwares
   * Memory
   * .......

## This course - principles and performance
* Design principles (more or less) same across various OS
* Performance objectives same across various OS.
* ...

## Organization
* Course [webpage](http://www.cs.cornell.edu/Courses/cs4410/2016fa/)
