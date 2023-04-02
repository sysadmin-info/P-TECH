---
title: "Welcome to the P-TECH website"
date:  2023-04-01T08:08:59+00:00
description: "Welcome to the P-TECH website. The lab section contains exercises and the theory needed to complete the exercises. As opportunities arise, the site will be expanded to include more workshops, exercises and theory."
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: admin
authorEmoji: 🐧
pinned: true
tags:
- P-TECH
series:
-
categories:
- general
image: images/2023-thumbs/linux-cli.webp
---
In class, we use virtual machines built from an AWS template. Why AWS and not Virtual Box virtual machines? For several reasons. First of all, it is very problematic to set up a web/www server on a virtual machine. For a simple reason. You need to know if it's possible to put up a virtual machine using a virtual bridge hooked up to our network card to the world, and how to set up port forwarding on the router so that traffic from ports 80 and 443 is forwarded to our computer and then to the virtual machine. Secondly, the price - free 750 hours of machines under the so-called "free tier" and thereafter the unit price per t2.nano machine is $0.0051 per hour of one virtual machine. Easier to expose content to the world after installing a web server (Apache2/Nginx). Although in practice, having a VPS, this is done differently and will be covered in the class. There are at least several ways to build sites and applications, and I won't have time to show them all. Speed, simplicity. The disadvantages of AWS? The inability to easily put up your own DHCP or DNS, because AWS performs these services automatically and provides them as a ready-made solution. It can be solved, while it is complicated. Hence, in addition, I am going to look around for a solution to configure the DNS server and DHCP as it is done according to good practices. For each class, I will prepare a solution in such a way as to allow you to do the exercises, or at least their presentation according to the rules. Please keep in mind that there is more than one solution, and it is up to you which one you choose. I encourage you to learn and practice on your own by repeating the exercises, commands and understanding what you are doing. Have fun learning!
