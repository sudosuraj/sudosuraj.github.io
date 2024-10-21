---
layout: post
title:  HackTheBox Sightless Walkthrough
author:  'Suraj Sharma (sudosuraj)'
categories:  [walkthourgh]
tags:  [HTB, sightless hackthebox, CTF]
image:
  path: /assets/img/sightless/image.png
  alt: "HTB sightless"
Status: Compleated
Domain Name: sightless.htb, sqlpad.sightless.htb
Type: Machine
Date: October 18, 2024
Initial Foothold: Docker, to SSH via abusing misconfigured permission of /etc/passwd and /etc/shadow file.
Notes: 
    Initial Access
        - Exploited SQLPad vulnerability (CVE-2022-0944) to gain access to a Docker container
        - Utilized misconfigured permissions on /etc/passwd and /etc/shadow to obtain user credentials
        - Successfully SSH'd into the machine as user Michael
    Privilege Escalation
        - Discovered multiple open internal ports using netstat
        - Exploited Chrome Remote Debugger to access Froxlor dashboard
        - Utilized a PHP-FPM configuration issue in Froxlor to escalate privileges and read root flag

Flags:
    - User flag: be54c4881a877da404570f49f3230f97
    - Root flag: 5c8445dd206dca771fbc7d15e48a5c84

Privilege Escalatin: CHROME Drive Exploit to web app debugging and gaining administrator access to froxlor admin page, in froxlor the PHP-FPM was being run by root user, using that, we managed to read the /root/root.txt file.

Shell Type: Limited Shell
---

![image.png](/assets/img/sightless/image.png)

[Owned Sightless from Hack The Box!](https://www.hackthebox.com/achievement/machine/539268/624?ref=ecorpsecurity.com)

# USER FLAG:

## Nmap scan with minmap script:

![image.png](/assets/img/sightless/image%201.png)

```
┌──(kali㉿kali)-[~/HTB/sightless]
└─$ minmap 10.10.11.32 | tee -a nmap.txt
[sudo] password for kali:
open ports: 21,22,80
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-18 19:12 IST
Nmap scan report for sqlpad.sightless.htb (10.10.11.32)
Host is up (0.37s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp
| fingerprint-strings:
|   GenericLines:
|     220 ProFTPD Server (sightless.htb FTP Server) [::ffff:10.10.11.32]
|     Invalid command: try being more creative
|_    Invalid command: try being more creative
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 c9:6e:3b:8f:c6:03:29:05:e5:a0:ca:00:90:c9:5c:52 (ECDSA)
|_  256 9b:de:3a:27:77:3b:1b:e1:19:5f:16:11:be:70:e0:56 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: SQLPad
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port21-TCP:V=7.94SVN%I=7%D=10/18%Time=671265BA%P=x86_64-pc-linux-gnu%r(
SF:GenericLines,A0,"220\x20ProFTPD\x20Server\x20\(sightless\.htb\x20FTP\x2
SF:0Server\)\x20\[::ffff:10\.10\.11\.32\]\r\n500\x20Invalid\x20command:\x2
SF:0try\x20being\x20more\x20creative\r\n500\x20Invalid\x20command:\x20try\
SF:x20being\x20more\x20creative\r\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 80.02 seconds
```

We found open ports and running services, lets first add the domain in /etc/passwd file.

```bash
┌──(kali㉿kali)-[~/HTB/sightless]
└─$ echo -e '10.10.11.32\tsightless.htb' | tee -a /etc/hosts
```

Visiting the domain, we found simple page with minimal functionalities, and one virtual host called `sqlpad.sightless.htb`

![image.png](/assets/img/sightless/image%202.png)

lets add this to `/etc/hosts` file:

```bash
┌──(kali㉿kali)-[~/HTB/sightless]
└─$ echo -e '10.10.11.32\tsqlpad.sightless.htb' | sudo tee -a /etc/hosts
```

After visiting the virtual host, we found its version, lets search for public exploit on google:

![image.png](/assets/img/sightless/image%203.png)

![image.png](/assets/img/sightless/image%204.png)

The following exploit, referring CVE-2022-0944 is simple to exploit, lets use this.

![image.png](/assets/img/sightless/image%205.png)

Download the exploit.py locally and run it with python3, this exploit needs target URL, attacker IP, and port, before that, open a netcat listener on any port and enter the same port in exploit.

![image.png](/assets/img/sightless/image%206.png)

We got the shell. Yehoo :) 

![https://media2.giphy.com/media/ihSdWLKtcMlvCb9FhD/giphy.gif?cid=7941fdc65o128qk4xtys46yupu45cwswrgwhj4gjk915ss6g&ep=v1_gifs_search&rid=giphy.gif&ct=g](https://media2.giphy.com/media/ihSdWLKtcMlvCb9FhD/giphy.gif?cid=7941fdc65o128qk4xtys46yupu45cwswrgwhj4gjk915ss6g&ep=v1_gifs_search&rid=giphy.gif&ct=g)

But wait!!!! Isn’t it fishy? How we got the root ‘#’ shell directly? Let’s see where we are.

Ah!, we are inside the docker, we are trapped, but not so late, lets enumerate the docker.

![image.png](/assets/img/sightless/image%207.png)

In the docker, we have read permission of `/etc/passwd` and `/etc/shadow` files, that the good hit now. Lets copy them to our attacker machine to crack the password

  

![image.png](/assets/img/sightless/image%208.png)

![image.png](/assets/img/sightless/image%209.png)

![image.png](/assets/img/sightless/image%2010.png)

We saved the `/etc/passwd` file as passwd and `/etc/shadow` file as shadow. To crack password, run the following commands:

![image.png](/assets/img/sightless/image%2011.png)

![image.png](/assets/img/sightless/image%2012.png)

We got root and Michael user’s password. lets try to SSH into the target host directly. Unfortunately, the root user’s password isn’t working but we got SSH into Michael’s shell.

![image.png](/assets/img/sightless/image%2013.png)

And we go the user’s flag:

![image.png](/assets/img/sightless/image%2014.png)

# ROOT FLAG

For privilege escalation, we enumerated internal services, and found multiple opened ports internally, using `netstat -tunlp` command:

![image.png](/assets/img/sightless/image%2015.png)

Copy all LISTEN ports and save them into `ports.txt`, use the following script to forward all port in one command.

```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 2 ]; then
  echo "Usage: $0 <username> <remote_host>"
  exit 1
fi

# Assign the first and second arguments to variables
REMOTE_USER="$1"
REMOTE_HOST="$2"

# Read the ports from the ports.txt file and build the SSH command
SSH_COMMAND="ssh -f"

# Loop through each line in the file
while read -r PORT; do
  # Append port forwarding (same port for both local and remote) to the SSH command
  SSH_COMMAND+=" -L $PORT:localhost:$PORT"
done < ports.txt

# Append the user and host to the SSH command
SSH_COMMAND+=" $REMOTE_USER@$REMOTE_HOST -N"

# Execute the SSH command
eval $SSH_COMMAND

# Notify that the ports are being forwarded
echo "Port forwarding established for ports listed in ports.txt."
```

![image.png](/assets/img/sightless/image%2016.png)

![image.png](/assets/img/sightless/image%2017.png)

### Exploiting Chrome Remote Debugger

For getting access to Froxlor dashboard, we can use chrome remote debugger exploit ([Link](https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/chrome-remote-debugger-pentesting/)).

Click configure and enter all ports with host-name as 127.0.0.1

![image.png](/assets/img/sightless/image%2018.png)

![image.png](/assets/img/sightless/image%2019.png)

![image.png](/assets/img/sightless/image%2020.png)

After saving above, we get new buttons, click inspect and you’ll find the username password in the payload section of index file. Use it to login at `http://127.0.0.1:8080`

![image.png](/assets/img/sightless/image%2021.png)

1. Visit [`http://127.0.0.1:8080/admin_phpsettings.php?page=fpmdaemons`](http://127.0.0.1:8080/admin_phpsettings.php?page=fpmdaemons) and click create new PHP version.

![image.png](/assets/img/sightless/image%2022.png)

1. In the `php-fpm restart command` section, input the `cp /root/root.txt /tmp/root.txt` , add any description and click save.

![image.png](/assets/img/sightless/image%2023.png)

![image.png](/assets/img/sightless/image%2024.png)

1. Now visit [`http://127.0.0.1:8080/admin_settings.php/?page=overview&part=phpfpm`](http://127.0.0.1:8080/admin_settings.php/?page=overview&part=phpfpm) , disable the PHP-FPM from here, click save.

![image.png](/assets/img/sightless/image%2025.png)

1. Now, verify the `/tmp/root.txt`  

![image.png](/assets/img/sightless/image%2026.png)

1. The file is here, but we don’t have any read permission as Michael user, lets change the permission via repeating the steps 1 to steps 3, just change the command to `chmod 644 /tmp/root.txt`  in the step 2.

![image.png](/assets/img/sightless/image%2027.png)

![image.png](/assets/img/sightless/image%2028.png)

![image.png](/assets/img/sightless/image%2029.png)