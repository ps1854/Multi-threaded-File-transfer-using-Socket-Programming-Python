# Multi-threaded-File-transfer-using-Socket-Programming-Python


##	ABSTRACT
This project aims to implement a server to facilitate multiple file exchanges between clients using TCP. Server program uses multi-threading to facilitate file transfer between multiple clients simultaneously. The project is totally implemented in Python. Socket, OS and threading are the main python modules used in this project
Client program can command six different functions to the server. The functions are HELP, LIST, UPLOAD, DOWNLOAD, DELETE, LOGOUT. HELP function displays the list of functions that a client can ask for. LIST function gives the list of files available in the server_data. UPLOAD function can be used to  upload files from client to server by specifying the path from which the file needs to be uploaded. DOWNLOAD function helps in downloading files from server_data to client_data by specifying the name of the file that needs to be downloaded. DELETE function, as it sounds, used to delete a file from the server_data by giving the file name on the client side. Finally, we have LOGOUT function. This function used to break the connection between a client and the server.



## ARCHITECTURE AND DESIGN

![Architecture](https://user-images.githubusercontent.com/89296568/152753017-1f8aecc7-ca67-431c-ac9b-4677c809e66d.png)



## IMPLEMENTATION

### Server Program
The server accepts connections with clients whenever a client wants to connect. After accepting the connection, a new thread is created with Thread method, which is handled by handle_client method.
```python
def main ():
    print("[STARTING] Server is starting")
    server = socket.socket (socket.AF_INET, socket.SOCK_STREAM)
    server.bind(ADDR)
    server.listen()
    print(f"[LISTENING] Server is listening on {IP}:{PORT}.")

    while True:
        conn, addr = server.accept()
        thread = threading.Thread(target=handle_client, args=(conn, addr))
        thread.start()
```
Whenever a client is connected with the server this function is called to handle all queries from the client. There are totally six commands that can be served by the server. 
```python
def handle_client(conn, addr):
    print(f"[NEW CONNECTION] {addr} connected.")
    conn.send("OK@Welcome to the File Server.\nEnter 'HELP' to get list of commands.".encode(FORMAT))
    while True:
        data = conn.recv(SIZE).decode(FORMAT)
        data = data.split("@")
        cmd = data[0]

```
The server serves according to the client requirements.


### Client Program
When the main function is called it starts with creating a TCP socket for client with IPv4 address family. Then, the client tries to connect with the server on the above specified PORT number. After a connection is acquired, it starts communicating with the server indefinitely.  The client receives greetings from the server. Client takes input from terminal which is sent to server. 
```python
    while True:
        data = client.recv(SIZE).decode(FORMAT)
        cmd, msg = data.split("@")

        if cmd == "DISCONNECTED":
            print(f"[SERVER]: {msg}")
            break
        elif cmd == "OK":
            print(f"{msg}")

        data = input("> ")
        data = data.split(" ")
        cmd = data[0]
```
The client may ask for any of the above mentioned six services from the server.



## How to run
Open a linux terminal. Run the server file
```
python3 server.py
```
IP address and PORT number will printed be to the terminal.

Run the client file in a new terminal.
```
python3 client.py
```
Connection message will printed ro the terminal



## Build and Test Environment
```
Ubuntu 20.04
```

