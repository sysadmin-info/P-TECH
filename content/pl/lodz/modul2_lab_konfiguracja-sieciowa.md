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
* Skonfiguruj połączenie VPN.
* Użyj narzędzia `tcpdump` do analizy ruchu sieciowego.
* Użyj narzędzi: `ifconfig`, `netstat`, `ss`, `ip`, `ethtool`, `iperf3`. Obejrzyj poniższy film, aby zobaczyć, w jaki sposób używać tych narzędzi.

{{< youtube fc8wMXoX8Lw >}}
<figcaption>Rozwiązywanie problemów z wolną komunikacją sieciową lub przekroczeniem limitu czasu połączenia w systemie Linux</figcaption>