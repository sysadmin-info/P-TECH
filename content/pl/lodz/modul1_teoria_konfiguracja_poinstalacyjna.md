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

Secure Shell (SSH) jest niezastąpionym narzędziem w arsenale każdego specjalisty IT, umożliwiając bezpieczne zarządzanie maszynami zdalnymi poprzez zaszyfrowane połączenia. Umożliwia wykonanie szerokiej gamy zadań, od prostego logowania po zaawansowane operacje przesyłania plików i tunelowania portów. Instalacja serwera SSH zaczyna się od wyboru odpowiedniego pakietu dla dystrybucji Linuxa, jak OpenSSH, dostępnego w większości repozytoriów systemowych.

Kluczowym elementem konfiguracji SSH jest wygenerowanie pary kluczy RSA, co zwiększa bezpieczeństwo poprzez eliminację potrzeby używania haseł do autoryzacji. Wdrażanie kluczy publicznych na serwerach, do których często się łączymy, automatyzuje proces logowania, jednocześnie zwiększając jego bezpieczeństwo. Dalsze zabezpieczenie serwera SSH polega na wyłączeniu logowania hasłem, co jest krytycznym krokiem w ochronie przed atakami siłowymi.

Dobrą praktyką jest również ograniczenie dostępu do serwera SSH tylko dla wybranych użytkowników oraz wyłączenie możliwości logowania się na konto roota bezpośrednio. Można to osiągnąć poprzez edycję pliku konfiguracyjnego `sshd_config`, gdzie określa się, które metody uwierzytelniania są dozwolone, jakie klucze są akceptowane, a także jakie protokoły i algorytmy szyfrowania mają być używane.

Zmiana domyślnego portu, na którym nasłuchuje serwer SSH, może dodatkowo zwiększyć bezpieczeństwo przez zmniejszenie widoczności serwera na typowych portach. To, wraz z ustawieniem ścisłych zasad dotyczących szyfrów, algorytmów wymiany kluczy (KexAlgorithms) i kodów uwierzytelniania wiadomości (MACs), tworzy warstwę obrony przed różnymi rodzajami ataków, w tym przed atakami "man in the middle".

Automatyzacja i zarządzanie sesjami, w tym konfiguracja nieaktywnych interwałów dla klientów oraz zarządzanie kluczami przez `ssh-agent`, to kolejne aspekty, które zasługują na uwagę. Pozwalają one na łatwiejszą i bezpieczniejszą pracę z kluczami prywatnymi, jak również na utrzymanie czystości i porządku w sesjach SSH.

Na koniec, stosowanie się do najlepszych praktyk bezpieczeństwa, jak wyłączenie protokołu 1 na rzecz protokołu 2, jest niezbędne dla zapewnienia najwyższego poziomu ochrony. Wdrażając opisane w ćwiczeniach zalecenia, można skutecznie zabezpieczyć serwer SSH przed nieautoryzowanym dostępem, a tym samym zwiększyć ogólną postawę bezpieczeństwa infrastruktury IT.

2. **Wprowadzenie do bezpieczeństwa systemu: przeglądanie dzienników systemowych.**

Przeglądanie dzienników systemowych w Linux jest kluczowym elementem zarządzania systemem i diagnozowania problemów. Dzienniki te zawierają informacje o działaniu systemu, aplikacji i usług systemowych, oferując wgląd w błędy, ostrzeżenia i inne zdarzenia systemowe. Główne narzędzia do przeglądania dzienników to `journalctl` dla systemów używających systemd oraz tradycyjne pliki dzienników w `/var/log`, takie jak `/var/log/syslog` czy `/var/log/messages`. Umożliwiają one monitorowanie systemu w czasie rzeczywistym, analizę przyczyn problemów oraz planowanie działań prewencyjnych, co jest niezbędne dla utrzymania zdrowia i stabilności systemu.

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

To nie jest kompletna lista – nie tylko syslog tworzy logi w /var/log.

Niektóre dystrybucje np.: Debian 12, Arch nie instalują domyślnie żadnego demona syslog.


3. **Wprowadzenie do fail2ban.**

Fail2Ban jest nieocenionym narzędziem dla administratorów systemów, zapewniającym ochronę przed atakami brute-force i innymi rodzajami prób nieautoryzowanego dostępu do serwerów. Program działa poprzez monitorowanie logów systemowych w poszukiwaniu wzorców nieudanych prób logowania i automatycznie blokuje adresy IP, które te wzorce generują, używając zapory sieciowej.

Instalacja Fail2Ban różni się w zależności od dystrybucji systemu operacyjnego. Na systemach CentOS wymagane jest dodatkowo zainstalowanie repozytorium EPEL, aby uzyskać dostęp do pakietu Fail2Ban, natomiast na systemach Debian/Ubuntu instalacja jest bezpośrednia za pomocą menedżera pakietów apt.

Konfiguracja Fail2Ban rozpoczyna się od skopiowania domyślnego pliku konfiguracyjnego `jail.conf` do `jail.local`, co pozwala na bezpieczną personalizację ustawień bez ryzyka ich nadpisania podczas aktualizacji. Podstawowe parametry konfiguracyjne zawarte w pliku `jail.local` umożliwiają administratorom dostosowanie, jakie adresy IP ignorować (`ignoreip`), określenie czasu bana (`bantime`), czasu poszukiwania (`findtime`) oraz maksymalnej liczby prób przed zbanowaniem (`maxretry`).

Specyficzne dla serwisów konfiguracje, takie jak ochrona SSH, są realizowane przez dodanie plików konfiguracyjnych w katalogu `jail.d`, np. `sshd.local`, gdzie można szczegółowo określić polityki dotyczące specyficznych usług, takich jak SSH.

Fail2Ban jest szczególnie elastyczny dzięki możliwości tworzenia własnych filtrów za pomocą wyrażeń regularnych, co umożliwia ochronę przed specyficznymi zagrożeniami, jak np. atakami na strony WordPress poprzez nieautoryzowane próby logowania.

Uruchomienie i zarządzanie Fail2Ban odbywa się za pomocą systemowego menedżera pakietów i narzędzia `fail2ban-client`, które umożliwia sprawdzanie statusu działania, monitorowanie zbanowanych adresów IP oraz zarządzanie indywidualnymi zbanowanymi adresami.

Dzięki Fail2Ban, administratorzy systemów mogą skutecznie zwiększyć poziom bezpieczeństwa swoich serwerów, dynamicznie reagując na próby nieautoryzowanego dostępu i automatycznie ograniczając potencjalne zagrożenia. Implementacja tego narzędzia jest kluczowym elementem strategii obronnej każdego serwera, zwłaszcza tych narażonych na ataki z Internetu.