---
title: TIL: Redirect to current_page after login with Devise gem
layout: default
---
Tadi abis makan siang, kepikiran gimana ya kalo user klik tombol yang mengharuskan user itu login, nah ketika user itu klik login, maka page akan redirect back ke tempat dimana user itu di prompt untuk login.


nah tadi cari-cari akhirnya ketemu juga caranya, ternyata devise sudah menyediakan method ini (capedes).


tambahkan method ini pada ```application_controller.rb```

```ruby
  def after_sign_in_path_for(resource)
    stored_location_for(resource) || root_path # ganti root_path dengan apapn sebagai alias
  end
```
