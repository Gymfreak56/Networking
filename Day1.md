## Bits, Nibbles, Bytes
```

255.255.255.0 == FF FF FF 00 == 11111111 11111111 11111111 00000000

```

## Message Formatting Method(Encapsulation/Decapsulation)
```

Tcp packet gets encapsulated into an ip packet -> Ethernet Frame -> Transmitted as bits

```

## OSI Model
```

Away        Application
Pizza       Presentation 
Sausage     Session  
Throw       Transport
Not         Network
Do          Data Link/
Please      Physical

```

## Layer 1 (Physical)
```

Hardware Specifications
Data transmission & reception
Physical network design (swtich,HUB,)

```

## Layer 2 (Data Link)
```

VLAN

Allows logical seperation of network
QOS(quality of service) == Urgency
VLAN TAG == Which VLAN its going to/coming from
**DOUBLE TAGGING**(2 VLAN IDS)

ETHERNET

MAC -> IP and vice versa

MAC Address Layer 2 -> 1
LLC (Logical Link Control) Layer 2 -> 3

ARP / RARP

cut through forwarding (only read destination mac so its faster)

0x0800 == ip4
0x0806 = ARP
0x86DD == ip6
0x8100 == VLAN TAG


ARP
IP -> MAC

PROXY ARP(router answers all ARP for network)
Switch breakup broadcast domains

Routers breakup colision dommmains

ARP Cache(ARP / ip neighbor)

ARP Operation 
1 == request 
2 == reply

ARP attacks:
Gratuitous ARP == pretend to be another machine in network
Proxy ARP == pretend to be a router
ARP Storm(?) == Loop

```

## Layer 3 (Network)
```

IPv4
IP Addresses

Logical addressing
Encapsulation
Fragmentation & reassembly of packets
Error handling/diagnostics

IPv4 Header:
Version == 4(Ipv4)
IHD(Internet header length) == unmber of 32 bit(4 bytes) words in header
DSCP/ECN (first 6 bits == DSCP; Last 2 bits == ECN) == 
  DSCP == type of traffic passe
  ECN == Congestion Notifications(usually 0)
Total Length == (whole packet)20-65,535
ID == used to identify fragmented packets
Flags/Fragmentation offset(3 bits == flags(1st bit(48th bit) == 0; 2nd bit(49th bit) == don't fragment; 3rd bit(50th bit) == more fragments)) ==
TTL(Time to live) == Max number of hops till packet gets dropped
Protocol == Protocol encapsulated in packet(TCP == 6; UDP == 11; ICMP == 16)
Checksum
Source Adress
Destination Address
options (If header field is > 5)

```

### IP Fragmentation
```

1500 mtu - 20(ip header)
185(fragmentation Offset) * 8 = 1480

```

## IPv6
```

Header:
Version == 6
Traffic Class(8 bits) == Priority/Urgency
Flow Label(20 bits) == Don't send stuff through different paths
Payload Length(in octets) == how many bytes
Next Header == Header after IPv6(TCP/UDP)
Hop Limit
Source
Destination

TTL:
Linux=64
Windows=128
Cisco=255


```

## ICMP
```

Type == 11(ttl exceeded)
Code == 0
Checksum 
ICMP Messages

Firewalking == Traceroute /ttls to map out nework
oversized ICMP messages can cause crashing

ICMP in IPv6 is for router discovery 

```

## Zero Configuration
```

IPv4:
APPIPA == If DHCP doesnt assign an address it automatically assigns one
RFC 3927 ==

IPv6:
SLAAC (Stateless Address Auto-Configuration)
RFC 4862

```

## 
```



```

## 
```



```

## 
```



```

## 
```



```

## 
```



```

## 
```



```

