# Laporan Proyek Machine Learning - Adrian Juansyah Hasan

## Domain Proyek

Saat ini penyewaan apartemen atau rumah berkembang begitu pesat. hal ini dikarenakan dengan pertumbuhan pendduk yang sedemikian pesatnya, penyewaan apartemen atau rumah adalah salah satu usaha yang bergerak dibidang jasa yang dapat membantu para travelling atau perjalanan bisnis untuk mendapatkan kenyamanan dan keamanan dalam berpergian[1]. Selain itu tidak semua manusia mampu memenuhi kebutuhan papan dengan memliki rumah atau apartemen sendiri. keterbatasan pemenuhan kebutuhan primer itu disebabkan kondisi ekonomi yang semakin tinggi. oleh karena itu sewa rumah atau apartemen sebagai salah satu alternatif untuk orang yang belum memliki tempat tinggal. maka dari pemaparan diatas dibuat sebuah model predictive analysis house/apartement Rent yang bertujuan untuk memprediksi harga penyewaan apartemen atau rumah pada masa yang akan datang.


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

Data yang digunakan untuk membuat model ini adalah _House Rent Prediction Dataset_. _Dataset_ berisikan 4700+ rumah yang siap untuk disewakan. karakteristik pada dataset terdiri dari dua jenis fitur numerik dan fitur _non_ numerik. karakteristik numerik adalah BHK, Rent, Size, Bathroom. Karakteristik non numerik adalah Floor, Area Type, Area Locality, City, Furnishing Status. Fitur fitur inilah yang akan digunakan untuk menemukan pola pada data sedangkan rent merupakan fitur target. dataset ini bersumber [kaggle.com] https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset.

 
### Variabel-variabel pada _House Rent Prediction Dataset_ adalah sebagai berikut:
- BHK : Berisikan banyaknya jumlah Bedrooms, Hall, Kitchen
- Rent : Berisikan harga sewa rumah atau apartemen
- Size : Berisikan luas dari rumah atau apartemen
- Floor : Berisikan jumlah keseluruhan lantai pada rumah atau apartemen
- Area Type : Berisikan tipe ukuran dari rumah atau apartemen
- Area Locality : Berisikan lokalitas dari rumah atau apartemen
- City : Berisikan wilayah kota pada rumah atau apartemen
- Furnishing Status : Berisikan status perlengkapan rumah pada rumah atau apartemen
- Bathroom : Berisikan banyaknnya kamar mandi pada rumah atau apartemen

### Memvisualisasikan Variabel variabel pada _House Rent Prediction_
Disini kita akan memvisualisasikan fitur kategori 
- Area Type
<br> pada fitur type terdapat 3 kategori dalam Area Type yaitu super area, carpet area dan built area. kategori Super Area memiliki sampel sebanyak 2352 atau dengan presentase 53%. lalu kategori Carpet Area memiliki sampel sebanyak 2052 atau dengan presentase 46% dan kategori terakhir Built Area memiliki sampel sebanyak 2 atau dengan presentase 0,1%. Dapat disimpulkan bahwa berdasarkan data type area pada rumah atau apartemen pada dataset yang terbanyak adalah kategori Super Area dengan sampel sebanyak 2352 atau presentase 53%.
<br>![image](https://user-images.githubusercontent.com/79002078/193218789-6f992671-a070-4ba4-88fc-7349c447f1f8.png)

- Area Locality
<br> 3 Data terbanyak pada Area Locality adalah Bandra West dengan jumlah sampel sebanyak 27 atau dengan presentase 0.6%, Electronic City dengan jumlah sampel sebanyak 24 atau dengan presentase 0.5% dan Gachibowli dengan jumlah sampel sebanyak 23 atau dengan presentase 0.5%.
<br>![image](https://user-images.githubusercontent.com/79002078/193267811-d089a4c0-ae49-409f-9c4f-6fb4e8814dc8.png)

- City
<br> pada fitur city terdapat 6 kategori pada City yaitu Bangalore, chennai, Mumbai, Hyderabad, Delhi dan Kolkata. Kategori Bangalore memiliki jumlah sampel sebanyak 850 atau dengan presentase 19.3%, Kategori Chenai memiliki jumlah sampel sebanyak 844 atau dengan presentase 19.2%, Kategori Mumbai memiliki jumlah sampel sebanyak 833 atau dengan presentase 18.9%, Kategori Hyderabad memiliki jumlah sampel 804 atau dengan presentase 18.2, kategori Delhi memiliki jumlah sampel sebanyak 559 atau dengan presentase 12.7% dan kateogri yang terakhir kolkata memliki jumlah sampel sebanyak 516 atau dengan presentase 11.7 
<br> ![image](https://user-images.githubusercontent.com/79002078/193268499-90098b3e-fb67-4d2d-84af-3faf345a3b2d.png)

- Furnishing Status
<br> Pada fitur _Furnishing Status_ terdapat 3 kategori yaitu _Semi-Furnished_, _Unfurnished_ dan _Furnished_. Semi-Furnished berarti rumah atau apartemen tersebut sudah dilengkapi dengan beberapa furnitur, sedangkan _unfurnished_ memiliki arti rumah atau apartemen tidak memiliki funitur dan _furnished_ memiliki arti bahwa rumah atau apartemen lengkap dengan furnitur. Kategori _Semi-Furnished_ memiliki jumlah sampel sebanyak 2056 atau dengan presentase 46.7%. lalu kategori _unfurnished_ memiliki jumlah sampel sebanyak 1749 atau dengan presentase 39.7% dan kategori Furnished memiliki jumlah sampel sebanyak 601 atau dengan presentase 13.6%.
<br> ![image](https://user-images.githubusercontent.com/79002078/193272664-010d67bb-d3bf-4650-ad44-9ceabeafe017.png)

- Tenant Preffered
<br> Pada fitur _Tenant Preffered_ terdapat 3 kategori yaitu _Bachelor/Family_, _Bachelor_ dan _Family_._ Bachelor_ memiliki arti bahwa rumah atau apartemen ini ditujukan untuk bujangan atau yang hidup sendiri, sedangkan _Family_ memiliki arti bahwa rumah atau apartemen ditujukan untuk yang sudah berkeluarga dan _bachelor/family_ ditujukan untuk yang hidup sendiri atau yang sudah berkeluarga. Pada kategori _Bachelor/Family_ memiliki jumlah sampel sebanyak 3235 atau dengan presentase 73.4%, lalu untuk kategori _Bachelor_ memiliki jumlah sampel sebanyak 755 atau dengan presentase 17.1% dan kategori yang terakhir _Family_  memiliki jumlah sampel sebanyak 416 atau dengan presentase 9.4%.
<br>![image](https://user-images.githubusercontent.com/79002078/193279991-4b768783-8c67-489f-9600-0b4b2ba68caf.png)


Selanjutnya akan memvisualisasikan Fitur Numerikal
<br> Seperti yang terlihat fitur numerikal terdiri dari BHK, Rent, Size, dan Bathroom. Fitur Rent akan menjadi target pada label data kita.
<br>![image](https://user-images.githubusercontent.com/79002078/193280176-b3fd995e-4337-46c7-8fbc-88ff08bd37e2.png)

## Mengubah Format Fitur
Pada Fitur Post on format berisikan sebuah bertipe data _date-time_ atau bertipe tanggal bulan tahun, tipe data seperti ini membuat model susah membaca data tersebut. Maka dari itu kita akan memisah dan membuat masing masing kolom baru dengan nama 'DAY', 'MONTH', 'YEAR'.
<br>
<br> **BEFORE**
|  Posted On |        
|-----------:|
| 2022-05-18 |
| 2022-05-13 |
| 2022-05-16 |
| 2022-07-04 |
| 2022-05-09 |
|        ... | 
| 2022-05-18 |
| 2022-05-15 |
| 2022-07-10 |
| 2022-07-06 |
| 2022-05-04 |

<br> **AFTER**
| Day | Month | Year |
|----:|------:|-----:|
|  18 |     5 | 2022 |
|  13 |     5 | 2022 |
|  16 |     5 | 2022 |
|   4 |     7 | 2022 |
|   9 |     5 | 2022 |
| ... |   ... |  ... |
|  18 |     5 | 2022 |
|  15 |     5 | 2022 |
|  10 |     7 | 2022 |
|   6 |     7 | 2022 |
|   4 |     5 | 2022 |

Selain fitur Post On, kita juga akan memisahkan Fitur Floor dimana fitur floor masih berisikan value bertipe data string. maka dari itu kita akan mengubah format fitur ini dari string menjadi integer dengan kolom baru bernama 'Living Floor' dan 'Total Floor'.
<br>
<br> **BEFORE**
|           Floor |
|----------------:|
| Ground out of 2 |
|      1 out of 3 |
|      1 out of 3 |
|      1 out of 2 |
|      1 out of 2 |
|             ... |
|      3 out of 5 |
|      1 out of 4 |
|      3 out of 5 |
|    23 out of 34 |
|      4 out of 5 |

**AFTER**
<br>
| Living Floor | Total Floor |
|-------------:|------------:|
|            0 |           0 |
|            1 |           3 |
|            1 |           3 |
|            1 |           2 |
|            1 |           2 |
|          ... |         ... |
|            3 |           5 |
|            1 |           4 |
|            3 |           5 |
|           23 |          34 |
|            4 |           5 |

## Visualisasi Correlation Matrix untuk Fitur Numerik
Koeefisien mengukur kekuatan antara hubungan dua variabel serta arahnya (positif atau negatif). mengenai kekuatan hubungan antar variabel, semakin dekat nilanya ke 1 atau -1, korelasinya semakin kuat. sedangkan, semakin dekat nilainya ke 0 korelasinya semakin rendah. pada grafik korelasi dibawah fitur 'year', 'month','BHK','Bathroom' memiliki skor korelasi yang tinggi dengan fitur rent, artinya fitur rent berkorelasi tinggi dengan keempat fitur tersebut.
<br>![image](https://user-images.githubusercontent.com/79002078/193302560-cb8925b7-c67b-4b6d-b947-0f24c02aae6d.png)

## Visualisasi Data untuk Mendeteksi Outlier
- Size
<br> Pada fitur Size terdapat Outlier
<br>  ![image](https://user-images.githubusercontent.com/79002078/193307196-d0876ba7-5cca-4d85-8bdd-117ac249f662.png)

- Rent
<br> Pada Fitur Rent Terdapat Outlier
<br> ![image](https://user-images.githubusercontent.com/79002078/193307356-b7c754b6-2f26-4b33-b4f6-74da627c427c.png)

- BHK
<br> Pada Fitur BHK Terdapat Outlier
<br> ![image](https://user-images.githubusercontent.com/79002078/193307962-2056738e-cbc5-440e-b2e8-a5e239da4a25.png)



## Data Preparation
Teknik data preparation yang digunakan pada pembuatan model ini adalah : 
- Menangani Outlier dengan IQR method
<br> IQR method adalah singkatan dari _Inter Quartile Range_ yang dapat menangagi outlier dengan kuartil tiga (Q3) dikurang kuartil pertama (Q1). Untuk menunjukkan apakah data memiliki _outlier_ maka kita akan menggunakan teknik visualisasi yaitu box plot. box plot menunjukkan ukuran lokasi dan penyebaran, serta memberikan informasi mengenai tentang simetri dan _outliers_. setelah dilakukan teknik visualisasi didapatkan bahwa beberapa fitur numerik memiliki _outlier_. Untuk mengatasi outliers tersebut kita akan mengurangi batas atas dengan batas bawah. lalu batas bawah di dapatkan dari Q1 - 1.5 * IQR, sedangkan batas atas didapatkan dari Q3 + 1.5 * IQR.

- Encoding fitur categorical
<br> Data yang masih berbentuk kategori akan diubah menjadi data numerikal agar data dapat masuk ke pelatihan model. untuk melakukan proses encoding pada fitur _categorical_ kita akan menggunakan teknik _one hot encoding_ yang disediakan oleh _library scikit-learn_. dengan teknik ini data mendapatkan fitur baru yang sesuai sehingga dapat mewakili fitur-fitur _categorical_. disini kita memiliki beberapa fitur yang berbentuk _categorical_ yaitu : Area Type','City','Furnishing Status','Bathroom','Tenant Preferred','Point of Contact', 'Area Locality. Proses encoding dilakukan dengan fungsi get_dummies.

- Split dataset dengan train_test_split
<br> Data akan dibagi menjadi data pelatihan dan data testing, data pelatihan akan dimasukan ke dalam pelatihan model lalu akan menghasilkan prediksi. untuk mengetes hasil prediksi itu digunakanlah data _testing_. untuk melakukan proses _split dataset_ maka kita menggunakan _library skicit-learn_ atau _sklearn_, disini kita akan menggunakan _variabel_ X sebagai tempat menyimpan semua fitur yang ada pada _dataset_ kecuali fitur Rent sedangkan _variabel_ Y akan menggunakan fitur Rent. Pembagian porsi pada split _dataset_ kali ini adalah 80% data latih 20% data test, dan parameter random state berisikan 123.

- Standarisasi
<br> Proses ini akan membuat fitur data menjadi bentuk yang lebih mudah di diolah oleh model, data akan mengurangkan _mean_ (nilai rata rata)  kemudian membaginya dengan standar _deviasi_ untuk menggeser distribusi. Standarisasi akan menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. sekitar 68% dari nilai akan berada diantara -1 dan 1. pada pembuatan model kali ini kita akan melakukan standarisasi dengan _libary skicit-learn_ atau sklearn dengan fungsi _StandarScaler_.

## Modeling

Tahap ini akan mengembangkan model machine learning dengan tiga algoritma lalu kemudian akan dievaluasi mengenai performa masing masing algoritma dan menentukan mana yang memberikan hasil prediksi terbaik. Tiga algoritma tersebut :
1. Knearest Negihbor (KNN)
<br> KNN merupakan algoritma yang relatif sederhana dibandingkan algoritma lain. Dikarenakan algoritma ini  menggunakan kesamaan fitur untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titip tersebut dalam set pelatihan. KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tentangga ( dengan k adalah sebuah angka positif ). pada model ini akan menggunakan _libary skicit learn_ atau sklearn dengan fungsi KNeighborsRegressor dengan parameter sejumlah k tetangga sebanyak 250 pada proses pelatihan, maka model akan mengunjungi tetangga atau sekitar sebanyak 250 kali. Hasil score prediksi yang didapat dari pelatihan model adalah -380%
Kelebihan KNN adalah pelatihan sangat cepat, sederhana dan mudah dipelajari, tahan terhadap data pelatihan yang memiliki derau, dan efektif jika data pelatihan besar.
Kekurangan KNN adalah Nilai k bias, Komputasi kompleks, Keterbatasan memori, dan 4) Mudah tertipu dengan atribut yang tidak relevan.

2. Random Forest (RF)
<br> _Random Forest_ merupakan salah satu algoritma supervised learning yang termasuk kedalam kategori _ensemble_ (group). _Ensemble_ adalah sekelompok model yang bekerja sama untuk menyelesaikan masalah. _Random Forest_ memiliki cara kerja dengan mengkombinasikan dari masing-masing tree yang baik kemudian dikombinasikan ke dalam satu model. jadi Random Forest bergantung dengan sebuah nilai vector random dengan distribusi yang sama pada semua pohon yang masing masing _decision tree_ memiliki kedalaman maksimal. pada model ini kita akan menggunakan skicit learn atau sklen dengan fungsi RandomForestRegressor disini kita akan menggunakan parameter _n_estimator_ yang berarti jumlah pohon di _forest_, disini kita mengisi 50 yang berarti akan ada 50 jumlah pohon diforest. selanjutnya menggunakan _parameter_ _max_depth_ yang berarti kedalaman atau panjang pohon dsini akan mengisi dengan 16, yang bearti panjang pohon adalah 16. Parameter Random State digunakan untuk mengontrol _random number generator_. Dan parameter terakhir_ n_jobs_ yang berfungsi untuk mengontrol thread atau proses berjalan paralel, disini kita mengisi dengan 1 yang berarti semua proses akan berjalan paralel. Hasil score prediksi yang didapat dari pelatihan model adalah 99%
Kelebihan RF adalah dapat mengatasi noise dan missing value serta dapat mengatasi data dalam jumlah yang besar
Kekurangan RF adalah interpretasi yang sulit dan membutuhkan tuning model yang tepat untuk data.

3. AdaBoosting Algoritma
<br> _Boosting_ adalah algoritma yang bertujuan untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah sehingga membentuk suatu model yang kuat. Pada model ini akan menggunakan _Adaptive Boost_, _Adaptive Boost_ bekerja dengan pada setiap tahapan semua data latih yang awalnya memiliki weight atau bobot yang sama, kemudian bobot yang lebih tinggi akan diberikan pada model yang salah sehingga mereka akan memasukkan ke dalam tahapan selanjutnya. pada model ini kita menggunakan _library dari skicit-learn_ atau _sklearn_ dengan fungsi _AdaBoostRegressor_ dengan menggunakan parameter _learning_rate_ sebanyak 0.05 yang berarti bobot yang diterapkan pada setiap _regressor_ di masing masing proses diterasi sebesar 0.05. lalu menggunakan parameter random_state  sebanyak 55. Hasil score prediksi yang didapat dari pelatihan model adalah 98%
Kelebihan AdaBoost adalah relatif lebih mudah untuk diimplementasikan dan waktu pengujian yang relatif cepat sehingga cocok dipakai dalam implementasi kondisi real time.

## Evaluation

Metrik yang digunakan untuk evaluasi model adalah MSE atau _mean Squared Error_ dan R2score. MSE menghitung jumlah selisih kuadrat rata rata nilai sebenernya dengan prediksi dan R2score digunakan untuk menghitung nilai prediksi yang diperoleh setiap algoritma. Berdasarkan evaluasi model algoritma Knearest Negihbor (KNN) mendapatkan skor akurasi untuk memprediksi di -380% dan MSE nya pada data train sebesar 0,74787, data testnya 0,75894. Algoritma Random Forest mendapatkan skor untuk memprediksi di 99% dan MSE nya pada data train 0,000027, data test 0,000115. Algoritma Boosting mendapatkan skor akurasi untuk memprediksi di 98% dan mse data train 0,000161 data test 0,000166. Maka dapat disimpulkan bahwa model yang akan digunakan untuk memprediksi adalah model dengan algoritma _Random Forest_ dikarenkaan memiliki score prediksi paling tinggi.

** Hasil Evaluasi dengan MSE**

|          |   Train  |    Test  |
|---------:|:--------:|:--------:|
|    KNN   | 0.074787 | 0.075894 |
|    RF    | 0.000027 | 0.000115 |
| Boosting | 0.000161 | 0.000166 |


## Daftar Pustaka
[1] Pitaloka, D. A., & Fauziah, S. (2019, February 2). SISTEM INFORMASI PENYEWAAN APARTEMEN U-RESIDENCE PADA PT. GRAHA KELOLA MANDIRI TANGERANG. JURNAL ILMU PENGETAHUAN DAN TEKNOLOGI KOMPUTER, 4(2).
