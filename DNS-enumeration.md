# DNS Enumeration

### Subdomain enumeration

```bash
gobuster dns -d trick.htb -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -u http://trick.htb -H "Host:FUZZ.trick.htb" -fw 1697
```
