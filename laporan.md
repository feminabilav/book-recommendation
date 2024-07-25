# Laporan Proyek Machine Learning - Femi Nabila

## Project Overview

Industri buku telah mengalami perubahan signifikan dengan munculnya teknologi digital dan e-commerce. Dengan perpustakaan yang luas dan beragam, serta kemudahan akses yang diberikan oleh toko buku online, pembaca kini memiliki lebih banyak pilihan daripada sebelumnya. Namun, dengan begitu banyaknya pilihan, menemukan buku yang sesuai dengan selera dan minat individu menjadi tantangan tersendiri. Oleh karena itu, sistem rekomendasi buku menjadi suatu peran penting dalam membantu pengguna menemukan buku yang mereka sukai.

Sistem rekomendasi sering digunakan dalam kehidupan online kita, sistem ini digunakan pada platform seperti YouTube, Amazon, dan Netflix. Sistem rekomendasi merupakan algoritma yang bertujuan menyarankan item yang relevan kepada pengguna. Penggunaan sistem rekomendasi yang baik dapat menghasilkan pendapatan besar karena loyalitas pengguna dan dapat menjadi pembeda dari kompetitor.

Proyek ini penting karena sistem rekomendasi yang efektif dapat secara signifikan meningkatkan pengalaman pengguna dengan menyarankan buku yang relevan dengan minat dan preferensi mereka. Dataset Book-Crossing adalah sumber data yang berharga untuk membangun sistem rekomendasi buku. Dataset ini mencakup informasi pengguna, buku, dan rating buku. Dengan menggunakan metode collaborative filtering, model rekomendasi ini memanfaatkan preferensi pengguna untuk menyarankan buku yang mungkin disukai.

## Business Understanding

Ada beberapa problem statement dan goals yang diangkat dalam proyek ini yaitu:

### Problem Statements

- Pengguna kesulitan menemukan buku yang sesuai dengan minat mereka di tengah banyaknya pilihan yang tersedia:
  Hal ini menyebabkan waktu yang dihabiskan untuk mencari buku yang tepat menjadi lebih lama dan dapat mengurangi kepuasan pengguna.
- Platform buku mengalami kesulitan dalam meningkatkan keterlibatan pengguna dan mempertahankan loyalitas mereka:
  Tanpa sistem rekomendasi yang efektif, pengguna mungkin merasa frustrasi atau tidak tertarik untuk kembali, yang dapat mengakibatkan penurunan penggunaan platform dan pendapatan.


### Goals

- Mengembangkan sistem rekomendasi yang dapat menyarankan buku-buku sesuai dengan minat dan preferensi pengguna:
  Menciptakan sistem rekomendasi berbasis collaborative filtering yang dapat memahami preferensi pengguna berdasarkan rating pengguna. 
- Meningkatkan keterlibatan dan loyalitas pengguna melalui rekomendasi yang lebih personal dan relevan:
  Dengan menyediakan rekomendasi buku yang relevan dan disesuaikan dengan preferensi masing-masing pengguna, diharapkan dapat membuat pengguna lebih terlibat dan loyal terhadap platform


## Data Understanding
Dataset Book-Crossing terdiri dari tiga file utama: Users, Books, dan Ratings. [Book Recommendation Dataset Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset?select=Books.csv).


**Users**
- Jumlah data: Terdiri dari 3 kolom dan 278,858 baris
- Kondisi: Terdapat outliers pada fitur Age, dan terdapat missing values pada User-ID dan Age

**Books**
- Jumlah data: Terdiri dari 8 kolom dan 271,360 baris
- Kondisi: Terdapat outliers dan tipe data yang salah pada fitur Year-Of-Publication, dan terdapat missing values pada Publisher dan Book-Author

**Ratings**
- Rating yang bernilai antara angka 0 sampai 10
- Jumlah data: Terdiri dari 3 kolom dan 1,149,780 baris
- Kondisi: Terdapat missing values pada Book-Rating

Variabel-variabel pada Book Recommendation dataset adalah sebagai berikut:

**Users**
- User-ID: ID pengguna yang telah dianonimkan dan dipetakan ke dalam angka integer.
- Location: Lokasi pengguna yang terdiri dari tiga komponen utama: kota, negara bagian, dan negara. Contoh: "New York, NY-USA".
- Age: Usia pengguna. Nilai ini bisa berupa NULL jika data usia tidak tersedia.

**Books**
- ISBN: International Standard Book Number, yang berfungsi sebagai identifikasi unik setiap buku.
- Book-Title: Judul buku.
- Book-Author: Nama penulis buku. Jika buku memiliki beberapa penulis, hanya penulis pertama yang dicantumkan.
- Year-Of-Publication: Tahun terbit buku.
- Publisher: Penerbit buku.
- Image-URL-S: URL gambar sampul buku ukuran kecil yang mengarah ke situs Amazon.
- Image-URL-M: URL gambar sampul buku ukuran sedang yang mengarah ke situs Amazon.
- Image-URL-L: URL gambar sampul buku ukuran besar yang mengarah ke situs Amazon.

**Ratings**
- User-ID: ID pengguna yang memberikan rating.
- ISBN: International Standard Book Number dari buku yang diberikan rating.
- Book-Rating: Nilai rating yang diberikan oleh pengguna. Rating ini dapat berupa:
    Nilai dari 1 hingga 10, di mana nilai yang lebih tinggi menunjukkan apresiasi yang lebih tinggi.
    Nilai 0 yang menunjukkan rating implisit (misalnya, pengguna menunjukkan ketertarikan tanpa memberikan rating eksplisit).

## Data Preparation
1. Dilakukan proses merge pada ketiga file dataset sehingga tabel berisi User-ID,	ISBN,	Book-Rating,	Book-Title,	Book-Author, Year-Of-Publication,	Publisher, dan	Age. Hal ini dilakukan untuk memudahkan analisis agar semua data yang diperlukan menjadi 1
2. Pengubahan tipe data Year-Of-Publication menjadi integer agar dapat digunakan dalam perhitungan numerik dan menangani nilai yang tidak valid
3. Menghapus data outliers berdasarkan IQR untuk memperbaiki distribusi data dan menghindari adanya pengaruh nilai ekstrim terhadap perhitungan model
4. Menghapus baris yang memiliki missing values untuk memastikan bahwa data yang digunakan lengkap
5. Encoding User-ID dan ISBN menjadi indeks integer agar data dapat dengan mudah diproses model
6. Train Test Split dengan rasio 80:20 dan dengan shuffle untuk menghindari adanya bias/urutan dalam data

## Modeling
Tahapan yang dilakukan dalam pengembangan model adalah sebagai berikut:

1. Data Preparation: Mengumpulkan dan membersihkan data. Memastikan data yang digunakan mencakup informasi yang relevan seperti rating buku, identitas pengguna, dan identitas buku.

2. Membangun Model RecommenderNet:
    - Model yang digunakan dalam proyek ini adalah model rekomendasi berbasis Item-Based Collaborative Filtering yang diimplementasikan menggunakan TensorFlow dan Keras. 
    - Model menghitung dengan mengambil vector user dan books, kemudian menggunakan dot product dan teknik embedding untuk menghitung kemiripan antara buku berdasarkan fitur-fitur tertentu. Kemudian ditambahkan bias pengguna dan bias buku untuk mendapatkan skor prediksi
    - Digunakan fungsi aktivasi sigmoid untuk menghasilkan output skor yang bernilai antara 0 sampai 1
    - Model melakukan prediksi Rating menggunakan kemiripan dan rating aktual dari buku-buku yang serupa untuk memprediksi rating buku yang belum dibaca oleh pengguna.
    - Parameter yang digunakan: 
      - num_users: Jumlah total pengguna dalam dataset.
      - num_book: Jumlah total buku dalam dataset.
      - embedding_size: Dimensi dari vektor embedding yang digunakan untuk merepresentasikan pengguna dan buku.

3. Model Training:
    - Model dilatih menggunakan Loss BinaryCrossentropy dan Optimizer Adam.
    - Epoch yang digunakan sebesar 10 dengan batch size 32 untuk melatih model hingga mencapai konvergensi yang cukup baik.

4. Evaluasi Model: Model dievaluasi menggunakan metric RMSE (Root Mean Squared Error) untuk mengukur seberapa akurat prediksi yang dihasilkan oleh model.

Setelah model dilatih, model dapat memberikan rekomendasi kepada pengguna dengan melakukan prediksi rating. Berikut adalah cara kerja sistem rekomendasi sehingga sistem rekomendasi dapat menyarankan buku-buku sesuai dengan minat dan preferensi pengguna.

5. Sistem Rekomendasi
    - Prediksi Rating: Model memprediksi rating buku berdasarkan kemiripan buku-buku yang telah di-rating oleh pengguna.
    - Top 10 Rekomendasi: Menghasilkan daftar Top 10 buku dengan prediksi rating tertinggi yang belum pernah dibaca atau di-rating oleh pengguna tersebut.

Berikut contoh hasil rekomendasi buku untuk user 63714
|Top 10 Book recommendation |
|---------------------------|
|The Outlandish Companion by DIANA GABALDON|
|The Lord of the Rings (Leatherette Collector's Edition) by J. R. R. Tolkien|
|The Last Battle (The Chronicles of Narnia, Book 7) by C. S. Lewis|
|Death: The High Cost of Living by Neil Gaiman|
|The Lorax by Dr. Seuss|
|...|

## Evaluation
Digunakan metrik evaluasi Root Mean Squared Error (RMSE) untuk mengukur akurasi prediksi rating model. RMSE dihitung dengan mengambil akar dari rata-rata kuadrat selisih nilai aktual dan nilai prediksi. Maka dari itu, metrik ini memberikan bobot lebih pada kesalahan yang besar, sehingga sangat berguna untuk mengevaluasi seberapa baik model dalam menangani prediksi dengan deviasi besar. 

**Hasil Evaluasi**
- RMSE Data Latih: ~0.2
- RMSE Data Uji: ~0.35

RMSE yang relatif rendah menunjukkan bahwa model memiliki akurasi prediksi yang baik secara keseluruhan. Ini mengindikasikan bahwa model cukup efektif dalam memprediksi rating buku sesuai dengan minat dan preferensi pengguna.

Sistem rekomendasi berbasis Item-Based Collaborative Filtering yang dikembangkan berhasil memahami preferensi pengguna berdasarkan rating pengguna lain yang serupa. Dengan RMSE yang rendah (0.2 dan 0.35), menunjukkan bahwa sistem ini akurat dalam memberikan rekomendasi untuk user berdasarkan rating yang telah diberikan. Dengan menyediakan rekomendasi buku yang relevan dan disesuaikan dengan preferensi masing-masing pengguna, sistem ini membuat pengguna lebih terlibat dan loyal terhadap platform. Rekomendasi yang akurat membuat pengguna merasa dihargai dan dimengerti, yang mendorong mereka untuk terus menggunakan platform. Pengguna yang merasa rekomendasinya tepat cenderung kembali menggunakan platform, yang pada akhirnya meningkatkan loyalitas dan penggunaan platform.
