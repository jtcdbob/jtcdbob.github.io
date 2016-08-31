---
title:  "ECE4450 - Lecture 2"
excerpt: "Lecture Notes for ECE 4450"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---

# 08/31/16

## Security

### Attacks

* Denial of service (DOS)
    * Flood bandwidth
    * Connection flooding (TCP)
    * Vulnerability in infrastructure
    * The best way to deal with DOS is to identify the source and dump all the information from it
* Distributed DOS
    * Botnet - update security patches frequently to avoid this
    * Security patches
        * Free rider problem
    * Packet sniffing
        * Very difficult to detect
        * Wireshark
        * Deep packet inspection
            * Examine application in packets in transit
            * Carnivore (used by FBI)
    * Masquerading
        * IP spoofing (beaten by authentication)
        * Phising
        * Spear phising
    * Man-in-the-middle attacks
        * Inject/modify/delete packets (from hacked routers)
        * Worm hole attack (use timestamps to defeat it)
        * Black hole attack. Delete packets with probability $$p$$

### Hacking

* Obtaining an authorized access to corporate/personal/government data --> identity theft
    * Zappos
    * Home depot
* Huge privacy issue

## Chapter 2 - Application Layer

### Internet

* **1960** - Packet switching was conceived (L, Kleinrock)
* 1967 - DARPA (Paper "Plan for a survivable computer network" L, Roberts)
* 1969 - IMP (First Internet message processor)
* 1970 - ALOHA (First wireless)
* 1976 - Circuit Switching (hard to pin down the date)
* 1980 - 200 hosts on Internet
* **1983** - TCP/IP required for Internet access
* 1986 - NSF net
* 1991 - HTTP/HTML invented by Tim Bernes-Lee
* **1995** - Internet goes commercial (growth explosion)

### Application

* uses interface
* Exploit lower layers

App -> socket -> transport -> socket -> app

### Architecture

#### Client server

* Originated in memory-starved/computationally starved era
* Still do this for
    * CAD software
    * Licensing restrictions

#### Peer-to-peer

* Enabled by computation
* No expensive infrastructure
* Distributed computing
    * SETI@home
* Redundancy
* Avoid legal intricacy (copyright law)
    * Bit Torrent
    * TOR
    * Napster
    * Grotester

### Interface

Socket - software interface
API - application programming interface

...

#### HTTP(www)

* Hypertext transfer protocol (HTTP) comm
* Hypertext markup language (html) webpages

Theory:

* Computer send GET and server responses

Partial reality:

* Computer sends UDP to DNS and DNS returns IP address as UDP
* Then the computer sends HTTP GET (TCP) to server and a html file is returned

Nonpersistent/persistent connections. HTTP is one-way, but it uses TCP.

#### Servers and Cookies

HTTP servers are stateless.

* No memory
* Greatly increase capacity/speed

Cookies provide state

User - host:

* User sends HTTP get
* Host response, set cookie.
* HTTP request with cookie
* User specific response

Host - database:

* Host creates and stores a cookie ID
* Generate cookie-specific response
