# Cross-Site Scripting (XSS)

### What is XSS?
XSS is a client side vulnerability that targets users by injecting a client-side script into the webpage/application to perform a malicious action. It is commonly used to steal users session cookies or make requests from the users client. 

### Types of XSS

##### Reflected XSS
Reflected XSS occurs when an input field or URL parameter is reflected back onto the page. A common example of this is the search string being display on the search results page.

##### Stored XSS
Stored XSS is when the XSS payload is stored server-side before being reflected onto the client. In this case stored XSS is persistant and affects every user visiting webpages where the XSS is reflected. A common example of this is message/comments which are stored and visible to multiple users.

### Where to find XSS?
XSS occurs wherever there is user controlled input.

- Input Fields (Including Hidden Fields)
- URL Paramaters or Just in the URL in general
- ...

### XSS Filtering

[XSS Filter Evasion Cheat Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)

### CSRF


###### Same Origin Policy
Same Origin Policy is a header field that specifies what content is allowed to render on the page.

### Other Resources
- [XSS Shortening Cheatsheet](https://labs.neohapsis.com/2012/04/19/xss-shortening-cheatsheet)