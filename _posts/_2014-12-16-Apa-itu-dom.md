---
layout: default
title: Apa itu DOM ?
---
##### DOM  
Atau "__*Document Object Model*__"  
sebuah struktur tree html yang di buat oleh browser.  
ketika kita membuka sebuah webpage, browser mulai 'get' HTML dari webpage, nah HTML ini akan di load oleh browser piece by piece menjadi sebuah __*DOM*__, ibaratnya DOM itu seperti silsilah keluarga, mulai dari kepala keluarga hingga anak, dan cucu,  
yang termasuk DOM adalah dokumen HTML, seluruh elemen HTML, dan atribut dari elemen HTML, serta teks di dalamnya.

##### Seperti Apa sih DOM ?  
oke gue kasih example, contoh kita punya document html sebagai berikut :  
```html
<!DOCTYPE HTML>
<html>
  <head>
    <title> Giff Me Mana </title>
  </head>
  <body>
    <h2> Giff me Buff </h2>
  </body>
</html>
```  

__DOM RESULT__  
```
|-- DOCUMENT
   |-- HTML
   |   |-- HEAD
   |     |-- title
   |       |-- Giff Me Mana
   |-- BODY
       |-- H2
         |-- Giff Me Buff
```  

udah paham sekarang ?
