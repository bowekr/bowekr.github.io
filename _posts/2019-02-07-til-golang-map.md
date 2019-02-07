---
date: 2019-02-07 09:03:14 +0000

---
---
title: TIL Golang Map
---

TIL

Pada data struktur Map, default key order yang di hasilkan tidak berdasarkan insertion order, melainkan random .  

```go

func main() {

  users := map\[string\]string{

    "color": "Blue",

    "size": "Big",

  }

  for _, v := range users {

    fmt.Println(v)

  }

}

```

output hasil println akan berbeda2 ordering nya.