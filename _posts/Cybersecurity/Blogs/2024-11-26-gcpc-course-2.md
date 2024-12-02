---
layout: post
title: GCPC Course 2 - Manage security risks
date: 2024-11-26 10:00 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://media.licdn.com/dms/image/v2/D5610AQGV6ogDvsWHmw/image-shrink_1280/image-shrink_1280/0/1696018945798?e=2147483647&v=beta&t=XPa5lWELqm72qw-BwtrNHWTCoGmsUIgOlJoAVFbLuQY
---

## Modul 1

### Security posture
An organizations ability to manage its defense of critical assets and data, and react to change

### CISSP - Security and risk management
Focused on defining security goals and objectives, risk mitigation, compliance, business continuity and legal regulations.

#### Risk mitigation:
The process of having the right procedures and rules in place to quickly reduce the impact of a risk like a breach

#### Business continuity:
An organizations ability to maintain their everyday productivity by establishing risk disaster recovery plans

### CISSP - Asset security
Focused on securing digital and physical assets. It's also related to the storage, maintenance, retention and destruction of data.

### CISSP - Security architecture and engineering
Focused on optimizing data security by ensuring effective tools, systems and processes are in place to protect an organizations assets and data.

#### Shared responsibility
All individuals within an organization take an active role in lowering risk and maintaining both physical and virtual security.

### CISSP - Communication and network security
Focused on managing and securing physical networks and wireless communications.

### CISSP - Identity and access management (IAM)
Focused on access and authorization to keep data secure, by making sure users follow established policies to control and manage assets.

#### Components of IAM
- Identification
- Authentication
- Authorization
- Accountability

### CISSP - Security assessment and testing
Focused on conducting security control testing, collecting and analyzing data, and conducting security audits to monitor for risks, threats and vulnerabilities

### CISSP - Security operations
Focused on conducting investigations and implementing preventative measures.

### CISSP - Software development security
Focused on using secure coding practices

### Threat
Any circumstance or event that can negatively impact assets.

### Risk
Anything that can impact the confidentiality, integrity and availability of an asset

### Low-risk asset
Information that would now harm the organizations reputation or ongoing operations, and would not cause financial damage if compromised.

### Medium-risk asset
Information that's not available to the public and may cause some damage to the organizations finances, reputation or ongoing operations.

### High-risk asset
Information protected by regulations or laws, which if compromised would have severe negative impact on an organizations finances, reputation or ongoing operations.

### Vulnerability
A weakness that can be exploited by a threat

### Ransomware
A malicious attack where threat actors encrypt an organizations data and demand payment to restore access.

### Layers of the web
- Surface web
- Deep web
- Dark web

### Key impacts of threats, risks and vulnerabilities
- Financial
- Identity theft
- Reputation

### NIST Risk Management Framework (RMF)
- #### Prepare
	- Activities that are necessary to manage security and privacy risks before a breach occurs
- #### Categorize
	- Used to develop risk management processes and tasks
- #### Select
	- Choose, customize and capture documentation of the controls that protect an organization
- #### Implement
	- Implement security and privacy plans for the organization
- #### Assess
	- Determine if established controls are implemented correctly
- #### Authorize
	- Being accountable for the security and privacy risks that may exist in an organization
- #### Monitor
	- Be aware of how systems are operating.


## Modul 2

### Security Frameworks
Guidelines used for building plans to help mitigate risk and threats to data and privacy

### Security Controls
Safeguards designed to reduce specific security risks

### Encryption
The process of converting data from a readable format to an encoded format

### Authentication
The process of verifying who someone or something is  
- Biometrics
	Unique physical characteristics that can be used to verify a persons identity
	- Vishing
		The exploitation of electronic voice communication to obtain sensitive information or to impersonate a known source

### Authorization
The concept of granting access to specific resources within a system

### Cyber Threat Framework (CTF)
Developed by U.S. government to provide a common language for decribing and communicating information about cyber threat activity.

### International Organization for Standardization (ISO) 27001
Internationally recognized and used framework. The ISO 27000 family of standards enables organizations of a ll sectors and sizes to manage the security assets, such as financial information, intellectual property, employee data and information entrusted to third parties. This framework outlines requirements for and information security management system, best practices and controls that support an organizations ability to manage risks.

### Examples of security controls
- Physical controls
	- Gates, fences and locks
	- Security guards
	- CCTV, surveillance cameras
	- Access cards or badges
- Technical controls
	- Firewalls
	- MFA (Multifactor auth)
	- Antivirus software
- Administrative controls
	- Separation of duties
	- Authorization
	- Asset classification

### CIA Triad
A model that helps inform how organizations consider risk when setting up systems and security policies  
- Confidentiality:
		Only authorized users can access specific assets or data
- Integrity:
		The data is correct, authentic and reliable
- Availablity:
		Data is accesible to those who are authorized to access it


### NIST Cybersecurity Framework (CSF)
A voluntary framework that consists of standards, guidelines and best practices to manage cybersecurity risk
5 important core functions:
- #### Identify
	- The management of cybersecurity risk and its effect on an organizations people and assets
- #### Protect
	- The strategy used to protect an organization through the implementation of policies, procedures, training and tools that help mitigate cybersecurity threats
- #### Detect
	- Identifying potential security incidents and improving monitoring capabilities to increase the speed and efficiency of detections
- #### Respond
	- Making sure that the proper procedures are used to contain, neutralize and analyze security incidents and implement improvements to the security process
- #### Recover
	- The process of returning affected systems back to normal operation

### NIST S.P. 800-53
A unified framework for protecting the security of information systems within the federal government


### OWASP security principles
- #### Minimize attack surface area
		Attack surface refers to all potential vulnerabilites a threat actor could exploit
- #### Principle of least privilige
		Users have the least amount of access required to perform their everyday tasks
- #### Defense in depth
		Organizations should have varying security controls that mitigate risks and threats
- #### Separation of duties
		Critical actions should rely on multiple people, each of whom follow the principle of least privilige
- #### Keep security simple
		Avoid unnecessarily complicated solutions. Complexity makes security difficult
- #### Fix security issues correctly
		When security incidents occur, identify the root cause, contain the impact, identify culnerabilites and conduct tests to ensure that remediation is successful


### Additional OWASP principles
- #### Establish secure defaults
		The optimal security state of an application is also its default state for users
- #### Fail securely
		When a control fails or stops, it should do so by defaulting to its most secure option.
- #### Don't trust services
		An organization shouldn't ecplicitly trust that their partners systems are secure.
- #### Avoid security by obscurity
		The security of key systems should not rely on keeping details hidden


### Security audit
A review of an organizations security controls, policies and procedures against a set of expectations. 2 types: external and internal.  
- Purpose of internal security audits:
	- Identify organizational risk
	- Assess controls
	- Correct compliance issues
- Common elements of internal audits:
	- Establishing the scope and goals
	- Conducting a risk assessment
	- Completing a controls assessment
	- Assessing compliance
	- Communicating results

#### Scope 
refers to the specific criteria of an internal security audit

#### Goals
are an outline of the organizations security objectives

### Audit questions
- What is the audit meant to achieve?
- Which assets are most at risk?
- Are current controls sufficient to protect those assets?
- What controls and compliance regulations need to be implemented?

### Security control categories
- Administrative controls
- Technical controls
- Physical controls

### Examples of security control types
- Preventative, designed to prevent an incident from occuring
- Corrective, used to restore an asset after an incident
- Detective, implemented to determine if an incident has occured
- Deterrent, designed to discourage attacks


### Stakeholder communication
- Summarizes scope and goals
- Lists existing risks
- Notes how quickly those risks need to be addressed
- Identifies compliance regulations
- Provides recommendations

## Modul 3

### Log
A record of events that occur within an organizations systems and networks

### Common log sources
- #### Firewall logs
	- A record of attempted or established connections for incoming traffic from the internet. It also includes outbound requests to the internet from within the network.
- #### Network logs
	- A record of all computers and devices that enter and leave the network. It also records connections between devices and services on the network
- #### Server logs
	- A record of events related to services, such as websites, emails or file shares. It includes actions such as login, password and username requests

### Security information and event management (SIEM)
An application that collects and analyzes log data to monitor critical activities in an organization.

### Metrics
Key technical attributes, such as response time, availability and failure rate, which are used to assess the perfomance of a software application.


### Types of SIEM tools
- Self-hosted
	- Ideal when an organization is required to maintain physical control over confidential data.
- Cloud-hosted
	-  Ideal for organizations that don't want to invest in creating and maintaining their own infrastructure
- Hybrid

### Splunk Enterprise
A self-hosted tool used to retain, analyze and search an organizations log data to provide security information and alerts in real-time.

### Splunk Cloud
A cloud-hosted tool used to collect, search and monitor log data.

### Google Chronicle
A cloud-native tool designed to retain, analyze and search data.

## Modul 4

### Playbook
A manual that provides details about any operational action

### Incident reponse
An organizations quick attempt to identify an attack, contain the damage and correct the effects of a security breach

### Incident response playbook phases
- #### Preparation
	- Before incidents occur, mitigate potential impacts on the organization by documenting, establishing staffing plans and educating users.
- #### Detection and analysis
	- Detect and analyze events by implementing defined processes and appropriate technology
- #### Containment
	- Prevent further damage and reduce immediate impact of incidents
- #### Eradication and recovery
	- Completely remove artifacts of the incident so that an organization can return to normal operations
- #### Post-incident activity
	- Document the incident, inform organizational leadership and apply lessons learned
- #### Coordination
	- Report incidents and share information throughout the response process, based on established standards

### Security orchestration, automation and response (SOAR) tool
A piece of software used to automate repetitive tasks generated by tools such as a SIEM or managed detection and response(MDR)
