---
title: "Instalacja i konfiguracja certyfikatu SSL za pomocą Let's Encrypt w serwerze Apache"
date:  2023-04-15T10:00:00+00:00
description: "Instalacja i konfiguracja certyfikatu SSL za pomocą Let's Encrypt w serwerze Apache"
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
1. Stwórz plik wirtualnego hosta dla http (port 80)
2. Zainstaluj/włącz mod ssl
3. Stwórz plik wirtualnego hosta dla https (port 443)

{{< notice success "Uprawnienia DocumentRoot" >}}
##### openSUSE Leap/SLES 15.x
Domyślnie w openSUSE Leap, katalog DocumentRoot /srv/www/htdocs i katalog CGI /srv/www/cgi-bin należą do użytkownika i grupy root. Nie należy zmieniać tych uprawnień. Jeśli katalogi są zapisywalne dla wszystkich, każdy użytkownik może umieszczać w nich pliki. Pliki te mogą być następnie wykonywane przez Apache z uprawnieniami wwwrun, co może dać użytkownikowi niezamierzony dostęp do zasobów systemu plików. 

###### Debian / Ubuntu / Red Hat / Fedora 
Użyj podkatalogów /srv/www lub /var/www (zależnie od dystrybucji) do umieszczenia katalogów DocumentRoot i CGI dla twoich wirtualnych hostów i upewnij się, że katalogi i pliki należą do użytkownika i grupy root. 
{{< /notice >}}

{{< notice success "Dostęp do systemu plików" >}}
Domyślnie w pliku /etc/apache2/httpd.conf zabroniony jest dostęp do całego systemu plików. Nie powinieneś nigdy nadpisywać tych dyrektyw, ale specjalnie umożliwić dostęp do wszystkich katalogów, które Apache powinien móc czytać. Szczegóły w sekcji 24.2.2.1.3, "Podstawowa konfiguracja hosta wirtualnego". Upewnij się przy tym, że żadne krytyczne pliki, takie jak hasła czy pliki konfiguracyjne systemu, nie mogą być odczytane z zewnątrz.
{{< /notice >}}

#### Konfiguracja wirtualnego hosta

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ##### SLES
  Katalog konfiguracyjny hosta wirtualnego zawiera szablon /etc/apache2/vhosts.d/vhost-ssl.template z dyrektywami specyficznymi dla SSL, które są obszernie udokumentowane. Patrz [Sekcja 24.2.2.1, "Konfiguracja hosta wirtualnego"](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-apache2.html#sec-apache2-configuration-manually-vhost), aby zapoznać się z ogólną konfiguracją hosta wirtualnego.

  Aby rozpocząć, skopiuj szablon do /etc/apache2/vhosts.d/MYSSL-HOST.conf i edytuj go. Dostosowanie wartości dla następujących dyrektyw powinno być wystarczające:

  * DocumentRoot
  * ServerName
  * ServerAdmin
  * ErrorLog
  * TransferLog

  ```
  sudo cp /etc/apache2/vhosts.d/vhost-ssl.template /etc/apache2/vhosts.d/strona.com.pl.conf
  ```
  {{< /tab >}}
  {{< tab >}}
  ####### Debian
  W przypadku Debian tworzymy plik wirtualnego hosta dla http (port 80) za pomocą poniższego polecenia:

  ```
  sudo vi /etc/apache2/sites-available/strona.com.pl.conf
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Red Hat
  W przypadku Red Hat tworzymy plik wirtualnego hosta dla http (port 80) za pomocą poniższego polecenia:

  ```
  sudo vi /etc/httpd/conf.d/strona.com.pl.conf
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Przykładowa konfiguracja wirtualnego hosta (port 80, czyli http) dla Debian / Ubuntu / Red Hat / Fedora

```
<VirtualHost *:80>
   ServerName strona.com.pl
   ServerAlias www.strona.com.pl
   DocumentRoot /var/www/strona.com.pl/public_html
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

{{< boxmd >}}
Wyjaśnienie: 

Staraj się utrzymywać logikę w katalogu z wirtualnymi hostami i twórz pliki konfiguracyjne wirtualnych hostów w postaci nazwa-domeny.conf
{{< /boxmd >}}


{{< notice success "W systemie Debian dla Apache musimy jeszcze włączyć stronę." >}}

```
sudo a2ensite strona.com.pl.conf
```
Co spowoduje stworzenie dowiązania symbolicznego w katalogu /etc/apache2/sites-enabled.
{{< /notice >}}

### Tworzenie fizycznej struktury i wgranie strony na serwer.

Teraz należy stworzyć katalog dla strony w katalogu /srv/www lub /var/www

```
sudo -i
```

(wpisz hasło użytkownika root)

```
cd /srv/www/
lub 
cd /var/www
sudo mkdir strona.com.pl
```

{{< boxmd >}}
Wyjaśnienie:

W openSUSE/SLES katalog DocumentRoot jest ustawiony jak wspomniano wcześniej na /srv/www/htdocs i można go zmienić na /srv/www w pliku /etc/apache2/default-server.conf, co moim zdaniem jest bardziej eleganckie i dużo bardziej logiczne. Poza tym podczas instalacji systemu, lub, gdy mamy wolumeny logiczne, można ustawić /srv jako osobną partycję/wolumen logiczny. 

W Debian/Ubuntu/Red Hat/Fedora natomiast jest to katalog /var/www
{{< /boxmd >}}


{{< notice warning "Uwaga" >}}
Ustaw użytkownika serwera WWW, <em><strong>www-data</strong></em>, jako właściciela katalogu domowego swojej witryny. <em><strong>www-data</strong></em> jest grupą. W przypadku CentOS będzie to grupa <em><strong>apache</strong></em>. Natomiast w przypadku openSUSE/SLES będzie to użytkownik <em><strong>root</strong></em> i grupa <em><strong>root</strong></em>. Uprawnienia w openSUSE/SLES dla katalogu www możemy nadać (naprawić) za pomocą poniższej komendy:

```
sudo chown -R root:root /srv/www
```

A następnie zrestartować apache.

```
sudo systemctl restart apache2.service
```
{{< /notice >}}

##### Zmiana właściciela i grupy dla katalogu strony


{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ##### SLES
  ```
  sudo chown -R root:root /srv/www/example.com.pl/
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Debian
  ```
  sudo chown -R www-data:www-data /var/www/example.com.pl/
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Red Hat
  ```
  sudo chown -R apache:apache /var/www/example.com.pl/
  ```
  {{< /tab >}}
{{< /tabs >}}


#### Aktywacja modułu mod_ssl w systemach linuksowych:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ##### SLES
  ```
  sudo a2enmod ssl
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Debian
  ```
  sudo a2enmod ssl
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Red Hat
  ```
  sudo yum install mod_ssl
  lub
  sudo dnf install mod_ssl
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Instalacja i konfiguracja certyfikatu SSL za pomocą Let&#8217;s Encrypt.

{{< box >}}
Wyjaśnienie: komunikacja pomiędzy serwerem Cloudflare a serwerem, na którym jest strona, musi być szyfrowana. 
{{< /box >}}

Wykorzystamy do tego stronę <https://certbot.eff.org>

Z rozwijanej listy Software wybieramy Apache, system operacyjny, to albo Ubuntu 16.04, albo Debian 9, albo CentOS/RHEL 7 i postępujemy zgodnie ze wskazówkami.

Wybierz stronę bez www, lub z www, jak tobie pasuje, ponieważ certbot nam rozpozna wirtualny host dla http, który utworzony został wcześniej. 

Nie włączaj przekierowania z http na https, ponieważ to zrobisz po stronie Cloudflare. Inaczej napotkasz błąd. Dlatego wybierz 1 , gdy zapyta o redirect.

Certbot zainstaluje automatycznie certyfikat, utworzy plik wirtualnego hosta. 


{{< notice success "Uwaga" >}}

W przypadku Debian / Ubuntu należy wejść do katalogu sites-available i włączyć dowiazanie symboliczne:

``` 
sudo -i
cd /etc/apache2/sites-available
ls -al
a2ensite strona.com.pl-le-ssl.conf
```
{{< /notice >}}

Polecam zmodyfikować plik wirtualnego hosta dla https, aby ostatecznie wyglądał tak:


{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ##### SLES
  W przypadku openSUSE / SLES tworzymy plik wirtualnego hosta dla http (port 443) za pomocą poniższego polecenia:
  ```
  sudo vi /etc/apache2/vhosts.d/strona.com-le-ssl.conf
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Debian
  W przypadku Debian tworzymy plik wirtualnego hosta dla http (port 443) za pomocą poniższego polecenia:

  ```
  sudo vi /etc/apache2/sites-available/strona.com.pl-le-ssl.conf
  ```
  {{< /tab >}}
  {{< tab >}}
  ##### Red Hat
  W przypadku Red Hat tworzymy plik wirtualnego hosta dla http (port 443) za pomocą poniższego polecenia:

  ```
  sudo vi /etc/httpd/conf.d/strona.com.pl-le-ssl.conf
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Przykładowa konfiguracja wirtualnego hosta (port 443, czyli https) dla Debian / Ubuntu / Red Hat / Fedora

```
<IfModule mod_ssl.c>
 SSLStaplingCache shmcb:/run/httpd/ssl_stapling(32768)
  <VirtualHost *:443>
   Header always set Strict-Transport-Security "max-age=15768000"
   SSLEngine on
   ServerName strona.com.pl
   ServerAlias www.strona.com.pl
   DocumentRoot /var/www/strona.com.pl/public_html
   LogLevel debug
   ErrorLog /var/log/httpd/error.log
   CustomLog /var/log/httpd/access.log combined

    <Directory /var/www/strona.com.pl/public_html>
     Options Indexes FollowSymLinks Includes IncludesNOEXEC SymLinksIfOwnerMatch                     
     AllowOverride All
     Require all granted
     DirectoryIndex index.php
     RewriteEngine On
    </Directory>

Include /etc/letsencrypt/options-ssl-apache.conf
SSLUseStapling on
SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
SSLCipherSuite HIGH:!aNULL:!MD5
SSLCipherSuite ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AE$
SSLHonorCipherOrder on
SSLCompression off
SSLSessionTickets off

    <FilesMatch "^\.ht">
       Require all denied
    </FilesMatch>

    <files readme.html>
       order allow,deny
       deny from all
    </files>

SSLCertificateFile /etc/letsencrypt/live/strona.com.pl/cert.pem
SSLCertificateKeyFile /etc/letsencrypt/live/strona.com.pl/privkey.pem
SSLCertificateChainFile /etc/letsencrypt/live/strona.com.pl/chain.pem

 </VirtualHost>
</IfModule>
```

[Dokumetacja openSUSE](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-apache2.html#sec-apache2-ssl)