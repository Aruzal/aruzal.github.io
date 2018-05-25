# Reconaissance and Asset Discovery
The first thing you should do when looking at a new target is to perform reconaissance. This is the first and most important step as it allows you to gain a general overview of the attack surfaces, what the assets are and the functionality of the application and the technologies that may be used. Knowing this kind of information allows you to pinpoint what parts of the application may be vulnerable as well as being able to make better decisions of what vulnerabilties may be present in the application itself.

### DNS and Subdomains
In many cases you may be provided with a scope consisting of just a domain name. In these cases there may be multiple subdomains for this domain other than the ones publicly available. These subdomains are generally hidden and thus you will have to find them. We want to find these subdomains as each one is another asset and may provide a new application or functionality that increases the attack surface. Most hidden subdomains that aren't publicly available will also generally contain staging or development environments, admin consoles or other applications that aren't meant for general user access.

##### What is a subdomain?
A subdomain is as the name implies, a subdivision of a larger domain, where a domain is commonly referred to as the website name. 
e.g. www.google.com
- 'www' is the subdomain
- 'google' is the domain name
- 'com' is the top level domain

##### DNS and Reverse DNS Lookup
By first using a DNS Lookup we can determine the IP that maps to that domain. We can they perform a reverse DNS lookup to find the domain that maps back to this IP. This will also include any other subdomains that map back onto that same IP or are related to that same IP space.

- DNS Lookup = provide a domain name and the IP mapped to it is returned
- Reverse DNS Lookup = provide an IP address and domain names mapped to it are returned

##### Online Tools
- [yougetsignal](https://www.yougetsignal.com/tools/web-sites-on-web-server/)
- [dnsDumpster](https://dnsdumpster.com)
- [pentest-tools](https://pentest-tools.com/information-gathering/find-subdomains-of-domain)

##### Subdomain Brute Force
In many cases the methods above are not enough to find all the subdomains and a brute force may be required. There are many tools our there that allow subdomain bruteforcing such as the ones below. It is often best to chain some of the tools. For example using gobuster to bruteforce subdomains and then using altdns to find permutations of those subdomains that are slightly more obscure and might not come up in a generic word list.

##### Brute Force Tools
- [goBuster](https://github.com/OJ/gobuster) - DNS & Directory/File Brute Force
- [altdns](https://github.com/infosec-au/altdns) - Subdomain brute force using permutations of a given wordlist.
- [subbrute](https://github.com/TheRook/subbrute) - Subdomain brute force tool. 
- [fierce](https://github.com/mschwager/fierce) - Locates non-contiguous IP spaces and subdomains

##### Other Resources
- [DNS Hacking](https://resources.infosecinstitute.com/dns-hacking/)
- [Discovering Subdomains](https://www.bugcrowd.com/discovering-subdomains/)

### Port Scan
This is one of the first things you should try when you come across a new IP. It will allow you to check what ports are open which can give you a good idea of what other services may be running. This is great as some services may already have known vulnerabilities. This will also let you increase the attack surface you have access to as browsers generally only use http/https. 

##### nmap
[nmap](https://nmap.org) is a tool that allows you to quickly and easily perform a portscan by specifying a domain name or an ip address. Basic usage can be done with `nmap [domain/ip]`. In order to get information about what services may be running on a port use the -sV flag.

### Application Layout/Funtionality
One you have discovered a handful subdomains it's time to start exploring their applications. It a good idea to play around with the functionality and get a good idea of how the applications work and what attack surfaces are present. A good idea is to use a tool like [Burp Suite](https://portswigger.net/burp) while you do this as it records your http history by passing requests through a proxy. This allows you to view any hidden requests made by the application, the fields present in forms as well as other information sent by requests or received by responses. Burp also has many other features such a 'spidering' feature which will crawl links on pages of the application to build a map for you.

### Directory's & Files
Sometimes traversing the application or spidering wont expose all of the available files and directories. In this case we can find hidden files by doing a brute force. This also includes routes/endpoints for any API's the application may use. We can also use [goBuster](https://github.com/OJ/gobuster) to brute force directories.

##### Common Files
- robots.txt - Contains hidden routes that developers don't want robots to index in search engines ect.
- .git - If you manage to find this file then you can essential grab all of the source code.
	- [DVCS-Pillage](https://github.com/evilpacket/DVCS-Pillage) - Used to build source code from a .git file
	- [truffleHog](https://github.com/dxa4481/truffleHog) - Used to find high entropy strings, useful for finding keys
- phpinfo.php

### WordLists
Word lists are required for all types of brute forcing, however using the correct word list is extremely important as it can increase the hit rate of the brute force as well as decrease the time it takes to complete. It is ideal to use a wordlist that is targeted towards not only the application you are trying to brute force but also the objective of the brute force. 

For example when brute forcing files and directories it would be preferred to include common files and routes in the word list. This is also the same for credentials, it is common sense to try the most common passwords as this increases your chance of being successful.

[Seclists](https://github.com/danielmiessler/SecLists) is a repository that contains multiple wordlists each with their own specific target use. While word lists like this are extremely useful, you should also update and include additional words into these lists so that the list are better suited to your target.