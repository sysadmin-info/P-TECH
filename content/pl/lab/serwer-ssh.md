---
title: "Serwer SSH"
description: "Konfiguracja serwera SSH w celu zalogowania się do serwera ze zdalnego komputera."
date: 2023-04-01T14:50:34+02:00
hideToc: false
enableToc: true
enableTocContent: false
author: sysadmin
authorEmoji: 🐧
pinned: false
categories:
  - 
tags:
  - P-TECH
series:
  -

draft: false
image: images/2023-thumbs/linux-cli.webp
---

##### OpenSSH : KeyBoard-Intereractive Auth

OpenSSH jest już domyślnie zainstalowany, więc nie ma potrzeby instalowania nowych pakietów. Domyślnie możesz logować się za pomocą KeyBoard-Interactive Authentication, ale zmień niektóre ustawienia dla bezpieczeństwa jak poniżej.

```
linux:~ # vi /etc/ssh/sshd_config
# change (prohibit root login remotely)
PermitRootLogin no
linux:~ # systemctl restart sshd
```

##### Instalacja firewalld

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować firewalld wpisz:
  ```
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj firewalld
  sudo zypper -n in firewalld
  # włącz firewalld podczas boot-owania
  sudo systemctl enable firewalld
  # wystartuj firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować firewalld wpisz:
  ```
  # odśwież repozytoria
  sudo apt update
  # zainstaluj firewalld
  sudo apt -y install firewalld
  # włącz firewalld podczas boot-owania
  sudo systemctl enable firewalld
  # wystartuj firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować firewalld wpisz:
  ```
  sudo yum install firewalld -y
  lub
  sudo dnf install firewalld -y
  # włącz firewalld podczas boot-owania
  sudo systemctl enable firewalld
  # wystartuj firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
{{< /tabs >}}

Domyślnie firewalld po instalacji ma zaimplementowaną usługę SSH jako dozwoloną. Jeśli nie, zawsze możesz zezwolić na usługę SSH.

```
linux:~ # firewall-cmd --add-service=ssh --permanent
success
linux:~ # firewall-cmd --reload
success
```

###### Konfiguracja klienta SSH 

Połącz się z serwerem SSH za pomocą zwykłego użytkownika.

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

##### Uwierzytelnianie parą kluczy SSH

Skonfiguruj serwer SSH do logowania za pomocą Key-Pair Authentication. Utwórz klucz prywatny dla klienta i klucz publiczny dla serwera, aby to zrobić.

Utwórz Key-Pair dla każdego użytkownika, więc zaloguj się wspólnym użytkownikiem na SSH Server Host i pracuj jak poniżej.
