---
title: "Moduł 1 - dystrybucje Linux - teoria"
date:  2024-02-07T14:00:00+00:00
description: "Moduł 1 - dystrybucje Linux - teoria"
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
image: images/2024-thumbs/podstawy_pracy_w_systemie_linux.webp
---
## Część Teoretyczna
### Moduł 1: Dystrybucje Linux - teoria
#### Czas Trwania: 10 minut

1. **Wstęp o dystrybucjach Linux:**
   - Porównanie popularnych dystrybucji (Debian, Fedora, Ubuntu, Arch).
   - Omówienie różnych metod instalacji systemu.

**1. Wprowadzenie:**
Linux nie jest jednolitym systemem operacyjnym, ale rodzajem systemu operacyjnego, który obejmuje wiele różnych dystrybucji. Każda dystrybucja, czyli "distro", oferuje unikalny zestaw funkcji, interfejs użytkownika, zarządzanie pakietami oraz społeczność wsparcia. Wybór odpowiedniej dystrybucji zależy od preferencji użytkownika, wymagań sprzętowych i celu użycia.

**2. Porównanie popularnych dystrybucji:**

- **Debian:**
  - **Charakterystyka:** Stabilność i bezpieczeństwo. Debian jest znany z długiego cyklu wydawniczego i skupia się na stabilności pakietów. 
  - **Zarządzanie pakietami:** APT (Advanced Package Tool).
  - **Użytkownicy:** Idealny dla serwerów i doświadczonych użytkowników ceniących stabilność.

- **Fedora:**
  - **Charakterystyka:** Innowacyjność. Fedora często wprowadza nowe technologie Linux, będąc rodzajem poligonu doświadczalnego dla Red Hat.
  - **Zarządzanie pakietami:** DNF.
  - **Użytkownicy:** Dla użytkowników szukających najnowszych technologii w stabilnym wydaniu.

- **Ubuntu:**
  - **Charakterystyka:** Łatwość użycia i popularność. Ubuntu jest jedną z najbardziej popularnych dystrybucji, często polecanych początkującym.
  - **Zarządzanie pakietami:** APT.
  - **Użytkownicy:** Idealna dla początkujących, jak i zaawansowanych użytkowników.

- **Arch Linux:**
  - **Charakterystyka:** Minimalizm i personalizacja. Arch pozwala użytkownikom zbudować system od podstaw.
  - **Zarządzanie pakietami:** Pacman.
  - **Użytkownicy:** Dla doświadczonych użytkowników, którzy chcą skonfigurować system według własnych potrzeb.

**3. Metody instalacji systemu:**

- **Instalacja graficzna:** Większość dystrybucji oferuje graficzne instalatory, które krok po kroku przeprowadzają przez proces instalacji. Ubuntu i Fedora oferują przyjazne dla użytkownika środowiska instalacyjne.
- **Instalacja tekstowa:** Alternatywa dla bardziej doświadczonych użytkowników lub dla serwerów, gdzie nie jest wymagane środowisko graficzne. Debian oferuje zaawansowaną instalację tekstową.
- **Instalacja sieciowa:** Niektóre dystrybucje, jak Arch Linux, oferują instalację przez pobranie najnowszych pakietów bezpośrednio z internetu. To pozwala na utworzenie zaktualizowanego systemu od razu po instalacji.

* W menu instalatora dowolnej dystrybucji wybieramy wersję minimal i/lub jeśli jest opcja wybieramy wersję server, lub od razu instalujemy dystrybucję w wersji server. Metoda instalacji zależy od wyboru. Można też wybrać wersję net-minimal.
Nie wybieramy żadnego środowiska graficznego. Chcemy mieć czyste CLI (command line).

**4. Sposoby instalacji:**
- **Z płyty** – po prostu nagrywamy obraz iso na płytę 
- **Z USB** – wykorzystujemy Balena Etcher do nagrania obrazu iso na pendrive. Możemy ewentualnie skorzystać z Rufus w Windows. Balena działa w różnych systemach, stąd większa uniwersalność tego rozwiązania.
- Można użyć też **Ventoy** (https://www.ventoy.net/)
- Lub użyć **IODD ST400** (działa podobnie jak Ventoy, ale kosztuje znacznie więcej, niż pendrive. Natomiast ciekawostką jest fakt, że działa z większością starych serwerów.

**5. Różnice pomiędzy dystrybucjami**

- **RPM based**
  - **RHEL-based** (Red Hat, AlmaLinux, Oracle Linux, Rocky Linux), 
  - **openSUSE-based** (openSUSE, SUSE Linux Enterprise aka SLES, GeckoLinux)
  - **Fedora-based** (Fedora, CentOS Stream, Amazon Linux 2, Qubes OS)

- **DEB-based**
  - **Debian-based** (Debian, antiX, BackTrack, Kali Linux, Parrot OS, Raspberry Pi OS)
  - **Ubuntu-based** (Ubuntu, Kubuntu, Lubuntu, Xubuntu)

- **Pacman-based**
  - **Arch Linux-based** (Arch , Antegros, Garuda, Manjaro, SteamOS)

- **Gentoo-based**
- **Slackware-based**
- **Android-based**

[Źródło](https://en.wikipedia.org/wiki/List_of_Linux_distributions)

- **Podstawowe różnice to najczęściej te związane z firewall oraz managerem sieci i package managerem (menadżer pakietów)**
- **iptables (te starsze), firewalld, openSUSE firewall, nftables**
- **NetworkManager, wicked**
- **yum, dnf, apt-get, apt, zypper, yast, pacman**

- Podstawowe polecenia używane w Linuksie są wspólne dla każdej dystrybucji:
- ifconfig, route, hostname, netstat, arp, mii-tool.
- Wiele dystrybucji zawiera teraz narzędzia iproute2 z ulepszonymi narzędziami do routingu i sieci, w tym potężne polecenia ip i tc.
- Każda dystrybucja ma własne narzędzie konfiguracyjne, które działa na różnie zdefiniowanych plikach konfiguracyjnych. Niektóre z nich są wspólne: /etc/resolv.conf, /etc/nsswitch.conf, /etc/hosts, /etc/services, /etc/protocols
- Niektóre, zwykle te, w których są zdefiniowane adresy IP i trasy, zmieniają się. Oto kilka odpowiednich plików dla różnych dystrybucji, ich składnia może się różnić w zależności od skryptów używanych do ich obsługi:


![pliki konfiguracyjne](/images/2024/pliki-konfiguracyjne.webp "pliki konfiguracyjne")
<figcaption>pliki konfiguracyjne</figcaption>

- Dodatkowo dla zainteresowanych 
– [instalacja Arch poprzez sieć (ssh)](https://wiki.archlinux.org/title/Install_Arch_Linux_via_SSH)
- [Gentoo – bardzo długa kompilacja paczek](https://wiki.gentoo.org/wiki/Main_Page)
- [Linux from scratch (LFS), gdzie samodzielnie buduje się cały system zaczynając od kernel](https://www.linuxfromscratch.org/)

##### Instalujemy X11/xorg

- [openSUSE/SLES](https://software.opensuse.org/download.html?project=X11:XOrg&package=xorg-x11-server)

```bash
sudo zypper add repo
sudo zypper refresh
sudo zypper install xorg-x11-server
```

- RPM-based (RedHat/Fedora/CentOS)

```bash
sudo yum install xorg-x11-xauth
sudo dnf install xorg-x11-xauth
```

- [DEB-based (Debian/Ubuntu)](https://wiki.debian.org/Xorg)

```bash
sudo apt install xorg
```

##### Instalujemy Gnome/KDE/XFCE/Awesome

**XFCE**

- openSUSE/SLES

```bash
sudo zypper install xfce4
```

- RPM-based (RedHat/Fedora/CentOS)

```bash
rpm -qi epel-release
sudo dnf --enablerepo=epel group
sudo dnf install epel-release
sudo dnf group list | grep -i xfce
sudo dnf groupinstall "Xfce" "base-x"
sudo echo "exec /usr/bin/xfce4-session" >>  ~/.xinitrc
sudo systemctl set-default graphical
```

- DEB-based (Debian/Ubuntu)

```bash
sudo apt install xubuntu-desktop
```

##### Aktualizujemy system 

- openSUSE/SLES 

```bash
sudo zypper ref
sudo zypper up
```
- Yast

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

### Podsumowanie

Wybór dystrybucji Linux zależy od wielu czynników, w tym od poziomu doświadczenia użytkownika, preferencji dotyczących stabilności vs. najnowszych technologii, a także od specyficznych wymagań dotyczących oprogramowania i sprzętu. Każda z wymienionych dystrybucji ma swoje unikalne cechy i społeczność, co czyni Linux systemem wyjątkowo elastycznym i dostosowującym się do potrzeb użytkowników.