---
title: TIL Rails Custom Validator
layout: default
---

Welcome,  
Ya kemarin gue habis ngerjain task, dimana task ini gue harus mem-validasi sebuah hash inside array,
mulai dari size array-nya, size hash inside array-nya, key dari hashnya, value dari hash nya,
dan itu semua harus gw buat validasinya atau policy nya, paham kan? belum?  


Oke fine, gue tau lo pasti belum paham, nih gue kasih contoh kasus deh, gini-gini  
fikirkanlah sebuah sayur asem, ya lu bayangin aja tuh sayur,
anggap disini kita lagi mau buat sayur asem yang paling enak sedunia, dimana ingredients nya sbb :  


```
Perfect Tamarind Vegetable Soup ( kata google translate )
Asem : 2 Butir
Melinjo : 1 Renceng
Daun Salam : 2 Helai
Belimbing Sayur : 2 Buah
Garam : 1 Sendok Mecin
```


Ini cuma contoh ya ga usah protes kalo ga ada labu nya, ga penting juga ada labu nya
ga di makan juga kan sama lo, paling lo nyeruput aer nya doang ama jagung nya yakan? ngaku looo!!


Oke sambil nungguin lo ngaku, kita lanjut contoh nya,  
Ehemm.. next kita buat semua ingredients ini menjadi hash dan array value
kurang lebih bakalan menjadi kaya begini :


```
[
    { asem: 2 },
    { melinjo: 1 },
    { daun_salam: 2 },
    { belimbing_sayur: 2 },
    { garam: 1 }
]
```


Mau protes lagi? ga usah lah ya, lama2in gue nulis doang nanti :D
Oke disini bisa kita lihat, schema dari formatting nya,


Nah seperti yang pertama udah gw jelasin, disini gw harus mem-validasi size array,
hash key, dan value nya jadi ibaratnya ini jumlah semua ingredients untuk sayur asem harus ada 5, kalo lebih dari lima namanya bukan sayur asem, tapi sayur lodeh atau sayur sop, loh!!,
yap bener banget, gue harus validasi untuk membuat sayur asem itu harus ada 5 bahan,
bahan disini juga harus benar, harus ada asem nya, dan harus 2 jumlah nya, jika lebih dari dua, maka sayurnya gagal,
begitupula dengan bahan2 yang lain nya,   


Namun ga cuma sampe situ aja validasi nya, gue juga harus buat validasi ini lebih modular,
misalnya dari bahan saur asem di atas, gimana caranya itu juga bisa di aplikasikan untuk membuat sayur lodeh dan sayur sop,
tanpa mengubah base atau strukturalnya, bingung kan? sama gue juga bingung.

Oke, How? Gimana caranya gue mengaplikasikan ini ke Rails ?  
Tunggu posting gue selanjutnya, babay :D

