---
title: "Moduł 2 - Wprowadzenie do LVM - zadania"
date:  2024-02-09T09:40:00+00:00
description: "Moduł 2 - Wprowadzenie do LVM - zadania"
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
- Wprowadzenie do LVM
image: images/2024-thumbs/lvm.webp
---
## Część Praktyczna
### Moduł 2: Wprowadzenie do LVM - zadania
#### Czas Trwania: 10 minut


#### 1. **Praca z LVM**

##### Praktyczne ćwiczenia z LVM

- **Ćwiczenie:** Stworzenie woluminu logicznego przy użyciu LVM.
  1. Inicjalizacja dwóch dysków (lub partycji) jako fizycznych woluminów LVM.
  2. Utworzenie grupy woluminów (VG) z tych fizycznych woluminów.
  3. Utworzenie woluminu logicznego (LV) o rozmiarze 500MB w tej grupie woluminów.
  4. Sformatowanie woluminu logicznego systemem plików ext4.
  5. Zamontowanie LV i utworzenie na nim pliku tekstowego z kilkoma linijkami tekstu.

 ##### Zadania z LVM (10 minut)

**Cel:** Naucz się używać LVM do zarządzania wolumenami logicznymi.
**Czas:** 10 minut
**Wymagania:**
* Komputer z systemem Linux
* Dwa dyski lub partycje
* Dostęp do terminala


**Ćwiczenie:**
1. Uruchom terminal.
2. Zainstaluj pakiet `lvm2`, jeśli nie jest jeszcze zainstalowany.
```bash
sudo apt install lvm2
```
3. Sprawdź listę dostępnych dysków za pomocą polecenia `fdisk -l`.
4. Wybierz dwa dyski, które chcesz użyć jako fizyczne woluminy LVM. Zapamiętaj ich nazwy (np. `/dev/sdb` i `/dev/sdc`).


**Inicjalizacja fizycznych woluminów:**
5. Uruchom polecenie `pvcreate` dla każdego z wybranych dysków:
```bash
pvcreate /dev/sdb
pvcreate /dev/sdc
```


**Utworzenie grupy woluminów:**
6. Uruchom polecenie `vgcreate` aby utworzyć grupę woluminów o nazwie "vg0" z dwóch fizycznych woluminów:
```bash
vgcreate vg0 /dev/sdb /dev/sdc
```


**Utworzenie woluminu logicznego:**
7. Uruchom polecenie `lvcreate` aby utworzyć wolumin logiczny o nazwie "lv0" o rozmiarze 500MB w grupie woluminów "vg0":
```bash
lvcreate -n lv0 -L 500M vg0
```


**Formatowanie i montowanie woluminu logicznego:**
8. Sformatuj wolumin logiczny systemem plików ext4:
```bash
mkfs.ext4 /dev/vg0/lv0
```
9. Zamontuj wolumin logiczny w katalogu `/mnt`:
```bash
mount /dev/vg0/lv0 /mnt
```


**Użycie woluminu logicznego:**
10. Utwórz plik tekstowy o nazwie `test.txt` w katalogu `/mnt` i wpisz w nim kilka linijek tekstu.
11. Sprawdź zawartość pliku `test.txt`:
```bash
cat /mnt/test.txt
```


**Po zakończeniu ćwiczenia:**
12. Odmontuj wolumin logiczny:
```bash
umount /mnt
```
13. Usuń wolumin logiczny:
```bash
lvremove /dev/vg0/lv0
```
14. Usuń grupę woluminów:
```bash
vgremove vg0
```


**Uwaga:**
* Należy zachować ostrożność podczas korzystania z LVM. Usunięcie woluminu logicznego może spowodować utratę danych.
* Przed rozpoczęciem ćwiczenia upewnij się, że masz kopię zapasową wszystkich ważnych danych.


**Pytania do dyskusji:**
* Jakie są zalety korzystania z LVM?
* Jakie są różne typy woluminów logicznych?
* Jakie polecenia służą do zarządzania wolumenami logicznymi?


**Zadania rozszerzające:**
* Utwórz wolumin logiczny z systemem plików NTFS.
* Utwórz raid z dwóch fizycznych woluminów i użyj go jako woluminu logicznego.
* Użyj LVM do rozszerzenia istniejącego woluminu logicznego.