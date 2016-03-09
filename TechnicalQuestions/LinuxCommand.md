##Linux Command
###
Linux command: kill -9   / scp / telnet / ps

###top
The easiest way to find out what processes are running on your server is to run the `top` command

###ps
- This output shows all of the processes associated with the current user and terminal session. This makes sense because we are only running bash and ps with this terminal currently.

- To get a more complete picture of the processes on this system, we can run the following:

```
ps aux
```

###kill
- The most common way of passing signals to a program is with the kill command.

```
As you might expect, the default functionality of this utility is to attempt to kill a process:

kill PID_of_target_process

This sends the TERM signal to the process. The TERM signal tells the process to please terminate. This allows the program to perform clean-up operations and exit smoothly.
```

###scp
- scp stands for secure cp (copy), which means you can copy files across ssh connection

- Copy one single local file to a remote destination

```
scp /path/to/source-file user@host:/path/to/destination-folder/
```

###telnet
The telnet command is used for interactive communication with another host using the TELNET protocol. It begins in command mode, where it prints a telnet command prompt ("telnet>").








