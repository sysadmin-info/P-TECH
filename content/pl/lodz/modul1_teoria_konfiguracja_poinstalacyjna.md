---
title: "Moduł 1 - Konfiguracja poinstalacyjna - teoria"
date:  2024-02-07T15:00:00+00:00
description: "Moduł 1 - Konfiguracja poinstalacyjna - teoria"
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
asciinema: true
tags:
- Linux
series:
- Łódź
categories:
- konfiguracja poinstalacyjna
image: images/2024-thumbs/podstawy_pracy_w_systemie_linux.webp
---
## Część Teoretyczna
### Moduł 1: Konfiguracja poinstalacyjna - teoria
#### Czas Trwania: 15 minut

1. Konfiguracja serwera SSH: instalacja, generowanie kluczy RSA.
Artykuł: [serwer SSH](https://sysadmin.info.pl/pl/blog/serwer-ssh/)

2. Wprowadzenie do bezpieczeństwa systemu: przeglądanie dzienników systemowych, wprowadzenie do fail2ban.

##### Przeglądanie dzienników systemowych

Przeglądanie dzienników systemowych w Linuxie jest kluczowym elementem zarządzania systemem i diagnozowania problemów. Dzienniki te zawierają informacje o działaniu systemu, aplikacji i usług systemowych, oferując wgląd w błędy, ostrzeżenia i inne zdarzenia systemowe. Główne narzędzia do przeglądania dzienników to `journalctl` dla systemów używających systemd oraz tradycyjne pliki dzienników w `/var/log`, takie jak `/var/log/syslog` czy `/var/log/messages`. Umożliwiają one monitorowanie systemu w czasie rzeczywistym, analizę przyczyn problemów oraz planowanie działań prewencyjnych, co jest niezbędne dla utrzymania zdrowia i stabilności systemu.

3. Fail2ban
Artykuł: [fail2ban](https://sysadmin.info.pl/pl/blog/fail2ban-instalacja-i-konfiguracja/)