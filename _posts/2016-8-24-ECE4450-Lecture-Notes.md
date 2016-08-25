---
title:  "ECE4450 Computer Networks and Telecommunications"
excerpt: "Lecture Notes for ECE 4450"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---

# Introduction

## Course information
**Lecturer:** Prof. Stephen Wicker [Email](wicker@ece.cornell.edu)

**Teaching Assistant**
kk152 TW 4-5
jmt329 R,F 3-4

**Required Text:**
Computer Networking 7th Edition

**Grading:**

2 tests + 1 final ~ 20% each

8 Homework (1 can be dropped, no late) ~ 40%


## Course Introduction:

### Application layer
* Web/HTTP
* HTTP live streaming protocol
* Email
* DNS
* Ethics module - Grotester/Napster/BitTorrent copyright
* Application module - VoLTE/VoWiFi/VoIP

### Transport layer
* Principles of reliable data transmission
* TCP/UDP/RTP

### Network layer
* Routing protocols
* Internetworking
* IP - routing on the internet

### Data Link layer / MAC sublayer
* Error control coding
* Multiple Access Techniques
    * ALOHA
    * Ethernet (802.3)
    * 802.11ac/ax/ay
* Application Module - Bluetooth

### Wireless / Mobile Networking
* 4G / 5G Cellular telephone
* Mobility management / Resource allocation
* Application module. IP multimedia (general). VoWiFi <-> VoLTE

### Network Security - privacy
* Cryptology
* AKA - Authentication -> key argument
* RSA
* Wiretapping / packet sniffing
* Location data

## Example
### Amazon
Akamai (CDN).
Backbone (ISD).
4G/LTE - WiFi
See course notes for this.

Key Technologies:

* WAN Technologies
    * TCP/IP
    * GPRS
* LAN Technologies
    * 802.11
    * 802.3

## Read Chapter 1:
The concept of

* Protocol. Format and order of messages exchanged between 2 or more entities, actions taken on transmission, receipt, or some other event.
* Host: Endpoints in a network.
* Access Networks: dial-up(dead) -> ADSL. Cable. Cellular.

### Cellular
* 1G (1983 - 1990):
    * Brick -> voice/analog -> BS(Base station) -> NTSO(Dead) -> PSTN(public switch telephone network).
    * Acoustic modem to transfer data.
* 2G (GSM, 1990 - 2000):
    * Cooler phones -> voice/digital -> BS -> MSC -> PSTN
* 3G :
    * Still cool phones -> Node B -> (circuit switched core (for voice) -> PSTN) \& (packet switched core (data) -> Internet)
* 4G :
    * VoLTE Device (with sim) -> (Voice/WiFi -> Internet -> LTE Core) \& (RAN -> LTE Core(PGW)) -> SBC -> IMS Core (USP)
    * Acronym:
        * IMS - IP Multimedia Services
        * PGW - PDN Gateway
        * ePDG - evolved Packet Data Gateway
        * AAA - Authentication, Authorization, Accounting
        * HSS - Home Subscriber Server
        * SBC - Session Border Controller

## ADSL - Asymmetric Digital Subscriber Loop
Phone -> Splitter.

MAC - ADSL Modem

DSLAM, Internet, PSTN, Local Exchange. Digital Subscriber Loop Access Multiplex.
