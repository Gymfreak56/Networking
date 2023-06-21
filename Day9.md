## COMMON IDS'
```

OSSEC
Snort
Suricata
Bro Network
Open WIPS
Samhain
Security Onion

```

## SNORT
```

[action] [protocol] [s.ip] [s.port] [direction] [d.ip] [d.port] ( match conditions ;)

Action - such as alert, log, pass, drop, reject
Protocol - includes TCP, UDP, ICMP and others
Source IP address - single address, CIDR notation, range, or any
Source Port - one, multiple, any, or range of ports
Direction - either inbound or in and outbound
Destination IP address - options mirror Source IP
Destination port - options mirror Source port


msg - specifies the human-readable alert message
reference - links to external source of the rule
sid - used to uniquely identify Snort rules
rev - uniquely identify revisions of Snort rules
Classtype - used to describe what a successful attack would do
priority - level of concern (1 - really bad, 2 - badish, 3 - informational)

content - looks for a string of text.
|binary data| - to look for a string of binary HEX
nocase - modified content, makes it case insensitive
depth - specify how many bytes into a packet Snort should search for the specified pattern
distance - how far into a packet Snort should ignore before starting to search for the specified pattern relative to the end of the previous pattern match
within - modifier that makes sure that at most N bytes are between pattern matches using the content keyword
offset - skips a certain number of bytes before searching (i.e. offset: 12)

Flow - direction (to/from client and server) and state of connection (established, stateless, stream/no stream)
ttl - The ttl keyword is used to check the IP time-to-live value.
tos - The tos keyword is used to check the IP TOS field for a specific value.
ipopts - The ipopts keyword is used to check if a specific IP option is present
seq - check for a specific TCP sequence number
ack - check for a specific TCP acknowledge number.
flags - The flags keyword is used to check if specific TCP flag bits are present.
itype - The itype keyword is used to check for a specific ICMP type value.
icode - The icode keyword is used to check for a specific ICMP code value.

logto - The logto keyword tells Snort to log all packets that trigger this rule to a special output log file.
session - The session keyword is built to extract user data from TCP Sessions.
react - This keyword implements an ability for users to react to traffic that matches a Snort rule by closing connection and sending a notice.
tag - The tag keyword allow rules to log more than just the single packet that triggered the rule.
activates - This keyword allows the rule writer to specify a rule to add when a specific network event occurs.
activated_by - This keyword allows the rule writer to dynamically enable a rule when a specific activate rule is triggered.
count - Allows the rule writer to specify how many packets to leave the rule enabled for after it is activated.

type [limit | threshold | both]
limit alerts on the 1st event during defined period then ignores the rest.
Threshold alerts every [x] times during defined period.
Both alerts once per time internal after seeing [x] amount of occurrences of event. It then ignores all other events during period.
track [by_src | by_dst] - rate is tracked either by source IP address, or destination IP address
count [#] - number of rule matching in [s] seconds that will cause event_filter limit to be exceeded
seconds [seconds] - time period over which count is accrued. [s] must be nonzero value

Look for anonymous ftp traffic:
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous"; sid:2121; )

This will cause the pattern matcher to start looking at byte 6 in the payload)
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous"; offset:5; sid:2121; )

This will search the first 14 bytes of the packet looking for the word “anonymous”.
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous"; depth:14; sid:2121; )

Deactivates the case sensitivity of a text search.
alert tcp any any -> any 21 (msg:"Anonymous FTP Login"; content: "anonymous"; nocase; sid:2121; )

snort --version == version

ps -elf | grep snort

snort.log.<timestamp>

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

## 
```



```

