---
layout: default
title: upgrade libc6 2.19 pada crunchbang waldorf!
---

dulu waktu awal ngoding rails belom pernah tau sih gimana caranya manggil data dari secrets.yml, trus pake cara manual buat manggil nya kurang lebih begini.   

```ruby
YAML.load(File.open('#{Rails.root/config/secrets.yml}'))
```




nah trus fungsi manual buat calling secrets based on env gw panggil dimana2 di controller model dan lain nya. udah susah2 bikin eh ternyata si rails punya helper buat calling rails secrets langsung. (kapret)


manggilnya cuma begini



```ruby
Rails.application.secrets.key
```


ntap nya doi bakalan manggil secrets based on current env, misalnya lagi di development doi bakalan panggil secrets key di dev env.



udah gitu aja, ga penting sih sharingnya. cuma buat ngingetin gua doang sih.


