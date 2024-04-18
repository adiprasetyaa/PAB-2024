# Tab Layout

***Pemahaman singkat mengenai Tab Layout***


  Tab Layout adalah salah satu bagian dari Android Design Support Library yang menyediakan UI untuk menavigasi antara beberapa tab dengan konten yang terkait dalam aplikasi Android. Dengan TabLayout, pengguna dapat dengan mudah beralih antara berbagai bagian atau fitur dalam aplikasi tanpa perlu meninggalkan tampilan utama. Setiap tab biasanya memiliki label yang deskriptif dan bisa memiliki ikon sebagai representasi visual dari konten yang terkait.

  TabLayout biasanya digunakan bersama dengan ViewPager, yang memungkinkan pengguna untuk menggeser antara tab atau dengan FragmentContainerView untuk menampilkan konten yang terkait dengan setiap tab. Berikut adalah beberapa kegunaan umum TabLayout dalam pengembangan aplikasi Android:

-  ***Navigasi antara bagian aplikasi***
-  ***Pengaturan***
-  ***Profil pengguna***

Untuk selengkapnya dapat dilihat dan belajar mandiri melalui tautan di bawah ini.

[Tab Layout](https://developer.android.com/reference/com/google/android/material/tabs/TabLayout)

## PRACTICE TAB LAYOUT WITH VIEWPAGER2

Pastikan bahwa kalian sudah menginstall Android Studio pada device kalian masing-masing yaa!

1. Kalian bisa Running Android Studio terlebih dahulu, maka akan menampilkan tampilan kurang lebih seperti ini. Kemudian, kalian bisa pilih New Project.

![1](assets/1.png)

2. Dikarenkakan kita hanya membuat basic project saja maka kalian bisa memilih yang Empty View Activity seperti biasa. Kemudian, bisa klik Next.

3. Maka, akan ditampilkan window seperti berikut ini. Untuk nama, Language, Minimum SDK, dan Build configuration language bisa mengikuti seperti pada gambar, sedangkan untuk package bisa disesuaikan dengan format berikut ini:

**com.nim.namapertama.tablayout**

![2](assets/2.png)

4. Kemudian, untuk save location bisa disesuaikan sesuai dengan path pada device masing-masing. Lalu bisa pilih Finish.

5. Dimulai dengan menambahkan library ViewPager2 dan material design untuk membuat TabLayout. Silahkan ke **Gradle Scripts** →  **build.gradle.kts(Module: app)** dan tambahkan kode seperpti di bawah ini.

```kotlin
implementation("com.google.android.material:material:1.11.0") //jika belum ada
implementation("androidx.viewpager2:viewpager2:1.0.0")
```
![3](assets/3.png)

Jangan lupa untuk **sync project** yang berada dipojok kanan atas agar library tersebut dapat berfungsi pada projek kalian.

6. Setelah itu tambahkan *TabLayout* dan *viewPager2* ke **activity_main.xml** seperti kode di bawah ini.

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">
 
    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tabs"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="?attr/colorPrimary"
        app:tabTextColor="@android:color/white"/>
    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/view_pager"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
```
-  ***Note*** :
  Untuk menerapkan **TabLayout**, cukup tambahkan komponen **TabLayout dan ViewPager2** di dalam layout, seperti kode di atas. ViewPager2 di sini digunakan supaya Anda dapat berpindah antar tab dengan menggunakan swipe tanpa memilih menu tab-nya. Sebenarnya ada juga versi ViewPager lama yang bisa Anda lihat di 
[sini](https://developer.android.com/guide/navigation/navigation-swipe-view)

7.  Kemudian buat *fragment* baru terlebih dahulu yang akan dipakai untuk isi dari TabLayout. Caranya sama seperti sebelumnya yaitu **klik kanan pada nama package  → new → Fragment → Fragment (Blank)**.

![4](assets/4.png)

![5](assets/5.png)

8.  Selanjutnya ubah layout pada file **fragment_home.xml** menjadi seperti di bawah ini.

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".HomeFragment">
 
    <TextView
        android:id="@+id/section_label"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="16dp"
        android:text="@string/content_tab_home" />
 
</FrameLayout>
```
Jangan lupa untuk menambahkan resource teks pada **res → value → strings.xml.** Resource ini akan dipakai sampai akhir latihan.

```kotlin
<resources>
    <string name="app_name">MyTabLayout</string>
    <string name="tab_text_1">Home</string>
    <string name="tab_text_2">Profile</string>
    <string name="tab_text_3">Setting</string>
    <string name="content_tab_home">Welcome Home</string>
    <string name="content_tab_profile">Change your Profile here</string>
    <string name="content_tab_text">This is Tab %1$d</string>
</resources>
```

9. Buat fragment sekali lagi dengan cara yang sama, yaitu **klik kanan pada nama package → new → Fragment → Fragment (Blank)**. Beri nama **ProfileFragment** dan klik Finish. Kemudian ubah layout pada **fragment_profile.xml** menjadi seperti berikut:

![6](assets/6.png)

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".ProfileFragment">
 
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="16dp"
        android:text="@string/content_tab_profile" />
 
</FrameLayout>
```

10. Selanjutnya kita akan membuat kelas baru untuk mengatur ViewPager2 dan TabLayout. Caranya, **klik kanan pada nama package → new → Kotlin Class / Java Class**. Beri nama **SectionsPagerAdapter**.

![7](assets/7.png)

![8](assets/8.png)

Pertama buat terlebih dahulu *constructor* dengan menambahkan kode berikut:

```kotlin
class SectionsPagerAdapter(activity: AppCompatActivity) : FragmentStateAdapter(activity) {
}
```
- ***Note*** :  Untuk mengatur ViewPager2 dan komponen yang ada di dalamnya, Anda memerlukan **SectionsPagerAdapter** yang extend ke kelas **FragmentStateAdapter**, contohnya seperti pada kode di atas. 

- ***Note*** :  Base adapter yang digunakan untuk mengatur data pada ViewPager2 adalah  **FragmentStateAdapter**. Dengan extends ke abstract class ini, kalian diminta untuk mengimplementasikan 2 fungsi utama yaitu, **createFragment** dan **getItemCount**. Selain itu, di sini juga terdapat constructor yang diperlukan yaitu **AppCompatActivity** karena kita menggunakan Activity. Apabila Anda menerapkannya di Fragment, gunakan **FragmentActivity**. Sebenarnya kalian dapat menggunakan **RecyclerView.Adapter** sebagai adapter. Hal ini karena pada dasarnya ViewPager2 dibuat menggunakan RecyclerView.

11. Jika muncul baris merah, jangan khawatir. **Arahkan kursor** pada SectionsPagerAdapter, tekan **Alt+Enter** untuk mendapatkan suggestion, dan pilih **implement members**.

![9](assets/9.png)

![10](assets/10.png)

Kemudian pilih kedua method dan klik **OK**.

![11](assets/11.png)

12.  Selanjutnya ubah kode didalamnya, sehingga kelas **SectionPagerAdapter** secara keseluruhan menjadi seperti di bawah ini.

```kotlin
package layout

import androidx.appcompat.app.AppCompatActivity
import androidx.fragment.app.Fragment
import androidx.viewpager2.adapter.FragmentStateAdapter
import com.m0521074.ayuk.tablayout.HomeFragment
import com.m0521074.ayuk.tablayout.ProfileFragment

class SectionPagerAdapter(activity: AppCompatActivity) : FragmentStateAdapter(activity) {
    override fun getItemCount(): Int {
        return 2
    }

    override fun createFragment(position: Int): Fragment {
        var fragment: Fragment? = null
        when (position) {
            0 -> fragment = HomeFragment()
            1 -> fragment = ProfileFragment()
        }
        return fragment as Fragment
    }

}
```
- ***Note*** :  Fungsi **getItemCount** untuk menentukan jumlah tab yang ingin ditampilkan. Pada projek kali ini yang ingin ditampilkan ada dua tab dan pastikan jumlah yang ingin ditampilkan sesuai dengan Fragment yang didefinisikan oleh fungsi **createFragment**
- ***Note*** :  Fungsi **createFragment** untuk menampilkan fragment sesuai dengan posisi tab-nya. Misalnya kode di atas untuk posisi 0 (tab pertama) menampilkan **HomeFragment** dan di posisi 1 (tab kedua) menampilkan **ProfileFragment**. 


13.Kemudian panggil kelas yang baru dibuat. Mulai dengan *setup* ViewPager2 dan TabLayout pada kelas **MainActivity** dengan kode di bawah ini.

```kotlin
package com.m0521074.ayuk.tablayout

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.annotation.StringRes
import androidx.viewpager2.widget.ViewPager2
import com.google.android.material.tabs.TabLayout
import com.google.android.material.tabs.TabLayoutMediator
import layout.SectionPagerAdapter

class MainActivity : AppCompatActivity() {

    companion object {
        @StringRes
        private val TAB_TITLES = intArrayOf(
            R.string.tab_text_1,
            R.string.tab_text_2
        )
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val sectionsPagerAdapter = SectionPagerAdapter(this)
        val viewPager: ViewPager2 = findViewById(R.id.view_pager)
        viewPager.adapter = sectionsPagerAdapter
        val tabs: TabLayout = findViewById(R.id.tabs)
        TabLayoutMediator(tabs, viewPager) { tab, position ->
            tab.text = resources.getString(TAB_TITLES[position])
        }.attach()

        supportActionBar?.elevation = 0f
    }
}
```
***Untuk menghubungkan ViewPager2 dengan TabLayout pada MainActivity***
Perhatikan kode di bawah ini.

```kotlin
val sectionsPagerAdapter = SectionsPagerAdapter(this)
viewPager.adapter = sectionsPagerAdapter
```
-  ***Note*** :  Jika dilihat kode ini mirip dengan kode yang digunakan untuk set adapter pada RecyclerView. Hal ini karena memang konsepnya sama, tetapi tampilannya saja yang berbeda. Kalian juga bisa menghubungkan ViewPager2 dengan TabLayout dengan menggunakan **TabLayoutMediator** seperti berikut:

```kotlin
TabLayoutMediator(tabs, viewPager) { tab, position ->
    tab.text = resources.getString(TAB_TITLES[position])
}.attach()
```

-  ***Note*** :  Dengan menerapkan TabLayoutMediator, maka Fragment yang tampil pada ViewPager2 akan sesuai dengan posisi yang dipilih pada tab. Selain itu, di sini Anda juga menentukan judul dari masing-masing Tab dengan menggunakan **TAB_TITLE** yang diambil sesuai dengan urutan posisinya.

14. 
15. Jalankan aplikasi kalian. Dan tampilannya akan menjadi seperti di bawah ini.

![simulesyen](assets/simulesyen.gif)

## Practice Tab Layout With One Fragment


Sekarang kita akan menampilkan dua tampilan yang mirip hanya dengan satu fragment. Dengan cara membuat TabLayout dengan satu fragment saja.

1. Buka kembali file projek kalian yang **TabLayout**.
2. Pertama, masuk ke **HomeFragment**, hapus kode yang tidak dibutuhkan dan tambahkan kode di bawah ini untuk mendapatkan data dan menampikan teks sesuai dengan urusan tab.

```kotlin
class HomeFragment : Fragment() {
 
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?,
                              savedInstanceState: Bundle?): View? {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_home, container, false)
    }
 
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        val tvLabel: TextView = view.findViewById(R.id.section_label)
        val index = arguments?.getInt(ARG_SECTION_NUMBER, 0)
        tvLabel.text = getString(R.string.content_tab_text, index)
    }
 
    companion object {
        const val ARG_SECTION_NUMBER = "section_number"
    }
}
```

3. Selanjutnya di dalam **SectionPagerAdapter**, ubah kode untuk menampilkan fragment dan jumlah data yang ditampilkan menjadi tiga, sehingga kode di dalamnya menjadi seperti berikut

```kotlin
class SectionPagerAdapter(activity: AppCompatActivity) : FragmentStateAdapter(activity) {
 
    override fun createFragment(position: Int): Fragment {
        val fragment = HomeFragment()
        fragment.arguments = Bundle().apply {
            putInt(HomeFragment.ARG_SECTION_NUMBER, position + 1)
        }
        return fragment
    }
 
    override fun getItemCount(): Int {
        return 3
    }
}
```

***Attention!***

-  Didalam fungsi pada kode di atas parameter yang dimasukkan yang dikirimkan ke dalam Bundle sesuai dengan tipe datanya dengan format *Key-Value*, dengan **ARG_SECTION_NUMBER** yang berguna sebagai *key* dan **position+1** sebagai *value* nya. Mengapa ada +1? hal ini karena position dimulai dari 0, sedangkan Anda ingin menampilkan urutan tab yang dimulai dari 1. Kemudian **setArgument** digunakan untuk mengirimkan data bundle tersebut ke fragment.

Dan kode di bawah adalah untuk mendapatkan data yang dikirimkan.

```kotlin
val index = arguments?.getInt(ARG_SECTION_NUMBER, 0)
```

4. Kemudian pada **MainActivity** tambahkan lagi satu value untuk judul tab ketiga seperti berikut:

```kotlin
companion object {
    @StringRes
    private val TAB_TITLES = intArrayOf(
            R.string.tab_text_1,
            R.string.tab_text_2,
            R.string.tab_text_3
    )
}
```

Sehingga full kode dari file **MainActivity** sebagai berikut:

```kotlin
package com.m0521074.ayuk.tablayout

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.annotation.StringRes
import androidx.viewpager2.widget.ViewPager2
import com.google.android.material.tabs.TabLayout
import com.google.android.material.tabs.TabLayoutMediator
import layout.SectionPagerAdapter

class MainActivity : AppCompatActivity() {

    companion object {
        @StringRes
        private val TAB_TITLES = intArrayOf(
            R.string.tab_text_1,
            R.string.tab_text_2,
            R.string.tab_text_3
        )
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val sectionsPagerAdapter = SectionPagerAdapter(this)
        val viewPager: ViewPager2 = findViewById(R.id.view_pager)
        viewPager.adapter = sectionsPagerAdapter
        val tabs: TabLayout = findViewById(R.id.tabs)
        TabLayoutMediator(tabs, viewPager) { tab, position ->
            tab.text = resources.getString(TAB_TITLES[position])
        }.attach()

        supportActionBar?.elevation = 0f
    }
}
```

5. Sekarang jalankan kembali projek nya dan aplikasi kalian akan menjadi seperti di bawah ini.

![simulesyen_2](assets/simulesyen2.gif)

 ### Mengirimkan data dari Activity ke Fragment

 Terkadang diperlukan data dari Activity untuk dikonsumsi di dalam Fragment, seperti nama tab atau variabel lainnya. Untuk caranya dengan dikirim data nya terlebih dahulu dari Activity ke SectionPagerAdapter menggunakan constructor atau setter kemudian dikirimkan lagi data tersebut ke Fragment. Contoh nya seperti kode di bawah.

 ```kotlin
cclass SectionsPagerAdapter(activity: AppCompatActivity) : FragmentStateAdapter(activity) {
 
    var appName: String = ""
    ...
}
```

Kemudian masukkan data yang ingin dikirimkan dari Activity:

```kotlin
val sectionsPagerAdapter = SectionsPagerAdapter(this)
sectionsPagerAdapter.appName = resources.getString(R.string.app_name)
```

Setelah data terkirim ke adapter, maka langkah selanjutnya adalah mengirimkannya kembali ke Fragment seperti cara pada codelab. Yakni siapkan terlebih dahulu key baru pada Fragment seperti ini:

```kotlin
class HomeFragment : Fragment() {
    ...
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        ...
        val index = arguments?.getInt(ARG_SECTION_NUMBER, 0)
        val name = arguments?.getString(ARG_NAME)
        ...
    }
 
    companion object {
        const val ARG_SECTION_NUMBER = "section_number"
        const val ARG_NAME = "app_name"
    }
}
```

Kemudian kirimkan data pada SectionsPagerAdapter seperti berikut:

```kotlin
override fun createFragment(position: Int): Fragment {
    val fragment = HomeFragment()
    fragment.arguments = Bundle().apply {
        putInt(HomeFragment.ARG_SECTION_NUMBER, position + 1)
        putString(HomeFragment.ARG_NAME, appName)
    }
    return fragment
}
```

Jika ingin mendalami mengenai penerapan animasi ketia ViewPAger digeser, kalian dapat belajar mandiri melalui dokumentasi di bawah ini.

[PageTransformer](https://developer.android.com/develop/ui/views/animations/screen-slide-2#pagetransformer)