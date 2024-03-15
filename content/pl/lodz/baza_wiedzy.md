---
title: "Baza wiedzy"
date:  2024-02-11T15:30:00+00:00
description: "Baza wiedzy dla chętnych, zainteresowanych rozwojem zawodowym w kierunkach SysOps, DevOps, SecOps."
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
- baza wiedzy
image: images/2024-thumbs/kb.webp
---
### Dla chętnych, zainteresowanych rozwojem zawodowym w kierunkach SysOps, DevOps, SecOps.

#### 1. **Źródła i literatura GNU/Linux**

🌐 [System operacyjny Linux (Wersja 2.2.12) - Podręcznik](https://students.mimuw.edu.pl/SO/LinuxPodrecznik/index.html)
🌐 [Świetne źródło do nauki Linux](https://wazniak.mimuw.edu.pl/index.php?title=Systemy_operacyjne )
🌐 [HowtoForge - świetne tutoriale](https://www.howtoforge.com/)
🌐 [moja strona](https://sysadmin.info.pl)
🌐 [Jakub Mrugalski -  - Fachowiec od Linux. Świetnie zna tematykę OSINT.](https://mrugalski.pl/)
🌐 [Kursy sprzedawane przez Arka Siczka. Znam i polecam.](https://asdevops.pl/)
🌐 [AWS EC2 Do nauki własnej. Można założyć konto na AWS i przez pierwszy rok sporo rzeczy jest za darmo: ](https://aws.amazon.com/ec2/)
🌐 [VPS dla pasjonatów](https://mikr.us/)
🌐 [Chris Titus](https://christitus.com/categories/linux/)
🌐 [Udemy - kursy Linux](https://www.udemy.com/courses/search/?src=ukw&q=Linux)

#### 2. **Darmowy serwer SSH.**

📌Projekt FROG to darmowa oferta małych (malutkich!) serwerów VPS przeznaczonych do nauki administracji serwerami, hostingu prostych aplikacji (np. checki, crony) i hostowania niewielkich stron WWW. Serwery są darmowe, ale wymagają wpłaty dowolnej kwoty (np. 5zł) w ramach weryfikacji tożsamości użytkownika. Jest to opłata jednorazowa. Możesz posiadać tylko JEDEN darmowy serwer w usłudze FROG. 🐸 [Frog](https://frog.mikr.us/)

#### 3.  **Chcesz się uczyć chmury (cloud), ale zastanawiasz się jak zacząć?**

   ✅ Przede wszystkim, pamiętaj o wersjach trial. Każdy, znaczący dostawca chmury oferuje na start konkretną kwotę, którą możesz wykorzystać, by za darmo sprawdzić podstawowe funkcjonalności. Nie ma zatem problemu, by w ramach wersji trial uruchomić serwer lub wybraną usługę i "pobawić się" ustawieniami.

   ✅ Na dzień dzisiejszy, oferta trialowa Microsoft Azure obejmuje $200 kredytu, które możesz wykorzystać w dowolny sposób przez pierwsze 30 dni od momentu rejestracji. Po wykorzystaniu, będziesz płacić tylko za to, co przekracza darmowe limity poszczególnych usług. Microsoft Azure oferuje również szereg usług, które są darmowe przez pierwszy rok lub przez 750 godzin użytkowania, w zależności od tego, co nastąpi wcześniej.

   ✅ Google Cloud Platform w skrócie GCP oferuje 90-dniowy darmowy okres próbny z kredytem w wysokości $300

   ✅ AWS udostępnia 12-miesięczny okres próbny z różnymi darmowymi poziomami usług, w tym t2.micro instancję serwera ogólnego przeznaczenia.

   ✅ Jak już uruchomisz wersję trial to pamiętaj o darmowych tutorialach, które oferuje każdy z dostawców chmury. Z tymi poradnikami będzie Ci łatwiej wystartować.

#### 4. **Jeśli nie chmura, to może własny homelab?**

📌 Hardware, czyli to, co ważne. Liczy się każda kilowatogodzina. Zatem szukamy rozwiązań energooszczędnych.

   ✅ Raspberry Pi 4 lub 5. Można zbudować własny klaster Kubernetes. Polecam K3S, gdyż wspiera procesory ARM i bez problemu można go zainstalować. Szczegóły znajdziecie na [mojej stronie](https://sysadmin.info.pl). Energooszczędne rozwiązanie. Plus ma przewagę nad innymi ze względu na porty GPIO i możliwość nauki mikroelektroniki. Jeśli kogoś interesuje mikroelektronika, to polecam zainteresować się ESP32 oraz Arduino. Są to znacznie tańsze rozwiązania i pozwalają na naukę IoT bez ponoszenia wielkich wydatków.

   ✅ DELL WYSE 5070 thin client
      Terminal wyposażony w procesor Intel jest określany jako najlepsze i najbardziej energooszczędne rozwiązania przy zachowaniu stosunkowo dobrej ceny i możliwości, a jednocześnie nie zrujnuje rachunkami za energię elektryczną. Przeczytaj artykuł: [Dell Wyse 5070 gdy chcesz czegoś więcej](https://hejdom.pl/blog/22-home-assistant/965-home-assistant-sprzet-dell-wyse-5070-gdy-chcesz-czegos-wiecej.html)

   ✅ [Porównanie dwóch powyższych rozwiązań](https://browser.geekbench.com/v5/cpu/compare/9792492?baseline=8704648)

   ✅ HP T630 
      Ma dwa dodatkowe sloty m.2 w porównaniu do DELL WYSE 5070. Jest nieco tańszy od DELL WYSE 5070 i wydaje się lepszym rozwiązaniem ze względu na wspomniane sloty. 

   ✅ Fujitsu ESPRIMO Q920 
      Cena zbliżona do DELL WYSE 5070. Niestety w porównaniu do DELL WYSE ma tylko 16 GB RAM. Używam w domu.

   ✅ Intel NUC
      Cena zbliżona do DELL WYSE 5070.

   ✅ Jakikolwiek sensowny thin-client lub coś zbliżonego do Intel NUC, lub Raspberry Pi.

Porównanie poszczególnych modeli wymienionych wyżej: [https://www.hardware-corner.net/compare/Dell-OptiPlex-5070M_vs_Fujitsu-Esprimo-Q920/](https://www.hardware-corner.net/compare/Dell-OptiPlex-5070M_vs_Fujitsu-Esprimo-Q920/). Z rozwijanej listy można wybrać modele i porównać między sobą.

Podsumowanie: Oczywiście są wersje dużo droższe. Wszystko zależy od budżetu. Tu chodzi o coś, co będzie w stanie pracować 24h na dobę, nie będzie hałasować i zużycie prądu zamknie się w kosztach ~ 200 PLN lub mniej rocznie.

#### 5. **Wirtualizacja, czy konteneryzacja?**

📌 Podejścia są dwa: wirtualizacja, gdzie w grę wchodzi kilka rozwiązań komercyjnych i jedno darmowe, które jest dobrze rozwijane. 

   ✅ Wirtualizacja - darmowe rozwiązania
      🌐 [Proxmox](https://www.proxmox.com/en/proxmox-virtual-environment/comparison)
   
   ✅ Wirtualizacja - płatne rozwiązania (komercyjne)
      🌐 [VMware vSphere](https://www.vmware.com/products/vsphere.html) (
      🌐 [darmowe ESXi się skończyło :(](https://blogs.vmware.com/cloud-foundation/2024/01/22/vmware-end-of-availability-of-perpetual-licensing-and-saas-services/) )
      🌐 [Oracle Linux KVM](https://www.oracle.com/virtualization/)
      🌐 [Citrix Hypervisor](https://www.citrix.com/downloads/citrix-hypervisor/)
      🌐 [SUSE Linux Enterprise Server](https://www.suse.com/pl-pl/products/server/)
      🌐 [Red Hat Virtualization](https://access.redhat.com/products/red-hat-virtualization)
      🌐 [Microsoft Azure Virtual Machines](https://azure.microsoft.com/en-us/products/virtual-machines)
   
   ✅ Konteneryzacja
      🌐 [Docker](https://www.docker.com/)
      🌐 [Docker Swarm](https://docs.docker.com/engine/swarm/key-concepts/)
      
   ❇️ Kubernetes
      🌐 [K8S](https://kubernetes.io/)
      🌐 [K3S](https://k3d.io/)
      🌐 [Minikube](https://minikube.sigs.k8s.io/docs/)
      🌐 [MicroK8s](https://microk8s.io/)
      🌐 [KinD](https://kind.sigs.k8s.io/)
      🌐 [KOS](https://docs.k0sproject.io/v1.27.2+k0s.0/)

   ❇️ Narzędzia dla Kubernetes
      🌐 [Kubeadm](https://kubernetes.io/docs/reference/setup-tools/kubeadm/)
      🌐 [Rancher](https://www.rancher.com/)
      🌐 [Portainer](https://www.portainer.io/)
      🌐 [Kubeflow](https://www.kubeflow.org/)
      🌐 [K9S](https://k9scli.io/topics/install/)
      🌐 [Octant](https://octant.dev/)
      🌐 [Kustomize](https://kustomize.io/)
      🌐 [Helm](https://helm.sh/)

   ❇️ Monitoring i cybersecurity dla kontenerów
      ⭕ eBPF
         🌐 [bpftrace](https://bpftrace.org/)
         🌐 [Calico](https://www.tigera.io/project-calico/)
         🌐 [Cilium](https://cilium.io/)
         🌐 [Falco](https://falco.org/)
         🌐 [Pixie](https://px.dev/)
         🌐 [eBPF Applications Landscape](https://ebpf.io/applications/)
      ⭕ Inne narzędzia
         🌐 [Snyk](https://snyk.io/) - skupia się na identyfikacji i naprawie podatności w zależnościach, kontenerach i kodzie.
         🌐 [Trivy](https://trivy.dev/) - skanuje kontenery, systemy plików i repozytoria pod kątem problemów z bezpieczeństwem.
         🌐 [Knative](https://knative.dev/) - zarządza bezserwerowymi obciążeniami na Kubernetes, usprawniając wdrożenie i skalowanie.
         🌐 [Jaeger](https://www.jaegertracing.io/) - zapewnia rozproszone śledzenie dla monitorowania i rozwiązywania problemów z systemami opartymi na mikrousługach.
         
#### 6. **Automatyzacja**

✅ Automatyzacja - płatne rozwiązania (komercyjne)

   🌐 [Ansible](https://www.ansible.com/)
   🌐 [Ansible Tower](https://docs.ansible.com/ansible-tower/)

✅ Automatyzacja - darmowe rozwiązania

   🌐 [AWX](https://github.com/ansible/awx)
   🌐 [Ansible Semaphore](https://www.semui.co/)

#### 7. **CI/CD - Continuous Integration/Continuous Delivery**

🌐 [GitLab](https://about.gitlab.com/)
🌐 [Jenkins](https://www.jenkins.io/)
🌐 [TeamCity](https://www.jetbrains.com/teamcity/)
🌐 [Bamboo](https://www.atlassian.com/software/bamboo)
🌐 [GoCD](https://www.gocd.org/)
🌐 [IBM Urbancode](https://www.ibm.com/products/urbancode)
🌐 [CircleCI](https://circleci.com/)
🌐 [Bitrise](https://github.com/bitrise-io/bitrise)

#### **8. Code repositories**

🌐 [Git](https://git-scm.com/)
🌐 [Github](https://github.com/)
🌐 [Bitbucket](https://bitbucket.org/)
🌐 [Mercurial](https://www.mercurial-scm.org/)
🌐 [Fossil](https://fossil-scm.org/home/doc/trunk/www/index.wiki)
🌐 [Apache Subversion](https://subversion.apache.org/)

#### **9. Cybersecurity**

✅ Nauka

🌐 [Hack The Box](https://www.hackthebox.com/)
🌐 [Try Hack Me](https://tryhackme.com/)
🌐 [VulnHub](https://www.vulnhub.com/)
🌐 [HackerOne](https://www.hackerone.com/)

✅ Portale

🌐 [infosec writeups](https://infosecwriteups.com/)
🌐 [System Weakness](https://systemweakness.com/)
🌐 [OWASP](https://owasp.org/)

✅ Software

🌐 [Nmap](https://nmap.org/)
🌐 [PortSwigger](https://portswigger.net/)
🌐 [Exploit Database](https://www.exploit-db.com/)
🌐 [Wazuh](https://wazuh.com/)
🌐 [Suricata](https://suricata.io/)
🌐 [Snort](https://www.snort.org/)
🌐 [SonarQube](https://www.sonarsource.com/products/sonarqube/)
🌐 [Mend](https://www.mend.io/)
🌐 [Black Duck](https://www.synopsys.com/software-integrity/software-composition-analysis-tools/black-duck-sca.html)
🌐 [Sonatype Nexus](https://www.sonatype.com/products/sonatype-nexus-repository)

✅ Systemy operacyjne dla pentesterów

🌐 [Kali](https://www.kali.org/)
🌐 [Parrot Security](https://www.parrotsec.org/)
🌐 [BackBox](https://www.backbox.org/)
🌐 [Black Arch](https://blackarch.org/)
