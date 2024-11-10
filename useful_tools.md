# Useful tools
List commonly used tools

## ssh
Secure shell - connect to remote shell

Variants: `ssh`


### Connect to shell with SSH

```zsh
ssh sshuser@<IP> -p PORT
```

### Connect to shell with SSH using certificate
```zsh
ssh sshuser@<IP> -p PORT -i id_rsa
```


## ftp 
Connect to file transfer protocol server

Variants: `ftp`

### Connect to FTP server

```zsh
ftp ftp://<FTP_USERNAME>:<FTPUSER_PASSWORD>@localhost
```



## smbclient
### Connect to smb server and list available shares

```zsh
smbclient -N -L \\\\IP
```
### Connect to smb share as user

```zsh
smbclient -U bob -L \\\\IP\sharename
```




`-U bob` as user bob

`-N` suppresses the password prompt

`-L`  retrieve a list of available shares 


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

`-l` listen mode


## whatweb
Get some information about certain website

```zsh
whatweb IP --no-errors
```

