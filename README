# Laporan Proyek Machine Learning - Bintang Ramadhan

## Project Overview

Aplikasi streaming digital saat ini mengalami lonjakan konten yang sangat besar, baik dalam bentuk film, serial, musik, hingga animasi Jepang atau anime. Platform seperti Netflix, Crunchyroll, atau Bstation menyediakan ribuan judul anime dari berbagai genre, durasi, dan segmentasi pasar. Di tengah berlimpahnya pilihan ini, pengguna sering kali mengalami kesulitan dalam menemukan tayangan yang sesuai dengan preferensi mereka. Hal ini dikenal sebagai information overload, yaitu kondisi di mana banyaknya informasi justru membuat proses pengambilan keputusan menjadi tidak efisien (Ricci et al., 2015).

Untuk menjawab tantangan tersebut, sistem rekomendasi menjadi solusi utama yang digunakan oleh berbagai platform digital. Sistem ini mempelajari perilaku, preferensi, dan histori tontonan pengguna untuk kemudian menyarankan konten yang relevan dan personal. Studi oleh Gómez-Uribe dan Hunt (2015) menunjukkan bahwa sistem rekomendasi berkontribusi secara signifikan dalam meningkatkan retensi pengguna, waktu menonton, dan pendapatan platform seperti Netflix.

Dalam konteks anime, tantangan ini menjadi semakin relevan. Anime memiliki keragaman genre yang sangat luas seperti action, slice of life, fantasy, dan psychological. Beberapa judul populer bahkan bisa masuk dalam lebih dari tiga genre sekaligus. Selain itu, anime seringkali memiliki nuansa budaya yang khas, sehingga preferensi terhadap anime bisa sangat personal dan tidak selalu tergambar dari genre atau rating saja. Oleh karena itu, pengembangan sistem rekomendasi khusus untuk anime menjadi sangat penting bagi platform streaming anime. Sistem ini tidak hanya menyarankan anime berdasarkan genre, tetapi juga mempertimbangkan kesamaan konten dan perilaku pengguna untuk memberikan rekomendasi yang lebih akurat dan memuaskan.

Dengan sistem rekomendasi anime yang baik, pengguna dapat menemukan judul-judul yang sesuai selera tanpa harus menelusuri ribuan konten secara manual. Hal ini meningkatkan pengalaman pengguna sekaligus efisiensi dan daya saing platform streaming anime itu sendiri.

**Referensi**:  
- Gómez-Uribe, C. A., & Hunt, N. (2015). The Netflix recommender system: Algorithms, business value, and innovation. ACM Transactions on Management Information Systems (TMIS), 6(4), 1–19. https://doi.org/10.1145/2843948

- Ricci, F., Rokach, L., & Shapira, B. (2015). Recommender systems handbook. Springer.

- Sharma, A., & Singh, S. (2017). A survey on recommendation system based on collaborative filtering and content based filtering. International Journal of Computer Applications, 163(7), 1–6.

## Business Understanding

### Problem Statements

* Bagaimana membangun sistem yang mampu merekomendasikan anime yang mirip berdasarkan konten seperti genre?
* Bagaimana sistem dapat mempelajari preferensi pengguna untuk memberikan rekomendasi yang lebih personal?

### Goals

* Menghasilkan sistem rekomendasi berbasis konten yang dapat mengidentifikasi kemiripan antar anime.
* Mengembangkan sistem rekomendasi berbasis perilaku pengguna untuk memberikan saran anime yang disukai pengguna berdasarkan riwayat rating mereka.

### Solution Statements

1. Pendekatan **Content-Based Filtering** dilakukan dengan cara memanfaatkan informasi genre dari setiap anime untuk mengukur kesamaan antar judul.
2. Pendekatan **Collaborative Filtering** dilakukan dengan mempelajari pola interaksi antara pengguna dan anime berdasarkan rating yang diberikan, agar sistem mampu menyarankan anime meskipun tidak memiliki informasi genre yang lengkap.

## Data Understanding

Dataset diperoleh dari Kaggle: [Anime Recommendation Database](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)

Terdapat 2 file :

1. **anime.csv**
   - Jumlah baris: 12.294
   - Jumlah kolom: 7
   - Fitur-fitur:
     - `anime_id`: ID unik untuk setiap anime
     - `name`: Nama anime
     - `genre`: Genre anime
     - `type`: Tipe anime (TV, Movie, dll.)
     - `episodes`: Jumlah episode
     - `rating`: Rating rata-rata
     - `members`: Jumlah yang menonton
    
    - Kondisi:
    ![Alt text](https://raw.githubusercontent.com/TangRmdhn/Rekomendasi-Anime/refs/heads/main/Assets1/Anime%20Null.png "a title")
        - Terdapat 62 data missing di kolom `genre` 
        - Terdapat 25 data missing di kolom `type` 
        - Terdapat 230 data missing di kolom `rating` 
        - Tidak ada data yang duplikat

2. **rating.csv**
   - Jumlah baris: 7.813.737
   - Jumlah kolom: 3
   - Fitur-fitur:
     - `user_id`: ID pengguna
     - `anime_id`: ID anime
     - `rating`: Skor rating yang diberikan pengguna

    - Kondisi:
    ![Alt text](https://raw.githubusercontent.com/TangRmdhn/Rekomendasi-Anime/refs/heads/main/Assets1/Rating%20Duplikat.png "a title")
        - Tidak ada missing value
        - Terdapat 1 data yang duplikat

**Insight**:
- Terdapat 43 genre berbeda
- Ditemukan user ID 48766 yang memberi lebih dari 10.000 rating dan semuanya -1

## Data Preparation

Beberapa tahapan data preparation yang dilakukan antara lain:

* Handling missing value Dataset Anime
Menghapus data yang hilang pada kolom `genre` Karena untuk membuat model Content Based Learning membutuhkan nilai dari kolom `genre` sehingga kolom `genre` sangat penting.
alasan: Tidak diketahui genre dari suatu anime tersebut.
* Handling duplikat data
Menghapus data yang duplikat
alasan: Karena hanya terdapat 1 data yang duplikat, cara mudahnya adalah dengan menghapus

* Menghubah format penulisan value pada kolom `genre`
Menghapus tanda `,` pada setiap baris yang memiliki genre lebih dari 1.
alasan: untuk memastikan representasi fitur genre yang benar saat menggunakan teknik Content-Based Filtering berbasis TF-IDF. 

* Menggabungkan Data
Menggabungkan Data rating user dengan anime dan genre
Alasan: Menyiapkan untuk digunakan nanti

* Handling data yang tidak logis
Menghapus data user ID 48766 yang memberi lebih dari 10.000 rating dan semuanya -1
alasan: Menghapus karena data tersebut tidak logis

* Handling missing value data yang sudah digabungkan
Menghapus data yang hilang pada kolom `nama` dan `genre` 
alasan : Menghapus adalah cara handling yang paling mudah

* Menghurutkan data
Menghurutkan data berdasarkan kolom `anime_id` dari value terkecil
alasan: lebih mudah dilihat

* Menghapus data duplikat
Membuat variable data preparation dan Menghapus data duplikat pada kolom `anime_id`
alasan : supaya tidak terjadi dobel atau rangkap genre dalam satu anime. Sehingga, sistem dapat merekomendasikan anime berdasarkan genre masakannya. 

* Konversi data
Konversi data series menjadi list
alasan : karena untuk nanti digunakan pelatihan model.predict() pada TensorFlow/Keras

* Membuat dictionary
Membuat dictionary untuk data `anime_id`, `anime_name`, dan `genre`
alasan: untuk digunakan pelatihan

* TF-IDF Vectorizer
Menggunakan fungsi tfidfvectorizer() dari library sklearn pada kolom `genre`
alasan: untuk menemukan representasi fitur penting dari setiap genre anime.

* Menghapus data yang terlalu banyak
Menghapus data dengan radom menjadi hanya 10.000 data saja 
alasan: data yang sangat banyak terlalu menguras sumber daya dan waktu untuk melakukan training

* Mengubah `user_id` menjadi list
mengubah menggunakan to_list
alasan: data ingin diencode

* Encoding `user_id`
encoding data `user_id` yang sangat banyak menjadi lebih mudah
alasan: agar data user_id tidak terlihat terlalu banyak dan mudah dibaca

* Memetakan `user_id` dan `anime_id`
Memetakan `user_id` dan `anime_id`  ke dataframe yang berkaitan.
  alasan: Agar data rating bisa terhubung dengan data anime dan pengguna, sehingga sistem bisa mengenali judul atau genre berdasarkan ID-nya.

* Mengubah nilai rating
Mengubah nilai rating menjadi float.
  alasan: Supaya rating bisa dihitung oleh model, karena sebagian besar algoritma butuh data numerik dalam format float.

* **Mapping user dan anime**  
  Mengambil kolom user dan anime dari dataframe dan mengubahnya ke dalam bentuk array NumPy.
alasan: Agar setiap pengguna dan anime punya ID unik dalam bentuk angka untuk mempermudah pemrosesan oleh model.

* **Mengubah rating ke skala 0–1**  
Menormalisasi nilai rating ke skala 0–1 menggunakan rumus min-max normalization.
alasan: Supaya model lebih mudah belajar karena nilai rating sudah dinormalisasi.

* **Spliting data** 
Membagi data menjadi (80:20) bagian: x_train, y_train untuk pelatihan, dan x_val, y_val untuk validasi.
alasan: Untuk memisahkan data pelatihan dan data validasi agar model bisa diuji performanya pada data yang belum pernah dilihat.

## Modeling

Proyek ini menggunakan dua jenis model sistem rekomendasi:

1. **Content-Based Filtering**  
   Sistem ini memberikan rekomendasi berdasarkan kesamaan konten antar anime, terutama dari sisi genre. Sistem akan mencari anime yang memiliki genre serupa dengan anime yang disukai pengguna sebelumnya.
    - Kelebihan: Content-Based Filtering memiliki kelebihan karena mampu memberikan rekomendasi yang relevan berdasarkan kesamaan konten seperti genre, serta tidak bergantung pada data pengguna lain.
    - Kekurangan: cenderung kurang variatif dan hanya merekomendasikan anime yang mirip dengan yang sudah disukai.

Output : ![Alt text](https://raw.githubusercontent.com/TangRmdhn/Rekomendasi-Anime/refs/heads/main/Assets1/Top%205%20Content%20Based.png "a title")

2. **Collaborative Filtering**  
   Sistem ini belajar dari pola rating pengguna. Dengan menggunakan teknik embedding dan neural network, model dapat mempelajari relasi antara pengguna dan anime untuk memprediksi rating terhadap anime yang belum ditonton.
    - Kelebihan: mampu memberikan rekomendasi yang lebih beragam dengan memanfaatkan pola rating dari pengguna lain yang memiliki preferensi serupa
    - kelemahan: memiliki masalah cold-start dan sulit dijelaskan secara transparan karena bergantung pada pola interaksi yang kompleks.

Output : ![Alt text](https://raw.githubusercontent.com/TangRmdhn/Rekomendasi-Anime/refs/heads/main/Assets1/Top%2010%20Collab.png "a title")

## Evaluation

Evaluasi dilakukan menggunakan metrik **Root Mean Squared Error (RMSE)** untuk model collaborative filtering. Nilai RMSE yang diperoleh pada data validasi adalah sekitar **1.03**, yang menunjukkan bahwa prediksi sistem cukup dekat dengan rating aktual yang diberikan oleh 

RMSE = sqrt( (1/n) * Σ(yᵢ - ŷᵢ)² )
Keterangan:
- `yᵢ` = rating aktual pengguna,
- `ŷᵢ` = rating hasil prediksi model,
- `n` = jumlah total data.

Semakin kecil nilai RMSE, maka semakin baik performa model karena berarti prediksi rating yang dihasilkan lebih mendekati nilai sebenarnya.

Untuk content-based filtering, evaluasi dilakukan secara manual dengan mengamati hasil rekomendasi dan memastikan bahwa anime yang direkomendasikan memang memiliki kemiripan konten dengan anime referensi. Walaupun tidak bisa dievaluasi secara kuantitatif seperti collaborative filtering, pendekatan ini cukup efektif dalam memberikan hasil yang relevan secara konten.

![Alt text](https://raw.githubusercontent.com/TangRmdhn/Rekomendasi-Anime/refs/heads/main/Assets1/epoch.png "a title")

Model collaborative filtering yang digunakan menunjukkan kinerja yang baik karena berhasil menurunkan RMSE pada data training dan test secara konsisten. Grafik ini menjadi indikator bahwa proses pelatihan berjalan dengan benar dan model memiliki kemampuan generalisasi yang layak.
