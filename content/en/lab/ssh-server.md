---
title: "SSH server"
date:  2023-04-01T15:00:00+00:00
description: "Configure SSH Server to login to a server from remote computer."
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
tags:
- P-TECH
series:
-
categories:
- 
image: images/2023-thumbs/linux-cli.webp
---

#### OpenSSH : KeyBoard-Intereractive Auth

OpenSSH is already installed by default, so it's not necessarry to install new packages. You can login with KeyBoard-Intereractive Authentication by default, but change some settings for security like follows.

```
linux:~ # vi /etc/ssh/sshd_config
# change (prohibit root login remotely)
PermitRootLogin no
linux:~ # systemctl restart sshd
```

#### Install firewalld

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  To install firewalld type:
  ```
  # refresh repositories
  sudo zypper ref
  # install firewalld
  sudo zypper -n in firewalld
  # enable firewalld on boot
  sudo systemctl enable firewalld
  # start the firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  To install firewalld type:
  ```
  # refresh repositories
  sudo apt update
  # install firewalld
  sudo apt -y install firewalld
  # enable firewalld on boot
  sudo systemctl enable firewalld
  # start the firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  To install firewalld type:
  ```
  sudo yum install firewalld -y
  or
  sudo dnf install firewalld -y
  # enable firewalld on boot
  sudo systemctl enable firewalld
  # start the firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
{{< /tabs >}}

By default the firewalld after installation has SSH service implemented as allowed. If not, you can always allow SSH service.

```
linux:~ # firewall-cmd --add-service=ssh --permanent
success
linux:~ # firewall-cmd --reload
success
```

#### Configure SSH Client
Connect to SSH server with a common user.

```
# ssh [login_user@hostname_or_IP_address]
adrian@client:~> ssh adrian@example.com
The authenticity of host 'example.com (10.0.0.50)' can't be established.
ECDSA key fingerprint is SHA256:h0QhlXgCZ860UjM8sAjY6Wmrr2EqSIY5UADBi0wAFV4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'example.com,10.0.0.50' (ECDSA) to the list of known hosts.
Password:          # login user's password
adrian@example.com:~>    # just logined
```

#### SSH Key-Pair Authentication

Configure SSH server to login with Key-Pair Authentication. Create a private key for client and a public key for server to do it.

Create Key-Pair for each user, so login with a common user on SSH Server Host and work like follows.

```
# create key-pair on a client
ssh-keygen -t rsa -b 4096
Generating public/private rsa key pair.
Enter file in which to save the key (/home/adrian/.ssh/id_rsa): /home/adrian/.ssh/p-tech
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/adrian/.ssh/p-tech
Your public key has been saved in /home/adrian/.ssh/p-tech.pub
The key fingerprint is:
SHA256:IPtApVZ/8o6mCY3lKSvcfEtkD6wzHJ0LzKeHFm3qbxs adrian@G02PLXN05963
The key's randomart image is:
+---[RSA 4096]----+
|      o          |
|     + .         |
|    = . o .      |
|   = * o +       |
|    O % S .      |
|   . ^ = o       |
| . o& E + .      |
|  oooOo=         |
|   .o+*o         |
+----[SHA256]-----+

# to generate a passphrase you can use the following command in a separate CLI window
hexdump -vn16 -e'4/4 "%08X" 1 "\n"' /dev/urandom

# list the key-pair
adrian@linux:~> ll ~/.ssh/p-tech*
-rw------- 1 adrian adrian 3.4K Apr  1 16:44 /home/adrian/.ssh/p-tech
-rw-r--r-- 1 adrian adrian  745 Apr  1 16:44 /home/adrian/.ssh/p-tech.pub

# copy the public key from the client to the server
ssh-copy-id -i ~/.ssh/p-tech.pub student@IP-ADDRRESS

# provide a password

# login with the key to the server
ssh -i ~/.ssh/p-tech student@IP-ADDRRESS

# provide a passphrase
```

#### Automation

Add below entries to .bashrc or .zshrc file located in your /home/user directory.
First entry starts ssh agent and a second loads your private key to the agent. If you did set up a passphrase on your key it will ask for it.
You can add more than one key. Bear in mind, that each time the Bash or Zsh starts aftyer a reboot or boot process of the operating system, in CLI it will ask you to provide a passphrase. 

```
eval $(ssh-agent -s)
ssh-add ~/.ssh/p-tech
```

#### Secure SSH

Edit /etc/ssh/sshd_config

```
sudo vi /etc/ssh/sshd_config

# uncomment these lines and change to [no]
PasswordAuthentication no
ChallengeResponseAuthentication no

# Add Protocol2
Protocol 2
#      Protocol
#             Specifies the protocol versions sshd(8) supports.  The possible
#             values are `1' and `2'.  Multiple versions must be comma-
#             separated.  The default is `2'.  Protocol 1 suffers from a number
#             of cryptographic weaknesses and should not be used.  It is only
#             offered to support legacy devices.

# Restart SSH service
sudo systemctl restart sshd
```
