---
title: "Moduł 2 - Zarządzanie dyskami - teoria"
date:  2024-02-08T13:00:00+00:00
description: "Moduł 2 - Zarządzanie dyskami - teoria"
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
- Zarządzanie dyskami
image: images/2024-thumbs/zarzadzanie-dyskami.webp
---
## Część Teoretyczna
### Moduł 2: Zarządzanie dyskami - teoria
#### Czas Trwania: 7 minut

### 1. **Omówienie systemów plików (ext3/4, btrfs, xfs.**

- Różnice pomiędzy /ext2/etx3/ext4, btrfs, xfs **(uwaga przy zmniejszaniu!)**

Tradycyjne linuksowe systemy plików nie obsługują tworzenia dziennika (kroniki - journal) danych oraz metadanych takich, jak uprawnienia, rozmiary plików, znaczniki czasowe itd.

Do tradycyjnych systemów plików możemy zaliczyć:

- **ext2** system plików bazujący na i-węzłach (i-node), projektowany pod kątem szybkości i efektywności, łatwo też nie ulega fragmentacji.
- **MS-DOS/VFAT – FAT** (File Allocation Table) jest podstawowym systemem dla klientów korzystających ze starszych wersji systemów Windows. VFAT jest 32-bitową, wirtualną wersją FAT obsługującą długie nazwy.
- **minix** – jest starym i dość ograniczonym co do możliwości systemem, wykorzystywanym jeszcze czasem dla napędów dyskietek czy RAM dysków.

Utworzenie dziennika przyspiesza i ułatwia sprawdzenie, czy dysk nie jest uszkodzony i czy dane nie zostały utracone. W dzienniku rejestrowane są zmiany dokonane od ostatniego kontrolowanego wyłączenia systemu. Dane te wskazują programowi skanującemu dysk i miejsce gdzie modyfikowane dane powinny się znajdować.
- **ext3** – rozszerzona wersja ext2 wspierająca księgowanie zmian w logach (dzienniki).
System wydajny i szybki, chociaż nie najlepiej skalowalny do wielkich wolumenów z wielka liczba plików.
- **ext4** - następca ext3, jeden z najpopularniejszych systemów plików dla Linuksa.
W porównianiu do swojego poprzednika, oferuje on obsługę większych woluminów i plików (używa adresowania 48-bitowego). Obsługuję także większą liczbę podfolderów (dwukrotnie wiekszą liczbę!). Ext4 jest wstecznie kompatybilny z ext3 oraz ext2, co pozwala na zamontowanie ext2 oraz ext3 jako ext4.
- **ReiserFS** – system stworzony od podstaw przez Hansa Reisera - bezpieczniejszy i szybszy niż ext2.
System ten zarządza blokami w sposób odmienny niż ext2, pozwalając wielu małym plikom na wspólne korzystanie z bloku.
ReiserFS traktuje całą partycję dysku jako pojedynczą tablicę bazy danych.
Katalogi, pliki, metadane plików są organizowanę w efektywną strukturę danych zwaną zrównoważonym drzewem (balanced tree), co znakomicie poprawia szybkość obsługi aplikacji, zwłaszcza pracujących na dużej ilości małych plików.
- **XFS** – bardzo wydajny system plików z księgowaniem, stworzony przez firmę SGI (Silicon Graphics, Inc.) dla systemów Unix, a następnie przeniesiony do systemów linuksowych.
XFS łączy zaawansowaną technologię tworzenia dzienników z pełnym wykorzystaniem 64 bitowego adresowania, skalowalne struktury i algorytmy.
- **NTFS** – New Technology File System – system wykorzystywany przez Microsoft.
Aktualnie w Linuksie można jedynie odczytywać dane z tego systemu, obsługa tworzenia, zapisu i kasowania plików jest w fazie eksperymentalnej.
- **BTRFS** -  (ang. B-tree File System) – system plików dla systemu Linux. Firma Oracle ogłosiła prace nad nim w 2007, a sam system został udostępniony na licencji GNU General Public License. Jest domyślnym systemem plików dla dystrybucji openSUSE i Fedora.
Więcej: https://pl.wikipedia.org/wiki/Btrfs 

#### Zarządzanie partycjami za pomocą fdisk

```bash
sudo fdisk -l
Disk /dev/sda: 111.79 GiB, 120034123776 bytes, 234441648 sectors
Disk model: 100-120-G3      
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 33553920 bytes
Disklabel type: dos
Disk identifier: 0xc2cf0f7b

Device     Boot  Start       End   Sectors   Size Id Type
/dev/sda1         8192    532479    524288   256M  c W95 FAT32 (LBA)
/dev/sda2       532480 234441647 233909168 111.5G 83 Linux
```
#### Tworzenie systemów plików z linii poleceń

Można użyć następujących poleceń, by utworzyć system plików z wiersza poleceń:

```bash
mkefs
mkfs.ext3
mkfs.ext4
mkreiserfs
```

Możemy utworzyć systemy plików (takie jak ext2, ext3, MS-DOS, MINIX, XFS, JFS) za pomocą polecenia mkfs (make file system).To polecenie jest kluczowym poleceniem używanym do tworzenia systemów plików. W poleceniu mkfs musimy poprzez opcję -t wskazać typ systemu plików, który chcemy utworzyć. Jeżeli nie wskażemy typu systemu plików, mkfs automatycznie utworzy, jako domyślny, system plików ext2.

```bash
mkfs -t ext3 /dev/sda1
mkfs -t ext4 /dev/sda1
mkfs -t reiserfs /dev/sda1
```

#### Montowanie systemu plików z linii poleceń

Linux nie używa liter jako nazw identyfikujących wolumeny/partycje (jak to robi np. Microsoft Windows), montuje partycje w katalogu w systemie plików. Katalogi użyte do montowania - nazywane są punktami montowania. Dla przykładu, aby dodać nowy dysk twardy do systemu Linux:
- najpierw należy go podzielić na partycje i sformatować,
- potem utworzyć katalog (taki jak np. /data) w systemie plików,
- w utworzonym katalogu zamontować dysk używając polecenia montowania – **mount**.

W celu skasowania montowania systemu plików, użyjemy polecenia odmontowania – **umount**.

Do katalogów utworzonych w naszym systemie plików można również zamontować zdalne systemy plików, udostępniane przez Network File System **(NFS)**.

Katalog / mnt / jest domyślnie używany do montowania lokalnych i zdalnych systemów plików.

Wszystkie mobilne urządzenia są zamontowane domyślnie w katalogu **/media** np.
- CD-ROM dev/cdrom jest domyślnie montowany do **/media/cdrom**,
- Dyskietka /dev/floppy jest domyślnie montowana do **/media/floppy**.

W środowisku graficznym GNOME lub KDE, nośniki takie jak dyskietki czy też CD lub DVD są automatycznie montowane i odmontowywane przy użyciu domyślnych ustawień w **/etc/fstab** i właściwości opisanych w **submount/subfs**.

#### Plik konfiguracyjny /etc/fstab

Aby zrozumieć jak zarządzać montowaniem (i odmontowywaniem) systemów plików, musimy poznać następujące zagadnienia:
- Plik konfiguracyjny /etc/fstab
- Przeglądanie aktualnie zamontowanych systemów plików
- Montowanie systemów plików
- Odmontowywanie systemów plików

Pliki systemowe i ich punkty montowania w drzewie katalogów są konfigurowane w pliku **/etc/fstab**. Plik ten zawiera jedną linię z 6 polami dla każdego zamontowanego systemu plików. Linie te wyglądają podobnie do przedstawionych poniżej:

```bash
cat /etc/fstab 
/dev/mapper/debian--vg-root                /               ext4         errors=remount-ro 0       1
UUID=0b118dfa-6c87-4274-8c67-ad6eda9ed4c0  /boot           ext2         defaults          0       2
UUID=C267-57A1                             /boot/efi       vfat         umask=0077        0       1
/dev/mapper/debian--vg-home                /home           ext4         defaults          0       2
/dev/mapper/debian--vg-tmp                 /tmp            ext4         defaults          0       2
/dev/mapper/debian--vg-var                 /var            ext4         defaults          0       2
/dev/mapper/debian--vg-swap_1              none            swap         sw                0       0
/dev/sr0                                   /media/cdrom0   udf,iso9660  user,noauto       0       0
```

#### Przeglądanie aktualnie zamontowanych systemów plików

W celu przejrzenia aktualnie zamontowanych systemów plików podajemy polecenie mount. Wynik tego polecenia przedstawiony jest poniżej.

```bash
# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=8104820k,nr_inodes=2026205,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=1626680k,mode=755,inode64)
/dev/mapper/debian--vg-root on / type ext4 (rw,relatime,errors=remount-ro)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,inode64)
tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k,inode64)
cgroup2 on /sys/fs/cgroup type cgroup2 (rw,nosuid,nodev,noexec,relatime)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
efivarfs on /sys/firmware/efi/efivars type efivarfs (rw,nosuid,nodev,noexec,relatime)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=30,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=17851)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,pagesize=2M)
debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)
tracefs on /sys/kernel/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)
configfs on /sys/kernel/config type configfs (rw,nosuid,nodev,noexec,relatime)
fusectl on /sys/fs/fuse/connections type fusectl (rw,nosuid,nodev,noexec,relatime)
sunrpc on /run/rpc_pipefs type rpc_pipefs (rw,relatime)
/dev/sda2 on /boot type ext2 (rw,relatime)
/dev/sda1 on /boot/efi type vfat (rw,relatime,fmask=0077,dmask=0077,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro)
/dev/mapper/debian--vg-home on /home type ext4 (rw,relatime)
/dev/mapper/debian--vg-tmp on /tmp type ext4 (rw,relatime)
/dev/mapper/debian--vg-var on /var type ext4 (rw,relatime)
lxcfs on /var/lib/lxcfs type fuse.lxcfs (rw,nosuid,nodev,relatime,user_id=0,group_id=0,allow_other)
/dev/fuse on /etc/pve type fuse (rw,nosuid,nodev,relatime,user_id=0,group_id=0,default_permissions,allow_other)
```

#### Montowanie systemów plików

- Poleceniem mount możemy ręcznie zamontować system plików.
- Ogólna składnia polecenia montowania wygląda następująco:
- mount [-t typ_systemu_plików] [-o opcje montowania] urządzenie punkt_montowania
- Polecenie mount nadpisuje domyślne ustawienia pobrane z pliku /etc/fstab.
- W poniższym przykładzie zamontowano partycje /dev/sdb6 w katalogu /space

#### Odmontowywanie systemów plików

Zamontowany system plików można odmontować z linii poleceń - poleceniem umount wskazując na urządzenie lub punkt montowania.
Przykładowo, aby rozmontować nagrywarkę CD zamontowaną w katalogu **/media/cdrecorder** wykonamy jedno z następujących poleceń:

```bash
umount /media/cdrecorder
```

lub

```bash
umount /dev/hdb
```

Wykonując polecenie umount system w pierwszej kolejności sprawdza czy dany system plików nie jest używany.

Gdy jest zajęty np. używany przez kogoś lub jakiś proces, wówczas system odmawia odmontowania go.

Jednym ze sposobów zapewniających pewniejsze odmontowanie systemu plików jest przejście do katalogu głównego poleceniem **cd /**.

Jednak, jeżeli dalej system widzi dany system plików jako zajęty, możemy zmusić go do natychmiastowego odmontowania danego sytemu plików poleceniem **umont -f**.

Polecenie to nakazuje natychmiastowe i bezwarunkowe rozmontowanie systemu plików.

Polecenie umount z opcją -f wykorzystujemy tylko w newralgicznych sytuacjach.

Bardziej bezpieczną opcją jest odmontowanie za pomocą polecenia **umount –l (lazy)**

Jaki jest najlepszy sposób na bezpieczne odmontowanie systemu plików?

#### Monitorowanie systemów plików

W momencie ustawienia konfiguracji systemu i rozpoczęcia działania, musimy rozpocząć również nadzorowanie jego pracy i wykorzystanie zasobów.

By efektywnie monitorować stan systemu oraz badać poprawność jego działania, powinniśmy zapoznać się następującymi tematami:
- Sprawdzanie wykorzystania partycji i plików
- Sprawdzanie otwartych plików
- Identyfikacja plików wykorzystywanych przez procesy
- Sprawdzanie katalogu lost+found
- Sprawdzanie i naprawa systemów plików
- Dodatkowe narzędzia do zarządzania systemami plików

#### Sprawdzanie wykorzystania partycji i plików

Polecenia liniowe pomagające w monitorowaniu wykorzystania partycji i systemu plików:

**df** - dostarcza informacje o lokalizacji punktów zamontowania dysków w systemie plików oraz o tym, ile miejsca zajmuje dany dysk twardy, partycja czy też inny napęd.

Po podaniu polecenia **df** bez parametrów - system wyświetla dostępną przestrzeń dyskową we wszystkich aktualnie zmontowanych systemach plików. Jeżeli wprowadzimy nazwę pliku, polecenie df wyświetli nam dostępną przestrzeń dyskową w systemie plików, w którym znajduje się wskazany plik.

Użyteczne opcje polecenia **df** , to:
- **-h** - df wyświetla nam dostępne miejsce w formacie czytelnym dla człowieka, tzn. w MB lub GB,
- **-i** - wyświetlana jest informacja o i-węźle zamiast informacji o wykorzystaniu bloku,
- **-l** – wyświetla limity dotyczące lokalnego systemu plików.

Przykład: polecenie liniowe **df -lh** wyświetli informację o wszystkich lokalnych systemach plików w formacie czytelnym dla człowieka/

**du** – dostarcza informacji o przestrzeni zajmowanej przez pliki i katalogi.

Pomocnymi opcjami wykorzystywanymi w tym poleceniu są:
- **-c** – wyświetla wszystko łącznie z podsumowaniem,
- **-h** – wyświetla wszystko, ale w przyjaznym formacie,
- **-s** – wyświetla tylko ogólne dane dla każdego argumentu,
- **--exclude=wzorzec** - bez informacji o plikach odpowiadających podanemu wzorcowi (pattern).

Przykład: **du-h --exclude='*.o'** wyświetli informacje w przyjaznym dla człowieka formacie dla wszystkich plików poza plikami, których nazwa kończy się znakami ".o".

#### Sprawdzanie otwartych plików

Polecenie liniowe **lsof** listuje otwarte pliki.

Polecenie **lsof** podane bez żadnych opcji, pokazuje wszystkie otwarte pliki należące do wszystkich aktywnych procesów.

Otwarte pliki mogą być plikami regularnymi, katalogami, plikami urządzeń, bibliotekami, strumieniami lub plikami sieciowymi.

Polecenie to można uruchomić w pętli, wykorzystując opcję **-r**, wtedy wyświetlanie aktualizowanej listy będzie powtarzane aż do zatrzymania działania polecenia sygnałem quit lub innym przerwaniem.

Polecenie sprawdzania otwartych plików ma kilka innych, przydatnych opcji.

Są to:
- **-c x** - wyświetla tylko pliki zaczynające się od x,
- **-s** - wyświetla rozmiary plików,
- **-u x** wyświetla pliki należące do użytkownika x.

Dla przykładu poleceniem: `lsof -s -u root,adrian` wyświetlimy listę otwartych plików należących do użytkownika root i adrian wraz z ich rozmiarem.

#### Identyfikacja plików wykorzystywanych przez procesy

Polecenie **fuser** wyświetla identyfikator procesu PID, wykorzystującego dane pliki lub system plików.

W domyślnym trybie wyświetlania, po każdej nazwie (lub PID) wyświetlane są oznaczenia literowe opisujące typ dostępu:
- **-c** : bieżący katalog,
- **-e** : uruchomiony plik wykonywalny,
- **-F** : plik otwarty (pomijany w domyślnym trybie wyświetlania),
- **-r** : katalog główny,
- **-m** : plik mapowania pamięci lub biblioteka współdzielona.

W poleceniu tym można wykorzystać, między innymi, następujące opcje:
- **-a** zwraca informacje o wszystkich plikach, nieużywanych też,
- **-v** włącza tryb szczegółowy (verbose),
- **-u** dołącza ID użytkownika - właściciela procesu do każdego identyfikatora PID,
- **-m** pokazuje wszystkie procesy, które mają dostęp do plików na danej partycji w danym katalogu.

Przykład: `fuser -m /home` wyświetli PID dla procesów o dostępie do plików na partycji, na której jest katalog `/home/`.

#### Sprawdzanie katalogu lost+found

- Katalog lost+found specyficzny dla systemów plików ext2 i ext3.
- Po załamaniu się systemu, Linux automatycznie przeprowadza kompleksowe sprawdzenie systemu plików.
- Pliki lub fragmenty plików których nie można do niczego przydzielić, nie są usuwane, lecz składowane w katalogu lost+found.
- Przeglądając zawartość tego katalogu, można próbować rekonstrukcji oryginalnej nazwy oraz przeznaczenia pliku.

#### Sprawdzanie i naprawa systemów plików

Polecenie liniowe `fsck` pozwala na sprawdzenie oraz (opcjonalnie) naprawę jednego lub kilku systemów plików linuksowych.

Standardowo polecenie to próbuje wykonywać sprawdzenie systemów plików na różnych dyskach równolegle, by zredukować całkowity czas trwania sprawdzenia wszystkich systemów plików.

Jeżeli nie podamy systemu plików w linii poleceń i nie podamy opcji `-A`, wówczas program `fsck` domyślnie sprawdzi systemy plików według `/etc/fstab` - po kolei.

Program `fsck` jest po prostu interfejsem dla różnych programów sprawdzających dostępne w linuksie systemy plików (fsck.fstype).

**Poszukiwanie programu specyficznego dla danego systemu plików odbywa się w pierwszej kolejności w katalogu `/sbin`, następnie w `/etc/fs` i `/etc`, a ostatecznie w katalogach wymienionych w zmiennej środowiskowej `PATH`.**

Składnie polecenia jest następująca:

`fsck` urządzenie (device)

`urządzenie` może być nazwą urządzenia (np. /dev/hda1, /dev/sda2), punktem montowania (np. /, /home), albo etykietą ext2 lub identyfikatorem UUID.

Najbardziej użyteczne opcje polecenia podano poniżej:
- **-A** nakazuje przejście poprzez plik /etc/fstab i sprawdzanie poszczególnych systemów zawartych w tym pliku,
- **-N** – nie wykonuje operacji, a jedynie pokazuje co byłoby wykonane,
- **-V** - przechodzi w tryb szczegółowy (verbose) wyświetlając szczegółowe komunikaty, łącznie ze wszystkimi wykonywanymi poleceniami specyficznymi dla poszczególnych systemów plików.

#### Sprawdzenie i naprawa systemów plików ext2/ext3 oraz ReiserFS

Zamknięcie systemu linuksowego bez prawidłowego rozmontowania partycji, powoduje powstawanie błędów w systemie plików. Podczas następnego startu systemu fakt, iż system został nieprawidłowo zamknięty - jest wykrywany przez system, a następnie automatycznie uruchamiane jest sprawdzanie systemu. Jeżeli błędy znajdują się w systemie plików, są one naprawiane w miarę możliwości. Jeżeli błędy znajdują się poza systemem plików i nie można uruchomić prawidłowo systemu, wówczas musimy ręcznie uruchomić system w trybie odzyskiwania; po wprowadzeniu hasła roota - sprawdzić system.

W przypadku uszkodzenia systemu plików mamy do dyspozycji system ratunkowy do naprawy systemu.

W zależności od systemu plików - wprowadzamy `/sbin/e2fsck` lub `/sbin/reiserfsck`.

Narzędzia `/sbin/e2fsck` oraz `/sbin/reiserfsck` sprawdzają system pod kątem poprawnego superbloku (bloku znajdującego się na początku partycji zawierającego informacje o strukturze systemu plików), wadliwych bloków danych lub błędnej alokacji (przydzielenia) bloków danych.

Najbardziej prawdopodobnym problemem w systemie ext2/ext3 jest uszkodzenie superbloku.

Należy więc w pierwszej kolejności przejrzeć wszystkie kopie superbloku programem `dumpe2fs`.

A następnie, za pomocą narzędzia `e2fsck`, możemy wykorzystać jedną z kopii zapasowych systemu:

```bash
e2fsck –f –b 32768 /dev/hda1
```

W przykładzie powyższym, użyto superblok ulokowany w bloku danych 32768 w systemie plików ext2 na partycji /dev/hda1, a główny (primary) superblok odpowiednio zostanie zaktualizowany po zakończeniu sprawdzania systmu plików.

Poleceniem `reiserfsck` sprawdzana jest spójność systemu plików ReiserFS.

Sprawdzany jest przede wszystkim dziennik (kronika) w celu określenia czy są jakieś transakcje, które powinny być powtórzone.

Z opcją `–fix-fixable`, błędy takie, jak zły rozmiar pliku zostają automatycznie naprawione jak tylko zostanie ukończone sprawdzanie systemu plików.

Jeżeli błąd występuje w binarnym drzewie (b-drzewo), istnieje możliwość odbudowania jego struktury poleceniem `reiserfsck –rebuild-tree`.

#### Dodatkowe narzędzia do zarządzania systemami plików

Dodatkowe narzędzia - polecenia liniowe przydatne administratorowi systemów plików:

`tune2fs` – wykorzystywany jest jako dodatkowe narzędzie do dostrajania parametrów systemu plików ext2/ext3.

Przykłady:
- ustalenie z góry liczby dni lub liczby montowań systemu plików, co które będzie wykonywane sprawdzenie systemu plików,
- dodanie etykiety do systemu plików lub dodanie księgowania do systemu `ext2`,
- konwersja `ext2` systemu plików w `ext3`.
- `reiserfstune` – jest narzędziem dostrajającym dla systemu ReiserFS.
- `resize2fs` i `resize_reiserfs` są z kolei używane do zmniejszenia lub rozszerzenia systemów odpowiednio: `ext2/ext3` oraz `ReiserFS`. 
- `resize_reiserfs` może powiększyć system `ReiserFS` online.

```
Pomniejszenie jak i powiększenie systemu `ext2/ext3` można przeprowadzić tylko gdy system plików jest odmontowany.
```

```
Przed każdą manipulacją partycjami i systemami plików - konieczne jest zrobienie dobrej kopii bezpieczeństwa danych!
```

### Dodatkowa wiedza

#### Dysk

Dysk, w skrócie dysk twardy, to urządzenie do przechowywania danych służące do zapisywania i odczytywania informacji cyfrowych za pomocą jednego lub większej liczby sztywnych, szybko obracających się dysków (talerek) pokrytych materiałem magnetycznym. Dyski mogą być różnych typów, w tym Dysków Twardych (HDD) i Dysków Stanu Stałego (SSD). Ich główne funkcje to:

- **Przechowywanie danych**: Służą jako główne medium do przechowywania wszelkiego rodzaju danych cyfrowych, w tym systemów operacyjnych, aplikacji i danych użytkownika.
- **Operacje odczytu/zapisu**: Wykonywanie operacji odczytu i zapisu w celu dostępu do danych i ich przechowywania. Wydajność tych operacji zależy od typu dysku (np. SSD są szybsze niż HDD).

##### Dyski (HDD i SSD)

- **Nośniki fizyczne**: Dyski używają fizycznych nośników do przechowywania danych. HDD przechowują dane magnetycznie na obracających się talerzach, podczas gdy SSD używają chipów pamięci flash (NAND flash) do przechowywania danych.
- **Mechanika dostępu do danych**: W przypadku HDD dostęp do danych wymaga części mechanicznych (np. głowice odczytu/zapisu poruszające się nad obracającymi się talerzami). SSD natomiast nie mają ruchomych części i używają interfejsów elektronicznych do dostępu do danych, co prowadzi do szybszych czasów dostępu do danych.
- **Format**: Dyski mają standaryzowane rozmiary (np. 2,5 cala, 3,5 cala dla HDD; różne formaty dla SSD, takie jak 2,5 cala, M.2, U.2) i łączą się przez interfejsy takie jak SATA, SAS lub NVMe.
- **Zużycie energii**: HDD zazwyczaj zużywają więcej energii ze względu na ruchome części, podczas gdy SSD są bardziej energooszczędne z powodu braku ruchomych części.

Podsumowując, dyski to fizyczne nośniki, na których przechowywane są dane, zaprojektowane do bezpośredniego wykonywania operacji odczytu i zapisu.

##### Jaka jest różnica między NVMe a złączem M.2?

Różnica między NVMe (Non-Volatile Memory Express) a M.2 polega głównie na ich definicjach i rolach w kontekście technologii przechowywania. NVMe to protokół zaprojektowany do dostępu do szybkich nośników pamięci masowej, podczas gdy M.2 to specyfikacja formy lub fizyczna specyfikacja złączy i modułów. Oto bliższe spojrzenie na każde z nich:

##### NVMe (Non-Volatile Memory Express)

- **Definicja**: NVMe to protokół pamięci masowej specjalnie zaprojektowany dla dysków półprzewodnikowych (SSD) w celu wykorzystania szybkiego magistrali PCIe (Peripheral Component Interconnect Express). Jego celem jest poprawa szybkości i efektywności transferu danych między systemem a urządzeniem przechowującym, w porównaniu ze starszymi protokołami pamięci masowej, takimi jak SATA.
- **Zastosowanie**: NVMe jest używane dla dysków SSD, które są bezpośrednio podłączone do magistrali PCIe, pozwalając im działać z znacznie wyższymi prędkościami niż dyski SSD oparte na SATA. Dyski NVMe są znane ze swojej niskiej latencji i wysokiej przepustowości, co czyni je idealnymi dla aplikacji wymagających szybkiego dostępu do danych i przetwarzania.
- **Kompatybilność**: Chociaż NVMe jest protokołem, może być implementowany przez różne fizyczne interfejsy, w tym gniazda PCIe i złącza M.2.

##### Złącze M.2

- **Definicja**: M.2 to specyfikacja dla wewnętrznie montowanych kart rozszerzeń komputerowych i powiązanych złączy. Obsługuje różne interfejsy i protokoły transferu danych, w tym PCIe, SATA i USB, co czyni go wysoce wszechstronnym.
- **Forma**: Moduły M.2 występują w różnych rozmiarach, identyfikowanych przez system numeracji, jak 2280, gdzie „22” oznacza szerokość w milimetrach, a „80” długość. Ta kompaktowa forma sprawia, że M.2 nadaje się do małych urządzeń, takich jak laptopy i kompaktowe komputery PC.
- **Zastosowanie**: Gniazdo M.2 może pomieścić urządzenia korzystające z różnych protokołów, w tym dyski SSD NVMe (korzystające z interfejsu PCIe) i dyski SSD SATA. Specyficzne możliwości gniazda M.2 zależą od sposobu, w jaki jest ono podłączone do płyty głównej - dla PCIe, SATA lub obu.

##### Kluczowe różnice

- **Protokół a złącze**: NVMe to protokół dla szybkiego transferu danych z dyskami SSD, podczas gdy M.2 to fizyczne złącze, które może obsługiwać wiele protokołów transferu danych, w tym NVMe.
- **Kompatybilność i użycie**: Gniazdo M.2 może przyjąć dyski SSD NVMe, jeśli jest kompatybilne z PCIe, ale nie wszystkie gniazda M.2 są skonfigurowane do obsługi PCIe, a tym samym NVMe. Z kolei dyski SSD NVMe mogą być podłączone przez inne interfejsy niż M.2, takie jak U.2 lub bezpośrednio do gniazda PCIe za pomocą odpowiedniego adaptera.

Podsumowując, chociaż NVMe i M.2 są oba związane z technologią SSD, pełnią różne role. NVMe definiuje, jak dane są transferowane z wysoką prędkością, a M.2 zapewnia kompaktowe fizyczne złącze, które może obsługiwać protokół NVMe wśród innych. Kompatybilność gniazda M.2 z dyskami SSD NVMe zależy od projektu płyty głównej i konfiguracji samego gniazda M.2.

Wyjaśnijmy związek między NVMe, M.2 i połączeniami między urządzeniami a gniazdami, aby pomóc zrozumieć, jak one współdziałają:

##### NVMe i M.2: Zrozumienie połączenia

- **NVMe (Non-Volatile Memory Express)** nie jest typem fizycznego gniazda ani złącza; to protokół zaprojektowany do maksymalizacji wydajności dysków półprzewodnikowych (SSD) poprzez wykorzystanie szybkiej magistrali PCIe (Peripheral Component Interconnect Express). Zasadniczo NVMe określa, jak dane są transferowane przez PCIe, aby osiągnąć szybsze prędkości odczytu/zapisu w porównaniu ze starszymi protokołami przechowywania, takimi jak SATA.

- **M.2** to forma złącza i modułów, która obsługuje różne typy interfejsów, w tym PCIe i SATA. Gniazdo M.2 na płycie głównej może pomieścić moduły M.2 (karty), które używają tych interfejsów do łączności.

##### Podłączanie dysków SSD NVMe do gniazd M.2

- Możesz podłączyć **dysk SSD NVMe do gniazda M.2**, które obsługuje PCIe. Dzieje się tak, ponieważ dyski SSD NVMe używają interfejs

u PCIe do transferu danych, a wiele gniazd M.2 jest przewodzone do obsługi łączności PCIe, wykorzystując tym samym wysokoszybkościowe możliwości protokołu NVMe.

##### Podłączanie modułów M.2 do płyt głównych

- Jeśli chodzi o **podłączanie modułu M.2 (który może być dyskiem SSD) do płyty głównej**, kluczowe jest dopasowanie interfejsu obsługiwanego przez gniazdo M.2 do modułu M.2. Jeśli moduł M.2 to dysk SSD NVMe (używający PCIe do transferu danych), gniazdo M.2 musi obsługiwać PCIe. Jeśli moduł M.2 używa SATA (inny protokół, który jest również obsługiwany przez niektóre gniazda M.2), wówczas gniazdo musi obsługiwać SATA.

##### Wyjaśnienie nieporozumienia

- Zamieszanie może wynikać z terminu **"gniazdo NVMe"**. Ponieważ NVMe jest protokołem, a nie fizycznym interfejsem, nie odnosimy się do fizycznych gniazd na płytach głównych jako "gniazd NVMe". Zamiast tego mamy gniazda PCIe i M.2, które mogą obsługiwać protokół NVMe, jeśli są kompatybilne z PCIe.

- Dlatego poprawne zrozumienie polega na tym, że **możesz podłączyć dysk SSD NVMe do gniazda M.2**, jeśli to gniazdo obsługuje połączenia PCIe. Nie ma pojęcia podłączania czegoś do "gniazda NVMe", ponieważ NVMe dotyczy sposobu transferu danych, a nie typu fizycznego połączenia.

Podsumowując, kompatybilność zależy od interfejsu obsługiwanego przez gniazdo M.2 (PCIe dla dysków SSD NVMe lub SATA dla dysków SSD SATA), a nie tylko od fizycznej formy. M.2 jest wszechstronny i może obsługiwać zarówno protokoły NVMe, jak i SATA, w zależności od tego, jak producent płyty głównej zaprojektował gniazdo M.2.

##### Gniazda PCIe i SATA

Podsumowując, w kontekście podłączania urządzeń do przechowywania danych, takich jak dyski SSD (Solid State Drives) do płyty głównej, głównymi rodzajami gniazd lub interfejsów, z którymi się spotkasz, są PCIe (Peripheral Component Interconnect Express) i SATA (Serial ATA). Oto krótki przegląd każdego z nich:

##### PCIe (Peripheral Component Interconnect Express)

- **Cel**: Standard interfejsu wysokiej prędkości do łączenia urządzeń sprzętowych z płytą główną komputera, w tym dysków SSD, kart graficznych i innych kart rozszerzeń.
- **Prędkość**: Oferuje znacznie wyższe prędkości transferu danych w porównaniu z SATA, z prędkościami zależnymi od liczby pasm (x1, x4, x8, x16) i wersji PCIe (np. PCIe 3.0, 4.0, 5.0). Każda wersja podwaja przepustowość na pasmo w porównaniu z poprzednią wersją.
- **Użycie dla dysków SSD**: Gniazda PCIe są używane dla dysków SSD NVMe, które są zaprojektowane, aby wykorzystać wysoką przepustowość PCIe, oferując szybsze prędkości odczytu/zapisu niż dyski SSD SATA. Dyski SSD NVMe mogą być bezpośrednio włożone do gniazd PCIe lub do gniazd M.2, które są kompatybilne z PCIe.

##### SATA (Serial ATA)

- **Cel**: Interfejs używany do łączenia urządzeń do przechowywania masowego, takich jak dyski twarde (HDD) i dyski półprzewodnikowe (SSD), z płytą główną.
- **Prędkość**: SATA III, najnowsza wersja SATA używana obecnie, oferuje prędkości transferu danych do 6 Gb/s, co jest wystarczające dla wielu zastosowań, ale wolniejsze niż rozwiązania oparte na PCIe.
- **Użycie dla dysków SSD**: Porty SATA są używane do łączenia dysków SSD SATA, które są powszechnie używane do przechowywania ze względu na ich równowagę między wydajnością, pojemnością i kosztem. Dyski SSD SATA mogą być również podłączone do gniazd M.2, które obsługują interfejs SATA.

##### Gniazda M.2: Warto wspomnieć

- **Wszechstronność**: M.2 to forma i może obsługiwać zarówno interfejsy SATA, jak i PCIe, w zależności od tego, jak gniazdo jest skonfigurowane przez producenta płyty głównej. Gniazdo M.2 może więc pomieścić zarówno dyski SSD SATA, jak i NVMe, ale ważne jest, aby sprawdzić specyfikacje płyty głównej, aby zrozumieć, co każde gniazdo M.2 obsługuje.

Podsumowując, PCIe i SATA są głównymi interfejsami do łączenia urządzeń do przechowywania danych z płytą główną, z PCIe oferującym wyższe prędkości, a SATA zapewniającym szeroką kompatybilność i opłacalność. Gniazda M.2 dodają wszechstronność, obsługując oba interfejsy, co pozwala na kompaktowe i elastyczne rozwiązania do przechowywania danych, szczególnie w laptopach i komputerach o małej formie.