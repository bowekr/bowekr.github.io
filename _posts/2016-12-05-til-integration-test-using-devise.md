---
title: (TIL) Login devise pada integration test
layout: default
---

kemarin mau coba highlevel test dengan mencoba integration test, cuma kendalanya adalah app yang sekarang gw mau test pake devise sebagai auth system, so jadi waktu mau test yg mengharuskan gw harus login jadi gagal deh.

so hasil seraching2 dan mencoba,
dan ternyata hasilnya mudah.


try this pada before block  
```ruby
user = create(:user) # FactoryGirl
post_via_redirect user_session_path, user: { email: user.email, password: user.password }
```


dan jeng jeng.