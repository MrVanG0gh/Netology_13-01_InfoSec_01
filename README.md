# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - `Иншаков Владимир`

---

## Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя nmap.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?
Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
Приведите ответ в свободной форме.

## Решение 1


Осуществим сканирование виртуальной машины "Metasploitable" в агрессивном режиме. Адрес системы: 192.168.1.123
```
┌──(kali㉿kali)-[~]
└─$ nmap -A 192.168.1.123
Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-07 08:33 EDT
Nmap scan report for 192.168.1.123
Host is up (0.0049s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.1.115
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
| ssl-cert: Subject: commonName=ubuntu804-base.localdomain/organizationName=OCOSA/stateOrProvinceName=There is no such thing outside US/countryName=XX
| Not valid before: 2010-03-17T14:07:45
|_Not valid after:  2010-04-16T14:07:45
|_smtp-commands: metasploitable.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
|_ssl-date: 2025-10-07T12:34:14+00:00; -2s from scanner time.
53/tcp   open  domain      ISC BIND 9.4.2
| dns-nsid: 
|_  bind.version: 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
|_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
|_http-title: Metasploitable2 - Linux
111/tcp  open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/udp   nfs
|   100005  1,2,3      44059/tcp   mountd
|   100005  1,2,3      57979/udp   mountd
|   100021  1,3,4      42841/tcp   nlockmgr
|   100021  1,3,4      51759/udp   nlockmgr
|   100024  1          37923/tcp   status
|_  100024  1          39212/udp   status
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  tcpwrapped
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
| mysql-info: 
|   Protocol: 10
|   Version: 5.0.51a-3ubuntu5
|   Thread ID: 10
|   Capabilities flags: 43564
|   Some Capabilities: SupportsCompression, Support41Auth, LongColumnFlag, SwitchToSSLAfterHandshake, SupportsTransactions, Speaks41ProtocolNew, ConnectWithDatabase
|   Status: Autocommit
|_  Salt: .:ubkpsoT7Rz1!NIa,WP
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
|_ssl-date: 2025-10-07T12:34:15+00:00; -2s from scanner time.
| ssl-cert: Subject: commonName=ubuntu804-base.localdomain/organizationName=OCOSA/stateOrProvinceName=There is no such thing outside US/countryName=XX
| Not valid before: 2010-03-17T14:07:45
|_Not valid after:  2010-04-16T14:07:45
5900/tcp open  vnc         VNC (protocol 3.3)
| vnc-info: 
|   Protocol version: 3.3
|   Security types: 
|_    VNC Authentication (2)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
| irc-info: 
|   users: 1
|   servers: 1
|   lusers: 1
|   lservers: 0
|   server: irc.Metasploitable.LAN
|   version: Unreal3.2.8.1. irc.Metasploitable.LAN 
|   uptime: 0 days, 0:05:12
|   source ident: nmap
|   source host: 2FEE2FEF.78DED367.FFFA6D49.IP
|_  error: Closing Link: jstomxrof[192.168.1.115] (Quit: jstomxrof)
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
|_http-title: Apache Tomcat/5.5
|_http-server-header: Apache-Coyote/1.1
|_http-favicon: Apache Tomcat
Device type: bridge|VoIP adapter|general purpose
Running (JUST GUESSING): Oracle Virtualbox (94%), Slirp (94%), AT&T embedded (92%), QEMU (90%)
OS CPE: cpe:/o:oracle:virtualbox cpe:/a:danny_gasparovski:slirp cpe:/a:qemu:qemu
Aggressive OS guesses: Oracle Virtualbox Slirp NAT bridge (94%), AT&T BGW210 voice gateway (92%), QEMU user mode net
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_

Host script results:
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: metasploitable
|   NetBIOS computer name: 
|   Domain name: localdomain
|   FQDN: metasploitable.localdomain
|_  System time: 2025-10-07T08:34:03-04:00
|_nbstat: NetBIOS name: METASPLOITABLE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smb2-time: Protocol negotiation failed (SMB2)
|_clock-skew: mean: 59m58s, deviation: 2h00m00s, median: -2s

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   0.12 ms 192.168.1.123

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 67.40 seconds

```
Анализ показал, что на удаленной машине разрешены службы (порт и L4-протокол):
- ftp 21/tcp
- ssh 22/tcp
- telnet 23/tcp
- smtp 25/tcp
- domain 53/tcp
- http 80/tcp
- rpcbind 111/tcp
- netbios-ssn 139/tcp
- netbios-ssn 445/tcp
- exec 512/tcp
- login 513/tcp
- tcpwrapped 514/tcp
- java-rmi 1099/tcp
- bindshell 1524/tcp
- nfs 2049/tcp
- ftp 2121/tcp
- mysql 3306/tcp
- postgresql 5432/tcp
- vnc 5900/tcp
- X11 6000/tcp
- irc 6667/tcp
- ajp13 8009/tcp
- http 8180/tcp

Теперь мы знаем какие службы на каких портах работают. С учетом известных версий найдем возможные уязвимости для 5 из них:

-   ftp 21/tcp - vsftpd 2.3.4 - https://www.exploit-db.com/exploits/49757
-   mysql 3306/tcp - MySQL 5.0.51a-3ubuntu5 - https://www.exploit-db.com/exploits/30020
-   netbios-ssn 445/tcp - Samba smbd 3.0.20-Debian (workgroup: WORKGROUP) - https://www.exploit-db.com/exploits/16320
-   mysql 3306/tcp - MySQL 5.0.51a-3ubuntu5 - https://www.exploit-db.com/exploits/30020
-   postgresql 5432/tcp - PostgreSQL DB 8.3.0 - 8.3.7 - https://www.exploit-db.com/exploits/7855

---


## Задание 2
Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
Как отвечает сервер?
Приведите ответ в свободной форме.

## Решение 2

Проведем сканирование в различных режимах.

Начнем с SYN

```
nmap -sS 192.168.1.123
```

![Screen_1](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/Screenshots/Screenshot_1.png)
[Link to pcap](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/pcaps/Metasploited_sS.pcapng)

Здесь видно, что при сканировании nmap передает L4-сегмент c поднятым флагом SYN (попытка установления соединения на отдельно взятом порте).
Ответ сервера может содержать сегмент с флагами [SYN, ACK] - порт открыт, либо с [RST, ACK] - порт закрыт.

Затем в режиме FIN

```
nmap -sF 192.168.1.123
```

![Screen_2](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/Screenshots/Screenshot_6.png)
[Link to pcap](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/pcaps/Metasploited_sF.pcapng)

Здесь видно, что при сканировании nmap передает L4-сегмент c поднятым флагом FIN (попытка завершить установленное соединение).
Ответ сервера позволяет сделать вывод о том, закрыт ли порт (в ответном сегменте будут подняты флаги [RST, ACK], либо он открыт/фильтруется (об этом говорит отсутствие ответа от сервера)

В режиме Xmas

```
nmap -sX 192.168.1.123
```

![Screen_3](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/Screenshots/Screenshot_3.png)
[Link to pcap](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/pcaps/Metasploited_sX.pcapng)

В данном случае мы передаем сегменты с поднятыми флагами [FIN, PSH, URG]
Проявление очень схоже с режимом FIN (также отсутствие ответа говорит о том, что порт открыт/фильтруется). Если порт закрыт, то в ответном сегменте 
будут подняты флаги [ACK, RST]

И в режиме UDP

```
nmap -sU 192.168.1.123
```

![Screen_4](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/Screenshots/Screenshot_4.png)
[Link to pcap](https://github.com/MrVanG0gh/Netology_13-01_InfoSec_01/blob/main/pcaps/Metasploited_sU.pcapng)

Этот способ оказался самым долгим из испробованных. Здесь мы проверяем открытые порты сервера для работы по протоколу UDP.
Если на наш запрос пришла ответная дейтаграмма, значит порт открыт. Если мы получили ответ по протоколу ICMP (порт недоступен), значит порт - закрыт.
Если ответа после направления нескольких дейтаграмм нет - значит порт либо открыт, либо фильтруется.


---