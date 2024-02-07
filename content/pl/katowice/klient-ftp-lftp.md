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

#### Obsługa klienta lfpt - podstawowe polecenia

```
# pokaż bieżący katalog na serwerze FTP
lftp ftp1@10.10.0.2:~> pwd
ftp://ftp1@10.10.0.2

# pokaż bieżący katalog na lokalnym serwerze
lftp ftp1@10.10.0.2:~> !pwd
/home/redhat

# pokaż pliki w bieżącym katalogu na serwerze FTP
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html
-rw-r--r--    1 1000     1000          399 Dec 20 16:32 test.py

# pokaż pliki w bieżącym katalogu na lokalnym serwerze
lftp ftp1@10.10.0.2:~> !ls -l
total 12
-rw-rw-r-- 1 redhat redhat 10 Dec 20 14:30 redhat.txt
-rw-rw-r-- 1 redhat redhat 10 Dec 20 14:59 test2.txt
-rw-rw-r-- 1 redhat redhat 10 Dec 20 14:59 test.txt

# Zmień katalog
lftp ftp1@10.10.0.2:~> cd public_html
lftp ftp1@10.10.0.2:~/public_html> pwd
ftp://ftp1@10.10.0.2/%2Fhome/ftp1/public_html

# prześlik plik na serwer 
# "-a" oznacza tryb ascii ( domyślnym trybem jest binarny)
lftp ftp1@10.10.0.2:~> put -a redhat.txt
22 bytes transferred
Total 2 files transferred
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html
-rw-r--r--    1 1000     1000           10 Dec 20 17:01 redhat.txt
-rw-r--r--    1 1000     1000          399 Dec 20 16:32 test.py
-rw-r--r--    1 1000     1000           10 Dec 20 17:01 test.txt

# prześlij kilka plików na serwer FTP
lftp ftp1@10.10.0.2:~> mput -a test.txt test2.txt
22 bytes transferred
Total 2 files transferred
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html
-rw-r--r--    1 1000     1000          399 Dec 20 16:32 test.py
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test.txt
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test2.txt

# pobierz plik z serwera ftp do lokalnego systemu plików
# "-a" oznacza tryb ascii ( domyślnym trybem jest binarny)
lftp ftp1@10.10.0.2:~> get -a test.py
416 bytes transferred

# pobierz kilka plików z serwera FTP do lokalnego systemu plików
lftp ftp1@10.10.0.2:~> mget -a test.txt test2.txt
20 bytes transferred
Total 2 files transferred

# uwórz katalog w bieżacym katalogu na serwerze FTP
lftp ftp1@10.10.0.2:~> mkdir testdir
mkdir ok, `testdir' created
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html
-rw-r--r--    1 1000     1000          399 Dec 20 16:32 test.py
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test.txt
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test2.txt
drwxr-xr-x    2 1000     1000            6 Dec 20 17:16 testdir
226 Directory send OK.

# usuń katalog w bieżącym katalogu na serwerze FTP
lftp ftp1@10.10.0.2:~> rmdir testdir
rmdir ok, `testdir' removed
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html
-rw-r--r--    1 1000     1000          399 Dec 20 16:32 test.py
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test.txt
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test2.txt

# usuń plik na serwerze FTP
lftp ftp1@10.10.0.2:~> rm test2.txt
rm ok, `test2.txt' removed
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html
-rw-r--r--    1 1000     1000          399 Dec 20 16:32 test.py
-rw-r--r--    1 1000     1000           10 Dec 20 17:06 test.txt

# usuń niektóre pliki na serwerze FTP
lftp ftp1@10.10.0.2:~> mrm redhat.txt test.txt
rm ok, 2 files removed
lftp ftp1@10.10.0.2:~> ls
drwxr-xr-x    2 1000     1000           23 Dec 19 01:33 public_html

# wykonaj polecenia za pomocą "![command]"
lftp ftp1@10.10.0.2:~> !cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
...
...
ftp1:x:1001:1001::/home/ftp1:/bin/bash

# rozłącz się
lftp ftp1@10.10.0.2:~> quit
221 Goodbye.
```
