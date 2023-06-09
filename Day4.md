## Network Reocn.
### RECON
```

Active - Sending packets to a host/network
Passive - packet sniffing (Takes longer - Low Risk)
Internal - Inside Network/On host 
External - outside of network

```

### Passive
```

WHOIS queries
Job listings
Phone Numbers
Google (Google Hacking)
Passive OS Fingerprinting (TTL, Ping content, ect.)

```

### DIG
```

dig google.com (MX,SOA,NS,A,AAAA,PTR,TXT)(SOA=Start OF Authority - Primary DNS)

Use Netcrft to see history of a domain

Google:
*google.com site:*.google.com
site:*.google.com "Powered by"

```

### SHODAN
```

look at IOT devices and vulnerabilities

```

### Active Recon/Scanning
```

Remote -> local
local -> remote
local -> local
remote -> remote

Network Scanning:
wide range target scan - automated - multiple hosts
target specific scan - thorough - single hosts

single source or multiple hosts scanning

Broadcast ping or ping sweep
arp scan
syn scan
full connect scan
Null scan
FIN scan
XMAS tree scan
UDP scan
ACK/Window scan
RPC scan
FTP scan
decoy scan
OS fingerprinting scan
version scan
Protocol ping
Discovery probes
SCTP INIT scan

nmap -sn <network/CIDR>
for i in {1..254}; do {ping -c 1 -W 1 10.10.10.$i | grep "from"}
nmap ports (21, 22, 23, 80)
nmap -sS 172016.1.15 -p 21,22,23,80 -vvvv (syn stealth scan)
     -sT -sV                              (full connect) (service version)
     -sN                                  (Null scan)(Get through some firewalls)
     -sF                                  (Sends the Fin flag)
     -sX                                  (Sets the Fin, Psh, and Urg flags)
     -sU                                  (UDP)
     -sI                                  (Idle scan)(both syn stealth and full connect)(uses ip add. spoofing)
     -sW                                  (Windw scan)
     -Pn                                  (No PING)
     -O --osscan-guess                    (Aggressively guess os)
     -T 4                                 (Sends packets faster)
     --min-rate                           (Sends packets no slower than number)
     -A                                   (OS detection, version, script, and traceroute)
     
hostname -f == domain
whoami
w
ifconfig
ip address
netstat
ss

```

### VYOS
```



```

### 
```



```

### 
```



```

### 
```



```

### 
```



```

### 
```



```

### 
```



```

### 
```



```

### 
```



```

### 
```



```

