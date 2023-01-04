# Domain enumeration 
A lot of useful tips can be found here https://book.hacktricks.xyz/network-services-pentesting/pentesting-dns

### Subdomain enumeration
A subdomain doesn't have to be present in the DNS, so this is a good way to find local vhosts on a server.

```bash
gobuster dns -d trick.htb -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt

# ffuf - filter out false positives with `-fw` (words), `-fs` (size), `-fc` (Status code)
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -u http://trick.htb -H "Host:FUZZ.trick.htb"
```

### Zone transfer
If allowed it can be useful to get all the records from the zone. Like subdomains. 

```bash
dig axfr @<DNS_IP> #Try zone transfer without domain
dig axfr @<DNS_IP> <DOMAIN> #Try zone transfer guessing the domain
fierce --domain <DOMAIN> --dns-servers <DNS_IP> #Will try toperform a zone transfer against every authoritative name server and if this doesn'twork, will launch a dictionary attack
```

### Certificate Transparency (CT) logs
These are publicly accessible logs of every SSL/TLS certificate created for a domain name. Can reveal new subdomains 

https://crt.sh/ & https://ui.ctsearch.entrust.com/ui/ctsearchui
