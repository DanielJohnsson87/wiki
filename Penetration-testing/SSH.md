### Tunneling - Using SSH as a "proxy/vpn"
Route all traffic for a specific port through an SSH tunnel. Could be useful when you wish to access websites that are behind firewalls or similar. Just configure your browser to proxy all traffic through `machine.com` using port `1337` and `SOCKS-5`. [More details here](https://blog.0xffff.info/2021/07/25/ssh-shenanigans-part-1-tips-tricks/)

```bash
ssh -D 1337 you@machine.com
```


### Stealthy & secure connect

```bash
ssh -o -T UserKnownHostsFile=/dev/null user@host.com bash -i -4 -C -c blowfish-cbc
```

- The -T flag prevents a TTY from being allocated upon login. There are some technical issues that arise regarding not using a TTY (some commands not outputting properly and some programs not working as intended) [Read more about it here.](https://blog.0xffff.info/2021/07/25/ssh-shenanigans-part-1-tips-tricks/)
- The bash -i flag will simulate a prompt for you, since the lack of a TTY will mean no prompt
- The -o flag alongside setting UserKnownHostsFile to /dev/null will result in nothing being logged to known_hosts when you connect.
- -4 will force IPv4 connectivity
- -C will compress the stream cipher
- -c blowfish-cbc will specify ‘blowfish’ for the encryption type for stream cipher