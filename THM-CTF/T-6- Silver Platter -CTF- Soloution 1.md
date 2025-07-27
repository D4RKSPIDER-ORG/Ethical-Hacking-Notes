We will start off with a standard nmap scan

![](https://miro.medium.com/v2/resize:fit:875/1*8YO2qnFBl_D1kyu89yTaUQ.png)

While this runs, we will visit the website

![](https://miro.medium.com/v2/resize:fit:875/1*lj8OUC1GkFb01iaxYb8Zhw.png)

If we click on the Contact link, we have a possible username

![](https://miro.medium.com/v2/resize:fit:875/1*5EveVtYBtuOLewMGG8HY8g.png)

Given that the nmap scan is going to take about 3 hrs to complete, decided to stop it and move on since ports 22, 80, and 8080 are open

![](https://miro.medium.com/v2/resize:fit:875/1*drUskOKUMS4prRSezzQZBw.png)

Running a gobuster scan to look for sub-directories on port 8080, so find 2

![](https://miro.medium.com/v2/resize:fit:875/1*XAcx_zytjgyX1-A2QNlTDQ.png)

/console gives us a 404 Not Found

![](https://miro.medium.com/v2/resize:fit:875/1*soz2SAdiwDKUt8G_dUIcFw.png)

/website gives us a 403 Forbidden

![](https://miro.medium.com/v2/resize:fit:875/1*j_V5P0roSw8zSYo16-Ifwg.png)

Trying some simple bypass techniques don’t work

[

## GitHub - LucasPDiniz/403-Bypass: Bypass 403 pages

### Bypass 403 pages. Contribute to LucasPDiniz/403-Bypass development by creating an account on GitHub.

github.com



](https://github.com/LucasPDiniz/403-Bypass?tab=readme-ov-file&source=post_page-----d89720449405---------------------------------------)

If we refer back to the Contact page from earlier, it references an application called: Silverpeas, trying this as a directory gives us a login page

![](https://miro.medium.com/v2/resize:fit:875/1*iX0M9iudp9-sy-P5Xv2ybA.png)

Looks like Silverpeas is vulnerable to an authentication bypass

![](https://miro.medium.com/v2/resize:fit:875/1*qjXxfaBB95mKO8x-at8E9w.png)

![](https://miro.medium.com/v2/resize:fit:875/1*4AEadrh1WyErnysvT4LONw.png)

![](https://miro.medium.com/v2/resize:fit:875/1*1Ee0ykIWQvPjXKqvWivj1g.png)

![](https://miro.medium.com/v2/resize:fit:875/1*Zg8CCNUIt7107pwgHs4EHQ.png)

Once we change our username to SilverAdmin, we will be logged in

![](https://miro.medium.com/v2/resize:fit:875/1*lJrFpIhqbH5okiEUlchZaQ.png)

Since the site is in a language I don’t understand, I decided to look for other CVEs

![](https://miro.medium.com/v2/resize:fit:875/1*mwRiYnBqZ0QZFMZ280XONw.png)

Let’s take a look at the All Messages one

![](https://miro.medium.com/v2/resize:fit:875/1*0JkrSwgQH2RpMO8U0T7JZA.png)

![](https://miro.medium.com/v2/resize:fit:875/1*C2yZJQNdyne1_o38_dGc3A.png)

All we have to do is keep incrementing the number to see if we come across anything useful

![](https://miro.medium.com/v2/resize:fit:875/1*nHyxB8oX3Bfg7RnDQZVwJQ.png)

Username: time

```
Password: cm0nt!md0ntf0rg3tth!spa$$w0rdagainlol
```

All we have to do is SSH in as tim

![](https://miro.medium.com/v2/resize:fit:875/1*xDfvrDTxOUFFsuTK3Q2vOQ.png)

What is the user flag?

![](https://miro.medium.com/v2/resize:fit:875/1*kECmlxCkFDNzpGxx4gc9fg.png)

Answer: **THM{c4ca4238a0b923820dcc509a6f75849b}**

Off to go figure out how to escalate privileges to root

Running sudo -l, gives us nothing of value

![](https://miro.medium.com/v2/resize:fit:875/1*imoMxi_EOqynbVusgYaw7w.png)

There is nothing in the home directory that is word writable, but we also can’t access Tyler’s home directory either

![](https://miro.medium.com/v2/resize:fit:875/1*XUcLJn9JX_Tw7yNupv0rAw.png)

Checking for SUID, nothing screams out to me

![](https://miro.medium.com/v2/resize:fit:875/1*8YF1zL04EsdS4ktiS00dZQ.png)

Running the command id shows that we are a part of the Admin group

![](https://miro.medium.com/v2/resize:fit:875/1*xPuLnFwUcscNXTezL4k67w.png)

Greping for pass within the /var/log directory shows a password

![](https://miro.medium.com/v2/resize:fit:875/1*lv-N3EcBw5CvU9fDawds1A.png)

su’ing as tyler using the password: _Zd_zx7N823/ gets us in

![](https://miro.medium.com/v2/resize:fit:795/1*meYmZPppUj9Ib-6jf3A2vQ.png)

This is a super bad idea, if we run sudo -l, tyler can run any and all commands

![](https://miro.medium.com/v2/resize:fit:875/1*MA17SBJkwHNQ4bKJLWArBg.png)

What is the root flag?

All we have to do is run sudo su

![](https://miro.medium.com/v2/resize:fit:875/1*QKWF-vpi026DQtMwYSGkog.png)

Answer: **THM{098f6bcd4621d373cade4e832627b4f6}**