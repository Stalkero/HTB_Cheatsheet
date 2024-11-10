# Scanning with nmap

## Scan the network with TCP-SYN
```zsh
sudo nmap -sS <IP>
```

## Scan network range
```zsh
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```

`10.129.2.0/24`  Range to scan

`-sn` Disable port scan

`-oA` Save results to file

## Scan network with range in file 

```zsh
sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
```

`-sn` Disable port scan

`-oA` Save results to file

`-iL hosts.lst` Scan the ranges from file


## Scan the address with ping and packet-trace

```zsh
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace 
```



`-sU` Scan for UDP ports

`-sA` Scan TCP ports with TCP-SYN

`-sV` Scan the service with version

`-A` Performs service detection, OS detection, traceroute and uses defaults scripts to scan the target.

`-O` OS Detection scan

------------------------------------



`-PE` Scan with 'ping'

`--disable-arp-ping` Do not 'ping' the target

`-n` Disable DNS resolution

`-Pn` Disable requests for ping 



------------------------------------





`--top-ports=10` Scan the most frequent 10 ports

`-p PORT` Scan the provided PORT 

`-F` Scan top 100 ports

`-sn` Disable port scan

`-p-` Scan all ports



----------

`--packet-trace` Rly i have to explain?

`--reason` Rly i have to explain?

`-oA` Save results to file

`--stats-every=5s` Rly i have to explain?



## nmap Scripting engine
### Categories of scripts


- `auth` Determination of authentication credentials.

- `broadcast` Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans.

- `brute` Executes scripts that try to log in to the respective service by brute-forcing with credentials.

- `default` Default scripts executed by using the `-sC` option.

- `discovery` Evaluation of accessible services

- `dos` These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services.

- `exploit` This category of scripts tries to exploit known vulnerabilities for the scanned port.

- `external` Scripts that use external services for further processing.

- `fuzzer` This uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time.

- `intrusive` Intrusive scripts that could negatively affect the target system.

- `malware` Checks if some malware infects the target system.

- `safe` Defensive scripts that do not perform intrusive and destructive access.

- `version` Extension for service detection.

- `vuln` Identification of specific vulnerabilities.


### Executing default script
```zsh
sudo nmap IP -sC
```

### Executing specific category of scripts or defined scripts

```zsh
sudo nmap <target> --script <category|name>
```



## Scan with decoys (Recommended)
```zsh
sudo nmap <target> -p <port> -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5 --source-port 53
```

`-D` Use decoys

`RND:5` 	Generates 5 random IP addresses that indicates the source IP the connection comes from.

`-S <IP>` Send different source IP address used to scan the network

`-e <interface>` Scan with that network interface

`--source-port <53|PORT>` Scan with different source port (DNS proxying) 
