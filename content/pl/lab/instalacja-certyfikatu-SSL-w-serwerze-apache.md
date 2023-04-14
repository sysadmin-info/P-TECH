---
title: "Instalacja certyfikatu SSL w serwerze Apache"
date:  2023-04-07T11:15:00+00:00
description: "Instalacja certyfikatu SSL w serwerze Apache"
draft: true
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
1. Zainstaluj/włącz mod ssl
2. 
3. 

<!--<script async id="asciicast-575108" src="https://asciinema.org/a/575108.js"></script>-->

#### Instalacja Apache'a i aktywacja modułu mod_ssl w systemach linuksowych:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo a2enmod ssl
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo a2enmod ssl
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo yum install mod_ssl
  lub
  sudo dnf install mod_ssl
  ```
  {{< /tab >}}
{{< /tabs >}}

### Konfiguracja wirtualnego hosta

{{< tabs CentOS Debian >}}
  {{< tab >}}

  W przypadku CentOS tworzymy plik wirtualnego hosta dla http (port 80) za pomocą poniższego polecenia:

  ```
  sudo vi /etc/httpd/conf.d/strona.com.pl.conf
  ```

  {{< /tab >}}
  {{< tab >}}

  Natomiast w przypadku Debian

  ```
  sudo vi /etc/apache2/sites-available/strona.com.pl.conf
  ```
  {{< /tab >}}
{{< /tabs >}}

```
<VirtualHost *:80>
   ServerName strona.com.pl
   ServerAlias www.strona.com.pl
   DocumentRoot /var/www/html/strona.com.pl/public_html
   ErrorLog /var/log/httpd/error.log
   CustomLog /var/log/httpd/access.log combined
   #ErrorLog /var/log/apache2/error.log # Debian/Ubuntu
   #CustomLog /var/log/apache2/access.log combined # Debian/Ubuntu
   DirectoryIndex index.php

   LogLevel info warn

   <FilesMatch "^\.ht">
       Require all denied
   </FilesMatch>

   <files readme.html>
       order allow,deny
       deny from all
   </files>
</VirtualHost>
```

Dla Debian/Apache musimy jeszcze włączyć stronę

```
sudo a2ensite strona.com.pl.conf
```

Co spowoduje stworzenie dowiązania symbolicznego w katalogu /etc/apache2/sites-enabled.

### Tworzenie fizycznej struktury i wgranie WordPress na serwer.

Teraz należy stworzyć katalog dla strony w katalogu /var/www/html

```
sudo -i
```

(wpisz hasło użytkownika, którego utworzyłeś na samym początku)

```
cd /var/www/html
sudo mkdir strona.com.pl
```

Utwórz katalog o nazwie src w katalogu swojej witryny, aby przechowywać nowe kopie plików źródłowych WordPress. W tym przewodniku jako przykład wykorzystano katalog domowy /var/www/html/strona.com.pl/. Przejdź do tego nowego katalogu:

```
sudo mkdir -p /var/www/html/strona.com.pl/src/
cd /var/www/html/strona.com.pl/src/
```

Ustaw użytkownika serwera WWW, <em><strong>www-data</strong></em>, jako właściciela katalogu domowego swojej witryny. <em><strong>www-data</strong></em> jest grupą. W przypadku CentOS będzie to grupa <em><strong>apache</strong></em>.

{{< tabs CentOS Debian >}}
  {{< tab >}}

  ### CentOS section

  ```
  sudo chown -R apache:apache /var/www/html/example.com.pl/
  ```

  {{< /tab >}}
  {{< tab >}}

  ### Debian section

  ```
  sudo chown -R www-data:www-data /var/www/html/example.com.pl/
  ```
  {{< /tab >}}
{{< /tabs >}}

### Zainstaluj certyfikat
