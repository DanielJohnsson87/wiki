# Upload files

### Netcat
On receiving end
```bash
nc -l -p 1234 > out.file
```

On sending end
```bash
nc -w 3 [destination] 1234 < out.file
```

[Read more](https://nakkaya.com/2009/04/15/using-netcat-for-file-transfers/)
