---
title: 'Setting up SSH Keys'
date: 2019-04-26
permalink: /posts/2019/04/blog_post_ssh_keys/
tags:
  - ssh
  - server
  - brito lab
---

Are you tired of typing in a password every time you log into the lab's server? Follow this tutorial to set up SSH keys so that you never have to type in your password again while logging in!

What are SSH Keys?
------------------
SSH stands for Secure Shell which is a cryptographic network protocol. What this means is that users can securely perform network services over an unsecured network. SSH keys allow you log into a server more securely through SSH than just using a password. 

The process outlined below will generate two keys, one public and one private. The idea is to place the public key on the server, and then unlock it by connecting to it with a client that has the private key (i.e. your private laptop). When the two keys match up, the system unlocks without the need for a password.

Step One: Create the RSA key pair
---------------------------------
The first step is to create the key pair on your personal laptop. Open a Terminal or (use Putty on Windows). Type and run the following command:

  `$ ssh-keygen -t rsa`
            
            
Step Two: Store the keys and optional passphrase
------------------------------------------------
Once you have entered the Gen Key command, you will get a few more questions:

  `Enter file in which to save the key (/home/fnew/.ssh/id_rsa):`
              
You can press enter here, saving the file to the user home (in this case, my example user is called fnew).

  `Enter passphrase (empty for no passphrase):`
              
You can decide if you want to use a passphrase. It is an added layer of security. If you decide to use one, you will have to type it in every time you use the key pair. 

The entire process looks likes this:

```console
            $ ssh-keygen -t rsa
            Output
            Generating public/private rsa key pair.
            Enter file in which to save the key (/home/fnew/.ssh/id_rsa): 
            Enter passphrase (empty for no passphrase): 
            Enter same passphrase again: 
            Your identification has been saved in /home/fnew/.ssh/id_rsa.
            Your public key has been saved in /home/fnew/.ssh/id_rsa.pub.
            The key fingerprint is:
            4a:dd:0a:c6:35:4e:3f:ed:27:38:8c:74:44:4d:93:67 fnew@a
            The key's randomart image is:
            +--[ RSA 2048]----+
            |          .oo.   |
            |         .  o.E  |
            |        + .  o   |
            |     . = = .     |
            |      = S = .    |
            |     o + = +     |
            |      . o + o .  |
            |           . o   |
            |                 |
            +-----------------+
 ```
 
At this point, the public key is located in /home/fnew/.ssh/id_rsa.pub and the private key is located in /home/fnew/.ssh/id_rsa.

Step Three: Copy the public key
-------------------------------
Now you have to place the public key on the remote server. Make sure to replace my example username and IP address below:

  `$ ssh-copy-id fnew@fake.server.school.edu`
            
_Note_: If you have a Mac you may not have ssh-copy-id on your machine. You can install it using Homebrew:
    
  `$ brew install ssh-copy-id`
             
You may see something like this:
     
   ```console
      The authenticity of host '198.51.100.0 (198.51.100.0)' can't be established.
      RSA key fingerprint is b1:2d:33:67:ce:35:4d:5f:f3:a8:cd:c0:c4:48:86:12.
      Are you sure you want to continue connecting (yes/no)? yes
      Warning: Permanently added '198.51.100.0' (RSA) to the list of known hosts.
      user@198.51.100.0's password: 
   ```
Don't worry about this, it just helps you to make sure you aren't adding extra keys that you weren't expecting. 

You can now log into the server as you normally would, but this time you will not be prompted for a password! 

This tutorial is adapted from [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2).
