---
title: "Zarządzanie logami Apache2"
date:  2023-04-06T20:30:00+00:00
description: "Zarządzanie logami Apache2"
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
1. Sprawdź access_log
2. Sprawdź error_log
3. Użyj grep do wyszukania specyficznych fraz w logach

<script async id="asciicast-575108" src="https://asciinema.org/a/575108.js"></script>

#### Zarządzanie logami Apache2

Jeśli chcesz wyświetlić i monitorować zapytania o dostęp do strony serwera Apache2 w czasie rzeczywistym, wpisz polecenie:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo tail -f /var/log/apache2/access_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo tail -f /var/log/apache2/access.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo tail -f /etc/httpd/logs/access_log
  sudo tail -f /var/log/httpd/access_log
  ```
  {{< /tab >}}
{{< /tabs >}}

Jeśli chcesz sprawdzić logi błędów Apache2, wpisz polecenie:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo tail -f /var/log/apache2/error_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo tail -f /var/log/apache2/error.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo tail -f /etc/httpd/logs/error_log
  sudo tail -f /var/log/httpd/error_log
  ```
  {{< /tab >}}
{{< /tabs >}}

Możesz ograniczyć liczbę linii do wyświetlenia logów serwera Apache2 (np. 100), używając opcji -n.

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo tail -n 100 /var/log/apache2/access_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo tail -n 100 /var/log/apache2/access.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo tail -n 100 /etc/httpd/logs/error_log
  sudo tail -n 100 /var/log/httpd/error_log
  ```
  {{< /tab >}}
{{< /tabs >}}

Uwaga: Widok logów zaczyna się na końcu linii i jest drukowany na standardowe wyjście.

#### Wyświetlanie określonego terminu z dzienników dostępu

Czasami chcesz wyświetlić tylko określony typ wpisu w dzienniku.  Można użyć polecenia grep do filtrowania raportu według określonych słów kluczowych.

Na przykład wpisz w terminalu następujące dane:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo grep GET /var/log/apache2/access_log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo grep GET /var/log/apache2/access.log
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo grep GET /etc/httpd/logs/access_log
  sudo grep GET /var/log/httpd/access_log
  ```
  {{< /tab >}}
{{< /tabs >}}

Podobnie jak poprzednie polecenie, to patrzy na plik /var/log/apache2/access.log, aby wyświetlić zawartość dziennika dostępu. Polecenie grep mówi maszynie, aby wyświetlała tylko wpisy z żądaniem GET.

Możesz zastąpić również inne frazy. Na przykład, jeśli chcesz monitorować dostęp do obrazów .jpg, możesz zastąpić GET frazą .jpg. Jak poprzednio, użyj rzeczywistej ścieżki do pliku dziennika twojego serwera.

#### Interpretacja logu dostępowego w Apache

Kiedy otwierasz plik dziennika dostępu po raz pierwszy, możesz czuć się przytłoczony.

Jest tam wiele informacji o żądaniach HTTP, a niektóre edytory tekstu (i terminal) zawijają tekst do następnej linii. Może to sprawić, że czytanie będzie dezorientujące, ale każda informacja jest wyświetlana w określonej kolejności.

Konwencjonalną metodą wyrażania formatu plików dziennika dostępu jest:

"%h %l %u %t "%r" %>s %b "%{Referer}i" "%{User-agent}i""

Jest to kod dla najczęściej występujących rzeczy w każdej linii dziennika.

Każdy znak % odpowiada fragmentowi informacji w dzienniku:

* %h - Adres IP klienta (źródło żądania dostępu).
* %l - Ten kolejny wpis może być po prostu myślnikiem - oznacza to, że nie pobrano żadnych informacji. To jest wynik sprawdzenia identd na kliencie.
* %u - Userid klienta, jeżeli żądanie dostępu wymagało uwierzytelnienia http.
* %t - Timestamp przychodzącego żądania.
* %r - Linia żądania, która została użyta. Mówi o metodzie http (GET, POST, HEAD, itd.), ścieżce do tego, co zostało zażądane, oraz o używanym protokole http.
* %>s - Kod stanu, który został zwrócony z serwera do klienta.
* %b - Rozmiar zasobu, który został zażądany.
* "%{Referer}i" - To mówi ci, czy dostęp przyszedł przez kliknięcie linku na innej stronie, lub inne sposoby, w jakie klient został skierowany na twoją stronę.
* "%{User-agent}i" - Mówi o informacji o podmiocie dokonującym żądania, takim jak przeglądarka internetowa, system operacyjny, źródło strony (w przypadku robota), itp.

Po prostu przeczytaj w poprzek linii w swoim pliku dziennika, a każdy wpis może zostać zdekodowany jak powyżej. Jeśli nie ma żadnych informacji, w dzienniku pojawi się myślnik. Jeśli pracujesz na wstępnie skonfigurowanym serwerze, twój plik dziennika może mieć więcej lub mniej informacji. Możesz również utworzyć niestandardowy format dziennika za pomocą modułu dziennika niestandardowego.

Więcej informacji na temat dekodowania formatów dzienników można znaleźć na tej stronie.

#### Jak wykorzystać dane z plików logów Apache

Analiza logów Apache daje możliwość zmierzenia sposobu, w jaki klienci wchodzą w interakcje z Twoją witryną.

Na przykład, możesz spojrzeć na znacznik czasu, aby dowiedzieć się ile żądań dostępu przychodzi na godzinę, aby zmierzyć wzorce ruchu. Możesz spojrzeć na agenta użytkownika, aby dowiedzieć się, czy poszczególni użytkownicy logują się na stronie, aby uzyskać dostęp do bazy danych lub tworzyć treści. Możesz nawet śledzić nieudane uwierzytelnienia, aby monitorować różne rodzaje ataków cybernetycznych na twój system.

Dziennik błędów apache może być używany podobnie. Często jest on po prostu używany do sprawdzenia, ile błędów 404 jest generowanych. Błąd 404 występuje, gdy klient żąda brakującego zasobu, a to może ostrzegać o uszkodzonych linkach lub innych błędach na stronie. Jednakże, może być również używany do znalezienia błędów w konfiguracji lub nawet ostrzeżeń o potencjalnych problemach z serwerem.

#### Wnioski

W tym przewodniku przedstawiono metody wyodrębniania danych do przeglądania plików dziennika dostępu Apache.

Plik access.log jest doskonałym źródłem informacji na temat sposobów interakcji klientów z serwerem. Plik error.log może pomóc Ci w rozwiązywaniu problemów z Twoją witryną.