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

ipconfig

<img width="646" height="591" alt="image" src="https://github.com/user-attachments/assets/991ccd0c-0a02-4801-ba89-9a74151ec3cb" />

ping www.google.com

<img width="610" height="327" alt="image" src="https://github.com/user-attachments/assets/1c70e9de-4f8f-45ff-8465-4a8bb5d258f1" />

nslookup www.google.com

<img width="422" height="259" alt="image" src="https://github.com/user-attachments/assets/cd5f9ec0-db42-46c1-81a3-f450e0ad709a" />

tracert / traceroute www.google.com

<img width="639" height="392" alt="image" src="https://github.com/user-attachments/assets/9ce3d6b4-37da-4b53-8c0c-ed68267e2da6" />

exit

<img width="644" height="52" alt="image" src="https://github.com/user-attachments/assets/5a354eb0-9735-4515-957b-a81a419601e8" />


server

<img width="660" height="240" alt="image" src="https://github.com/user-attachments/assets/9b8ea018-67f7-4ab6-aa89-ae5eeefebe06" />


## Result
Thus Execution of Network commands Performed 
