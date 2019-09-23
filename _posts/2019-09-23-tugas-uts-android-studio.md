---
title: Tugas UTS Pembuatan Aplikasi Contact Sederhana dengan Android Studio dan SQLite.
layout: default
---


### Deskripsi Program
Pembuatan aplikasi contact sederhana dengan android studio dan SQLite
program ini dibuat untuk manage contact (nama dan nomor telpon), dengan fitur yang terdiri dari


### Fitur Program
- Membuat contact baru
- Mengubah contact yang ada
- Menghapus contact yang ada
- Melihat seluruh contact
- Melihat satu contact

### Data yang di simpan
- Nama
- Nomor Telpon


### Component Program
- 3 Activity (MainActivity, AddActivity, EditActivity)
- ListView
- SQLite sebagai database contact.


### Screenshot Hasil Program
#### Halaman Utama / Main Activity
![Halaman Utama / Main Activity](https://www.dropbox.com/s/ktzvpbgsa2ydx8a/Tugas%20-%201%20-%20Index.png?raw=1)


#### Halaman Tambah Contact
![Halaman Tambah Contact / AddActivity](https://www.dropbox.com/s/npr94q9jyxf88fa/Tugas%20-%202%20-%20Add.png?raw=1)
![Halaman Utama / MainActivity Added](https://www.dropbox.com/s/34qvh25ct3jzzc9/Tugas%20-%204%20-%20Added.png?raw=1)


#### Halaman Edit Contact
![Halaman Melihat Contact / EditActivity](https://www.dropbox.com/s/jdq6vi9h2mqrvti/Tugas%20-%205%20-%20Show%20Open%20Single.png?raw=1)



#### Delete Contact
![Delete Contact / MainActivity](https://www.dropbox.com/s/wdhe7yujaax6ysz/Tugas%20-%206%20-%20Delete.png?raw=1)










### Source Code
#### XML
##### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <ListView
        android:id="@+id/listView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="2dp"
        android:layout_marginLeft="2dp"
        android:layout_marginTop="4dp"
        android:layout_marginEnd="2dp"
        android:layout_marginRight="2dp"
        android:layout_marginBottom="34dp"
        app:layout_constraintBottom_toTopOf="@+id/addContactButton"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/addContactButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="19dp"
        android:layout_marginRight="19dp"
        android:layout_marginBottom="18dp"
        android:clickable="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/listView"
        app:srcCompat="@android:drawable/ic_menu_add"
        android:onClick="addContact"
        android:focusable="true"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```


##### activity_edit.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".EditActivity">


        <EditText
            android:id="@+id/editPhone"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="25dp"
            android:ems="10"
            android:hint="Nomor Telpon"
            android:inputType="textPersonName"
            app:layout_constraintStart_toStartOf="@+id/editName"
            app:layout_constraintTop_toBottomOf="@+id/editName" />

        <EditText
            android:id="@+id/editName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="88dp"
            android:layout_marginLeft="88dp"
            android:layout_marginTop="147dp"
            android:ems="10"
            android:hint="Nama"
            android:inputType="textPersonName"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <Button
            android:id="@+id/btnEdit"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="55dp"
            android:layout_marginLeft="55dp"
            android:layout_marginTop="24dp"
            android:onClick="editContact"
            android:text="Save edit"
            app:layout_constraintStart_toStartOf="@+id/editPhone"
            app:layout_constraintTop_toBottomOf="@+id/editPhone" />

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="30dp"
            android:onClick="deleteContact"
            android:text="Delete"
            app:layout_constraintStart_toStartOf="@+id/btnEdit"
            app:layout_constraintTop_toBottomOf="@+id/btnEdit" />

</androidx.constraintlayout.widget.ConstraintLayout>
```




##### activity_add.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".AddActivity">

    <EditText
        android:id="@+id/editText2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="4dp"
        android:layout_marginLeft="4dp"
        android:layout_marginTop="44dp"
        android:ems="10"
        android:hint="Nomor Telpon"
        android:inputType="textPersonName"
        app:layout_constraintEnd_toEndOf="@+id/editText"
        app:layout_constraintStart_toStartOf="@+id/editText"
        app:layout_constraintTop_toBottomOf="@+id/editText" />

    <EditText
        android:id="@+id/editText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="84dp"
        android:layout_marginLeft="84dp"
        android:layout_marginTop="68dp"
        android:ems="10"
        android:hint="Nama"
        android:inputType="textPersonName"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="68dp"
        android:onClick="insertContact"
        android:text="Tambah"
        app:layout_constraintEnd_toEndOf="@+id/editText2"
        app:layout_constraintHorizontal_bias="0.47"
        app:layout_constraintStart_toStartOf="@+id/editText2"
        app:layout_constraintTop_toBottomOf="@+id/editText2"
        />
</androidx.constraintlayout.widget.ConstraintLayout>
```



##### contact_list.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="5dip" >

    <TextView
        android:id="@+id/name"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:textSize="30sp"></TextView>

    <TextView
        android:id="@+id/phoneNumber"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="40sp"
        android:textSize="30sp" />

</RelativeLayout>
```




### Java Code

#### MainActivity.java
```java
package com.example.ariefwibowowicaksono_161021450104;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;
import android.widget.Toast;
;;;
import com.example.ariefwibowowicaksono_161021450104.adapter.ContactListAdapter;
import com.example.ariefwibowowicaksono_161021450104.handler.ContactListHandler;
import com.example.ariefwibowowicaksono_161021450104.handler.DatabaseHandler;
import com.example.ariefwibowowicaksono_161021450104.model.Contact;

import java.util.ArrayList;
import java.util.List;


public class MainActivity extends AppCompatActivity {
    public DatabaseHandler dbHandler;
    public ListView listView;
    public ContactListAdapter contactAdapter;
    public ArrayList<Contact> contactArrayList;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Database
        dbHandler = new DatabaseHandler(this);
        contactArrayList = dbHandler.getContacts();

        ContactListHandler contactHandler = new ContactListHandler();
        contactAdapter = new ContactListAdapter(this, contactArrayList);

        // View Handler
        listView = (ListView) findViewById(R.id.listView);
        listView.setAdapter(contactAdapter);
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int position, long l) {
                Contact contact = (Contact) adapterView.getItemAtPosition(position);

                // Redirect to Edit Intent
                Intent editIntent = new Intent(getBaseContext(), EditActivity.class);
                editIntent.putExtra("id", contact.getId());
                editIntent.putExtra("name", contact.getName());
                editIntent.putExtra("phone", contact.getPhoneNumber());
                startActivity(editIntent);
            }
        });
    }

    @Override
    protected void onResume() {
        super.onResume();
        contactAdapter.clear();
        contactArrayList = dbHandler.getContacts();
        contactAdapter.setContactList(contactArrayList);

        Toast.makeText(getBaseContext(), "RESUME", Toast.LENGTH_LONG).show();
    }

    public void addContact(View view) {
        Intent intent = new Intent(this, AddActivity.class);
        startActivity(intent);
    }
}
```



#### EditActivity.java   
```java
package com.example.ariefwibowowicaksono_161021450104;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

import com.example.ariefwibowowicaksono_161021450104.handler.DatabaseHandler;
import com.example.ariefwibowowicaksono_161021450104.model.Contact;

public class EditActivity extends AppCompatActivity {
    private Contact contact;
    private TextView txtName, txtPhone;
    private DatabaseHandler db;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_edit);

        int id = getIntent().getExtras().getInt("id");
        String nameExtra = getIntent().getExtras().getString("name");
        String phoneExtra = getIntent().getExtras().getString("phone");
        db = new DatabaseHandler(getBaseContext());

        contact = new Contact(id, nameExtra, phoneExtra);

        txtName = (TextView) findViewById(R.id.editName);
        txtPhone = (TextView) findViewById(R.id.editPhone);


        txtName.setText(contact.getName());
        txtPhone.setText(contact.getPhoneNumber());
    }

    public void editContact(View view) {
        String newName = txtName.getText().toString();
        String newPhone = txtPhone.getText().toString();
        long updateResp = db.updateRecord(contact.getId(), contact);

        Toast.makeText(getBaseContext(), "Success edit contact", Toast.LENGTH_LONG).show();
        finish();

        contact = new Contact(contact.getId(), newName, newPhone);
        startActivity(getIntent());
    }

    public void deleteContact(View view) {
        db.deleteRecord(contact.getId());

        Toast.makeText(getBaseContext(), "Success delete contact", Toast.LENGTH_LONG).show();

        finish();
    }
}
```


#### AddActivity.java
```java
package com.example.ariefwibowowicaksono_161021450104;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

import com.example.ariefwibowowicaksono_161021450104.handler.DatabaseHandler;
import com.example.ariefwibowowicaksono_161021450104.model.Contact;

public class AddActivity extends AppCompatActivity {
    private TextView name, phone;
    private DatabaseHandler db;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_add);

        name = (TextView) findViewById(R.id.editText);
        phone = (TextView) findViewById(R.id.editText2);

        db = new DatabaseHandler(this);
    }


    public void insertContact(View view) {
        Contact contact = new Contact(1,name.getText().toString(), phone.getText().toString());
        Contact contactCreated = db.addRecord(contact);

        if (contactCreated != null) {
            Toast.makeText(getBaseContext(), "Success Create Contact", Toast.LENGTH_LONG).show();
            finish();
        } else {
            Toast.makeText(getBaseContext(), "Unknown error when create contact", Toast.LENGTH_LONG).show();
        }
    }
}
```



#### model/Contact.java
```java
package com.example.ariefwibowowicaksono_161021450104.model;

import android.widget.Adapter;

public class Contact {
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    private int id;
    private String name;
    private String phoneNumber;

    public Contact(int id, String name, String phoneNumber) {
        this.id = id;
        this.name = name;
        this.phoneNumber = phoneNumber;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    @Override
    public String toString() {
        return this.getName();
    }

}
```



#### handler/ContactListHandler.java
```java
package com.example.ariefwibowowicaksono_161021450104.handler;

import android.content.Context;
import android.content.Intent;
import android.view.View;
import android.widget.AdapterView;
import android.widget.Toast;

import com.example.ariefwibowowicaksono_161021450104.EditActivity;
import com.example.ariefwibowowicaksono_161021450104.model.Contact;

public class ContactListHandler {
    public AdapterView.OnItemClickListener getContactListItemClickHandler(Context context) {
        return new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int position, long l) {
                Contact contact = (Contact) adapterView.getItemAtPosition(position);
            }
        };
    }
}
```


#### handler/DatabaseHandler.java
```java
package com.example.ariefwibowowicaksono_161021450104.handler;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import com.example.ariefwibowowicaksono_161021450104.model.Contact;

import java.util.ArrayList;
import java.util.List;

public class DatabaseHandler extends SQLiteOpenHelper {

    // static variable
    private static final int DATABASE_VERSION = 1;

    // Database name
    private static final String DATABASE_NAME = "AriefContactManager";

    // table name
    private static final String TABLE_CONTACT = "contacts";

    // column tables
    private static final String KEY_ID = "id";
    private static final String KEY_NAME = "name";
    private static final String KEY_PHONE = "phone";

    public DatabaseHandler(Context context){
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    //Create table
    @Override
    public void onCreate(SQLiteDatabase db) {
        String CREATE_CONTACTS_TABLE = "CREATE TABLE " + TABLE_CONTACT + "("
                + KEY_ID + " INTEGER PRIMARY KEY," + KEY_NAME + " TEXT,"
                + KEY_PHONE + " TEXT" + ")";
        db.execSQL(CREATE_CONTACTS_TABLE);
    }

    // on Upgrade database
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS " + TABLE_CONTACT);
        onCreate(db);
    }

    public Contact addRecord(Contact contact){
        SQLiteDatabase db  = getWritableDatabase();

        ContentValues values = new ContentValues();
        values.put(KEY_NAME, contact.getName());
        values.put(KEY_PHONE, contact.getPhoneNumber());

        db.insert(TABLE_CONTACT, null, values);
        db.close();

        return contact;
    }

    public long deleteRecord(int id) {
        SQLiteDatabase db = getWritableDatabase();

        long resp = db.delete(TABLE_CONTACT, "ID = ?", new String[] { String.valueOf(id) });
        db.close();

        return resp;
    }

    public long updateRecord(int id, Contact contact) {
        SQLiteDatabase db = getWritableDatabase();

        ContentValues values = new ContentValues();
        values.put(KEY_NAME, contact.getName());
        values.put(KEY_PHONE, contact.getPhoneNumber());

        long resp = db.update(TABLE_CONTACT, values, "ID = ?", new String[] { String.valueOf(id) });
        db.close();

        return resp;
    }

    public ArrayList<Contact> getContacts() {
        SQLiteDatabase db = getReadableDatabase();

        ArrayList<Contact>  contactList = new ArrayList<Contact>();
        String selectQuery = "SELECT id, name, phone FROM " + TABLE_CONTACT;
        Cursor cursor = db.rawQuery(selectQuery, null);

        if (cursor.moveToFirst()) {
            do {
                Contact contact = new Contact(Integer.parseInt(cursor.getString(0)), cursor.getString(1), cursor.getString(2));
                contactList.add(contact);
            } while (cursor.moveToNext());
        }

        return contactList;
    }

    public Contact getContact(int id) {
        SQLiteDatabase db = this.getReadableDatabase();

        Cursor cursor = db.query(TABLE_CONTACT, new String[] { KEY_ID,
                        KEY_NAME, KEY_PHONE}, KEY_ID + " = ?",
                new String[] { String.valueOf(id) }, null, null, null, null);

        if (cursor != null) {
            cursor.moveToFirst();
        }

        Contact contact = new Contact(Integer.parseInt(cursor.getString(0)),
                cursor.getString(1), cursor.getString(2));
        // return contact
        return contact;
    }
}
```



#### adapter/ContactListAdapter.java
```java
package com.example.ariefwibowowicaksono_161021450104.adapter;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;

import com.example.ariefwibowowicaksono_161021450104.R;
import com.example.ariefwibowowicaksono_161021450104.model.Contact;

import java.util.ArrayList;

public class ContactListAdapter extends BaseAdapter {
    private ArrayList<Contact> contactList;
    private LayoutInflater layoutInflater;

    public ContactListAdapter(Context ctx, ArrayList<Contact> listData) {
        this.contactList= listData;
        layoutInflater = LayoutInflater.from(ctx);
    }

    @Override
    public int getCount() {
        return contactList.size();
    }

    @Override
    public Object getItem(int position) {
        return contactList.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    public void clear() {
        contactList.clear();
    }

    public void setContactList(ArrayList<Contact> contacts) {
        this.contactList = contacts;
        this.notifyDataSetChanged();
    }

    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder holder;
        if (convertView == null) {
            convertView = layoutInflater.inflate(R.layout.contact_list, null);
            holder = new ViewHolder();
            holder.nameView = (TextView) convertView.findViewById(R.id.name);
            holder.phoneView = (TextView) convertView.findViewById(R.id.phoneNumber);

            convertView.setTag(holder);
        } else {
            holder = (ViewHolder) convertView.getTag();
        }

        holder.nameView.setText(contactList.get(position).getName());
        holder.phoneView.setText(contactList.get(position).getPhoneNumber());

        return convertView;
    }

    static class ViewHolder {
        TextView nameView;
        TextView phoneView;
    }
}
```
