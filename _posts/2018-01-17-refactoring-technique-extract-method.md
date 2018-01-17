---
title: Refactoring Technique Extract method
layout: default
---
Banyak jalan menuju roma, mungkin bisa di bilang begitu dalam dunia programming, kalo kalo ga bisa pake int, bisa pake string, kalo ga bisa pake array, bisa pake hash, kalo ga bisa pake hash, bisa pake tuple, dan seterusnya sampe kiamat, sebenernya tujuannya satu, cuma cara nya aja yang beda, BETUL!   


Dari sekian banyak cara, mana sih yang paling baik dan bagus? GOOD QUESTION!


consider code ini




```ruby
class UserController
  ...

  def index
    user = User.find(params[:id])

    if user.status == "active"
      redirect_to dashboard_path
    else
      render :index
    end
  end
end
```


kalo di liat dari code nya, disana kita melakuka pengecekan kondisional, jika user status "active", maka redirect user ke dashboard.


ada yang ngerasa ga kalo statement kondisional nya agak kurang representatif?
masih belum ya?, Oke sekarang kita ubah spesifikasi program nya, katakanlah gw mau nambahin satu atau dua statement lagi di dalam kondisional tersebut, katakanlah user harus berumur di atas 17 taun baru dapat masuk ke dashboard, jika di buat code maka menjadi seperti ini


```ruby
...
  if user.status == "active" && user.age > 17
    redirect_to dashboard_path
  else
    render :index
  end
end

## or this

  if user.status == "active" && user.age > 17 || user.posts.count > 1 # dst
    redirect_to dashboard_path
  else
    render :index
  end
```


apa yang lo rasain ketika baca kode di atas? berapa lama kalian bisa pahamin kondisionalnya? 2 menit? 1 menit?



how about this


```ruby
class User
  def active?
    self.status == "active"
  end

  def adult?
    self.age > 17
  end
end

class UserController
  def index
    ...
    if user.active? && user.adult?
      ...
    else
      ...
  end
end
```


sekarang begimana baca kode nya? lebih cepet dari sebelumnya kah?



Yes ini namanya extract method, jadi sebisa mungkin statement atau kondisional statement kalian itu di extract jadi single method yang responsible buat check statement, selain lebih mudah di baca, juga lebih mudah dalam perubahan code, 



misalnya gw mau ganti string "active" jadi "activated", kalo pake cara lama yang contoh sebelumnya, gw bakalan mengganti hampir semua file yang menggunakan statement sejenis, mengganti "active" menjadi "activated", nah dengan cara ini, gw cukup mengganti 1 method aja, langsung mengubah seluruh statement yang menggunakannya, easy bukan? bahkan kalian juga bisa buat method untuk lawan kata dari method yang kalian buat,
contoh gw mau bikin statement untuk inactive




```ruby
# avoid menggunkaan seperti ini, ini malah jadi bikin bingung lagi.
# instead using NOT operator, kita bisa extract ke dalam object class nya.
def index
  if !user.active?
    ..
  else
    ..
  end
end

## menjadi seperti ini
def User
  def active?
    self.status == "active"
  end

  def inactive?
    !active
  end
end

## dan lebih mudah di baca
  if user.inactive?
    ...
  else
    ...

```


So sebisa mungkin extract kondisional statement kalian jadi sebuah method apapun itu context nya, dengan mengextract sebuah statement, kode kita juga telihat jadi lebih bersih dan mudah di baca,. :)
