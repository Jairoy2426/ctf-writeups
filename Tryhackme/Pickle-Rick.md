---
title: "Pickle Rick - THM Writeup"
difficulty: "Easy"
tags: ["gobuster", "netcat", "reverse-shell"]
platform: "Try Hack Me"
date: "2020-05-17"
author: "Jai Roy / Hercules"
---

# Writeup Title

**Introduction :**
The purpose of this writeup is to document the steps I took to complete Tryhackme.com (THM)'s room Pickle Rick hacking tasks.

**Resources/Tools Used :**

[Task 1] Pickle Rick

> Gobuster
> http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
> Netcat

This Ricky and Morty themed challenge requires you to exploit a webserver to find three ingredients that will help Rick make his potion to transform himself back to a human from a pickle. 

**#1 This subtask requires you to find first ingredient.**

First ingredient was found by following these steps:

- Browsed to webpage.

![Webpage](![alt text](https://h3rcules.space/u/qa601D.png))

- Reviewed the source of this page that gave a username "R1ckRul3s".

![Username-Discovered](![alt text](https://h3rcules.space/u/dUTgbI.png))

- Browsed to “robots.txt” file and found one interesting piece of information there.

![Robots-File](![alt text](https://h3rcules.space/u/obnrwC.png))

- Used gobuster to brute force directories to discover directories and pages on this website. Gobuster discovered few interesting pages.

![Gobuster-Output](![alt text](https://h3rcules.space/u/JkWwMM.png))

- Browsed to “login.php” and found a login page asking for a username and password. Tried information gathered in previous steps to login to this portal.

![login.php](![alt text](https://h3rcules.space/u/95eVqn.png))
![Credentials](![alt text](https://h3rcules.space/u/02q4D4.png))
![Login-Successful](![alt text](https://h3rcules.space/u/uEcCE8.png))

- Tried listing the contents of directory.

![Directory-Listing](![alt text](https://h3rcules.space/u/msnn5v.png))

- Saw an interesting file “Sup3rS3cretPickl3Ingred.txt” but could not read contents of the file (using cat) as this functionality was disabled on the server.

![Try-To-Read-Files](![alt text](https://h3rcules.space/u/8OImsU.png))
![Cat-Disabled](![alt text](https://h3rcules.space/u/LoIqPz.png))

- As this was a very restrictive environment, tried getting a reverse shell from the server. First tried to identify if python (python2 was not available) is available on the server.

![python3-check](![alt text](https://h3rcules.space/u/SXKDQx.png))
![python3-available](![alt text](https://h3rcules.space/u/umrGVx.png))

- We had python3 available on the server. Used pentestmonkey cheat sheet for python reverse shell. Started a netcat listener on port 4444 and copied the command and changed IP and port to reflect our attack machine IP and local port (running netcat).

![Python-reverse-shell-from-pentestmonkey-website](![alt text](https://h3rcules.space/u/DZ4noZ.png))

![Python-reverse-shell-command](![alt text](https://h3rcules.space/u/y8uz5D.png))
![Netcat-Listener](![alt text](https://h3rcules.space/u/2U8AQ3.png))

- Upon executing the python reverse shell command immediately got the shell with user “www-data” authority from system.

![reverse-shell](![alt text](https://h3rcules.space/u/g8MECl.png))

- From this folder got first ingredient.

![First-Ingredient](![alt text](https://h3rcules.space/u/Xa2ZF9.png))

- From this folder read the file “clue.txt” to see contents of the file for remaining ingredients.

![clue.txt](![alt text](https://h3rcules.space/u/tXLbTM.png))

**#2 This subtask requires you to find second ingredient.**

- Browsed to “/home/rick” folder to get the second ingredient.

![Second-Ingredient](![alt text](https://h3rcules.space/u/X8RoCj.png))

**#3 This subtask requires you to find third ingredient.**

- Tried accessing “/root” folder but access was denied to our current user (www-data).

![Root-folder-inaccessible](https://h3rcules.space/u/iCwHaB.png)

- For privilege escalation tried to identify what commands are allowed to current user with root privileges and to our surprise all commands were allowed without any password.

![sudo-l](https://h3rcules.space/u/se4xsw.png)

- Ran “sudo bash -i” to get root access to system.

![root-access](![alt text](https://h3rcules.space/u/9OEfrX.png))

- Browsed to “/root” folder to get the third and last ingredient.

![Third-and-last-ingredient](![alt text](https://h3rcules.space/u/uWsXmV.png))



**I hope this helped. Thanks.**