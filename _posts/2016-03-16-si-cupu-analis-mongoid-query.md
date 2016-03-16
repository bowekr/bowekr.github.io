---
title: Iseng benchmarking mongoid query ala newbie
layout: default
---

Goal: Menampilkan hanya 1 filed yang di butuhkan  
Test Methods: Pluck, Distinct, & Only  
DB Collections: 4 items  

```ruby
Benchmark.bm do |x|
  x.report { Post.all.pluck "id" }
  x.report { Post.all.distinct "id" }
  x.report { Post.all.only "id" }
end
```

```
    user     system      total        real
0.000000   0.000000   0.000000 (  0.007666)
0.000000   0.000000   0.000000 (  0.001932)
0.000000   0.000000   0.000000 (  0.000139)
```

Whats going on?
Lets Explain



###Pluck  
----
pada dokumentasi mongoid tertulis : `Get all the non nil values for the provided field.`
yap, tugasnya pluck adalah mengambil data record dari collection,
lalu mereturn array of spesifik field yang valuenya tidak nil,
jika valuenya nil, mongoid akan skip record tersebut dan berjalan maju hingga menemukan field yang valuenya available.

But gue menemukan fact, pluck ternyata juga mereturn nil dalam array nya  

```ruby
Post.pluck(:name)
=> [ "bowo", nil, nil "owob" ]
```

mungkin bisa dilihat source code pluck ini seperti apa, tapi pada article ini gue engga akan coba sampe sana.

<br />
<br />
<br />

##Distinct
----
pada dokumentasi mongoid tertulis : `Get a list of distinct values for a single field.`
simplenya distinct akan remove duplicate value, dan mereturn hanya 1 yang distinct, contohnya
anggap kita punya field :nama, pada record pertama nama: "bowo", record kedua nama: "bowo"
lalu kita run distinct

remember distinct dan pluck sama2 mereturn array

```ruby
Post.distinct(:name)
=> [ "bowo" ]
```
<br />
<br />
<br />


##Only
----
pada dokumentasi mongoid tertulis : `Return only selected fields of each records`
penjelasan pada qoute di atas sepertinya sudah menjelaskan mungkin short of code ini bisa nambahin

```ruby
Person.only(:name, :age)
=> Mongoid::Criteria
```

yap instead mereturn langsung object array, method only ini hanya mereturn Mongoid::Criteria class,
untuk transform nya menjadi array, kita butuh `mapping` atau `each`

Lohlohhhh, sebentar dulu wo, tujuan artikel ini kan buat query dan mereturn array langsung, tapi ini kok malah musti each dan mapping lagi ga fair dong namanya.

Ok karna only ini mereturn criteria instead langsung array maka kita coba compare lagi dengan array
test kali ini gw coba pake 18 data record, dan dengan tambahan benchmark yaitu memory consumption

```ruby
Benchmark.bmbm do |x|
  x.report { Post.all.pluck(:id)           }
  x.report { Post.all.distinct(:id)        }
  x.report { Post.all.only(:id).map(&:id)  }
  x.report { Post.all.only(:id).each(&:id) }
end
```

Result :

```
Rehearsal ------------------------------------
   0.000000   0.000000   0.000000 (  0.002182)
   0.000000   0.000000   0.000000 (  0.010644)
   0.000000   0.000000   0.000000 (  0.001593)
   0.000000   0.000000   0.000000 (  0.001500)
--------------------------- total: 0.000000sec

       user     system      total        real
   0.000000   0.000000   0.000000 (  0.001270)
   0.000000   0.000000   0.000000 (  0.002086)
   0.000000   0.000000   0.000000 (  0.002590)
   0.000000   0.000000   0.000000 (  0.002631)
```


So udah liat sendiri kan perbedaan masing2 method, jadi gunakan method tersebut sesuai kebutuhan.
Btw ini cuma analisis amatiran ala gue, mudah2an membantu
