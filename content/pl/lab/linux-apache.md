---
title: "Konfiguracja Apache w systemie GNU/Linux"
date:  2023-04-13T15:17:00+00:00
description: "Konfiguracja Apache w systemie GNU/Linux."
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
image: images/2023-thumbs/apache2.webp
---
#### Ćwiczenia do wykonania:
1. Zainstaluj apache na serwerze.
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

Zadanie 1:
<script async id="asciicast-577321" src="https://asciinema.org/a/577321.js"></script>
Jako dokumentację wykonaj zrzut ekranu lub przekierowanie stdout uruchomionych poleceń do plików tekstowych (wykorzystaj script).
<script async id="asciicast-577292" src="https://asciinema.org/a/577292.js"></script>
