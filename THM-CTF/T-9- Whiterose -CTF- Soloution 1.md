> Welcome to my writeup where I am gonna be pwning the **WhiteRose** machine from **TryHackMe**. This challenge has two flags, and our goal is to capture both. Let’s get started!

# GETTING STARTED

To access the challenge, click on the link given below:

[

## Whiterose

### Yet another Mr. Robot themed challenge.

tryhackme.com


> **This writeup documents the steps that successfully led to pwnage of the machine. It does not include the dead-end steps encountered during the process (which were numerous). This is just my take on pwning the machine and you are welcome to choose a different path.**

# RECONAISSANCE

I performed an **nmap** aggressive scan to find open ports and the services running on them.

![](https://miro.medium.com/v2/resize:fit:875/1*-yMDaFk4Fkjo-sO38QgkFg.png)

I also saved the credentials that were given to me by the creator.

![](https://miro.medium.com/v2/resize:fit:875/1*y1OQOgL1J7vENpLG59Lc6g.png)

# FOOTHOLD

Since the **nmap** scan revealed port 80 to be running, I tried to access it through my browser but couldn’t do so as the domain was not being identified. Hence, I manually mapped the domain to the machine IP in the _/etc/hosts_ file.

![](https://miro.medium.com/v2/resize:fit:875/1*0QK5P3bXJNjCQi0Q6eILaA.png)

I then tried accessing the website.

![](https://miro.medium.com/v2/resize:fit:875/1*zXjhFR6VRUJvxLEuDjoehg.png)

The home page revealed nothing interesting, so I tried brute forcing available subdomains.

![](https://miro.medium.com/v2/resize:fit:875/1*DYG1vnAQvxDzzl5MuffS2w.png)

> I initially tried fuzzing subdomains using **FUZZ.cyprus.thm** as the target without specifying the **Host** header but that didn’t work. So I looked around on the internet and found a better way of performing subdomain fuzzing. Here’s a breakdown simple explanation and purpose of the above command:
> 
> - The **/etc/hosts** entry maps the IP to a particular domain. This IP is only mapped to that particular domain and not to any subdomains related to it unless explicitly mentioned.
> 
> - The HTTP **Host** header is a part of web requests that tells the server which website the client wants to connect to. So if I type example.com, the browser sends a request with **Host: example.com** header.
> 
> - So I can use this mechanism to check if a particular IP has a subdomain in it by looking for different **Host** header values on a domain.
> 
> - Also, **-fw 1** Filters out responses with 1 word in the response, typically used to ignore consistent error responses.

After finding a subdomain, I mapped it in the _/etc/hosts_ file.

![](https://miro.medium.com/v2/resize:fit:875/1*OlOi911bC47JSl_iS6-ftA.png)

I navigated to the **admin** panel that I had discovered and tried logging in using the credentials that I had been given at the start.

![](https://miro.medium.com/v2/resize:fit:875/1*KNFL4f0Y_SP-hmMT1iPixw.png)

I logged in as **Olivia** and was able to view information about customers and their transactions.

![](https://miro.medium.com/v2/resize:fit:875/1*Wh82mxXNWazlXLdf8pJEGA.png)

I looked in the _Messages_ tab and found a bunch of messages.

![](https://miro.medium.com/v2/resize:fit:875/1*FLf_91SBGxw8juHv6PnfRg.png)

From the url, I found that the page displayed messages based on the parameter **c**. So I tried changing its value to view more messages. On **c=10**, I found the credentials of the privileged admin account.

![](https://miro.medium.com/v2/resize:fit:875/1*1q0hEBQkJLkBi6UGLP6Feg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*TIfemdk8-WNpc2x1E7rm1g.png)

I used these credentials to log in as a privileged user.

![](https://miro.medium.com/v2/resize:fit:875/1*tHihPM9smFuz0ih31hDh1w.png)

Now I could view information that was hidden from **Olivia**.

![](https://miro.medium.com/v2/resize:fit:875/1*-B_IGna4j-vpoB3d2pidPQ.png)

I visited the _Settings_ tab and found an option to change user passwords. I tried changing password of _Terry Colby_.

![](https://miro.medium.com/v2/resize:fit:875/1*clsbTnuqan4ftnrVqCSkyg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*a68-DvNWJetUQIMeTRO0Zg.png)

However, it didn’t actually work. I couldn’t log in as _Terry_ with the new password. So I sent another request and analyzed it on **Burp Suite**.

![](https://miro.medium.com/v2/resize:fit:875/1*egeaqoEnKEpvTetRPHaKfg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*aJo3gzyaHw7r7WsKageReA.png)

I forwarded the request to **Repeater** for further testing and analyzed the application behavior for different password values. I tested for SQL injection and empty password field but got no response in return.

![](https://miro.medium.com/v2/resize:fit:875/1*V7jDPTq8Nl-sOYr8EPc1cA.png)

However, when I removed the **password** field altogether, I received an error that revealed backend information.

![](https://miro.medium.com/v2/resize:fit:875/1*InMSAHzpyzasVNSs51qoww.png)

The error message specified **settings.ejs**. I did not know much about **ejs** so I asked **chatgpt**.

> EJS (Embedded JavaScript) is a templating engine for Node.js. It allows you to embed JavaScript code within HTML and helps you generate HTML markup with dynamic content. With EJS, you can create reusable templates that render data passed from the server, making it easier to build dynamic web applications.

Next, I looked for exploits on google and found a bunch of addressing a remote code execution vulnerability.

![](https://miro.medium.com/v2/resize:fit:875/1*VhhNSeDOzAWDNBkw2VkZkw.png)

So I then looked for **rce** exploits and found a bunch of articles.

![](https://miro.medium.com/v2/resize:fit:875/1*AkYf-ZPhsVrB8r-jtYYi0g.png)

![](https://miro.medium.com/v2/resize:fit:875/1*q-TxPQ-N3h-pKo3DYn-TCQ.png)

I appended the payload to my request and forwarded it. However, the **nc** version on the server did not support the **-e** argument.

![](https://miro.medium.com/v2/resize:fit:875/1*DqJ5FbnSz2FGiBYU9YDkyg.png)

Since, normal **nc** didn’t work, I visited **revshells** to look for other ways. The **busybox** payload worked.

![](https://miro.medium.com/v2/resize:fit:875/1*mmT8zWTiVdsBMVsw-5OofQ.png)

![](https://miro.medium.com/v2/resize:fit:875/1*EiJCFxU8rcn4h1PbCLbrvw.png)

Before forwarding the payload, I had started a reverse shell listener. Upon execution, I received a reverse shell.

![](https://miro.medium.com/v2/resize:fit:875/1*780IBvKVKvUCTTcA0ef-jw.png)

I found the first flag in the **web** user’s **home** directory.

![](https://miro.medium.com/v2/resize:fit:875/1*6iU9gu9F2SvglUe8xNQu8A.png)

# PRIVILEGE ESCALATION

I listed the **sudo** privileges of the user and found it could edit a configuration file. I viewed the file using the allowed command.

![](https://miro.medium.com/v2/resize:fit:875/1*7vt2-jrEYLl5fw2zn44hFQ.png)

![](https://miro.medium.com/v2/resize:fit:875/1*zoZRZt_BbP2nRo3Dxp35Ew.png)

The shell was super buggy and unstable, so I spawned a more robust shell using the following steps:

background current session using `ctrl+z`  
enter: `stty raw -echo; fg`

I did not have any idea as to what had to be done. So I looked for ways I could use the available command to escalate my privilege.

![](https://miro.medium.com/v2/resize:fit:875/1*CRETdQiUh1uE_hkArsvHGA.png)

I found an article that demonstrated a way to exploit this configuration.

![](https://miro.medium.com/v2/resize:fit:875/1*4aF2yLojbB2VxYB4Nepl2A.png)

Hence I followed the steps to set **vim** as the default editor for **/etc/sudoers** file.

export EDITOR="vim - /etc/sudoers"

![](https://miro.medium.com/v2/resize:fit:875/1*uqCRofCG1RRwqASQYQdR2A.png)

![](https://miro.medium.com/v2/resize:fit:875/1*V3U5cE2TR-TMC4UFh6g4HQ.png)

I then executed the available command.

![](https://miro.medium.com/v2/resize:fit:875/1*Om02PMKGcHAm6AIKEWOOAg.png)

This opened the **/etc/sudoers** file in **vim** editor. I simply allowed my user to execute all commands without a password similar to the **root** using the below command.

web ALL=(ALL:ALL) NOPASSWD: ALL

![](https://miro.medium.com/v2/resize:fit:875/1*JC8V3x96klIliKb8YVUeVg.png)

Finally, I switched to user using **sudo** to become **root** and captured the final flag from the **/root** directory.

![](https://miro.medium.com/v2/resize:fit:875/1*6oJL6YOtPb-BVqwwNcHgbw.png)