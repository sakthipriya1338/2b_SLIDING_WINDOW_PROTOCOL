# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
##CLIENT
```
import socket

server_socket = socket.socket()
port = 8000
while True:
    try:
        server_socket.bind(('localhost', port))
        break
    except OSError:
        port += 1

print(f"Listening on localhost:{port}")
server_socket.listen(5)
client_socket, addr = server_socket.accept()
print(f"Connected by {addr}")

size = int(input("Enter number of frames to send : "))
frames = list(range(size))
window_size = int(input("Enter Window Size : "))
index = 0

while index < len(frames):
    end = min(index + window_size, len(frames))
    client_socket.send(str(frames[index:end]).encode())
    ack = client_socket.recv(1024).decode()
    if ack:
        print(ack)
        index = end
```

##SERVER
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    print(s.recv(1024).decode())
    s.send("acknowledgement recived from the server".encode())
```

## OUTPUT
<img width="1887" height="1001" alt="Screenshot 2026-05-22 150133" src="https://github.com/user-attachments/assets/c59f4e67-850d-4ba5-aff6-682e00756379" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
