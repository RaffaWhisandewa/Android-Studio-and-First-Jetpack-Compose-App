# Homework 6_Android Studio and First Jetpack Compose App

## Task 3: Colour and Spacing
Colour used: `Color.LightGray`

Padding kept: 20 dp

What changed / what stayed the same: Dari 8 dp ke 48 dp, jarak kosong antara tepi layar dan isi (dua teks dan gambar) berubah. Pada 8 dp isi hampir menempel ke tepi layar, sedangkan pada 48 dp isi bergeser ke dalam dan area yang tersedia untuk teks dan gambar menjadi lebih sempit. Yang tetap sama adalah warna latar Surface, isi dua teks, gambar, dan urutan susunannya di dalam Column. Ini mirip dengan margin berwarna kuning pada Module M06, Figure 13: padding adalah ruang kosong di antara tepi Column dan isinya, bukan bagian dari isinya.

## Task 4: Build Error
First error message:
```
'M' is not a valid file based resource name character: File based resource names must contain only lowercase a-z, 0-9, or underscore
```
(Task `:app:packageDebugResources` FAILED, file: `app\src\main\res\drawable\My-Picture.png`)

Cause: Nama file resource di folder `res/drawable` hanya boleh berisi huruf kecil a-z, angka 0-9, dan underscore. File `My-Picture.png` melanggar aturan ini karena memakai huruf besar (`M` dan `P`) dan tanda hubung (`-`). Build berhenti pada karakter pertama yang salah, yaitu `M`.

Why other errors appear: Karena nama file tidak valid, Android tidak bisa membuat ID `R.drawable.my_picture`. Kode di `MainActivity.kt` yang memakai ID itu lalu menghasilkan error seperti *unresolved reference*. Error berikutnya hanyalah akibat dari error pertama, jadi yang diperbaiki cukup penyebab pertama.

Fix: Mengganti nama file kembali menjadi `my_picture.png` huruf kecil semua, underscore, memastikan kode memakai `R.drawable.my_picture`, lalu build ulang. Proyek bisa build dan berjalan lagi.

## Task 5: Explore the Project
a. MainActivity: path `app/src/main/java/com/example/myfirstcomposeapp/MainActivity.kt` file ini berisi class `MainActivity`, titik masuk aplikasi yang memanggil `setContent { }` untuk menampilkan UI Compose.

b. Gradle file: path `app/build.gradle.kts` file ini mengatur konfigurasi modul app, seperti `compileSdk`, `minSdk`, `targetSdk`, dan daftar library yang dipakai dependencies.

c. Launcher image line: `painterResource(id = R.drawable.ic_launcher_foreground)` di dalam `Image(...)` pada fungsi `MyFirstScreen` di `MainActivity.kt` baris ini mengambil gambar launcher dari folder `res/drawable` untuk ditampilkan di layar.

## Task 6: Preview vs Run
Saya mengubah satu teks di `MyFirstScreen` yaitu di bagian nama lengkap yang awalnya "Hai, Perkenalkan namaku Raffa Whisandewa Wibowo." menjadi "Hai, Perkenalkan namaku Bowowowowowowo Raffa Whisandewa Wibowo.", Setelah itu Preview `MyFirstScreenPreview` langsung berubah otomatis, tetapi aplikasi di emulator masih menampilkan teks yang lama. Emulator baru berubah setelah saya menekan tombol Run.

Penyebabnya, Preview hanya menggambar ulang fungsi composable di dalam Android Studio tanpa menjalankan aplikasi. Aplikasi di emulator adalah hasil build sebelumnya yang sudah terinstall, sehingga tidak ikut berubah. Agar perubahan muncul di emulator atau HP, saya tekan Run dulu supaya proyek di build ulang, lalu aplikasi baru di install dan dijalankan di perangkat.

## Task 7: Views vs Compose
1. Pada pendekatan **imperatif** Views, tampilan disusun di file XML, lalu di kode kita memberi perintah langkah demi langkah untuk mengubahnya, misalnya mencari TextView dengan `findViewById` lalu memanggil `setText(...)`. Kita mengatur *bagaimana* layar berubah. Pada pendekatan **deklaratif** Compose, kita cukup menjelaskan *seperti apa* layar seharusnya. Di `MyFirstScreen` milik saya, saya hanya menulis bahwa ada `Surface` berwarna abu-abu, berisi `Column` dengan dua `Text` dan satu `Image`, dengan padding 20 dp. Tidak ada perintah "cari lalu ubah". Kalau data atau teksnya berubah, Compose yang menggambar ulang tampilannya sendiri.

2.

| Composable | Package | Library layer |
|---|---|---|
| Column | `androidx.compose.foundation.layout` | Foundation |
| Text | `androidx.compose.material3` | Material |
| Image | `androidx.compose.foundation` | Foundation |
