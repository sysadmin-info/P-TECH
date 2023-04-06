---
title: "Serwer Web - Apache2"
date:  2023-04-06T12:00:00+00:00
description: "Zainstaluj Apache2, aby skonfigurować serwer WWW."
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
#### Ćwiczenia do uzupełnienia:
1. Zainstaluj Apache2.
2. Włącz i uruchom Apache2
3. Dodaj port do firewalld
4. Utwórz prostą stronę internetową
5. Sprawdź czy strona wyświetla się poprawnie przy użyciu adresu IP

<script async id="asciicast-575077" src="https://asciinema.org/a/575077.js"></script>

#### Zainstaluj Apache2

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować Apache2 wpisz:
  ```
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj Apache2
  sudo zypper -n in apache2
  # włącz Apache2 przy starcie systemu
  sudo systemctl enable apache2
  # uruchom Apache2
  sudo systemctl start apache2
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować Apache2 wpisz:
  ```
  # odśwież repozytoria
  sudo apt update
  # zainstaluj Apache2
  sudo apt -y install Apache2
  # włącz Apache2 przy starcie systemu
  sudo systemctl enable apache2
  # uruchom Apache2
  sudo systemctl start apache2
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować Apache2 wpisz:
  ```
  # zainstaluj Apache2
  sudo yum install httpd -y
  or
  sudo dnf install httpd -y
  # włącz Apache2 przy starcie systemu
  sudo systemctl enable httpd
  # uruchom Apache2
  sudo systemctl start httpd
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Zezwól na usługę Apache2

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

#### Utwórz prostą stronę internetową

```
echo 'Podstawy Linux - laboratorium' | sudo tee -a /srv/www/htdocs/index.html
```

#### Sprawdź czy strona wyświetla się poprawnie przy użyciu adresu IP

```
curl http://checkip.amazonaws.com
curl http://IP-ADDRESS
```