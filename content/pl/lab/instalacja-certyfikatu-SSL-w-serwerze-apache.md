---
title: "Instalacja certyfikatu SSL w serwerze Apache"
date:  2023-04-07T11:15:00+00:00
description: "Instalacja certyfikatu SSL w serwerze Apache"
draft: true
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
#### Ćwiczenia do wykonania:
1. Zainstaluj/włącz mod ssl
2. 
3. 

<!--<script async id="asciicast-575108" src="https://asciinema.org/a/575108.js"></script>-->

#### Instalacja Apache'a i aktywacja modułu mod_ssl w systemach linuksowych:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo a2enmod ssl
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo a2enmod ssl
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo yum install mod_ssl
  lub
  sudo dnf install mod_ssl
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Instalacja certyfikatu SSL:

1. Dodaj certyfikat
