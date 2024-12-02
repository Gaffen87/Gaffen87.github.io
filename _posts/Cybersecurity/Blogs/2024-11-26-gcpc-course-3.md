---
layout: post
title: GCPC Course 3 - Networks and network security
date: 2024-11-26 10:01 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://media.licdn.com/dms/image/v2/D5610AQGV6ogDvsWHmw/image-shrink_1280/image-shrink_1280/0/1696018945798?e=2147483647&v=beta&t=XPa5lWELqm72qw-BwtrNHWTCoGmsUIgOlJoAVFbLuQY
---

## Modul 1

### Network
A group of connected devices

### Local Area Network (LAN)
A Network that spans a small area like an office building, a school or a home

### Wide Area Network (WAN)
A network that spans a large geographic area like a city, state og country

### Hub
A network device that broadcasts information to every device on the network

### Switch
A device that makes connections between specific devices on a network by sending and recieving data between them

### Router
A network device that connects multiple networks together

### Modem
A device that connects your router to the internet and brings internet access to the LAN

### Virtualization tools
Pieces of software that perform network operations

### Cloud computing
The practice of using remote servers, applications and network services that are hosted on the internet instead of on local physical devices

### Cloud network
A collection of servers or computers that stores resources and data in remote data centers that can be accessed via the internet

### Cloud service providers offer
- On-demand storage
- Processing power
- Analytics

### Categories of cloud service providers:
- Software as a service (SaaS)
	- refers to software suites operated by the CSP that a company can use remotely without hosting the software.
- Infrastructure as a Service (IaaS)
	- refers to the use of virtual computer components offered by the CSP.
- Platform as a Service (PaaS)
	- refers to tools that application developers can use to design custom applications for their company


### Data packet
A basic unit of information that travels from one device to another within a network  
Contains:  
- Header
	- IP adress / MAC address / Protocol number
- Body
	- Message that needs to be transmitted
- Footer
	- Signals to the recieving device that the packet is finished


### Bandwidth
The amount of data a device receives every second

### Speed
The rate at which data packets are received of downloaded

### Packet sniffing
The practice of capturing and inspecting data packets across a network

### Transmission Control Protocol (TCP)
An internet communication protocol that allows two devices to form a connection and stream data

### Internet protocol (IP)
A set of standards used for routing and addressing data packets as they travel between devices on a network

### Port
A software-based location that organizes the sending and receiving of data between devices on a network

### TCP/IP model
A framework used to visualize how data is organized and transmitted across the network  

#### 4 layers:
1. Network access layer
	- The network access layer, sometimes called the data link layer, deals with the creation of data packets and their transmission across a network. This layer corresponds to the physical hardware involved in network transmission. Hubs, modems, cables, and wiring are all considered part of this layer.
2. Internet layer
	- The internet layer, sometimes referred to as the network layer, is responsible for ensuring the delivery to the destination host, which potentially resides on a different network. It ensures IP addresses are attached to data packets to indicate the location of the sender and receiver. The internet layer also determines which protocol is responsible for delivering the data packets and ensures the delivery to the destination host.
1. Transport layer
	- The transport layer is responsible for delivering data between two systems or networks and includes protocols to control the flow of traffic across a network. TCP and UDP are the two transport protocols that occur at this layer.
1. Application layer
	- The application layer in the TCP/IP model is similar to the application, presentation, and session layers of the OSI model. The application layer is responsible for making network requests or responding to requests. This layer defines which internet services and applications any user can access.

### Internet protocol (IP) address
A unique string of characters that identifies the location of a device on the internet
- IP version 4 (IPv4)
	- fx. 19.117.63.126
- IP version 6 (IPv6)
	- 684D:1111:222:3333:4444:5555:6:77

### Mac address
A unique alphanumeric identifier that is assigned to each physical device on a network

## Module 2

### Network protocols
A set of rules used by two or more devices on a network to describe the order of delivery and the structure of the data

### Address Resolution Protocol (ARP)
A network protocol used to determine the MAC address of the next router or device on the path

### HyperText Transfer Protocol Secure (HTTPS)
A network protocol that provides a secure method of communication between clients and website servers

### Domain Name System (DNS)
A network protocol that translates internet domain names into IP addresses

### Security protocols
- HTTPS
- SSL/TLS

### IEEE 802.11 (WiFi)
A set of standards that define communication for wireless LANs

### WiFi Protected Access (WPA)
A wireless security protocol for devices to connect to the internet

### Firewall
A network security device that monitors traffic to and from your network

### Port filtering
A firewall function that blocks or allows certain port numbers to limit unwanted communication

### Cloud-based firewalls
Software firewalls that are hosted by a cloud service provider

### Stateful firewall
A class of firewall that keeps track of information passing through it and proactively filters out threats

### Stateless firewall
A class of firewall that operates based on predefined rules and does not keep track of information from data packets

### Next generation firewalls (NGFWs)
- Deep packet inspection
- Intrusion protection
- Threat intelligencs

### Virtual Private Network (VPN)
A network security service that changes your public IP address and hides your virtual location so that you can keep your data private when you are using a public network like the internet
Encrypts data and performs encapsulation on data in transit.
Uses a VPN tunnel

### Encapsulation
A process performed by a VPN service that protects your data by wrapping sensitive data in other data packets

### Security zone
A segment of a network that protects the internal network from the internet

### Network segmentation
A security technique that divides the network into segments

### Uncontrolled zone
Any network outside of the organizations control

### Controlled zone
A subnet that protects the internal network from the uncontrolled zone

### Areas in the controlled zone
- #### Demilitarized zone (DMZ)
- #### Internal network
- #### Restricted zone

### Subnetting
The subdivision of a network into logical groups called subnets. It works like a network inside a network

### Proxy server
A server that fulfills the requests of a client by forwarding them on to other servers

### Forward proxy server
Regulates and restricts a persons access to the internet

### Reverse proxy server
Regulates and restricts the internets access to an internal server

### Email proxy server
Filters spam email by verifying wether a senders address was forged

### Categories of network protocols
- Communication protocols
	- Used to establish connections between servers. Examples include TCP, UDP, and Simple Mail Transfer Protocol (SMTP), which provides a framework for email communication
- Management protocols
	- Used to troubleshoot network issues. One example is the Internet Control Message Protocol (ICMP)
- Security protocols
	- Provide encryption for data in transit. Examples include IPSec and SSL/TLS


## Module 3

### Common network intrusion attacks
- Malware
- Spoofing
- Packet sniffing
- Packet flooding

### Attacks can harm an organization by
- Leaking valuable or confidential information
- Damaging an organizations reputation
- Impacting customer retention
- Costing money and time

### Denial of service attack (DoS)
An attack that targets a network or server and floods it with network traffic

### Distributed DoS
A type of denial of service attack that uses multiple devices or servers in different locations to flood the target network with unwanted traffic

### SYN flood attack
A type of DoS attack that simulates a TCP connection and floods a server with SYN packets

### Internet Control Message Protocol (ICMP)
An internet protocol used by devices to tell each other about data transmission errors across the network

### ICMP flood attack
A type of DoS attack performed by an attacker repeatedly sending ICMP packets to a network server

### Ping of death attack
A type of DoS attack caused when a hacker pings a system by sending it an oversized ICMP packet that is bigger than 64kb

### Passive packet sniffing
A type of attack where data packets are read in transit

### Active packet sniffing
A type of attack where data packets are manipulated in transit

### IP spoofing
A network attack performed when an attacker changes the source IP of a data packet to impersonate an authorized system and gain access to a network

- On-path attack
	- An attack where a malicious actor places themselves in the middle of an authorized connection and intercepts or alters the data in transit
- Replay attack
	- A network attack performed when a malicious actor intercepts a data packet in transit and delays it or repeats it at another time
- Smurf attack
	- A network attack performed when an attacker sniffs an authorized users IP address and floods it with packets


## Modul 4

### Security hardening
The process of strengthening a system to reduce its vulnerability and attack surface  
Conducted on:  
- Hardware
- Operating systems
- Applications
- Computer networks
- Databases

### Attack surface
All the potential vulnerabilities that a threat actor could exploit

### Penetration test
A simulated attack that helps identify vulnerabilities in systems, networks, websites, applications and processes

### Baseline configuration (baseline image)
A documented set of specifications within a system that is used as a basis for future builds, releases and updates

### Network security hardening
- Port filtering
- Network access privilege
- Encryption

### Regular tasks
- Firewall rules maintenance
- Network log analysis
- Patch updates
- Server backups

### Port filtering
A firewall function that blocks or allows certain port numbers to limit unwanted communication

### Cloud network
A collection of servers or computers that stores resources and data in remote data centers that can be accessed via the internet

