# Laporan Proyek Machine Learning - Yosriko Rahmat Karoni Sabelekake

## Project Overview

Dengan semakin meningkatnya jumlah aplikasi di Play Store, pengguna sering kali dibanjiri dengan berbagai pilihan yang beragam dan kesulitan menemukan aplikasi yang benar-benar sesuai dengan kebutuhan mereka. Sebagai contoh, pencarian aplikasi pendidikan bisa menampilkan ribuan hasil dengan kualitas dan fungsionalitas yang bervariasi. Dalam kondisi ini, sistem rekomendasi sangat diperlukan untuk membantu menyaring dan menampilkan aplikasi yang lebih relevan sesuai preferensi pengguna (Abdulghani dkk, 2020).

Pengembangan model rekomendasi berbasis konten untuk aplikasi Android memiliki beberapa keunggulan. Model ini menggunakan fitur-fitur seperti rating, jumlah ulasan, genre, dan deskripsi aplikasi untuk memberikan rekomendasi yang lebih tepat. Salah satu alasan utama pentingnya model ini adalah kemampuannya untuk bekerja tanpa memerlukan data dari pengguna lain, sehingga dapat tetap berfungsi optimal meskipun data pengguna terbatas. Hal ini menjadikan sistem rekomendasi berbasis konten sangat cocok untuk platform atau pengguna baru yang belum memiliki banyak histori interaksi.

Selain itu, dengan mempertimbangkan berbagai atribut aplikasi seperti rating yang mencerminkan kualitas aplikasi, jumlah ulasan sebagai indikator popularitas, serta genre yang sesuai dengan kategori minat pengguna, model ini dapat memberikan hasil yang lebih dipersonalisasi. Pengguna akan mendapatkan rekomendasi aplikasi yang lebih akurat, sehingga mereka dapat lebih mudah menemukan aplikasi yang tepat tanpa harus melalui banyak pilihan yang tidak relevan.
  
Referensi: [A Recommender System for Mobile Applications of Google Play Store](https://www.researchgate.net/publication/346077457_A_Recommender_System_for_Mobile_Applications_of_Google_Play_Store) 

***
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
***
## Data Understanding

Dataset yang digunakan dapat diakses di tautan berikut: [kaggle](https://www.kaggle.com/datasets/lava18/google-play-store-apps)  
Informasi dari dataset dapat dilihat pada tabel dibawah ini:  

| Jenis                  | Keterangan                                                                                                        |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Sumber                 | [Google Play Store Apps](https://www.kaggle.com/datasets/lava18/google-play-store-apps)               |
| Lisensi                | Creative Commons Attribution 3.0 Unported License                                     |
| Jenis & Ukuran berkas  | ZIP (2 MB)                                                                                                   |  
| Isi berkas  | googleplaystore.csv & googleplaystore_user_reviews.csv                                                                      |  
| Jumlah baris dan kolom | 10841 x 13

		
Untuk penjelasan mengenai 13 kolom yaitu sebagai berikut:  
| Field           | Description                                                                                                      |
|-----------------|------------------------------------------------------------------------------------------------------------------|
| App             | Nama aplikasi di Google Play Store.                                                                              |
| Category        | Kategori aplikasi, seperti "ART_AND_DESIGN", "ENTERTAINMENT", dll.                                               |
| Rating          | Penilaian pengguna dalam bentuk skor, biasanya dari 1 hingga 5.                                                  |
| Reviews         | Jumlah ulasan dari pengguna.                                                                                     |
| Size            | Ukuran aplikasi. Biasanya dalam format MB atau KB.                                                               |
| Installs        | Jumlah pengunduhan aplikasi dalam bentuk angka dengan tanda “+” (misalnya, 10,000+).                             |
| Type            | Jenis aplikasi: Free atau Paid.                                                                                  |
| Price           | Harga aplikasi. Untuk aplikasi gratis, biasanya diisi dengan 0.                                                  |
| Content Rating  | Rating konten, menunjukkan usia pengguna yang disarankan.                                                        |
| Genres          | Genre atau subkategori aplikasi.                                                                                 |
| Last Updated    | Tanggal pembaruan terakhir aplikasi.                                                                             |
| Current Ver     | Versi aplikasi saat ini.                                                                                        |
| Android Ver     | Versi minimum Android yang diperlukan untuk menjalankan aplikasi.                                               |

Preview data:
| App                                                 | Category      | Rating | Reviews | Size | Installs     | Type | Price | Content Rating | Genres                  | Last Updated     | Current Ver           | Android Ver    |
|-----------------------------------------------------|---------------|--------|---------|------|--------------|------|-------|----------------|-------------------------|------------------|------------------------|----------------|
| Photo Editor & Candy Camera & Grid & ScrapBook      | ART_AND_DESIGN| 4.1    | 159     | 19M  | 10,000+      | Free | 0     | Everyone       | Art & Design            | January 7, 2018  | 1.0.0                  | 4.0.3 and up   |
| Coloring book moana                                 | ART_AND_DESIGN| 3.9    | 967     | 14M  | 500,000+     | Free | 0     | Everyone       | Art & Design;Pretend Play| January 15, 2018 | 2.0.0                  | 4.0.3 and up   |
| U Launcher Lite – FREE Live Cool Themes, Hide ...   | ART_AND_DESIGN| 4.7    | 87510   | 8.7M | 5,000,000+   | Free | 0     | Everyone       | Art & Design            | August 1, 2018   | 1.2.4                  | 4.0.3 and up   |
| Sketch - Draw & Paint                               | ART_AND_DESIGN| 4.5    | 215644  | 25M  | 50,000,000+  | Free | 0     | Teen           | Art & Design            | June 8, 2018     | Varies with device     | 4.2 and up     |
| Pixel Draw - Number Art Coloring Book               | ART_AND_DESIGN| 4.3    | 967     | 2.8M | 100,000+     | Free | 0     | Everyone       | Art & Design;Creativity | June 20, 2018    | 1.1                    | 4.4 and up     |

### Kondisi data
| Column          | Non-Null Count | Dtype   | Missing Count |
|-----------------|----------------|---------|---------------|
| App             | 10841          | object  | 0             |
| Category        | 10841          | object  | 0             |
| Rating          | 9367           | float64 | 1474          |
| Reviews         | 10841          | object  | 0             |
| Size            | 10841          | object  | 0             |
| Installs        | 10841          | object  | 0             |
| Type            | 10840          | object  | 1             |
| Price           | 10841          | object  | 0             |
| Content Rating  | 10840          | object  | 1             |
| Genres          | 10841          | object  | 0             |
| Last Updated    | 10841          | object  | 0             |
| Current Ver     | 10833          | object  | 8             |
| Android Ver     | 10838          | object  | 3             |

### Installs and numbers of application corelation

![Visual](images/Installs.png?raw=true)

Distribusi ini dapat mencerminkan preferensi dan perilaku konsumen terkait dengan instalasi aplikasi. Sebagai contoh, sebagian besar aplikasi masuk dalam kategori "1M and above", ini bisa menunjukkan tren di mana pengguna lebih menyukai aplikasi yang sudah mapan atau populer. Hal ini menjadikan installs dapat menjadi salah satu parameter penentu rekomendasi

***

## Data Preparation

- Cleaning Data: Membersihkan data dari nilai-nilai yang hilang dan memperbaiki format data.
- Minmaxscaler: menormalisasi kolom Installs, sehingga memudahkan dalam analisis atau pemodelan data dengan skala yang seragam (0-1)

$$
X_{\text{scaled}} = \frac{X - X_{\text{min}}}{X_{\text{max}} - X_{\text{min}}}
$$

- Text Preprocessing: Melakukan pemrosesan teks untuk menggabungkan beberapa atribut untuk selanjutnya di tokenisasi, agar query dapat menjadi lebih general dan tidak terbatas nama aplikasi
- Feature Extraction: Menggunakan TF-IDF untuk mengekstrak fitur-fitur dari teks deskripsi aplikasi.

$$
\text{TF-IDF}(t,d,D) = \text{TF}(t,d) \times \text{IDF}(t,D)
$$


## Modeling

### Top-N Recommendation
Sistem ini mampu memberikan rekomendasi teratas berdasarkan **cosine similarity** antara aplikasi yang ada dan input query pengguna. Berikut adalah contoh fungsi yang memberikan rekomendasi teratas:

```python
def get_recommendations_from_query(query, alpha=0.7):
    # Transformasikan query pengguna menggunakan vektor TF-IDF
    query_tfidf = tfidf.transform([query.lower()])

    # Hitung kesamaan kosinus antara query dan semua aplikasi dalam dataset
    cosine_sim_query = linear_kernel(query_tfidf, tfidf_matrix).flatten()

    # Buat DataFrame sementara untuk menyimpan hasil dan urutkan
    df_temp = df_clean.copy()
    df_temp['cosine_sim'] = cosine_sim_query

    # Sort berdasarkan cosine similarity (descending) terlebih dahulu,
    # jika sama, urutkan berdasarkan installs (descending juga)
    df_temp = df_temp.sort_values(by=['cosine_sim', 'Installs'], ascending=[False, False])

    # Ambil top-10 aplikasi yang direkomendasikan
    top_recommendations = df_temp[['App', 'cosine_sim', 'Installs']].head(10)

    return top_recommendations
```

`query` adalah parameter berupa teks yang dimasukkan oleh pengguna untuk mencari aplikasi yang relevan. Fungsi ini akan memproses teks tersebut untuk diubah menjadi representasi vektor yang dapat dihitung kesamaannya dengan aplikasi dalam dataset.

Parameter `alpha`, dengan nilai default 0.7, adalah nilai berupa angka desimal (float) yang dapat digunakan untuk memberikan bobot pada skor cosine similarity atau untuk dikombinasikan dengan faktor lain (misalnya popularitas atau rating aplikasi). Meskipun dalam fungsi ini alpha belum digunakan, parameter ini bisa berguna jika nanti ingin memberikan penyesuaian bobot rekomendasi.

Pada bagian `query_tfidf`, fungsi `tfidf.transform([query.lower()])` digunakan untuk mengonversi teks query menjadi vektor dengan metode TF-IDF (Term Frequency-Inverse Document Frequency), yang menghasilkan representasi query yang mencerminkan frekuensi kata penting dalam konteks dataset.

Lalu, variabel `cosine_sim_query` adalah hasil dari perhitungan `linear_kernel(query_tfidf, tfidf_matrix).flatten()`, yang digunakan untuk menghitung cosine similarity antara query dan setiap aplikasi dalam dataset. Fungsi linear_kernel akan menghasilkan matriks kesamaan antara query_tfidf dan tfidf_matrix, sementara flatten mengubahnya menjadi array satu dimensi untuk memudahkan pemrosesan lebih lanjut. Nilai cosine similarity akan berkisar antara 0 hingga 1, di mana nilai yang lebih tinggi menandakan kesamaan yang lebih besar.

`df_temp` adalah salinan dari dataset aplikasi asli (`df_clean`) yang digunakan untuk menampung hasil rekomendasi, dengan kolom tambahan cosine_sim yang menyimpan skor cosine similarity antara query dan setiap aplikasi dalam dataset.

Dalam proses pengurutan, `df_temp` diurutkan terlebih dahulu berdasarkan kolom `cosine_sim` secara menurun (descending) agar aplikasi dengan skor cosine similarity tertinggi berada di posisi atas, yang menunjukkan bahwa aplikasi tersebut paling relevan terhadap query pengguna. Jika terdapat aplikasi dengan nilai cosine similarity yang sama, pengurutan berikutnya dilakukan berdasarkan kolom Installs dalam urutan menurun sebagai pengganti untuk menunjukkan aplikasi yang lebih populer.

Bagian terakhir dari fungsi adalah variabel `top_recommendations`, yang mengambil 10 aplikasi teratas berdasarkan hasil pengurutan dan menampilkannya sebagai hasil rekomendasi untuk ditampilkan kepada pengguna.

***
**Content-Based Filtering:**

**Deskripsi:** Menggunakan fitur konten dari aplikasi untuk merekomendasikan aplikasi yang relevan.

**Cosine Similarity:**
Cosine similarity mengukur sudut kosinus antara dua vektor dalam ruang multidimensi yang merepresentasikan atribut dari aplikasi. Nilai cosine similarity berkisar antara -1 hingga 1, di mana nilai 1 menunjukkan kesamaan yang sempurna, 0 menunjukkan tidak ada hubungan, dan -1 menunjukkan perbedaan total.

Dalam konteks rekomendasi aplikasi, vektor ini dapat berupa representasi fitur seperti kategori, kata kunci, atau deskripsi aplikasi. Jika dua aplikasi memiliki fitur yang mirip, cosine similarity mereka akan tinggi, dan aplikasi tersebut kemungkinan besar akan direkomendasikan kepada pengguna.

$$
\text{cosine\_similarity} = \frac{\sum_{i=1}^{n} A_i B_i}{\sqrt{\sum_{i=1}^{n} A_i^2} \cdot \sqrt{\sum_{i=1}^{n} B_i^2}}
$$


**Kelebihan:**
- Tidak memerlukan data pengguna lain.
- Rekomendasi lebih personal berdasarkan minat spesifik pengguna.

**Kekurangan:**
- Keterbatasan dalam mengeksplorasi aplikasi yang tidak dikenal pengguna.
- Mungkin menghasilkan rekomendasi yang terlalu mirip (serupa).

## TOP-N RESULT

Hasil testing model menunjukkan index atau urutan aplikasi yang sesuai dengan query **"Coloring book moana"**

|    | App                                      | cosine_sim | Installs |
|----|------------------------------------------|------------|----------|
| 1  | Coloring book moana                      | 0.744337   | 500000   |
| 2033 | Coloring book moana                    | 0.744337   | 500000   |
| 7010 | Pixyfy: coloring by number coloring book | 0.510429   | 500000   |
| 5628 | Coloring Book at Five Nights           | 0.502382   | 100000   |
| 8298 | Coloring Book for Me & Mandala         | 0.484044   | 10000000 |
| 705  | Princess Coloring Book                 | 0.457244   | 5000000  |
| 2025 | Princess Coloring Book                 | 0.457244   | 5000000  |
| 8   | Garden Coloring Book                    | 0.435604   | 1000000  |
| 13  | Mandala Coloring Book                   | 0.426164   | 100000   |
| 1771 | Color by Number – New Coloring Book    | 0.418503   | 5000000  |


## Evaluation

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
<<<<<<< Updated upstream
| Precision  | 70.00%                |
| Recall     | 100.00%                |
| F1-Score   | 82.35%   |
|Accuracy|100.00%|
=======
| Precision  | 10.00%                 |
| Recall     | 100.00%               |
| F1-Score   | 18.18%   |
>>>>>>> Stashed changes

**Menjawab Problem Statement:** Model ini berhasil menjawab problem statement dengan baik. Sistem rekomendasi berbasis konten mampu memberikan rekomendasi aplikasi yang relevan berdasarkan deskripsi aplikasi dan atribut lainnya, seperti rating dan genre. Selain itu, sistem ini juga dapat memberikan rekomendasi personal tanpa memerlukan data pengguna lain, sesuai dengan problem statement yang kedua.

**Pencapaian Goals:** Sistem ini mencapai goals yang ditetapkan, yaitu mengembangkan sistem rekomendasi berbasis konten yang membantu pengguna menemukan aplikasi sesuai preferensi mereka di Play Store. Model menggunakan TF-IDF untuk ekstraksi fitur deskripsi aplikasi dan cosine similarity untuk menghitung kesamaan, memungkinkan pengguna mendapatkan aplikasi yang mirip dengan minat mereka.

**Dampak Solusi Terhadap Bisnis:** Solusi yang dirancang memiliki dampak positif pada bisnis. Sistem ini meningkatkan user experience dengan memberikan rekomendasi yang relevan, berpotensi meningkatkan konversi aplikasi yang diunduh, serta mengurangi ketergantungan pada data pengguna lain, yang penting untuk menjaga privasi pengguna dan mematuhi regulasi.

**Ruang Perbaikan:** Meskipun berhasil, masih ada ruang untuk meningkatkan variasi rekomendasi agar tidak terlalu mirip satu sama lain, dan meningkatkan nilai Precision untuk memastikan aplikasi yang direkomendasikan lebih sesuai dengan kebutuhan pengguna. Hal ini akan membantu memperluas cakupan aplikasi yang dapat dieksplorasi oleh pengguna.

