---
title: "Serwer DHCP"
date:  2023-04-28T11:00:00+00:00
description: "Konfiguracja serwera DHCP"
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
image: images/2023-thumbs/dhcp.webp
---
#### Ćwiczenia do wykonania:
1. Zainstaluj DHCP.
2. Skonfiguruj serwer DHCP
3. Skonfiguruj klienta, by pobierał adres z DHCP

<script async id="asciicast-581198" src="https://asciinema.org/a/581198.js"></script>

#### Zainstaluj serwer DHCP

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  {{< highlight Shell "linenos=table" >}}
  sudo zypper -n install dhcp-server
  {{< /highlight >}}  
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  {{< highlight Shell "linenos=table" >}}
  sudo apt -y install isc-dhcp-server 
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  {{< highlight Shell "linenos=table" >}}
  sudo yum install dhcp-server -y
  sudo dnf install dhcp-server -y
  {{< /highlight >}}
  {{< /tab >}}
{{< /tabs >}}

#### Skonfiguruj serwer DHCP

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  {{< highlight Shell "linenos=table" >}}
  sudo vim /etc/sysconfig/dhcpd
  # użyj interfejsu sieciowego, który odpowiada za komunikację w danej sieci/podsieci.
  DHCPD_INTERFACE="eth1"
  mv /etc/dhcpd.conf /etc/dhcpd.conf.org
  sudo vim /etc/dhcpd.conf
  # wklej
  option domain-name "p-tech.pl";
  option domain-name-servers ns1.p-tech.pl;
  max-lease-time 7200;
  authoritative;
  subnet 10.10.5.0 netmask 255.255.255.0 {
    # określ zakres dzierżawionego adresu IP
    range dynamic-bootp 10.10.5.200 10.10.5.254;
    # podaj adres rozgłoszeniowy
    option broadcast-address 10.10.5.255;
    # podaj domyślną bramę
    option routers 10.10.5.1;
  }
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  {{< highlight Shell "linenos=table" >}}
  sudo vim /etc/default/isc-dhcp-server
  # odkomentuj poniższą linię:
  DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
  # użyj interfejsu sieciowego, który odpowiada za komunikację w danej sieci/podsieci.
  INTERFACESv4="enp1s1"
  sudo vim /etc/dhcp/dhcpd.conf 
  option domain-name "p-tech.pl";
  option domain-name-servers ns1.p-tech.pl;
  max-lease-time 7200;
  authoritative;
  subnet 10.10.5.0 netmask 255.255.255.0 {
    # określ domyślną bramę
    option routers 10.10.5.1;
    # określ maskę podsieci
    option subnet-mask 255.255.255.0;
    # określ zakres dzierżawionego adresu IP
    range dynamic-bootp 10.10.5.200 10.10.5.254;
  }
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  {{< highlight Shell "linenos=table" >}}
  sudo vim /etc/dhcp/dhcp.conf
  default-lease-time 600;
  max-lease-time 7200;
  authoritative;
  subnet 10.10.5.0 netmask 255.255.255.0 {
    range 10.10.5.200 10.10.5.254;
    option routers 10.10.5.1;
    option subnet-mask 255.255.255.0;
    option domain-name-servers 10.10.5.1;
  }
  {{< /highlight >}}
  {{< /tab >}}
{{< /tabs >}}


#### skonfiguruj firewall

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  {{< highlight Shell "linenos=table" >}}
  sudo firewall-cmd --add-service=dhcp --permanent
  sudo firewall-cmd --reload
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  {{< highlight Shell "linenos=table" >}}
  sudo ufw allow bootps
  sudo ufw allow 53/udp
  sudo ufw allow 53/tcp
  sudo ufw allow from any port 68 to any port 67 proto udp
  {{< /highlight >}}
  wyjaśnienie: port 53 jest dla DNS, porty 67 i 68 są dla komunikacji DHCP. 

  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  {{< highlight Shell "linenos=table" >}}
  sudo firewall-cmd --add-service=dhcp --permanent
  firewall-cmd --reload
  {{< /highlight >}}
  {{< /tab >}}
{{< /tabs >}}


#### Uruchom serwer DHCP

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  {{< highlight Shell "linenos=table" >}}
  sudo systemctl start dhcpd
  sudo systemctl enable dhcpd 
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  {{< highlight Shell "linenos=table" >}}
  sudo systemctl start isc-dhcp-server
  sudo systemctl enable isc-dhcp-server
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  {{< highlight Shell "linenos=table" >}}
  sudo systemctl start dhcpd
  sudo systemctl enable dhcpd 
  {{< /highlight >}}
  {{< /tab >}}
{{< /tabs >}}

#### Skonfiguruj klienta DHCP

{{< tabs SLES Debian RedHat >}}
  {{< tab >}}
  ### SLES
  {{< highlight Shell "linenos=table" >}}
  sudo vim /etc/sysconfig/network/ifcfg-eth1
  # zmiana
  BOOTPROTO='dhcp'
  # zmień na puste wszystkie poniżej
  BROADCAST=''
  IPADDR=''
  NETMASK=''
  NETWORK=''
  # ewentualnie użyj yast i dokonaj zmiany
  sudo yast2
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Debian
  {{< highlight Shell "linenos=table" >}}
  sudo vim /etc/network/interfaces
  # zmień na [dhcp] w docelowej linii iface
  iface enp1s1 inet dhcp
  # zrestartuj interfejs
  sudo systemctl restart ifup@enp1s1
  {{< /highlight >}}
  {{< /tab >}}
  {{< tab >}}
  ### Red Hat
  {{< highlight Shell "linenos=table" >}}
  sudo vim /etc/sysconfig/network-scripts/ifcfg-eth1
  DEVICE=eth1
  BOOTPROTO=dhcp
  ONBOOT=yes
  {{< /highlight >}}
  {{< /tab >}}
{{< /tabs >}}

#### Sprawdź czy klient dostał prawidłową adresację

```
ip a
ip r
```

#### Przeszukaj logi

{{< highlight Shell "linenos=table" >}}
sudo tail -50 /var/log/messages | grep -i 10.10.5.200
{{< /highlight >}}
