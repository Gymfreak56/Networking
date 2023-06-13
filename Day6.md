## SSH
```

ssh replaced rsh (remote shell)
authenticate
encryption
used for tunneling

```

## SSH Port Forwarding
```

uses SSH-CONN protocol
use other services with ssh tunnel(telnet through an ssh tunnel)

Local Port Forwardung:
ssh -p (alternate port) user@ip -L <port to open>:<tgt host>:port -NT
                                   (Start of tunnel)          (Port you want access to)

ssh user@tonyhost -L 3095:localhost:22 -NT
ssh user@localhost -p 3095 -L 22222:johnhost:443 -NT
wget -r https://localhost:22222 || firefox https://localhost:22222

Remote Port Forwarding:
ssh -p (alternate port) user@ip -R <remote bind>:<tgt host>:<Port> -NT
                               (start of tunnel(local box))  (port you want access to)

ssh student@ihost -R 4444:localhost:25 -NT
telnet localhost 4444 (test) > ehlo

(FROM TONYHOST) ssh student@ihost -R 5432:johnhost:23 -NT
(FROM IHOST) telnet localhost 5432

Johnhost> ssh tony@tonyhost -R 6789:localhost(johnhost):22
Tonyhost> ssh -p 6789 jony@localhost (test)
ihost> ssh tony@tonyhost -L 9135:localhost:6789
ihost> ssh -p 9135 john@localhost (test)

Dynamic Port Forwarding:
ssh -p (alternate port) user@ip(pivot ip) -D <port> -NT
proxy chains -- forwards ONLY TCP traffic through port
ssh -p 9135 john@localhost -D 9050 -NT

ihost> proxychains nmap -Pn <options> BillHost
ihost> proxychains wget -r billhost:8080
ihost> proxychains telnet billhost 25 (ehlo)

ihost> proxychains ./scan.sh
ihost> proxychains ./scan.py

ihost> proxychains wget -r ftp://Laurahost

ihost> ssh -p 9135 john@localhost -L 9898:amoshost:23 -NT
ihost> telnet localhost 9898
amos> ss -ntlp -> port 22 open
amos> ssh john@johnhost -R 8217:localhost:22 -NT
john> ssh -p 8217 amos@localhost (test)
ihost> ssh -p 9135 john@localhost -L 8210:localhost:8217 -NT
ihost> ssh -p 8210 amos@localhost (test)

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
