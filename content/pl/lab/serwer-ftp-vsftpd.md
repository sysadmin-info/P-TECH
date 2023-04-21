---
title: "Serwer FTP - Vsftpd"
date:  2023-04-21T10:30:00+00:00
description: "Zainstaluj Vsftpd, aby skonfigurować serwer FTP."
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
1. Zainstaluj Vsftpd.
2. Włącz i uruchom Vsftpd
3. Dodaj port do firewalld

#### Zainstaluj Vsftpd

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować Vsftpd wpisz:
  ```
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj Vsftpd
  sudo zypper -n in vsftpd
  # włącz Vsftpd przy starcie systemu
  sudo systemctl enable vsftpd
  # uruchom Vsftpd
  sudo systemctl start vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować Vsftpd wpisz:
  ```
  # odśwież repozytoria
  sudo apt update
  # zainstaluj sftpd
  sudo apt -y install vsftpd
  # włącz Vsftpd przy starcie systemu
  sudo systemctl enable vsftpd
  # uruchom Vsftpd
  sudo systemctl start vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować Vsftpd wpisz:
  ```
  # zainstaluj Vsftpd
  sudo yum install vsftpd -y
  or
  sudo dnf install vsftpd -y
  # włącz Vsftpd przy starcie systemu
  sudo systemctl enable vsftpd
  # uruchom Vsftpd
  sudo systemctl start vsftpd
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Zezwól na usługę Vsftpd

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  linux:~ # sudo firewall-cmd --add-service=ftp --permanent
  linux:~ # sudo firewall-cmd --add-port=21000-21010/tcp --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo ufw allow 'FTP'
  lub
  sudo ufw allow 'Vsftpd'
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  linux:~ # sudo firewall-cmd --add-service=ftp --permanent
  linux:~ # sudo firewall-cmd --add-port=21000-21010/tcp --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Zmodyfikuj konfigurację Vsftpd dla openSUSE/SLES

```
sudo vim /etc/vsftpd.conf
# line 19: change
write_enable=YES
# line 36: uncomment
ls_recurse_enable=YES
# line 62,63: uncomment ( enable chroot )
chroot_local_user=YES
chroot_list_enable=YES
# line 65: uncomment ( chroot list file )
chroot_list_file=/etc/vsftpd.chroot_list
# line 80: change (no anonymous)
anonymous_enable=NO
# line 171,172: uncomment ( allow ascii mode )
ascii_upload_enable=YES
ascii_download_enable=YES
# line 184: change if need (if listen only IPv4)
listen=YES
# line 189: change if need (if listen only IPv4)
# if YES, listen on both IPv4 and IPv6
listen_ipv6=NO
# line 217: uncomment (turn off seccomp filter)
seccomp_sandbox=NO
# add to the end
# specify root directory if need
# if not specify, users' home directory become FTP home directory
local_root=public_html
# use local time
use_localtime=YES
```

#### Dodaj użytkowników, którym zezwolisz na przejście do ich katalogu domowego

```
sudo vim  /etc/vsftpd.chroot_list
add 
suse
```

#### Jeśli Firewalld jest uruchomiony, zezwól na usługę FTP.

```
sudo vim /etc/vsftpd.conf
# dodaj na końcu pliku
# dodaj porty PASV, aby umożliwić dostęp do FTP za pomocą PASV
pasv_enable=YES
pasv_min_port=21000
pasv_max_port=21010
```

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