# Reconaissance and Asset Discovery
The first thing you should do when looking at a new target is to perform reconaissance. This is the first and most important step as it allows you to gain a general overview of the attack surfaces, what the assets are and the functionality of the application and the technologies that may be used. Knowing this kind of information allows you to pinpoint what parts of the application may be vulnerable as well as being able to make better decisions of what vulnerabilties may be present in the application itself.

### DNS and Subdomains
In many cases you may be provided with a scope consisting of just a domain name. In these cases there may be multiple subdomains for this domain other than the ones publicly available. These subdomains are generally hidden and thus you will have to find them. We want to find these subdomains as each one is another asset and may provide a new application or functionality that increases the attack surface. Most hidden subdomains that aren't publicly available will also generally contain staging or development environments, admin consoles or other applications that aren't meant for general user access.

##### DNS and Reverse DNS Lookup
A reverse IP lookup is when you provide a domain name (with or without a subdomain) and it returns the IP address

- [yougetsignal](https://www.yougetsignal.com/tools/web-sites-on-web-server/)

##### Subdomain Brute Force
In 

#### Other Resources

- [DNS Hacking](https://resources.infosecinstitude.com/dns-hacking/)
- [Discovering Subdomains](https://www.bugcrowd.com/discovering-subdomains/)

### Port Scan
This is one of the first things you should try when you come across a new IP. It will allow you to check what ports are open which can give you a good idea of what other services may be running. This is great as some services may already have known vulnerabilities. This will also let you increase the attack surface you have access to as browsers generally only use http/https. 

##### nmap
[nmap](https://nmap.org) is a tool that allows you to quickly and easily perform a portscan by specifying a domain name or an ip address. Basic usage can be done with `nmap [domain/ip]`. In order to get information about what services may be running on a port use the -sV flag.

### Application Layout/Funtionality

Spidering

### Directory's & Files
This also includes routes and endpoints for API's

##### Common Files
- robots.txt
- .git
- phpinfo.php

[DVCS-Pillage](https://github.com/evilpacket/DVCS-Pillage)
[truffleHog](https://github.com/dxa4481/truffleHog)

### WordLists
Word lists are required for all types of brute forcing, however using the correct word list is extremely important as it can increase the hit rate of the brute force as well as decrease the time it takes to complete. It is ideal to use a wordlist that is targeted towards not only the application you are trying to brute force but also the objective of the brute force. 

For example when brute forcing files and directories it would be preferred to include common files and routes in the word list. This is also the same for credentials, it is common sense to try the most common passwords as this increases your chance of being successful.

[Seclists](https://github.com/danielmiessler/SecLists) is a repository that contains multiple wordlists each with their own specific target use. While word lists like this are extremely useful, you should also update and include additional words into these lists so that the list are better suited to your target.

### Links to Tools
- [goBuster](https://github.com/OJ/gobuster) DNS & Directory/File Brute Force
- [Burp Suite](https://portswigger.net/bup)
- [subbrute]() - Subdomain brute force tool. 
- [altdns]() - Subdomain brute force using permutions of a given wordlist.
- [goBuster](https://github.com/OJ/gobuster) - DNS & Directory/File Brute Force
