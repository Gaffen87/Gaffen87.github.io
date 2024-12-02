---
layout: post
title: GCPC Course 6 - Detection and Response
date: 2024-11-26 10:01 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://media.licdn.com/dms/image/v2/D5610AQGV6ogDvsWHmw/image-shrink_1280/image-shrink_1280/0/1696018945798?e=2147483647&v=beta&t=XPa5lWELqm72qw-BwtrNHWTCoGmsUIgOlJoAVFbLuQY
---

## Module 1

### Nist CSF
- Identify
- Protect
- Detect
- Respond
- Recover

### NIST Incident Response Lifecycle
- Preperation
- Detection & Analysis
- Containment, Eradication and Recovery
- Post-incident activity

### Incident
An occurrence that actually or imminently jeopardizes, without lawful authority, the confidentiality, integrity or availability of information or an information system; or constitutes a violation or imminent threat of violation of law, security policies, security procedures or acceptable use policies

### Event
An observable occurrence on a network, system or device

### The 5 W's of an incident
- Who triggered the incident
- What happened
- When the incident took place
- Where the incident took place
- Why the incident occurred

### Incident handler's journal
A form of documentation used in incident response

### Computer security incident response teams (CSIRT)
A specialized group of security professionals that are trained in incident management and response

### Roles in CSIRT
- Security analyst
- Technical lead
- Incident coordinator

### Elements of a security plan
- Policies
- Standards
- Procedures

### Incident response plan
A document that outlines the procedures to take in each step of incident response

### Elements of an incident plan
- Incident response procedures
- System information
- Other documents

### Tool types
- Detection and management tools
- Documentation tools
- Investigative tools

### Documentation
Any form of recorded content that is used for a specific purpose  
- Playbooks
- Incident handler's journal
- Policies
- Plans
- Final reports

### Playbook
A manual that provides details about any operational action

### Instrusion detection system (IDS)
An application that monitors system and network activity and produces alerts on possible intrusions

### Intrusion prevention system (IPS)
An application that monitors system activity for instrusions and take action to stop the activity

### IDS and IPS tools
- Snort
- Zeek
- Kismet
- Sagan
- Suricata

### Endpoint Detection and Response (EDR)
Monitors, records, and analyzes endpoint system activity to identify, alert, and respond to suspicious activity. Unlike IDS or IPS tools, EDRs collect endpoint activity data and perform _behavioral analysis_ to identify threat patterns happening on an endpoint

### Security Information and Event Management (SIEM) tool
An application that collects and analyzes log data to monitor critical activities in an organization

### SIEM process
1. Collect and aggregate data
2. Normalize data
3. Analyze data

### Security orchestration, automation and response (SOAR) tool
A collection of applications, tools and workflows that uses automation to respond to security events

## Modul 2

### Network traffic
The amount of data that moves across a network

### Network data
The data that's transmitted between devices on a network

### Indicators of compromise (IOC)
Observable evidence that suggests signs of a potential security incident

### Data exfiltration
Unauthorized transmission of data from a system

### Defensive measures
- Prevent attacker access
- Monitor network activity
- Protect assets
- Detect and stop exfiltration

### Components of a packet
- Header
- Payload
- Footer

### Packet capture (P-cap)
A file containing data packets intercepted from an interface or network

### **IPv4**

IPv4 is the most commonly used version of IP. There are thirteen fields in the header:

- **Version**: This field indicates the IP version. For an IPv4 header, IPv4 is used. 
    
- **Internet Header Length (IHL)**: This field specifies the length of the IPv4 header including any Options.
    
- **Type of Service (ToS)**: This field provides information about packet priority for delivery.
    
- **Total Length**: This field specifies the total length of the entire IP packet including the header and the data.
    
- **Identification**: Packets that are too large to send are fragmented into smaller pieces. This field specifies a unique identifier for fragments of an original IP packet so that they can be reassembled once they reach their destination.
    
- **Flags**: This field provides information about packet fragmentation including whether the original packet has been fragmented and if there are more fragments in transit.
    
- **Fragment Offset**: This field is used to identify the correct sequence of fragments.
    
- **Time to Live (TTL)**: This field limits how long a packet can be circulated in a network, preventing packets from being forwarded by routers indefinitely.
    
- **Protocol**: This field specifies the protocol used for the data portion of the packet.
    
- **Header Checksum**: This field specifies a checksum value which is used for error-checking the header.
    
- **Source Address**: This field specifies the source address of the sender.
    
- **Destination Address**: This field specifies the destination address of the receiver.
    
- **Options**: This field is optional and can be used to apply security options to a packet.

### **IPv6**

IPv6 adoption has been increasing because of its large address space. There are eight fields in the header:

- **Version**: This field indicates the IP version. For an IPv6 header, IPv6 is used.
    
- **Traffic Class**: This field is similar to the IPv4 Type of Service field. The Traffic Class field provides information about the packet's priority or class to help with packet delivery.
    
- **Flow Label**: This field identifies the packets of a flow. A flow is the sequence of packets sent from a specific source. 
    
- **Payload Length**: This field specifies the length of the data portion of the packet.
    
- **Next Header**: This field indicates the type of header that follows the IPv6 header such as TCP.
    
- **Hop Limit**: This field is similar to the IPv4 Time to Live field. The Hop Limit limits how long a packet can travel in a network before being discarded.
    
- **Source Address**: This field specifies the source address of the sender.
    
- **Destination Address**: This field specifies the destination address of the receiver.

## Modul 3

### Detection
The prompt discovery of security events

### Analysis
The investigation and validation of alerts

### Challenges in the detection and analysis phase
- Impossible to detect everything
- High volumes of alerts

### Pyramid of pain

![](../assets/painpyramid.png)

1. **Hash values**: Hashes that correspond to known malicious files. These are often used to provide unique references to specific samples of malware or to files involved in an intrusion.
    
2. **IP addresses**: An internet protocol address like 192.168.1.1
    
3. **Domain names**: A web address such as www.google.com 
    
4. **Network artifacts**: Observable evidence created by malicious actors on a network. For example, information found in network protocols such as User-Agent strings. 
    
5. **Host artifacts:** Observable evidence created by malicious actors on a host. A host is any device that’s connected on a network. For example, the name of a file created by malware.
    
6. **Tools**: Software that’s used by a malicious actor to achieve their goal. For example, attackers can use password cracking tools like John the Ripper to perform password attacks to gain access into an account.
    
7. **Tactics, techniques, and procedures (TTPs)**: This is the behavior of a malicious actor. Tactics refer to the high-level overview of the behavior. Techniques provide detailed descriptions of the behavior relating to the tactic. Procedures are highly detailed descriptions of the technique. TTPs are the hardest to detect.

### Benefits of documentation
- Transparency
- Standardization
- Clarity

### Chain of custody
The process of documenting evidence possession and control during an incident lifecycle

### Broken chain of custody
Inconsistencies in the collection and logging of evidence in the chain of custody

### Chain of custody establishes
 - Integrity
 - Reliability
 - Accuracy

### Types of playbooks
- Non-automated
- Automated
- Semi-automated

### Triage
The prioritizing of incidents according to their level of importance or urgency

### Triage process
1. Receive and assess
2. Assign priority
3. Collect and analyze

### Questions to ask
- Is there anything out of the ordinary?
- Are there multiple failed login attempts?
- Did the login happen outside of normal working hours?
- Did the login happen outside of the network?

### Containment
The act of limiting and preventing additional damage caused by an incident

### Eradication
The complete removal of the incident elements from all affected systems

### Recovery
The process of returning affected systems back to normal operations

### Post-incident activity phase
The process of reviewing an incident to identify areas for improvement during incident handling

### Final report
Documentation that provides a comprehensive review of an incident

### Questions to ask
- What happened?
- What time did it happen?
- Who discovered it?
- How did it get contained?
- What were the actions taken for recovery?
- What could have been done differently?

## Modul 4

### Log
A record of events that occur within an organizations systems
- Date
- Time
- Location
- Action
- Names

### Log analysis
The process of examining logs to identify events of interest

### Log types
- Network
- System
- Application
- Security
- Authentication

### Logs contain
- Timestamps
- System characteristics
- Action

### Commonly used logformats
- Syslog
- JSON
- XML
- CSV
- CEF (Common Event Format)

### Telemetry
The collection and transmission of data for analysis

### Host-based intrusion detection system
An application that monitors the activity of the host on which it's installed

### Network-based intrusion detection system
An application that collects and monitors network traffic and network data

### Signature-based analysis
A detection method used to find events of interest  

**Advantages**:

- **Low rate of false positives:** Signature-based analysis is very efficient at detecting known threats because it is simply comparing activity to signatures. This leads to fewer false positives. Remember that a **false positive** is an alert that incorrectly detects the presence of a threat.

**Disadvantages**:  
- **Signatures can be evaded:** Signatures are unique, and attackers can modify their attack behaviors to bypass the signatures. For example, attackers can make slight modifications to malware code to alter its signature and avoid detection.
- **Signatures require updates:** Signature-based analysis relies on a database of signatures to detect threats. Each time a new exploit or attack is discovered, new signatures must be created and added to the signature database.
- **Inability to detect unknown threats:** Signature-based analysis relies on detecting known threats through signatures. Unknown threats can't be detected, such as new malware families or **zero-day** attacks, which are exploits that were previously unknown.

### Anomaly-based analysis
Identifies abnormal behaviour  

**Advantages**:

- **Ability to detect new and evolving threats:** Unlike signature-based analysis, which uses known patterns to detect threats, anomaly-based analysis _can_ detect unknown threats.

**Disadvantages**:
- **High rate of false positives:** Any behavior that deviates from the baseline can be flagged as abnormal, including non-malicious behaviors. This leads to a high rate of false positives.
- **Pre-existing compromise:** The existence of an attacker during the training phase will include malicious behavior in the baseline. This can lead to missing a pre-existing attacker.
 
### Components of a NIDS rule
- Action
	- Determines the action to take if the rule criteria is met
	- Common actions: Alert, pass or reject
- Header
	- Defines the signature's network traffic
	- Source and destination IP addresses
	- Source and destination ports
	- Protocols
	- Traffic direction
- Rule options
	- Customize signatures with additional parameters

### Suricata format type
- EVE JSON
	- Extensible Event Format JSON

### Suricata log types
- Alert logs
- Network telemetry logs

### Search Processing Language (SPL)
- Splunks query language

### YARA-L
A computer language used to create rules for searching through ingested log data

### Types of search
- UDM search
- Raw log search
