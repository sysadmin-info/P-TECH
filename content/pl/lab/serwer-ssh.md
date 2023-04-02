---
title: "Serwer SSH"
description: "Konfiguracja serwera SSH w celu zalogowania się do serwera ze zdalnego komputera."
date: 2023-04-01T14:50:34+02:00
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
categories:
  - 
tags:
  - P-TECH
series:
  -

draft: false
image: images/2023-thumbs/ssh.webp
---

#### OpenSSH : KeyBoard-Intereractive Auth

OpenSSH jest już domyślnie zainstalowany, więc nie ma potrzeby instalowania nowych pakietów. Domyślnie możesz logować się za pomocą KeyBoard-Interactive Authentication, ale zmień niektóre ustawienia dla bezpieczeństwa jak poniżej.

```
linux:~ # vi /etc/ssh/sshd_config
# change (prohibit root login remotely)
PermitRootLogin no
linux:~ # systemctl restart sshd
```

#### Instalacja firewalld

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

#### Konfiguracja klienta SSH 

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

#### Uwierzytelnianie parą kluczy SSH

Skonfiguruj serwer SSH do logowania za pomocą Key-Pair Authentication. Utwórz klucz prywatny dla klienta i klucz publiczny dla serwera, aby to zrobić.

Utwórz Key-Pair dla każdego użytkownika, więc zaloguj się wspólnym użytkownikiem na SSH Server Host i pracuj jak poniżej.

```
# utwórz parę kluczy na kliencie
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

# aby wygenerować passphrase możesz użyć następującego polecenia w osobnym oknie CLI
hexdump -vn16 -e'4/4 "%08X" 1 "\n"' /dev/urandom

# wylistuj parę kluczy
adrian@linux:~> ll ~/.ssh/p-tech*
-rw------- 1 adrian adrian 3.4K Apr  1 16:44 /home/adrian/.ssh/p-tech
-rw-r--r-- 1 adrian adrian  745 Apr  1 16:44 /home/adrian/.ssh/p-tech.pub

# skopiuj klucz publiczny z klienta na serwer
ssh-copy-id -i ~/.ssh/p-tech.pub student@IP-ADDRRESS

# podaj hasło

# zaloguj się z kluczem do serwera
ssh -i ~/.ssh/p-tech student@IP-ADDRRESS

# podaj passphrase
```

#### Automatyzacja

Dodaj poniższe wpisy do pliku .bashrc lub .zshrc znajdującego się w katalogu /home/user. Pierwszy wpis uruchamia agenta ssh, a drugi ładuje do niego Twój klucz prywatny. Jeśli ustawiłeś passphrase na swoim kluczu, agent zapyta o jego wpisanie. Możesz dodać więcej niż jeden klucz. Należy pamiętać, że za każdym razem, gdy Bash lub Zsh uruchomi proces restartu lub rozruchu systemu operacyjnego, w CLI poprosi o podanie passphrase.

```
eval $(ssh-agent -s)
ssh-add ~/.ssh/p-tech
```

#### Zabezpieczanie SSH

Edytuj /etc/ssh/sshd_config

```
sudo vi /etc/ssh/sshd_config

# odkomentuj te linie i zmień na [no]
PasswordAuthentication no
ChallengeResponseAuthentication no

# Dodaj Protocol2
Protocol 2
#      Protocol
#             Określa wersje protokołu, które obsługuje sshd(8).  Możliwe
#             wartości to '1' i '2'.  Wiele wersji musi być rozdzielonych przecinkami.
#             Domyślnie jest to '2'.  Protokół 1 cierpi na szereg
#             słabości kryptograficznych i nie powinien być używany.  Jest on jedynie
#             oferowany w celu wsparcia starszych urządzeń.

# Zrestartuj usługę SSH
sudo systemctl restart sshd
```
