---
title:  "CS4410 Lecture 3 - Processes"
excerpt: "Lecture Notes for CS 4410"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---

# 08/30/2016

## Announcement

* One way to prevent attacks to the OS: [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization)
* Challenging: avoid randomization without using flag. `-no-pie` (Don't produce a position independent executable. More [info](https://gcc.gnu.org/onlinedocs/gcc/Link-Options.html))
* HW0 is in flight
* 10-P1 goes out tonight (pdf on piazza already)
* OH are happening
    * VM woes (?)

## Processes and threads (more on processes)

What is a process?

* An instance of a program
* An abstraction of a computer (Address space + Hardware contect + environment).

A good abstraction:

* is portable and hides implementation details
* has an intuitive and easy-to-use interface
* can be instantiated many times
* is efficient and reasonably easy to implement

### Process management

Questions: can a program

* create and instance of another program?
    1. Only the kernel may start a Process
        * May have malicious software operations
    2. User-level processes may start processes
        * A process may want to offload its work
* wait for it to complete?
* stop or resume another running program?
* sned it an asynchronous event?

### System call interface
System call interface is the means through which the software can access the hardware. The interface is skinny. Only a few ways exist for the software to communicate with the hardware. Easy to manage.

### Creating a process
Windows: `CreateProcess`. Kernel has to

* create & initialize PCB in he kernel
* create & initialize a new address space
* load the program into the address space
* copy arguments into memory in address space
* initialize hardware context to start execution at "start"
* inform scheduler that new process is ready to run

Unix: `fork` + `exec`.

* create & initialize PCB in he kernel
* create & initialize a new address space
* initialize the address space with a copy of the entire contents of the address space of the parent
* Inherit execution context of parent (e.g. open file)
* Inform scheduler that the new process is ready to run.

#### Creating and managing Processes

* fork - create a child process as a clone of the current process. Return to both parent and child.
* exec - Run the application prog in the current process
* exit - Tell the kernel.
* ...

### What is a shell?

Job control Systems

* runs programs on behalf of the user
* allows programmer to create/manage set of programs

* sh - Original Unix Shell (Stephen Bourne, AT&T Bell Labs, 1977)
* csh - BSD Unix C Cornell
