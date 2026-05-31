# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<<BR>
## Program 
```
server
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
~~~
CLIENT:
~~~
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

#Download webpage

if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

#Upload webpage

else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()

~~~
INDEX.html:
~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Page</title>
</head>
<body>
    <h1>Welcome to the Python HTTP Server!</h1>
    <p>This is the default page served by the server.</p>

</body>
</html>
```
## OUTPUT
CLIENT(download):

<img width="892" height="507" alt="image" src="https://github.com/user-attachments/assets/9022453a-302c-4308-8577-e51ebc8ced18" />

SERVER(download):

<img width="849" height="270" alt="image" src="https://github.com/user-attachments/assets/d37c4b78-5e76-4456-a102-b073c8188d77" />

CLIENT(upload):

<img width="818" height="294" alt="image" src="https://github.com/user-attachments/assets/3b07e95d-99ea-4381-a14e-514e87e2d103" />

SERVER(upload):

<img width="849" height="270" alt="image" src="https://github.com/user-attachments/assets/ec21a01d-2e39-494b-8d51-504e2a658acd" />

<img width="1377" height="464" alt="image" src="https://github.com/user-attachments/assets/f2ac4153-ab55-4674-a324-cd75c94b981e" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
