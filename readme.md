# Compilation

```bash
$ make
```

# Notes on code execution

File Structure
- a.out is a sample file to transfer. It's and executable for a "Hello" prining programme.
- scriptfile and script_log are for replaying the server code
- Client executaion is seen in readme.pdf as text and screenshot.
  
```
├── a.out
├── client
│   └── client.c
├── makefile
├── readme.md
├── readme.pdf
├── scriptfile
├── script_log
└── server.c
```

In one terminal, execute the server code by:

## Server

```bash
$ ./s 4444
# format ./s [port no]
```

The server will now prompt the user to enter an interface number from the oprions displayed. 
Please type the required integer, and press enter.

## Client

For each client, open a new terminal, and run:

```bash
$ cd ./client
$ ./c 127.0.0.1 4444
# format ./c [server ip] [server port no]
```

The client will now prompt the user for a filename. 
Please type a valid filename and press enter.
Type `quit` to exit.


# Replay demo

For best results, please run when terminal is >= 94 characters wide. This will replay the demo in real time.
The replay will show an execution of the server code for about 2 minutes.

```bash
$ scriptreplay --timing=script_log scriptfile
```

For the 6 instances of clients tested, execution is seen in the screenshot below:

- Requested the server.c file
```
❯ ./c 10.4.19.67 4444
# Connection established! type msg after the prompt 'C>' 
C>server.c
Scanned: server.c
Reading file in 7184 chunks
File perms: 664
C>quit
Scanned: quit
# exiting
```

- Requested an executable, a.out. We can see that the file successfuly runs
```
❯ ./c 10.4.19.67 4444
# Connection established! type msg after the prompt 'C>' 
C>a.out
Scanned: a.out
Reading file in 16696 chunks
File perms: 775
C>quit
Scanned: quit
# exiting
❯ ./a.out
Hello!
```

- Joined and quit
```
❯ ./c 10.4.19.67 4444
# Connection established! type msg after the prompt 'C>' 
C>quit
Scanned: quit
# exiting
```

- Joined and quit
```
❯ ./c 10.4.19.67 4444
# Connection established! type msg after the prompt 'C>' 
C>quit
Scanned: quit
# exiting
```

- Joined and quit
```
❯ ./c 10.4.19.67 4444
# Connection established! type msg after the prompt 'C>' 
C>quit
Scanned: quit
# exiting
```

- Extra client, only able to join if someone above quit
- Requests the server executable
- We can see that the large executable file `s` successfully executs.
```
❯ ./c 10.4.19.67 4444
# Server refused connection
❯ ./c 10.4.19.67 4444
# Connection established! type msg after the prompt 'C>' 
C>s
Scanned: s
Reading file in 22664 chunks
File perms: 775
C>quit
Scanned: quit
# exiting
❯ ./s 4445
[info] Interface no. 0 : lo     address: 127.0.0.1
[info] Interface no. 1 : enp3s0 address: 10.4.19.67
[info] Interface no. 2 : virbr0 address: 192.168.122.1
[action] please type the interface number you wish to use: 
```


![](assets/20220412_194624_image.png)
