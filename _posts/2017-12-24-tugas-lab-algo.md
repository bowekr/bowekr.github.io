---
layout: default
title: UTS Lab Alpro II
---

### Definisi Program yang di buat   
Ini adalah Prototype program Reservasi Restoran yang saya buat untuk Tugas UTS
Lab Algoritma dan Pemrograman II, Pak Agus selaku Dosen pengajar.   


Tujuannya dibuat program ini adalah, guna mempermudah Customer atau Pelanggan
untuk Reservasi tempat beserta Owner Tempat untuk manajemen Reservasi.




### Tampilan Program
![Tampilan Awal](https://www.dropbox.com/s/2dk2ue1la962q34/1.png?raw=1)


Ini adalah tampilan awal program interface nya menggunakan Java Swing.
Field-Field yang harus di isi oleh Owner tempat adalah StartTime EndTime dan Nama, __Untuk__ ComboBox itu adalah ID dari Table yang
sudah Pre-defined ketika __Window__ Swing nya Load. __Dan__ Total Harga akan akan terisi apabila Customer sudah memilih Table mana yang
ingin di Booking.




![Tampilan Terisi](https://www.dropbox.com/s/elxlhj3o1ab6nae/2.png?raw=1)   


Ini adalah Tampilan Combo Box yang telah di Klik Dropdown nya.





![Tampilan Booking](https://www.dropbox.com/s/elxubom0u09gh3t/3.png?raw=1)   


Ini adalah tampilan ketika Tombol Booking di pencet, Tombol Booking langsung kelkulasi total harga berdasarkan quantity bangu per table.






### Pengerjaan Real.   


Berikut saya kirimkan juga netbeans waktu saya mengerjakan program nya.
![Bukti](https://www.dropbox.com/s/hfltucrmsr3lwyr/4.png?raw=1)




```java
        // TODO add your handling code here:
        // BUAT BOOKING RECORD
        
        if (nameInput.getText().equals("")) {
            return;
        }
        
        if (startTimeInput.getText().equals("")) {
            return;
        }
        
        if (endTimeInput.getText().equals("")) {
            return;
        }
        
        Booking booking;
        booking = new Booking(
                nameInput.getText(),
                startTimeInput.getText(),
                endTimeInput.getText(),
                selectedTable
        );
        
        // TAMPILKAN RECORD BOOKING KE LISTVIEW
        this.totalPriceOutput.setText("" + booking.getTotalPrice());
        
        DefaultListModel<String> model = new DefaultListModel<>();
        model.addElement("" + booking.getName() + " " + booking.getStartTime() + " " + booking.getEndTime() + " " + booking.getTotalPrice());
        
        jList1.setModel(model);
```




```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package models;

/**
 *
 * @author bowoekren
 */
public class Booking {
    public static final int pricePerChair = 10000;
    int id;
    Table table;
    String name;
    String startTime;
    String endTime;
    int priceTotal;
    
    public Booking(String name, String startTime, String endTime, Table table) {
        this.startTime = startTime;
        this.endTime = endTime;
        this.table = table;
        this.name = name;
    }
    
    public int getTotalPrice() {
        return table.getChairQty() * Booking.pricePerChair;
    }

    public static int getPricePerChair() {
        return pricePerChair;
    }

    public int getId() {
        return id;
    }

    public Table getTable() {
        return table;
    }

    public String getName() {
        return name;
    }

    public String getStartTime() {
        return startTime;
    }

    public String getEndTime() {
        return endTime;
    }

    public int getPriceTotal() {
        return priceTotal;
    }
}


```
