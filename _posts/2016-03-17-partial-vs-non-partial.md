---
title: Partial Render vs Non Partial Performance
layout: default
---

Partial Render Performance vs Non Partial Render

satu kata buat hari ini, 'not bad' begitulah kira2 bunyinya.
Oke back to topic, kali ini gue bukan lagi mau ngebahas apa yang gue rasain hari ini,
bukan juga ngebahas hp gw yang udah rusak LOH!, Tapi kali ini kita ngebahas.
Trererreeett JENG-JENG `Partial Render vs Non Partial Render Performance Pada Rails`..



Yak setelah task atau kerjaan gw sudah mencapai titik Frontend, disinilah gue baru merasakan aroma2 pain and gain nya frontend engineer, salah satunya dalam masalah performance.

Back to Topic, gue mau ngasih comparison perbandingan yang gue rasakan ketika menggunakan Partial, atau tidak dengan Partial view, di rails biasanya kita menggunakan partial agar view kita bisa di Reuse dengan komponen lain atau dalam segi Konsistensi. Yak partial emang menjadi solusi buat 2 masalah ini. tapi Bagaimana performancenya?

Oke kali ini gue mencoba rendering partial `jbuilder`, buat yang engga tau apa itu jbuilder bisa main2 dulu ke ke rumahnya si jbuilder (disini)[https://github.com/rails/jbuilder] baca2 dulu biar paham, kalo udah paham ajarin yang laen biar jadi orang yang berguna okeh? LOHH!, untuk contoh kali ini gw coba buat sample json format, kurang lebih begini schema nya

```javascript
{
  post_id: "string",
  poster_id: "string",
  poster_name: "string"
}
```

nah schema di atas gw taro di dalam folder `shared` di `view`, lalu HomeController merender nya sebagai partial dari file home.json.jbuilder, kurang lebih begini code nya

```ruby
# /home/home.json.jbuilder
{
  json.partial! 'shared/post', locals: { post: @new_post }
}
```

ga usah pake nanya apa kenapa ada syntax locals disitu, dan gue yakin kalian pasti udah tau apa maksutnya.

lalu gue coba `GET` home.json itu dengan mengakses nya langsung lewat browser 'localhost:3000/home.json'
setelah gue mengaksesnya, gw coba buka rails server consolenya dan melihat time render nya dari sana,
FYI: untuk test kali ini gue menggunakan 10 data yang di gunakan dan dengan 3x refresh GET, dan berikut result nya :

```
Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:33:08 +0700
Processing by HomeController#home as JSON
  Rendered posts/_post.json.jbuilder (5.2ms)
  Rendered posts/_post.json.jbuilder (4.2ms)
  Rendered posts/_post.json.jbuilder (4.4ms)
  Rendered posts/_post.json.jbuilder (4.6ms)
  Rendered posts/_post.json.jbuilder (4.1ms)
  Rendered posts/_post.json.jbuilder (4.0ms)
  Rendered posts/_post.json.jbuilder (4.1ms)
  Rendered posts/_post.json.jbuilder (4.8ms)
  Rendered posts/_post.json.jbuilder (4.0ms)
  Rendered posts/_post.json.jbuilder (5.5ms)
  Rendered home/home.json.jbuilder (100.0ms)
Completed 200 OK in 144ms (Views: 121.2ms)


Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:33:13 +0700
Processing by HomeController#home as JSON
  Rendered posts/_post.json.jbuilder (4.6ms)
  Rendered posts/_post.json.jbuilder (4.1ms)
  Rendered posts/_post.json.jbuilder (4.1ms)
  Rendered posts/_post.json.jbuilder (4.2ms)
  Rendered posts/_post.json.jbuilder (4.1ms)
  Rendered posts/_post.json.jbuilder (4.7ms)
  Rendered posts/_post.json.jbuilder (3.9ms)
  Rendered posts/_post.json.jbuilder (6.7ms)
  Rendered posts/_post.json.jbuilder (5.0ms)
  Rendered posts/_post.json.jbuilder (4.3ms)
  Rendered home/home.json.jbuilder (107.4ms)
Completed 200 OK in 169ms (Views: 133.5ms)


Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:33:15 +0700
Processing by HomeController#home as JSON
  Rendered posts/_post.json.jbuilder (4.9ms)
  Rendered posts/_post.json.jbuilder (4.3ms)
  Rendered posts/_post.json.jbuilder (4.7ms)
  Rendered posts/_post.json.jbuilder (4.2ms)
  Rendered posts/_post.json.jbuilder (4.1ms)
  Rendered posts/_post.json.jbuilder (4.0ms)
  Rendered posts/_post.json.jbuilder (6.0ms)
  Rendered posts/_post.json.jbuilder (4.9ms)
  Rendered posts/_post.json.jbuilder (4.4ms)
  Rendered posts/_post.json.jbuilder (4.0ms)
  Rendered home/home.json.jbuilder (108.6ms)
Completed 200 OK in 156ms (Views: 132.3ms)
```

Total sekitar 160.1ms atau sekitar 0.1601 detik, cukup mengesankan, oke kita keep ini sebagai catatan lalu kita coba test lagi dengan tidak menggunakan partial, tapi kita ketik langsung di home.json.jbuilder nya.
schema nya begini

```ruby
# /home/home.json.jbuilder
{
  json.posts @posts.each do |post|
    json.post_id post.id
    json.poster_id post.poster_id
    json.poster_name post.poster_name
  end
}
```

back to browser, saatnya kita refresh browser, and result from rails server console

```
Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:30:40 +0700
Processing by HomeController#home as JSON
  Rendered home/home.json.jbuilder (85.2ms)
Completed 200 OK in 137ms (Views: 106.8ms)
```

ah masa kecil banget, coba di refresh lagi sampe 3x wo, Oke lets see


```
Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:31:15 +0700
Processing by HomeController#home as JSON
  Rendered home/home.json.jbuilder (85.1ms)
Completed 200 OK in 144ms (Views: 112.0ms)


Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:31:17 +0700
Processing by HomeController#home as JSON
  Rendered home/home.json.jbuilder (82.8ms)
Completed 200 OK in 129ms (Views: 106.8ms)


Started GET "/home.json" for 127.0.0.1 at 2016-03-17 21:31:18 +0700
Processing by HomeController#home as JSON
  Rendered home/home.json.jbuilder (84.9ms)
Completed 200 OK in 131ms (Views: 108.5ms)
```





## Partial Render :
### Pros
__*Konsistensi Schema*__
Dengan menggunakan partial template, schema json yang di return akan lebih konsisten, ketika partial itu di gunakan dimanapun schema akan tetap seperti itu, tidak berubah.

__*Easy to Maintain*__
Template dapat di gunakan dimana saja, sebagai contoh ada 10 pages yang mangambil partial post ketika kita ingin merubah schema nya, kita cukup merubah 1 file template saja.

__*DRY*__
Kering, WHAT? Don't Repeat Yourself.

__*Single Responsibility*__

### Cons :
__*Hard to customize*__
Ada satu kaskus dimana kita ingin menambahkan satu field tambahan untuk spesifik page, contohnya Page A menggunakan default partial, Page B ingin menggunakan partial tersebut tetapi dengan tambahan field price


## Non Partia

## Pros
__*Easy to Customize*__
Tiap2 page dapat menambahkan atau mengurangi field yang hanya mereka butuhkan saja.

### Cons
__*Schema tidak Konsisten*__
Ketika 10 page membutuhkan data yang sama atau schema yang sama, kita harus menulis kembali schema pada tiap2 pages yang membutuhkan data atau schema tersebut.

__*Ketika*__ schema tersebut ingin kita tambahkan field baru atau menguranginya, kita harus remove 10 other yang  membutuhkan schema yang sama

__*WET*__



ya kira2 begitulah hasil benchmarking dengan pikiran dangkal gue, Enjoy!