# Laporan Proyek Machine Learning - Adrian Juansyah Hasan

## Project Overview

Buku merupakan jendela dunia. Dengan membaca buku kita dapat memperoleh banyak ilmu. Salah satu manfaat buku adalah menunjang proses belajar mengajar, baik itu disekolah maupun diperguruan tinggi, Memperluas wawasan dan dapat membuat individu meningkatkan kecerdasan. dan sebaliknya semakin jarang membaca, pengetahuan individu semakin terbatas[1]. jadi membaca merupakan salah satu pintu utama untuk mendapatkan informasi dan pengetahuan. Banyaknya jumlah buku dapat membuat pembaca terkadang kesulitan dalam menentukan buku yang hendak mereka baca selanjutnya[2]. Terkadang ada pembaca yang hanya ingin membaca buku-buku yang memiliki reputasi penjualan terbaik atau bukuk yang populer. Ada juga pembaca yang ingin membaca buku yang mirip dengan buku-buku yang pernah dibaca sebelumnya. Berdasarkan penjelasan diatas maka akan dibuat model sistem rekomendasi menggunakan metode _item-based collaborative filtering_ yang diharapkan dapat membantu pembaca untuk menentukan buku untuk dibaca selanjutnya[3].

## Business Understanding

Dikarenakan banyaknya jumlah buku membuat banyak pembaca kebingungan dalam menentukan buku yang akan dibaca selanjutnya. Maka dari itu diperlukan membuat sistem rekomendasi yang diharapkan dapat membantu para pembaca.

### Problem Statements

Menjelaskan pernyataan masalah:
- Berdasarkan data mengenai buku, bagaimana membuat sistem rekomendasi dengan menggunakan _Collaborative-Filtering_ metode _item-based-filtering_?
- Dengan data rating yang dimiliki, bagaimana perusahaan dapat merekomendasikan sebuah buku lain yang mungkin disukai dan belum pernah dibaca oleh para pembaca?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Menghasilkan sejumlah rekomendasi buku yang diperuntukan para pembaca dengan teknik _Collaborative Filtering _
- Menghasilkan sejumlah rekomendasi buku berdasarkan kepopulerannya

### Solution Approach
- Menggunakan dua algoritma untuk melihat perbedaan dari algoritma tersebut dalam merekomendasikan buku. Pada pembuatan model ini menggunakan algoritma dimana merekomendasikan berdasarkan kepopulearnnya dan menggunakan Cosine Similarity dimana kita menghitung derajat kesamaan antara buku dan user.


## Data Understanding
Dataset yang kita gunakan kali ini adalah Book Recommendation Dataset. Dataset ini berisikan 242135+ judul buku yang siap dibaca. Dataset berisikan 3 file yaitu books.csv, rating.csv, dan users.csv. book.csv berisikan informasi mengenai buku, didalam file ini terdapat beberapa kolom atau fitur seperti ISBN, Book-Title, Book-Author, Year-Of-Publication, Publisher, Image-URL-S, Image-URL-M, Image-URL-L. Lalu pada file rating.csv berisikan informasi mengenai rating yang diberikan oleh pembaca, pada file ini terdapat beberapa kolom atau fitur seperti User-ID, ISBN, Book-Rating. Dan pada file terakhir users.csv berisikan informasi mengenai para pembaca, pada file ini terdapat bebreapa kolom atau fitur seperti User-ID, Location, Age. Dataset ini bersumber pada [kaggle.com] (https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset?select=Users.csv)


## Variabel-variabel pada Book Recommendation dataset adalah sebagai berikut:
- ISBN : Berisikan mengenai kode pengidentifikasian buku yang bersifat unik, didalam kode ini terdapat informasi seperti Informasi tentang judul, penerbit, dan kelompok penerbit.
- Book-Tile : Berisikan mengenai nama-nama judul buku
- Book-Author : Berisikan mengenai nama-nama penulis buku
- Year-Of-Publication : Berisikan mengenai tahun penerbitan buku
- Publisher : Berisikan kumpulan nama-nama publisher buku
- Image-URL-S : Berisikan mengenai cover buku berukuran kecil
- Image-URL-M : Berisikan mengenai cover buku berukuran sedang
- Image-URL-L : Berisikan mengenai cover buku berukuran besar
- User-ID : Berisikan mengenai nomor identitas yang dimiliki oleh setiap pembaca
- Book-Rating : Berisikan mengenai kumpulan penilaian buku yang berikan oleh para pembaca
- Location : Berisikan mengenai lokasi para pembaca
- Age : Berisikan mengenai umur para pembaca

## Exploratory data analysis pada Dataset
Disini kita akan melakukan ekplorasi pada file atau variabel pada dataset

### Variabel Books
Explorasi variabel books yang berisikan informasi mengenai buku, dengan mengecek informasi didalamnya dengan fungsi .info()
|   # | Column            | Non-Null Count  | Dtype  |
|----:|-------------------|-----------------|--------|
| --- | ------            | --------------  | -----  |
|   0 | ISBN              | 271360 non-null | object |
|   1 | BookTitle         | 271360 non-null | object |
|   2 | BookAuthor        | 271359 non-null | object |
|   3 | YearOfPublication | 271360 non-null | object |
|   4 | Publisher         | 271358 non-null | object |
|   5 | ImageURLS         | 271360 non-null | object |
|   6 | ImageURLM         | 271360 non-null | object |
|   7 | ImageURLL         | 271357 non-null | object |

Berdasarkan output diatas, kita dapat mengetahui bahwa file books.csv berisikan range entri 27160. Pada file ini terdapat 8 fitur, yaitu ISBN, BookTitle, BookAuthor, YearOfPublication, Publisher, ImageURLS, ImageURLM, ImageURLL. Pada fitur ISBN meliki entri 271360 dengan type data object, fitur BookTitle memiliki entri 271360 dengan type data object, fitur BookAuthor memiliki entri 271360 dengan type data object, fitur YearOfPublication memiliki entri 271360 dengan type data object, fitur publisher memiliki entri 271358 dengan type data object, fitur ImageURLS memiliki entri 271360 dengan type data object, fitur ImageURLM memiliki entri 271360 dengan type data object, fitur ImageURLL memiliki entri 271357 dengan type data object.

### Variabel Ratings
Explorasi variabel Ratings yang berisikan informasi mengenai penilaian pada buku dari para pembaca, dengan mengecek informasi didalamnya dengan fungsi .info()
| # | Column     | Non-Null Count   | Dtype  |
|:-:|------------|------------------|--------|
| 0 |   UserID   | 1149780 non-null | int64  |
| 1 |    ISBN    | 1149780 non-null | object |
| 2 | BookRating | 1149780 non-null | int64  |

Berdasarkan output diatas, kita dapat mengetahui bahwa file ratings.csv berisikan range entri 1149780. Pada file ini berisikan 3 fitur yaitu UserID, ISBN, BookRating. Fitur UserID memiliki entri 1149780 dengan type data integer, fitur ISBN memiliki entri 1149780 dengan type data object, pada fitur BookRating memiliki entri 1149780 dengan type data integer.

### Variabel Users
Explorasi variabel Users yang berisikan informasi mengenai para pembaca, dengan mengecek informasi didalamnya dengan fungsi .info()
| # |  Column  |  Non-Null Count |  Dtype  |
|:-:|:--------:|:---------------:|:-------:|
| 0 |  UserID  | 278858 non-null |  int64  |
| 1 | Location | 278858 non-null |  object |
| 2 |    Age   | 168096 non-null | float64 |

Berdasarkan output diatas, kita dapat mengetahui bahwa file Users.csv berisikan range entri 278858. pada file ini berisikan 3 fitur yaitu UserID, Location dan Age. Pada fitur UserID memiliki entri 278858 dengan type data integer, fitur Location memiliki entri 278858 dengan type data object, fitur age memiliki entri 168096 dengan type data float64.

### Mengecek Nilai Unik
Explorasi pengecekan nilai unik pada fitur BooTitle, BookAuthor, Publisher, UserID pada file Ratings.csv, UserID pada File Users.csv. Dengan menggunakan fungsi .unique()

|              Pengecekan Nilai Unik             |        |
|:----------------------------------------------:|--------|
|           Jumlah data banyaknya Buku:          | 242135 |
|       Jumlah data banyaknya penulis buku:      | 102024 |
|     Jumlah data banyaknya Publishers buku:     |  16808 |
| Jumlah data Penilaian yang diberikan pengguna: | 105283 |
|          Jumlah data profil pengguna:          | 278858 |

Pada output diatas kita dapat melihat bahwa jumlah data banyaknya buku terdapat 242135, jumlah data banyaknya penulis terdapat 102024, jumlah data banyaknya publisher buku 16808, jumlah data penilaian yang diberikan pengguna terdapat 105283, jumlah data profil penggun terdapat 278858.

### Melakukan Penggabungan pada file
Melakukan penggabungan pada file ratings dengan file books berdasarkan fitur ISBN dengan fungsi .merge(). Lalu hasil penggabungan tersebut akan simpan dalam variabel book_info.
|  UserID |   ISBN |  BookRating | BookTitle |                                        BookAuthor | YearOfPublication | Publisher |                  ImageURLS |                                         ImageURLM |                                         ImageURLL |                                                   |
|--------:|-------:|------------:|----------:|--------------------------------------------------:|------------------:|----------:|---------------------------:|--------------------------------------------------:|--------------------------------------------------:|---------------------------------------------------|
|    0    | 276725 |  034545104X |         0 |                              Flesh Tones: A Novel |        M. J. Rose |      2002 |           Ballantine Books | http://images.amazon.com/images/P/034545104X.0... | http://images.amazon.com/images/P/034545104X.0... | http://images.amazon.com/images/P/034545104X.0... |
|    1    | 276726 |  0155061224 |         5 |                                  Rites of Passage |        Judith Rae |      2001 |                     Heinle | http://images.amazon.com/images/P/0155061224.0... | http://images.amazon.com/images/P/0155061224.0... | http://images.amazon.com/images/P/0155061224.0... |
|    2    | 276727 |  0446520802 |         0 |                                      The Notebook |   Nicholas Sparks |      1996 |               Warner Books | http://images.amazon.com/images/P/0446520802.0... | http://images.amazon.com/images/P/0446520802.0... | http://images.amazon.com/images/P/0446520802.0... |
|    3    | 276729 |  052165615X |         3 |                                    Help!: Level 1 |     Philip Prowse |      1999 | Cambridge University Press | http://images.amazon.com/images/P/052165615X.0... | http://images.amazon.com/images/P/052165615X.0... | http://images.amazon.com/images/P/052165615X.0... |
|    4    | 276729 |  0521795028 |         6 | The Amsterdam Connection : Level 4 (Cambridge ... |       Sue Leather |      2001 | Cambridge University Press | http://images.amazon.com/images/P/0521795028.0... | http://images.amazon.com/images/P/0521795028.0... | http://images.amazon.com/images/P/0521795028.0... |
|   ...   |    ... |         ... |       ... |                                               ... |               ... |       ... |                        ... |                                               ... |                                               ... |                                               ... |
| 1149775 | 276704 |  1563526298 |         9 | Get Clark Smart : The Ultimate Guide for the S... |      Clark Howard |      2000 |           Longstreet Press | http://images.amazon.com/images/P/1563526298.0... | http://images.amazon.com/images/P/1563526298.0... | http://images.amazon.com/images/P/1563526298.0... |
| 1149776 | 276706 |  0679447156 |         0 | Eight Weeks to Optimum Health: A Proven Progra... |       Andrew Weil |      1997 |            Alfred A. Knopf | http://images.amazon.com/images/P/0679447156.0... | http://images.amazon.com/images/P/0679447156.0... | http://images.amazon.com/images/P/0679447156.0... |
| 1149777 | 276709 |  0515107662 |        10 |  The Sherbrooke Bride (Bride Trilogy (Paperback)) | Catherine Coulter |      1996 |                 Jove Books | http://images.amazon.com/images/P/0515107662.0... | http://images.amazon.com/images/P/0515107662.0... | http://images.amazon.com/images/P/0515107662.0... |
| 1149778 | 276721 |  0590442449 |        10 |                                 Fourth Grade Rats |    Jerry Spinelli |      1996 |                 Scholastic | http://images.amazon.com/images/P/0590442449.0... | http://images.amazon.com/images/P/0590442449.0... | http://images.amazon.com/images/P/0590442449.0... |
| 1149779 | 276723 | 05162443314 |         8 |                                               NaN |               NaN |       NaN |                        NaN |                                               NaN |                                               NaN |                                               NaN |

Pada output dapat kita lihat bahwa fitur ratings telah masuk kedalam file books.csv. Lalu masih terdapat missing value pada hasil penggabungan tersebut, maka masalah ini harus diatasi.

## Data Preparation
Teknik Preparation yang digunakan pada pembuatan model ini :
### Mengatasi Missing Value
Pada kali ini kita akan mengatasi missing value pada variabel book_info untuk melakukan pengecekan kita dapat melakukan dengan menggunakan fungsi .isnull().sum()
| Pengecekan Missing Value |        |
|:------------------------:|--------|
|          UserID          |    0   |
|           ISBN           |    0   |
|        BookRating        |    0   |
|         BookTitle        | 118644 |
|        BookAuthor        | 118645 |
|     YearOfPublication    | 118644 |
|         Publisher        | 118646 |
|         ImageURLS        | 118644 |
|         ImageURLM        | 118644 |
|         ImageURLL        | 118648 |

Pada output dapat kita lihat bahwa beberapa fitur masih terdapat missing value. Fitur BookTitle memiliki missing value sebanyak 118644, Fitur BookAuthor memiliki missing value sebanyak 118645, fitur YearOfPublication memiliki missing value sebanyak 118644, fitur Publisher memiliki missing value sebanyak 118646, fitur ImageURLS memiliki missing value sebanyak 118644, fitur ImageURLM memiliki missing value sebanyak 118644, fitur ImageURLL memiliki missing value sebanyak 118648.
<br>
Missing value dapat kita atasi dengan menggunakan fungsi .dropna(). Fungsi dropna memiliki cara kerja dengan akan menghapus baris atau kolom yang mengandung missing value.
| Pengecekan Missing Value |   |
|--------------------------|---|
|          UserID          | 0 |
|           ISBN           | 0 |
|        BookRating        | 0 |
|         BookTitle        | 0 |
|        BookAuthor        | 0 |
|     YearOfPublication    | 0 |
|         Publisher        | 0 |
|         ImageURLS        | 0 |
|         ImageURLM        | 0 |
|         ImageURLL        | 0 |

Dapat kita lihat pada output bahwa missing value pada beberapa fitur telah teratasi.

### Menghilangkan values 0
Pada fitur YearOfPublication terdapat value tersebut adalah 0, maka dari itu masalah ini harus diatasi.
|         | UserID |       ISBN | BookRating |                                         BookTitle |                    BookAuthor | YearOfPublication |                Publisher |
|--------:|-------:|-----------:|-----------:|--------------------------------------------------:|------------------------------:|------------------:|-------------------------:|
|  703628 | 171118 | 0000913154 |          8 | The Way Things Work: An Illustrated Encycloped... | C. van Amerongen (translator) |              1967 |     Simon &amp; Schuster |
|  866078 | 209516 | 0001010565 |          0 |                                   Mog's Christmas |                   Judith Kerr |              1992 |                  Collins |
|  357256 |  86123 | 0001010565 |          0 |                                   Mog's Christmas |                   Judith Kerr |              1992 |                  Collins |
|  103677 |  23902 | 0001046438 |          9 |                                              Liar |                   Stephen Fry |                 0 |         Harpercollins Uk |
|  807953 | 196149 | 0001046713 |          0 |                      Twopence to Cross the Mersey |               Helen Forrester |              1992 | HarperCollins Publishers |
|   ...   |    ... |        ... |        ... |                                               ... |                           ... |               ... |                      ... |
| 1100731 | 264317 | B000234N76 |          0 |                                    Falling Angels |               Tracy Chevalier |              2001 |               E P Dutton |
|  423108 | 100906 | B000234NC6 |          0 | It Must've Been Something I Ate: The Return of... |           Jeffrey Steingarten |              2002 |                    Knopf |
|  419279 | 100088 | B00029DGGO |          0 |                       Good Wife Strikes Back, The |              Elizabeth Buchan |                 0 |             Viking Adult |
|  743545 | 179791 | B0002JV9PY |          0 |                              The Blockade Runners |                   Jules Verne |                 0 |            Digireads.com |
|  743546 | 179791 | B0002K6K8O |          0 |                              The Underground City |                   Jules Verne |                 0 |            Digireads.com |


Melakukan pengecekan berapa banyak nilai 0 pada fitur YearOfPublication
|              Pengecekan Nilai 0              |
|:--------------------------------------------:|
| Nilai 0 di kolom YearOfPublication ada 12744 |

Disini kita berdasarkan output maka kita dapat melihat bahwa nilai 0 pada kolom atau fitur YearOfPublication ada 12744. hal ini dapat diatasi dengan menggunakan operator tidak sama dengan atau !=. Cara kerja operator tersebut kita akan memanggil data fitur YearOfPublication yang tidak memiliki nilai 0.

|            Pengecekan Nilai 0            |
|:----------------------------------------:|
| Nilai 0 di kolom YearOfPublication ada 0 |

Dapat kita lihat pada output bahwa nilai 0 pada kolom atau fitur YearOfPublication sudah teratasi.

### TF-IDF Vectorizer
TF-IDF Vectorizer memiliki fungsi untuk menemukan representasi fitur penting dari buku, disini menggunakan TfidfVectorizer dari library sklearn. pada awal kita akan melakukan perhitungan pada fitur target yaitu fitur Author, lalu setelah itu kita akan melakukan fit lalu ditransformasikan ke bentuk matrix. Vector Tf-idf tersebut akan diubah menjadi matrix dengan fungsi .todense(). lalu kita akan menampilkan tf-Idf_matrix untuk melihat korelasi antara buku dan authornya.
#### Menampikan TF-Idf_Matrix.

|                                                      | krentz | lichtenstein | dumaine | horn | lasky | brewers | raleigh | devito | wangerin | renee | ... | golenbock |  al | milgram | weinman | heim | sisson | johnston | motter | deirdrie | lenkert |
|-----------------------------------------------------:|-------:|-------------:|--------:|-----:|------:|--------:|--------:|-------:|---------:|------:|----:|----------:|----:|--------:|--------:|-----:|-------:|---------:|-------:|---------:|--------:|
|                       BookTitle                      |        |              |         |      |       |         |         |        |          |       |     |           |     |         |         |      |        |          |        |          |         |
|              Mara and Dann: An Adventure             |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|         Handbook for Boys : A Novel (Amistad)        |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
| The Complete Idiot's Guide to Football (2nd Edition) |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|  Zolar's Compendium of Occult Theories and Practices |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|                      Shabby Chic                     |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|      Britney Spears: The Unauthorized Biography      |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|                   The Phantom Major                  |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|         Love on the Dole (Modern Classics S.)        |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|                  Pooh's Workout Book                 |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |
|                   Inimitable Jeeves                  |    0.0 |          0.0 |     0.0 |  0.0 |   0.0 |     0.0 |     0.0 |    0.0 |      0.0 |   0.0 | ... |       0.0 | 0.0 |     0.0 |     0.0 |  0.0 |    0.0 |      0.0 |    0.0 |      0.0 |     0.0 |


## Modeling

Tahap ini kita membuat model dengan menggunakan Collaborative-Filtering dengan metode item-based-filtering dan User-based-filtering. Disini kita membuat model dengan sistem rekomendasi berdasarkan kepopuleran dan sistem rekomendasi menggunakan cosine similarity.
<br>
- Sistem Rekomendasi berdasarkan kepopuleran 
<br>
pada sistem rekomendasi ini kita melakukan pemanggilan data pada BookRating, dimana kita melakukan pengelompokkan data dan pengurutan data tersebut berdasarkan yang paling banyak memiliki rata-rata paling banyak berdasarkan penilaian dari pada pembaca. pada awal kita akan melakukan penghitungan ratincount untuk melihat berapa banyak orang yang memberikan penilaian pada suatu buku dengan fungsi .count(), lalu setelah itu kita melakukan perhitungan rata-rata pada suatu buku dengan fungsi .mean(). Setelah itu kita melakukan penggabungan dan melakukan pengurutan berdasarkan rata-rata penilaian. Kelebihan sistem rekomendasi ini buku yang direkomendasikan oleh sistem sudah pasti populer dan dibaca oleh banyak orang, sedangkan kekurangan dari sistem ini adalah para pembaca belum tentu relevan dan suka dikarenakan setiap orang memiliki seleranya masing-masing.

#### Menampilkan 10 Rekomendasi buku terpopuler

|    |                                         BookTitle |     BookAuthor | RatingCount | AvgRating |
|---:|--------------------------------------------------:|---------------:|------------:|----------:|
|  0 | Harry Potter and the Prisoner of Azkaban (Book 3) |  J. K. Rowling |         428 |  5.852804 |
|  3 |      Harry Potter and the Goblet of Fire (Book 4) |  J. K. Rowling |         387 |  5.824289 |
|  5 |    Harry Potter and the Sorcerer's Stone (Book 1) |  J. K. Rowling |         278 |  5.737410 |
|  9 | Harry Potter and the Order of the Phoenix (Boo... |  J. K. Rowling |         347 |  5.501441 |
| 13 |  Harry Potter and the Chamber of Secrets (Book 2) |  J. K. Rowling |         556 |  5.183453 |
| 16 | The Hobbit : The Enchanting Prelude to The Lor... | J.R.R. TOLKIEN |         281 |  5.007117 |
| 17 | The Fellowship of the Ring (The Lord of the Ri... | J.R.R. TOLKIEN |         368 |  4.948370 |
| 26 | Harry Potter and the Sorcerer's Stone (Harry P... |  J. K. Rowling |         575 |  4.895652 |
| 28 |    The Two Towers (The Lord of the Rings, Part 2) | J.R.R. TOLKIEN |         260 |  4.880769 |
| 39 |                             To Kill a Mockingbird |     Harper Lee |         510 |  4.700000 |

Disini kita melakukan rekomendasi 10 buku terpopuler atau 10 buku yang memiliki rata-rata penilaian terbanyak dari para pembaca. Berdasarkan output diatas maka buku dengan judul  Harry Potter and the Prisoner of Azkaban (Book 3) dan penulis J. K. Rowling adalah buku paling populer dikarenakan memiliki RatingCount 428 dan memiliki rata-rata pada penilain pembaca 5.852804.

- Sistem Rekomendasi Cosine Similarity
<br>
Cosine Similarity kita akan melakukan penghitungan derajat kesamaan berdasarkan korelasi. Disini kita menggunakan fungsi cosine_similarity dari library sklearn. Pada awal kita akan melakukan perhitungan cosine_similarity dengan tfidf_matrix, setelah melakukan perhitungan dengan tfidf_matrix kita akan menampilkan dataframe hasil perhitungan tersebut untuk melihat korelasi antara buku.

|                                BookTitle | Johnny Panic and the Bible of Dreams : Short Stories, Prose, and Diary Excerpts | Anthropology (10th Edition) | The last time I saw mother | Britney Spears: The Unauthorized Biography | The Hedge of Mist: A Book of the Keltiad (Tales of Arthur/Patricia Kennealy-Morrison, Vol 3) |
|-----------------------------------------:|--------------------------------------------------------------------------------:|----------------------------:|---------------------------:|-------------------------------------------:|---------------------------------------------------------------------------------------------:|
|              The Thorn Birds             |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|       Desert Song (Harper Monogram)      |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|               Hiroshima Joe              |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|          Jazz: A Listeners Guide         |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|           The Year of the Panda          |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|             The green ribbon             |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
| Diagrams for Living : The Bible Unveiled |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|                Black Light               |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|              Modern Baptists             |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |
|                The matrix                |                                                                             0.0 |                         0.0 |                        0.0 |                                        0.0 |                                                                                          0.0 |

lalu setelah itu kita akan membuat function book_recommendation yang digunakan untuk membuat rekomendasi buku berdasarkan perhitungan cosine similarity. kita akan menampilkan 5 rekomendasi buku berdasarkan buku The Levant Trilogy (Fortunes of War) dengan penulisnya Olivia Manning.

#### Menampilkan 5 Rekomendasi buku
|   |                 BookTitle |       BookAuthor |
|--:|--------------------------:|-----------------:|
| 0 |        The Balkan Trilogy |   Olivia Manning |
| 1 |        The Levant Trilogy |   Olivia Manning |
| 2 |      Young Wives: A Novel | Olivia Goldsmith |
| 3 |            The Bestseller | Olivia Goldsmith |
| 4 | Fashionably Late: A Novel | Olivia Goldsmith |

Dapat kita lihat bahwa sistem ini dapat merekomendasikan 2 buku olivia manning lainnya, dikarenakan olivia manning hanya memiliki 3 buku. Maka dari itu sistem merekomendasikan buku dari olivia lainnya. Kelebihan sistem ini tidak terpengaruh pada panjang pendeknya suatu dokumen dan memiliki tingkat akurasi yang tinggi. kekurangan dari sistem ini adalah akan merekomendasikan nama yang mirip dengan penulis tersebut.


## Evaluation

Kita akan melakukan evaluasi manual dengan precission, precission adalah merupakan rasio prediksi benar positif dibandingkan dengan keseluruhan hasil yang diprediksi positf. precission memiliki rumus p = # of our recommendations that are relevant / of item we recommend. 

#### Menampilkan 5 Rekomendasi buku pada Cosine Similarity
|   |                 BookTitle |       BookAuthor |
|--:|--------------------------:|-----------------:|
| 0 |        The Balkan Trilogy |   Olivia Manning |
| 1 |        The Levant Trilogy |   Olivia Manning |
| 2 |      Young Wives: A Novel | Olivia Goldsmith |
| 3 |            The Bestseller | Olivia Goldsmith |
| 4 | Fashionably Late: A Novel | Olivia Goldsmith |

Berdasarkan hasil rekomendasi pada sistem cosine similarity kita dapat melihat bahwa sistem memberikan rekomendasi 2 dari 5 rekomendasi yang relevan, maka precission dari hasil rekomendasi ini adalah 40% atau 2/5 


## Sumber Pustaka
[1] BIKI, Y. (n.d.). PENGARUH BIMBINGAN KLASIKAL TEKNIK BIBLIOKONSELING TERHADAP MINAT MEMBACA SISWA KELAS XDI SMA NEGERI 2 GORONTALO. Universitas Negeri Gorontalo.
<br>[2] RAHMAN, S. R. F. (n.d.). ANALISIS TENTANG MINAT BACA SISWA KELAS V SEKOLAH DASAR NEGERI 130 PEKANBARU. Universitas Islam Negeri Sultan Syarif Kasim Riau.
<br>[3] RITDRIX, A. H. (n.d.). SISTEM REKOMENDASI BUKU MENGGUNAKAN METODE ITEM-BASED COLLABORATIVE FILTERING. UNIVERSITAS DIPONEGORO.
