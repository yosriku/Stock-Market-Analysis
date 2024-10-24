# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

Dengan semakin meningkatnya jumlah aplikasi di Play Store, pengguna sering kali dibanjiri dengan berbagai pilihan yang beragam dan kesulitan menemukan aplikasi yang benar-benar sesuai dengan kebutuhan mereka. Sebagai contoh, pencarian aplikasi pendidikan bisa menampilkan ribuan hasil dengan kualitas dan fungsionalitas yang bervariasi. Dalam kondisi ini, sistem rekomendasi sangat diperlukan untuk membantu menyaring dan menampilkan aplikasi yang lebih relevan sesuai preferensi pengguna (Abdulghani dkk, 2020).

Pengembangan model rekomendasi berbasis konten untuk aplikasi Android memiliki beberapa keunggulan. Model ini menggunakan fitur-fitur seperti rating, jumlah ulasan, genre, dan deskripsi aplikasi untuk memberikan rekomendasi yang lebih tepat. Salah satu alasan utama pentingnya model ini adalah kemampuannya untuk bekerja tanpa memerlukan data dari pengguna lain, sehingga dapat tetap berfungsi optimal meskipun data pengguna terbatas. Hal ini menjadikan sistem rekomendasi berbasis konten sangat cocok untuk platform atau pengguna baru yang belum memiliki banyak histori interaksi.

Selain itu, dengan mempertimbangkan berbagai atribut aplikasi seperti rating yang mencerminkan kualitas aplikasi, jumlah ulasan sebagai indikator popularitas, serta genre yang sesuai dengan kategori minat pengguna, model ini dapat memberikan hasil yang lebih dipersonalisasi. Pengguna akan mendapatkan rekomendasi aplikasi yang lebih akurat, sehingga mereka dapat lebih mudah menemukan aplikasi yang tepat tanpa harus melalui banyak pilihan yang tidak relevan.
  
Referensi: [A Recommender System for Mobile Applications of Google Play Store](https://www.researchgate.net/publication/346077457_A_Recommender_System_for_Mobile_Applications_of_Google_Play_Store) 

## Business Understanding

### Problem Statements
- Bagaimana memberikan rekomendasi aplikasi yang relevan berdasarkan informasi deskriptif aplikasi?
- Bagaimana menyajikan rekomendasi personal tanpa melibatkan data pengguna lain?

### Goals
- Mengembangkan sistem rekomendasi berbasis konten yang menggunakan atribut aplikasi seperti rating, ulasan, dan genre.
- Memudahkan pengguna menemukan aplikasi yang sesuai dengan preferensi mereka melalui Play Store.

### Solution Approach
- Content-Based Filtering: Membandingkan atribut aplikasi dengan preferensi pengguna.
- Tidak membutuhkan kolaborasi dengan data pengguna lain, sehingga fokus pada analisis konten aplikasi seperti yang disarankan Abdulghani dkk. (2020).

## Data Understanding
Menggunakan modul [google-play-scraper](https://pypi.org/project/google-play-scraper/) untuk mengambil data aplikasi dari Google Play. Informasi seperti judul aplikasi, rating, jumlah ulasan, genre, dan status gratis/berbayar digunakan dalam sistem rekomendasi.

| appId                                          | icon                                                                                          | screenshots                                                                                             | title                          | score     | genre      | price | free | currency | video                                                                                                | videoImage                                                                                     | description                                                        | developer     | installs     |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|--------------------------------|-----------|------------|-------|------|----------|------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|---------------|--------------|
| com.duolingo                                   | ![icon](https://play-lh.googleusercontent.com/vIMymGDz...)                                     | [screenshot](https://play-lh.googleusercontent.com/akiGQip...)                                          | Duolingo: Belajar Bahasa       | 4.775087  | Pendidikan | 0     | True | IDR      | None                                                                                                 | None                                                                                           | Belajar bahasa baru bersama aplikasi pendidikan...                  | Duolingo      | 500.000.000+ |
| com.google.android.apps.classroom              | ![icon](https://play-lh.googleusercontent.com/w0s3au7c...)                                     | [screenshot](https://play-lh.googleusercontent.com/aJ5Cxjd...)                                          | Google Kelas                   | 3.449997  | Pendidikan | 0     | True | IDR      | None                                                                                                 | None                                                                                           | Classroom memudahkan pelajar dan pengajar untuk...                 | Google LLC    | 100.000.000+ |
| com.microblink.photomath                       | ![icon](https://play-lh.googleusercontent.com/Ma_HEbK1...)                                     | [screenshot](https://play-lh.googleusercontent.com/OnXcxa_...)                                          | Photomath                      | 4.511481  | Pendidikan | 0     | True | IDR      | [video](https://www.youtube.com/embed/qd37NrZY2_4?ps=p...)                                           | ![videoImage](https://i.ytimg.com/vi/qd37NrZY2_4/hqdefault.jpg)                                 | Pelajari cara memecahkan soal matematika, memecah...                | Google LLC    | 100.000.000+ |
| com.quizlet.quizletandroid                     | ![icon](https://play-lh.googleusercontent.com/hiQHKRhp...)                                     | [screenshot](https://play-lh.googleusercontent.com/ZFOkNgi...)                                          | Quizlet: flashcard bertenaga AI | 4.730392  | Pendidikan | 0     | True | IDR      | [video](https://www.youtube.com/embed/q-cEib6fAfs?ps=p...)                                           | ![videoImage](https://i.ytimg.com/vi/q-cEib6fAfs/hqdefault.jpg)                                 | Quizlet adalah cara termudah untuk belajar, latihan...              | Quizlet Inc.  | 10.000.000+  |
| com.rvappstudios.baby.toddler.kids.games.learn | ![icon](https://play-lh.googleusercontent.com/gmTqub2o...)                                     | [screenshot](https://play-lh.googleusercontent.com/QUu0R_v...)                                          | Game Anak: Balita Usia 3-7     | 4.710744  | Edukasi    | 0     | True | IDR      | [video](https://www.youtube.com/embed/nFKJAhfzV5M?ps=p...)                                           | ![videoImage](https://i.ytimg.com/vi/nFKJAhfzV5M/hqdefault.jpg)                                 | Permainan aktivitas anak-anak guna membantu mempercepat perkembangan... | RV AppStudios | 50.000.000+  |
 

Variabel-variabel pada dataset yang akan digunakan adalah sebagai berikut:
- appId: ID unik dari aplikasi.
- title: Judul aplikasi.
- score: Rating atau skor aplikasi.
- genre: Kategori aplikasi, seperti pendidikan, hiburan, dll.
- price: Harga aplikasi.
- free: Status gratis atau berbayar.
- description: Deskripsi aplikasi.

### Melihat korelasi dan pesebaran beberapa atribut



## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
