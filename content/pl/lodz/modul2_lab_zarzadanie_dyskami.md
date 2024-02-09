---
title: "Moduł 2 - Zarządzania dyskami - zadania"
date:  2024-02-09T09:30:00+00:00
description: "Moduł 2 - Zarządzania dyskami - zadania"
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
- Zarządzania dyskami
image: images/2024-thumbs/zarzadzanie-dyskami.webp
---
## Część Praktyczna
### Moduł 2: Zarządzania dyskami - zadania
#### Czas Trwania: 10 minut
#### 1. **Demonstracja partycjonowania dysku**
- **Ćwiczenie:** Użyj narzędzia `fdisk` lub `gparted` (w zależności od dostępności środowiska graficznego) do stworzenia nowej partycji na podłączonym dysku zewnętrznym lub wirtualnym dysku. Zadaniem jest utworzenie nowej partycji o rozmiarze 1GB.
##### Zadania z zarządzania dyskami
**Cel:** Naucz się partycjonować dysk za pomocą narzędzi `fdisk` lub `gparted`.
**Czas:** 10 minut
**Wymagania:**
* Komputer z systemem Linux
* Podłączony dysk zewnętrzny lub wirtualny dysk
* Dostęp do terminala
**Ćwiczenie:**
1. Uruchom terminal.
2. Sprawdź listę podłączonych dysków za pomocą polecenia `lsblk`.
3. Wybierz dysk, na którym chcesz utworzyć nową partycję. Zapamiętaj jego nazwę (np. `/dev/sdb`).
4. Uruchom narzędzie `fdisk` lub `gparted`.
**Opcja 1: Użycie narzędzia `fdisk`**
1. Wpisz polecenie `fdisk /dev/sdb`, gdzie `/dev/sdb` to nazwa wybranego dysku.
2. Wpisz `n` aby utworzyć nową partycję.
3. Wybierz typ partycji:
    * `p` - partycja podstawowa
    * `e` - partycja rozszerzona
4. Wpisz rozmiar partycji w megabajtach (np. `1000M` dla partycji 1GB).
5. Wpisz `w` aby zapisać zmiany i wyjść z programu `fdisk`.
**Opcja 2: Użycie narzędzia `gparted`**
1. Wpisz polecenie `gparted /dev/sdb`, gdzie `/dev/sdb` to nazwa wybranego dysku.
2. Kliknij prawym przyciskiem myszy na wolnym miejscu na dysku i wybierz "Nowa".
3. Wprowadź rozmiar partycji w megabajtach (np. `1000`) i wybierz system plików (np. `ext4`).
4. Kliknij "Dodaj".
5. Kliknij "Zastosuj" aby zapisać zmiany.
**Po zakończeniu ćwiczenia:**
* Sprawdź listę partycji na dysku za pomocą polecenia `lsblk`.
* Sformatuj nową partycję za pomocą narzędzia `mkfs`.
* Zamontuj nową partycję.
**Dodatkowe informacje:**
* Dokumentacja narzędzia `fdisk`: [https://man7.org/linux/man-pages/man8/fdisk.8.html](https://man7.org/linux/man-pages/man8/fdisk.8.html)
* Dokumentacja narzędzia `gparted`: [https://gparted.org/documentation.php](https://gparted.org/documentation.php)
**Uwaga:**
* Należy zachować ostrożność podczas partycjonowania dysku. Usunięcie partycji może spowodować utratę danych.
* Przed rozpoczęciem ćwiczenia upewnij się, że masz kopię zapasową wszystkich ważnych danych.
**Pytania do dyskusji:**
* Jakie są różne typy partycji?
* Jaki system plików wybrać dla danej partycji?
* Jakie są zalety i wady korzystania z narzędzi graficznych do partycjonowania dysków?
**Zadania rozszerzające:**
* Utwórz partycję z systemem plików NTFS.
* Utwórz partycję rozszerzoną i umieść na niej kilka partycji logicznych.
* Zaszyfruj partycję za pomocą narzędzia `cryptsetup`.