---
title: "Moduł 2 - Wprowadzenie do LVM - teoria"
date:  2024-02-08T13:30:00+00:00
description: "Moduł 2 - Wprowadzenie do LVM - teoria"
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
## Część Teoretyczna
### Moduł 2: Wprowadzenie do LVM - teoria
#### Czas Trwania: 10 minut

### 2. **Wprowadzenie do LVM: co to jest, podstawowe zastosowania.**

#### Konfiguracja LVM i RAID

`LVM (Logical Volume Manager)` - Menadżer woluminów logicznych jest nową technologią pozwalającą wykorzystać miejsce na kilku napędach jako jeden logiczny wolumin.

Daje to możliwość elastycznego przydzielania dostępnej przestrzeni dyskowej dla aplikacji i użytkowników.

Po stworzeniu logicznych woluminów za pomocą LVM - można (z pewnymi ograniczeniami) zmieniać rozmiar i przenosić logiczne woluminy nawet w czasie ich pracy (mogą być zamontowane i normalnie używane).

Możemy również wykorzystać LVM do zarządzania woluminami logicznymi z nazwami które są sensowne z punktu widzenia użytkownika (np. Marketing, Handel), zamiast fizycznych nazw dysków.

Aby dobrze skonfigurować system plików za pomocą LVM, musimy poznać następujące zagadnienia:
- Jak używać komponentów LVM
- Jak wykorzystać cechy LVM
- Konfiguracja logicznych woluminów za pomocą YaSTa
- Konfiguracja LVM z linii poleceń

Dodatkowe informacje o konfigurowaniu LVM można znaleźć w [LVM HOWTO:](http://tldp.org/HPWTO/LVM-HOWTO)

#### Jak używać komponentów LVM

W linuksowym systemie plików konwencjonalne partycje na dysku twardym są mało elastyczne.

Gdy partycja jest zapełniona, musimy przenieść dane na inne medium zanim możemy zwiększyć rozmiar partycji, po zmianie rozmiaru - musimy stworzyć nowy system plików, a następnie ponownie przekopiować dane.

W dodatku - na ogół te zmiany łączą się ze zmianami partycji sąsiednich, co znowu zmusza do robienia kopii zapasowych tych partycji na inne media, a następnie, po zakończeniu partycjonowania, na nowo zapisania oryginalnych danych.

```
Projekt LVM był odpowiedzią na problem modyfikacji rozmiaru partycji w linuksowych systemach plików.
```

LVM dostarczą dodatkowej warstwy abstrakcji - wirtualnego zasobu pamięci zwanego grupą woluminów, z których z kolei można tworzyć potrzebne woluminy.

System operacyjny zapewnia dostęp do logicznych woluminów identycznie jak do fizycznych partycji.

To podejście pozwala na zmianę rozmiaru fizycznych mediów bez wpływu na aplikacje.

Podstawowa struktura LVM składa się z następujących składowych:
