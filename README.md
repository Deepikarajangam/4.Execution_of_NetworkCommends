# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>
 

## INPUT:
client.py:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

try:
    while True:
        ip = input("Enter the website you want to ping: ")
        s.send(ip.encode())
        response = s.recv(1024).decode()
        if response:
            print("Ping Result:", response)
        else:
            print("No response from server.")
except Exception as e:
    print("Error:", e)
finally:
    s.close()

```

server.py:
```
import socket
import requests

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

print("Server started... Listening on localhost:8000")

while True:
    c, addr = s.accept()
    print("Connection from", addr)

    try:
        hostname = c.recv(1024).decode().strip()

        if hostname:
            try:
                response = requests.get("http://" + hostname)
                if response.status_code == 200:
                    c.send("Ping successful: Website is reachable".encode())
                else:
                    c.send("Ping failed: Website is not reachable".encode())
            except Exception as e:
                c.send(f"Ping failed: {e}".encode())
        else:
            c.send("Hostname not provided".encode())
    except Exception as e:
        print("Error:", e)
    finally:
        c.close()
```

Trace
```
from scapy.all import *

target = ["www.google.com"]
result, unans = traceroute(target, maxttl=32)
print(result, unans)

```
## Output
client:
<img width="1043" height="92" alt="image" src="https://github.com/user-attachments/assets/25768e51-b692-4200-926a-16a7c66e4f9a" />
server:
<img width="1041" height="82" alt="image" src="https://github.com/user-attachments/assets/758040d6-b6d9-4706-9754-42d6ab2c5adf" />
Trace comment:

<img width="1039" height="295" alt="image" src="https://github.com/user-attachments/assets/9010149e-270c-47fb-a261-8622e5e7f841" />





## Result
Thus Execution of Network commands Performed 
