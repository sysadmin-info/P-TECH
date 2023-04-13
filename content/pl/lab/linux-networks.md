---
title: "Konfiguracja sieci w systemie GNU/Linux"
date:  2023-04-13T13:35:00+00:00
description: "Konfiguracja sieci w systemie GNU/Linux. Podstawowa konfiguracja routera z systemem openWRT. Wykorzystanie narzędzi yast, nmtui, nmcli, nmap. Lokalizacja plików konfiguracyjnych."
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
asciinema: true
tags:
- P-TECH
series:
-
categories:
- 
image: images/2023-thumbs/network.webp
---
#### Ćwiczenia do wykonania:
1. Skonfiguruj router według zaleceń:
* adres IP interfejsu LAN: 10.10.10.1
* adres bramy (GW - gateway) 10.10.10.1
* maska 24-bitowa: 255.255.255.0
* DNS: 10.10.0.100
2. Skonfiguruj interfejsy sieciowe serwera w systemie Linux i stacji roboczej w systemie Linux:
* na serwerze skonfiguruj interfejs sieciowy podłączony do routera:
- adres IP: 10.10.10.2/24
- brama domyślna: 10.10.10.1
- serwer DNS: 10.10.10.1
* na stacji roboczej skonfiguruj interfejs sieci bezprzewodowej:
- adres IP: 10.10.10.3/24
- brama domyślna: 10.10.10.1
- serwer DNS: 10.10.10.1
3. Wykonaj test komunikacji serwera z routerem, routera z serwerem i stacją roboczą.
4. Przeprowadź na serwerze w systemie Linux diagnostykę podzespołów i systemu: 
* Za pomocą dostępnych narzędzi systemowych sprawdź parametry systemu operacyjnego oraz pamięci RAM.
5. Zainstaluj apache nba serwerze.
* W katalogu /srv/www utwórz plik o nazwie index.html z zawartością:

```
<html>
  <body>
    <p>Strona testowa</p>
  </body>
</html>
```

* ustaw prawa do katalogu /www na 555
* ustaw prawa 444 do pliku index.html
* z konfiguracji serwera HTTP odczytaj użytkownika i grupę, na prawach których działa serwer HTTP
* ustaw właściciela i grupę, na prawach których działa serwer HTTP
-- dla katalogu /www
-- dla pliku index.html
* zmień port, na którym działa serwer HTTP na 8080
* zmień lokalizację głównej witryny Web na /www
* sprawdź na stacji roboczej, czy przy użyciu adresu IP interfejsu WAN rutera wyświetla się udostępniona witryna

Zadanie 1 i 2:
<script async id="asciicast-577289" src="https://asciinema.org/a/577289.js"></script>
Zadanie 3:
<script async id="asciicast-577291" src="https://asciinema.org/a/577291.js"></script>
Zadanie 4:
<script async id="asciicast-577290" src="https://asciinema.org/a/577290.js"></script>
Zadanie 5:
<script async id="asciicast-577321" src="https://asciinema.org/a/577321.js"></script>
Jako dokumentację wykonaj zrzut ekranu lub przekierowanie stdout uruchomionych poleceń do plików tekstowych so oraz ram (wykorzystaj script).
<script async id="asciicast-577292" src="https://asciinema.org/a/577292.js"></script>
