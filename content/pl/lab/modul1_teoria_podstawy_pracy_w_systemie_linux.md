---
title: "Podstawy pracy w systemie Linux - teoria"
date:  2024-02-07T15:00:00+00:00
description: "Podstawy pracy w systemie Linux - teoria"
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
asciinema: true
tags:
- Docker
series:
- Docker
categories:
- Docker
image: images/2023-thumbs/docker.webp
---
## Część Teoretyczna
### Moduł 1: Podstawy pracy w systemie Linux
#### Czas Trwania: 30 minut

2. **Podstawy pracy w systemie Linux (30 minut):**
   - **Zarządzanie użytkownikami:**
   - **Opis:** 
   Omówienie procesu tworzenia i zarządzania użytkownikami w systemie Linux. Wprowadzenie do pojęć użytkownika, grupy, UID (User ID), GID (Group ID), pliku `/etc/passwd`, `/etc/group`, oraz narzędzi `useradd`, `usermod`, `userdel`.
   - **Zarządzanie plikami i katalogami:**
   - **Opis:** 
     * Wprowadzenie do systemu plików Linux, ścieżek absolutnych i względnych, podstawowych operacji na plikach i katalogach z użyciem `touch`, `mkdir`, `rm`, `cp`, `mv`, `chmod`, `chown`. 
     * Omówienie struktury katalogów w Linuxie oraz podstawowych uprawnień plików. 

**Zarządzanie użytkownikami:**

- **Opis:** Linux to system wieloużytkownikowy, co oznacza, że na jednym komputerze może pracować wiele osób, każda z własnym kontem użytkownika. Zarządzanie użytkownikami obejmuje tworzenie, modyfikację i usuwanie kont użytkowników oraz grup, a także zarządzanie ich uprawnieniami i dostępem do zasobów systemowych. Kluczowe pojęcia to:
  - **Użytkownik** (ang. user) – osoba lub proces posiadający dostęp do systemu i zasobów.
  - **Grupa** (ang. group) – zestaw użytkowników zgrupowanych w celu łatwiejszego zarządzania uprawnieniami.
  - **UID** (User ID) – unikalny identyfikator każdego użytkownika.
  - **GID** (Group ID) – unikalny identyfikator każdej grupy.
  - **`/etc/passwd`** – plik zawierający informacje o użytkownikach systemu.
  - **`/etc/group`** – plik zawierający informacje o grupach w systemie.
  - **Narzędzia:** `useradd`, `usermod`, `userdel` służą do zarządzania kontami użytkowników.
  
**Zarządzanie plikami i katalogami:**

- **Opis:** System plików Linuxa jest hierarchicznie uporządkowany, co umożliwia efektywne zarządzanie danymi i aplikacjami. Kluczowe operacje na plikach i katalogach to tworzenie, usuwanie, kopiowanie, przenoszenie, zmiana uprawnień dostępu oraz właściciela. Ważne pojęcia i narzędzia to:
  - **Ścieżki absolutne i względne** – określają lokalizację pliku lub katalogu w systemie.
   Te dwa podejścia do definiowania lokalizacji zasobów w systemie plików mają kluczowe znaczenie dla efektywnego nawigowania i zarządzania systemem.

**Ścieżki absolutne:**
- Ścieżka absolutna to pełna ścieżka do pliku lub katalogu, zaczynająca się od katalogu głównego, czyli od `/`. Na przykład `/home/uzytkownik/dokumenty/plik.txt` jest ścieżką absolutną do pliku `plik.txt`.
- Ścieżka absolutna zawsze wskazuje na to samo miejsce w systemie plików, niezależnie od bieżącej lokalizacji użytkownika w strukturze katalogów. Jest to jak podanie pełnego adresu domu na mapie, który jednoznacznie identyfikuje lokalizację.

**Ścieżki względne:**
- Ścieżka względna definiuje lokalizację pliku lub katalogu w odniesieniu do bieżącego katalogu roboczego użytkownika. Na przykład, jeśli bieżącym katalogiem jest `/home/uzytkownik`, to ścieżka względna do pliku `plik.txt` w katalogu `dokumenty` będzie po prostu `dokumenty/plik.txt`.
- Ścieżka względna może różnie wskazywać na lokalizację w zależności od tego, gdzie aktualnie znajduje się użytkownik w systemie plików. Jest to podobne do podawania kierunków dojścia do jakiegoś miejsca, które zmieniają się w zależności od punktu startowego.

**Znaczenie w praktyce:**
Zrozumienie różnicy między ścieżkami absolutnymi a względnymi jest niezbędne dla efektywnego korzystania z wiersza poleceń oraz skryptów shell. Umożliwia to precyzyjne wskazywanie lokalizacji plików i katalogów podczas wykonywania operacji takich jak kopiowanie, przenoszenie, tworzenie czy usuwanie plików. Ścieżki względne są szczególnie użyteczne w skryptach, gdzie operacje na plikach mogą zależeć od bieżącej lokalizacji skryptu lub kiedy chcemy, aby skrypt był bardziej przenośny między różnymi systemami bez konieczności dostosowywania ścieżek absolutnych.

  - **Podstawowe operacje**:
    - `touch` – tworzy pusty plik lub aktualizuje datę dostępu do pliku.
    - `mkdir` – tworzy nowy katalog.
    - `rm` – usuwa pliki lub katalogi.
    - `cp` – kopiuje pliki lub katalogi.
    - `mv` – przenosi lub zmienia nazwy plików lub katalogów.
    - `chmod` – zmienia prawa dostępu do plików lub katalogów.
    - `chown` – zmienia właściciela pliku lub katalogu.
  
  - **Struktura katalogów** – omówienie głównych katalogów w Linuxie, takich jak `/bin`, `/etc`, `/home`, `/var`, i ich znaczenie.

### Struktura katalogów w Linuxie

W systemie Linux, struktura katalogów jest zaprojektowana w sposób hierarchiczny, gdzie każdy katalog pełni określoną rolę:

- **`/bin`** zawiera podstawowe programy (binaries) dostępne dla wszystkich użytkowników (np. bash, ls, cp).
- **`/etc`** przechowuje pliki konfiguracyjne systemu i aplikacji.
- **`/home`** zawiera osobiste katalogi użytkowników.
- **`/var`** jest miejscem na zmienne dane systemowe, takie jak logi, bazy danych.
  
Ta struktura upraszcza zarządzanie systemem i organizację plików, pomagając w utrzymaniu porządku i przewidywalności lokalizacji danych.

  - **Uprawnienia plików** – system uprawnień w Linuxie określa, kto i w jaki sposób może dostępować do plików i katalogów (czytanie, pisanie, wykonanie).

### Uprawnienia plików w Linuxie

System uprawnień w Linuxie określa, jakie działania mogą być wykonywane na plikach i katalogach, zdefiniowane dla właściciela, grupy i innych użytkowników:

- **Czytanie (r)** - pozwala na odczytanie zawartości pliku lub listowanie katalogu.
- **Pisanie (w)** - upoważnia do modyfikacji pliku lub dodawania/usuwania plików w katalogu.
- **Wykonywanie (x)** - pozwala na uruchomienie pliku jako programu lub wejście do katalogu.

System ten zapewnia kontrolę dostępu do danych, umożliwiając zarządzanie prywatnością i bezpieczeństwem systemu.

Obrazek

## Setuid i Setgid - szczegółowe wyjaśnienie

**Setuid** i **setgid** to specjalne flagi uprawnień plików w systemach uniksopodobnych, takich jak Linux. Pozwalają one na uruchamianie plików wykonywalnych z uprawnieniami właściciela lub grupy pliku, a nie z uprawnieniami użytkownika, który uruchamia program.

**Setuid:**

* Umożliwia użytkownikom uruchamianie programów z wyższymi uprawnieniami niż te, które normalnie posiadają.
* Przydatne do zadań, które wymagają dostępu do plików systemowych lub innych zasobów, do których normalni użytkownicy nie mają dostępu.
* Przykłady:
    * `sudo`: pozwala użytkownikom na tymczasowe uruchamianie poleceń z uprawnieniami roota.
    * `passwd`: umożliwia użytkownikom zmianę własnego hasła.
    * `ping`: wysyła i odbiera pakiety ICMP, co wymaga dostępu do interfejsu sieciowego.

**Setgid:**

* Umożliwia użytkownikom tworzenie plików i podkatalogów w katalogu z uprawnieniami grupy, do której należy katalog.
* Przydatne do współpracy w grupach, gdy użytkownicy muszą być w stanie modyfikować pliki należące do grupy.
* Przykłady:
    * Katalog `/tmp`: Użytkownicy mogą tworzyć pliki w tym katalogu, ale tylko root może je usuwać.
    * Katalog `/home/users`: Użytkownicy mogą tworzyć i modyfikować pliki w swoich własnych katalogach domowych.

**Uwaga:**

* Flagi `setuid` i `setgid` mogą być potencjalnie niebezpieczne, jeśli nie są używane ostrożnie.
* Należy je ustawiać tylko na plikach, którym ufasz.
* Użytkownicy, którzy uruchamiają programy z flagami `setuid` lub `setgid`, mogą uzyskać dostęp do plików i zasobów, do których normalnie nie mieliby dostępu.

**Dodatkowe informacje:**

* Strona man: `man 7 setuid`
* Artykuł w Wikipedii: `https://pl.wikipedia.org/wiki/Setuid`
* Poradnik: `https://www.digitalocean.com/community/tutorials/how-to-add-and-remove-setuid-and-setgid-permissions-on-ubuntu-and-centos`

**Przykładowe scenariusze:**

* **Zmiana hasła:** Użytkownik musi mieć możliwość zmiany własnego hasła, ale nie ma dostępu do pliku shadow. Plik `passwd` ma ustawioną flagę `setuid`, co pozwala użytkownikowi na tymczasowe uruchomienie go z uprawnieniami roota i zmianę hasła.
* **Udostępnianie drukarki:** Grupa użytkowników musi mieć możliwość drukowania na drukarce, ale nie ma dostępu do urządzenia. Katalog `/dev/lp0` ma ustawioną flagę `setgid`, co pozwala użytkownikom na tworzenie plików w tym katalogu z uprawnieniami grupy, a tym samym na drukowanie.

**Podsumowując:**

Flagi `setuid` i `setgid` są potężnymi narzędziami, które mogą być używane do ułatwienia zarządzania systemem i współpracy. Należy je jednak używać ostrożnie, aby uniknąć potencjalnych zagrożeń bezpieczeństwa.

Te dwa elementy — struktura katalogów i system uprawnień — są fundamentem organizacji i bezpieczeństwa systemu Linux, umożliwiając efektywne i kontrolowane użytkowanie zasobów przez różnych użytkowników i aplikacje.

### Zakończenie

Ten moduł daje solidne podstawy do zrozumienia, jak system Linux zarządza użytkownikami i jak można manipulować plikami oraz katalogami. To kluczowe umiejętności dla każdego, kto rozpoczyna pracę z Linuxem, niezależnie od tego, czy jest to użytkownik końcowy, programista, czy administrator systemu. Zrozumienie tych podstaw jest fundamentem do dalszej nauki i pracy z Linuxem.