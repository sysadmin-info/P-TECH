---
title: "Moduł 1 - Podstawy pracy w systemie Linux - teoria"
date:  2024-02-07T14:30:00+00:00
description: "Moduł 1 - Podstawy pracy w systemie Linux - teoria"
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
- Podstawy pracy w systemie Linux
image: images/2024-thumbs/podstawy_pracy_w_systemie_linux.webp
---
## Część Teoretyczna
### Moduł 1: Podstawy pracy w systemie Linux - teoria
#### Czas Trwania: 20 minut

2. **Podstawy pracy w systemie Linux (30 minut):**
   - **Zarządzanie użytkownikami:**
   - **Opis:** 
   Omówienie procesu tworzenia i zarządzania użytkownikami w systemie Linux. Wprowadzenie do pojęć użytkownika, grupy, UID (User ID), GID (Group ID), pliku `/etc/passwd`, `/etc/group`, oraz narzędzi `useradd`, `usermod`, `userdel`.
   - **Zarządzanie plikami i katalogami:**
   - **Opis:** 
     * Wprowadzenie do systemu plików Linux, ścieżek absolutnych i względnych, podstawowych operacji na plikach i katalogach z użyciem `touch`, `mkdir`, `rm`, `cp`, `mv`, `chmod`, `chown`. 
     * Omówienie struktury katalogów w Linux oraz podstawowych uprawnień plików. 

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

- Dodawanie użytkowników, hasła użytkowników, dodawanie grup, chmod: [https://sysadmin.info.pl/pl/page/13/](https://sysadmin.info.pl/pl/page/13/)

Edycja plików:
- vi,vim,nano,emacs,gedit
- chroot/jail: [https://sekurak.pl/chroot-w-praktyce/](https://sekurak.pl/chroot-w-praktyce/)
- ACL i sticky bit: [https://sysadmin.info.pl/pl/blog/uprawnienia-specjalne-i-sticky-bit-w-linux/ ](https://sysadmin.info.pl/pl/blog/uprawnienia-specjalne-i-sticky-bit-w-linux/)

  
  - **Struktura katalogów** – omówienie głównych katalogów w Linux, takich jak `/bin`, `/etc`, `/home`, `/var`, i ich znaczenie.

### Struktura katalogów w Linux

W systemie Linux, struktura katalogów jest zaprojektowana w sposób hierarchiczny, gdzie każdy katalog pełni określoną rolę:

- **`/bin`** zawiera podstawowe programy (binaries) dostępne dla wszystkich użytkowników (np. bash, ls, cp).
- **`/etc`** przechowuje pliki konfiguracyjne systemu i aplikacji.
- **`/home`** zawiera osobiste katalogi użytkowników.
- **`/var`** jest miejscem na zmienne dane systemowe, takie jak logi, bazy danych.
  
Ta struktura upraszcza zarządzanie systemem i organizację plików, pomagając w utrzymaniu porządku i przewidywalności lokalizacji danych.

  - **Uprawnienia plików** – system uprawnień w Linux określa, kto i w jaki sposób może dostępować do plików i katalogów (czytanie, pisanie, wykonanie).

### Uprawnienia plików w Linux

System uprawnień w Linux określa, jakie działania mogą być wykonywane na plikach i katalogach, zdefiniowane dla właściciela, grupy i innych użytkowników:

- **Czytanie (r)** - pozwala na odczytanie zawartości pliku lub listowanie katalogu.
- **Pisanie (w)** - upoważnia do modyfikacji pliku lub dodawania/usuwania plików w katalogu.
- **Wykonywanie (x)** - pozwala na uruchomienie pliku jako programu lub wejście do katalogu.

System ten zapewnia kontrolę dostępu do danych, umożliwiając zarządzanie prywatnością i bezpieczeństwem systemu.

![uprawnienia plików i katalogów](/images/2024/uprawnienia-plikow-i-katalogow.webp "uprawnienia plików i katalogów")
<figcaption>uprawnienia plików i katalogów</figcaption>

#### Uproszczone wyjaśnienie

Wyobraź sobie, że masz skrzynkę, do której różne osoby mają różne klucze. Każdy klucz pozwala robić inne rzeczy: jeden pozwala tylko oglądać to, co jest w środku (czytać), inny pozwala coś dołożyć lub wyjąć (pisać), a jeszcze inny pozwala to zrobić oraz zamieniać zamki (wykonywać).

W Linux, kiedy masz plik, system sprawdza, co możesz z nim zrobić, sprawdzając trzy rodzaje kluczy:
1. Klucz użytkownika – to Twój osobisty klucz.
2. Klucz grupy – to klucz, którym dzielisz się z grupą osób (jak rodzina).
3. Klucz innych – to klucz dla każdego, kto nie ma innego specjalnego klucza.

System patrzy na klucze w tej kolejności i zatrzymuje się, gdy znajdzie pierwszy pasujący. Oznacza to, że nawet jeśli grupa, do której należysz, może coś więcej zrobić z plikiem, jeśli Twój osobisty klucz pozwala na mniej, to właśnie te mniejsze uprawnienia będziesz miał.

Jednak jest specjalna postać, "root" (jak superbohater), który ma uniwersalny klucz, dzięki któremu może robić wszystko z każdym plikiem, bez względu na zamki.

##### Przykład:

```bash
[test@localhost test ]$ id
uid=1000 (test) gid=1000 (test) groups-1000 (test)

[test@localhost test ]$ ls -1 file
-r--rw-rwx 1 test test

[test@localhost test ]$ cat file
Adrian

[test@localhost test ]$ echo ADI > file
bash: file: Permission denied

root@localhost:/tmp/test# id
uid=0(root) gid=0(root) groups-0 (root)

root@localhost:/tmp/test# ls -la file
-r--r-- 1 root root

root@localhost:/tmp/test# cat file
Adrian

root@localhost:/tmp/test# echo ADI > file

root@localhost:/tmp/test# cat file
ADI

root@localhost:/tmp/test# chmod 0000 file

root@localhost:/tmp/test# chown test file

root@localhost:/tmp/test# chgrp test file

root@localhost:/tmp/test# ls -lah file
1 test test
```

W Linux system uprawnień do plików określa, kto i jak może interagować z danym plikiem lub katalogiem. Uprawnienia są podzielone na trzy kategorie:

1. **Uprawnienia dla użytkownika** (owner) - To są uprawnienia dla osoby, która jest właścicielem pliku. Właściciel może mieć uprawnienia do czytania (r), pisania (w) lub wykonywania (x) pliku.
2. **Uprawnienia dla grupy** (group) - Osoby należące do grupy, do której przypisany jest plik, mogą mieć różne uprawnienia. Podobnie jak właściciel, grupa może mieć uprawnienia do czytania, pisania lub wykonywania pliku.
3. **Uprawnienia dla innych** (others) - To są uprawnienia dla wszystkich pozostałych użytkowników, którzy nie są właścicielem ani nie należą do grupy. Również mogą mieć uprawnienia do czytania, pisania lub wykonywania.

Każde z tych uprawnień jest niezależne i nie sumuje się z innymi. Oznacza to, że jeśli użytkownik ma uprawnienie do czytania na poziomie użytkownika, ale grupa, do której należy, ma uprawnienia do czytania i pisania, użytkownik wciąż będzie miał tylko uprawnienie do czytania. System sprawdza uprawnienia od użytkownika do grupy, a potem do innych, i stosuje pierwszy zestaw znalezionych uprawnień.

**Uprawnienia w praktyce:**

W podanym przykładzie, `test` to użytkownik i grupa, a plik ma uprawnienia `-r--rw-rwx`:
- `-r--` dla użytkownika: oznacza, że właściciel może tylko czytać plik.
- `rw-` dla grupy: oznacza, że członkowie grupy mogą czytać i pisać do pliku.
- `rwx` dla innych: oznacza, że wszyscy inni mogą czytać, pisać i wykonywać plik.

Jednak, jako użytkownik `test`, dostajesz tylko uprawnienia do czytania (`-r--`), ponieważ system nie sumuje uprawnień z różnych kategorii. Nawet jeśli grupa ma większe uprawnienia, system stosuje tylko uprawnienia specyficzne dla użytkownika.

**Wyjątek `root`:**

Użytkownik `root` jest wyjątkowy, ponieważ ma uprawnienie `CAP_DAC_OVERRIDE`, co oznacza, że może ignorować zwykłe ograniczenia uprawnień i robić prawie wszystko z każdym plikiem. Dlatego w Twoim przykładzie `root` może zmodyfikować plik, nawet jeśli jego uprawnienia są ustawione na `0000`, co zwykle uniemożliwia wszystkim działania na pliku.

Użytkownik `root` w systemie Linux jest bardzo potężny i ma szereg przywilejów, które pozwalają mu wykonywać operacje, które są zablokowane dla innych użytkowników. `root` jest często nazywany superużytkownikiem lub użytkownikiem administracyjnym, ponieważ ma dostęp do wszystkich plików i procesów w systemie.

**CAP_DAC_OVERRIDE** to jedna z wielu możliwości (capabilities), które może mieć proces w systemie Linux. W kontekście `root` i uprawnień systemu plików:

- **CAP_DAC_OVERRIDE**: Pozwala procesowi na omijanie kontroli dostępu do danych (czyli uprawnień do plików i katalogów). Oznacza to, że użytkownik lub proces z tą zdolnością może czytać, pisać i wykonywać pliki bez względu na ustawione uprawnienia. W praktyce, gdy użytkownik `root` próbuje uzyskać dostęp do pliku, system nie sprawdza typowych uprawnień pliku (czyli rwx), ponieważ `CAP_DAC_OVERRIDE` umożliwia pominięcie tych kontroli.

To przywilej ma znaczące implikacje bezpieczeństwa, ponieważ daje `root` lub innym procesom z tą zdolnością możliwość dostępu do wszystkich plików i katalogów w systemie, niezależnie od ich uprawnień. Dzięki temu `root` może naprawiać problemy, zarządzać systemem i wykonywać administracyjne zadania konserwacji, ale również stwarza ryzyko bezpieczeństwa, jeśli nie jest właściwie zarządzane lub jeśli dostęp do konta `root` zostanie skompromitowany.

W nowoczesnych systemach Linux, koncept zdolności (capabilities) pozwala na bardziej szczegółowe zarządzanie uprawnieniami niż tradycyjny model wszystko albo nic `root`. To znaczy, że poszczególnym procesom można przypisać tylko te zdolności, które są im potrzebne do wykonania swoich zadań, zamiast dawać im pełne uprawnienia `root`. Takie podejście, nazywane zasadą najmniejszych uprawnień, pomaga ograniczyć potencjalne szkody w przypadku eksploatacji luki bezpieczeństwa.

Więcej na temat CAP_DAC_OVERRIDE znajdziesz tu: [https://man7.org/linux/man-pages/man7/capabilities.7.html](https://man7.org/linux/man-pages/man7/capabilities.7.html)


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

### Quiz

[Quiz - Moduł 1 - Podstawy pracy w systemie Linux - teoria](https://play.kahoot.it/v2/?quizId=97eb5d9b-b6f2-4498-a396-bd4fa9710c8f&hostId=ff76223a-8f37-446c-9d65-7189c6fe887c)