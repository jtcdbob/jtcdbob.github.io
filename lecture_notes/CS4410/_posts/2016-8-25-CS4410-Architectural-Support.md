---
title:  "CS4410 Lecture 2 - Architectural Support"
excerpt: "Lecture Notes for CS 4410"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---

# 08/25/2016 Architectural Support for Operating Systems

## Announcement

* Homework 0 - deadlines on Monday.
* Find a homework Partner.
* First project - will be released next tuesday.
* Office hours start next week.
* Problem solving session starts on 09/05. Ives Hall 115. Will have multiple sessions, can sign up for one to go.

## Lecture
Chapter 2 (approximately).

### What is needed to help the OS do its job

#### What is a process

Process is an instance of a program. (People uses some terms loosely, and "process" is one of them.)

code\[Disk\] --compile--> executable (instructions, static data, initial values)\[Disk\] --run--> \[Physical Memory\]

\[Physical Memory\]

* Stack (temporary variables for functions, grows down and pops up)
* Heap (dynamic memory)
* Data
* Instructions

Final run step: OS sets PC to program's first instruction.

OS Kernel lives above the processes in physical memory.

* OS Kernel (stack, heap, data, instructions)
* Processes (stack, heap, data, instructions)

Not all Kernel code lives in memory, but some do.

#### What could possibly go wrong?

* Corruption of program/operating system. (privacy)
* Reading others' data. (security)
* Infinite loop. (fairness)
* Illegal operation triggers reboot.

##### Privilege levels
Some processor functionality cannot be made accessible to untrusted user applications.

Operating system = the mediator betewen untrusted/untrusting apps. The only trusted identity.

Need to differentiate untrusted apps and OS code.

Solution: "privilege mode" bit in the processor. (0 = untrusted = user, 1 = trusted = OS).

Some privileged instructions:

* changing the privilege mode
* writing to certain registers (page table base register)
* enabling a co-processor
* changing memory access permissions
* manipulate device settings
* signal other users' processes
* print character to secretLetterCountsend a packet on the network
* allocate a new page in memory

CPU knows which instructions are privileged. `opcode == privileged && mode == 0` --> Exception!

##### Context switch / mode transfer
Hardware transfer from user -> kernel:

1. mask interrupts
2. save: privilege mode, SP, PC, eflags register (x86)
3. switches SP to the kernel stack
4. save values from \#2 onto kernel stack
5. save error code (optional)
6. Set PC to the interrupt vector table

Interrupt handler

1. Save all registers (maybe fewer)
2. Eliminates the cause
3. Performs operations acquired
4. Restores  all registers (maybe fewer)
5. Performs "return from interrupt" instruction (maybe)
5. Restores the privilige mode, SP, and PC

##### Process Control Block (PCB)
For each process, the OS has a PCB containing:

* Location in memory
* Location of executable on disk
* Which user is executing this process
* Process privilege levelProcess arguments.

PCB Usually lives on the OS stack.

##### System call
Hardware transfer from user to kernel:

Instead of save error code, it's a system call not an error


#### In the very beginning.
When the system starts up

* privilege mode set to 1
* PC contains address of boot code
* Boot code loads kernel into memory
* Kernel does some setup (devices, initializes MMU, creates interupt).
* .....

##### Interrupts
Timer interrupts - process interrupted after certin period (number of instructions executed or time passed)

E.g.:
OS -> P1 -> OS -> P1 -> OS -> P2 -> OS -> P3 -> OS -> P2 (OS is not running all the time.)

More generally: hardware interrupts. External event has happened, OS needs to check it out. Process stops what it's doing, invokes OS, which handles the interrupt.

##### Interrupt management
Interrupt controllers manage interrupts

Interrupts have descriptor of the interrupting device.

Priority selector circuits ..

##### Masking Interrupts
__Maskable interrupts__: can be turned off by the CPU for critical processing (misnomer: delayed)

__Nonmaskable interrupts__: signifies serious erros.

#### Three ways for the OS to be invoked

1. Hardware interrupt
    * Some other entity trying to get CPU's attention
    * Asynchronous = caused by an external event
    * Example: keystroke, arrival of a packet from network
2. System call
    * Process needs help from the OS
    * Intentional, synchronous = caused by the syscall instruction.
    * Examples: open, write, fork, exit
3. Exception
    * Something went wrong
    * ...
    *
#### Uniprogramming

Application:

* Only one application at a time
* Always runs at the same place in physical memory.

#### Mutliprogramming, V1

No translation. Adjust addresses (ld, st, jmps) when program loaded into memory

* Everything adjusted to memory location of programming"Translation" by linker/loader
* Common in early days

No protection:

* Any process can crash another (or the OS)!

#### Mutliprogramming, V1++
Add protection:

* Two special registers (base and limit) keep user inside designated area.
* Try to access illegal addres -> error
* during switch, kernel loads new base and limits...

#### Minimum hardware requirements:

* Privileged instructions
* Timer interrupts
* Memory protection
