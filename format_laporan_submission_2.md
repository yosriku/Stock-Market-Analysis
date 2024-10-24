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
- Installs: jumlah penginstallan aplikasi.

### Melihat korelasi dan pesebaran beberapa atribut

#### Installs

![Install Images](images/Installs.png?raw=true)

#### Installs vs Rating

![Rating Images](images/Score.png?raw=true)


## Data Preparation

- Cleaning Data: Membersihkan data dari nilai-nilai yang hilang dan memperbaiki format data.
- Text Preprocessing: Melakukan pemrosesan teks pada kolom deskripsi aplikasi, seperti tokenisasi, stemming, dan menghilangkan stopwords untuk membuatnya lebih relevan dalam rekomendasi.
- Feature Extraction: Menggunakan TF-IDF untuk mengekstrak fitur-fitur dari teks deskripsi aplikasi.

$$
\text{TF-IDF}(t,d,D) = \text{TF}(t,d) \times \text{IDF}(t,D)
$$

## Modeling

### Top-N Recommendation
Sistem ini mampu memberikan rekomendasi teratas berdasarkan **cosine similarity** antara aplikasi yang ada dan input query pengguna. Berikut adalah contoh fungsi yang memberikan rekomendasi teratas:

```python
# Fungsi untuk rekomendasi berdasarkan input query
def get_recommendations_from_query(query, alpha=0.7):
    # Transformasikan query pengguna menggunakan vektor TF-IDF
    query_tfidf = tfidf.transform([query.lower()])
    
    # Hitung kesamaan kosinus antara query dan semua aplikasi dalam dataset
    cosine_sim_query = linear_kernel(query_tfidf, tfidf_matrix).flatten()
    
    # Buat DataFrame sementara untuk menyimpan hasil dan urutkan
    df_temp = df_clean.copy()
    df_temp['cosine_sim'] = cosine_sim_query
    
    # Sort berdasarkan cosine similarity dan installs
    df_temp = df_temp.sort_values(by=['cosine_sim', 'installs'], ascending=[False, False])
    
    # Ambil top-10 aplikasi yang direkomendasikan
    top_recommendations = df_temp[['title', 'cosine_sim', 'installs']].head(10)

    return top_recommendations
```

**Content-Based Filtering:**
**Deskripsi: **Menggunakan fitur konten dari aplikasi (title, genre, dan deskripsi) untuk merekomendasikan aplikasi yang relevan.

**Kelebihan:**
- Tidak memerlukan data pengguna lain.
- Rekomendasi lebih personal berdasarkan minat spesifik pengguna.

**Kekurangan:**
- Keterbatasan dalam mengeksplorasi aplikasi yang tidak dikenal pengguna.
- Mungkin menghasilkan rekomendasi yang terlalu mirip (serupa).

## Testingg

Hasil testing model menunjukkan index atau urutan aplikasi yang sesuai dengan query yang diberikan

![Hasil Testing](images/Hasil.png?raw=true)

## Metrik Evaluasi

### 1. **Precision @ K**

Definisi: Mengukur berapa banyak aplikasi relevan yang ada dalam N rekomendasi teratas.

$$
\text{Precision@K} = \frac{\text{Jumlah aplikasi relevan yang direkomendasikan}}{K}
$$

### 2. **Recall @ K**

Definisi: Mengukur seberapa banyak aplikasi relevan ditemukan dari semua aplikasi relevan.

$$
\text{Recall@K} = \frac{\text{Jumlah aplikasi relevan yang direkomendasikan}}{\text{Jumlah total aplikasi relevan}}
$$

### 3. **F1-Score**

Definisi: Kombinasi dari Precision dan Recall.

$$
F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$


### Hasil

Hasil dicoba dengan menggunakan aplikasi ABC Kids - Tracing & Phonics dan HelloTalk: Pembelajaran Bahasa dengan query "Belajar Inggris"
| Metric     | Value                |
|------------|----------------------|
| Precision  | 0.2                  |
| Recall     | 1.0                  |
| F1-Score   | 0.33333333333333337   |

