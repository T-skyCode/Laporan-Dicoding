# Laporan Proyek Machine Learning - Adrian Juansyah Hasan

## Domain Proyek

Saat ini penyewaan apartemen atau rumah berkembang begitu pesat. hal ini dikarenakan dengan pertumbuhan pendduk yang sedemikian pesatnya, penyewaan apartemen atau rumah adalah salah satu usaha yang bergerak dibidang jasa yang dapat membantu para travelling atau perjalanan bisnis untuk mendapatkan kenyamanan dan keamanan dalam berpergian. Selain itu tidak semua manusia mampu memenuhi kebutuhan papan dengan memliki rumah atau apartemen sendiri. keterbatasan pemenuhan kebutuhan primer itu disebabkan kondisi ekonomi yang semakin tinggi. oleh karena itu sewa rumah atau apartemen sebagai salah satu alternatif untuk orang yang belum memliki tempat tinggal. maka dari pemaparan diatas dibuat sebuah model predictive analysis house/apartement Rent yang bertujuan untuk memprediksi harga penyewaan apartemen atau rumah pada masa yang akan datang.


**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa dan bagaimana masalah tersebut harus diselesaikan
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding

Harga pernyewaan rumah atau apartemen berbeda-beda, hal ini difaktori oleh beberapa fitur khusus. fitur tersebut seperti tempat, berapa banyak kasur, ukuran rumah atau apartemen, berapa lantai. tidak adanya acuan harga pasti pada penyewaan rumah atau apartemen menyebabkan memerlukan sistem untuk memprediksi harga.


### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Berapa harga penyewaan rumah atau apartemen dengan karateristik atau fitur tertentu?
- dari serangkaian fitur yang ada, fitur apa yang paling berpengaruh terhadap harga penyewaan rumah atau apartemen?
- 

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang paling berkorelasi dengan harga penyewaan rumah atau apartemen
- membuat model machine learning yang dapat memprediksi harga penyewaan rumah atau apartemen seakurat mungkin berdasarkan fitur-fitur yang ada.

### Solution statements
- Menggunakan 2 atau lebih algoritma untuk melihat kefektifitasan algoritma mana yang memiliki akurasi paling baik dalam memprediksi harga penyewaan rumah atau apartemen.

## Data Understanding

Data yang digunakan untuk membuat model ini adalah House Rent Prediction Dataset. Dataset berisikan 4700+ rumah yang siap untuk disewakan. karakteristik pada dataset terdiri dari dua jenis fitur numerik dan fitur non numerik. karakteristik numerik adalah BHK, Rent, Size, Bathroom. Karakteristik non numerik adalah Floor, Area Type, Area Locality, City, Furnishing Status. Fitur fitur inilah yang akan digunakan untuk menemukan pola pada data sedangkan rent merupakan fitur target. dataset ini bersumber [kaggle.com] https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset.

 
### Variabel-variabel pada House Rent Prediction Dataset adalah sebagai berikut:
- BHK : Berisikan banyaknya jumlah Bedrooms, Hall, Kitchen
- Rent : Berisikan harga sewa rumah atau apartemen
- Size : Berisikan luas dari rumah atau apartemen
- Floor : Berisikan jumlah keseluruhan lantai pada rumah atau apartemen
- Area Type : Berisikan tipe ukuran dari rumah atau apartemen
- Area Locality : Berisikan lokalitas dari rumah atau apartemen
- City : Berisikan wilayah kota pada rumah atau apartemen
- Furnishing Status : Berisikan status perlengkapan rumah pada rumah atau apartemen
- Bathroom : Berisikan banyaknnya kamar mandi pada rumah atau apartemen

## Data Preparation
Teknik data preparation yang digunakan pada pembuatan model ini adalah : 
- encoding fitur categori
data yang masih berbentuk kategori akan diubah menjadi data numerikal agar data dapat masuk ke pelatihan model.
- Split dataset dengan train_test_split
data akan dibagi menjadi data pelatihan dan data testing, data pelatihan akan dimasukan ke dalam pelatihan model lalu akan menghasilkan prediksi. untuk mengetes hasil prediksi itu digunakanlah data testing
- Standarisasi
proses ini akan membaut fitur data menjadi bentuk yang lebih mudah di diolah oleh model, data akan mengurangkan mean (nilai rata rata)  kemudian membaginya dengan standar deviasi untuk menggeser distribusi.

## Modeling

Tahap ini akan mengembangkan model machine learning dengan tiga algoritma lalu kemudian akan dievaluasi mengenai performa masing masing algoritma dan menentukan mana yang memberikan hasil prediksi terbaik. Tiga algoritma tersebut :
1. Knearest Negihbor (KNN) 
Kelebihan KNN adalah pelatihan sangat cepat, sederhana dan mudah dipelajari, tahan terhadap data pelatihan yang memiliki derau, dan efektif jika data pelatihan besar.
Kekurangan KNN adalah Nilai k bias, Komputasi kompleks, Keterbatasan memori, dan 4) Mudah tertipu dengan atribut yang tidak relevan.

2. Random Forest (RF)
Kelebihan RF adalah dapat mengatasi noise dan missing value serta dapat mengatasi data dalam jumlah yang besar
Kekurangan RF adalah interpretasi yang sulit dan membutuhkan tuning model yang tepat untuk data.

3. AdaBoosting Algoritma
Kelebihan AdaBoost adalah relatif lebih mudah untuk diimplementasikan dan waktu pengujian yang relatif cepat sehingga cocok dipakai dalam implementasi kondisi real time.

## Evaluation

Metrik yang digunakan untuk evaluasi model adalah MSE atau mean Squared Error dan R2score. MSE menghitung jumlah selisih kuadrat rata rata nilai sebenernya dengan prediksi dan R2score digunakan untuk menghitung nilai prediksi yang diperoleh setiap algoritma. Berdasarkan evaluasi model algoritma Knearest Negihbor (KNN) mendapatkan skor akurasi untuk memprediksi di -380% dan MSE nya pada data train sebesar 0,74787, data testnya 0,75894. Algoritma Random Forest mendapatkan skor untuk memprediksi di 99% dan MSE nya pada data train 0,000027, data test 0,000115. Algoritma Boosting mednapatkan skor akurasi untuk memprediksi di 98% dan mse data train 0,000161 data test 0,000166

	train	test
KNN	0.074787	0.075894
RF	0.000027	0.000115
Boosting	0.000161	0.000166
