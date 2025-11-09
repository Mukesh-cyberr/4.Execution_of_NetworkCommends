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

## PROGRAM
CLIENT
```


import socket

HOST = '127.0.0.1'
PORT = 8080

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect((HOST, PORT))

print("Connected to server.")
print("Enter network commands like:")
print("  - ipconfig / ifconfig")
print("  - ping www.google.com")
print("  - nslookup www.google.com")
print("  - tracert / traceroute www.google.com")
print("Type 'exit' to close the connection.\n")

while True:
    command = input("Enter command: ")

    if command.strip() == "":
        continue

    client_socket.send(command.encode())

    if command.lower() == "exit":
        print("Disconnected from server.")
        break

    result = client_socket.recv(65535).decode()
    print("\n=== Command Output ===")
    print(result)
    print("======================\n")

client_socket.close()

```
SERVER
```

import socket
import subprocess

HOST = '127.0.0.1'  
PORT = 8080          

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind((HOST, PORT))
server_socket.listen(1)

print(f"Server started... Listening on {HOST}:{PORT}")

while True:
    conn, addr = server_socket.accept()
    print(f"\nConnected by {addr}")

    while True:
        command = conn.recv(1024).decode()
        if not command or command.lower() == "exit":
            print("Client disconnected.")
            break

        print(f"Received command: {command}")

        try:
           
            result = subprocess.getoutput(command)
        except Exception as e:
            result = f"Error executing command: {str(e)}"

        
        conn.send(result.encode())

    conn.close()

```
## Output
client

<img width="650" height="348" alt="Screenshot 2025-11-09 202145" src="https://github.com/user-attachments/assets/2b3b3872-dec2-4a5f-9fba-3e36bd7da7f9" />

server

<img width="688" height="333" alt="Screenshot 2025-11-09 202156" src="https://github.com/user-attachments/assets/ef686225-9957-42b1-8737-9fc8298437b3" />


## Result
Thus Execution of Network commands Performed 
