# Useful tools
List commonly used tools

## ssh
Secure shell - connect to remote shell

Variants: `ssh`


### Connect to shell with SSH

```zsh
ssh sshuser@<IP> -p PORT
```
## ftp 
Connect to file transfer protocol server

Variants: `ftp`

### Connect to FTP server

```zsh
ftp ftp://<FTP_USERNAME>:<FTPUSER_PASSWORD>@localhost
```



## netcat
Connect to ip and port just as easy as it sounds

Variants : `netcat` `ncat` `nc`


### Connect to address with specific port
```zsh
ncat IP PORT
```

### Connect to address with specific port
```zsh
ncat -nv IP:PORT
```

### Connect to address with specific filtered port
```zsh
ncat -nv --source-port <DNS_SERVER_PORT> IP:PORT
```

`-n` Do not resolve hostnames via DNS

`-v` Verbose