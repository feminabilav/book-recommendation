# Book Recommendation with Collaborative Filtering

| | Deskripsi |
| ----------- | ----------- |
| Dataset | [Book Recommendation Dataset Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset?select=Books.csv) |
| Masalah | Adanya kesulitan menemukan buku yang sesuai dengan minat mereka di tengah banyaknya pilihan yang tersedia |
| Solusi machine learning | Menciptakan sistem rekomendasi berbasis collaborative filtering yang dapat memahami preferensi pengguna berdasarkan rating pengguna |
| Metode pengolahan | Penanganan tipe data yang tidak sesuai, penanganan outliers, penanganan missing values, dan train-test split |
| Arsitektur model | Membangun Model RecommenderNet yang menghitung kemiripan antar buku menggunakan dot product dan teknik embedding dan juga fungsi aktivasi sigmoid untuk output |
| Metrik evaluasi | Digunakan metrik evaluasi Root Mean Squared Error (RMSE) untuk mengukur akurasi prediksi rating model. RMSE dihitung dengan mengambil akar dari rata-rata kuadrat selisih nilai aktual dan nilai prediksi. |
| Performa model | RMSE Data Latih sebesar ~0.2 dan RMSE Data Uji sebesar ~0.35 |
