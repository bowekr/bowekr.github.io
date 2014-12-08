---
layout: default
title: Cable Unplugged .
---
Abis clean install Ubuntu 14.04, terus tiba-tiba wired network disconnect, lanjut gw buka aja Network, pas liat disana ternyata eth0 Cable Unplug, padahal kabel sama port ethernet work fine di windows. bingung kan nih ceritanya.


gw coba2 berbagai macam cara ( ifup, ifdown, ifconfig ) setting macem-macem ttp aja ga status masih unplug, dengan semangat 45 gw terus bejuang mencari solusi, dapet lah 1 artikel di forum ubuntu. disana tertulis gw harus compile driver eth0 gw ( RTL8111 | Chipset G41 ). okelah gue download source code driver dari official site, dengan harapan bakalan fix + semangat 45, gue klik lah tuh tomvol download, ternyata kaga bisa di download, servernya dobol.


gue searching aja filename nya di google, hasilnya dapet dari [repo archlinux](https://aur.archlinux.org/packages/r8168-all/ "Archlinux")
lanjuttt gw extract lalu gw running scriptnya 

```
$ ./autorun.sh
```


anddd doi auto make, compile, dan install ke kernel. setelah reboot, fualaaaaaaaaah internet nya working lagi. seneng beet, langsung gw install legacy drivernyaa, daaan waktunya ga cukup karna gue harus pergi kerumah vieri buat gajian.


dan ini tulisan gw tulis dirumah vieri, bocah pada nyanyi + ngobrol, gw malah ngetik artikel wkwkwkwkw.
