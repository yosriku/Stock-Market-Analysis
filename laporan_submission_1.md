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

|Date|Close|Close|High&|Low|Open|Volume|
|---|---|---|---|---|---|---|
|2022-04-11 00:00:00+00:00|382\.0|382\.0|416\.0|372\.0|400\.0|9410897000|
|2022-04-12 00:00:00+00:00|370\.0|370\.0|442\.0|360\.0|422\.0|3887331000|
|2022-04-13 00:00:00+00:00|374\.0|374\.0|380\.0|360\.0|370\.0|3262811400|
|2022-04-14 00:00:00+00:00|376\.0|376\.0|382\.0|374\.0|374\.0|3675981900|
|2022-04-18 00:00:00+00:00|378\.0|378\.0|380\.0|370\.0|376\.0|2660312700|
|2022-04-19 00:00:00+00:00|358\.0|358\.0|380\.0|358\.0|378\.0|2252971800|
|2022-04-20 00:00:00+00:00|338\.0|338\.0|364\.0|338\.0|358\.0|5804281200|
|2022-04-21 00:00:00+00:00|340\.0|340\.0|340\.0|336\.0|340\.0|1670584600|
|2022-04-22 00:00:00+00:00|340\.0|340\.0|340\.0|330\.0|340\.0|6075753400|
|2022-04-25 00:00:00+00:00|328\.0|328\.0|338\.0|318\.0|318\.0|1960587900|
|2022-04-26 00:00:00+00:00|310\.0|310\.0|348\.0|308\.0|348\.0|1843997100|
|2022-04-27 00:00:00+00:00|290\.0|290\.0|310\.0|290\.0|300\.0|2077577300|
|2022-04-28 00:00:00+00:00|272\.0|272\.0|290\.0|270\.0|270\.0|2280309800|
|2022-05-09 00:00:00+00:00|254\.0|254\.0|270\.0|254\.0|254\.0|621345600|
|2022-05-10 00:00:00+00:00|238\.0|238\.0|254\.0|238\.0|254\.0|201334400|
|2022-05-11 00:00:00+00:00|222\.0|222\.0|238\.0|222\.0|224\.0|2942404500|
|2022-05-12 00:00:00+00:00|208\.0|208\.0|220\.0|208\.0|212\.0|312982800|


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

|Metrics|Result|
|---|---|
|MAE Prophet| 17.6285819313176|
|RMSE Prophet| 25.876196885311575|
|MAE ARIMA| 6.105609482323135|
|RMSE ARIMA| 20.40746911530558|

Berdasarkan evaluasi performa, model ARIMA menghasilkan nilai MAE sebesar 6.11 dan RMSE sebesar 20.41. Sedangkan model Prophet memiliki MAE sebesar 17.63 dan RMSE sebesar 25.88. Dari hasil ini, ARIMA lebih unggul dalam hal akurasi prediksi dibandingkan Prophet pada data saham GOTO.

**Kesimpulan:** Meskipun Prophet dirancang untuk menangkap tren jangka panjang, pada dataset ini ARIMA memberikan hasil yang lebih akurat dalam memprediksi harga saham GOTO. Oleh karena itu, model ARIMA dipilih sebagai solusi terbaik berdasarkan performa evaluasi yang lebih baik pada metrik MAE dan RMSE dibandingkan dengan Prophet.


