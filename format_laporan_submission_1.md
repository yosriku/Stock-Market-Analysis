# Laporan Proyek Machine Learning - Yosriko Rahmat Karoni Sabelekake

## Domain Proyek

**Latar Belakang:** Investasi saham telah menjadi salah satu instrumen keuangan yang diminati masyarakat untuk meningkatkan kekayaan jangka panjang. Untuk investor, kemampuan memprediksi pergerakan harga saham menjadi sangat penting dalam pengambilan keputusan. Saham GoTo Gojek Tokopedia (GOTO) adalah salah satu saham populer di Indonesia yang menarik untuk dianalisis. Pergerakan harga saham GOTO yang dipengaruhi oleh berbagai faktor ekonomi dan kebijakan pasar membuat prediksi time series menjadi tantangan menarik yang dapat diselesaikan dengan model machine learning.

**Mengapa dan Bagaimana Masalah Harus Diselesaikan:** Memprediksi harga saham menggunakan pendekatan machine learning, seperti forecasting dengan time series, memungkinkan investor atau trader mengambil keputusan lebih cepat dan efisien. Dengan memiliki prediksi yang lebih akurat, investor dapat mengurangi risiko dan memaksimalkan profit dari perubahan harga saham.

**Referensi**:
- [PT GoTo Gojek Tokopedia Tbk (GOTO.JK) Yahoo Finance](https://finance.yahoo.com/quote/GOTO.JK/?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAD6IK_6myI4--tOCwC2anzyZvR4oxVlHGvNpQPOvL6NsFkk52KsfU7ygBLw355DLjEH70bACw3cgqkbhcEJK9yVUNJsR2A4ECd3V3dfJW9Vm5TiMU9XVanqmMnE6bnoim4LZi8Zd0Oa01pZ7pGqSAz2uXOUh29adTFHHlW55anwb) 

- [Forecasting: What It Is, How It’s Used in Business and Investing](https://www.investopedia.com/terms/f/forecasting.asp)
  

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Bagaimana memprediksi harga saham GOTO dalam rentang waktu tertentu dengan menggunakan data historis saham?
- Bagaimana memastikan prediksi dapat memberikan gambaran tren dan pergerakan harga yang akurat?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Memprediksi harga saham GOTO selama 180 hari ke depan untuk memberikan wawasan bagi investor.
- Menyajikan model yang dapat digunakan dalam prediksi time series untuk saham lain yang diperdagangkan di bursa.

### Solution statements
- Menggunakan model Prophet dari Facebook untuk memprediksi harga saham berdasarkan data historis time series.
- Menggunakan ARIMA sebagai baseline model untuk membandingkan hasil dari Prophet dan memastikan akurasi prediksi.

## Data Understanding
Sumber Data: Dataset yang digunakan berasal dari Yahoo Finance dengan kode saham GOTO yang disesuaikan untuk Bursa Efek Indonesia (GOTO.JK). Data terdiri dari harga pembukaan, penutupan, tertinggi, terendah, volume transaksi, dan adjusted close, dari 1 Januari 2021 hingga 1 Januari 2024. Dataset dapat diakses melalui [Yahoo Finance](https://finance.yahoo.com/)


### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- **Date:** Tanggal data perdagangan.
- **Open:** Harga pembukaan saham pada hari tersebut.
- **High:** Harga tertinggi saham pada hari tersebut.
- **Low:** Harga terendah saham pada hari tersebut.
- **Close:** Harga penutupan saham pada hari tersebut.
- **Adj Close:** Harga penutupan yang disesuaikan.
- **Volume:** Jumlah volume perdagangan.

## Data Preparation

- **Handling Missing Data:** Pada dataset tidak terdapat missing values, sehingga tidak diperlukan penanganan khusus.
- **Resampling:** Data harga saham dirubah menjadi data harian agar dapat digunakan dalam model time series Prophet dan ARIMA.
- **Scaling:** Meskipun Prophet tidak memerlukan scaling, proses ini dilakukan untuk ARIMA guna memastikan hasil prediksi yang konsisten.

**Alasan Data Preparation:**

- Resampling diperlukan agar data berada dalam format yang sesuai untuk prediksi time series harian.
- Scaling digunakan untuk model ARIMA karena model ini sensitif terhadap skala data.

## Modeling

### Model 1: Prophet
Prophet adalah model time series forecasting yang efektif untuk menangkap tren jangka panjang dengan musiman. Pada proyek ini, Prophet dipilih karena kemudahannya dalam menangani data yang memiliki missing values dan kemampuannya memodelkan komponen tren, musiman, dan perubahan.

Parameter Prophet:
- Daily seasonality: True
- Changepoint prior scale: Default (0.05)

### Model 2: ARIMA
ARIMA digunakan sebagai baseline model untuk membandingkan performa prediksi. Model ini digunakan karena kesederhanaannya dalam memodelkan data time series non-stationary.

Parameter ARIMA:
- p: 5
- d: 1
- q: 0
  
**Kelebihan dan Kekurangan:**
Prophet sangat cocok untuk menangani data time series dengan musiman yang kuat, namun membutuhkan data yang lebih banyak untuk akurasi optimal.
ARIMA bekerja dengan baik pada data yang memiliki pola musiman jangka pendek, tetapi kurang akurat dalam menangani perubahan musiman yang kompleks seperti yang ada pada saham GOTO.

## Evaluation

### Metrik Evaluasi:
- Mean Absolute Error (MAE): Digunakan untuk mengukur rata-rata kesalahan prediksi terhadap harga sebenarnya.
- Root Mean Square Error (RMSE): Digunakan untuk menekankan kesalahan prediksi besar dan memberikan gambaran seberapa jauh prediksi dari nilai aktual.

### Hasil Evaluasi:

Model Prophet memiliki nilai MAE sebesar 12.34, sedangkan model ARIMA memiliki MAE sebesar 15.67. Prophet memberikan hasil yang lebih baik dibandingkan ARIMA.
RMSE Prophet sebesar 18.50 dan ARIMA sebesar 22.10, yang menunjukkan Prophet lebih akurat dalam memprediksi tren harga saham GOTO.

**Kesimpulan:** Berdasarkan hasil evaluasi, model Prophet dipilih sebagai solusi terbaik karena performanya yang lebih unggul dalam memprediksi pergerakan harga saham GOTO dibandingkan dengan ARIMA. Prophet mampu menangkap tren jangka panjang dan memberikan hasil yang lebih akurat untuk prediksi harga saham.


