Pendahuluan

Modul ini dibuat untuk rekan developer sekalian di Indonesia yang ingin memulai untuk mempelajari cara membuat aplikasi mobile berbasis Android. Modul ini dibuat oleh Sidiq Permana, Google Developer Expert dan disempurnakan oleh tim dicoding academy.




Aplikasi yang dibuat dengan Android bisa dihasilkan dari penggunaan berbagai cara, misalnya dengan Builder (AppInventor), HTML5+CSS3+JS (Phonegap, Intel XDK, Sencha), Native (Eclipse, Android Studio), dan lain-lain. Salah satu tools yang disarankan oleh google adalah menggunakan Android Studio, seperti yang digunakan pada modul ini.

Semoga modul ini dapat bermanfaat bagi rekan sekalian dan Selamat Berkarya!

Pengantar Layout : https://goo.gl/iECaAZ

Referensi

Android Application Development Guide (http://developer.android.com/guide/index.html)
Android Application Development Training (http://developer.android.com/training/index.html)
Buku : Professional Android 4 Application Development by Reto Meier (PA4AD)
User Interface Design : http://pttrns.com/?did=6
 

Listview dan Gridview

Listview merupakan komponen utama yang dapat menampilkan dan menampung data dalam jumlah yang banyak secara vertical dalam bentuk list yang dapat di-scroll secara vertical. Contoh aplikasi yang menggunakan Listview adalah Whatsapp. Lebih lanjut mengenai Listview dapat dibaca di http://developer.android.com/guide/topics/ui/layout/listview.html







Sedangkan gridview merupakan komponen utama yang dapat menampilkan dan menampung data dalam jumlah yang banyak dalam bentuk grid (baris dan kolom). Biasanya implementasinya adalah menampilkan katalog barang pada mobile commerce, gallery Image dsb. Salah satu apps yang memanfaatkan gridview adalah Instagram. Lebih lanjut mengenai Gridview, dapat dibaca pada tautan http://developer.android.com/guide/topics/ui/layout/gridview.html.







Persamaan dua komponen ini adalah untuk menampilkan data kedalam bentuk List dan Grid dibutuhkan Adapter yang berfungsi untuk memproses dan menformat tiap item data dalam GridView atau ListView.

Adapter

Adapter adalah sebuah mekanisme untuk membinding sekumpulan data, memproses dan memformat tampilan item-item data yang akan ditampilkan melalui listview atau gridview. Lebih lanjut dapat dibaca pada http://developer.android.com/reference/android/widget/Adapter.html.

Android SDK telah menyediakan Adapter bawaan yang secara default dapat digunakan dan dikustomisasi sesuai dengan kebutuhan yang ada. Berikut adalah native adapter yang terdapat didalam Android SDK. 

ArrayAdapter : Adapter yang diperuntukan untuk mem-binding data-data dalam format array.

SimpleCursorAdapter : Adapter yang diperuntukan untuk mem-binding data-data column dalam format objek Cursor (umumnya merupakan hasil nilai balik jika kita melakukan query pada ContentProvider)

Ref : Professional Android 4 Application Development page 156 - 164

Untuk customisasi Adapter dari Stractch bisa menggunakan BaseAdapter : http://developer.android.com/reference/android/widget/BaseAdapter.html

 

Practice Session #6 : 

SimpleListView

Pada codelab kali ini kita akan membuat implementasi dari ListView dalam menampung data bentuk String array sehingga dapat ditampilkan dalam bentuk List yang bisa diakses oleh pengguna. Implementasi ListView sangat luas, selain memiliki tujuan utama yaitu menampilkan data dalam jumlah yang banyak. ListView juga bisa digunakan sebagai tampilan pilihan menu pada aplikasi Android.

 

1. Buat Project dengan Start a new Android Studio Project





2. Lalu isikan Application Name dengan SimpleListView dan Company domain dengan nama yang kamu mau, kemudian Klik Next dan pilih Blank Activity. Lanjutkan hingga Finish. Biarkan gradle menggenerate project kita.



3. Pada activity_main.xml lengkapi kodenya sebagai berikut.

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" 
    android:layout_width="match_parent"
    android:layout_height="match_parent" 
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin" 
    tools:context=".MainActivity">
    <ListView
        android:id="@+id/lv_item"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:cacheColorHint="@android:color/transparent">
    </ListView>
</RelativeLayout> 
Pada code diatas kita menambahkan ListView kedalam tampilan xml kita dan nantinya akan kita manipulasi di class Activity java yang kita punya.



4. Pada MainActivity.java silakan lengkapi kodenya sebagai berikut. Sesuaikan nama package yang kamu gunakan (Baris 1)

package com.sidiq.codelab.simplelistview;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private ListView lvItem;
    private String[] footballClubs = new String[]{
            "Juventus", "Manchester United", "Liverpool",
            "Bayern Munchen", "Real Madrid", "Ajax Amsterdam",
            "Barcelona"
    };
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        lvItem = (ListView)findViewById(R.id.lv_item);
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(MainActivity.this,
                android.R.layout.simple_list_item_1,
                android.R.id.text1, footballClubs);
        lvItem.setAdapter(adapter);

        lvItem.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Toast.makeText(MainActivity.this, "Kamu klik : "+footballClubs[position], Toast.LENGTH_LONG).show();
            }
        });
    }
}


Pada kode diatas (perhatikan komentar dalam kode) kita melakukan beberapa langkah :

Menginisialisasi ListView berdasarkan id yang ada di file layout xml (line 16)
Menginisialisasi data String array yang akan kita tampilkan di ListView (line 17)
Membuat object adapter dengan menggunakan Adapter bawaah android secara default dengan menentukan beberapa parameter sebagai inputannya (line 28-37):
Class Activity mana yang memanggil/menggunakan class ArrayAdapter
Layout xml untuk tampilan item list (disini kita menggunakan bawaan android)
Id dari object TextView untuk menampilkan item-item data dari object String array
Sumber data yang akan ditampilkan dalam konteks ini adalah : String array bernama footballClubs
Men-set objek adapter kedalam ListView
 

5. Silakan Run dengan tombol Run ke emulator atau device atau export ke apk untuk instal secara manual di device. Tampilan hasil apps adalah sebagai berikut.

