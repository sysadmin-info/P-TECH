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

##### OpenSSH : KeyBoard-Intereractive Auth

OpenSSH is already installed by default, so it's not necessarry to install new packages. You can login with KeyBoard-Intereractive Authentication by default, but change some settings for security like follows.

```
linux:~ # vi /etc/ssh/sshd_config
# change (prohibit root login remotely)
PermitRootLogin no
linux:~ # systemctl restart sshd
```

##### Install firewalld

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

###### Configure SSH Client
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

##### SSH Key-Pair Authentication

Configure SSH server to login with Key-Pair Authentication. Create a private key for client and a public key for server to do it.

Create Key-Pair for each user, so login with a common user on SSH Server Host and work like follows.
