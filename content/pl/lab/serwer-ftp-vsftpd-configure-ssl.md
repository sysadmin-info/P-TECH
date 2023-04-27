---
title: "Serwer FTP - Vsftpd - Konfiguracja SSL"
date:  2023-04-27T11:00:00+00:00
description: "Konfiguracja SSL w Vsftpd."
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
image: images/2023-thumbs/vsftpd.webp
---
#### Ćwiczenia do wykonania:
1. Wygeneruj certyfikat.
2. Skonfiguruj serwer do obsługi SSL
3. Skonfiguruj klienta do obsługi SSL
4. Zaloguj się, utwórz katalogi i skopiuj pliki z klienta do serwera.

<script async id="asciicast-580937" src="https://asciinema.org/a/580937.js"></script>

#### Wygeneruj certyfikat

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  {{< highlight Shell "linenos=table" >}}
  cd /etc/ssl/private
  openssl req -x509 -nodes -newkey rsa:2048 -keyout vsftpd.pem -out vsftpd.pem -days 365
Generating a RSA private key
.....................+++++
...................................................................................................................................................+++++
writing new private key to 'vsftpd.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]: country code
State or Province Name (full name) [Some-State]: state
Locality Name (eg, city) []: city
Organization Name (eg, company) [Internet Widgits Pty Ltd]: company
Organizational Unit Name (eg, section) []: department
Common Name (e.g. server FQDN or YOUR name) []: server's FQDN
Email Address []: admin's e-mail
{{< /highlight >}}  
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  {{< highlight Shell "linenos=table" >}}
  cd /etc/ssl/private
  openssl req -x509 -nodes -newkey rsa:2048 -keyout vsftpd.pem -out vsftpd.pem -days 365
Generating a RSA private key
..............+++++
.+++++
writing new private key to 'vsftpd.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]: country code
State or Province Name (full name) [Some-State]: state
Locality Name (eg, city) []: city
Organization Name (eg, company) [Internet Widgits Pty Ltd]: company
Organizational Unit Name (eg, section) []: department
Common Name (e.g. server FQDN or YOUR name) []: server's FQDN
Email Address []: admin's e-mail
{{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  {{< highlight Shell "linenos=table" >}}
  cd /etc/ssl/certs
  openssl req -x509 -nodes -newkey rsa:2048 -keyout vsftpd.pem -out vsftpd.pem -days 365
.+..+.+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.....+.....+.......+...+..+.+...+.....+.......+..+.+...........+...+...+...+.+.........+..+.......+..+.+..+.+......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.....+...........+......+.+..+......+.+...+..+.+........+.+...+......+..+..........+..+.+.....................+......+.....+....+......+..+.+......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
........+.........+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*..+...+......+.........+.+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*...+....+...........+..........+......+.....+...+...+.......+...+...+..+...+....+..+.+..+...+.......+............+.........+..+...+......+....+......+.....+.+..............+...+...+...+....+..+....+.........+...............+........+..........+..+......+.......+.........+......+...............+..+..........+.................+....+...........+.............+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]: country code
State or Province Name (full name) []: state
Locality Name (eg, city) [Default City]: city
Organization Name (eg, company) [Default Company Ltd]: company
Organizational Unit Name (eg, section) []: department
Common Name (eg, your name or your server's hostname) []: server's FQDN
Email Address []: admin's e-mail
{{< /highlight >}}
  {{< /tab >}}
{{< /tabs >}}

#### Skonfiguruj SSL w Vsftpd

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo vim /etc/vsftpd.conf
  ssl_enable=YES
  rsa_cert_file=/etc/ssl/private/vsftpd.pem
  rsa_private_key_file=/etc/ssl/private/vsftpd.pem
  ssl_ciphers=HIGH
  force_local_data_ssl=YES
  force_local_logins_ssl=YES
  #dsa_cert_file=
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo vim /etc/vsftpd.conf
  ssl_enable=YES
  rsa_cert_file=/etc/ssl/private/vsftpd.pem
  rsa_private_key_file=/etc/ssl/private/vsftpd.pem
  ssl_ciphers=HIGH
  force_local_data_ssl=YES
  force_local_logins_ssl=YES
  #dsa_cert_file=
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo vim vim /etc/vsftpd/vsftpd.conf
  ssl_enable=YES
  rsa_cert_file=/etc/ssl/private/vsftpd.pem
  rsa_private_key_file=/etc/ssl/private/vsftpd.pem
  ssl_ciphers=HIGH
  force_local_data_ssl=YES
  force_local_logins_ssl=YES
  #dsa_cert_file=
  ```
  {{< /tab >}}
{{< /tabs >}}

Zrestartuj Vsftpd.

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo systemctl restart vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo systemctl restart vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo systemctl restart vsftpd
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Skonfiguruj klienta lftp

{{< highlight Shell "linenos=table" >}}
vim ~/.lftprc
set ftp:ssl-protect-fxp yes
set ftp:ssl-allow yes
set ftp:ssl-auth TLS
set ftp:ssl-force yes
set ssl:verify-certificate no
set ftp:ssl-protect-data yes
set ftp:ssl-protect-list yes
{{< /highlight >}}

#### Zaloguj się za pomocą klienta lftp

{{< highlight Shell "linenos=table" >}}
lftp ftp1@10.10.0.111
Password:
lftp ftp1@10.10.0.111:~> ls
-rw-------    1 1001     100            14 Apr 27 11:00 file-ssl
-rw-------    1 1001     100             0 Apr 27 11:02 some-file
drwx------    1 1001     100            26 Apr 27 11:00 test-dir
{{< /highlight >}}
