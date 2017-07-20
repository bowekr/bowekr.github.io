---
title: Tugas UAS Algoritma Pemrograman 1 - STMIK ERESHA TPLP001 - 403
layout: default
---

## 2.1 Deskripsi Project  
Projek Buku Telpon untuk menyimpan kontak kontak kerabat atau teman, atau memudahkan User untuk Organize Contact, Organize Contact dapat Membuat, Mengedit, dan Menghapus Contact dari Organizer.  



## 2.2 Komponen Dan Formula
Program Java MainClass tidak menggunakan Component Melainkan Library yang di import; untuk library yang saya import ke project yaitu:  


- java.util.Scanner;
- java.awt.List
- java.utils.ArrayList;


Karna Program hanya berbasis CRUD Action maka Program tidak menggunakan Formula, Karna peruntukannya hanya untuk Store / indexing Contact.

Untuk Flow nya sendiri setiap Contact yang di buat akan langsung di 'push' ke dalam ContactsRepository guna indexing, ContactsRepository ini bisa di artikan sebagai Database Seluruh Contact Object, Karna Project sebatas Java MainClass maka saya membuatnya hanya store di dalam Memory.




## 2.3 Screenshoot Program  

##### Tambah Contact  
![Tambah Menu](https://www.dropbox.com/s/wuj238fxx4u94zy/tambahMenu.jpg?raw=1)


##### Edit Contact  
![Edit Contact](https://www.dropbox.com/s/lkogtmu8y01f4c0/EditMenu.jpg?raw=1)

##### Delete Contact
![Delete Contact](https://www.dropbox.com/s/cmeuw2dvg26h174/deleteContact.jpg?raw=1)



##### Lihat Contact   
![Lihat Contact](https://www.dropbox.com/s/8h2glfa5b1u1qeb/Contacts.jpg?raw=1)



## 2.4 Source Code



#### MainClass Class
```java
// MainClass

import java.util.Scanner;

public class MainClass {
  private static Scanner scanner;

  public static void main(String[] args) {
    // TODO Auto-generated method stub
    // Repository
    ContactsRepository contacts = new ContactsRepository();
    
    // Populate Data
    for(int i = 0; i < 10; i++) {
      String nama = "Kontak " + i;
      String nomorTelpon = "1234-125125-" + i;
      Contact contact = new Contact(nama, nomorTelpon);
      
      contacts.addContact(contact);
    }
    
    scanner = new Scanner(System.in);
    
    // Render Menu
    printPilihanMenu();
    String pilihanMenu = scanner.nextLine();
    
    
    // Menu Decision
    if ("1".equals(pilihanMenu)) {
      // Lihat Menu Action
      for(int i = 0; i < contacts.getContacts().size(); i++) {
        String nama = contacts.getContacts().get(i).getNama();
        String nomorTelpon = contacts.getContacts().get(i).getNomorTelpon();
        
        System.out.println("Nama: " + nama);
        System.out.println("Nomor Telpon: " + nomorTelpon);
      }
    } else if ("2".equals(pilihanMenu)) {
      // Tambah Contact Action
      System.out.println("Masukan Nama");
      String nama = scanner.nextLine();
      
      System.out.println("===========");
      System.out.println("Masukan Nomor Telpon");
      String nomorTelpon = scanner.nextLine();
      
      Contact contact = new Contact(nama, nomorTelpon);
      contacts.addContact(contact);
      System.out.println("Kontak di Tambah : " + contact.getNama() + " : " + contact.getNomorTelpon());
    } else if ("3".equals(pilihanMenu)) {
      // Edit Menu Action
      System.out.println("Masukan ID Contact Yang ingin di Edit");
      int idContact = scanner.nextInt();
      
      try {
        Contact contact = contacts.getContacts().get(idContact);
        
        System.out.println("Masukan Nama Baru: ");
        String namaBaru = scanner.nextLine();
        
        System.out.println("===");
        System.out.println("Masukan Nomor Telpon Baru: ");
        String nomorBaru = scanner.nextLine();
        
        contact.setNama(namaBaru);
        contact.setNomorTelpon(nomorBaru);
        
        System.out.println("Data Berhasil di Ubah---");
        System.out.println("MENJADI: " + contact.getNama() + " " + contact.getNomorTelpon());
      } catch (Exception e) {
        System.out.println("ID KONTAK TIDAK DAPAT DI TEMUKAN -");
      }
      
    } else if ("4".equals(pilihanMenu)) {
      // Delete Menu Action
      System.out.println("Masukan ID Contact Yang ingin di Delete: ");
      String idContact = scanner.nextLine();
      
      contacts.removeContact(Integer.parseInt(idContact));
      Contact contact = contacts.getContacts().get(Integer.parseInt(idContact));
      System.out.println("Contact :" + contact.getNama() + " : " + contact.getNomorTelpon() + " --- Berhasil Di Delete");
    } else {
      // Unknown Menu
      System.out.println("Pilihan Menu salah;");
    }
  }
  
  public static void printPilihanMenu() {
    System.out.println("Pilih Menu:");
    System.out.println("1. Lihat Contact");
    System.out.println("2. Tambah Contact");
    System.out.println("3. Edit Contact");
    System.out.println("4. Delete Contact");
    System.out.println("=================");
  }
}
```


#### Contact Class
```java
// Contact Object
public class Contact {
  public String nama;
  public String nomorTelpon;

  public Contact(String nama, String nomorTelpon){
    this.nama = nama;
    this.nomorTelpon = nomorTelpon;
  }
  
  public String getNama() {
    return nama;
  }

  public void setNama(String nama) {
    this.nama = nama;
  }

  public String getNomorTelpon() {
    return nomorTelpon;
  }

  public void setNomorTelpon(String nomorTelpon) {
    this.nomorTelpon = nomorTelpon;
  }

}
```



#### ContactsRepository Class
```java
import java.awt.List;
import java.util.ArrayList;

public class ContactsRepository {
  public ArrayList<Contact> contacts = new ArrayList<Contact>();
  
  // Add To Contact Method
  public void addContact(Contact contact) {
    this.contacts.add(contact);
  }
  
  public void editContact(Contact contact) {
    this.contacts.add(contact);
  }
  
  public ArrayList<Contact> getContacts() {
    return this.contacts;
  }
  
  public void removeContact(int idContact) {
    this.contacts.remove(idContact);
  }
}

```