---
title: "Moduł 2 - Konfiguracja sieciowa - zadania"
date:  2024-02-09T09:50:00+00:00
description: "Moduł 2 - Konfiguracja sieciowa - zadania"
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
- Konfiguracja sieciowa
image: images/2024-thumbs/konfiguracja-sieciowa.webp
---
## Część Praktyczna
### Moduł 2: Konfiguracja sieciowa - zadania
#### Czas Trwania: 15 minut

#### 1. **Praktyczne ćwiczenia z konfiguracji sieciowej**

- **Ćwiczenie:** Konfiguracja statycznego adresu IP na interfejsie sieciowym.
  1. Użyj narzędzia `ip` lub `nmcli` do zmiany adresu IP na wybranym interfejsie na statyczny adres z wybranej podsieci.
  2. Sprawdź połączenie z nowym adresem IP, wykonując ping na adres routera.

##### Zadania z analizy i konfiguracji sieci (7 minut)

**Cel:** Naucz się konfigurować statyczny adres IP i rozwiązywać podstawowe problemy sieciowe.
**Czas:** 15 minut
**Wymagania:**
* Komputer z systemem Linux
* Podłączenie do sieci
* Dostęp do terminala

**Ćwiczenie:**
1. Uruchom terminal.
2. Sprawdź listę interfejsów sieciowych za pomocą polecenia `ip link show`.
3. Wybierz interfejs, na którym chcesz skonfigurować statyczny adres IP. Zapamiętaj jego nazwę (np. `enp0s3`).

**Konfiguracja statycznego adresu IP:**
4. Użyj narzędzia `ip` lub `nmcli` do zmiany konfiguracji interfejsu sieciowego.

**Opcja 1: Użycie narzędzia `ip`**
```bash
ip address add 192.168.1.10/24 dev enp0s3
```

**Opcja 2: Użycie narzędzia `nmcli`**
```bash
nmcli connection modify enp0s3 ipv4.addresses "192.168.1.10/24"
```
5. Sprawdź, czy nowy adres IP został poprawnie skonfigurowany:
```bash
ip address show dev enp0s3
```
6. Wykonaj ping na adres routera, aby sprawdzić połączenie sieciowe:
```bash
ping 192.168.1.1
```  

#### 2. **Praktyczne ćwiczenia z rozwiązywania problemów sieciowych**

##### Rozwiązywanie problemów sieciowych na przykładowych scenariuszach (7 minut)

- **Ćwiczenie:** Symulacja i rozwiązanie problemu sieciowego.
  1. Symuluj problem z siecią przez zmianę maski podsieci na niewłaściwą.
  2. Użyj `ping` i `traceroute` do zdiagnozowania problemu.
  3. Przywróć poprawną maskę podsieci i sprawdź ponownie łączność.

**Ćwiczenie:**
1. Zmień maskę podsieci na interfejsie sieciowym na niewłaściwą (np. `255.255.255.0`).
```bash
ip address add 192.168.1.10/0 dev enp0s3
```
2. Spróbuj wykonać ping na adres routera. PING powinien zawieść.
3. Użyj narzędzia `traceroute` do zdiagnozowania problemu:
```bash
traceroute 192.168.1.1
```
4. Zmień maskę podsieci na poprawną (np. `255.255.255.24`).
```bash
ip address add 192.168.1.10/24 dev enp0s3
```
5. Sprawdź ponownie połączenie sieciowe za pomocą polecenia `ping`.


**Uwaga:**
* Należy zachować ostrożność podczas konfiguracji sieci. Nieprawidłowa konfiguracja może uniemożliwić dostęp do Internetu.
* Przed rozpoczęciem ćwiczenia upewnij się, że znasz adres IP routera.


**Pytania do dyskusji:**
* Jakie są zalety i wady korzystania ze statycznego adresu IP?
* Jakie są najczęstsze problemy sieciowe?
* Jakie narzędzia służą do diagnozowania problemów sieciowych?


**Zadania rozszerzające:**
* Skonfiguruj serwer DHCP na swoim komputerze. 
Podpowiedź: Zobacz ten artykuł: [https://p-tech.net.pl/pl/katowice/serwer-dhcp/ ](https://p-tech.net.pl/pl/katowice/serwer-dhcp/)
* Skonfiguruj połączenie VPN. Instrukcja na samym końcu.
* Użyj narzędzia `tcpdump` do analizy ruchu sieciowego. Instrukcja poniżej.
* Użyj narzędzi: `ifconfig`, `netstat`, `ss`, `ip`, `ethtool`, `iperf3`. 
Podpowiedź: Obejrzyj poniższy film, aby zobaczyć, w jaki sposób ich używać.

{{< youtube fc8wMXoX8Lw >}}
<figcaption>Rozwiązywanie problemów z wolną komunikacją sieciową lub przekroczeniem limitu czasu połączenia w systemie Linux</figcaption>

Dodatkowo zestaw zadań do samodzielnego przećwiczenia:

Analiza problemów sieciowych wymaga podejścia wieloaspektowego, gdzie wykorzystanie zarówno przestarzałych narzędzi (deprecated) jak i nowoczesnych odpowiedników jest kluczowe do głębokiej diagnostyki i rozwiązywania problemów. Poniżej przedstawię proste zadania, które pomogą Ci lepiej zrozumieć, jak pracować z tymi narzędziami oraz jakie są różnice w ich wykorzystaniu:

### Zadanie 1: Analiza konfiguracji sieciowej i interfejsów

- **Stare narzędzie:** `ifconfig`
  - **Zadanie:** Wyświetl informacje o wszystkich interfejsach sieciowych na swoim systemie.
  - **Komenda:** `ifconfig -a`

- **Nowe narzędzie:** `ip address` (`ip a`)
  - **Zadanie:** Wyświetl informacje o wszystkich interfejsach sieciowych na swoim systemie, włącznie z adresami IPv4 i IPv6.
  - **Komenda:** `ip address show`

### Zadanie 2: Analiza tras sieciowych

- **Stare narzędzie:** `route`
  - **Zadanie:** Wyświetl tabelę trasowania w systemie.
  - **Komenda:** `route -n`

- **Nowe narzędzie:** `ip route` (`ip r`)
  - **Zadanie:** Wyświetl tabelę trasowania w systemie.
  - **Komenda:** `ip route show`

### Zadanie 3: Diagnostyka nazw domenowych

- **Stare narzędzie:** `nslookup`
  - **Zadanie:** Sprawdź adres IP dla domeny `google.com`.
  - **Komenda:** `nslookup google.com`

Uwaga:

Program `nslookup` nie zawsze jest domyślnie zainstalowany we wszystkich dystrybucjach Linuxa. Jest to narzędzie służące do zapytań o systemy nazw domen (DNS) i może być używane do znajdowania adresów IP powiązanych z nazwami domen oraz odwrotnie. Chociaż jest powszechnie dostępne i używane, niektóre dystrybucje mogą wymagać jego ręcznej instalacji.

W dystrybucjach bazujących na Debianie (jak Ubuntu), `nslookup` może być zainstalowany za pomocą pakietu `dnsutils`. W dystrybucjach opartych na Red Hat (takich jak Fedora lub CentOS), narzędzie to jest częścią pakietu `bind-utils`. Jeśli więc stwierdzisz, że `nslookup` nie jest dostępne na twoim systemie, możesz je łatwo zainstalować za pomocą odpowiedniego menedżera pakietów:

- Dla systemów opartych na Debianie/Ubuntu:
  ```bash
  sudo apt-get update
  sudo apt-get install dnsutils
  ```

- Dla systemów opartych na Red Hat/CentOS/Fedora:
  ```bash
  sudo yum install bind-utils
  ```

- Dla systemów opartych na Arch Linux:
  ```bash
  sudo pacman -S bind-tools
  ```

Warto zauważyć, że w nowoczesnych systemach i dystrybucjach Linuxa coraz częściej zaleca się używanie narzędzia `dig` zamiast `nslookup` ze względu na jego większą elastyczność i rozbudowane możliwości konfiguracyjne. `dig` również może nie być dostępny domyślnie w niektórych dystrybucjach i może wymagać instalacji w podobny sposób.

- **Nowe narzędzie:** `dig`
  - **Zadanie:** Sprawdź adres IP dla domeny `google.com`.
  - **Komenda:** `dig google.com`

Uwaga:

Podobnie jak `nslookup`, `iperf3`, i `ethtool`, narzędzie `dig` również może nie być dostępne domyślnie we wszystkich dystrybucjach Linuxa. `Dig` (Domain Information Groper) jest zaawansowanym narzędziem do przeprowadzania zapytań do serwerów DNS. Jest często używane przez administratorów systemów i sieci do rozwiązywania problemów związanych z DNS, takich jak sprawdzanie propagacji rekordów DNS.

`Dig` jest częścią pakietu `bind-utils` w dystrybucjach opartych na Red Hat (takich jak Fedora, CentOS) i pakietu `dnsutils` w dystrybucjach opartych na Debianie (takie jak Ubuntu). Oto jak można zainstalować `dig`:

- **Debian/Ubuntu i pochodne:**
  ```bash
  sudo apt update
  sudo apt install dnsutils
  ```

- **CentOS/RHEL:**
  ```bash
  sudo yum install bind-utils
  ```
  Dla nowszych wersji używających `dnf`:
  ```bash
  sudo dnf install bind-utils
  ```

- **Fedora:**
  ```bash
  sudo dnf install bind-utils
  ```

- **Arch Linux:**
  `dig` jest dostępny jako część pakietu `bind-tools`, który można zainstalować za pomocą:
  ```bash
  sudo pacman -S bind-tools
  ```

Podobnie jak inne narzędzia specjalistyczne, `dig` jest niezbędny dla zaawansowanych zadań związanych z DNS, ale może nie być konieczny dla przeciętnego użytkownika lub w standardowej instalacji systemu. Jego instalacja jest jednak prosta i może znacznie ułatwić diagnostykę problemów sieciowych.

### Zadanie 4: Analiza statystyk połączeń sieciowych

- **Stare narzędzie:** `netstat`
  - **Zadanie:** Wyświetl statystyki połączeń sieciowych, w tym połączenia TCP i UDP.
  - **Komenda:** `netstat -tuln` 
  - Sprawdż co daje -p za pomocą man netstat lub netstat --help.

- **Nowe narzędzie:** `ss`
  - **Zadanie:** Wyświetl statystyki połączeń sieciowych, w tym połączenia TCP i UDP.
  - **Komenda:** `ss -tuln`
  - Sprawdż co daje -p za pomocą man ss lub ss --help

Uwaga:

`netstat` jest klasycznym narzędziem do monitorowania połączeń sieciowych, trasowania, interfejsów sieciowych, statystyk interfejsów, masquerading, i wielu innych aspektów sieci. Tradycyjnie było ono dostępne w większości dystrybucji Linuxa jako część pakietu `net-tools`.

Jednakże, w ostatnich latach, wiele dystrybucji Linuxa zaczęło przechodzić na nowsze narzędzia, takie jak `ss` z pakietu `iproute2`, które oferują podobną funkcjonalność, ale są bardziej wydajne i mają nowocześniejszą bazę kodu. W związku z tym, `netstat` i inne narzędzia z pakietu `net-tools` mogą nie być instalowane domyślnie w nowszych wersjach niektórych dystrybucji.

Jeśli odkryjesz, że `netstat` nie jest dostępne na twoim systemie, możesz je zainstalować ręcznie za pomocą menedżera pakietów swojej dystrybucji:

- **Debian/Ubuntu i pochodne:**
  ```bash
  sudo apt update
  sudo apt install net-tools
  ```

- **CentOS/RHEL:**
  ```bash
  sudo yum install net-tools
  ```
  W nowszych wersjach korzystających z `dnf`, użyj:
  ```bash
  sudo dnf install net-tools
  ```

- **Fedora:**
  Fedora również używa `dnf`:
  ```bash
  sudo dnf install net-tools
  ```

- **Arch Linux:**
  ```bash
  sudo pacman -S net-tools
  ```

Pomimo że `netstat` jest nadal używane przez wielu administratorów sieci i deweloperów ze względu na swoją znajomość i wygodę, zaleca się zapoznanie się z narzędziami z pakietu `iproute2`, takimi jak `ss`, które są bardziej aktualne i często oferują lepszą funkcjonalność.

### Zadanie 5: Testowanie przepustowości sieci

- **Narzędzie:** `iperf3`
  - **Zadanie:** Przeprowadź test przepustowości sieci między dwoma hostami.
  - **Komenda:** `iperf3 -s` na serwerze i `iperf3 -c <adres_IP_serwera>` na kliencie.

Uwaga:

Program `iperf3`, nie jest narzędziem dostępnym domyślnie we wszystkich dystrybucjach Linuxa. `iperf3` jest zaawansowanym narzędziem do testowania przepustowości sieci, które pozwala na mierzenie maksymalnej przepustowości TCP i UDP między dwoma punktami w sieci. Z jego pomocą można przeprowadzać różnorodne testy prędkości sieci, co jest szczególnie przydatne w środowiskach profesjonalnych.

Jeśli potrzebujesz `iperf3` na swoim systemie, zazwyczaj musisz go zainstalować ręcznie, korzystając z menedżera pakietów dostępnego w twojej dystrybucji. Oto jak możesz zainstalować `iperf3` w najpopularniejszych dystrybucjach Linuxa:

- **Debian/Ubuntu i pochodne:**
  ```bash
  sudo apt update
  sudo apt install iperf3
  ```

- **CentOS/RHEL:**
  - Dla CentOS/RHEL 7 i nowszych, `iperf3` można zainstalować z domyślnego repozytorium EPEL, które może wymagać wcześniejszej instalacji:
    ```bash
    sudo yum install epel-release
    sudo yum install iperf3
    ```

- **Fedora:**
  ```bash
  sudo dnf install iperf3
  ```

- **Arch Linux:**
  ```bash
  sudo pacman -S iperf3
  ```

Instalacja `iperf3` jest prosta i pozwala szybko rozpocząć testy wydajności sieci. Narzędzie to jest nieocenione podczas diagnozowania problemów z siecią, planowania jej rozbudowy czy też weryfikowania jakości usług świadczonych przez dostawców internetu.

### Zadanie 6: Analiza parametrów karty sieciowej

- **Narzędzie:** `ethtool`
  - **Zadanie:** Wyświetl statystyki i parametry karty sieciowej.
  - **Komenda:** `ethtool <nazwa_interfejsu>`

Uwaga:

`ethtool` jest kolejnym przykładem narzędzia, które nie jest zainstalowane domyślnie we wszystkich dystrybucjach Linuxa. `ethtool` służy do zapytania oraz kontrolowania ustawień sterownika sieci i sprzętu sieciowego. Umożliwia między innymi wyświetlanie i zmianę ustawień prędkości połączenia, auto-negocjacji, a także wyświetlanie statystyk sieciowych interfejsu.

Aby zainstalować `ethtool` w różnych dystrybucjach Linuxa, można użyć następujących poleceń:

- **Debian/Ubuntu i pochodne:**
  ```bash
  sudo apt update
  sudo apt install ethtool
  ```

- **CentOS/RHEL:**
  ```bash
  sudo yum install ethtool
  ```
  Dla nowszych wersji systemów opartych na Red Hat, takich jak RHEL 8 lub CentOS 8, zaleca się używanie `dnf` zamiast `yum`:
  ```bash
  sudo dnf install ethtool
  ```

- **Fedora:**
  ```bash
  sudo dnf install ethtool
  ```

- **Arch Linux:**
  ```bash
  sudo pacman -S ethtool
  ```

`ethtool` jest bardzo przydatnym narzędziem dla administratorów systemów i sieci, umożliwiającym szczegółową analizę i konfigurację interfejsów sieciowych. Pomimo że nie jest dostępne domyślnie, jego instalacja jest prosta i szybka, co pozwala łatwo rozszerzyć możliwości diagnostyczne i konfiguracyjne systemu operacyjnego.

### Zadanie 7: Przeglądanie logów systemowych w kontekście problemów sieciowych

- **Zadanie:** Przejrzyj logi systemowe (np. `/var/log/syslog` na systemach opartych na Debianie) w poszukiwaniu wiadomości związanych z siecią.
- **Komenda:** `grep -i network /var/log/syslog` lub użyj narzędzia `journalctl` na systemach z systemd, np. `journalctl -u NetworkManager`.

### Porównanie narzędzi `deprecated` vs nowe narzędzia

- **ifconfig vs ip**: `ip` oferuje bardziej zintegrowane podejście do zarządzania siecią, pozwalając na łatwiejsze manipulowanie zarówno adresami IP, trasami, jak i regułami polityki routingu.
- **route vs ip route**: Podobnie, `ip route` oferuje bardziej spójne i elastyczne zar

ządzanie trasowaniem w porównaniu do `route`.
- **netstat vs ss**: `ss` jest znacznie szybszy i dostarcza więcej informacji niż `netstat`, szczególnie przy dużej liczbie połączeń.
- **nslookup vs dig**: `dig` oferuje bardziej szczegółowe informacje i większą elastyczność w formacie wyjściowym niż `nslookup`.

Pamiętaj, że efektywna diagnostyka problemów sieciowych często wymaga użycia kombinacji narzędzi, aby uzyskać pełny obraz sytuacji.

---

`Tcpdump` jest niezwykle potężnym narzędziem do przechwytywania i analizy pakietów sieciowych, które pozwala na głęboką diagnostykę problemów sieciowych. Jest ono powszechnie stosowane przez administratorów sieci i bezpieczeństwa do monitorowania ruchu sieciowego na żywo lub do zapisywania ruchu do pliku do późniejszej analizy.

### Zadanie z `tcpdump`

**Zadanie:** Przechwyć wszystkie pakiety przechodzące przez interfejs sieciowy `eth0` i zapisz je do pliku do późniejszej analizy.

- **Komenda:**
  ```bash
  sudo tcpdump -i eth0 -w przechwycone_pakiety.pcap
  ```

**Wariant zadania:** Przefiltruj i wyświetl tylko pakiety HTTP przechodzące przez interfejs sieciowy.

- **Komenda:**
  ```bash
  sudo tcpdump -i eth0 port 80
  ```

`tcpdump` oferuje szeroki zakres opcji i filtrów, które pozwalają na bardzo szczegółową analizę ruchu sieciowego. Można na przykład filtrować pakiety według adresu IP, portu, protokołu i wielu innych kryteriów.

Podobnie jak inne narzędzia do analizy sieci, `tcpdump` może nie być zainstalowane domyślnie we wszystkich dystrybucjach Linuxa, ale jest szeroko dostępne i można je łatwo zainstalować za pomocą menedżera pakietów systemu operacyjnego:

- **Debian/Ubuntu i pochodne:**
  ```bash
  sudo apt update
  sudo apt install tcpdump
  ```

- **CentOS/RHEL/Fedora:**
  ```bash
  sudo yum install tcpdump
  ```
  Lub przy użyciu `dnf`:
  ```bash
  sudo dnf install tcpdump
  ```

- **Arch Linux:**
  ```bash
  sudo pacman -S tcpdump
  ```

Dzięki `tcpdump` można uzyskać wgląd w to, co dokładnie dzieje się w sieci, co jest nieocenione przy diagnozowaniu problemów z połączeniem, ataków sieciowych czy nieoczekiwanego ruchu sieciowego.

---

Konfiguracja połączenia VPN (Virtual Private Network) w systemie Linux może wydawać się skomplikowana, ale postaram się wytłumaczyć to w sposób, który będzie zrozumiały nawet dla ucznia szkoły średniej zainteresowanego technologiami. Podzielę proces na proste kroki, korzystając z przykładu OpenVPN, jednego z najpopularniejszych rozwiązań VPN.

### Krok 1: Instalacja OpenVPN

Najpierw musisz zainstalować OpenVPN na swoim systemie Linux. Możesz to zrobić za pomocą menedżera pakietów dostępnego w twojej dystrybucji. Na przykład, dla systemów bazujących na Debianie (takich jak Ubuntu), użyjesz terminala i wpiszesz:

```bash
sudo apt update
sudo apt install openvpn
```

Dla systemów bazujących na Red Hat (takich jak Fedora lub CentOS), użyjesz:

```bash
sudo dnf install openvpn
```

### Krok 2: Pobierz pliki konfiguracyjne VPN

Aby połączyć się z serwerem VPN, potrzebujesz plików konfiguracyjnych. Zwykle dostarcza je usługodawca VPN. Pobierz te pliki na swoje urządzenie. Mogą mieć rozszerzenie `.ovpn`.

### Krok 3: Ustanowienie połączenia VPN

Po pobraniu plików konfiguracyjnych możesz nawiązać połączenie za pomocą terminala. Przejdź do katalogu, w którym znajdują się pliki konfiguracyjne, a następnie użyj OpenVPN do nawiązania połączenia. Załóżmy, że twój plik konfiguracyjny to `moj-vpn.ovpn`, wtedy komenda wygląda tak:

```bash
sudo openvpn --config moj-vpn.ovpn
```

Wprowadź swoje dane uwierzytelniające, gdy zostaniesz o to poproszony.

### Krok 4: Sprawdź połączenie

Po nawiązaniu połączenia możesz sprawdzić, czy twoje IP zostało zmienione, odwiedzając w przeglądarce stronę typu whatismyip.com lub używając komendy `curl`:

```bash
curl ifconfig.me
```

To pokaże twoje publiczne IP, które powinno teraz odpowiadać lokalizacji serwera VPN.

### Dodatkowe wskazówki

- Jeśli potrzebujesz, aby połączenie VPN uruchamiało się automatycznie przy starcie systemu, możesz skonfigurować OpenVPN do pracy jako usługa systemowa.
- Używaj zawsze zaufanych i bezpiecznych dostawców usług VPN, aby chronić swoją prywatność i bezpieczeństwo online.
- W razie problemów z połączeniem, sprawdź logi OpenVPN oraz upewnij się, że konfiguracja jest poprawna i aktualna.

Pamiętaj, że poszczególne kroki mogą się nieznacznie różnić w zależności od dystrybucji Linuxa i dostawcy VPN. Zawsze warto też zajrzeć do dokumentacji swojego dostawcy VPN oraz dystrybucji Linuxa, aby uzyskać najbardziej aktualne i szczegółowe informacje.