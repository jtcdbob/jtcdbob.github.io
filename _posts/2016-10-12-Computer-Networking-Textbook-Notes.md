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

## Chapter 3

### Overview of Transport-Layer Services

A transport-layer protocol provides for **logical communication** between application processes running on different hosts. From an appplication's perspective, the two hosts function as if they're directly connected. The transport layer converts the application-layer messages into transport-layer packets, also known as transport-layer segments.

#### Relationship between transport and Network Layers

Transport layer provides **logical** communication between processes running on different hosts. A network-layer protocol provides logical communication between hosts.

The service that a transport protocol can provide are often constrained by the service model of the underlying network-layer protocol. Nevertheless, certain services can be offered by a transport protocol even when the underlying network protocol doesn't offer the corresponding service, such as reliable data transfer.

#### Overview of the Transport Layer in the Internet

The IP service model is a **best-effort delivery service**, hence an **unreliable service**.

Extending host-to-host delivery to process-to-process delivery is called **transport-layer multiplexing** and **demultiplexing**.

TCP provides

* **reliable data transfer** - data received are correct and in order
* Congestion control - TCP tries to give each connection an equal share of the link bandwidth on a congested link.

### MUltiplexing and Demultiplexing

The job of delivering the data in a transport-layer segment to the correct socket is called **demultiplexing**. The job of gathering and encapsulating data to create segments passed to the network layer is called **multiplexing**.

Both UDP and TCP have **source port number field** and **destination port number field**. Each port number is a 16-bit number, ranging from 0 to 65535. The port number ranging from 0 to __1023__ are called **well-known port numbers** and are restricted (reserved for well-known application protocols, HTTP:80, FTP:21).

For UDP, typically the server side assigns a specific port number while the client side lets the transport layer automatically assign an available port number. UDP socket is fully identified by destIP and dest port number.

TCP socket is identified by srcIP, src port number, destIP and dest port number.

### Connectionless Transport: UDP

> UDP does just about as little as a transport protocol can do. Aside from the multiplexing/demultiplexing function and some light error checking, it adds nothing to IP.

With UDP, there is no handshaking between sender and receivers, so it is said to be __connectionless__.

Some applications prefer UDP over TCP for the following reasions:

* Finer application-level control over what data is sent, and when. For example, TCP may apply congestion control and it can harm some time-sensitive applications.
* No connection establishment.
* No connection state.
* Small packet header overhead. TCP segment has 20 bytes of overhead whereas UDP has only 8 bytes.

| TCP     | SMTP(Email), Telnet(Remote access), HTTP(Web), FTP(File Transfer),       |
|---------|--------------------------------------------------------------------------|
| UDP/TCP | Streaming multimedia, Internet telephony                                 |
| UDP     | NFS(Remote File Server), SNMP(Network Management), DNS(Name Translation) |

Must note that it is possible for an application to have reliable data transfer when using UDP, which can be done if reliability is built into the application itself.

#### UDP Segment Structure

UDP has four fields in its header (each two bytes) - src port number, dest port number, length, checksum.

UDP performs error checking with checksum. A simple example of checksum is to add the bit presentation of two data up and wrap the last digit around.

UDP has error checking even though other layers has similar functionality. This is an example of **end-end principle** (necessary waste something something). Although UDP provides error checking, it does nothing to recover from error.

### Principles of Reliable Data Transfer

It is the responsibility of a **reliable data transfer protocol** to implement the service abstraction (of reliable data transfer). Most cases discussed are **unidirectional data transfer** but the concept can be easibly adapted for **bidirectional data transfer**.

#### Bulding a reliable data transfer protocol

Assume a perfectly reliable channel: `rdt1.0`. The finite-state machine (FSM) definition.

Over a chanel with bit errors: `rdt2.0`. The message-dictation protocol uses both **positive/negative acknowledgement** (for "OK" and "repeat that"). In a computer network setting, reliable data transfer protocols based on such retransmission are known as **ARQ(Automatic Repeat reQuest) protocols**.

ARQ protocols must have the capabilities for:

* Error detection.
* Receiver feedback.
* Retransmission.

`rdt2.0` is also known as **stop-and-wait** protocol because it waits for one packet to finish transferring before starting the next one.

To differentiate the ACK and NACK for different packets, there is also a **sequence number** for the data packets (`rdt2.1`). In the case of a stop-and-wait protocol, a 1-bit sequence number will suffice. `rdt2.2` eliminated NACK by sending ACK with the previous sequence number to indicate error.

`rdt3.0` adds a **countdown timer** to interrupt the sender after a given amount of time has expired. Because the sequence number alternate between 0 and 1, protocol `rdt3.0` is also known as the **alternating-bit protocol**.

`rdt3.0` is a functional protocol, but its **utilization** is poor. One way to improve it is to do **pipelining**.

#### Go-Back-N (GBN)

**Go-Back-N** protocol sends packet without waiting for an acknowledgement, but it will not have more than N unacknowledged packets in the pipeline. The GBN protocol is a **sliding-window protocol** and the number N is often referred to as **window size**.

The GBN sender respons to three types of events:

* Invocation from above. The sender will send packets when called if the window is not full.
* Receipt of an ACK. An acknowledge for a packet with seq number n will be taken to be a **cumulative acknowledgement**, meaning that packets < n have been correctly received.
* A timeout event. The sender will resend all unacknowledged packets and restart a timer.

The receiver will send an ACK for n if all previous packets have been received correctly and in order. In any other cases, the receiver discards the packet and resends an ACK for the most recently received in-order packet.

The protocol will likely result in an **event-based programming** because its actions respond to certain situations.

#### Selective Repeat (SR)

Selective-repeat protocols avoid unnecessary retransmission by having the sender retransmit only those packets that it suspects were received in error (lost or corrupted) at the receiver. A window of size N is also used to limit the number of packets in the pipeline.

The receiver will ACK packets in `[rcv_base, rcv_base + N - 1]`. If the received packets are correct but out of order, the receiver will buffer them and send the ACK.

### 3.5 Connection-Oriented Transport: TCP

#### 3.5.1 The TCP Connection

TCP is **connection-oriented** because of the **three-way handshake** that two processes have to go through before starting communication. The TCP "connection" is not an end-to-end TDM or FDM circuit as in a circuit-switch network but instead is a logical one. A TCP connection provides a **full-duplex service** - application layer data can flow in both direction at the same time. A TCP connection is also always **point-to-point** (between single sender and single receiver) and "multicasting" is not possible with TCP.

Three-way handshake:

1. The client process first sends a special TCP segment
2. The server process responds with a second special TCP segment
3. The client process responds with a third special segment

TCP directs payload data to the connection's send buffer, which is set aside during the initial three-way handshake.

![TCP Send And Receive Buffers](/images/Computer_Networking/TCP_Buffer.PNG)

The maximum amount of data that can be grabbed and placed in a **TCP segment** is limited by the **maximum segment size (MSS)**. The MSS is typically set by determining the length of the largest link-layer frame that can be sent by the local sending host (**maximum tranmission unit (MTU)**) and then subtracting the TCP/IP header length (typically 40 bytes).

#### 3.5.2 TCP Segment Structure

The TCP header includes **source and destination port number** which are used for multiplexing/demultiplexing data from/to upper-layer applications. The header also includes a **checksum field**. Additionally, the TCP segment header contains

* The 32-bit **sequence number field** and the 32-bit **acknowledgement number field**
* 16-bit **receive window** field for flow control
* 4-bit **header length field**
* Optional and variable-length **options field**.
* The **flag field** that contains 6 bits. The **ACK bit**, **RST**, **SYN** and **FIN** bit for connection setup and tear down. **PSH** bit that indicates the receiver should pass the data to the upper layer immediately. The **URG** bit that is used to indicate urgency. A 16-bit **urgent data pointer field**. (In practice, the PSH, URG and urgent data pointer are not used.)

**Sequence number for a segment** is the byte-stream number of the first byte in the segment. **Acknowledge number** is the segment number of the next byte that the sending host is expecting from the receiving host. TCP provides **cumulative acknowledgement**.

#### 3.5.3 Round-Trip Time Estimation and Timeout

TCP takes sameple RTT and updates its estimated RTT using a weighted combination algorithm.

```
EstimatedRTT = (1 - a) * EstimatedRTT + a * SampleRTT
```

The recent samples better reflect the current congestion in the network. Such average is called an **exponential weighted moving average (EWMA)**.

In addition, it is also useful to measure the variability of the RTT:

```
DevRTT = (1 - b) * DevRTT + b * abs(SampleRTT - EstimatedRTT)
```

Usually timeout interval is set to

```
TimeoutInterval = EstimatedRTT + 4 * DevRTT
```

#### 3.5.4 Reliable Data Transfer

TCP creates a **reliable data service** on top of IP's unreliable best-effort service.

TCP sender responds to three major events: data received from application above, timeout and ACK receipt.

* When data is received from the application it encapsulates the data in a segment and passes the segment to IP.
* When there is a timeout, TCP will retranmit the segment that caused the timeout.
* When ACK segments arrive, The TCP compares the ACK value `y` with its variable `SendBase` (the sequence number of the oldest unacknowledged byte).

Doubling the Timeout Interval - each time TCP retransmits, it sets the next timeout interval to twice its previous size rather than deriving from the `EstimatedRTT`.

For fast retransmission, TCP uses **duplicate ACK** - an ACK that acknowledge a segment that has been received via previous acknowledgement. In the case when 3 duplicate ACKs are received, the TCP sender assumes that the segment following this one is lost and performs a **fast retansmit** (retransmitting missing segment before that segment's timer expires).

The TCP's error-recovery mechanism(**selective acknowledgement**) is a hybrid of GBN and SR protocol.

#### 3.5.5 Flow Control

TCP provides a **flow-control service** to its applications to eliminate the possibility of the sender overflowing the receiver's buffer. Flow control is a speed-matching service. In comparison, a TCP sender is throttled due to congestion within the IP network, which is referred to as **congestion control**.

TCP provides flow control by having the sender maintain a variable called the **receive window**, which basically gives the sender an idea of how much free buffer space is available at the receiver. In contrast, UDP does not provide flow control and therefore there will be segment loss due to buffer overflow.

#### 3.5.6 TCP Connection Management

See book for a more detailed description of three-way handshake. And there are various TCP states during the life of a TCP connection.

### 3.6 Principles of Congestion Control

#### 3.6.1 The Causes and the Costs of Congestion

##### Scenario 1: Two Senders, a Router with Infinite Buffers

The send speed is limited to the sharing link capacity between two connections (R/2). As a consequence of congested network in this case, large queuing delays are experienced as the packet-arrival rate nears the link capacity.

![TCP Congestion Scenario 1](/images/Computer_Networking/Congestion_S1.PNG)

![TCP Congestion Scenario 1 Graph](/images/Computer_Networking/Congestion_S1_Graph.PNG)

##### Scenario 2: Two Senders and a Router with Finite Buffers

Suppose the buffer is now finite and each dropped segment will eventually be retransmitted. The rate at which the transport layer sends segments into the network is sometimes referred to as the **offered load** to the network. The performance will now depend strongly on how the retransmission is implemented.

For a congested network, the sender must also perform retransmission in order to compensate for dropped(lost) packets due to buffer overflow.

If a sender times out prematurely and retransmit a packet that is delayed in the queue but not lost, then there will be unneeded retransmissions by the sender in the face of large delay.

![TCP Congestion Scenario 1 Graph](/images/Computer_Networking/Congestion_S2_Graph.PNG)

##### Scenario 3: Four Senders, Routers with Finite Buffers, and Multihop Paths

Segments goes through multiple routers. When a packet is dropped along a path, the transmission that was used at each of the upstream links to forward the packet to this point is wasted.

![TCP Congestion Scenario 1 Graph](/images/Computer_Networking/Congestion_S3.PNG)

![TCP Congestion Scenario 1 Graph](/images/Computer_Networking/Congestion_S3_Graph.PNG)

#### 3.6.2 Approaches to Congestion Control

At highest level, the congestion-control approaches are divided into

* End-to-end congestion control. The network layer provides no explicit support to the transport layer for congestion control purposes.
* Network-assisted congestion contrl. Router provide explicit feedback to the send and/or receiver regarding the congestion state of the network.

### 3.7 TCP Congestion Control

Sender keeps an additional variable, the **congestion window** (`cwnd`). Specifically, the amount of unacknowledged data at a sender may not exceed the minimum of `cwnd` and `rwnd`.

```
LastByteSent - LastByteAcked <= min {cwnd, rwnd}
```

TCP is **self-clocking** in the sense that it uses acknowledgement to trigger (or clock) its increase in congestion window size.

TCP has the following guiding principles to deal with congestion:

* A lost segment implies congestion, and hence, the TCP sender's rate should be decreased when a segment is lost.
* An acknowledged segment indicates that the network is delivering the sender's segments to the receiver, and hence the sender's rate can be increased when an ACK arrives for a previously unacknowledged segment.
* Bandwidth probing.

The celebrated **TCP congestion-control algorithm**.

##### Slow Start

The value of `cwnd` is initialized to a small value of 1 MSS and it increases by 1 MSS every time a transmitted segment is first acknowledged. The process results in a doubling of the sending rate every RTT. E.g. it sends 1, receives 1, then sends 2 and receives 2 (the `cwnd` is now at 4).

##### Congestion Avoidance

For time-out event, the value of `cwnd` is set to 1 MSS, and the value of `ssthresh` is updated to half the value of `cwnd` when the loss event occurred. For a triple-duplicate-ACK loss event happens, TCP halves the value of `cwnd` and the value of `ssthresh`.

##### Fast Recovery

The value of `cwnd` is increased by 1 MSS for every duplicate ACK received for the missing segment that caused TCP to enter the fast-revocery state.

An early version of TCP, **TCP Tahoe**, unconditionally cut the congestion window to 1 MSS and enter the slow-start phase after encountering a timeout-indeicated or triple-duplicate-ACK-indicated event. The newer version of TCP, **TCP Reno** incorporates fast recovery.

![FSM Description of the TCP congestion control](/images/Computer_Networking/TCP_Congestion_Control.PNG)

![Evolution of TCP's congestion window (Tahoe and Reno)](/images/Computer_Networking/TCP_CC_Window_Evo.PNG)

##### A Retrospective View

TCP congestion control is often referred to as an **additive-increase, multiplicative-decrease(AIMD)** form of congestion control.

#### 3.7.1 Fairness

A congestion control mechanism is said to be fair if the average transmission rate of each connection is approximately R/K.

Many applications, such as video call and streaming, do not use TCP because they don't want to get throttled.

## Chapter 4 The Network Layer: Data Plane

### 4.1 Overview of Network Layer

#### 4.1.1 Forwarding and Routing: The Data and Control Plane

Two important network-layer functions are

* Forwarding. When a packet arrives at a router's input link, the router must move the packet to the appropriate output link.
* Routing. The network layer must determine the route or path taken by the packets as they flow from the sender to a receiver. **Routing algorithms** are used to calculate those paths.

A key element in every network router is its **forwarding table**. A router forwards a packet by examing the value of one or more fields in the arriving packet's header, and then using these header values to index into its forwarding table.

Control Plane

* The traditional approach. A routing algorithm runs in each router and both forwarding and routing algorithms are contained within a router.
* The software-defined networking (SDN) approach. A remote controller is implemented to compute and distribute forwarding tables, and the routing devices perform forwarding only.

#### 4.1.2 Network Service Model

The **network service model** defines the characteristics of end-to-end delivery of packets between sending and receiving hosts. The services could include:

* Guaranteed deliver.
* Guaranteed delivery with bounded delay.
* In-order packet delivery.
* Guaranteeed minimal bandwidth.
* Security.

The Internet's network layer provides a single service, known as **best-effort service**.

### 4.2 What is Inside a Router?

A router consists of

* Input ports. An **input port** performs:
    * Physical layer function of terminating an incoming physical link at a router.
    * Link-layer functions needed to interoperate with the link layer at the other side of the incoming link.
* Switching fabric. The switching fabric connects the router's input ports to its output ports.
* Output ports. An **output port** stores packets received from the switching fabric and transmits these packets on the outgoing link by performing the necessary link-layer and physical layer functions. An output port is typically paired with the input port for that link on the same line card.
* Routing processor. The routing processor performs control-plane functions. In traditional routers, it executes the routing protocol. In SDN routers, the routing processor is responsible for communicating with the remote controller in order to receive forwarding tables and etc.

A router's input/output ports and switching fabric are almost always implemented in hardware, because software will be too slow.

![Router Architecture Diagram](/images/Computer_Networking/Router_Architecture.PNG)


#### 4.2.1 Input Port Processing and Destination-based Forwarding

![Router Architecture Diagram](/images/Computer_Networking/Input_Port_Processing.PNG)

The router matches a **prefix** of the packet's destination address with the entries in the forwarding table. When there are multiple matches, the router uses the **longest prefix matching** rule to forward the packet.

In addition to look-up, the input port also take other actions:

* Physical- and link-layer processing.
* The packet's version number, vhecksum and time-to-live field will be checked and rewritten if necessary.
* Updating counters used for network management.

#### 4.2.2 Switching

There are several ways to accomplish switching:

* Switching via memory.
* Switching via a bus.
* Switcing via an interconnection network, A crossbar switch is non-blocking.

![Switching Techniques](/images/Computer_Networking/Switching_Techniques.PNG)

#### 4.2.3 Output Port Processing

Output port takes packets in the memory and transmit them over the output link. This includes selecting and dequeueing packets for transmission and performing necessary link-layer and physical-layer transmission.

#### 4.2.4 Where Does Queueing Occur?

**Packet loss** occurs when no memory is available to store arriving packets.

If the switch fabric is not fast enough to transfer all arriving packets through the fabric without delay, then packet queueing can occur at the input layer. **Head-of-the-line (HOL) blocking** - the packet is blocked by another packet at the head of line even when some output links are free.

When there is not enough memory to buffer an incoming packet, the router must either drop the arriving packet (**drop-tail** policy) or remove one or more already-queued packets to make room. A number of proactive packet-dropping and -marking policies (collectively known as **active queue management(AQM)** algorithms). One of the widely studied and implemented AQM algorithm is the **Random Early Detection (READ)** algorithm. **A packet scheduler** at the output port must choose one packet among those queued.

#### 4.2.5 Packet Scheduling

Some scheduling:

* First-in-First-out (FIFO)
* Priority Queuing. Packets arriving at the output link are classified into priority classes upon arrival at the queue. For example, real-time voice-over-IP packets might receive higher priority over non-real-time traffic such as SMTP and IMAP e-mail packets. A priority class typically has its own queue.
* Round Robin and Weighted Fair Queuing (WFQ). **work-conserving queueing)** discipline. A generalized form of round robin queuing is widely implemented in routers as the so-called **weighted fair queuing (WFQ) discipline**.

### 4.3 The Internet Protocol (IP): IPv4, Addressing, IPv6, and More

#### 4.3.1 IPv4 Datagram Format

The key firlds in the IPv4 datagram are

* 4-bit Version number for the IP protocol version.
* 4-bit Header length. Without options, a typical IP datagram has 20-byte header.
* Type of service (TOS).
* Datagram Length. Theoretical, the maximum length is 65,535 bytes, but in reality, it's rarely longer than 1,500 bytes.
* Identifier, flags, fragmentation offset.
* Time-to-live (TTL).
* Protocol.
* Header checksum.
* Source and destination IP addresses.
* Options.
* Data (payload).

![IPv4 Datagram Format](/images/Computer_Networking/IPv4_Format.PNG)

#### 4.3.2 IPv4 Datagram Fragmentation

The maximum amount of data that a link-layer frame can carry is called the **maximum transmission unit (MTU)**. To squeeze an oversized IP datagram into the payload field of the link-layer frame, the payload in the IP datagram is fragmented into many smaller IP datagrams encapsulated in separate link-layer frames. Each of the smaller datagrams are referred to as **fragments**.

#### 4.3.3 IPv4 Addressing

The boundary between the host and the physical link is called an **interface**. IP requires each host and router interface to have its own IP address, so the IP adress is technically associated with an interface, rather than with the host or router containing that interface.

Each IP address is 32 bits long (4 bytes). These addresses are typically written in so-called **dotted-decimal notation**. Each interface on every host and router in the global internet must have an IP address that is globally unique (except the interfaces behind NAT).

The network interconnecting three host interfaces and one router interface forms a **subnet**(or an IP network). Eg. IP addressing assigns an address to this subnet: 223.1.1.0/24 where the /24 notation is sometimes known as a **subnet mask**, indicating that the leftmost 24 bits quantity define the subnet address.

The Internet's address assignment strategy is known as **Classless Interdomain Routing(CIDR)**. CIDR generalizes the notion of subnet addressing with the format a.b.c.d/x. The x most significant bits of an address constitute the network portion of the IP address and often referred to as the **prefix** (or network prefix). The remaining bits are to distinguish among the devices within the organization.

Before CIDR, the network portion of an IP address were constrained to be 8, 16, or 24 bits in length, an addressing scheme known as **classful addressing**, since they were known as class A, B and C networks.

There is another type of IP address, the IP broadcast address 255.255.255.255. When a host sends a datagram with destination address 255.255.255.255, the message is delivered to all hosts on the same subnet. Router optionally forward the message into neighboring subnets as well (although they usually don't).

##### Obtaining a Block of Addresses

A network admin might contact its ISP, which would provide addresses from a larger block of address that had been allocated to the ISP. IP addresses are managed under the authority of the Internet Corporation of Assigned Names and Numbers (ICANN).ICANN does not only allocate IP addresses but also manage the DNS root servers.

##### Obtaining a Host Address: The Dynamic Host Configuration Protocol

Host addresses can be configured manually, but typically it is done using the **Dynamic Host Configuration Protocol(DHCP)**. DHCP allows a host to obtain an IP address automatically. A network admin can configure DHCP so that a given host receives the same IP address or it gets a **temporary IP address** that is different everytime.

DHCP is often referred to as a **plug-and-play** or **zeroconf** protocol.

For a newly arriving host, the DHCP protocol is a four-step process:

1. DHCP server discovery. This is done using a **DHCP discover message**, which a client sends within a UDP packet to port 67. The DHCP client sends to 255.255.255.255 and the host source IP address 0.0.0.0.
2. DHCP server offer. A DHCP server receiving a DHCP discover message responds to the client with a **DHCP offer message** that is broadcast to all nodes on the subnet, again using 255.255.255.255.
3. DHCP request. The newly arriving client will choose from among one or more server offers and respond to its selected offer with a **DHCP request message**.
4. DHCP ACK. The server responds to the DHCP request message with a **DHCP ACK message**, confirming the requested parameter.

Once the client receives the DHCP ACK, the interaction is complete and the client can use the DHCP-allocated IP address for the lease duration.

#### 4.3.4 Network Address Translation (NAT)

Netword address translation (NAT) deals with the problem when a subnet grows bigger and requires a larger blcok of addresses.

The address space 10.0.0.0/8 is one of the three portions of the IP address space that is reserved in [RFC 1918] for a **private network** or a **realm with private addresses**.

The NAT-enabled router does not look like a router to the outside world - it behaves as if it is a single device with a single IP address. It hides the details of the home network from the outside world. NAT router has a **NAT translation table** that includes port numbers as well as IP addresseds in the table entries.

#### 4.3.5 IPv6

##### IPv6 Datagram Format

IPv6 Datagram format changes are

* Expanded addressing capacity. The IP address capacity is now 128 bits. IPv6 also introduced a new type of address, called an **anycast address**, which allows a datagram to be delivered to any one of a group of hosts.
* A streamlined 40-byte header.
* Flow labeling.

IPv6 fields are

* Version.
* Traffic class.
* Flow label
* Payload length
* Next header
* Hop limit - how many routers can be used to forward to datagram
* Source and destination addresses
* Data

In comparison to IPv4, IPv6

* No longer allows fragmentation/reassembly
* Has no header checksum
* Has no options field

![IPv6 Datagram Format](/images/Computer_Networking/IPv6_Format.PNG)

##### Transition from IPv4 to IPv6
The approach to IPv4-to-IPv6 transition that has been most widely adopted in practice involves **tunneling**. With tunneling, the IPv6 node takes the entire IPv6 datagram and puts it in the data (payload) field of an IPv4 datagram. On the receiving end, the IPv6 node will note the flag in protocol number field and extract the IPv6 datagram.

### 4.4 Generalized Forwarding and SDN

## Chapter 5

### 5.1 Introduction

There are two possible ways to do routing:

* Per-router control. Both a forwarding and a routing function are contained within each router.
* Logically centralized control. A centrolized controller performs traditional IP forwarding as well as a rich set of other functions (load sharing, firewalling, and NAT).

### 5.2 Routing Algorithms

Two kinds of routing algorithms:

* Centralized routing algorithms, e.g., link-state(LS) algorithms.
* Decentralized routing algorithms, e.g., distance-vector(DV) algorithms.

Another way to classify routing algorithms is based on whether they're static or dynamic. Or load-sensitive or load-insensitive.

#### 5.2.1 The Link-State (LS) routing algorithm

Each node broadcast link-state packets to all other nodes in the network, with each link-state packet containing the identities and costs of its attached links. Each node has an identical and complete view of the network, and runs the LS algorithm to compute the same set of least-cost paths as every other node. The shortest-path (Djikstra) algorithm is used to compute the forwarding table.

#### 5.2.2 The Distance-Vector (DV) routing algorithm

The DV algorithm is iterative, asynchronous and distributed. The least costs are related by the Bellman-Ford equation.

$$
D_x(y) = \min_v \{ c(x, v) + D_v(y)\}
$$

for each node $y$ in N.

Routing loops can occur when there are network changes, which is sometimes referred to as the count-to-infinity problem. Adding poisoned reverse is a way to reduce the occurance of such problem.

### Intra-AS Routing in the Internet: OSPF

Routers are organized into autonomous systems (AS) with each AS consisting of a group of routers that are under the same administration control. Routers within the same AS all run the same algorithms and have information about each other. Such algorithms are called intra-autonomous system routing protocols.

Open Shortest Path First (OSPF) routing and IS-IS are widely used for intra-AS routing in the Internet. OSPF is a link-state protocol that uses flooding of link-state information and a Dijkstra's least-cost path algorithm to determine a shortest-path tree to all subnets.

Sme advantages embodied in OSPF include security

* authentication can be done for each exchange between routers.
* Multiple same-cost paths. OSPF allows multiple paths to be used when they have the same cost.
* Integrated support for unicast and multicast routing.
* Support for hierachy within a single AS. An OSPF AS can be configured hierarchically into areas, with each area running its own OSPF link-state routing algorithm.

### 5.4 Routing Among the ISPs: BGP

All ASs run the same inter-AS routing protocol, called the Border Gateway Protocol (BGP).

#### 5.4.1 The Role of BGP

BGP provides each router a means to

* Obtain prefix reachbility information from neighboring ASs.
* Determine the "best" routes to the prefixes

#### 5.4.2 Advertising BGP Route Information

For each AS, each router is either a gateway router or an internal router. In BGP, pairs of routers exchange routing information over semi-permanent TCP connections using port 179. Each such TCP connection is called a BGP connection, either as an external BGP (eBGP) connection or as an internal BGP (iBGP) connection.

#### 5.4.3 Determining the Best Routes

How potato routing.

#### 5.4.4 IP-Anycast

#### 5.4.5 Routing Policy

#### 5.4.6 Putting the Pieces Together: Obtaining Internet Presence

### 5.5 The SDN Control Plane

### 5.6 ICMP: The Internet Control Message Protocol.

The ICMP is used by hosts and routers to communicate network-layer information to each other. The most typical use of ICMP is for error reporting.

### 5.7 Network Management and SNMP

## Chapter 6 The Link Layer and LANs

### 6.1 Introduction to the Link Layer

A node is any device that runs a link-layer protocol. The communication channels that connect adjacent nodes along the communication path are links. Over a given link, a transmission node encapsulates the datagram in a link-layer frame and transmits the frame into the link.

#### 6.1.1 The Services Provided by the Link Layer

* Framing. Almost all link-layer protocols encapsulate the datagram within a link-layer frame before transmission.
* Link access. A medium access control (MAC) protocol specifies the rules by which a frame is transmitted onto the link.
* Reliable delivery. When a link-layer protocol guarantees to move each network-layer datagram across the link without error
* Error detection and correction.

#### 6.1.2 Where Is the Link Layer Implemented?

For the most part, the link layer is implemented in a network adapter, sometimes known as a network interface card (NIC).

### 6.2 Error-Detection and Correction Techniques.

The link layer provides bit-level error detection and correction.

#### 6.2.1 Parity checks

The simplest form of error detection is the use of a single parity bit. This can be extended to two-dimensional parity scheme.

#### 6.2.3 Checksumming Methods

The Internet checksum. Checksumming methods require relatively little packet overhead.

#### 6.2.3 Cyclic Redundancy Check (CRC)

CRC codes are also known as polynomial codes.

### 6.3 Multiple Access Links and Protocols

A point-to-point link consists of a single sender at one end of the link and a single receiver at the other end of the link. The second type of link, a broadcast link, can have multiple sending and receiving nodes all connected to the same, single, shared broadcast channel.


#### 6.3.1 Channel Partitioning Protocols

Time division multiple access (TDMA), frequency division multiple access (FDMA), code division multiple access (CDMA)

#### 6.3.2 Random Access Protocols

ALOHA and slotted ALOHA.

Carrier Sense Multiple Access (CSMA). CSMA/CD (collion dection) protocols are commonly used in Ethernet. Binary exponential backoff is used.

#### 6.3.3 Taking-Turns Protocol

Pooling protocol and token-passing protocol.

#### 6.3.4 DOCSIS: THe Link-Layer Protocol for Cable Internet Access

### Switched Local Area Network

#### 6.4.1 Link-Layer Addressing and ARP

MAC  Address. A link-layer address is often called a LAN address, a physical address or a MAC address. It is 6 bytes long and has a flat structure.

Address Resolution protocol (ARP). Each host and router has an ARP table in its memory.

#### 6.4.2 Ethernet

#### 6.4.3 Link-Layer Switches

#### 6.4.4 Virtual Local Area Networks (VLANs)

### 6.5 Link Virtualization: A Network as a Link Layer

#### 6.5.1 Multiprotocol Label Switching

### 6.6 Data Center Networking

### 6.7 Retrospective: A Day in the Life of a Web Page Request

#### 6.7.1 Getting Started: DHCP, UDP, IP, and Ethernet

#### 6.7.2 Still Getting Started: DNS and ARP

#### 6.7.3 Still Getting Started: Intra-Domain Routing to the DNS Server

#### 6.7.4 Web Client-Server Interaction: TCP and HTTP

## Chapter 7 Wireless and Mobile Network

### 7.1 Introduction

* Wireless hosts: end systems that run applications.
* Wireless links: communication links through which the hosts connect to base stations.
* Base station: responsible for sending and receiving data to and from an associated wireless host.
    * Cell towers in cellular networks
    * Access points in 802.11 wireless LAN

Hosts can operate in

* infrastructure mode, when they are connected to base stations.
* ad hoc networks, when no infrastructure is involved.

When a mobile host changes its associated base station while moving, it is called handoff.

### 7.2 Wireless Links and Network Characteristics

A wireless network has a few important differences from a wired link:

1. Decreasing signal strengt due to path loss.
2. Interference from other sources. Such as 802.11b wireless LAN (2.4GHz) conflicts with microwave.
3. Multipath propagation due to reflection off objects.

Signal-to-noise ratio(SNR) is a relative measure of the strength of the received signal.

Hidden terminal problem: two stations cannot hear each other's transmissions due to physical distance or obstruction.

#### 7.2.1 CDMA

Code division multiple access(CDMA) belongs to the family of channel partitioning protocols. In a CDMA protocol, each bit being sent is encoded by multiplying the bit by a signal(the code) that changes at a much faster rate(known as the chipping rate).

### 7.3 WiFi: 802.11 Wireless LAN

#### 7.3.1 The 802.11 Architecture

The fundamental building block of the 802.11 architecture is the basic service set(BSS)/ A BSS contains one or more wireless stations and a central base station known as an access point(AP). It is often referred to as infrastructure wireless LANs when APs act as infrastructures.

Each wireless station needs to associate with an AP before it can send or receive network-layer data. A Service Set Identifier(SSID) is assigned to the access point by the network admin.

A WiFi jungle is any physical location where a wireless station receives a sufficiently strong signal from more than one APs. In 802.11, an AP periodically send beacon frames that include the AP's SSID and MAC address.

A wireless can scan channels and listen for beacon frames, known as passive scanning, but it can also perform active scanning by broadcasting a probe frame that will be received by all APs within the wireless device's range. Before association, the wireless usually authenticates itself to the AP, which is done by an authentication server.

#### 7.3.2 The 802.11 MAC Protocol

802.11 Uses a random-access protocol referred to as CSMA with collision avoidance (CSMA/CA).

The 802.11's link-layer acknowledgement scheme waits a short period of time, Short Inter-frame Spacing(SIFS) after receiving data and then sends back an acknowledgement frame.

When a station has a frame to transmit:

1. If the station senses the channel idle, it transmits the frame after a short period of time known as the Distributed Inter-frame Spacing(DIFS).
2. Otherwise, the station backs off a random amount of time using binary expoinential backoff and counts down the value after DIFS when the channel is sensed idle.
3. When counter reaches zero, the station transmits the entire frame and waits for an acknowledgemet.
4. If an ACK is received and the station has another frame to send, it begins the CSMA/CA protocol at step 2, otherwise, the transmitting will use a larger interval and re-enter step 2.

To solve the hidden terminal problem, the 802.11 protocol also allows the stations to use a short Request-to-Send(RTS) control frame and a short Clear-to-Send(CTS) to reserve access to the channel. Stations that hear the CTS frames refrain from transmitting for the time specified in the CTS frame.

#### 7.3.3 The IEEE 802.11 Frame

The 802.11 frames have payload, CRC fields, Address fields, sequence number, duration, and frame control fields.

#### 7.3.4 Mobility in the Same IP Subnet.

In the same subnet, when a host disassociates itself from a BSS and reconnect to another on (due to weakening signals), the IP address and ongoing TCP sessions are all kept.

#### 7.3.5 Advanced Features in 802.11

* Rate adaptation.
* Power Management

### 7.4 Cellular Internet Access

#### 7.4.1 An Overview of Cellular Network Architecture

Global System for Mobile Communications (GSM) standards.

* First generation (1G) system were analog FDMA systems designed exclusively for voice-only communication.
* Digial 2G systems - initially designed for voice, but later extended (2.5G) to support data.
* 3G system also supports voice and data, but with an emphasis on data capacities.
* The 4G systems are developed based on LTE technology, featuring an all-IP core network and providing integrated voice and data.

For a typical 2G system:

* Base station system (BSS) contains a base transceiver station (BTS).
* A base station controller (BSC) will service several BTS.
* A mobile switching center (MSC) plays a central role in user authorization and accounting.

#### 7.4.2 3G Cellular Data Networks: Extending the Internet to Cellular Subscribers

UMTS(Universal Mobile Telecommunications Service) 3G and 4G standards developed by the 3rd Generation Partnership project. 3G core network has two types of nodes:

* Serving GPRS support nodes (SGSNs): deliver datagrams to/from the mobile nodes in the radio access network.
* Gateway GPRS support nodes (GGSNs): act as gateways, connecting multiple SGSNs into the larger Internet.
* GPRS stands for Generalized Packet Radio Service, an early cellular data service in 2G networks.

The Radio Network Controller (RNC) controls several cell base transceiver stations.

UMTS does not use GSM's FDMA/TDMA schemes, rather a CDMA known as Direct Sequence Wideband CDMA (DS-WCDMA).

#### 7.4.3 On to 4G: LTE

4G architecture has a few important characteristics:

* A unified, all-IP network architecture.
* A clear separation of the 4G plane and 4G control plane.
* A clear separation between the radio access network, and the all-IP-core network.

The principal componenets of the 4G architecutre are as follows

* The eNodeB is the logical descendant of the 2G base stations and the 3G Radio Network controller.
* The Packet Data Network Gateway (P-GW) allocates IP addresses to the UEs (User) and performs QoS enforcement.
* The Serving Gateway (S-GW) is the data-plane mobility anchor point - all UE traffic will pass through the S-GW.
* The Mobility Management Entity (MME) performs connection and mobility management on behalf of the UEs resident in the cell it controls.
* The Home Subscriber Server (HSS) contains UE information including roaming access capacities, quality of service profiles and authentication information.

LTE uses a combination of frequency divsion multiplexing and time division multiplexing, known as orthogonal frequency division multiplexing (OFDM).

### 7.5 Mobility Management: Principles

* Home network: the permanent home of a mobile node.
* Home agent: the entity within the home network that performs the mobility management functions.
* Foreign/visited network: the network in which the mobile node is currently residing.
* Foreign agent: the entity within the foreign network that helps the mobile node with the mobility management functions.
* Correspondent: the entity wishing to communicate with the mobile node.

#### 7.5.1 Addressing

A mobile node has two addresses:

* Permanent address
* Care-of address (COA), sometimes known as a foreign address, assigned by the foreign agent.

#### 7.5.2 Routing to a Mobile Node

Indirect routing to a mobile node: the correspondent simply addresses the datagram to the mobile node's permanent address and sends the data gram into the network. The datagram is then forwarded from the agent to the mobile node.

The mobile node returns the datagram by addressing the reply directly to the correspondent.

The indirect routing has:

* A mobile-node-to-foreign-agent protocol.
* A foreign-agent-to-home-agent registration protocol.
* A home-agent datagram encapsulation protocol.
* A foreign-agent decapsulation protocol.

The indirect routing approach suffers from the triangle routing problem - datagram does not take the most efficient route. In direct routing, a correspondent agent in the correspondent's network first learns the COA of the mobile node by sending queries to the home agent, and then tunnels the datagrams directly to the mobile node's COA. It requires additional work:

* A mobile-user location protocol.
* A scheme to update the COA when a mobile agent moves.

An anchor foreign agent is the first agent found in the foreign network. New foreign agent will provide the anchor foreign agent with the mobile node's new COA and then encapsulated and forwarded to the home node.

### 7.6 Mobile IP

Mobile IP standard consists of three main pieces:

* Agent discovery: a mobile IP node arrives at a new network learns the identity of the corresponding foreign or home agent. An agent advertise its services by periodically broadcasting an ICMP message.
* Registration with the home agent: once a mobile node receives a COA, the address must be registered with the home agent, either by the foreign agent or the mobile node itself.
* Indirect routing of datagram

### 7.7 Managing Mobility in Cellular Networks

* Home network maintains a database known as the home location register (HLR), which contains the permanent cell phone number and subscriber profile information. It also has the current locations of the subscribers. A special switch known as Gateway Mobile Services Switching Center (GMSC), home MSC, is contacted when a correspondent palces a call to a mobile user.
* The visited network maintains a database known as the visitor location register (VLR) that contains an entry for each mobile user in its network.
