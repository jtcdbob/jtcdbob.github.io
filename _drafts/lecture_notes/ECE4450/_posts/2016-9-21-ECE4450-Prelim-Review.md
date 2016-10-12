---
title:  "ECE4450 - Lecture N"
excerpt: "Lecture Notes for ECE 4450"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---

# 09/21/16

## Network concepts

Networks generally consist of endpoints, packet switches, and links

* Circuit switching
    * Dedicated resources guaranteed for the duration of the connection
    * On the way out
* Packet switching
    * Messages are divided into packets
    * Allows much better utilization of links compared to circuit switching

Packet switching: store and forward

* Entire packet must be received at switch before forwarding
* To read destination, error checking

Edge networks

* Endpoints/Hosts
* Access networks
    * ISP
        * Cable
        * Satellite
        * ADSL
        * Fiber
    * Cellular
* Core network
    * Packet switches
    * IPX

Protocols - "A protocol defines and format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event" - Kurose & Ross

TCP/IP Protocol Stack:

* Application Layer
* Transport Layer
* Network Layer
* Link Layer
* Physical Layer

Layering makes designing, debugging, modifying protocols simpler

Encapsulation enables modularity in design. Layered design enables encapsulation of protocols

Network performance metrics

* Throughput
* Delay
* Packet loss

Propagation Delay

* The time it takes information to propagate through a link
* Medium-dependent

Transmission delay

* Time it takes to put the packet on the link

Packet Loss

* Packet loss commonly due to full queues
* Can also be because packet got corrupted

### Security

* (D)DOS
* Malware
* Botnets
* Worms, Viruses
* Spoofing (man-in-the-middle)
* More later

### Application architecture

Two main application architectures are P2P and Client-Server

### Services used / Needed

* Reliable data transfer
* Throughput
* Timing
* Security
* Multiplexing/Demultiplexing

### Sockets

* A programming abstraction
* Common terminology across socket APIs
    * Open, close, bind, listen, etc.

### Domain Name System

* Distributed database to resolve domain names
* Resolve: translate domain name into IP address
* Load balancing, host aliasing, mail server aliasing
* Goes over UDP

### HTTP

Cookies can add state to HTTP

* Allow login/logout
* Shopping cart

HTTP persistence

* Non-persistent HTTP retrieves one object per TCP connections
* Persistent HTTP can retrieve multiple objects per TCP connection

### Web caching

* Enables faster loading
* Decreases strain on network resources

### EMail

* SMTP protocol
* POP3 protocol
* IMAP protocol
* User agents, mail transfer agents, mail servers

### BItTorrent

* Peers in a torrent download equal-sized chunks from each other
* Chunks are typically 256 kB
* A tracker keeps track of peers in a torrent
* A new peer asks the tracker for a list of peers
* Ask each peer for a list of chunks
* Asks for the rarest chunk first
* Tit-for-tat: peers only upload to the peers they get the most chunks from
* Optimistic unchoking: regularly pick a peer at random and send them chunks

## Transport layer

* Reliable data transfer
* Flow control
* Congestion control
* Multiplexing ...

### Reliable data transfer

* Error detection
* In-order delivery
* ARQ

### Error Detection

* Checksums
    * E.g. TCP/UDP checksums: compute the one's complement of the sum of all 16 bit words in packet
* Cyclic Redundancy Codes (CRC)
    * The remainder in a polynomial long division over a finite field
    * Easier than it sounds
    * More on that when we get to link layer

### In-order delivery

* Each packet is routed independently
* Can arrive out of order
* Use sequence numbers to achieve in-order delivery

### Stop-and-wait

* Positive and negative acknowledgements (ACKs and NACKs)
* Send next packet when current packet is ACKed
* Resend on NACK or timeout
* Simple, low-complexity
* Poor utilization of bandwidth

### Flow Control

* Prevent sender from overwhelming receiver
* May be needed even in point-to-point links


### UDP

* No-frills encapsulation
* Provides only multiplexing/demultiplexing and basic error detection

### TCP

* Multiplexing/Demultiplexing
* Reliable data transfer
* Flow control
* Congestion control
