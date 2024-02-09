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
image: images/2024-thumbs/konfiguracja-linux.webp
---
## Część Teoretyczna
### Moduł 1: Konfiguracja poinstalacyjna - teoria
#### Czas Trwania: 15 minut

1. **Konfiguracja serwera SSH: instalacja, generowanie kluczy RSA.**
Artykuł: [serwer SSH](https://sysadmin.info.pl/pl/blog/serwer-ssh/)

2. **Wprowadzenie do bezpieczeństwa systemu: przeglądanie dzienników systemowych.**

Przeglądanie dzienników systemowych w Linuxie jest kluczowym elementem zarządzania systemem i diagnozowania problemów. Dzienniki te zawierają informacje o działaniu systemu, aplikacji i usług systemowych, oferując wgląd w błędy, ostrzeżenia i inne zdarzenia systemowe. Główne narzędzia do przeglądania dzienników to `journalctl` dla systemów używających systemd oraz tradycyjne pliki dzienników w `/var/log`, takie jak `/var/log/syslog` czy `/var/log/messages`. Umożliwiają one monitorowanie systemu w czasie rzeczywistym, analizę przyczyn problemów oraz planowanie działań prewencyjnych, co jest niezbędne dla utrzymania zdrowia i stabilności systemu.

Skąd się biorą logi?

- Zapis bezpośredni (proces lub usługa pisze do /var/log/xyz.log)
- Mechanizm syslog - kiedyś działał tak:
    - Proces: "Szanowny kernelu, zapisz do logów komunikat o treśi `XXXXX` z priorytetem `YY` i typem `ZZ`.
    - Demon `syslog-ng`, `rsysylog` (albo jakiś inny `syslog`) odbiera komunikaty z kernela i zapisuje je do włąściwego logu według swojej konfiguracji.
    - ... ale już nie jest tak prosto :(

3. **Wprowadzenie do fail2ban.**

Artykuł: [fail2ban](https://sysadmin.info.pl/pl/blog/fail2ban-instalacja-i-konfiguracja/)