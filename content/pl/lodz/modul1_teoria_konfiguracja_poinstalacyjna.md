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

##### Skąd się biorą logi?

- Zapis bezpośredni (proces np.: Apache lub NGINX pisze do /var/log/xyz.log)
- Mechanizm syslog - kiedyś działał tak:
    - Proces nie zajmuje się zapisywaniem logów samodzielnie, tylko wywołuje funkcję systemową mówiącą: "Szanowny kernelu, zapisz do logów komunikat o treści `XXXXX` z priorytetem `YY` i typem `ZZ`.
    - Demon `syslog-ng`, `rsysylog` (albo jakiś inny `syslog`) odbiera komunikaty z kernela i zapisuje je do włąściwego logu według swojej konfiguracji. Co się dzieje z takimi komunikatami? Zbierane są one na poziomie jądra systemu i demon syslog zbiera komunikaty i w zależności od tego skąd przyszły, jakiego są typu i jaki mają priorytet, i co mówi konfiguracja demona syslog, to one trafiają lub nie trafiają do odpowiedniego logu.
    - ... ale już nie jest tak prosto :( Na scenę wszedł systemd.

##### Logi "systemowe"

- Było:

proces -> kernel -> demon syslog -> pliki/zdalny serwer/...

- Jest:

proces -> kernel -> journald -> `nie zawsze` demon syslog -> ...

Co journald robi ze swoimi logami binarnymi i jak je przejrzeć?

"Storage=" w `/etc/systemd/journald.conf` (i man 5 journald.conf)

|                      | RHEL i pokrewne   | Debian-based                |
|----------------------|-------------------|-----------------------------|
| Uwierzytelnienie     | /var/log/secure   | /var/log/auth.log           |
| Poczta               | /var/log/maillog  | /var/log/mail.{log,err,...} |
| Cron                 | /var/log/cron     | /var/log/syslog             |
| Demony usług         | /var/log/messages | /var/log/syslog             |
| Kernel (diagnostyka) | /var/log/messages | /var/log/kern.log           |

To nie jest kompletna list – nie tylko syslog tworzy logi w /var/log.

Niektóre dystrybucje np.: Debiuan 12, Arch nie instalują domyślnie żadnego demona syslog.


3. **Wprowadzenie do fail2ban.**

Artykuł: [fail2ban](https://sysadmin.info.pl/pl/blog/fail2ban-instalacja-i-konfiguracja/)