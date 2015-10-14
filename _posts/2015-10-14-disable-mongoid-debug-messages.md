---
layout: default
title: Disable Mongoid Logger Permanently
---

Sejak mongoid update dari versi 4 ke versi 5, tiba2 aja semuanya berubah.
rails server dan rails console semuanya stdout mongoid debugging messages,
yang mengakibatkan proses debugging nya terganggu karna adanya anon messages yg spam setiap saat.
Oke deh langsung aja begini caranya.  

<br/>
pertama masuk ke directory gems, untuk mengetahui directory gem bisa pake command  
```
$ gem environment
```

lalu ```cd``` ke gem list, dan masuk ke gems mongo-ruby-driver  
dan edit logger.rb file nya  
```
$ cd gems/mongo-*/lib/mongo
$ vim logger.rb
```

lalu edit pada method default_logger sehingga menjadi seperti ini    
```ruby
def default_logger
    logger = ::Logger.new($stdout)
    logger.level = ::Logger::FATAL
    logger
end
```