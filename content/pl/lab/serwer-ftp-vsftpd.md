---
title: "Serwer FTP - Vsftpd"
date:  2023-04-21T10:30:00+00:00
description: "Zainstaluj Vsftpd, aby skonfigurować serwer FTP."
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
image: images/2023-thumbs/vsftpd.webp
---
#### Ćwiczenia do wykonania:
1. Zainstaluj Vsftpd.
2. Włącz i uruchom Vsftpd
3. Dodaj port do firewalld

<script async id="asciicast-580161" src="https://asciinema.org/a/580161.js"></script>

#### Zainstaluj Vsftpd

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować Vsftpd wpisz:
  ```
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj Vsftpd
  sudo zypper -n in vsftpd
  # włącz Vsftpd przy starcie systemu
  sudo systemctl enable vsftpd
  # uruchom Vsftpd
  sudo systemctl start vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować Vsftpd wpisz:
  ```
  # odśwież repozytoria
  sudo apt update
  # zainstaluj sftpd
  sudo apt -y install vsftpd
  # włącz Vsftpd przy starcie systemu
  sudo systemctl enable vsftpd
  # uruchom Vsftpd
  sudo systemctl start vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować Vsftpd wpisz:
  ```
  # zainstaluj Vsftpd
  sudo yum install vsftpd -y
  or
  sudo dnf install vsftpd -y
  # włącz Vsftpd przy starcie systemu
  sudo systemctl enable vsftpd
  # uruchom Vsftpd
  sudo systemctl start vsftpd
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Zezwól na usługę Vsftpd

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  linux:~ # sudo firewall-cmd --add-service=ftp --permanent
  linux:~ # sudo firewall-cmd --add-port=21000-21010/tcp --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo ufw allow 'FTP'
  lub
  sudo ufw allow 'Vsftpd'
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  linux:~ # sudo firewall-cmd --add-service=ftp --permanent
  linux:~ # sudo firewall-cmd --add-port=21000-21010/tcp --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Zmodyfikuj konfigurację Vsftpd dla openSUSE/SLES

```
sudo vim /etc/vsftpd.conf
# linia 19: zmień
write_enable=YES
# linia 36: odkomentuj
ls_recurse_enable=YES
# linia 53: odkomentuj (Pozwól lokalnym użytkownikom zalogować się do FTP, jeśli są na liście użytkowników)
local_enable=YES
# linie 62,63: odkomentuj ( włącz chroot )
chroot_local_user=NO
chroot_list_enable=YES
# linia 65: odkomentuj ( plik z listą chroot )
chroot_list_file=/etc/vsftpd.chroot_list
# linia 80: zmień (żadnego anonymous)
anonymous_enable=NO
# linie 171,172: odkomentuj ( zezwól na ascii mode )
ascii_upload_enable=YES
ascii_download_enable=YES
# linia 184: zmień wedle potrzeb (jeśli vsftpd ma nasłuchiwać połączeń tylko za pomocą protokołu IPv4)
listen=YES
# linia 189: zmień wedle potrzeb (jeśli vsftpw ma nasłuchiwać połączeń także za pomocą protokołu IPv6)
listen_ipv6=NO
# linia 217: odkomentuj (wyłącz filtr seccomp)
seccomp_sandbox=NO

# dodaj na końcu pliku

# używaj czasu lokalnego
use_localtime=YES

# ogranicz użytkowników FTP do ich katalogu domowego i zezwól im na zapisywanie plików tylko tam
allow_writeable_chroot=YES
```

#### Dodaj użytkowników, którym zezwolisz na przejście do ich katalogu domowego

```
sudo vim  /etc/vsftpd.chroot_list
add 
suse
```

#### Jeśli Firewalld jest uruchomiony, zezwól na usługę FTP.

```
sudo vim /etc/vsftpd.conf
# zmień porty 30000 i 31000 na te poniższe
# dodaj porty PASV, aby umożliwić dostęp do FTP za pomocą PASV
pasv_enable=YES
pasv_min_port=21000
pasv_max_port=21010
```

#### Dodaj użytkowników

```
sudo useradd -d /srv/www/ftp1 ftp1
sudo passwd ftp1

sudo useradd -d /srv/www/ftp2 ftp2
sudo passwd ftp2
```

#### Skonfiguruj vsftpd, by korzystał z nowo utworzonych użytkowników

```
sudo vim /etc/vsftpd.conf

# Włącz listę użytkowników
userlist_enable=YES

# Skonfiguruj listę użytkowników, aby działała jako biała lista (zezwalaj tylko na użytkowników, którzy są tam wymienieni) 
userlist_deny=NO

# Plik z listą użytkowników
userlist_file=/etc/vsftpd.userlist
 
# Zezwalaj użytkownikom wirtualnym na korzystanie z tych samych uprawnień co użytkownikom lokalnym 
virtual_use_local_privs=YES
 
# Ustaw katalog konfiguracyjny dla użytkowników wirtualnych 
user_config_dir=/etc/vsftpd_user_config_dir/
```

{{< notice success "WAŻNE" >}}
Staraj się unikać duplikatów ustawień: jeśli niektóre z powyższych ustawień są już obecne w twoim pliku vsftpd.conf albo je wykomentuj, albo usuń, w przeciwnym razie usługa VSFTPD nie będzie mogła się uruchomić.

Powyższe opcje są dość oczywiste: w zasadzie mówimy VSFTP, aby zezwolił na dostęp do FTP tylko lokalnym użytkownikom, których umieścimy w pliku user_list, pobierając ich konfigurację z katalogu /etc/vsftpd_user_config_dir
{{< /notice >}}

Otwórzmy teraz plik /etc/vsftpd/user_list i dodajmy użytkowników ftp1 i ftp2 w następujący sposób:

```
sudo vim /etc/vsftpd.userlist

# dodaj poniższych użytkowników
ftp1
ftp2
```

#### Konfiguracja folderów domowych

Teraz, gdy zezwoliliśmy tym dwóm użytkownikom na dostęp do naszego serwera FTP (i zamknęliśmy go dla wszystkich innych), ostatnią rzeczą, którą musimy zrobić, jest skonfigurowanie ich folderów domowych.

Aby to zrobić, utwórz folder /etc/vsftpd/user_config_dir/ i stwórz dwa pliki o dokładnie takich samych nazwach, jak dwóch użytkowników:

```
mkdir -p /etc/vsftpd_user_config_dir/
touch /etc/vsftpd_user_config_dir/ftp1
touch /etc/vsftpd_user_config_dir/ftp2
```

Zaraz po tym edytuj plik ftp1 w następujący sposób:

```
sudo vim /etc/vsftpd_user_config_dir/ftp1
local_root=/srv/www/ftp1
write_enable=YES
```

Po wykonaniu tej czynności, zrób to samo z plikiem ftp2, określając inny folder domowy:

```
sudo vim /etc/vsftpd_user_config_dir/ftp2
local_root=/srv/www/ftp2
write_enable=YES
```

Następnie utwórz powyższe katalogi:

```
sudo mkdir -p /srv/www/{ftp1,ftp2}
```

A także nadaj im uprawnienia:

```
sudo chown -R ftp1:users /srv/www/ftp1
sudo chown -R ftp2:users /srv/www/ftp2
```

Zrestartuj Vsftpd.

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  ```
  sudo systemctl restart vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  ```
  sudo systemctl restart vsftpd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  ```
  sudo systemctl restart vsftpd
  ```
  {{< /tab >}}
{{< /tabs >}}

Teraz możesz stworzyć osobne, dedykowane katalogi domowe dla każdego z użytkowników FTP.

{{< notice success "WAŻNE" >}}
Pamiętaj, aby dodać certyfikat SSL do swojego serwera VSFTP, aby lepiej go zabezpieczyć, a także ochronić przed złośliwymi próbami kradzieży Twoich cennych danych!
{{< /notice >}}

Dla pewności poniżej konfiguracja, która jest przetestowana i działa. Jeszcze bez SSL. Konfiguracja SSL będzie opisana osobno.

```
# Example config file /etc/vsftpd.conf
#
# The default compiled in settings are fairly paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
# Please see vsftpd.conf.5 for all compiled in defaults.
#
# If you do not change anything here you will have a minimum setup for an
# anonymus FTP server.
#
# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
# capabilities.
#
# ################
# General Settings
# ################
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# You may fully customise the login banner string:
#ftpd_banner=Welcome to blah FTP service.
#
# You may activate the "-R" option to the builtin ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
#ls_recurse_enable=YES
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_file=/etc/vsftpd.banned_emails
#
# If  enabled,  all  user  and  group  information in
# directory listings will be displayed as "ftp".
#hide_ids=YES
#
# #######################
# Local FTP user Settings
# #######################
#
# Uncomment this to allow local users to log in.
local_enable=YES
#
# Default umask for local users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
#local_umask=022
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
chroot_local_user=NO
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd.chroot_list
#
# Performs chroot with original (non-root) credentials. This is usefull on nfs with squash_root,
# where root becomes nobody and would need -x access.
#allow_root_squashed_chroot=YES
#
# The maximum data transfer rate permitted, in bytes per second, for
# local authenticated users. The default is 0 (unlimited).
#local_max_rate=7200
#
# ##########################
# Anonymus FTP user Settings
# ##########################
#
# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
anonymous_enable=NO
#
# The maximum data transfer rate permitted, in bytes per second, for anonymous
# authenticated users. The default is 0 (unlimited).
#anon_max_rate=7200
#
# Anonymous users will only be allowed to download files which are
# world readable.
anon_world_readable_only=YES
#
# Default umask for anonymus users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
#anon_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
#
# Uncomment this to enable anonymus FTP users to perform other write operations
# like deletion and renaming.
#anon_other_write_enable=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using "root" for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# ############
# Log Settings
# ############
#
# Log to the syslog daemon instead of using an logfile.
syslog_enable=NO
#
# Uncomment this to log all FTP requests and responses.
log_ftp_protocol=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# You may override where the log file goes if you like. The default is shown
# below.
#
vsftpd_log_file=/var/log/vsftpd.log
#
# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
xferlog_std_format=YES
#
# You may override where the log file goes if you like. The default is shown
# below.
xferlog_file=/var/log/vsftpd.log
#
# Enable this to have booth logfiles. Standard xferlog and vsftpd's own style log.
dual_log_enable=YES
#
# Uncomment this to enable session status information in the system process listing.
setproctitle_enable=YES
#
# #################
# Transfer Settings
# #################
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# Enable this and the server will recognise asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below options to have the server actually do ASCII
# mangling on files when in ASCII mode.
# Beware that on some FTP servers, ASCII support allows a denial of service
# attack (DoS) via the command "SIZE /big/file" in ASCII mode. vsftpd
# predicted this attack and has always been safe, reporting the size of the
# raw file.
# ASCII mangling is a horrible feature of the protocol.
#ascii_upload_enable=YES
#ascii_download_enable=YES
#
# Set to NO if you want to disallow the  PASV  method of obtaining a data
# connection.
pasv_enable=YES
#
# PAM setting. Do NOT change this unless you know what you do!
pam_service_name=vsftpd
#
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=YES
#
# This directive enables listening on IPv6 sockets. To listen on IPv4 and IPv6
# sockets, you must run two copies of vsftpd with two configuration files.
# Make sure, that one of the listen options is commented !!
listen_ipv6=NO
#
# Set "ssl_enable=YES" to enable SSL support and configure the location of
# your local certificate (RSA, DSA, or both). Note that vsftpd won't start
# if either of the "xxx_cert_file" options sets a path that doesn't exist.
ssl_enable=NO
rsa_cert_file=
dsa_cert_file=
#
# Limit passive ports to this range to assis firewalling
pasv_min_port=21000
pasv_max_port=21010

### security features that are incompatible with some other settings. ###

# isolate_network ensures the vsftpd subprocess is started in own network
# namespace (see CLONE_NEWNET in clone(2)). It however disables the
# authentication methods needs the network access (LDAP, NIS, ...).
#isolate_network=NO

# seccomp_sanbox add an aditional security layer limiting the number of a
# syscalls can be performed via vsftpd. However it might happen that a
# whitelist don't allow a legitimate call (usually indirectly triggered by
# third-party library like pam, or openssl) and the process is being killed by kernel.
#
# Therefor if your server dies on common situations (file download, upload),
# uncomment following line and don't forget to open  bug at
# https://bugzilla.novell.com
seccomp_sandbox=NO

# specify root directory if need
# if not specify, users' home directory become FTP home directory

# use local time
use_localtime=YES

# Enable the userlist
userlist_enable=YES

# Configure the userlist to act as a whitelist (only allow users who are listed there)
userlist_deny=NO

# Userlist file
userlist_file=/etc/vsftpd.userlist

# Allow virtual users to use the same privileges as local users
virtual_use_local_privs=YES

# Setup the virtual users config folder
user_config_dir=/etc/vsftpd_user_config_dir/

#restrict FTP users to their /home directory and allow them to write there
allow_writeable_chroot=YES
```
