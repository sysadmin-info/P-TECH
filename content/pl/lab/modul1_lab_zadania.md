---
title: "Podstawy pracy w systemie Linux - zadania"
date:  2024-02-07T15:30:00+00:00
description: "Podstawy pracy w systemie Linux - zadania"
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: false
asciinema: true
tags:
- Docker
series:
- Docker
categories:
- Docker
image: images/2023-thumbs/docker.webp
---
## Część Praktyczna
### Moduł 1: Podstawy pracy w systemie Linux
#### Czas Trwania: 45 minut

- **Zadania:**
      1. Tworzenie użytkownika `mario` z określonymi grupami pomocniczymi i powłoką.
      2. Zmiana powłoki użytkownika, ustawienie hasła, i konfiguracja wymuszenia zmiany hasła.
      3. Utworzenie, modyfikacja uprawnień, i zarządzanie dostępem do pliku `report.txt`.
      4. Praca z linkami symbolicznymi i twardymi, oraz zarządzanie systemem plików za pomocą `ln`, `find`, `chattr`.

      ### Przykładowe zadania do częsci praktycznej:

**Zarządzanie użytkownikami:**

1. Załóż jednym poleceniem (nie interaktywnie!) użytkownika o nazwie ‘mario’. Spraw, aby jego główną grupą użytkownika była ‘mushroom‘, a grupy pomocnicze to ‘adm’ oraz ‘audio’. Użytkownik mario ma mieć powłokę ustawioną na /bin/sh.
Podpowiedź: man useradd

2. Spraw, aby każdy nowo założony użytkownik w systemie miał w swoim katalogu plik ‘rules.txt’ z jakimś krótkim tekstem w środku. Podpowiedź: odpowiedni parametr do useradd + katalog tzw. szkieletu (skel)

3. Zmień użytkownikowi mario powłokę na /usr/bin/vim (to nie jest poprawny shell! Musisz to jakoś obejść). Gdy Ci się uda, zmień mu powłokę na /bin/bash, aby dało się na tym użytkowniku nadal pracować.

Podpowiedź: narzędzie do zmiany shella (jedno polecenie) + lista dozwolonych powłok w /etc/

4. Ustaw użytkownikowi ‘mario’ hasło ‘coins100’, ale w sposób nieinteraktywny, za pomocą jednego polecenia.
Podpowiedź: echo + polecenie do zmiany hasła (ale nie passwd, bo ono jest interaktywne!).

5. Wykonaj polecenie ‘whoami’ jako mario, ale będąc zalogowanym jako root.
Podpowiedź: sudo

6. Zmień (jednym poleceniem) podstawową grupę użytkownika ‘mario’ na ‘players’. Jeśli jest taka potrzeba, to przy okazji utwórz taką grupę.
Podpowiedź: usermod

7. Wymuś na użytkowniku ‘mario’ regularną zmianę hasła co 7 dni (jednym poleceniem).
Podpowiedź: chage

8. Zablokuj konto ‘mario’ tak, aby nie dało się na niego zalogować (nie chodzi o zmianę hasła, ani usunięcie konta), a później ponownie odblokuj tego użytkownika.
Podpowiedź: passwd lub chage

9. Spraw, aby nowo zakładani użytkownicy mieli automatycznie przypisywane numery ID od 8000 w górę.
Podpowiedź: /etc/login.defs

10. Spraw, aby mario po zalogowaniu się na swoje konto zobaczył aktualny uptime i load na serwerze (zakładamy, że mario używa basha)

Podpowiedź: polecenie uptime + pliki ~/.bash_profile lub ~/.bashrc (poczytaj o różnicach!).

11. Spraw, aby użytkownik ‘mario’ mógł uruchomić maksymalnie 5 procesów
jednocześnie.

Podpowiedź: /etc/security/limits.conf