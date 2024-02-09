---
title: "Moduł 2 - Zaawansowane zarządzanie systemem i dokumentacja techniczna  - teoria"
date:  2024-02-08T14:30:00+00:00
description: "Moduł 2 - Zaawansowane zarządzanie systemem i dokumentacja techniczna  - teoria"
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
- Zaawansowane zarządzanie systemem i dokumentacja techniczna 
image: images/2024-thumbs/zarzadzanie-systemem.webp
---
## Część Teoretyczna
### Moduł 2: Zaawansowane zarządzanie systemem i dokumentacja techniczna - teoria
#### Czas Trwania: 15 minut

### 1. **Analiza oprogramowania w GNU/Linux**

Sporządzanie wykazu zainstalowanego oprogramowania w systemie jako dobra praktyka administratora. Aby sporządzić wykaz zainstalowanego oprogramowania w systemie Linux, uczniowie mogą użyć kilku narzędzi dostępnych w większości dystrybucji. Oto niektóre z nich:

- dpkg - na dystrybucjach opartych na Debianie (takich jak Ubuntu):
Komenda: `dpkg -l`
Ta komenda wyświetli listę wszystkich zainstalowanych pakietów w systemie.

- apt - również na dystrybucjach opartych na Debianie:
Komenda: `apt list --installed`
Podobnie jak `dpkg -l`, ale może dostarczać dodatkowych informacji i jest często bardziej przyjazna dla użytkownika.

- rpm - na dystrybucjach opartych na RPM (takich jak Fedora, CentOS):
Komenda: `rpm -qa`
Wyświetla listę wszystkich zainstalowanych pakietów RPM.

- yum - starsze wersje dystrybucji opartych na RPM:
Komenda: `yum list installed`
Ta komenda wyświetli zainstalowane pakiety zarządzane przez yum.

- dnf - nowsze wersje dystrybucji opartych na RPM (np. Fedora):
Komenda: `dnf list installed`
Podobnie jak `yum`, ale dla nowszego menedżera pakietów.

- zypper - na dystrybucjach openSUSE:
Komenda: `zypper se --installed-only`
Wyświetla tylko zainstalowane pakiety.

- pacman - na dystrybucjach Arch Linux:
Komenda: `pacman -Q`
Lista zainstalowanych pakietów w systemie Arch.

- eopkg - na dystrybucjach Solus:
Komenda: `eopkg list-installed`
Wyświetla zainstalowane pakiety w systemie Solus.

- flatpak - dla aplikacji zainstalowanych jako Flatpaks:
Komenda: `flatpak list`
Wyświetla listę zainstalowanych aplikacji Flatpak.

- snap - dla aplikacji zainstalowanych jako Snaps:
Komenda: `snap list`
Pokazuje zainstalowane pakiety snap.

Po uzyskaniu listy, uczniowie można przekierować wynik do pliku tekstowego za pomocą przekierowania wyjścia, np. `dpkg -l > zainstalowane-pakiety.txt`, aby stworzyć dokumentację zainstalowanego oprogramowania. Jest to przydatna praktyka administratora, która pozwala na szybkie zorientowanie się w zainstalowanym oprogramowaniu i może służyć jako punkt odniesienia w przypadku przywracania systemu lub rozwiązywania problemów.

Analiza stanu systemu komputerowego za pomocą dostępnych narzędzi w Linux i sporządzanie raportu zawierającego spis urządzeń wraz z ich specyfikacją.

Dodatkowo:

[Pomiar układu wejścia/wyjścia](https://sysadmin.info.pl/pl/blog/pomiar-ukladu-wejscia-wyjscia/)
[Monitorowanie wykorzystania zasobów systemu Linux](https://sysadmin.info.pl/pl/blog/monitorowanie-wykorzystania-zasobow-systemu-linux/)


### 2. **Zaawansowane zarządzanie systemem i dokumentacja techniczna**

##### Praktyczne ćwiczenia z monitorowania stanu systemu.

Monitorowanie zasobów systemowych przy użyciu `top`, `htop` (jeśli dostępne) oraz `dmesg`.

* Jakie są różne rodzaje zasobów systemowych?

Wyróżniamy kilka głównych typów zasobów systemowych:

- Procesor (CPU): Wykonuje instrukcje programów.
- Pamięć (RAM): Przechowuje dane i kod programów podczas ich wykonywania.
- Pamięć masowa: Przechowuje dane trwale, nawet po wyłączeniu komputera.
- Sieć: Umożliwia komunikację z innymi komputerami i urządzeniami.
- Wejście/wyjście (I/O): Umożliwia interakcję z użytkownikiem i peryferiami, takimi jak klawiatura, mysz, monitor,

* Jakie narzędzia służą do monitorowania zasobów systemowych?

Istnieje wiele narzędzi do monitorowania zasobów systemowych, m.in.:

- top: Wyświetla listę procesów wraz z informacjami o ich zużyciu CPU, pamięci RAM i innych zasobów.
- htop: Bardziej graficzna wersja narzędzia top.
- dmesg: Wyświetla wiadomości kernela, w tym informacje o błędach i ostrzeżeniach.
- sar: Generuje raporty o wydajności systemu.
- vmstat: Wyświetla statystyki dotyczące pamięci wirtualnej.
- iostat: Wyświetla statystyki dotyczące operacji wejścia/wyjścia.

* Jakie są najczęstsze problemy z wydajnością systemu?

- Wysokie zużycie CPU: Może być spowodowane przez jeden lub wiele procesów, które zużywają zbyt dużo czasu procesora.
- Niski poziom pamięci RAM: Może powodować spowolnienie działania systemu i zacinanie się aplikacji.
- Problemy z pamięcią masową: Mogą obejmować błędy dysku twardego, fragmentację danych lub niewystarczającą ilość wolnego miejsca.
- Problemy z siecią: Mogą obejmować niską przepustowość, problemy z połączeniem lub błędy konfiguracji.

* Jakie są rodzaje wiadomości kernela?

Wiadomości kernela można podzielić na kilka kategorii:

- Informacyjne: Informują o zdarzeniach w systemie, takich jak uruchomienie sterownika urządzenia.
- Ostrzeżenia: Informują o potencjalnych problemach, które mogą nie wymagać natychmiastowej interwencji.
- Błędy: Informują o problemach, które uniemożliwiają prawidłowe działanie systemu.
- Krytyczne błędy: Informują o poważnych problemach, które mogą spowodować awarię systemu.

##### Wprowadzenie do tworzenia dokumentacji technicznej: praktyczne zastosowanie narzędzi do dokumentacji.

1. Tworzenie dokumentacji technicznej na przykładzie Confluence.
2. Instalacja Confluence (pokaz z mojej strony).
3. Utworzenie prostego dokumentu. 
4. Uczniowie utworzą dokumentację w dowolnym edytorze tekstu na swoim komputerze. Zadanie do wykonania jest opisane w części praktycznej.

