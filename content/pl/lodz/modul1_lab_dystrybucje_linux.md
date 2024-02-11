---
title: "Moduł 1 - Dystrybucje Linux - zadania"
date:  2024-02-07T15:30:00+00:00
description: "Moduł 1 - Dystrybucje Linux - zadania"
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
- dystrybucje Linux
image: images/2024-thumbs/dystrybucje-linux.webp
---
## Część Praktyczna
### Moduł 1: Dystrybucje Linux - zadania
#### Czas Trwania: 10 minut

#### 1. **Przygotowanie bootowalnego pendrive i instalacja systemu (10 minut):**
   📌 Demonstracja tworzenia bootowalnego nośnika. 
      ✅ Rufus. Instrukcja: [https://rufus.ie/pl/](https://rufus.ie/pl/)
      ✅ Balena Etcher [https://etcher.balena.io/](https://etcher.balena.io/)
      ✅ Rozpoczęcie procesu instalacji systemu Linux.

   📌Jako ciekawostka:
      ✅ [Ventoy](https://www.ventoy.net/)
      ✅ IODD ST400 - koszt samego urządzenia wynosi około 500 PLN. Do tego należy doliczyć osobno cenę dysku. Nie jest to tanie rozwiązanie, ale dla osób nazywanych `distro hoppers` lub specjalistów, którzy używają zawodowo takich rozwiązań - koszt urządzenia nie ma znaczenia. W przypadku firmy można wrzucić to sobie w koszty. Przydaje się to w sytuacji, gdy mamy kolejne wydania jakiejś dystrybucji i chcemy testować instalacje różnych wersji tej samej dystrybucji na różnych serwerach fizycznych. 

#### 2. **Dla chętnych - darmowy serwer ssh.**

📌Projekt FROG to darmowa oferta małych (malutkich!) serwerów VPS przeznaczonych do nauki administracji serwerami, hostingu prostych aplikacji (np. checki, crony) i hostowania niewielkich stron WWW. Serwery są darmowe, ale wymagają wpłaty dowolnej kwoty (np. 5zł) w ramach weryfikacji tożsamości użytkownika. Jest to opłata jednorazowa. Możesz posiadać tylko JEDEN darmowy serwer w usłudze FROG. 🐸 [Frog](https://frog.mikr.us/)

#### 3.  **Chcesz się uczyć chmury (cloud), ale zastanawiasz się jak zacząć?**

   ✅ Przede wszystkim, pamiętaj o wersjach trial. Każdy, znaczący dostawca chmury oferuje na start konkretną kwotę, którą możesz wykorzystać, by za darmo sprawdzić podstawowe funkcjonalności. Nie ma zatem problemu, by w ramach wersji trial uruchomić serwer lub wybraną usługę i "pobawić się" ustawieniami.

   ✅ Na dzień dzisiejszy, oferta trialowa Microsoft Azure obejmuje $200 kredytu, które możesz wykorzystać w dowolny sposób przez pierwsze 30 dni od momentu rejestracji. Po wykorzystaniu, będziesz płacić tylko za to, co przekracza darmowe limity poszczególnych usług. Microsoft Azure oferuje również szereg usług, które są darmowe przez pierwszy rok lub przez 750 godzin użytkowania, w zależności od tego, co nastąpi wcześniej.

   ✅ Google Cloud Platform w skrócie GCP oferuje 90-dniowy darmowy okres próbny z kredytem w wysokości $300

   ✅ AWS udostępnia 12-miesięczny okres próbny z różnymi darmowymi poziomami usług, w tym t2.micro instancję serwera ogólnego przeznaczenia.

   ✅ Jak już uruchomisz wersję trial to pamiętaj o darmowych tutorialach, które oferuje każdy z dostawców chmury. Z tymi poradnikami będzie Ci łatwiej wystartować.

#### 4. **Jeśli nie chumra, to może własny Home Lab?**

📌 Hardware, czyli to, co ważne. Liczy się każda kilowatogodzina. Zatem szukamy rozwiązań energooszczędnych.

   ✅ Raspberry Pi 4 lub 5. Można zbudować własny klaster Kubernetes. Polecam K3S, gdyż wspiera procesory ARM i bez problemu można go zainstalować. Szczegóły znajdziecie na [mojej stronie](https://sysadmin.info.pl). Energooszczędne rozwiązanie. Plus ma przewagę nad innymi ze względu na porty GPIO i możliwość nauki mikroelektroniki. Jeśli kogoś interesuje mikroelektronika, to polecam zainteresować się ESP32 oraz Arduino. Są to znacznie tańsze rozwiązania i pozwalają na naukę IoT bez ponoszenia wielkich wydatków.

   ✅ DELL WYSE 5070 
      Terminal wyposażony w procesor Intel jest określany jako najlepsze i najbardziej energooszczędne rozwiązania przy zachowaniu stosunkowo dobrej ceny i możliwości, a jednocześnie nie zrujnuje rachunkami za energię elektryczną.

   ✅ [Porównanie dwóch powyższych rozwiązań](https://browser.geekbench.com/v5/cpu/compare/9792492?baseline=8704648)

   ✅ HP T630 
      Ma dwa dodatkowe sloty m.2 w porównaniu do DELL WYSE 5070. Jest nieco tańszy od DELL WYSE 5070 i wydaje się lepszym rozwiązaniem ze względu na wspomniane sloty. 

   ✅ Fujitsu ESPRIMO Q920 
      Cena zbliżona do DELL WYSE 5070. 

   ✅ Intel NUC
      Cena zbliżona do DELL WYSE 5070.

   ✅ Jakikolwiek sensowny thin-client lub coś zbliżonego do Intel NUC, lub Raspberry Pi.    

Podsumowanie: Oczywiście są wersje dużo droższe. Wszystko zależy od budżetu. Tu chodzi o coś, co będzie w stanie pracować 24h na dobę, nie będzie hałasować i zużycie prądu zamknie się w kosztach ~ 200 PLN lub mniej rocznie.