---
layout: default
title: upgrade libc6 2.19 pada crunchbang waldorf!
---
coba2 pake distro yang katanya ubuntu based paling 'ringan'.
jajalin install android emu di crunchbang, install vbox, install, download genymotion.
lanjut running si geny, nah pas running. libc6 ga support. katanya musi pake yg v >= 2.15
googling sana sini akhirnya nemu juga di stackoverflow.  
1. musti exit display manager, ctrl + alt + f1
2. add ke sources.list
```bash
deb deb http://ftp.debian.org/debian sid main
```

3. update package, # apt-get update
```bash
#apt-get install libc6
```

4.profit
