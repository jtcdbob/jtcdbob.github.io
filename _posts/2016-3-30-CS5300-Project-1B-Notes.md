---
title:  "CS5300 Project 1B"
excerpt: "Notes for working on CS5300 Project 1B"
categories:
  - Blog
tags:
  - CODE_DEBUG_LIFE
use_math: true
---

## Overview of the solution
What we will need to complete the homework:

+ Servlets for processing client requests
+ A distributed session state database analogous to __the SSM system__
+ A "bootstrapping" protocol for new server instances to register themselves in SimpleDB
+ A "reboot" protocol for a crashed instance to rejoin the group

## 3.1 EC2 Bootstrapping: User Data and Instance Metadata
Write a server "installation script" that is responsible for

1. Install the Tomcat server, application code, and any other software the server will need.
2. Determine the internal IP address of the instance.
3. Determine the instance's ami-launch-index for use as a server ID.
4. Upload the internal IP address to SimpleDB at a domain + item + attribute name computed from the ami-launch-index.
5. Download the internal IP addresses of all the other EC2 instances from SimpleDB and store them in the file system.
6. Start the Tomcat server running my application.

For AWS EC2:

+ User data shell scripts must start with the #! characters and the path to the interpreter you want to read the script (commonly /bin/bash).
+ Scripts entered as user data are executed as the root user, so do not use the `sudo` command in the script.
+ To start an instance: select Oregon as region, start using launch-wizard-1 as security group and use existing kay pairs.
+ To connect to an instance, just do<br/>
`sudo ssh -i "kay-pair" ec2-user@ec2-**-**-**-**.us-west-2.compute.amazonaws.com`
<br />
! Do NOT change username, it is `ec2-user`.
+ To scp local file to remote server:<br/>
`scp -i "kay-pair" filename ec2-user@ec2-***.us-west-2.compute.amazonaws.com:~/filename`
+ SimpleDB does not exist in console (it was hidden by amazon, somewhat intentionally). It only works with API.

For TomCat8:

+ Its local path is usually `/Library/Tomcat` (if it is set up as tutorial).
+ Its path on AWS is `/usr/share/tomcat7`.xit

Script:

```
#!/bin/bash
# Update YUM
yum update
# Install JAVA 1.8.0 (to run my script)
yum install java-1.8.0
# Remove JAVA 1.7.0
sudo yum remove java-1.7.0-openjdk
# install TomCat8 Server
yum install tomcat8-webapps tomcat8-docs-webapp tomcat8-admin-webapps

# Application code
Retrieve from sc2

# For ami-launch-index
curl http://169.254.169.254/latest/meta-data/ami-launch-index >> ~/local_info
echo >> ~/local_info
# For private IP address of the instance (wget for Windows)
curl http://169.254.169.254/latest/meta-data/local-ipv4 >> ~/local_info
# For public IP address of the instance
# curl http://169.254.169.254/latest/meta-data/public-ipv4


## List all SimpleDB domains
# aws sdb create-domain --domain-name "cs5300"
# aws sdb list-domains

## Upload the internal IP address to SimpleDB
# aws sdb put-attributes --domain-name test --item-name="1" --attributes Name="2",Value="Hello again"

## Download all the other internal IP address from simpleDB
# aws sdb get-attributes --domain-name test --item-name="ip"
# aws sdb get-attributes --domain-name test --item-name="1" --attribute-names="1"

# Start the Tomcat Server
service tomcat8 start
```

## 3.2 Crash and Reboot
The running system must be at least 1-resilient. There is no explicit recovery protocol after a failure. ["Crash-only"](https://www.usenix.org/legacy/events/hotos03/tech/full_papers/candea/candea.pdf "Described in this paper") philosophy.

Reboot an instance:

```
reboot-instances
[--dry-run | --no-dry-run]
--instance-ids <value>
[--cli-input-json <value>]
[--generate-cli-skeleton]
```

## 3.3 Outline of the SSM Protocol
[SSM Paper](http://research.microsoft.com/pubs/74713/ssm-nsdi.pdf "Operation of the SSM System")


$$
1 \le R \le WQ \le W \le N
$$
where $N$ is number of bricks. $R$ is the read group size and $W$ is the write group size. $WQ$ is the minimum number of bricks that must retrun "success" to the stub before the stub returns to the caller. ($WQ-1$ is the number of simultaneous brick failures that the system can tolerate before potentially losing data.)

A client stub sends read request to $R$ bricks and uses the first response it receives.

A client stub sends write request to $W$ bricks and waits for $WQ$ responses, then update the cookie metadata to the set of $WQ$ that respond.

## 3.4 Server/Session Identifiers and Session Cookies

### Session ID
Each server should have an ID (`SvrID`), which can be `ami-launch-index` of the instance. Use this id to find the server's internal IP address and then communicate with it.<br />
And `sess_num` is incremented whenever a new session is created by this server.
<br />
To make things easier:
```
SessID = <SvrID, reboot_num, sess_num>
```

### Session Version Number
A per-session number that is incremented for every request within the session.

### Session Cookies
A `CS5300PROJ1SESSION` cookie will be sent with each client request in an existing session. It will contain the `SessID` and Session Version Number. It also needs some "location metadata" into the session cookie.

## 3.5 Remote Procedure Call (RPC) Communication
Use User Datagram Protocol (UDP). RPC servers should all listen at the same well-known port number.

## 3.6 Retrieving Session State

## 3.7 Storing Session State

## 3.8 Creating New Sessions

## 3.9 Implementing Session Timeouts

## 3.10 Garbage Collection
