---
title: "Moduł 2 - Zaawansowane zarządzanie systemem i dokumentacja techniczna  - teoria"
date:  2024-02-08T14:30:00+00:00
description: "Moduł 2 - Zaawansowane zarządzanie systemem i dokumentacja techniczna  - teoria"
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
## Część Teoretyczna
### Moduł 2: Zaawansowane zarządzanie systemem i dokumentacja techniczna - teoria
#### Czas Trwania: 15 minut

### 1. **Analiza oprogramowania w GNU/Linux**

Sporządzanie wykazu zainstalowanego oprogramowania w systemie jako dobra praktyka administratora. Aby sporządzić wykaz zainstalowanego oprogramowania w systemie Linux, uczniowie mogą użyć kilku narzędzi dostępnych w większości dystrybucji. Oto niektóre z nich:

- dpkg - na dystrybucjach opartych na Debianie (takich jak Ubuntu):
Komenda: `dpkg -l`
Ta komenda wyświetli listę wszystkich zainstalowanych pakietów w systemie.

- apt - również na dystrybucjach opartych na Debianie:
Komenda: `apt list --installed`
Podobnie jak `dpkg -l`, ale może dostarczać dodatkowych informacji i jest często bardziej przyjazna dla użytkownika.

- rpm - na dystrybucjach opartych na RPM (takich jak Fedora, CentOS):
Komenda: `rpm -qa`
Wyświetla listę wszystkich zainstalowanych pakietów RPM.

- yum - starsze wersje dystrybucji opartych na RPM:
Komenda: `yum list installed`
Ta komenda wyświetli zainstalowane pakiety zarządzane przez yum.

- dnf - nowsze wersje dystrybucji opartych na RPM (np. Fedora):
Komenda: `dnf list installed`
Podobnie jak `yum`, ale dla nowszego menedżera pakietów.

- zypper - na dystrybucjach openSUSE:
Komenda: `zypper se --installed-only`
Wyświetla tylko zainstalowane pakiety.

- pacman - na dystrybucjach Arch Linux:
Komenda: `pacman -Q`
Lista zainstalowanych pakietów w systemie Arch.

- eopkg - na dystrybucjach Solus:
Komenda: `eopkg list-installed`
Wyświetla zainstalowane pakiety w systemie Solus.

- flatpak - dla aplikacji zainstalowanych jako Flatpaks:
Komenda: `flatpak list`
Wyświetla listę zainstalowanych aplikacji Flatpak.

- snap - dla aplikacji zainstalowanych jako Snaps:
Komenda: `snap list`
Pokazuje zainstalowane pakiety snap.

Po uzyskaniu listy, uczniowie można przekierować wynik do pliku tekstowego za pomocą przekierowania wyjścia, np. `dpkg -l > zainstalowane-pakiety.txt`, aby stworzyć dokumentację zainstalowanego oprogramowania. Jest to przydatna praktyka administratora, która pozwala na szybkie zorientowanie się w zainstalowanym oprogramowaniu i może służyć jako punkt odniesienia w przypadku przywracania systemu lub rozwiązywania problemów.

Analiza stanu systemu komputerowego za pomocą dostępnych narzędzi w Linux i sporządzanie raportu zawierającego spis urządzeń wraz z ich specyfikacją.

Dodatkowo:

[Pomiar układu wejścia/wyjścia](https://sysadmin.info.pl/pl/blog/pomiar-ukladu-wejscia-wyjscia/)
[Monitorowanie wykorzystania zasobów systemu Linux](https://sysadmin.info.pl/pl/blog/monitorowanie-wykorzystania-zasobow-systemu-linux/)


### 2. **Zaawansowane zarządzanie systemem i dokumentacja techniczna**

##### Praktyczne ćwiczenia z monitorowania stanu systemu.

Monitorowanie zasobów systemowych przy użyciu `top`, `htop` (jeśli dostępne) oraz `dmesg`.

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

* Co to jest load average?

Load average w systemach operacyjnych typu Unix, takich jak Linux, to miara obciążenia systemu w danym okresie czasu. Jest to średnia ilość procesów czekających na wykonanie lub w stanie wykonywania na procesorze. Load average jest zazwyczaj przedstawiane jako trzy liczby odpowiadające średniemu obciążeniu systemu w ciągu ostatnich 1, 5 i 15 minut.

Load average jest miarą obciążenia systemu, która uwzględnia procesy znajdujące się w kolejce do CPU oraz procesy aktualnie wykonywane przez CPU. Oto szczegółowe wyjaśnienie tych dwóch aspektów:

1. **Procesy czekające na wykonanie (w kolejce):** Są to procesy, które są gotowe do wykonania, ale muszą czekać, ponieważ CPU jest zajęte innymi procesami. Oznacza to, że te procesy są w stanie "runnable", czyli gotowe do uruchomienia, ale nie zostały jeszcze przypisane do procesora.

2. **Procesy w stanie wykonywania:** Są to procesy, które aktualnie korzystają z CPU. Obejmuje to procesy, które faktycznie są przetwarzane przez procesor (w stanie "running") oraz procesy, które są tymczasowo zatrzymane (w stanie "sleeping"), ponieważ czekają na zakończenie jakiejś operacji wejścia-wyjścia, takiej jak odczyt z dysku twardego lub komunikacja przez sieć.

Load average agreguje te dwa rodzaje procesów i przedstawia je jako jedną liczbę dla okresów 1, 5 i 15 minut. Oto jak można to zrozumieć w praktyce:

- **Load average < 1.00 na jednordzeniowym procesorze:** Oznacza, że procesor nie jest w pełni wykorzystany i nie ma procesów oczekujących na wykonanie.
- **Load average = 1.00 na jednordzeniowym procesorze:** Oznacza, że procesor jest wykorzystywany w 100%, ale bez nadmiaru procesów czekających.
- **Load average > 1.00 na jednordzeniowym procesorze:** Wskazuje, że procesy muszą czekać na wykonanie, ponieważ jest więcej pracy, niż procesor może obsłużyć w danym momencie. 

Dla systemu wielordzeniowego, wartości load average należy interpretować w kontekście liczby rdzeni. Na przykład, na systemie z 4 rdzeniami, load average wynoszący 4.00 oznacza pełne wykorzystanie wszystkich rdzeni.

Podsumowując, load average daje wgląd w to, ile pracy ma system do wykonania i czy zasoby CPU są wystarczające do obsługi obciążenia. Wartości powyżej liczby rdzeni procesora przez dłuższe okresy czasu mogą wskazywać na konieczność optymalizacji lub dodania zasobów.

Aby zmierzyć load average za pomocą narzędzia `top`, wystarczy uruchomić `top` w terminalu. Po uruchomieniu, na górze ekranu wyświetlane są różne statystyki dotyczące systemu, w tym load average. Przykładowo, linia może wyglądać tak:

```bash
top - 15:20:43 up  1:22,  2 users,  load average: 0.25, 0.35, 0.33
```

W tym przypadku `0.25, 0.35, 0.33` to właśnie średnie obciążenie systemu w ciągu ostatnich 1, 5 i 15 minut. Interpretacja tych wartości może się różnić w zależności od liczby rdzeni procesora w systemie. Na przykład, load average `1.00` na jednordzeniowym procesorze oznacza, że procesor jest wykorzystywany w 100%. Natomiast na systemie z 4 rdzeniami, wartość `1.00` oznacza wykorzystanie około 25% mocy obliczeniowej.

W kontekście monitorowania, load average może pomóc określić, czy system jest przeciążony i czy potrzeba więcej zasobów lub optymalizacji. Wartości wyższe niż liczba dostępnych rdzeni procesora przez dłuższy czas mogą wskazywać na przeciążenie systemu.

##### Wprowadzenie do tworzenia dokumentacji technicznej: praktyczne zastosowanie narzędzi do dokumentacji.

1. Tworzenie dokumentacji technicznej na przykładzie Confluence.
2. Instalacja Confluence (pokaz z mojej strony).
3. Utworzenie prostego dokumentu. 
4. Uczniowie utworzą dokumentację w dowolnym edytorze tekstu na swoim komputerze. Zadanie do wykonania jest opisane w części praktycznej.

