---
title: "Klient FTP - lftp"
date:  2023-04-26T13:00:00+00:00
description: "Zainstaluj klienta ltpd, aby móc połączyć się z serwerem vsftpd"
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
1. Zainstaluj lftp.
2. Połącz się z serwerem vsftpd
3. Stwórz katalog i skopiuj do niego dowolny plik ze swojego komputera, z którego łączysz się do serwera vsftpd.

#### Zainstaluj lftp

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować lftp wpisz:
  ```
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj lftp
  sudo zypper -n in lftp
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować lftp wpisz:
  ```
  # odśwież repozytoria
  sudo apt update
  # zainstaluj lftp
  sudo apt -y install lftp
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować lftp wpisz:
  ```
  # zainstaluj lftp
  sudo yum install lftp -y
  or
  sudo dnf install lftp -y
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Jak działa lftp

LFTP obsługuje zarówno FTP z włączonym SSL, jak i bez niego. Domyślnie próbuje łączyć się za pomocą SSL.

Można to obejść na dwa sposoby. Na serwerze vsftpd włączyć obsługę trybu pasywnego FTP, co zostało opisane w artykule na stemat konfiguracji vsftpd, lub też połączyć się w następujący sposób:

```
lftp -e "set ftp:ssl-allow off;" -u username adres_IP_serwera_lub_hostname
```

Można też edytować plik lftp.conf 

```
sudo vim /etc/lftp.conf
```

i dopisać do niego dyrektywę:

```
set ftp:ssl-allow false
```

Pamiętaj, aby logować się przy pomocy użytkownika, który został utworzony na serwerze FTP.

##### Co to jest tryb pasywny/aktywny podczas połączenia przez FTP oraz jakie problemy mogą wystąpić?

Więcej informacji znajdziesz tutaj:
* [Tryb pasywny i aktywny](https://panel.kylos.pl/knowledgebase/239/Co-to-jest-tryb-pasywnyoraktywny-podczas-polaczenia-przez-FTP-oraz-jakie-problemy-moga-wystapic.html)
* [Jaka jest różnica między aktywnym a pasywnym trybem ftp](https://hostmark.pl/knowledgebase/142/Jaka-jest-ronica-midzy-aktywnym-a-pasywnym-trybem-ftp.html)
