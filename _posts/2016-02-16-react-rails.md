---
layout: default
title: React-Rails
---


Ya udah hampir 2 bulan ini gue di tugaskan untuk megang ReactJS pada RailsApp kantor gue,
jadi tugas gue yaitu converting semua frontend ke react component,
ya waktu itu jujur pengetahuan frontend gue masih sangat minim, maklum lah start belajar coding pake ruby soalnya jadi engga nyentuk sama sekali tuh yang namanya Javascript.


Oke berbekal pengetahuan minim, gue pun tertantang untuk mencoba untuk menyanggupi Task dari bos gue,
Sheeeet, ketak ketik ketak ketik, baca official document ReactJS, coba sebentar, langsung ngerti, Chakep nih feeling gue.

"Ok, ReactJS udah faham konsepnya, sekarang bagiamana cara integrate ke rails project" bisik gue,
gue pun langsung nanya sama mbah "react on rails" , emang dasar si mbah ini pengalaman banget, tau aja apa yang gue butuhin gitu,
di bawalah gue sama si mbah ke github pages nya (react-rails)[https://github.com/reactjs/react-rails], emang pengertian dah.


Oke setelah gue di bawah ke pagesnya react-rails gue coba baca README pada halaman depan nya, ga sampe 10 menit gue langsung paham cara kerja gemfile ini, dan gue langsung decide untuk pake ini ke project kantor gue,
sebelum gue pake ke project, gue biasanya mastiin dulu ke bos gue minta pendapat perihal react-rails ini, "Mas, untuk react di rails nya kita pake gem atau pakai assets saja ya?" tanya gue ke bos, "Pakai gem saja" jawab bos gue. YAY!!

Yop seperti biasa juga sebelum implementasi sesuatu ke project vital atau real project, gue coba dulu ke project dummy dan gue harus pastiin kalo emang gem ini bener2 worth untuk di pake ke main project,
abis nyoba, besoknya gue langsung pake gem itu ke project kantor dan hasilnya lumayan membantu, react-rails ini punya UJS, jadi dia bikin helper sendiri gitu untuk view, jadi kalo lo mau render component pada view yang lu ingin, lo ketik begini ```<%= react_component 'NamaComponent', props: value %> ```
Gampang kan? Yoi,  dan satu lagi yang gue suka dari react-rails ini nih, dia bisa melakukan prerender component hanya dengan passing parameter ```prerender: true``` SEO friendly banget sob kalo pake opsi ginian.


sejauh ini sih gue belom explore terlalu jauh si react-rails ini, karna kebutuhan gue hanyalah untuk transforming JSX to JS dan Rendering Component aja, ibarat Leave By Default.
Oke segini dulu deh cerita react-rails nya, See you soon,

Thanks for reading






