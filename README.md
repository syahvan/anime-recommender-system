# Anime Recommender System
## Project Overview

<p align="center">
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/anime.jpg" />
  <br>
  Gambar 1. Anime
</p>

Anime telah menjadi bagian tak terpisahkan dari budaya populer di Indonesia, merajai hati para penggemar selama bertahun-tahun. Dari klasik seperti Doraemon dan Sailormoon hingga saga epik seperti Dragonball, One Piece, dan Naruto, keduanya telah mengukir jejaknya di layar televisi dan di hati para penggemar di seluruh negeri. Stasiun televisi pun tak ragu-ragu memanjakan penonton dengan aksi seru dan petualangan dari dunia anime yang memikat.

Dengan laju perkembangan yang pesat, industri animasi Jepang telah melahirkan sejumlah besar anime yang menggugah minat para penonton dari berbagai kalangan. [1]. Kehadiran platform _streaming_ dan _database_ yang kaya akan konten anime membuat penggemar anime memiliki kemudahan akses untuk menonton berbagai judul anime dari berbagai *genre* dan era. Namun, dengan begitu banyaknya pilihan yang tersedia, penggemar seringkali kesulitan untuk menemukan anime yang sesuai dengan preferensi dan minat mereka [2].

Untuk mengatasi tantangan ini, perlu adanya pengembangan sebuah sistem yang dapat memberikan rekomendasi secara efektif. Sistem rekomendasi bertujuan untuk menyajikan konten yang relevan dan menarik bagi penggemar anime berdasarkan preferensi mereka [3]. Dengan adanya sebuah sistem rekomendasi, diharapkan penggemar dapat lebih mudah menemukan anime yang sesuai dengan selera dan minat mereka, sehingga pengalaman menonton mereka dapat ditingkatkan dan mereka dapat menikmati berbagai judul anime dengan lebih maksimal.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang di atas, berikut ini batasan masalah yang dapat diselesaikan dengan proyek ini:

- Bagaimana caranya mengembangkan sebuah sistem rekomendasi anime yang dapat disesuaikan dengan preferensi individu para penggemar anime?
- Bagaimana proses kerja sistem rekomendasi dalam memberikan rekomendasi kepada penggemar anime untuk memilih anime yang sesuai dengan preferensi mereka?
- Berdasarkan eksplorasi dataset, bagaimana karakteristik dataset? Ada berapa banyak jumlah data? Fitur apa yang bisa dipilih untuk pengembangan model?
- Bagaimana mengolah dataset agar dapat dibuat model sistem rekomendasi?
- Bagimana membuat model sistem rekomendasi menggunakan _Content Based Filtering_ dan _Collaborative Filtering_?
- Bagaimanna cara mengukur nilai perfoma model sistem rekomendasi yang telah dibangun?

### Goals

Adapun tujuan dilakukannya proyek ini yaitu:

- Membuat suatu sistem rekomendasi anime bertujuan untuk memberikan kemudahan kepada penggemar anime dalam menemukan judul-judul anime yang cocok dengan preferensi mereka.
- Menjelaskan prinsip kerja dari algoritma-algoritma model yang digunakan dalam sistem rekomendasi untuk memberikan rekomendasi anime kepada penggemar anime berdasarkan data seperti preferensi sebelumnya, _rating_, atau informasi lainnya.
- Mengeksplorasi informasi dataset dan melihat fitur yang paling memungkinkan dipilih untuk pengembangan model
- Melakukan proses Data Preparation seperti _Vectorizing_, _Encoded_, dan _Data Spliting_ sebelum pembuatan model
- Membuat model sistem rekomendasi _Content Based Filtering_ dan _Collaborative Filtering_ berdasarkan fitur yang telah dipilih dari dataset
- Mengukur perfoma model sistem rekomendasi dengan menggunakan metrik evaluasi

### Solution Statements

- Untuk eksplorasi fitur, dilakukan melalui Analisis Univariat yang bertujuan untuk memeriksa distribusi suatu fitur tertentu di dalam dataset. Pendekatan ini melibatkan penggunaan teknik visualisasi data, seperti barplot, untuk menyajikan informasi mengenai fitur yang dipilih tersebut.
- Melakukan pemodelan menggunakan beberapa algoritma seperti _Content Based Filtering_ dan _Collaborative Filtering_ untuk mencapai solusi yang diinginkan.
- Untuk mengetahui perfoma model dilakukan pengecekan performa dengan metrik evaluasi seperti _Cosine similarity_, dan _Root Mean Squared Error_ (RMSE).

## Data Understanding
Dataset yang digunakan merupakan data anime yang berasal dari [MyAnimeList.net](https://myanimelist.net/) pada laman [Kaggle](https://www.kaggle.com/datasets/timnosov/anime-recommendations-database-clean/). Dataset tersebut berisikan 2 file csv, yaitu file *Anime* dan *Rating*. File `anime.csv` yang terdiri dari 7 kolom dan 10228 baris, Sedangkan file `rating_.csv` terdiri dari 3 kolom dan 7813737 baris. 

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
3.   `rating`: anime yang telah dinilai oleh pengguna ini, _rating_ dari 10 pengguna ini telah ditetapkan (-1 jika pengguna menontonnya tetapi tidak menetapkan peringkat).

Untuk memahami data lebih lanjut, dilakukan **Analisis Univariat** serta **Visualisasi Data**

Analisis Univariat merupakan bentuk analisis data yang hanya merepresentasikan informasi yang terdapat pada satu variabel. Jenis visualisasi ini umumnya digunakan untuk memberikan gambaran terkait distribusi sebuah variabel dalam suatu dataset. Sebagai alat bantu analisis, dilakukan teknik Visualisasi Data. Memvisualisasikan data memberikan wawasan mendalam tentang perilaku berbagai fitur-fitur yang tersedia dalam dataset.

Berikut adalah hasil *Exploratory Data Analysis* (EDA) menggunakan Analisis Univariat:

<p align="center">
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/1-top-komunitas-anime.png" />
  <br>
  Gambar 2. Top Komunitas Anime
</p>

💡 _Insights_:

Death Note memiliki anggota komunitas tertinggi diikuti oleh Shingeki no Kyojin dan Sword Art Online.

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/2-distribusi-kategori-anime.png" />
  <br>
  Gambar 3. Distribusi Kategori Anime
</p>

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/3-top-kategori-anime.png" />
  <br>
  Gambar 4. Top Kategori Anime
</p>

💡 _Insights_:

- Ada 3430 anime atau 33.54% dari total anime yang disiarkan di TV.
- Sebanyak 2219 anime atau 21.7% dari total anime disiarkan sebagai film.
- Terdapat 1936 anime atau 18.93% dari total anime yang disiarkan sebagai OVA. Hal tersebut lebih banyak dari ONA yang mencakup 633 anime atau 6.19% dari total anime.

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/4-top-anime-rating.png" />
  <br>
  Gambar 5. Top Rating Anime
</p>

💡 _Insights_:

Taka no Tsume 8 memiliki rating tertinggi diikuti oleh Spoon-hime no Swing Kitchen dan Mogura no Motoro.

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/5-distribusi-rating-anime.png" />
  <br>
  Gambar 6. Distribusi Rating Anime dan Distribusi Rating Anime yang Diberikan Oleh User
</p>

💡 _Insights_:

- Sebagian besar rating Anime tersebar antara 5.5 - 8.0
- Sebagian besar rating pengguna tersebar antara 6.0 - 10.0
- Modus dari distribusi rating pengguna berada di sekitar 8.0
- Rating user bernilai -1 merupakan outliers dalam rating pengguna yang dapat diabaikan

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/6-top-genre.png" />
  <br>
  Gambar 7. Top Genre Anime
</p>

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/6-wordcloud-genre.png" />
  <br>
  Gambar 8. Wordcloud Genre
</p>

💡 _Insights_:

Terdapat 39 genre dengan genre Comedy memiliki jumlah terbanyak diikuti oleh genre Action dan Adventure

## Data Preparation
Dalam _data preparation_, prinsip **"_garbage in, garbage out_"** berlaku. Artinya, jika data yang digunakan untuk melatih model tidak berkualitas baik, maka hasil prediksi dari model tersebut juga akan tidak akurat atau tidak dapat diandalkan. Dengan memastikan data yang digunakan untuk melatih model memiliki kualitas yang baik, model yang dihasilkan dapat lebih andal dalam merekomendasikan anime.

Proses _data preparation_ meliputi beberapa tahap:

- **_Data Cleaning_**

  Tahap awal adalah membersihkan data untuk menangani nilai yang hilang, outlier, dan duplikat. Selain itu, dilakukan pembersihan teks jika diperlukan, seperti menghilangkan karakter tidak diperlukan dalam judul anime. Dengan demikian, kebersihan data terjaga untuk analisis lebih lanjut.

- **_Feature extraction_ menggunakan TfidfVectorizer**

  Dalam langkah ini, alat TfidfVectorizer digunakan untuk mengonversi teks atau data mentah menjadi representasi numerik dalam bentuk matriks fitur TF-IDF. Penggunaan TfidfVectorizer pada kasus ini membantu mengubah nilai-nilai dalam kolom tertentu menjadi vektor, yang akan digunakan dalam proses perhitungan _cosine similarity_.

- **_Scaling_**

  Pada tahap ini, dilakukan proses _scaling_ menggunakan metode `MinMaxScaler` secara manual. Proses _scaling_ ini bertujuan untuk menormalkan skala data terutama pada data numerik. _scaling_ tersebut diterapkan dalam persiapan data untuk pengembangan model dengan _Collaborative Filtering_.

- **Pembagian Dataset menjadi _Data Train_ dan _Data Validation_**

  Tahap selanjutnya adalah membagi dataset menjadi dua bagian: data latih dan data validasi. Pembagian ini dilakukan dengan tujuan untuk melatih dan mengevaluasi kinerja model yang akan dikembangkan. Dalam proyek ini, sebanyak 80% dari dataset digunakan untuk melatih model, sementara 20% sisanya disisihkan untuk mengevaluasi model.

## Modeling

Untuk tahap pemodelan, digunakan dua algoritma, yakni _Content Based Filtering_ dan _Collaborative Filtering_. Berikut adalah gambaran ringkas tentang kedua algoritma tersebut:

### 1. _Content Based Filtering_

_Content Based Filtering_ adalah salah satu pendekatan dalam sistem rekomendasi dimana rekomendasi diberikan berdasarkan karakteristik atau konten dari item yang sudah ada. Dalam konteks sistem rekomendasi anime, algoritma ini menganalisis atribut-atribut dari setiap anime, seperti genre, kategori, dan _rating_, untuk menghasilkan rekomendasi kepada pengguna.

Langkah-langkah dalam membangun model sebagai berikut:

1. Memulai proses pengembangan dengan melakukan ekstraksi fitur dari teks menggunakan TfidfVectorizer yang disediakan oleh library sklearn.feature_extraction.text.
2. Mengonversi vektor TF-IDF yang dihasilkan menjadi bentuk matriks menggunakan metode `todense()`.
3. Membuat dataframe untuk menampilkan matriks TF-IDF, dengan kolom yang mewakili genre dan baris yang mewakili judul.
4. Menghitung kemiripan kosinus antar dokumen pada matriks TF-IDF menggunakan fungsi `cosine_similarity()`.
5. Membuat dataframe dari hasil perhitungan kemiripan kosinus, di mana judul anime menjadi baris dan kolom.
6. Membuat fungsi `rekomendasi_anime` yang akan merekomendasikan anime berdasarkan kemiripan yang ada dalam dataframe tersebut.

`def rekomendasi_anime(title, similarity_data=cosine_sim_df, items=data_genre[['name', 'genre', 'type']], k=5)`

     Parameter:
     - `title`: tipe data string (str) judul anime (index kemiripan dataframe)
     - `similarity_data` : tipe data pd.DataFrame (object) kesamaan dataframe, simetrik, dengan anime sebagai indeks dan kolom
     - `items` : tipe data pd.DataFrame (object) mengandung kedua nama dan fitur lainnya yang digunakan untuk mendefinisikan kemiripan
     - `k` : tipe data integer (int) Banyaknya jumlah rekomendasi yang diberikan

Contoh seseorang yang telah menonton anime 'Naruto: Shippuuden'. Ia suka dengan film anime tersebut. Lalu ia ingin mencari anime yang secara cerita dan alur mirip dengan 'Naruto: Shippuuden'

<p align="center">
    <br>
    <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/naruto.gif"/>
    <br>
    Gambar 9. Naruto
</p>

Maka, sistem akan merekomendasikan anime-anime yang memiliki kesamaan fitur dengan anime 'Naruto: Shippuuden'

|                  title_name                 |                     genre                    |     Type      | Similarity Score |         
|:-------------------------------------------:|:--------------------------------------------:|:-------------:|:----------------:|
|                    Boruto: Naruto the Movie |        Action, Comedy, Martial Arts, Shounen |       Special |              1.0 |
|                                 Naruto x UT |        Action, Comedy, Martial Arts, Shounen |           OVA |              1.0 |
|        Naruto Shippuuden: Sunny Side Battle |        Action, Comedy, Martial Arts, Shounen |       Special |              1.0 |
| Naruto: Shippuuden Movie 4 - The Lost Tower |        Action, Comedy, Martial Arts, Shounen |         Movie |              1.0 |
|                                      Naruto |        Action, Comedy, Martial Arts, Shounen |            TV |              1.0 |


Kelebihan dari _Content Based Filtering_ adalah kemampuannya dalam memberikan rekomendasi yang personal dan relevan untuk setiap pengguna berdasarkan preferensi mereka sendiri, serta tidak terlalu terpengaruh oleh _cold start problem_. Namun, kelemahannya adalah kurangnya variasi dalam rekomendasi yang diberikan karena hanya mempertimbangkan item yang memiliki atribut atau fitur yang mirip dengan item yang telah dikonsumsi atau disukai oleh pengguna.

### 2. _Collaborative Filtering_

_Collaborative Filtering_ adalah pendekatan lain dalam sistem rekomendasi dimana rekomendasi diberikan berdasarkan perilaku atau preferensi pengguna serta kelompok pengguna lainnya. Dalam konteks sistem rekomendasi anime, algoritma ini menganalisis perilaku penonton, seperti _rating_ yang diberikan oleh pengguna pada anime tertentu, untuk memberikan rekomendasi kepada pengguna. 

Langkah Langkah dalam membangun model:
1. Melakukan proses encoding angka ke user_id, anime_id ke dalam indeks integer.
2. Mapping user_id ke dataframe user dan Mapping anime_id ke dataframe anime melalui embedding matrix.
3. Mendapatkan jumlah user dan jumlah anime.
4. Mencari nilai minimum rating dan nilai maksimum rating.
5. Mengacak dataset.
6. Membuat variabel x untuk mencocokkan data user dan anime menjadi satu value dan variabel y untuk membuat rating dari hasil.
7. Membagi menjadi 80% data train dan 20% data validasi.
8. Memanggil class RecommenderNet() dari library tf.keras
9. Menginisiasi model RecommenderNet() yang memiliki parameter: num_users, num_anime, embedding_size=50.   
10. Setelah itu model bekerja dengan menghitung skor kecocokan antara user_embbeding dan anime_embbeding melalui operasi perkalian dot product.
11. Lalu menambahkan bias per user dan bias per anime.
12. Proses pencocokan skor(score matching) diskalakan ke interval [0, 1] melalui sigmoid function.
13. Melakukan inisialsisasi model. dengan parameter num_user, num_anime dan embbeding berdimensi 50.
14. Mengcompile model. Pada proses compile, model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation.
15. Melakukan proses training-validate data dan memvisualisasikan hasil dari metrics evaluasi root mean squared error (RMSE) menggunakan library matplotlib.
16. Lalu melakukan prediksi.

`model = RecommenderNet(num_users, num_anime, 128)`

     Parameter:
     - `num_users`: jumlah id user anime
     - `num_anime` : jumlah judul anime
     - `embedding_size` : Melakukan embbeding(penyematan) pada user_id dan anime_id ke dalam vektor 128 dimensi. 

Hasilnya:

    ```
    Showing best anime recommendations for users: 1798

    Anime with high ratings from user:
    Ookami to Koushinryou II : Adventure, Fantasy, Historical, Romance
    Toki wo Kakeru Shoujo : Adventure, Drama, Romance, Sci-Fi
    Angel Beats! : Action, Comedy, Drama, School, Supernatural
    Ookami to Koushinryou : Adventure, Fantasy, Historical, Romance
    Kill la Kill : Action, Comedy, School, Super Power

    Top 10 Anime recommendation:
    Kimi no Na wa. : Drama, Romance, School, Supernatural
    Fullmetal Alchemist: Brotherhood : Action, Adventure, Drama, Fantasy, Magic, Military, Shounen
    Gintama° : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Steins;Gate : Sci-Fi, Thriller
    Gintama : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Hunter x Hunter (2011) : Action, Adventure, Shounen, Super Power
    Ginga Eiyuu Densetsu : Drama, Military, Sci-Fi, Space
    Gintama Movie: Kanketsu-hen - Yorozuya yo Eien Nare : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Gintama: Enchousen : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Koe no Katachi : Drama, School, Shounen
    ```

Sebagai contoh, hasil di atas adalah rekomendasi untuk user dengan id 1798. Dari output tersebut, kita dapat membandingkan antara _Anime with high ratings_ from user dan _Top 10 Anime recommendation_ untuk user.

Kelebihan dari _Collaborative Filtering_ adalah kemampuannya dalam memberikan rekomendasi yang beragam dan dapat menangani _cold start problem_ dengan baik. Namun, kelemahannya adalah kerentanan terhadap _sparsity data_ dan kebutuhan akan jumlah data yang besar untuk memberikan rekomendasi yang akurat.

### Result

## Evaluation
### Metrik Evaluasi

#### 1. _Cosine similarity_

_Cosine similarity_ mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai _cosine similarity_. _Cosine Similarity_ dituliskan dalam rumusan berikut

$$ Cosine Similarity (A, B) = (A · B) / (||A|| * ||B||) $$ 

dimana: 
- (A·B)menyatakan produk titik dari vektor A dan B.
- ||A|| mewakili norma Euclidean (magnitudo) dari vektor A.
- ||B|| mewakili norma Euclidean (magnitudo) dari vektor B.

Keuntungan dari _cosine similarity_ adalah kemampuannya untuk mengukur kesamaan antara dua objek data berdasarkan sudut antara vektor yang mewakilinya, bukan jarak Euclidean di antara mereka. Hal ini bermanfaat karena walaupun dua objek data memiliki ukuran yang berbeda-beda dan terpisah jauh di ruang multidimensi, mereka masih bisa dianggap mirip jika sudut antara vektor mereka kecil. Dengan demikian, _cosine similarity_ mampu menangkap orientasi atau arah dari objek data, yang merupakan informasi yang penting dalam analisis dan pengelompokan data.

Berikut merupakan contoh _Matrix Cosine Similarity_:

|       **name**                                     | Cossette no Shouzou | Sekai Meisaku Douwa: Wow! Maerchen Oukoku | Wonderful Days | Kitte no Gensou | 
|----------------------------------------------------|---------------------|-------------------------------------------|----------------|-----------------|
| Inazuma Eleven                                     | 0.000000            | 0.0                                       | 0.000000       | 0.000000        |
| World Trigger                                      | 0.179823            | 0.0                                       | 0.457044       | 0.000000        |
| Bulg-eunmae                                        | 0.000000            | 0.0                                       | 0.000000       | 0.000000        |
| Higurashi no Naku Koro ni Special: Nekogoroshi-hen | 0.000000            | 0.0                                       | 0.000000       | 0.427819        |
| Giga Tribe                                         | 0.000000            | 0.0                                       | 0.000000       | 0.236277        |

Pada perhitungan _cosine similarity_, skor kesamaan berkisar dari 0 hingga 1, dengan 0 sebagai yang terendah (paling tidak mirip) dan 1 sebagai yang tertinggi (paling mirip).

#### 2. _Root Mean Squared Error_

_Root Mean Squared Error_ (RMSE) adalah metode evaluasi yang umum digunakan dalam _collaborative filtering_ untuk mengukur seberapa akurat model dalam memprediksi peringkat atau preferensi pengguna terhadap item tertentu. RMSE menghitung akar dari rata-rata kuadrat selisih antara nilai sebenarnya dengan nilai prediksi.

Rumus RMSE:

RMSE = sqrt(Σ(actual_rating - predicted_rating)^2 / n)

dimana:
- `actual_rating` adalah nilai peringkat yang sebenarnya oleh pengguna.
- `predicted_rating` adalah nilai peringkat yang diprediksi oleh model.
- `n` adalah jumlah pengukuran.

RMSE memiliki keuntungan dalam evaluasi model _collaborative filtering_ karena memberikan gambaran yang jelas tentang seberapa akurat model dalam memprediksi preferensi pengguna terhadap item. Nilai RMSE yang lebih rendah menunjukkan tingkat akurasi yang lebih tinggi. Selain itu, interpretasinya yang mudah dimengerti dan konsistensinya dalam menangani _outlier_ atau kesalahan besar membuat RMSE menjadi metode evaluasi yang efektif dan dapat diandalkan dalam pengembangan model rekomendasi.

Berikut merupakan hasil dari _Root Mean Squared Error_ dari model dengan _Collaborative Filtering:_

<p align="center">
  <br>
  <img src="https://raw.githubusercontent.com/syahvan/anime-recommender-system/main/img/rmse.png" />
  <br>
  Gambar 10. Grafik Root Mean Squared Error dari model dengan Collaborative Filtering
</p>

Dari grafik tersebut, terlihat bahwa nilai error akhir sebesar sekitar 0.13 dan error pada data validasi sebesar 0.13 pula. Nilai tersebut cukup bagus untuk sistem rekomendasi. Selain itu, nilai tersebut juga menandakan bahwa model tidak _overfitting_.

## Conclusion

Sistem rekomendasi ini dirancang untuk mempermudah pengguna dalam menemukan anime sesuai dengan minat mereka. Untuk pengguna baru yang belum memiliki riwayat menonton anime, sistem rekomendasi menggunakan _collaborative filtering_ dapat digunakan untuk merekomendasikan anime berdasarkan rating yang diberikan oleh pengguna lain. Sedangkan untuk pengguna yang telah memiliki riwayat menonton anime, sistem rekomendasi menggunakan _content-based filtering_ dapat digunakan untuk membantu mereka memilih anime berdasarkan genre atau plot yang mirip dengan anime yang telah mereka tonton sebelumnya.

## References

[1] Nuurshadieq and A. T. Wibowo, "Leveraging Side Information to Anime Recommender System using Deep learning," 2020 3rd International Seminar on Research of Information Technology and Intelligent Systems (ISRITI), Yogyakarta, Indonesia, 2020, pp. 62-67, doi: 10.1109/ISRITI51436.2020.9315363.

[2] S. Ota, H. Kawata, M. Muta, S. Masuko, dan J. Hoshino, "AniReco: Japanese Anime Recommendation System," dalam Entertainment Computing – ICEC 2017, N. Munekata, I. Kunita, dan J. Hoshino, Eds. Cham: Springer, 2017, jld. 10507. https://doi.org/10.1007/978-3-319-66715-7_49.

[3] F. Ricci, L. Rokach, dan B. Shapira, "Introduction to Recommender Systems Handbook," dalam Recommender Systems Handbook, F. Ricci, L. Rokach, B. Shapira, dan P. Kantor, Eds. Boston, MA: Springer, 2011. https://doi.org/10.1007/978-0-387-85820-3_1.
