---
title: "Web Server - Apache2"
date:  2023-04-06T12:00:00+00:00
description: "Install Apache2 to configure Web Server."
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
asciinema: true
tags:
- P-TECH
series:
-
categories:
- 
image: images/2023-thumbs/apache2.webp
---
#### Exercises to complete:
1. Install Apache2
2. Enable and start Apache2
3. Add a port to firewalld
4. Create a simple website
5. Check does the website display correctly using IP address

<!---<script async id="asciicast-574590" src="https://asciinema.org/a/574590.js"></script>-->

#### Install Apache2

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  To install Apache2 type:
  ```
  # refresh repositories
  sudo zypper ref
  # install Apache2
  sudo zypper -n in apache2
  # enable Apache2 on boot
  sudo systemctl enable apache2
  # start the Apache2
  sudo systemctl start apache2
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  To install apache2 type:
  ```
  # refresh repositories
  sudo apt update
  # install apache2
  sudo apt -y install apache2
  # enable apache2 on boot
  sudo systemctl enable apache2
  # start the apache2
  sudo systemctl start apache2
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  To install apache2 type:
  ```
  sudo yum install httpd -y
  or
  sudo dnf install httpd -y
  # enable apache2 on boot
  sudo systemctl enable httpd
  # start the apache2
  sudo systemctl start httpd
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Allow Apache2 service

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  linux:~ # sudo firewall-cmd --add-service=http --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo ufw allow 'WWW'
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  linux:~ # sudo firewall-cmd --add-service=http --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Create a simple webiste

```
echo 'Linux fundamentals - lab' | sudo tee -a /srv/www/htdocs/index.html
```

#### Check does the website display correctly using IP address

```
curl http://checkip.amazonaws.com
curl http://IP-ADDRESS
```