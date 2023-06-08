## Packet Creation & Socket Programming
### Socket
```

IP/Port destination
connected to
difference between kernel and user space

```

### Socket Types
```

Stream Sockets:
TCP, SCTP, Bluetooth

Datagram Socket:
UDP, Connectionless

Raw Sockets:
Not according to a standard (hand crafted)

```

### User Space vs. Kernel Space
```

User Space:
Stream Sockets
Datagram Sockets

Well known ports need root priviledges to edit(1024+)
dev/tcp or /dev/udp to transmit data

Kernel Space:
Raw Sockets

Capture on the wire
Using os scan or set flags on nmap
Using netcat to create a listener in the well known port range (0 - 1023)
Using Scapy to craft or modify a packet for transmission

```

### Socket Function
```

socket.socket([*family*[,*type*[*proto*]]])
family constants should be: AF_INET (default), AF_INET6, AF_UNIX == IPv4, IPv6, RAW

type constants should be: SOCK_STREAM (default), SOCK_DGRAM, SOCK_RAW = TCP, UDP

proto constants should be: 0 (default), IPPROTO_RAW

```

### Raw Socket
```

Raw Socket scripts must include the IP header and the next headers.

Requires guidance from the "Request for Comments" (RFC) to follow header structure properly.

RFCs contain technical and organizational documents about the Internet, including specifications and policy documents.

See RFC 791, Section 3 - Specification for details on how to construct an IPv4 header.

```

### Custom RAW
```

# For building socket
import socket

# For system level commands
import sys

# for doing an array in tcp checksum
import array

# For establishing packet structure, direct access to methods(dont need to do struct.pack)
from struct import *

# create a raw socket
try:
    s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_RAW)
except socket.error as msg:
    print(msg)
    sys.exit()

packet = ''
src_ip = "10.1.0.2"
dst_ip = "10.3.0.2"

#  add ipv4 headers
ip_ver_ihl = 69 # putting decimal converson of 0x45 (version and IHL)
ip_tos = 0 # Combines DSCP and ECN
ip_len = 0 # the kernal will fill actual length of packet
ip_id = 12345 # sets IP ID to 12345
ip_frag = 0 # sets fragmentation to off
ip_ttl = 64 # sets ttl to 64
ip_proto = 6 # sets next protocol to 6 (TCP) (16=CHAOS) (6=TCP) (17=UDP)
ip_check = 0 # kernel will set

ipsrcadd = socket.inet_aton(src_ip) # inet_aton() will convert to a 32 bit binary
ipdstadd = socket.inet_aton(dst_ip) # converts into 32 bit binary

ip_header = pack('!BBHHHBBH4s4s' , ip_ver_ihl, ip_tos, ip_len, ip_id, ip_frag, ip_ttl, ip_proto, ip_check, ipsrcadd, ipdstadd)
# B = 1 Byte; H = 2 Bytes; 4s = 4 Bytes

# TCP HEADER
tcp_src = 54321     # Source port
tcp_dst = 7777      # dest port
tcp_seq = 454       # sequence num
tcp_ack_seq = 0     # TCP ack seq number
tcp_data_off = 5    # data offset is multiplied by 4 === 20
tcp_reserve = 0     # the 3 reserve bits + ns flag in reserve field
tcp_flags = 0       # TCP flags field all off (Null)
tcp_win = 56535     # Max allowd window size 
tcp_chk = 0       # Checksum will be calculated later
tcp_urg_ptr = 0 # urgent pointer only if urg flag is set

# combine the left shifted 4 bits of tcp bit offset and reserve field
tcp_off_res = (tcp_data_off << 4) + tcp_reserve

# play with tcp flags

tcp_fin = 0 # finished
tcp_syn = 1 # synchronized
tcp_rst = 0 # reset
tcp_psh = 0 # push
tcp_ack = 0 # acknowledgement
tcp_urg = 0 # urgent
tcp_ece = 0 # explicit congestion notification echo
tcp_cwr = 0 # congestion window reduced

# combine flags into a byte by shifting them together
tcp_flags = tcp_fin + (tcp_syn << 1) + (tcp_rst << 2) + (tcp_psh << 3) + (tcp_ack << 4) + (tcp_urg << 5) + (tcp_ece << 6) + (tcp_cwr << 7)

# the ! in pack format means network order
tcp_hdr = pack('!HHLLBBHHH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res, tcp_flags, tcp_win, tcp_chk, tcp_urg_ptr)

user_data = b'This is a message, is this hidden??'

# Pseudo header fields
src_address = socket.inet_aton(src_ip)
dst_address = socket.inet_aton(dst_ip)
reserved = 0
protocol = socket.IPPROTO_TCP
tcp_length = len(tcp_hdr) + len(user_data)

# pack the pseudo header and combine with user data
ps_hdr = pack('!4s4sBBH', src_address, dst_address, reserved, protocol, tcp_length)
ps_hdr = ps_hdr + tcp_hdr + user_data

def checksum(data):
    if len(data) %2 != 0:
        data += b'\0'
        res = sum(array.array("H", data))
        res = (res >> 16) + (res & 0xffff)
        res = res >> 16
        return (~res) & 0xffff
tcp_chk = checksum(ps_hdr)

# Pack tcp header to fill in correct checksum - checksum is NOT network in network order
tcp_hdr = pack('!HHLLBBH', tcp_src, tcp_dst, tcp_seq, tcp_ack_seq, tcp_off_res, tcp_flags, tcp_win) + pack('H', tcp_chk) + pack ('!H', tcp_urg_ptr)


packet = ip_header + tcp_hdr + user_data

# send packet
s.sendto(packet, (dst_ip, 0)) # sends to dest ip on port 0

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

