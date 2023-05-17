# Privilege escalation

Various ways to recon and find privilege escalation paths.


### Recon

- `sudo -l` - Is the user allowed to run any commands as root
- `find / -user "$(whoami)" -type f 2>/dev/null | grep -v sys | grep -v proc` - List files belonging to current user. Can be useful to spot files that can be used to priv esc.
- `./linpeas.sh > linpeas-output.txt` - Run [linpeas](https://github.com/carlospolop/PEASS-ng/blob/master/linPEAS/README.md) to find possible paths. 
- `./pspy32` - pspy - unprivileged Linux process snooping. See if it's possible to catch any processes that root is running. Might give away useful information.
- `getcap [binary]` - It might be possible that python, php or what ever program is running on the machine has some special capabilities set that could be useful. (Linpeas will probably have found that already.)
- `cat /etc/passwd` & `cat /etc/shadow` - Get users and possibly the password hashed in /etc/shadow. While you're at it. Check if you have write permissions to any of these files. If you do, it should be possible to add a new privileged user.
- `ps aux` / `ps faux` - Check processes currently running that you have access to. 
