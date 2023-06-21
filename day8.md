## Network Filtering
```

can filter on email address
can filter on mac addr

filtering can decrease load on infrastructure
block malicious traffic
obfuscate internal networks (hide internal network from discovery)

Devices that can filter:
switches (layer 2/3)
routers (layer 3/4)
proxies (layers 3-7)
IDS's(intrusion detection system) (layers 3-7)
host based firewall (layers 3-7) (rules)
network firewall (stateless/stateful)(layers 3-7)

```

## Filtering concepts
```

whitelist = allowed ---- Blacklist = Denied
Routed = a hop(routes traffic) ----- Transparant = not a hop(just watches data pass)(still filters data but doesn't decrement ttl)

firewall:
stateless == works with tcp/udp and ip
stateful == tcp
application == in depth inspection of packet

```

## Traffic Directions
```

Traffic going from localhost to remote host (and return traffic)
traffic going to localhost from trusted places (and eturn traffic)  

```

## Host Based Filtering
```

Windows:
Windows Defender firewall (new)
Windows Firewall (old)

Linux:
IPtables
Firewalld
UFW?

Linux:
netfiltering
stateful/stateless
Network address and port address translation

```

## Netfilter hooks
```

NF_IP_PRE_ROUTING-> PREROUTING

NF_IP_LOCAL_IN → INPUT

NF_IP_FORWARD → FORWARD

NF_IP_LOCAL_OUT → OUTPUT

NF_IP_POST_ROUTING → POSTROUTING

```

## NETFILTER PARADIGM
```

tables - contain chains

chains - contain rules

rules - dictate what to match and what actions to perform on packets when packets match a rule

```

## IPTABLES
```

filter - default table. Provides packet filtering.
  INPUT, FORWARD, and OUTPUT
NAT filter --
  PREROUTING, POSTROUTING, OUTPUT
MANGLE -- Packet Alteration
  ALL CHAINS
RAW -- Configure exemptions
  PREROUTING and OUTPUT
SECURITY -- exists
  google some shit later

-A == append
-I == Insert(top of list)
-D delete rule {chain}{rule#}
-L == List
-P == Change policy for chain
-S == Rules
-P == protocol
--sport/--dport == source/destnation port
-d == destination
-s == source
-j == jump to action
-n == port num instead of service
-t == table
--line numbers == prints rule number in output

iptables -t [table] -A [chain] [rules] -j [action]

iptables -t [table] -L --line-numbers

iptables -t [table] -I [chain] [rule#] [rules] -j [action]

iptables -t [table] -R [chain] [rule#] [rules] -j [action]

iptables -t [table] -D [chain] [rule#]

iptables -t [table] -L --line-numbers

iptables -t [table] -P [chain] [action] == CHANGE DEFAULT POLICY TO ACCEPT TRAFFIC BEFORE FLUSHING TABLE

iptables -t [table] -F == flush all rules for a table

Rules:

-i or -o [iface]
-s or -d [ip.add | network/mask]
-p [protocol(in ipv4 header)]

-m is used with:
  state --state [state]
  mac [--mac-source | --mac-destination] [mac]
  tcp | udp [--dport | --sport] [port | port1:port2]
  multiport [--sports | --dports | --ports]
                [port1,[port2,[port3:port15]]]
  bpf --bytecode [ 'bytecode' ]

[action] - ACCEPT, REJECT, DROP

```

## NFTABLES
```
NFTABLE Families:
ip - IPv4 packets

ip6 - IPv6 packets

inet - IPv4 and IPv6 packets

arp - layer 2

bridge - processing traffic/packets traversing bridges.

netdev - allows for user classification of packets - nftables passes up to the networking stack
(no counterpart in iptables)

INTRODUCES CHAIN-TYPES
There are three chain types:

filter - to filter packets - can be used with arp, bridge, ip, ip6, and inet families

route - to reroute packets - can be used with ip and ipv6 families only

nat - used for Network Address Translation - used with ip and ip6 table families only

CREATION OF HOOKS
PREROUTING

POSTROUTING

INPUT

OUTPUT

FORWARD

INGRESS - used with NETDEV family only

```

## NFTABLES SYNTAX
```

nft add table [family] [table]
[family] = ip, ip6, inet, arp, bridge and netdev.
[table] = user provided name for the table.

Create base chain
nft add chain [family] [table] [chain] { type [type] hook [hook]
    priority [priority] \; policy [policy] \;}
[chain] = User defined name for the chain.
[type] =  can be filter, route or nat.
[hook] = prerouting, ingress, input, forward, output or
         postrouting.
[priority] = user provided integer. Lower number = higher
             priority. default = 0. Use "--" before
             negative numbers.
; [policy] ; = set policy for the chain. Can be
              accept (default) or drop.
 Use "\" to escape the ";" in bash

create rule for chain
nft add rule [family] [table] [chain] [matches (matches)] [statement]
[matches] = typically protocol headers(i.e. ip, ip6, tcp,
            udp, icmp, ether, etc)
(matches) = these are specific to the [matches] field.
[statement] = action performed when packet is matched. Some
              examples are: log, accept, drop, reject,
              counter, nat (dnat, snat, masquerade)

MODIFY NFTABLES
nft {list | flush} ruleset
nft {delete | list | flush } table [family] [table]
nft {delete | list | flush } chain [family] [table] [chain]

MODIFY NFTABLES
nft list table [family] [table] [-a]
Adds after position
nft add rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
Inserts before position
nft insert rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
Replaces rule at handle
nft replace rule [family] [table] [chain] [handle <handle>] [matches (matches)] [statement]
Deletes rule at handle
nft delete rule [family] [table] [chain] [handle <handle>]

```

## DEMO
```

iptables -A INPUT -m state  --state INVALID -j DROP -- drops invalid packets

iptables -A INPUT -f -j DROP -- drops fragmented packets

iptables -A INPUT -i eth0 -p tcp --syn -m limit --limit 10/second -j ACCEPT -- only accepts a max of 10 syn packets per second 

iptables -save > coscipt.conf -- saves configuration to a file

iptables-restore < coscipt.conf -v -- loads configuration from a file

```

## nftables
```

ct state invalid
ip frag-off !=0
tcp flags syn limit rate 10/second accept

sudo nft add rule ip COSC input ip saddr 172.16.82.112 ct state { NEW, ESTABLISHED } accept


```

## NAT (Network Address Translation)
```

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 1.1.1.1 ---- packet that leaves box looks like it came from 1.1.1.1

iptables -t nat -A PREROUTING -o eth0 -j DNAT --to 10.0.0.1

iptables -t nat -A POSTROUTING -p tcp -o eth0 -j SNAT --to 1.1.1.1:9001

iptables -t nat -A PREROUTING -p tcp -i eth0 -j DNAT --to 10.0.0.1:8080


NFTABLES:

nft add table NAT
nft add chain NAT PREROUTING { type nat hook prerouting priority 0 \; }
nft add chain NAT POSTROUTING { type nat hook postrouting priority 100 \; }

nft add rule NAT POSTROUTING ip saddr 10.1.0.2 oif eth0 snat 144.15.60.11
nft add rule NAT PREROUTING iif eth0 tcp dport { 80, 443 } dnat 10.1.0.3
nft add rule NAT POSTROUTING ip saddr 10.1.0.0/24 oif eth0 masquerade
nft add rule NAT PREROUTING tcp dport 80 redirect 8080

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

