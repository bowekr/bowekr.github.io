---
title: UTS Tugas Algoritma Pemrograman
layout: default
---

A) Penjelasan Program
Ya sesuai judul program yang saya buat kemarin, yaitu membuat Aplikasi Laundry untuk owner laundry.
yang mana inputnya yaitu :  



- id : unique int (auto generated)
- nama : string
- beratKg : int
- tanggalOrder : Date (auto generated)
- potonganHarga : int (auto generated)
- harga_per_kg : int



sesuai kemaren pada kertas uts, ini saya implementasi dalam bentuk program, nah untuk program nya sendiri saya pake java main class, dan penambahan class baru yaitu "Order",  



untuk fitur nya itu sendiri, pada aplikasi laundry ini punya fitur potongan harga, yang mana apabila beratKg >= 5Kg maka akan mendapatkan potongan harga sebanyak 5.000, dan apabila beratKg >= 10Kg maka akan mendapatkan potongan sebesar 10.000 tidak berlaku untuk kelipatan (saya limit).



berikut screenshoot program yang sudah saya buat yang sudah running well (run mode):


![Output Hasil](https://www.dropbox.com/s/4rv1appeswi1tdi/PROGRAM%20JADI.jpg)



C) Source Code

```java
import java.util.Date;
import java.util.Scanner;
/*
  Nama: Arief Wibowo Wicaksono
  NIM: 161021450104
  KELAS: 01TPLP001 (Reguler A)
  TUGAS: [UTS] Membuat Program

  JUDUL: Aplikasi Laundry.
*/

class Order {
    public static final int HARGA_PER_KG = 7000;
    public static final String NAMA_TOKO = "CEMERLANG LAUNDRY";
    private double id;
    private String nama;
    private int beratKg;
    private Date tanggalOrder;
    private int potonganHarga = 0;
    
    // Constructor
    public Order(String namaPenerima, int berat) {
        id = Math.random();
        nama = namaPenerima;
        beratKg = berat;
        tanggalOrder = new Date();
    }
    
    public int getTotalHarga() {
        int totalHarga = this.beratKg * HARGA_PER_KG;
        int potonganHarga = 0;
        
        // Jika berat lebih dari 5Kg dapat potongan 5rb
        if (this.beratKg >= 5) {
            totalHarga -= 5000;
            this.potonganHarga = 5000;
        // JIka berat lebih dari 10kg dapat potongan 10ribu.
        } else if (this.beratKg >= 10) {
            totalHarga -= 10000;
            this.potonganHarga = 10000;
        }
        
        // Jika tidak masuk kondisi maka langsung di return totalHarganya.
        return totalHarga;
    }
    
    public void printStruk() {
        System.out.println(NAMA_TOKO);
        System.out.println("------");
        System.out.println("ID ORDER: " + this.id);
        System.out.println("NAMA: " + this.nama);
        System.out.println("BERAT: " + this.beratKg);
        System.out.println("TANGGAL ORDER: " + this.getTanggalOrder());
        System.out.println("------");
        System.out.println("HARGA PER KG: " + HARGA_PER_KG);
        System.out.println("RINCIAN: " + this.beratKg + "Kg"+ " * " + HARGA_PER_KG);
        System.out.println("-------");
        System.out.println("-----POTONGAN HARGA: " + this.getPotonganHarga());
        System.out.println("TOTAL HARGA: " + this.getTotalHarga() );
    }
    
    /*
        GETTER SETTER
    */
    public String getNama() {
        return this.nama;
    }
    
    public int getBeratKg() {
        return this.beratKg;
    }
    
    public String getTanggalOrder() {
        return this.tanggalOrder.toString();
    }
    
    public double getId() {
        return this.id;
    }
    
    public int getPotonganHarga() {
        return this.potonganHarga;
    }
}

/** MAIN CLASS **/
class Main {
     public static void main(String[] args) {
         System.out.println("WELCOME TO CEMERLANG LAUNDRY");
         System.out.println("SILAKAN INPUT ORDER");
         System.out.println("------------------------");
         Scanner input = new Scanner(System.in);
         
         System.out.print("Nama Binatu: ");
         String namaBinatu = input.nextLine();
         
         System.out.println("------");
         
         System.out.print("BERAT PAKAIAN: ");
         int beratPakaian = input.nextInt();
         
         
         Order order = new Order(namaBinatu, beratPakaian);
         order.printStruk();
         
     }
}
```