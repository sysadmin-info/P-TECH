---
title: "Moduł 1 - Konfiguracja poinstalacyjna - zadania"
date:  2024-02-07T16:30:00+00:00
description: "Moduł 1 - Konfiguracja poinstalacyjna - zadania"
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
- konfiguracja poinstalacyjna
image: images/2024-thumbs/podstawy_pracy_w_systemie_linux.webp
---
## Część Praktyczna
### Moduł 1: Konfiguracja poinstalacyjna - zadania
#### Czas Trwania: 10 minut

### **Konfiguracja serwera SSH: instalacja, generowanie kluczy RSA.**

#### Ćwiczenia do wykonania:
1. Wygeneruj parę kluczy RSA za pomocą ssh-keygen
2. Wyeksportuj klucz publiczny z klienta do serwera za pomocą ssh-copy-id
3. Zaloguj się za pomocą hasła poprzez ssh do serwera i przełącz na konto root za pomocą komendy sudo - su lub sudo -i
4. Włącz logowanie kluczami i wyłącz logowanie hasłem. Zapisz zmiany i zrestartuj usługę ssh.
5. Nie zamykaj bieżącej sesji. Otwórz nową sesję ssh i zaloguj się do serwera za pomocą klucza prywatnego. 
6. Jeśli udało ci się zalogować, zabezpiecz serwer korzystając z poniższych informacji a następnie zrestartuj usługę ssh na drugiej sesji.
7. Pamiętaj, by pierwszą sesję ssh cały czas mieć otwartą, by w razie potrzeby móc cofnąć zmiany.
8. Zrestartuj usługę ssh i sprawdź, czy możesz zalogować się za pomocą trzeciej sesji do serwera. Jeśli tak, udało ci się poprawnie skonfigurować serwer ssh.
9. Dla chętnych napisz skrypt z użyciem sed lub awk, który dokona zmian po stronie serwera w pliku sshd_config, aby nie trzeba było ręcznie nanosić zmian.

<script async id="asciicast-574590" src="https://asciinema.org/a/574590.js"></script>

#### OpenSSH : KeyBoard-Intereractive Auth

OpenSSH jest już domyślnie zainstalowany, więc nie ma potrzeby instalowania nowych pakietów. Domyślnie możesz logować się za pomocą KeyBoard-Interactive Authentication, ale zmień niektóre ustawienia dla bezpieczeństwa jak poniżej.

Jeśli OpenSSH jednak nie jest jeszcze zainstalowany możesz go zainstalować za pomocą następującego polecenia:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować OpenSSH wpisz:
```bash
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj OpenSSH
  sudo zypper -n in openssh
  # włącz OpenSSH podczas boot-owania
  sudo systemctl enable sshd
  # wystartuj openSSH
  sudo systemctl start sshd
  # włącz regułę w firewalld dla ssh
  sudo firewall-cmd --permanent --add-service=ssh
  success
  # Przeładuj reguły firewalld
  sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować OpenSSH wpisz:
```bash
  # odśwież repozytoria
  sudo apt update
  # zainstaluj OpenSSH
  sudo apt -y install openssh-server
  # włącz OpenSSH podczas boot-owania
  sudo systemctl enable sshd
  # wystartuj OpenSSH
  sudo systemctl start sshd
  # włącz regułę w ufw firewall dla ssh
  sudo ufw allow ssh
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować OpenSSH wpisz:
```bash
  sudo yum install openssh-server -y
  lub
  sudo dnf install openssh-server -y
  # włącz OpenSSH podczas boot-owania
  sudo systemctl enable sshd
  # wystartuj OpenSSH
  sudo systemctl start sshd
  # włącz regułę w firewalld dla ssh
  sudo firewall-cmd --permanent --add-service=ssh
  success
  # Przeładuj reguły firewalld
  sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
{{< /tabs >}}

Następnie na maszynie z Linux, za pomocą której zamierzasz łączyć się do serwera, musisz zainstalować odpowiedniego klienta:

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować OpenSSH wpisz:
```bash
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj OpenSSH
  sudo zypper -n in openssh-clients
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować OpenSSH wpisz:
```bash
  # odśwież repozytoria
  sudo apt update
  # zainstaluj OpenSSH
  sudo apt -y install openssh-client
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować OpenSSH wpisz:
```bash
  sudo yum install openssh-clients -y
  lub
  sudo dnf install openssh-clients -y
  ```
  {{< /tab >}}
{{< /tabs >}}

#### Instalacja firewalld

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  Aby zainstalować firewalld wpisz:
```bash
  # odśwież repozytoria
  sudo zypper ref
  # zainstaluj firewalld
  sudo zypper -n in firewalld
  # włącz firewalld podczas boot-owania
  sudo systemctl enable firewalld
  # wystartuj firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  Aby zainstalować firewalld wpisz:
```bash
  # odśwież repozytoria
  sudo apt update
  # zainstaluj firewalld
  sudo apt -y install firewalld
  # włącz firewalld podczas boot-owania
  sudo systemctl enable firewalld
  # wystartuj firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  Aby zainstalować firewalld wpisz:
```bash
  sudo yum install firewalld -y
  lub
  sudo dnf install firewalld -y
  # włącz firewalld podczas boot-owania
  sudo systemctl enable firewalld
  # wystartuj firewalld
  sudo systemctl start firewalld
  ```
  {{< /tab >}}
{{< /tabs >}}

Domyślnie firewalld po instalacji ma zaimplementowaną usługę SSH jako dozwoloną. Jeśli nie, zawsze możesz zezwolić na usługę SSH.

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
```bash
  linux:~ # sudo firewall-cmd --add-service=ssh --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian
```bash
  sudo ufw allow ssh
```
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
```bash
  linux:~ # sudo firewall-cmd --add-service=ssh --permanent
  success
  linux:~ # sudo firewall-cmd --reload
  success
```
  {{< /tab >}}
{{< /tabs >}}

#### Konfiguracja klienta SSH 

Połącz się z serwerem SSH za pomocą zwykłego użytkownika.

```bash
# ssh [login_user@hostname_or_IP_address]
adrian@client:~> ssh adrian@example.com
The authenticity of host 'example.com (10.0.0.50)' can't be established.
ECDSA key fingerprint is SHA256:h0QhlXgCZ860UjM8sAjY6Wmrr2EqSIY5UADBi0wAFV4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'example.com,10.0.0.50' (ECDSA) to the list of known hosts.
Password:          # login user's password
adrian@example.com:~>    # just logined
```

#### Uwierzytelnianie parą kluczy SSH

Skonfiguruj serwer SSH do logowania za pomocą Key-Pair Authentication. Utwórz klucz prywatny dla klienta i klucz publiczny dla serwera, aby to zrobić.

Utwórz Key-Pair dla każdego użytkownika, więc zaloguj się wspólnym użytkownikiem na SSH Server Host i pracuj jak poniżej.

```bash
# utwórz parę kluczy na kliencie
ssh-keygen -t rsa -b 4096 -C "imię i nazwisko"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/adrian/.ssh/id_rsa): /home/adrian/.ssh/p-tech
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/adrian/.ssh/p-tech
Your public key has been saved in /home/adrian/.ssh/p-tech.pub
The key fingerprint is:
SHA256:IPtApVZ/8o6mCY3lKSvcfEtkD6wzHJ0LzKeHFm3qbxs adrian@G02PLXN05963
The key's randomart image is:
+---[RSA 4096]----+
|      o          |
|     + .         |
|    = . o .      |
|   = * o +       |
|    O % S .      |
|   . ^ = o       |
| . o& E + .      |
|  oooOo=         |
|   .o+*o         |
+----[SHA256]-----+
```

Aby wygenerować passphrase możesz użyć następującego polecenia w osobnym oknie CLI
```bash
hexdump -vn16 -e'4/4 "%08X" 1 "\n"' /dev/urandom
```

Wylistuj parę kluczy

```bash
adrian@linux:~> ll ~/.ssh/p-tech*
-rw------- 1 adrian adrian 3.4K Apr  1 16:44 /home/adrian/.ssh/p-tech
-rw-r--r-- 1 adrian adrian  745 Apr  1 16:44 /home/adrian/.ssh/p-tech.pub
```

Skopiuj klucz publiczny z klienta na serwer

```bash
ssh-copy-id -i ~/.ssh/p-tech.pub student@IP-ADDRRESS
```

Podaj hasło

Zaloguj się z kluczem do serwera

```bash
ssh -i ~/.ssh/p-tech student@IP-ADDRRESS
```

Podaj passphrase

#### Automatyzacja

Dodaj poniższe wpisy do pliku .bashrc lub .zshrc znajdującego się w katalogu /home/user. Pierwszy wpis uruchamia agenta ssh, a drugi ładuje do niego Twój klucz prywatny. Jeśli ustawiłeś passphrase na swoim kluczu, agent zapyta o jego wpisanie. Możesz dodać więcej niż jeden klucz. Należy pamiętać, że za każdym razem, gdy Bash lub Zsh uruchomi proces restartu lub rozruchu systemu operacyjnego, w CLI poprosi o podanie passphrase.

```bash
eval $(ssh-agent -s)
ssh-add ~/.ssh/p-tech
```

#### Zabezpieczanie SSH

Edytuj /etc/ssh/sshd_config

```bash
sudo vi /etc/ssh/sshd_config
```

```vim
# odkomentuj te linie i zmień na [no]
PasswordAuthentication no
ChallengeResponseAuthentication no

# Wyłącz puste hasła
# Musisz zapobiec zdalnym logowaniom z kont z pustymi hasłami dla zwiększenia bezpieczeństwa.

PermitEmptyPasswords no

# Ograniczenie dostępu użytkowników do SSH
# Aby zapewnić kolejną warstwę bezpieczeństwa, powinieneś ograniczyć logowanie do SSH
# tylko do niektórych użytkowników, którzy potrzebują zdalnego dostępu.
# W ten sposób zminimalizujesz wpływ posiadania użytkownika ze słabym hasłem.
# Dodaj linię "AllowUsers", a następnie listę nazw użytkowników i oddziel je spacją:

AllowUsers student adrian

# Wyłączanie logowania roota
# Jedną z najbardziej niebezpiecznych dziur w zabezpieczeniach, 
# jakie możesz mieć w swoim systemie jest umożliwienie bezpośredniego logowania się 
# do roota przez SSH. W ten sposób hakerzy próbujący złamać hasło roota mogą
# hipotetycznie uzyskać dostęp do systemu; a jeśli się nad tym zastanowić,
# root może wyrządzić dużo więcej szkód na maszynie niż zwykły użytkownik.
# Aby wyłączyć logowanie przez SSH jako root, zmień linię na taką:

PermitRootLogin no

# Ostatecznie możesz pozwolić rootowi na logowanie się przez SSH przy użyciu pary kluczy.
# Zrób to tylko jeśli serwer nie jest w DMZ (nie ma dostępu z Internetu)

PermitRootLogin prohibit-password

# Dodaj Protocol 2
# SSH posiada dwa protokoły, których może używać. Protokół 1 jest starszy i mniej bezpieczny.
# Protokół 2 jest tym, czego powinieneś używać, aby wzmocnić swoje bezpieczeństwo.
# Jeśli chcesz, aby Twój serwer był zgodny z PCI, musisz wyłączyć protokół 1.

Protocol 2

# Protocol
#  Określa wersje protokołu, które obsługuje sshd(8).  Możliwe.
#  wartości to '1' i '2'.  Wiele wersji musi być oddzielonych przecinkami.
#  Domyślnie jest to '2'.  Protokół 1 cierpi na szereg
#  słabości kryptograficznych i nie powinien być używany.
#  Jest oferowany tylko w celu wsparcia starszych urządzeń.
#  Przykład: Protocol 2, 1

# Użyj innego portu
# Jedną z głównych korzyści ze zmiany portu i użycia niestandardowego portu
# jest uniknięcie bycia widzianym przez przypadkowe skanowanie. Zdecydowana większość hakerów
# szukających otwartych serwerów SSH będzie szukała portu 22, ponieważ domyślnie,
# SSH nasłuchuje połączeń przychodzących na tym porcie.
# Jeśli trudniej jest zeskanować Twój serwer SSH, to zmniejszają się Twoje szanse na atak.
# Uruchom SSH na niestandardowym porcie powyżej portu 1024.

Port 2025

# Możesz wybrać dowolny nieużywany port, o ile nie jest on używany przez inną usługę.
# Wiele osób może wybrać 222 lub 2222 jako swój port, ponieważ
# jest to dość łatwe do zapamiętania, ale właśnie z tego powodu, hakerzy skanujący port 22
# prawdopodobnie będą również próbować portów 222 i 2222. Spróbuj wybrać numer portu
# który nie jest jeszcze używany, podążaj za tym linkiem, aby uzyskać listę numerów portów i ich znanych usług.

# Jeśli StrictModes jest ustawiony na tak, to wymagane są poniższe uprawnienia.
# sudo chmod 700 ~/.ssh
# sudo chmod 600 ~/.ssh/authorized_keys

StrictModes yes

# Konfiguracja interwału czasu bezczynności

ClientAliveInterval 360
ClientAliveCountMax 1

# ClientAliveInterval - Ustawia interwał czasowy w sekundach, po którym, jeśli nie otrzymano żadnych danych od klienta, 
# sshd wyśle wiadomość przez kanał szyfrowany, aby zażądać odpowiedzi od klienta. Domyślnie jest to 0, co oznacza, 
# że te wiadomości nie będą wysyłane do klienta. Opcja dotyczy tylko protokołu w wersji 2.

# ClientAliveCountMax - Wartość domyślna to 3. Jeśli ClientAliveInterval ustawiony jest na 15, a ClientAliveCountMax 
# na wartość domyślną, to niereagujący klienci SSH będą rozłączani po około 45 sekundach. 
# Opcja dotyczy tylko protokołu w wersji 2.

# Wartość timeout jest obliczana przez pomnożenie
# ClientAliveInterval i ClientAliveCountMax.
# timeout interval = ClientAliveInterval * ClientAliveCountMax
# Opcje OpenSSH ClientAliveInterval i ClientAliveCountMax
# nie są używane do rozłączania nieaktywnych sesji.
# W rzeczywistości zapobiegają one zamknięciu połączenia,
# nawet na nieaktywnych sesjach, tak długo jak klient i łącze sieciowe jest żywe.
# Jest to wewnętrzny mechanizm ssh, który wysyła pakiet "null
# wewnątrz ustanowionego tunelu, i czeka na odpowiedź od klienta.
# W tym przypadku wysyła jeden pakiet co 360 sekund, i rozłącza się po 1 brakującej odpowiedzi.
# Chociaż te opcje są pomocne w wykrywaniu i czyszczeniu rozłączonych sesji klientów,
# nie zabiją one sesji klientów, którzy nadal są połączeni, nawet jeśli są nieaktywni.
# Chyba, że ich klient nie odpowie na pakiet null.
```

Aby odłączyć nieaktywnych klientów, jeśli używasz bash jako powłoki, możesz ustawić wartość TMOUT w ogólnosystemowym profilu domyślnym lub na użytkownika:

```vim
# TMOUT Jeśli ustawione na wartość większą od zera,
# TMOUT traktowane jest jako domyślny limit czasu (tiomeout) 
# dla wbudowanego odczytu (read).
#
# Polecenie select kończy pracę jeśli nie otrzyma danych na wejściu 
# z terminala po TMOUT sekund.
#
# W powłoce interaktywnej, wartość ta interpretowana jest jako liczba
# sekund oczekiwania na wiersz wejścia po wydaniu głównej zachęty.
#
# Bash kończy pracę po odczekaniu tej liczby sekund
# jeśli nie nadejdzie pełny wiersz wejścia.

# Na przykład, dodanie następującej linii do `/etc/.bashrc`.
# zamknie sesje bashowe nieaktywnego użytkownika po 5 minutach,
# ale przeczytaj następujące ostrzeżenie przed włączeniem tego:

`export TMOUT=300`

# Ostrzeżenie: jako codzienny użytkownik powłoki, często pozwalam,
# aby jakiś terminal był otwarty podczas wielozadaniowości.
# Osobiście uznałbym ten mechanizm TMOUT za bardzo denerwujący,
# jeśli byłby ustawiony na niską wartość (nawet 10 minut).
# Nie polecam tego, chyba że jest przynajmniej ustawiony
# na bardzo wysoką wartość (co najmniej 1 godzinę - 3600 sekund).

# Moja opinia jest taka, że opcje OpenSSH `ClientAliveInterval` i `ClientAliveCountMax`
# (lub `ServerAliveInterval` i `ServerAliveCountMax`, ustawiane po stronie serwera),
# wystarczą, aby pozbyć się zombie/rozłączonych klientów.
# Używając ich, masz już gwarancję, że aktywna sesja na serwerze
# odpowiada otwartemu terminalowi na podłączonym kliencie.
#
# To jest wybór użytkownika, aby utrzymać swój terminal otwarty, 
# podczas gdy rozumiem. że chcesz zamknąć rozłączonych klientów.
# Nie widzę sensu zamykania sesji od legalnych użytkowników.
```

#### Bezpieczna konfiguracja szyfrów/MAC/Kex dostępnych w SSH 

```vim
KexAlgorithms diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group-exchange-sha256,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,curve25519-sha256,curve25519-sha256@libssh.org
Ciphers aes256-ctr,aes192-ctr,aes128-ctr
MACs hmac-sha2-512

# Mniej bezpieczne, lecz działające
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp521,ecdh-sha2-nistp384,ecdh-sha2-nistp256,diffie-hellman-group-exchange-sha256
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr
MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,umac-128@openssh.com
```

Upewnij się, że twój klient ssh może używać tych szyfrów, uruchom:

```bash
ssh -Q cipher | sort -u
to see the list
```

Polecam przeczytać ten artykuł::
[Secure Configuration of Ciphers/MACs/Kex available in SSH](https://security.stackexchange.com/questions/39756/secure-configuration-of-ciphers-macs-kex-available-in-ssh "Secure Configuration of Ciphers/MACs/Kex available in SSH")

Przeładuj usługę SSH

```bash
sudo systemctl reload sshd
```

### **Wprowadzenie do bezpieczeństwa systemu. Przeglądanie dzienników systemowych**

#### Wprowadzenie do bezpieczeństwa systemu Linux

1. **Aktualizacja systemu i oprogramowania**
   - Zadanie: Przeprowadź pełną aktualizację systemu operacyjnego i zainstalowanych pakietów na maszynie z systemem Linux. Użyj menedżera pakietów specyficznego dla Twojej dystrybucji (np. `apt` dla Debian/Ubuntu, `yum` dla CentOS, `dnf` dla Fedora).
   - Cel: Zrozumienie znaczenia utrzymywania aktualności oprogramowania w kontekście bezpieczeństwa.

#### Aktualizujemy system 

- openSUSE/SLES 

```bash
sudo zypper ref
sudo zypper up
```
- Yast

Wzmianka o Yast nie zawiera bezpośrednich poleceń, ponieważ Yast (Yet another Setup Tool) jest graficznym i tekstowym narzędziem do zarządzania systemem dostępnym w openSUSE i SLES. Można go użyć do zarządzania pakietami, ale konkretnych poleceń CLI nie podano.

- RPM-based (RedHat/Fedora/CentOS) 

```bash
sudo yum check-update
sudo yum update
# lub
sudo dnf check-update
sudo dnf update
```

DEB-based (Debian/Ubuntu)

```bash
sudo apt update
sudo apt upgrade
```

#### Konfiguracja firewalla

   - Zadanie: Skonfiguruj `ufw` (Uncomplicated Firewall) lub `firewalld` w zależności od dystrybucji, aby zezwolić tylko na ruch na portach 22 (SSH), 80 (HTTP) i 443 (HTTPS).
   - Cel: Nauka podstawowych zasad ograniczania dostępu do usług sieciowych w celu zwiększenia bezpieczeństwa systemu.

##### ufw

1. **Instalacja i włączenie `ufw`**
   - Zadanie: Upewnij się, że `ufw` jest zainstalowany na Twoim systemie. Jeśli nie, zainstaluj go za pomocą menedżera pakietów. Następnie włącz `ufw`.
     ```bash
     sudo apt install ufw  # Na Debianie/Ubuntu
     sudo ufw enable
     ```

2. **Konfiguracja podstawowych zasad**
   - Zadanie: Skonfiguruj `ufw`, aby domyślnie blokować wszystkie przychodzące połączenia i zezwalać na wszystkie wychodzące.
     ```bash
     sudo ufw default deny incoming
     sudo ufw default allow outgoing
     ```

3. **Otwieranie portów dla usług**
   - Zadanie: Otwórz porty 22 (SSH), 80 (HTTP) i 443 (HTTPS) w `ufw`, aby zezwolić na przychodzące połączenia do tych usług.
     ```bash
     sudo ufw allow 22
     sudo ufw allow 80
     sudo ufw allow 443
     ```

4. **Sprawdzenie statusu i reguł `ufw`**
   - Zadanie: Wyświetl status `ufw` oraz aktualne reguły, aby sprawdzić, czy konfiguracja jest zgodna z oczekiwaniami.
     ```bash
     sudo ufw status verbose
     ```

##### firewalld

1. **Instalacja i uruchomienie `firewalld`**
   - Zadanie: Upewnij się, że `firewalld` jest zainstalowany i uruchomiony na Twoim systemie. Jeśli nie, zainstaluj go i uruchom.
     ```bash
     sudo yum install firewalld  # Na CentOS/Red Hat
     sudo systemctl start firewalld
     sudo systemctl enable firewalld
     ```

2. **Ustawienie domyślnej polityki**
   - Zadanie: Skonfiguruj `firewalld`, aby domyślnie blokować wszystkie przychodzące połączenia i zezwalać na wszystkie wychodzące.
     ```bash
     sudo firewall-cmd --set-default-zone=public
     sudo firewall-cmd --zone=public --change-interface=eth0  # eth0 dostosuj do swojej karty sieciowej
     ```

3. **Otwieranie portów dla usług**
   - Zadanie: Otwórz porty 22 (SSH), 80 (HTTP) i 443 (HTTPS) w `firewalld`, aby zezwolić na przychodzące połączenia do tych usług.
     ```bash
     sudo firewall-cmd --zone=public --add-service=ssh --permanent
     sudo firewall-cmd --zone=public --add-service=http --permanent
     sudo firewall-cmd --zone=public --add-service=https --permanent
     ```

4. **Zastosowanie zmian i sprawdzenie konfiguracji**
   - Zadanie: Zastosuj zmiany w konfiguracji i sprawdź aktualne zasady `firewalld`.
     ```bash
     sudo firewall-cmd --reload
     sudo firewall-cmd --list-all
     ```

#### Utworzenie i zarządzanie użytkownikami
   - Zadanie: Utwórz nowego użytkownika z ograniczonymi uprawnieniami (bez dostępu sudo/root). Skonfiguruj dla tego użytkownika silne hasło i zapoznaj się z plikiem `/etc/sudoers` w kontekście zarządzania uprawnieniami.
   - Cel: Zrozumienie znaczenia zasady najmniejszych uprawnień i zarządzania dostępem użytkowników.

##### Zadania

1. **Tworzenie nowego użytkownika**
   - Zadanie: Utwórz nowego użytkownika o nazwie `test_admin` za pomocą polecenia `useradd` lub `adduser` (w zależności od dystrybucji). Następnie ustaw hasło dla tego użytkownika.
     ```bash
     sudo useradd -m test_admin
     sudo passwd test_admin
     ```
   - Cel: Nauka tworzenia kont użytkowników i ustawiania haseł.

2. **Przypisywanie użytkownika do grupy**
   - Zadanie: Dodaj `test_admin` do grupy `sudo` (na Debianie/Ubuntu) lub `wheel` (na CentOS/Fedora), aby umożliwić mu wykonanie poleceń jako superużytkownik.
     ```bash
     sudo usermod -aG sudo test_admin  # Debian-based
     sudo usermod -aG wheel test_admin  # RHEL-based
     ```
   - Cel: Zrozumienie zarządzania członkostwem w grupach i delegowania uprawnień.

3. **Ograniczenie dostępu do sudo**
   - Zadanie: Edytuj plik `/etc/sudoers` za pomocą `visudo`, aby `test_admin` mógł wykonywać polecenia sudo bez podawania hasła (opcjonalnie, dla zaawansowanych użytkowników).
     ```bash
     sudo visudo
     ```
     Dodaj na końcu pliku:
     ```
     test_admin ALL=(ALL) NOPASSWD: ALL
     ```
   - Cel: Nauka zaawansowanego zarządzania uprawnieniami za pomocą `sudo`.

4. **Zmiana powłoki domyślnej**
   - Zadanie: Zmień powłokę domyślną dla `test_admin` na `bash`, jeśli nie została ona ustawiona podczas tworzenia konta.
     ```bash
     sudo chsh -s /bin/bash test_admin
     ```
   - Cel: Zrozumienie, jak zarządzać powłokami użytkowników i dostosowywać środowisko pracy.

5. **Usuwanie użytkownika**
   - Zadanie: Usuń `test_admin` z systemu, zachowując jego katalog domowy jako backup.
     ```bash
     sudo userdel -r test_admin
     ```
   - Cel: Nauka bezpiecznego usuwania kont użytkowników i zarządzania danymi użytkownika.

Pamiętaj, że działania związane z `sudo` i edycją `/etc/sudoers` powinny być wykonywane ostrożnie, aby uniknąć problemów z uprawnieniami i bezpieczeństwem systemu.   

#### Przeglądanie dzienników systemowych w Linux

1. **Przeglądanie dzienników za pomocą `journalctl`**
   - Zadanie: Wykorzystaj narzędzie `journalctl` do przeglądania i filtrowania dzienników systemowych. Znajdź i wyświetl wpisy dziennika dotyczące usługi SSH (`sshd`) z ostatnich 24 godzin.
   - Cel: Nauka korzystania z `journalctl` do analizy dzienników systemowych i zrozumienie struktury dzienników w systemie Linux.

##### Zadania do przeglądania dzienników za pomocą `journalctl`

1. **Podstawowe wykorzystanie `journalctl`**
   - Zadanie: Wyświetl wszystkie dostępne dzienniki systemowe. Następnie użyj przewijania (scrollowania) do przeglądania wpisów.
     ```bash
     journalctl
     ```
   - Cel: Zapoznanie się z podstawową funkcjonalnością `journalctl` i nauka nawigacji po dziennikach.

2. **Filtrowanie dzienników dla określonego zakresu czasu**
   - Zadanie: Wyświetl wpisy dziennika dla konkretnego zakresu czasu. Na przykład, znajdź wszystkie wpisy od początku bieżącego dnia.
     ```bash
     journalctl --since today
     ```
   - Cel: Nauka filtrowania dzienników na podstawie czasu, co jest przydatne do analizy zdarzeń w określonych okresach.

3. **Wyszukiwanie wpisów od konkretnego serwisu**
   - Zadanie: Wyświetl wszystkie wpisy dziennika dla usługi SSH (`sshd`).
     ```bash
     journalctl -u sshd
     ```
   - Cel: Zrozumienie, jak filtrować dzienniki dla określonej usługi, co jest kluczowe przy diagnozowaniu problemów związanych z tą usługą.

4. **Zaawansowane filtrowanie z użyciem kilku kryteriów**
   - Zadanie: Znajdź wszystkie wpisy dziennika związane z usługą `sshd` zawierające słowo "Failed". Użyj grep do filtrowania wyników.
     ```bash
     journalctl -u sshd | grep 'Failed'
     ```
   - Cel: Nauka zaawansowanego filtrowania dzienników, co pozwala na dokładne analizowanie wpisów związanych z konkretnymi problemami.

5. **Wyświetlanie dzienników dla konkretnego urządzenia**
   - Zadanie: Wyświetl dzienniki związane z konkretnym urządzeniem, np. dyskiem (`/dev/sda`).
     ```bash
     journalctl _DEVNAME=/dev/sda
     ```
   - Cel: Zrozumienie, jak identyfikować i analizować zdarzenia związane z określonymi urządzeniami w systemie.

6. **Monitorowanie w czasie rzeczywistym**

   - Zadanie: Użyj `tail -f` lub `journalctl -f` do monitorowania w czasie rzeczywistym dzienników dotyczących autentykacji użytkowników. Obserwuj próby logowania i identyfikuj nieudane próby.
   - Cel: Zrozumienie, jak monitorować aktywność systemu w czasie rzeczywistym oraz identyfikować potencjalne próby nieautoryzowanego dostępu.

   - Zadanie: Użyj `journalctl`, aby monitorować dzienniki w czasie rzeczywistym. To przydatne do obserwacji bieżącej aktywności systemu.
     ```bash
     journalctl -f
     ```
   - Cel: Nauka, jak śledzić dzienniki w czasie rzeczywistym, co jest niezbędne przy debugowaniu bieżących problemów.

Te zadania oferują solidne wprowadzenie do korzystania z `journalctl` do pracy z dziennikami systemowymi w Linuxie. Opanowanie `journalctl` jest kluczowe dla każdego, kto zajmuje się administracją systemami, zapewniając umiejętności niezbędne do monitorowania, debugowania i utrzymania zdrowia systemu.   

##### Zadania dla monitorowania w czasie rzeczywistym z użyciem `tail -f`

1. **Monitorowanie dziennika systemowego**
   - Zadanie: Użyj `tail -f` do monitorowania głównego dziennika systemowego. Dla systemów używających rsysloga (typowo w dystrybucjach takich jak Debian, Ubuntu), plik ten zazwyczaj znajduje się w `/var/log/syslog`. Dla systemów opartych na `systemd`, których głównym narzędziem do logowania jest `journald`, możesz monitorować tradycyjne pliki logów w `/var/log`, np. `/var/log/messages` w dystrybucjach takich jak Fedora, CentOS.
     ```bash
     tail -f /var/log/syslog  # Debian-based
     tail -f /var/log/messages  # RHEL-based
     ```
   - Cel: Nauka monitorowania ogólnego dziennika systemowego, co jest kluczowe do obserwacji bieżącej aktywności systemu.

2. **Obserwacja logów autentykacji**
   - Zadanie: Skorzystaj z `tail -f` do monitorowania logów autentykacji. Wiele systemów przechowuje te informacje w pliku `/var/log/auth.log` (Debian/Ubuntu) lub `/var/log/secure` (CentOS/RedHat).
     ```bash
     tail -f /var/log/auth.log  # Debian-based
     tail -f /var/log/secure  # RHEL-based
     ```
   - Cel: Nauka identyfikacji i reagowania na próby logowania, zarówno udane, jak i nieudane, co jest kluczowe dla bezpieczeństwa systemu.

Wykorzystanie `tail -f` do monitorowania plików dzienników w czasie rzeczywistym jest podstawową, ale potężną techniką w diagnostyce systemów i aplikacji. Pozwala administratorom systemów i deweloperom na bieżąco obserwować aktywność systemową i aplikacji, ułatwiając szybkie identyfikowanie i rozwiązywanie problemów.

3. **Analiza logów zabezpieczeń**
   - Zadanie: Znajdź w dziennikach systemowych informacje o aktualizacjach bezpieczeństwa, które zostały zastosowane, oraz wszelkie ostrzeżenia związane z bezpieczeństwem. Możesz użyć `grep` lub `awk` do filtrowania odpowiednich wpisów.
   - Cel: Zrozumienie znaczenia regularnego przeglądania dzienników systemowych w kontekście identyfikacji i reagowania na problemy związane z bezpieczeństwem.

Analiza logów zabezpieczeń to kluczowy element utrzymania bezpieczeństwa systemu i identyfikacji potencjalnych zagrożeń. Poniżej przedstawiam kilka zadań, które pomogą Ci rozwijać umiejętności związane z przeszukiwaniem i analizą dzienników w poszukiwaniu informacji o aktualizacjach bezpieczeństwa i ostrzeżeniach.

##### Zadania do analizy logów zabezpieczeń

1. **Wyszukiwanie wpisów o aktualizacjach bezpieczeństwa**
   - Zadanie: Użyj `grep` do przeszukania dzienników systemowych w poszukiwaniu informacji o aktualizacjach bezpieczeństwa. Na przykład, w systemach opartych na Debianie/Ubuntu, informacje o aktualizacjach mogą być rejestrowane w `/var/log/apt/history.log`. Szukaj wpisów zawierających frazę "security".
     ```bash
     grep 'security' /var/log/apt/history.log
     ```
   - Cel: Nauka identyfikowania wpisów dziennika dotyczących aktualizacji bezpieczeństwa, co pozwala śledzić, które łatki bezpieczeństwa zostały zainstalowane.

2. **Filtrowanie ostrzeżeń bezpieczeństwa w dziennikach systemowych**
   - Zadanie: Skorzystaj z `awk` do przefiltrowania i wyświetlenia tylko tych linii z pliku dziennika systemowego (np. `/var/log/syslog` lub `/var/log/messages`), które zawierają poziom ostrzeżenia (`warn` lub `warning`).
     ```bash
     awk '/warn|warning/' /var/log/syslog
     ```
   - Cel: Zrozumienie, jak wyszukiwać specyficzne poziomy ostrzeżeń bezpieczeństwa w dziennikach, co jest kluczowe do wczesnego identyfikowania potencjalnych problemów.

3. **Analiza nieudanych prób logowania**
   - Zadanie: Użyj kombinacji `grep` i innych narzędzi tekstowych, jak `cut` lub `awk`, do zidentyfikowania i wyświetlenia szczegółów dotyczących nieudanych prób logowania. Dla systemów używających `systemd`, możesz wykorzystać `journalctl` do przefiltrowania logów usługi SSH (`sshd`), a następnie użyć `grep` do wyszukiwania nieudanych prób.
     ```bash
     journalctl -u sshd | grep 'Failed'
     ```
   - Cel: Nauka identyfikowania nieudanych prób logowania, co jest kluczowe dla monitorowania potencjalnych prób nieautoryzowanego dostępu.

4. **Śledzenie błędów systemowych i awarii**
   - Zadanie: Wykorzystaj `grep` lub `awk` do wyszukiwania dzienników systemowych w celu znalezienia wpisów związanych z błędami systemowymi lub awariami. Możesz przeszukać `/var/log/syslog` lub `/var/log/messages` dla słów kluczowych takich jak `error`, `fail`, `critical`.
     ```bash
     grep -i -E "error|fail|critical" /var/log/syslog
     ```
   - Cel: Rozwinięcie umiejętności szybkiego identyfikowania i reagowania na krytyczne błędy systemowe oraz awarie.

Te zadania są przeznaczone do rozwijania podstawowych umiejętności niezbędnych do efektywnej analizy dzienników zabezpieczeń. Praktyczne opanowanie tych technik pozwoli Ci lepiej zrozumieć stan bezpieczeństwa Twojego systemu i reagować na potencjalne zagrożenia.

### **Wprowadzenie do fail2ban.**

{{< tabs CentOS Ubuntu >}}
  {{< tab >}}
  ### CentOS
  Aby zainstalować Fail2Ban na CentOS 7.6, w pierwszej kolejności trzeba będzie zainstalować repozytorium EPEL (ang. _Extra Packages for Enterprise Linux_). EPEL zawiera dodatkowe pakiety dla wszystkich wersji CentOS, jednym z tych dodatkowych pakietów jest Fail2Ban.
  ```bash
  sudo yum install epel-release
  sudo yum install fail2ban fail2ban-systemd
  ```
  {{< /tab >}}
  {{< tab >}}
  ### Debian/Ubuntu
  Dla Debian/Ubuntu wystarczy komenda:
  ```bash
  sudo apt-get install fail2ban
  ```
  {{< /tab >}}
{{< /tabs >}}

W przypadku CentOS następnym kroku należy zaktualizować zasady SELinux. (uwaga: na mikr.us nie ma zainstalowanego SELinux).

```bash
sudo yum update -y selinux-policy*
```

Debian i Ubuntu posiadaja AppArmor. 


Po zainstalowaniu, będziemy musieli skonfigurować i dostosować oprogramowanie za pomocą pliku konfiguracyjnego jail.local. Plik jail.local zastępuje plik jail.conf i jest używany w celu zapewnienia bezpieczeństwa aktualizacji konfiguracji użytkownika.

Zrób kopię pliku jail.conf i zapisz go pod nazwą jail.local: zaktualizuj politykę SELinux:

```bash
cp -pf /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Otwórz plik jail.local do edycji w Vim za pomocą następującego polecenia:

```bash
sudo -e /etc/fail2ban/jail.local
```

Kod pliku może składać się z wielu linii kodów, które wykonują się, aby zapobiec zablokowaniu jednego lub wielu adresów IP, ustawić czas trwania bantime, itp. Typowy plik konfiguracyjny więzienia zawiera następujące linie:

```vim
[DEFAULT]
ignoreip = 127.0.0.1/8
ignorecommand =
bantime = 600
findtime = 600
maxretry = 5
backend = systemd
```

  * IgnoreIP służy do ustawienia listy adresów IP, które nie będą zakazane. Lista adresów IP powinna być podana z separatorem spacji. Ten parametr jest używany do ustawienia osobistego adresu IP (jeśli istnieje dostęp do serwera ze stałego adresu IP).
  * Parametr Bantime służy do ustawienia czasu trwania sekund, na które host ma zostać zbanowany.
  * Findtime jest parametrem, który służy do sprawdzenia, czy host musi zostać zbanowany czy nie. Gdy host generuje maksimum w ostatnim findtime, jest on banowany.
  * Maxretry jest parametrem używanym do ustawienia limitu liczby prób przez hosta, po przekroczeniu tego limitu, host jest banowany.

#### Dodawanie pliku więzienia (ang. jail), w celu ochrony SSH.

Utwórz nowy plik za pomocą edytora Vim.

```bash
sudo -e /etc/fail2ban/jail.d/sshd.local
```

Do powyższego pliku należy dodać następujące wiersze kodu.

```vim
[sshd]
enabled = true
port = ssh
action  = iptables-allports
# logpath = /var/log/secure # manualne ustawienie ścieżki 
logpath = %(sshd_log)s
findtime = 600
maxretry = 3
bantime = 86400
```

W przypadku, gdy używasz iptables , action ustaw jak poniżej:

```vim
action = iptables-allports
```

  * Parametr enable jest ustawiony na wartość true, w celu zapewnienia ochrony, aby wyłączyć ochronę, jest ustawiony na false. Parametr filtra sprawdza plik konfiguracyjny sshd, znajdujący się w ścieżce /etc/fail2ban/filter.d/sshd.conf.
  * Parametr action służy do wyprowadzenia adresu IP, który musi być zakazany za pomocą filtra dostępnego w pliku /etc/fail2ban/action.d/iptables-allports.conf.
  * Parametr port można zmienić na nową wartość, np. port=2244, jak to ma miejsce w tym przypadku. W przypadku korzystania z portu 22, nie ma potrzeby zmiany tego parametru.
  * Ścieżka logowania podaje ścieżkę, na której zapisany jest plik logu. Ten plik dziennika jest skanowany przez Fail2Ban.
  * Maxretry służy do ustawienia maksymalnego limitu nieudanych wpisów logowania.
  * Parametr Bantime służy do ustawienia czasu trwania sekund, na który host musi zostać zablokowany.

#### Uruchomienie usługi Fail2Ban

Jeśli jeszcze nie używasz zapory sieciowej CentOS, uruchom ją:

```bash
sudo systemctl enable firewalld
sudo systemctl start firewalld
```

Jeśli używasz iptables, to:

```bash
sudo systemctl enable iptables
sudo systemctl start iptables
```

Wykonaj poniższe plecenia, aby uruchomić Fail2Ban na serwerze.

```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

#### Śledzenie wpisów logowania fail2ban

Poniższe polecenie służy do sprawdzenia, które próby zalogowania się do serwera przez post ssh nie powiodły się.

```bash
cat /var/log/secure | grep 'Failed password'
```

Wykonanie powyższej komendy spowoduje wyświetlenie listy nieudanych prób wprowadzenia hasła głównego z różnych adresów IP. Format wyników będzie podobny do pokazanego poniżej:

```vim
Feb 12 19:27:12 centos sshd[25729]: Failed password for root from 150.10.0.107 port 9074 ssh2
Feb 13 15:05:35 deb_usr sshd[1617]: Failed password for invalid user pi from 42.236.138.215 port 58182 ssh2
```

#### Sprawdzanie zbanowanych adresów IP przez Fail2Ban

Poniższe polecenie służy do uzyskania listy zablokowanych adresów IP, które zostały rozpoznane jako zagrożenia metodą brute force.

```bash
iptables -L –n
```

#### Sprawdzanie statusu Fail2Ban

Użyj następującej komendy, aby sprawdzić status plików jail w Fail2Ban:

```bash
sudo fail2ban-client status
```

Wynik powinien być podobny do tego:

```bash
# fail2ban-client status
Status
|- Number of jail: 1
`- Jail list: sshd
```

Poniższe polecenie wyświetli zbanowane adresy IP dla danego więzienia (jail).

```bash
sudo fail2ban-client status sshd
```
#### Usunięcie zbanowanego adresu IP

W celu usunięcia adresu IP z zablokowanej listy, parametr IPADDRESS jest ustawiony na odpowiedni adres IP, który wymaga odbanowania. Nazwa &#8222;sshd&#8221; jest nazwą więzienia, w tym przypadku jest to więzienie &#8222;sshd&#8221;, które skonfigurowaliśmy powyżej. Poniższe polecenie pozwala usunąć adres IP.

```bash
sudo fail2ban-client set sshd unbanip IPADDRESS
```
#### Dodawanie własnego filtra w celu zwiększenia ochrony

Fail2ban umożliwia tworzenie własnych filtrów. Poniżej krótki opis konfiguracji jednego z nich.

1.Należy przejść do katalogu filter.d Fail2ban:

```bash
sudo cd /etc/fail2ban/filter.d
```

2.Utworzyć plik wordpress.conf i dodać do niego wyrażenie regularne.

```bash
sudo -e wordpress.conf
```

```vim
#Fail2Ban filter for WordPress
[Definition]
failregex =  - - [(\d{2})/\w{3}/\d{4}:\1:\1:\1 -\d{4}] "POST /wp-login.php HTTP/1.1" 200
ignoreregex =
```

Zapisać i zamknąć plik.

3.Dodać sekcję WordPress na końcu pliku jail.local:

```bash
$ sudo -e /etc/fail2ban/jail.local
```

```vim
[wordpress]
enabled = true
filter = wordpress
logpath = /var/log/httpd/access_log 
#CentOS Zwróć uwagę, czy jest _ czy . 
# W pliku /etc/httpd/conf/httpd.conf masz informację, 
# gdzie jest zapisywany log.
# logpath = /var/log/apache2/access.log // Ubuntu/Debian
port = 80,443
```

Jeśli chcemy banować boty, wystarczy dodać akcję, czas bana oraz ilość prób, jak w przypadku jail sshd opisanego wyżej.

W tym celu użyty zostanie domyślny ban i akcja e-mail. Inne akcje mogą być zdefiniowane przez dodanie akcji = linia.  
Zapisz i wyjdź, a następnie uruchom ponownie Fail2ban poleceniem:

```bash
sudo systemctl restart fail2ban
```

Sprawdź również, czy Twój regex działa:

```bash
fail2ban-regex /var/log/apache2/access.log /etc/fail2ban/filter.d/wordpress.conf
```

Celem opisanego zadania jest wprowadzenie do korzystania z Fail2Ban - narzędzia służącego do ochrony serwerów przed atakami brute-force i innymi próbami nieautoryzowanego dostępu. Zadanie obejmuje kroki instalacji Fail2Ban na różnych dystrybucjach Linuxa (CentOS i Debian/Ubuntu), konfigurację podstawowych ustawień bezpieczeństwa poprzez edycję plików konfiguracyjnych, oraz dodatkowe kroki takie jak aktualizacja zasad SELinux (dla CentOS) i konfiguracja zapor sieciowych. Zadanie zawiera również instrukcje dotyczące monitorowania i zarządzania zbanowanymi adresami IP, a także tworzenia własnych filtrów dla specyficznych potrzeb, takich jak ochrona aplikacji WordPress przed nieautoryzowanym dostępem.