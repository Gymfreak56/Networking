## Layer 4 (Transport)
### TCP
```

Header:
Source Port
Destination Port
Sequence Number -- used to make sure all the data is there and in order
Acknowledgement Number -- used to make sure all the data is there and in order
Offset -- size of tcp header in 32 bit chunks(min=5, max=15?)
Reserved
Tcp Flags -- each bit represents a flag
Window -- how much data the reciever can take at once
Checksum
Urgent Pointer -- if urg in flags is set it does stuff
Options

```

### UDP
```

Header:
Source Port
Destination Port
Length -- Length of Header and Data
Checksum

```

## Layer 5 (Session)
### Protocols
```

SOCKS 4=(TCP) 5=(TCP/UDP):
TCP 1080
Used for initiating connections through a proxy
Client can provide authentication to server
Client can request connections from server

NetBIOS/SMB/CIFS:
TCP 139/445 and UDP 137/138)
SMB rides over NetBIOS
SAMBA and CIFS are slightly different from SMB
138 UDP -- Datagram
139 TCP - Session


PPTP/L2TP:
Point to Point Tunneling Protocol - Obsolete
TCP 1701
Layer 2 Tunneling Protocol - VPN. Unecrypted
TCP 1723

RPC:
ANY PORT (Linux 111?)
Sends a request for info from a server
recieves the info 
display data

```

## Layer 6 (Presentation)
### Responsibilities
```

Translation

Formating

Encoding (ASCII, EBCDIC, HEX, BASE64)

Encryption (Symmetric or Asymmetric)

Compression

```

## Layer 7 (Application)
### FTP
```

TCP 20/21

Messages:
FTP Commands
FTP Reply codes

Modes:
Active(Default)
Passive

ACTIVE:


Passive:
PASV
(10,10,10,83,128,93)
   IP       x256
                +93
              PORT 32861
Server tells the Client which port it opens and gets data from that port

```

### Telnet
```

CANNOT TUNNEL WITH TELNET
TCP 23
No Encryption


```

### SMTP
```

TCP 25
Communication with Mail Servers

```

### TACAS
```

TCP 49
Network Authentication Protocol

```

### HTTP/HTTPS
```

INTERNET

Methods:
GET/HEAD/POST/PUT

Status Codes:
100,200,300,400

```

### POP/IMAP 
```

EMIAL protocols used by clients to interact with email servers
POP (Post office protocol) TCP 110
IMAP (Internet Message Access Protocol) TCP 143

```

### RDP
```

TCP 3389
Remote Desktop Protocol
Supports Compression/Encryption

```

### DNS
```

Domain Name Server
TCP 53 (Zone Transfers)
UDP 53 (Queries & Resposnses) -- client/server

```

### DHCP
```

UDP 67/68
Dynamic Host Configuration Server
Dynamically assigns IP addresses

Client sends on port 67
Server responds on port 68

```

### TFTP
```

UDP 69
Trivial File Transfer Protocol
Used for Pixie Boot(remote boot?)
Good for switch/router configuration?

```

### NTP
```

UDP 123
Network Time Protocol
Synchs up the time to make stuff easier

```

### SNMP
```

UDP 161/162
Simple Network Management Protocol
Clients can send info to server
or server gets info on clients

```

### RADIUS
```

UDP 1645/1646 AND 1812/1813
Authentication

```

### RTP
```

UDP > 1023
Real Time Transport Protocol
Delivering Audio/Video over IP

```

### SSH
```

TCP 22
Secure Shell
Client/server Authentication
Asymmetric or PKI for key exchange
Symmetric for session
User authentication
Data Stream channeling



```

## TCPDUMP
```

Primatives:
tcpdump -D == shows interfaces
tcpdump -i eth0 == shows all traffic on that interface
sudo tcpdump -i eth0 -X == shows hex and ASCII
sudo tcpdump -i eth0 -XX == include ethernet in frame
sudo tcpdump -i eth0 -w test.pcap == writes to a file
sudo tcpdump -r test.pcap == reads from file
sudo tcpdump -i eth0 -XXvv == verbose (more info)
sudo tcpdump -i eth0 -XXvvn == shows actual port number and unresolved DNS (IP instead of FQDN)
can use && (and) || (or) ! (not) and () (parenthesis)



```

## Berkely Packet Filters
```

tcpdump {A} [B:C] {D} {E} {F} {G}

A = Protocol (ether | arp | ip | ip6 | icmp | tcp | udp)
B = Header Byte offset
C = optional: Byte Length. Can be 1, 2 or 4 (default 1)
D = optional: Bitwise mask (&)
E = Operator (= | == | > | < | <= | >= | != | () | << | >>) (>> == bitshifting) (= -- set equal to) (== - comparison)
F = Result of Expresion
G = optional: Logical Operator (&& ||) to bridge expressions



```

### Bitwise Masking
```

ip[0] & 0x0F > 0x05

bitmask  1111 1111
bits     0101 0101 -- won't match
bits     0101 0111 -- will match


tcp[13] & 0x11 = 0x11
fin and ack need to be set, and the others can be on

tcp[13] & 0x11 !=0
only the fin OR the ack have to be on

```

##
```



```

