# Recon
Reconnaissance is the first step for any successful attack. 

### DNS Reconnaissance
Generally you are provided a scope consisting of just a domain name.

###### Subdomains

### Port Scan
This is one of the first things you should try when you come across a new IP. It will allow you to check what ports are open which can give you a good idea of what other services may be running. This is great as some services may already have known vulnerabilities. This will also let you increase the attack surface you have access to as browsers inherently onyl use http/https. 

###### nmap
nmap is a tool that allows you to quickly and easily perform a portscan. -sV flag.

`nmap [domain/ip]`

### Directory's & Files
This also includes routes and endpoints for API's

###### Common Files
- robots.txt
- .git
- phpinfo.php

### WordLists
- seclists

### Tools
- nmap -p [domain/ip]
- [goBuster](https://github.com/OJ/gobuster) DNS & Directory/File Brute Force
- Burp Suite
- [subbrute] - Subdomain brute force tool. 
- [altdns]() - Subdomain brute force using permutions of a given wordlist.
- [goBuster](https://github.com/OJ/gobuster) - DNS & Directory/File Brute Force
