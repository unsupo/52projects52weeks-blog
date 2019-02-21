---
ID: 183
post_title: SSH Utility
author: jarndt
post_excerpt: ""
layout: post
permalink: >
  https://52projects52weeks.com/2019/02/21/ssh-utility/
published: true
post_date: 2019-02-21 22:15:05
---
<!-- wp:heading -->

## Introduction

<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->

### SSH

<!-- /wp:heading -->

<!-- wp:paragraph -->

SSH or secure shell is a way to login into a machine and send commands to it while logged in.  Once on a machine you can edit files, install and run application, ect. SSH is a secure way to send these commands to a machine, that way someone listening in doesn’t know what commands you’re sending and can’t send any themselves without logging in via SSH.  


<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### 2FA (Duo)

<!-- /wp:heading -->

<!-- wp:paragraph -->

Now depending on password strength, and other factors that I won’t go into related to network security,  it’s possible to hack into a machine through ssh. That’s why a 2 factor authentication is typically used to further protect a server from getting hacked.  2 factor authentication is simply having another device, typically your phone, help verify that it really is you logging into the machine. Typically a push is sent to your phone as a prompt you have to click yes to.  


<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

### User Login

<!-- /wp:heading -->

<!-- wp:paragraph -->

When you ssh into a machine, on machines that have been setup with user level authentication, you are logged in as your username.  However to increase security on the machine, some actions require you to become other users. So a command is required and your password and another duo prompt.  Becoming root gives you full authority over the machine, so things all users can do, root can do as well as things only root can do.  


<!-- /wp:paragraph -->

<!-- wp:heading -->

## Problem

<!-- /wp:heading -->

<!-- wp:paragraph -->

Almost daily I need to log into several machines a day and perform root operations.  So, I need to look up the machine’s host or ip and then log into that machine. This forces a password prompt and a duo prompt, then I need to be the root user and another password prompt and another duo prompt.  Then do these for sometimes 20 hosts in a day and you can see how this login process becomes tedious and time consuming.  


<!-- /wp:paragraph -->

<!-- wp:heading -->

## Solution

<!-- /wp:heading -->

<!-- wp:paragraph -->

So, to ease this process, I created an ssh utility.  This utility uses globbing to find hosts by name, which I can add aliases to to help me remember.  It then uses expect shell to login into the machine, send me a duo prompt, I then accept the prompt on my phone, then it logs me in as root and sends the duo prompt and then i accept that prompt as well.  Now i’m logged into the host with just one command and 2 prompts I simply wait for my phone to buzz me for.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Globbing is using the star character * to mean anything.  

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

For instance let’s say you had a list of words 

<!-- /wp:paragraph -->

<!-- wp:list -->

*   hi
*   bye
*   hello
*   help
*   byebye
*   high

<!-- /wp:list -->

<!-- wp:paragraph -->

if you used the glob: \*hi\* you would get 

<!-- /wp:paragraph -->

<!-- wp:list -->

*   hi
*   high

<!-- /wp:list -->

<!-- wp:paragraph -->

because * means anything before hi and then another star means anything after hi  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

So \*e\* would get:

<!-- /wp:paragraph -->

<!-- wp:list -->

*   bye
*   hello
*   help
*   byebye

<!-- /wp:list -->

<!-- wp:paragraph -->

because they all contain the letter e  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

My script creates a sqllite3 database.  Which is kind of like an excel spreadsheet.  It stores data in rows with columns being the identifier for that piece of data.  I simply insert into the database a list of ips and associated names that correspond to it and then glob for those names when trying to find the host i want to log into.  It also stores defaults, for instance my script wants to know what user you want to log into after logging into the server. So, instead of entering root everytime, add it as a default and it won’t ask anymore.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The script will also check if the host is available.  For instance if you try to ssh into a host that isn’t available, it will hang for a while before reporting that it couldn’t log you in.  However, with the ping, it will try to ping the host first and if they ping is unresponsive, which only takes a second or two, then it will return that the host is unavailable.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The script will also add the host to your known_hosts file.  The known_hosts file is a list of machines that your computer trusts.  If it hasn’t seen the host, or the host signature has changed, it normally asks you if you’re sure you want to connect to the host.  The script bypasses this by adding it directly to the known_hosts file.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Lastly the script uses expect shell to spawn an ssh process, wait for a glob then send a value (password or duo response, ect).  I tried sshpass, a utility created to automate ssh logins, but this didn’t work. I also tried setsid, which didn’t work. These might not have worked due to the duo or 2FA, but i didn’t investigate further on this.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Quick Note

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

This script only works on mac at this time.  It also only works on mac with gtimeout downloaded, which can be downloaded through brew, also sqllite3 might be needed to be downloaded through brew.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

<https://github.com/unsupo/SSH-Utility>  


<!-- /wp:paragraph -->