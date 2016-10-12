---
title:  "Computer Networking Reading Notes"
excerpt: "Notes for Computer Networking - a top down approach"
categories:
  - Blog
tags:
  - NOTES
use_math: true
---

# Computer Networking - A Top-Down Approach

## Chapter 1

### What is the Internet

#### A Nuts-and-Bolts Description

* Hosts/End systems: devices that are connected to network
* Communication links
    * Coaxial cable, copper wire, optical fiber, and radio spectrum
    * Transmission rate in bits/second
    * Packet = data + header
* Packet switches
    * Routers (typically in network core)
    * Link layer switches (typically in access network)
* Internet Service Providers (ISPs)
* TCP/IP
    * Transmission Control Protocol (TCP)
    * Internet Protocol (IP)
* Internet Standards
    * Developed by Internet Engineering Task Force (IETF)
    * IETF documents are called requests for comments (RFCs)

#### A service Description

* Internet is an infrastructure that provides services to applications
* Distributed applications
* Application Programming Interface (API)

#### What is a protocol?

* A protocol defines the format and the order of messages exchanged between
two or more communicating entities, as well as the actions taken on the transmission
and/or receipt of a message or other event.

## The Network Edge

* Hosts/End systems
    * Clients
    * Servers
    * Data centers

### Access Networks

##### Home access

* Digital subscriber line (DSL)
    * Digital subscriber line access multiplexer (DSLAM) in telco's local central office (CO) separates data and phone signals
    * Splitter (on the customer side) separates data and telephone signals
    * Asymmetric upstream/downstream speed
    * Limited rate when tiered service are offered
    * Short-distance service around CO.
* Cable Internet access
    * Coaxial cables -> fiber nodes -> fiber cable -> cable modem termination system (CMTS)
    * Also known as hybrid fiber coax (HFC)
    * Asymmetric
    * Share broadcast medium
* Fiber to the home (FTTH)
    * Active optical network (AON) - essentially switched Ethernet
    * Passive optical network (PON)
        * Home ->
        * Optical network terminator (ONT) ->
        * Optical splitter ->
        * Optical line terminator (OLT) ->
        * CO (optical signals => electrical signals)

##### Enterprise (and the home) access

* Local area network (LAN)
    * Ethernet
    * Wireless (802.11) - WiFi

##### Wide-Area Wireless Access

* 3G
* Long-term evolution (LTE)

### Physical Media

* Guided media
    * E.g. fiber-optic cable, a twisted-pair
copper wire, or a coaxial cable
* Unguided media
    * E.g. a wireless LAN or a digital satellite
channel
* Because the labor cost associated with the installation of the physical
link can be orders of magnitude higher than the cost of the material, many builders install twisted pair, optical fiber, and coaxial cable in every room in a
building

##### Twisted-Pair Copper Wire

* Twisted pair consists of two insulated copper wires, each about 1 mm thick, arranged in a regular
spiral pattern.
* Unshielded twisted pair (UTP) for LAN. 10Mbps to 10Gbps

##### Coaxial cable

* Coaxial cable consists of two concentric copper wires.
* Coaxial cable can be used as a guided shared medium. A number of
end systems can be connected directly to the cable, with each of the end systems
receiving whatever is sent by the other end systems

##### Fiber Optics

* An optical fiber is a thin, flexible medium that conducts pulses of light, with each pulse representing a bit.
* A single optical fiber can support tremendous bit rates, up to tens or even hundreds of gigabits per second. They are immune to electromagnetic interference, have very low signal attenuation up to 100 kilometers, and are very hard to tap.

##### Terrestrial Radio Channels

* Radio channels carry signals in the electromagnetic spectrum.

##### Satellite Radio Channels

* A communication satellite links two or more Earth-based microwave transmitter/
receivers, known as ground stations.

* Geostationary satellites - permanently remain above the same spot on Earth
    * Long delay - 280ms
* Low-earth orbiting (LEO) satellites
    * Much lower than geostationary satellites. Do not stay at the same spot
    * Many must be placed to work
    * Communicate with ground stations as well as each others

### The Network Core

#### Packet Switching

* End systems exchange messages with each other
* Packets are transmitted over each communication link at a rate equal to the full transmission rate of the link

##### Store-and-Forward Transmission

* Store-and-forward transmission means that the packet switch must receive the entire packet before it can begin to transmit the first bit of the packet onto the outbound link.
* For $N$ Links, the end-to-end delay is $$d = N\frac{L}{R}$$

##### Queuing Delays and Packet Loss

* Output buffer (output queue)
* Wait for the link to finish transmitting other packets in the output buffer
* Queuing delays
* Packet loss

##### Forwarding Tables and Routing Protocols

* Forwarding table (destination address - outbound link)
* Routing protocols

##### Circuit Switching

* In circuit-switched networks, the resources needed along a path to provide for communication between the end systems are reserved for the duration of the communication session between the end systems.
* Guaranteed constant rate

##### Multiplexing in Circuit-Switched Networks

* Frequency-division multiplexing (FDM) - the frequency spectrum of a link is divided up
    * bandwidth
* Time-division multiplexing (TDM)
* Silent periods

##### Packet Switching Versus Circuit Switching

* The trend has certainly been in the direction of packet switching

#### A Network of Networks

* Network Structure 1 interconnects all of the
access ISPs with a single global transit ISP
* Network Structure 2 consists of the hundreds of thousands of access ISPs and multiple global transit ISP
    * two-tier hierarchy
    * regional ISP - connect to tier-1 ISPs
* Network Structure 3
    * Multi-tier hierachy
    * Points of presence(PoPs, a group of one or
more routers at the same location), multi-homing, peering, and Internet exchange points(IXPs)
    * Peer - directly connect networks together so that all the traffic between them passes over the direct connection rather than through upstream intermediaries.
* Network Structure 4.
    * The ecosystem consisting of access ISPs, regional ISPs, tier-1 ISPs, PoPs, multi-homing, peering, and IXPs—as
* Network Structure 5
    * Add ontent provider networks

### Delay, Loss, and Throughput in Packet-Switched Networks

#### 1.4.1 Overview of Delay in Packet-Switched Networks

##### Types of Delays

* Processing Delay
    * Examine packet header and other information
    * On the order of microseconds or less
* Queuing Delay
    * Wait for transmission
    * Can be on the order of microseconds to milliseconds in practice.
* Transmission Delay
    * $ d= L/R $
    * Typically on the order of microseconds to
milliseconds in practice
* Propagation Delay
    * On the order of milliseconds
* Nodal Delay
    * All the delay together

#### Queuing Delay and Packet Loss

* Statistical measure for queuing delay
* Traffic intensity $ La/R$, $a$ for the average packet arrival rate
    * $La/R > 1$ may cause the system to have an infinite queue

#### End-to-End Delay

* ALl the nodal delay together $Nd$

#### Throughput in Computer Networks

* Instantaneous throughput
* Average throughput
* Bottleneck link

### Protocol Layers and Their Service Models

#### Layered Architecture

* Protocol Layering
    * service model of a layer
    * A protocol layer can be implemented in software, in hardware, or in a combination of the two.
    * Protocol stack
        * The Internet protocol stack consists of five layers: the physical, link, network, transport, and application layers
* Application Layer
* Transport Layer
    * Two transport-layer messages: TCP, UDP
    * Segment: transport-layer packet
* Network Layer (IP Layer)
    * Datagrams: network-layer packets
    * IP protocol, routing protocols
* Link Layer
    * frames: link layer packets
* Physical layer
* OSI model
    * Open Systems Interconnection (OSI)
    * application layer, presentation layer, session layer, transport layer, network layer, data link layer, and physical layer.
    * Presentation layer: data compression, data encryption and data description
    * Session layer: for delimiting and synchronization of data exchange, including the means to build a checkpointing and recovery scheme.

#### Encapsulation

* At each layer, a packet has two types of
fields: header fields and a payload field. The payload is typically a packet from the layer above.

### Networks Under Attack

* Malware in host
    * Botnet, self-replicating
    * Virus, worms
* Attack servers and infrastructure
    * Denial-of-service (DoS)
        * Vulnerability attack
        * Bandwidth flooding
        * Connection flooding
    * Distributed DoS (DDoS)
    * Packet sniffer
* Masquerade as trusted
    * IP spoofing
    * end-point authentication

## Chapter 2

### The Web and HTTP

Examples of web applications:

* The browser in user's host
* Web server program in web server host

Two common application architectures:

* Client-server
    * Server: fixed IP address, always on, generally with multiple data center (DC) to improve server performance and create virtual server (i.e.) Google has 30-50 DC.
    * Client: no strict restriction
* Peer-to-peer (P2P)
    * Self-scalability, cost effective
    * Downloading side is labeled as client whiereas uploading side is a server.

In general, the process that initiates the communication is labeled as a client and the other a server.

#### Socket

Processes get and send messages into a socket. Socket is an application programming interface (API) between application layer and transport layer.

Application developers

1. has everything in control in application layer
2. has little control in transport layer
    * can only choose which transport protocol to use
    * ability to fix transport layer parameters, such as buffer size, segment size and etc.

IP address (32 bit) is used to find host. Port number is used to find process on a host.

#### Transport layer protocol

Transport layer protocol provides 4 services:

* Reliable data transfer
* Throughput
* Timing
* Security

TCP service is

* Connection-oriented (CS architecture, handshaking)
* Reliable data transfer services
* Congestion control mechanism

UDP communicates but makes no promises in delivery.

The application layer protocol defines

* Type of message that is exchanged
* Syntax of the various message Type
* Sematics of the fields
* Rules for determining when and how a process sends messages or responds.

Application Protocols:

* HTTP (Web)
* Electronic Mail
* Directory service (DNS, not in direct contact with users but invoked by other applications indirectly)

#### Overview of HTTP
HyperText Transfer Protocol (HTTP) is the Web's application-layer protocol. It is defined in [RFC 1945] and [RFC2616].

Terminologies:

* Web page/document consists of object.
* An object is simply a file, such as an HTML file, a JEPG file and etc. Usually a web page has a base HTML file and several referenced object (by URL).
* Web browsers implement client side of HTTP.
* Web servers implement server side of HTTP. Popular choices include Apache and Microsoft Internet Information Server.

HTTP uses TCP as its underlying transport protocol. HTTP stores no information about its client - it is a stateless protocol.

#### Non-Persistent and Persistent Connections

For non-persistent connections, the TCP connection is closed after each object is sent from the server to the client. For **each object**, the response time is 2 Round Trip Time (RTT) plus the time needed to transfer the file.

The non-persistent connections must open a brand-new connection for each requested object. For those connections, TCP buffers must be allocated.

Persistent connections will maintain the TCP connection throughout communication unless waiting time is too long (> timeout on servers).

#### HTTP Message Format

##### HTTP Request
HTTP Message format:

* Request line: the first line of an HTTP request message
    * the method field (`GET`, `POST`, `HEAD`, `PUT`)
    * the URL field
    * HTTP version field.
* Header line: the subsequent lines

![HTTP Request Message Format](/images/Computer_Networking/HTTP_Request_Format.PNG)

##### HTTP Response

* 1 status line
    * Some common status code: `200 OK`, `301 Moved Permanently`, `400 Bad Request`, `404 Not Found`, `505 HTTP Version Not Supported`.
* 6 header lines
* entity body

![HTTP Response Message Format](/images/Computer_Networking/HTTP_Response_Format.PNG)

#### Cookies

Cookies are used to store client state. Servers will respond with `Set Cookie` and client will then request with the cookie in its following messages till cookies expire.

#### Web Caching

A **Web cache**—also called a **proxy server**—is a network entity that satisfies HTTP requests on the behalf of an origin Web server.

A user request usually goes to a web cache first. The proxy server will check if a local copy of the requested item exists. If it does, it will respond with the local copy, otherwise it will get the requested item and store it locally for a period of time.

Web caches are usually purchased and installed by ISPs.

Web caches have two functionalities:

1. Reduce response for cached objects.
2. Reduce network traffic.

Through the use of Content Distribution Networks (CDNs), Web caches are increasingly playing an important role in the Internet.

Conditional GET: HTTP request will specify certain criteria for the requested data (such as `last-modified-by`) and web cache will make sure the response contains up-to-date information for the client.

### Electronic Mail in the Internet

Internet mail system has three main componenets:

* user agents
* mail servers
* Simple Mail Transfer Protocol (SMTP)

Each user has a **mailbox** on the mail servers and the servers will send the mails to each other. If the other server cannot be reached, the message will be stored in a message queue for reattempts later on. A mail server acts as an SMTP client when sending and as an SMTP server when receiving.

#### SMTP

Basic steps for email sending:

1. Alice composes and sends an email using her email agent, providing Bob's address.
2. The agent places the email in Alice's email server mail queue.
3. Alice's email server gets the email and sends it over to Bob's email server using TCP.
4. Bob's email server places the email in Bob's mailbox.
5. Bob reads the mail at his convenience using his email agent.

SMTP will initiate the mail delivering process with handshakes, which can include the sender's and recipient's mail addresses.

Compared to HTTP, SMTP is a **push protocol** whereas HTTP is a **pull protocol**. SMTP imposes restriction on the message format whereas HTTP does not. SMTP puts all all of message's objects into one message whereas HTTP encapsulates each object in its own HTTP response message.

Mail messages has `FROM`, `TO`, `SUBJECT` and other header lines.

#### Mail Access Protocol

There are several mail access protocols:

* Post Office Protocol—Version 3 (POP3)
    * Easy but with limited features.
    * TCP connection to mail server port 110, performa authorization, transaction and update.
    * The protocol will rerive a message and deletes it. This can be a problem for users.
* Internet Mail Access Protocol (IMAP)
    * More complext and feature-rich than POP3.
    * Messages are associated with folders.
    * User can choose what to do with the messages after reading them.
* HTTP.
    * Web based Email. Becoming popular.
    * Mail content are accessed via HTTP instead of POP3 or IMAP.

### DNS

A host is identified by a **hostname** (easy for human to understand) and **IP addresses**.

A domain name server (DNS) translates the hostname to IP addresses. It is

1. a distributed database implemented in a hierachy of **DNS servers**.
2. an application layer protocol that allows hosts to query the distributed database.

The DNS protocol runs over UDP and uses port 53.

#### DNS Services

DNS provides:

* Host aliasing (for a host with one or more alias names. Canonical hostname.)
* Mail server aliasing (similar to host aliasing, company.com => company.mail)
* Load distribution (rotate the servers to which the traffic is directed in order to reduce the network traffic/congestion)

#### Overview of DNS

DNS simple mapping. DNS has the four properties:

* Single point of failure: DNS crashes => entire Internet crashes
* Traffic Volume: each DNS server has to handle all queries
* Distant centralized database
* Maintainence

DNS is a distributed, hierachical database:

* Root Server - Root DNS server
* Top-level-domain servers - (com, org, edu DNS)
* Authoritative DNS
    * Local DNS doesn't strictly belong to the hierarchy of severs but central to DNS architecture. Each ISP has local DNS
    * Both iterative and recursive. Requester -> local: recursive, the rest are iterative.
    * DNS caching

#### DNS Records and Messages
The DNS servers together implement a distributed database that stores **resource records (RRs)**. A resource record is a four-tuple that contains the following fields:

```
(Name, Value, Type, TTL)
```

`TTL` is the time to live for the record. The `Name` and `Value` depend on `Type`. A `Type` can be

* `A`: `Name` is hostname and `Value` is the IP address (A record).
* `NS`: `Name` is a domain name and `Value` is a hostname that knows how to obtain the IP address. This is used to send the query further along in the query chain.
* `CNAME`: `Name` is an alias for the hostname and `VALUE` is the canonical name.
* `MX`: `Name` is the alias hostname and `VALUE` is the name of mail servers.

There is only two kinds of DNS messages: DNS query and reply. They have the same format:

* Header section (12 bytes)
    * 16-bit number that identifies the query. Used in reply too.
    * Query/Reply flag bit.
    * Authoritative flag bit.
    * Recursion desired flag bit.
* Question section
    * A name field and a type field.
* Answer section
    * Type, Value, TTL field.
* Authority section
    * Records of other authoritative servers.
* Additional section

To send a query message to DNS server, use nslookup program.

A registar is a commercial entity that verifies the uniqueness of domain name and enters the domain name into the database.
### Peer-to-Peer Applications
A P2P architecture has a minimal (or no) reliance on always-on infrastructure servers.

For client-server, the lower bound for distribution time is

$$D_{cs} \ge \max\left\{\frac{NF}{u_s}, \frac{F}{d_{\min}}\right\}$$

For P2P, the lower bound is

$$D_{P2P} \ge \max\left\{\frac{F}{u_s}, \frac{F}{d_{\min}}, \frac{NF}{u_s + \sum_{i = 1}^N u_i}\right\}$$

The lower bound scales linearly for client-server and sub-linearly for P2P.

#### BitTorrent
BitTorrent is a popular P2P protocol. The collection of all peers participating the sharing of a particular file is called **torrent**. Peers in a torrent download equal-sized **chunks** from one another (typically 256KBytes).

Each torrent has an infrastructure node called a **tracker**. A peer registers itself in a tracker when it first joins the torrent and periodically updates the tracker that it is still in the torrent.

The tracker assigns neighbors for each peer.

The peer will request **rarest** chunk first. The peer will send chunks based on requester's contribution in the torrent.

A user is **choked** when it has no contribution. But it will be **optimistically unchoked** when other peers select random neighbors to send chunks.

The mechanism is referred to as **tic-for-tat**.

#### Distributed Hash Tables (DHTs)

Not discussed in class.
