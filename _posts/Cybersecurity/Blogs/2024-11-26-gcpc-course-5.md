---
layout: post
title: GCPC Course 5 - Assets, threats and vulnerabilities
date: 2024-11-26 10:01 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://media.licdn.com/dms/image/v2/D5610AQGV6ogDvsWHmw/image-shrink_1280/image-shrink_1280/0/1696018945798?e=2147483647&v=beta&t=XPa5lWELqm72qw-BwtrNHWTCoGmsUIgOlJoAVFbLuQY
---

## Modul 1

### Risk
Anything that can impact the confidentiality, integrity or availability of an asset

### Security risk planning
- Assets
- Threats
- Vulnerabilities

### Asset
An item perceived as having value to an organization

### Threat
Any circumstance or event that can negatively impact assets

### Vulnerability
A weakness that can be exploited by a threat

### Likelihood * Impact = Risk

### Asset management
The process of tracking assets and the risks that affect them

### Asset inventory
A catalog of assets that need to be protected

### Asset classification
The practice of labeling assets based on sensitivity and importance to an organization

### Levels of asset classification
- Public
	- is the lowest level of classification. These assets have no negative consequences to the organization if they’re released
- Internal-only
	- describes assets that are available to employees and business partners
- Confidential
	- refers to assets whose disclosure may lead to a significant negative impact on an organization
- Restricted
	- is the highest level. This category is reserved for incredibly sensitive assets,  like need-to-know information


### Data
Information that is translated, processed or stored by a computer

### States of data
- In use
	- Data being accessed by on or more users
- In transit
	- Data traveling from on point to another
- At rest
	- Data not currently being accessed

### Information security (InfoSec)
The practice of keeping data in all states away from unauthorized users

### Types of risk categories
- Damage
- Disclosure
- Loss of information

### Elements of a security plan
- Policies
	- A set of rules that reduces risk and protects information
- Standards
	- References that inform how to set policies
- Procedures
	- Step-by-step instructions to perform a specific security task

### Compliance
The process of adhering to internal standards and external regulations

### Regulations
Rules set by a government or other authority to control the way something is done

### NIST Cybersecurity Framework (CSF)
A voluntary framework that consists of standards, guidelines and best practices to manage cybersecurity risk

### NIST CSF components
- #### Core
	- 5 functions:
		- Identify
		- Protect
		- Detect
		- Respond
		- Recover
- Tiers
	- Levels 1-4 (1, lowest - 4, highest)
	- level 1 - passive
	- level 4 - adaptive
- Profiles
	- pre-made templates, developed by a team of industry experts. Tailored to address the specific risks of an organization or industry. Used to help develop a baseline


### Security controls
Safeguards designed to reduce specific security risks

### Types of security controls
- Technical
	- Encryption, authentication systems
- Operational
	- Awareness training, incident response
- Managerial
	- Policies, standards and procedure

### Information privacy
The protection of unauthorized access and distribution of data

### Principle of least privilege
The concept of granting only the minimal access and authorization required to complete a task or function

### Data governance
A set of processes that define how an organization manages information

### Data owner
The person that decides who can access, edit, use or destroy their information

### Data custodian
Anyone or anything that's responsible for the safe handling, transport and storage of information

### Data steward
The person or group that maintains and implements data governance policies set by an organization

### Data lifecycle
- Collection
- Storage
- Usage
- Archival
- Destruction

### PII
Personally identifiable information
	Any information that can be used to infer an individual's identity

### PHI
Protected health information

### SPII
Sensitive personally identifiable information

## Modul 2

### Cryptography
The process of transforming information into a form that unintended readers can't understand

### Cipher
An algorithm that encrypts information

### Brute force attack
A trial and error process of discovering private information

### Public Key Infrastructure (PKI)
An encryption framework that secures the exchange of information online  
Process:  
	1. Exchange of encrypted information
	2. Establish trust using a system of digital certificates

### Asymmetric encryption
The use of a public and private key pair for encryption and decryption of data

### Symmetric encryption
The use of a single secret key to exchange information

### Digital certificate
A file that verifies the identity of a public key holder

### Hash function
An algorithm that produces a code that can't be decrypted

### Non-repudiation
The concept that the authenticity of information can't be denied

### Access controls
Security controls that manage access, authorization and accountability of information

### AAA framework
- Authentication
- Authorization
- Accounting

### Factors of authentication
1. Knowledge: something the user knows
2. Ownership: something the user possesses
3. Characteristics: something the user is

### Single sign-on (SSO)
A technology that combines several different logins into one

### LDAP
Lightweight Directory Access Protocol

### SAML
Security Assertion Markup Language

### Basic auth
The technology used to establish a user's request to access a server
Transmits username and password openly over network

### OAuth
An open-standard authorization protocol that shares designated access between applications

### API token
A small block of encrypted code that contains information about a user

### Session
A sequence of network HTTP basic auth requests and responses associated with the same user

### Session ID
A unique token that identifies a user and their device while accessing the system

### Session cookie
A token that websites use to validate a session and determine how long that session should last

### Session hijacking
An event when attackers obtain a legitimate user's session ID

### Identity and access management (IAM)
A collection of processes and techs that helps organizations manage digital identities in their environment

### User provisioning
The process of creating and maintaining a user's digital identity

### Mandatory Access Control (MAC)
Authorization is based on a strict need-to-know basis. Access to information must be granted manually by a central authority or system administrator. Non-discretionary control.

### Discretionary Access Control (DAC)
When a data owner decides appropriate levels of access. fx when the owner of a Google Drive folder shares editor, viewer or commentor access.

### Role-Based Access Control
Used when authorization is determined by a user's role.

## Modul 3

### Vulnerability
A weakness that can be exploited by a threat

### Exploit
A way of taking advantage of a vulnerability

### Vulnerability management
The process of finding and patching vulnerabilities  
1. Identify vulnerabilities
2. Consider potential exploits
3. Prepare defenses against threats
4. Evaluate those defenses

### Zero-day
An exploit that was previously unknown

### Defense in depth (Castle approach)
A layered approach to vulnerability management that reduces risk  
1. Perimeter layer
	- like authentication systems that validate user access
2. Network layer
	- which is made up of technologies like network firewalls and others
3. Endpoint layer
	- which describes devices on a network, like laptops, desktops, or servers
4. Application layer
	- which involves the software that users interact with
5. Data layer
	- which includes any information that’s stored, in transit, or in use


### Exposure
A mistake that can be exploited by a threat

### Common Vulnerabilites and Exposures list (CVE list)
An openly accesible dictionary of known vulnerabilites and exosures

### MITRE
A collection of non-profit research and development centers

### CVE Numbering Authority (CNA)
An organization that volunteers to analyze and distribute information on eligible CVEs

### CVE list criteria
1. Independent of other issues
2. Recognized as a potential security risk
3. Submitted with supporting evidence
4. Only affect one codebase

### Common Vulnerability Scoring System (CVSS)
A measurement system that scores severity of a vulnerability

### Vulnerability assessment
The internal review process of an organizations security systems  
1. Identification
2. Vulnerability analysis
3. Risk assessment
4. Remediation

### Simulating threats
- Proactive simulations
	- assume the role of an attacker by exploiting vulnerabilities and breaking through defenses. This is sometimes called a red team exercise.
- Reactive simulations 
	- assume the role of a defender responding to an attack. This is sometimes called a blue team exercise.

### Attack vectors
The pathway attackers use to penetrate security defenses

### Practicing an attacker mindset
1. Identify a target
2. Determine how the target can be accessed
3. Evaluate attack vectors that can be exploited
4. Find the tools and methods of attack

### Defending attack vectors
1. Educating users
2. Applying the principle of least privilege
3. Using the right security controls and tools
4. Building a diverse security team

## Modul 4

### Social engineering
A manipulation technique that ecploits human error to gain private information, access or valuables  
1. Prepare
2. Establish trust
3. Use persuasion tactics
4. Disconnect from the target

### Prevent social engineering
- Implementing managerial controls
- Staying informed of trends
- Sharing your knowledge with others

### Phishing
The use of digital communications to trick people into revealing sensitive data or deploying malicious software

### Phishing kit
A collection of software tools needed to launch a phishing campaign  
Tools:  
- Malicious attachments
- Fake data-collection forms
- Fraudulent web links

### Smishing
The use of text messages to obtain sensitive information or to impersonate a known source

### Vishing 
The exploitation of electronic voice communication to obtain sensitive information or impersonate a known source

### Phishing security measures
- Anti-phishing policies
- Employee training resources
- Email filters
- Intrusion prevention systems

### Malware
Software designed to harm devices or networks

### Types of malware
- Virus
	- Malicious code written to interfere with computer operations and cause damage to data and software. Must be activited by the user
- Worm
	- Malware that can duplicate and spread itself across systems on its own
- Trojan
	- Malware that looks like a legitimate file or program
- Ransomware
	- Type of malicious attack where attackers encrypt an organizations data and demand payment to restore access
- Spyware
	- Malware that's used to gather and sell information without consent

### Cryptojacking
A form of malware that installs software to illegally mine cryptocurrencies

### Intrusion detection systems (IDS)
An application that monitors system activity and alerts on possible intrusions

### Signs of cryptojacking
- Slowdown
- Increased CPU usage
- Sudden system crashes
- Fast draining batteries
- Unusually high electricity costs

### Web-based exploits
Malicious code or behaviour that's used to take advantage of coding flaws in a web application

### Injection attack
Malicious code inserted into a vulnerable application

### Cross-site scripting (XSS)
An injection attack that inserts code into a vulnerable website or web application

### Types of cross-site scripting attacks
- Reflected
	- An instance when malicious script is sent to a server and activated during the server's response
- Stored
	- An instance when malicious script is injected directly on the server
- DOM-based
	- An instance when malicious script exists in the webpage a browser loads

### SQL injection
An attack that executes unexpected queries on a database  
- In-band SQL injection
	- Uses the same communication channel to launch the attack
- Out-of-band SQL injection
	- Uses a different communication channel to launch the attack
- Inferential SQL injection
	- When an attacker is unable to directly see the result of their attack. Instead they interpret the results by analyzing the behaviour of the system

### Prepared statement
A coding technique that executes SQL statements before passing them on to the database

### Threat modeling
The process of identifying assets, their vulnerabilites and how each is exposed to threats

### Threat modeling steps
1. Define the scope
2. Identify threats
3. Characterize the environment
4. Analyze threats
5. Mitigate risks
6. Evaluate findings

### Attack tree
A diagram that maps threats to assets

### Process for Attack Simulation and Threat Analysis (PASTA)
A popular threat modeling framework that's used across many industries
1. Define business and security objectives
2. Define the technical scope
3. Decompose the application
4. Perform a threat analysis
5. Perform a vulnerability analysis
6. Conduct attack modeling
7. Analyze risk and impact

### Common threat modeling frameworks
- STRIDE
- PASTA
- Trike
- VAST
