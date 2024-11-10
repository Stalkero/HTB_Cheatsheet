# Fuzzing with FFUF

## Useful wordlists

### Skip wordlists copyright info 

```zsh
ffuf -ic 
```

### SecLists

```zsh
sudo apt-get install locate seclists
```

```zsh
locate directory-list-2.3-small.txt

/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt
```

## Directory fuzzing

```zsh
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ
```

`-w <wordlist>:FUZZ` select wordlist used to fuzzing. FUZZ is our label for words inside text file

`-u < IP:PORT | ADRESS:PORT > / FUZZ` select adress on which we will be fuzzing. FUZZ is a placeholder for words inside wordlist file


## Extension fuzzing

```zsh
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt:FUZZ u http://SERVER_IP:PORT/blog/indexFUZZ
```

`-w <wordlist>:FUZZ` select wordlist used to fuzzing. FUZZ is our label for words inside text file

`-u < IP:PORT | ADRESS:PORT > / FUZZ` select adress on which we will be fuzzing. FUZZ is a placeholder for words inside wordlist file

## Page fuzzing

```zsh
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php  -t 200 -fs 281 -e .php,.phps
```

`-w <wordlist>:FUZZ` select wordlist used to fuzzing. FUZZ is our label for words inside text file

`-u < IP:PORT | ADRESS:PORT > / FUZZ` select adress on which we will be fuzzing. FUZZ is a placeholder for words inside wordlist file

`-t 200` 200 Threads

`-fs 281` filter by response size

`-e .php,.phps` filter by extension

## DNS records fuzzing

### Sub-domain fuzzing
```zsh
ffuf -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://FUZZ.academy.htb/
```


### Vhost fuzzing
```zsh
ffuf -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb'
```

`-H` Header flag

## Parameter fuzzing


### GET Fuzzing
```zsh
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx
```

### GET Fuzzing with known parameter name
```zsh
ffuf -w /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt:FUZZ-u http://admin.academy.htb:PORT/admin/admin.php?parameter=FUZZ -fs xxx
```

### POST Fuzzing

```zsh
fuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

### POST Fuzzing with known parameter name

```zsh
fuf -w /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'parameter=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```


### Send POST request

```zsh
curl http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded'
```

### Value Fuzzing
```zsh
fuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```


## Recursive scanning 
```zsh
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v
```

`-w <wordlist>:FUZZ` select wordlist used to fuzzing. FUZZ is our label for words inside text file

`-u < IP:PORT | ADRESS:PORT > / FUZZ` select adress on which we will be fuzzing. FUZZ is a placeholder for words inside wordlist file

`-e .php,.phps` filter by extension

`recursion` Enable recursive scanning

`-recursion-depth 2` Recursive scanning depth 

`-v` Full verbose mode 



## Useful
### Generate id's
```zsh
for i in $(seq 1 1000); do echo $i >> ids.txt; done
```