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

![woluminy logiczne](/images/2024/logical_volumes.webp "woluminy logiczne")
<figcaption>woluminy logiczne</figcaption>

#### Jak używać komponentów LVM

- Fizyczny wolumin – fizycznym woluminem może być partycja lub cały dysk.
- Grupa woluminów – grupa woluminów zawierająca jeden lub wiele fizycznych woluminów zgrupowanych razem.

Fizyczne partycje mogą się rozpościerać na różnych dyskach twardych. Można dodać dyski twarde lub partycje do grupy woluminów w dowolnym momencie, kiedy tylko jest to potrzebne.

Grupy woluminów można również redukować (zmniejszać ich wielkość) poprzez usunięcie fizycznych woluminów (dysków twardych lub partycji).

- Logiczne woluminy – są częścią grupy woluminów. Logiczne woluminy można formatować lub montować tak jak fizyczne partycje.

```
Można myśleć o grupie woluminów jako o dyskach twardych, a o logicznych woluminach jak o partycjach na tych dyskach.
```

Grupę woluminów można podzielić na szereg logicznych dysków, którym można przypisać nazwy urządzeń (np. `/dev/system/usr`) podobnie jak konwencjonalnym partycjom (`/dev/hda1`).

#### Jak wykorzystać cechy LVM

`LVM` jako bardzo elastyczne i wygodne rozwiązanie przy wprowadzaniu zmian w organizacji przestrzeni dyskowej jest bardzo użyteczne praktycznie dla dowolnego komputera.

Następujące cechy `LVM` są szczególne użyteczne przy praktycznej implementacji rozwiązań organizacji pamięci masowej:
- można połączyć kilka dysków twardych lub partycji w dużą grupę woluminów,
- wygodna zmiana organizacji pamięci masowej - w każdej chwili można powiększyć logiczny wolumin, gdy brakuje na nim wolnego miejsca dla danych.

Zmiana rozmiarów logicznych woluminów jest o wiele łatwiejsza niż zmiana rozmiarów partycji fizycznych.
- Możemy utworzyć ekstremalnie duże logiczne woluminy – liczone w terabajtach,
- zdolność do wymiany części sprzętu bez wyłączania całości ( "hot-swappable") - można dodawać dysk twardy do grupy woluminów przy pracującym systemie,
- można "na gorąco" dodać logiczny wolumin w pracującego systemie - o ile jest wolna przestrzeń w grupie woluminów,
- można użyć kilka dysków z poprawioną wydajnością w trybie RAID 0 (striping),
- nie ma praktycznie limitu liczby logicznych woluminów (limit w LVM v1 wynosił 256),
- dostępna jest cecha tzw. migawek (snapshot) z systemu i co za tym idzie, - tworzenia kopii zapasowych w pracującym systemie - " na bieżąco".

#### Konfiguracja LVM z linii poleceń

Procedura "ręcznej" konfiguracji LVM poleceniami liniowymi zawiera wiele kroków, z dedykowanymi narzędziami dla każdego z nich:
- Narzędzia do administracji fizycznymi woluminami
- Narzędzia do zarządzania grupami woluminów
- Narzędzia do administracji woluminami logicznymi
J
est to krótki przegląd, niezawierający wszystkich narzędzi LVM.

Do przejrzenia narzędzi dostępnych z LVM, należy wprowadzić polecenie 

```bash
rpm -ql lvm2 | less.
```
Wyświetlone zostaną odpowiednie strony manuala.

#### Narzędzia do administracji fizycznymi woluminami

Partycje lub dyski - `LVM` może obsługiwać jako fizyczne woluminy.

`ID partycji` użytej jako część LVM powinien być Linux LVM, 0x8e; ale 0x83, Linux też jest obsługiwany poprawnie.

By wykorzystać cały dysk jako fizyczny wolumin - nie może zawierać on tablicy partycji.

Istniejącą tablicę partycji nadpisujemy poleceniem liniowym dd:

```bash
dd if=/dev/zero of=/dev/sdb1 bs=512 count=1
```

Następnym krokiem będzie inicjalizacja partycji LVM narzędziem pvcerate:

```bash
pvcreate /dev/sdb1
```

Pozostałe polecenia:

```bash
pvs
pvdisplay
```

#### Narzędzia do zarządzania grupami woluminów

Narzędzie `vgcreate` wykorzystywane jest do tworzenia nowych grup woluminów.

Poniższy przykład pokazuje tworzenie grupy woluminów o nazwie `system` z dodaniem partycji `/dev/sdb1`:

```bash
vgcreate system /dev/sdb1
```

Pozostałe polecenia:

```
vgs, vgdisplay, vgresize, vgreduce, vgextend, vgchange, vgscan
```

#### Narzędzia do administracji woluminami logicznymi

W celu stworzenia woluminu logicznego podajemy polecenie lvcreate określając rozmiar woluminu, nazwę woluminu i grupy woluminów, w ramach której wolumin logiczny tworzymy. W tym przypadku rozmiar woluminu to 100 MB.

Możemy też przypisać całą dostępną przestrzeń poniższym poleceniem:

```bash
lvcreate –L 100M –n data system
```

Pozostałe polecenia:

```bash
lvcreate -l 100%VG –n data system
```

```
lvs, lvdisplay, lvresize, lvreduce, lvextend
```

#### Narzędzia do zmiany rozmiarów partycji

W celu zmiany rozmiaru partycji możemy zastosować poniższe narzędzia:

- xfs_growfs - rozszerza istniejący system plików XFS

```bash
xfs_growfs -n /dev/system/data
```

- resize2fs - zmienia rozmiar systemu plików ext2/ext3/ext4

```bash
resize2fs /dev/system/data
```

