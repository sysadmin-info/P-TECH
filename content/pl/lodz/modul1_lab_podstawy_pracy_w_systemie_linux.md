---
title: "Moduł 1 - Podstawy pracy w systemie Linux - zadania"
date:  2024-02-07T15:30:00+00:00
description: "Moduł 1 - Podstawy pracy w systemie Linux - zadania"
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
- Podstawy pracy w systemie Linux
image: images/2024-thumbs/podstawy_pracy_w_systemie_linux.webp
---
## Część Praktyczna
### Moduł 1: Podstawy pracy w systemie Linux - zadania
#### Czas Trwania: 25 minut

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

**Zarządzanie plikami i katalogami:**

Wykonanie poniższej listy zadań sprawi, że lepiej poznasz zasadę zarządzania plikami w Linuksie.

Założenia wstępne: w systemie posiadasz tylko trzech użytkowników:

– mario - jest w grupie ‘brothers’
– luigi - jest w grupie ‘brothers’ oraz ‘helpers’
– peach - jest w grupie ‘princess’

1. Załóż pusty plik o nazwie ‘report.txt’. Użytkownicy luigi i mario mogą czytać jego zawartość.
Użytkownik mario może także pisać do niego, a peach nie ma do niego dostępu.
Podpowiedź: chmod + chown

2. Spraw, aby do pliku ‘logs.txt’ dało się tylko dopisywać nowe dane na końcu i aby mogli robić to tylko luigi i mario.
Podpowiedź: chmod + chown + chattr

3. Plik o nazwie ‘config.yaml’ ma być zdatny do odczytania przez wszystkich użytkowników, ale NIKT nie może go usunąć. Nawet jego właściciel.
Podpowiedź: chattr

4. Wszyscy użytkownicy mogą zakładać pliki w katalogu /tmp/data/, ale pomimo tego, że każdy ma tam dostęp, to tylko właścicielom wolno usuwać swoje pliki i zmieniać ich nazwy (i to nawet gdyby plik miał chmod 777!).
Podpowiedź: sticky bit

5. Spraw, aby pliki “first.txt” oraz “second.txt” miały dokładnie taką samą zawartość, a zmiana tekstu w jednym automatycznie powodowała zmianę tekstu w drugim z plików. Zmiana praw dostępu (chmod) do jednego z plików automatycznie zmienia te same prawa na drugim pliku (widoczne przez ls -l).
Podpowiedź: komenda ‘ln’

6. Stwórz plik, który ma dokładnie 100MB. Zrób to jednym poleceniem.
Podpowiedź: polecenie ‘truncate’ lub ‘dd’ (w ramach nauki wypróbuj oba)

7. Utwórz plik ‘elders.txt’ w taki sposób, aby polecenie ‘ls -l’ pokazywało, że został
on założony 1 stycznia 1999 roku.
Podpowiedź: touch

8. W katalogu masz kilkaset plików z rozszerzeniem TXT. Zmień każdemu z nich rozszerzenie na DOC. Zrób to jednym poleceniem, bez pętli.
Podpowiedź: rename

9. Jesteś w katalogu, w którym są tysiące plików. Usuń te, których rozmiar jest większy niż 1MB, a nazwa zaczyna się na literę ‘b’. Zrób to jednym poleceniem.
Podpowiedź: find

10. W katalogu masz tysiące plików. Musisz usunąć wszystkie, które nie zawierają litery ‘x’ w nazwie. Nie używaj do tego pętli (for/while).
Podpowiedź: find z negacją (prostsze) / ls + grep z xargs

11. W katalogu masz dziesiątki plików. Stwórz paczkę ‘package.tgz’ (tar+gzip) zawierającą jedynie pliki większe niż 1MB i do tego mające rozszerzenie txt.
Podpowiedź: tar + find (być może trzeba będzie użyć subshella lub pipe)