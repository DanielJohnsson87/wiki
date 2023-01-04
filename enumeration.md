# Enumeration
Wordlists 👉 https://github.com/DanielJohnsson87/wiki/blob/main/Wordlists.md

### `fuff`
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://MACHINE_IP/FUZZ
```

### `dirb` 
```bash
dirb http://MACHINE_IP/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

### `gobuster`

```bash
gobuster dir --url http://MACHINE_IP/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```