# 2a_Stop_and_Wait_Protocol

## AIM 
To write a python program to perform stop and wait protocol

## ALGORITHM
1. Start the program.
2. Get the number of frames from the user.
3. Create frames based on the user input.
4. Send one frame at a time from sender to receiver.
5. Wait for an acknowledgment (ACK) from the receiver.
6. If ACK is received, send the next frame.
7. Repeat until all frames are transmitted.
8. Stop the program.

## PROGRAM
### sender.py
```py
import socket
import time

sender = socket.socket()
sender.bind(('localhost', 8000))
sender.listen(1)

print("Waiting for receiver connection...")

conn, addr = sender.accept()
print("Connected to:", addr)

n = int(input("Enter number of frames: "))

for i in range(n):
    frame = f"Frame {i}"

    print("\nSending:", frame)
    conn.send(frame.encode())

    ack = conn.recv(1024).decode()

    if ack:
        print("Received:", ack)

    time.sleep(1)

print("\nAll frames sent successfully")

conn.close()
sender.close()
```
### receiver.py
```py
import socket

receiver = socket.socket()
receiver.connect(('localhost', 8000))

while True:
    frame = receiver.recv(1024)

    if not frame:
        break

    frame = frame.decode()

    print("Received:", frame)

    ack = "ACK for " + frame

    receiver.send(ack.encode())

receiver.close()
```
## OUTPUT
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/13dc53e2-6b66-4cbf-8032-15798dbc2a3f" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
