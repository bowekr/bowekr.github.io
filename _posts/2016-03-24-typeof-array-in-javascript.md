---
title: typeof([]) == Object, Whaaat ?
layout: default
---

ketika kita working dengan bahasa yang datatype nya dynamic, kadang kita ingin mentetahui or validate 'apa sih tipe data object ini' in javascript kita bisa menggunakan special keyword yaitu `typeof()`, but muncul keanehan ketika gue coba ngecek datatype array in javascript, dan ternyata mereka kasih gue `'object'`, dan gue berfikir hmm what happening, dan gue coba searching bagaimana array ini terbentuk, dan berikut hasilnya

Test Example


```javascript
typeof([])
'object'
```



for example we have this array

```javascript
['a', 'b', 'c']
```

in deep javascript ini yang mereka lakukan pada array kalian


```javascript
{
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3,
  __proto__: {
    slice: function()
    __proto__: {
      toString: function()
    }
  }
}
```


ya bisa kalian lihat sendiri array seperti sebuah hash mereka punya key dan value
index nya berupa number, so ketika kita pangggil arr[0]
javascript akan merefrensikan object ketika di panggil index / key dari objectnya.
dan disana juga ada proto, itu sebuah helper yang biasa kita pake untuk chaining method seperti

```javascript
['a','b','c'].toString().toUpperCase();
```

