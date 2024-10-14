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
