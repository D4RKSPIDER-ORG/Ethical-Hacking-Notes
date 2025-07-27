**📌 Hello Cybersecurity Enthusiasts**

I am continuing with TryHackMe WriteUps. These write-ups are not just solution shares but also a source of encouragement for those at the beginning of their cybersecurity journey. Every step is a milestone in the endless journey of knowledge.

• 🗂️ **Room Name:** Light (CTF)

• 📜 **Description:** Welcome to the Light database application!

• 🔗 **Room URL:** [https://tryhackme.com/r/room/lightroom](https://tryhackme.com/r/room/lightroom)

• **⚡ Difficulty Level:** Easy

• 🏹 **Included in Paths:** -

• **🔍 Specifically Tools Mentioned in Room:** -

• 🛠️ **Types of Tools Used in Room:** -

• **🛠️ Tools Used in Room:** -

• **🎯 Target System:** Database

• **🏳️ Relevant Team:** 🔴 Red

![](https://miro.medium.com/v2/resize:fit:688/0*7qiWLkFC27KFTwuf)

# Task 1 — Welcome

## 1.1 What is the admin username?

We need to find the admin username. Now let’s first establish our connection to the target as specified:

nc 10.10.82.164 1337

![](https://miro.medium.com/v2/resize:fit:875/1*JBwWtvEfZJamYsJUaQX4NQ.png)

Our username was given as “smokey”:

![](https://miro.medium.com/v2/resize:fit:875/1*IfuvaNvIV6xEJi2RH4CHXw.png)

Normally, when we log in to any system, we enter our username and password, and if the username and password match correctly, the other system will add us to the system.

But here, when we enter the username, a string that reminds us of the password from the target system is returned to us. Moreover, the system puts us in the “Please enter your username” loop at the first login.

The only thing we have control over right now is entering the username. Let’s test the system with a few different usernames:

![](https://miro.medium.com/v2/resize:fit:875/1*vyVK-p5uJVJygWfssmuaUg.png)

Now we understand what is happening in the other system. In fact, there is a service that sends back the password of the user name we enter. So how does it do this? Let’s think with SQL query logic:

SELECT password FROM USER_DB_NAME WHERE username = "INPUT";

Let’s examine the part we can change in bold and take a closer look:

> SELECT password FROM USER_DB_NAME WHERE username = “**INPUT**”;

In other words, whatever input we enter is replaced by INPUT.

The username requested from us in the question is admin. So the command we want to run would be:

SELECT username FROM USER_DB_NAME;

Now let’s test whether we can perform SQL Injection with various strings:

![](https://miro.medium.com/v2/resize:fit:875/1*pMmS9VYRilZfkIVthmJGyg.png)

Here we are trying various payloads but we can’t find anything. Let’s go a little further:

![](https://miro.medium.com/v2/resize:fit:875/1*XU2G_p3AJ1OK_J_u_RULsw.png)

When we still can’t get results, we decide to collect intelligence directly on the table’s columns:

Let’s see if we can use the sqlite_master file, which is a critical table:

![](https://miro.medium.com/v2/resize:fit:875/1*_UAFvVnD-TvDw9dcqv-Z9w.png)

![](https://miro.medium.com/v2/resize:fit:875/1*14DqIaiaxqZHomDFjaefEA.png)

Good! At least we can see that the columns in the table are “username” and “password”.

![](https://miro.medium.com/v2/resize:fit:875/1*0YE78sFRLdNtuYFBSqCoHw.png)

We have seen another unnecessary and insufficient measure. UNION and SELECT are not accepted, but Union and Select are accepted.

![](https://miro.medium.com/v2/resize:fit:875/1*lNWZcnAGqbQT48t3i4pQ_w.png)

Yes, we found a way to print any argument to the screen. Now let’s see what kind of useful information we can get:

Let’s see what kind of information we can get from our special sqlite_master table:

![](https://miro.medium.com/v2/resize:fit:875/1*WrX8kIxZir6QL29D7iwPAg.png)

Great! Here we see that there is a “usertable” and an “admintable”. Since the admin username is what is asked of us in the question, we need to focus on the admintable now:

![](https://miro.medium.com/v2/resize:fit:875/1*vj8eQ5byns_yYDIsvFMT2w.png)

What is this! 3 data were returned with a query. And I don’t know if you noticed, 3 data are the answers to 3 different questions. Now let’s place the answers one by one:

![](https://miro.medium.com/v2/resize:fit:875/1*trxrT4xmG_nqrg_UbqZXQw.png)

> **_Answer:_** TryHackMeAdmin

## 1.2 What is the password to the username mentioned in question 1?

![](https://miro.medium.com/v2/resize:fit:875/1*3gMfnC81WDur9b0-RM_dWQ.png)

> **_Answer:_** mamZtAuMlrsEy5bp6q17

## 1.3 What is the flag?

![](https://miro.medium.com/v2/resize:fit:875/1*rdLG23zjLg7nagtqHhovjA.png)

> **_Answer:_** THM{SQLit3_InJ3cTion_is_SimplE_nO?}

It was actually a nice challenge. However, it would have been more educational if expressions like -, #, /* were not prohibited. Also, I don’t think the difficulty of the room is easy. It would have been more realistic if the difficulty of this room, which may be difficult for beginners, was classified as Medium.

The biggest lesson we will learn from the room is that although we take many security measures, access to special tables and databases (such as sqlite_master, information.schema) must also be controlled and blocked, otherwise the measures we take are useless.

I’ve not only tried to explain what works but also to highlight what doesn’t, providing detailed information to help beginners gain a better perspective. I hope it has been informative enough!