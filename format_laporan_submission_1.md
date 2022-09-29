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
- Menangani Outlier dengan IQR method
<br>
IQR method adalah singkatan dari Inter Quartile Range yang dapat menangagi outlier dengan kuartil tiga (Q3) dikurang kuartil pertama (Q1). Untuk menunjukkan apakah data memiliki outlier maka kita akan menggunakan teknik visualisasi yaitu box plot. box plot menunjukkan ukuran lokasi dan penyebaran, serta memberikan informasi mengenai tentang simetri dan outliers. setelah dilakukan teknik visualisasi didapatkan bahwa beberapa fitur numerik memiki outlier. Untuk mengatasi outliers tersebut kita akan mengurangi batas atas dengan batas bawah. lalu batas bawah di dapatkan dari Q1 - 1.5 * IQR, sedangkan batas atas didapatkan dari Q3 + 1.5 * IQR.

- Encoding fitur categorical
<br>
data yang masih berbentuk kategori akan diubah menjadi data numerikal agar data dapat masuk ke pelatihan model. untuk melakukan proses encoding pada fitur categorical kita akan menggunakan teknik one hot encoding yang disediakan oleh library scikit-learn. dengan teknik ini data mendapatkan fitur baru yang sesuai sehingga dapat mewakili fitur-fitur categorical. disini kita memiliki beberapa fitur yang berbentuk categorical yaitu : Area Type','City','Furnishing Status','Bathroom','Tenant Preferred','Point of Contact', 'Area Locality. Proses encoding dilakukan dengan fungsi get_dummies.

- Split dataset dengan train_test_split
<br>
data akan dibagi menjadi data pelatihan dan data testing, data pelatihan akan dimasukan ke dalam pelatihan model lalu akan menghasilkan prediksi. untuk mengetes hasil prediksi itu digunakanlah data testing. untuk melakukan proses split dataset maka kita menggunakan library skicit-learn atau sklearn, disini kita akan menggunakan variabel X sebagai tempat menyimpan semua fitur yang ada pada dataset kecuali fitur Rent sedangkan variabel Y akan menggunakan fitur Rent. Pembagian porsi pada split dataset kali ini adalah 80% data latih 20% data test, dan parameter random state berisikan 123.

- Standarisasi
<br>
proses ini akan membaut fitur data menjadi bentuk yang lebih mudah di diolah oleh model, data akan mengurangkan mean (nilai rata rata)  kemudian membaginya dengan standar deviasi untuk menggeser distribusi. Standarisasi akan menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. sekitar 68% dari nilai akan berada diantara -1 dan 1. pada pembuatan model kali ini kita akan melakukan standarisasi dengan libary skicit-learn atau sklen dengan fungsi StandarScaler.

## Modeling

Tahap ini akan mengembangkan model machine learning dengan tiga algoritma lalu kemudian akan dievaluasi mengenai performa masing masing algoritma dan menentukan mana yang memberikan hasil prediksi terbaik. Tiga algoritma tersebut :
1. Knearest Negihbor (KNN)
<br>
KNN merupakan algoritma yang relatif sederhana dibandingkan algoritma lain. Dikarenakan algoritma ini  menggunakan kesamaan fitur untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titip tersebut dalam set pelatihan. KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tentangga ( dengan k adalah sebuah angka positif ). pada model ini akan menggunakan libary skicit learn atau sklearn dengan fungsi KNeighborsRegressor dengan parameter sejumlah k tetangga sebanyak 250 pada proses pelatihan, maka model akan mengunjungi tetangga atau sekitar sebanyak 250 kali. Hasil score prediksi yang didapat dari pelatihan model adalah -380%
Kelebihan KNN adalah pelatihan sangat cepat, sederhana dan mudah dipelajari, tahan terhadap data pelatihan yang memiliki derau, dan efektif jika data pelatihan besar.
Kekurangan KNN adalah Nilai k bias, Komputasi kompleks, Keterbatasan memori, dan 4) Mudah tertipu dengan atribut yang tidak relevan.

2. Random Forest (RF)
<br>
Random Forest merupakan salah satu algoritma supervised learning yang termasuk kedalam kategori ensemble (group). Ensemble adalah sekelompok model yang bekerja sama untuk menyelesaikan masalah. Random Forest memiliki cara kerja dengan mengkombinasikan dari masing-masing tree yang baik kemudian dikombinasikan ke dalam satu model. jadi Random Forest bergantung dengan sebuah nilai vector random dengan distribusi yang sama pada semua pohon yang masing masing decision tree memiliki kedalaman maksimal. pada model ini kita akan menggunakan skicit learn atau sklen dengan fungsi RandomForestRegressor disini kita akan menggunakan parameter n_estimator yang berarti jumlah pohon di forest, disini kita mengisi 50 yang berarti akan ada 50 jumlah pohon diforest. selanjutnya menggunakan parameter max_depth yang berarti kedalaman atau panjang pohon dsini akan mengisi dengan 16, yang bearti panjang pohon adalah 16. Parameter Random State digunakan untuk mengontrol random number generator. Dan parameter terakhir n_jobs yang berfungsi untuk mengontrol thread atau proses berjalan paralel, disini kita mengisi dengan 1 yang berarti semua proses akan berjalan paralel. Hasil score prediksi yang didapat dari pelatihan model adalah 99%
Kelebihan RF adalah dapat mengatasi noise dan missing value serta dapat mengatasi data dalam jumlah yang besar
Kekurangan RF adalah interpretasi yang sulit dan membutuhkan tuning model yang tepat untuk data.

3. AdaBoosting Algoritma
<br>
Boosting adalah algoritma yang bertujuan untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah sehingga membentuk suatu model yang kuat. Pada model ini akan menggunakan Adaptive Boost, Adaptive Boost bekerja dengan pada setiap tahapan semua data latih yang awalnya memiliki weight atau bobot yang sama, kemudian bobot yang lebih tinggi akan diberikan pada model yang salah sehingga mereka akan memasukkan ke dalam tahapan selanjutnya. pada model ini kita menggunakan library dari skicit-learn atau sklearn dengan fungsi AdaBoostRegressor dengan menggunakan parameter learning_rate sebanyak 0.05 yang berarti bobot yang diterapkan pada setiap regressor di masing masing proses diterasi sebesar 0.05. lalu menggunakan parameter random_state  sebanyak 55. Hasil score prediksi yang didapat dari pelatihan model adalah 98%
Kelebihan AdaBoost adalah relatif lebih mudah untuk diimplementasikan dan waktu pengujian yang relatif cepat sehingga cocok dipakai dalam implementasi kondisi real time.

## Evaluation

Metrik yang digunakan untuk evaluasi model adalah MSE atau mean Squared Error dan R2score. MSE menghitung jumlah selisih kuadrat rata rata nilai sebenernya dengan prediksi dan R2score digunakan untuk menghitung nilai prediksi yang diperoleh setiap algoritma. Berdasarkan evaluasi model algoritma Knearest Negihbor (KNN) mendapatkan skor akurasi untuk memprediksi di -380% dan MSE nya pada data train sebesar 0,74787, data testnya 0,75894. Algoritma Random Forest mendapatkan skor untuk memprediksi di 99% dan MSE nya pada data train 0,000027, data test 0,000115. Algoritma Boosting mendapatkan skor akurasi untuk memprediksi di 98% dan mse data train 0,000161 data test 0,000166. Maka dapat disimpulkan bahwa model yang akan digunakan untuk memprediksi adalah model dengan algoritma Random Forest dikarenkaan memiliki score prediksi paling tinggi.
