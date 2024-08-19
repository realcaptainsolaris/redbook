---
title: Firefox DNS LEAK VPN Setting
date: 20221223
author: realcaptainsolaris
---

# DNS LEAK
Firefox 129.x.x scheint einen DNS-Leak zu haben.

Abhilfe schafft:

    about:config
    network.trr.mode = 3

