# Laporan Proyek _Anime Recommender System_ - Syahvan Alviansyah Diva Ritonga
## Project Overview

<p align="center">
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/anime.jpg" />
  <br>
  Gambar 1. Anime
</p>

Anime telah menjadi bagian tak terpisahkan dari budaya populer di Indonesia, merajai hati para penggemar selama bertahun-tahun. Dari klasik seperti Doraemon dan Sailormoon hingga saga epik seperti Dragonball, One Piece, dan Naruto, keduanya telah mengukir jejaknya di layar televisi dan di hati para penggemar di seluruh negeri. Stasiun televisi pun tak ragu-ragu memanjakan penonton dengan aksi seru dan petualangan dari dunia anime yang memikat.

Dengan laju perkembangan yang pesat, industri animasi Jepang telah melahirkan sejumlah besar anime yang menggugah minat para penonton dari berbagai kalangan. [1]. Kehadiran platform _streaming_ dan _database_ yang kaya akan konten anime membuat penggemar anime memiliki kemudahan akses untuk menonton berbagai judul anime dari berbagai genre dan era. Namun, dengan begitu banyaknya pilihan yang tersedia, penggemar seringkali kesulitan untuk menemukan anime yang sesuai dengan preferensi dan minat mereka [2].

Untuk mengatasi tantangan ini, perlu adanya pengembangan sebuah sistem yang dapat memberikan rekomendasi secara efektif. Sistem rekomendasi bertujuan untuk menyajikan konten yang relevan dan menarik bagi penggemar anime berdasarkan preferensi mereka [3]. Dengan adanya sebuah sistem rekomendasi, diharapkan penggemar dapat lebih mudah menemukan anime yang sesuai dengan selera dan minat mereka, sehingga pengalaman menonton mereka dapat ditingkatkan dan mereka dapat menikmati berbagai judul anime dengan lebih maksimal.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang di atas, berikut ini batasan masalah yang dapat diselesaikan dengan proyek ini:

- Bagaimana caranya mengembangkan sebuah sistem rekomendasi anime yang dapat disesuaikan dengan preferensi individu para penggemar anime?
- Model apa yang paling efektif dalam memberikan rekomendasi kepada penggemar anime untuk memilih anime yang sesuai?
- Bagaimana proses kerja sistem rekomendasi dalam memberikan rekomendasi kepada penggemar anime untuk memilih anime yang sesuai dengan preferensi mereka?

### Goals

Adapun tujuan dilakukannya proyek ini yaitu:

- Membuat suatu sistem rekomendasi anime bertujuan untuk memberikan kemudahan kepada penggemar anime dalam menemukan judul-judul anime yang cocok dengan preferensi mereka.
- Melakukan perbandingan kinerja berbagai model dalam sistem rekomendasi anime guna menemukan yang paling efektif.
- Menjelaskan prinsip kerja dari algoritma-algoritma model yang digunakan dalam sistem rekomendasi untuk memberikan rekomendasi anime kepada penggemar anime berdasarkan data seperti preferensi sebelumnya, rating, atau informasi lainnya.

### Solution Statements

- Untuk eksplorasi fitur, dilakukan melalui Analisis Univariat yang bertujuan untuk memeriksa distribusi suatu fitur tertentu di dalam dataset. Pendekatan ini melibatkan penggunaan teknik visualisasi data, seperti barplot, untuk menyajikan informasi mengenai fitur yang dipilih tersebut.
- Melakukan pemodelan menggunakan beberapa algoritma seperti _Content Based Filtering_ dan _Collaborative Filtering_ untuk mencapai solusi yang diinginkan.
- Untuk mengetahui perfoma model dilakukan pengecekan performa dengan metrik evaluasi seperti _Precision_, _Cosine similarity_, dan _Root Mean Squared Error_ (RMSE).

## Data Understanding
Dataset yang digunakan merupakan data anime yang berasal dari [MyAnimeList.net](https://myanimelist.net/) pada laman [Kaggle](https://www.kaggle.com/datasets/timnosov/anime-recommendations-database-clean/). Dataset tersebut berisikan 2 file csv, yaitu file *Anime* dan *Rating*. File Anime.csv yang terdiri dari 7 kolom dan 12294 baris, Sedangkan file Rating.csv terdiri dari 3 kolom dan 7813737 baris. 

Berikut merupakan informasi lebih detail dari masing masing kolom dataset:

*   **Anime.csv**
1.   `anime_id`: Id unik myanimelist.net untuk mengidentifikasi anime.
2.   `name`: nama lengkap anime
3.   `genre`: daftar genre untuk anime ini.
4.   `type`: film, TV, OVA, dll.
5.   `episodes`: seberapa banyak episode dalam acara ini, 1 jika film.
6.   `rating`: peringkat rata-rata dari 10 untuk anime ini.
7.   `members`: jumlah anggota komunitas yang ada di anime ini

*   **Rating.csv**

1.   `user_id`: id pengguna yang dibuat secara acak yang tidak dapat diidentifikasi.
2.   `anime_id`: anime yang telah dinilai pengguna ini.
3.   `rating`: anime yang telah dinilai oleh pengguna ini, rating dari 10 pengguna ini telah ditetapkan (-1 jika pengguna menontonnya tetapi tidak menetapkan peringkat).

Untuk memahami data lebih lanjut, dilakukan **Analisis Univariat** serta **Visualisasi Data**

Analisis Univariat merupakan bentuk analisis data yang hanya merepresentasikan informasi yang terdapat pada satu variabel. Jenis visualisasi ini umumnya digunakan untuk memberikan gambaran terkait distribusi sebuah variabel dalam suatu dataset. Sebagai alat bantu analisis, dilakukan teknik Visualisasi Data. Memvisualisasikan data memberikan wawasan mendalam tentang perilaku berbagai fitur-fitur yang tersedia dalam dataset. Teknik visualisasi yang digunakan pada pembuatan model proyek ini adalah dengan menggunakan barplot yang digunakan untuk memplot distribusi data.

Berikut adalah hasil Exploratory Data Analysis (EDA) menggunkan Analisis Univariat dengan teknik Visualisasi Data menggunakan barplot.

## Data Preparation
Dalam _data preparation_, prinsip **"_garbage in, garbage out_"** berlaku. Artinya, jika data yang digunakan untuk melatih model tidak berkualitas baik, maka hasil prediksi dari model tersebut juga akan tidak akurat atau tidak dapat diandalkan. Dengan memastikan data yang digunakan untuk melatih model memiliki kualitas yang baik, model yang dihasilkan dapat lebih andal dalam merekomendasikan anime.

Proses _data preparation_ meliputi beberapa tahap:

- **Pembersihan Data**

  Dalam tahap ini, langkah awal dilakukan dengan membersihkan dataset agar data menjadi lebih terstruktur dan siap untuk diproses lebih lanjut. Teknik pembersihan yang digunakan termasuk penggunaan metode Dropna, di mana baris yang memiliki nilai kosong (null/NaN) dalam kolom tertentu akan dihapus. Selain itu, metode fillna juga diterapkan untuk mengisi nilai kosong dengan nilai tertentu dalam kolom yang relevan, memastikan integritas data tetap terjaga.

- **Merging Dataset**

  Selanjutnya, dataset anime.csv dan rating.csv digabungkan berdasarkan kunci yang sama, yaitu 'anime_id'. Proses penggabungan dataset ini dilakukan untuk menggabungkan informasi yang terkait dari kedua dataset menjadi satu kesatuan yang lebih lengkap dan terintegrasi.

- **Feature extraction menggunakan TfidfVectorizer**

  Dalam langkah ini, alat TfidfVectorizer digunakan untuk mengonversi teks atau data mentah menjadi representasi numerik dalam bentuk matriks fitur TF-IDF. Penggunaan TfidfVectorizer pada kasus ini membantu mengubah nilai-nilai dalam kolom tertentu menjadi vektor, yang akan digunakan dalam proses perhitungan kesamaan kosinus (cosine_similarity).

- **Pembagian Dataset menjadi Data Train dan Data Validation**

  Tahap selanjutnya adalah membagi dataset menjadi dua bagian: data latih dan data validasi. Pembagian ini dilakukan secara manual dengan tujuan untuk melatih dan mengevaluasi kinerja model yang akan dikembangkan. Dalam proyek ini, sebanyak 80% dari dataset digunakan untuk melatih model, sementara 20% sisanya disisihkan untuk mengevaluasi model.

- **Standardisasi**

  Pada tahap ini, dilakukan proses standardisasi menggunakan metode MinMaxScaler secara manual. Proses standardisasi ini bertujuan untuk menormalkan skala data terutama pada data numerik. Standardisasi tersebut diterapkan dalam persiapan data untuk pengembangan model dengan Collaborative Filtering.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

## References

[1] Nuurshadieq and A. T. Wibowo, "Leveraging Side Information to Anime Recommender System using Deep learning," 2020 3rd International Seminar on Research of Information Technology and Intelligent Systems (ISRITI), Yogyakarta, Indonesia, 2020, pp. 62-67, doi: 10.1109/ISRITI51436.2020.9315363.

[2] S. Ota, H. Kawata, M. Muta, S. Masuko, dan J. Hoshino, "AniReco: Japanese Anime Recommendation System," dalam Entertainment Computing – ICEC 2017, N. Munekata, I. Kunita, dan J. Hoshino, Eds. Cham: Springer, 2017, jld. 10507. https://doi.org/10.1007/978-3-319-66715-7_49.

[3] F. Ricci, L. Rokach, dan B. Shapira, "Introduction to Recommender Systems Handbook," dalam Recommender Systems Handbook, F. Ricci, L. Rokach, B. Shapira, dan P. Kantor, Eds. Boston, MA: Springer, 2011. https://doi.org/10.1007/978-0-387-85820-3_1.
