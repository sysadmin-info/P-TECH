---
title: "Moduł 2 - Zaawansowane zarządzanie systemem i dokumentacja techniczna  - zadania"
date:  2024-02-08T14:30:00+00:00
description: "Moduł 2 - Zaawansowane zarządzanie systemem i dokumentacja techniczna  - zadania"
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
## Część Praktyczna
### Moduł 2: Zaawansowane zarządzanie systemem i dokumentacja techniczna - zadania
#### Czas Trwania: 10 minut

#### 1. **Praktyczne ćwiczenia z monitorowania stanu systemu**

- **Ćwiczenie:** Monitorowanie zasobów systemowych przy użyciu `top`, `htop` (jeśli dostępne) oraz `dmesg`.
  1. Uruchom `top` lub `htop` i zidentyfikuj proces zużywający najwięcej zasobów CPU.
  2. Użyj `dmesg` do sprawdzenia najnowszych wiadomości kernela.

##### Zadania z monitorowania stanu systemu (5 minut)

**Cel:** Naucz się używać narzędzi do monitorowania zasobów systemowych i wiadomości kernela.
**Czas:** 15 minut
**Wymagania:**
* Komputer z systemem Linux
* Dostęp do terminala

**Ćwiczenie:**
1. Uruchom terminal.
2. Uruchom narzędzie `top` lub `htop` (jeśli dostępne) do monitorowania procesów:
    * `top`
    * `htop`
3. Zidentyfikuj proces, który zużywa najwięcej zasobów CPU.
4. Użyj `dmesg` do sprawdzenia najnowszych wiadomości kernela:

```bash
dmesg
```

**Dodatkowe informacje:**
* Dokumentacja narzędzia `htop`: [https://hisham.hm/htop/](https://hisham.hm/htop/)

**Pytania do dyskusji:**
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

**Zadania rozszerzające:**

* Zainstaluj i skonfiguruj narzędzie do monitorowania serwera, takie jak `Nagios` lub `Zabbix`.
* Użyj skryptu do automatycznego monitorowania zasobów systemowych i wysyłania alertów w przypadku problemów.
* Wygeneruj raport z analizą wydajności systemu.

#### 2. **Praktyczne ćwiczenia z tworzenia dokumentracji technicznej**

##### Wprowadzenie do tworzenia dokumentacji technicznej (5 minut)

- **Ćwiczenie:** Utworzenie prostej dokumentacji technicznej.
  1. Użyj Markdown lub innego edytora tekstu do stworzenia dokumentu opisującego wykonane kroki w ćwiczeniach z LVM.
  2. Zawrzyj opis kroków, użyte komendy oraz zrzuty ekranu (jeśli możliwe).
  3. Sporządź wykaz zainstalowanego oprogramowania w systemie.

  Aby sporządzić wykaz zainstalowanego oprogramowania w systemie Linux, uczniowie mogą użyć kilku narzędzi dostępnych w większości dystrybucji. Oto niektóre z nich:

1. **dpkg** - na dystrybucjach opartych na Debianie (takich jak Ubuntu):
   - Komenda: `dpkg -l`
   - Ta komenda wyświetli listę wszystkich zainstalowanych pakietów w systemie.

2. **apt** - również na dystrybucjach opartych na Debianie:
   - Komenda: `apt list --installed`
   - Podobnie jak `dpkg -l`, ale może dostarczać dodatkowych informacji i jest często bardziej przyjazna dla użytkownika.

3. **rpm** - na dystrybucjach opartych na RPM (takich jak Fedora, CentOS):
   - Komenda: `rpm -qa`
   - Wyświetla listę wszystkich zainstalowanych pakietów RPM.

4. **yum** - starsze wersje dystrybucji opartych na RPM:
   - Komenda: `yum list installed`
   - Ta komenda wyświetli zainstalowane pakiety zarządzane przez yum.

5. **dnf** - nowsze wersje dystrybucji opartych na RPM (np. Fedora):
   - Komenda: `dnf list installed`
   - Podobnie jak `yum`, ale dla nowszego menedżera pakietów.

6. **zypper** - na dystrybucjach openSUSE:
   - Komenda: `zypper se --installed-only`
   - Wyświetla tylko zainstalowane pakiety.

7. **pacman** - na dystrybucjach Arch Linux:
   - Komenda: `pacman -Q`
   - Lista zainstalowanych pakietów w systemie Arch.

8. **eopkg** - na dystrybucjach Solus:
   - Komenda: `eopkg list-installed`
   - Wyświetla zainstalowane pakiety w systemie Solus.

9. **flatpak** - dla aplikacji zainstalowanych jako Flatpaks:
   - Komenda: `flatpak list`
   - Wyświetla listę zainstalowanych aplikacji Flatpak.

10. **snap** - dla aplikacji zainstalowanych jako Snaps:
    - Komenda: `snap list`
    - Pokazuje zainstalowane pakiety snap.

Po uzyskaniu listy, uczniowie mogą przekierować wynik do pliku tekstowego za pomocą przekierowania wyjścia, np. `dpkg -l > zainstalowane-pakiety.txt`, aby stworzyć dokumentację zainstalowanego oprogramowania. Jest to przydatna praktyka administratora, która pozwala na szybkie zorientowanie się w zainstalowanym oprogramowaniu i może służyć jako punkt odniesienia w przypadku przywracania systemu lub rozwiązywania problemów.

Te ćwiczenia mają na celu nie tylko wprowadzenie w praktyczne aspekty zarządzania systemem Linux, ale również rozwijanie umiejętności niezbędnych do efektywnego rozwiązywania problemów i dokumentowania pracy technicznej.