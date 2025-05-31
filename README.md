# Laporan Proyek Machine Learning - Jocelyn Nathaniel Patricktan 

## Project Overview

Film adalah salah satu media komunikasi modern efektif yang berbentuk audio visual dan sifatnya sangat kompleks di mana mampu menuangkan gagasan dalam bentuk gambar hidup sekaligus menjadi informasi yang dapat menjadi alat penghibur, politik, propaganda, sarana rekreasi, serta edukasi yang dapat dinikmati oleh masyarakat luas. Film dapat disebut sebagai sinema atau gambar hidup yang diartikan sebagai karya seni yang lahir dari proses tuntutan kebebasan kreativitas dan merupakan bentuk populer dari hiburan, produksi industri, maupun barang bisnis. Film biasanya dikategorikan menurut genrenya di mana sebuah film dapat memiliki lebih dari satu genre. Terdapat beberapa macam genre yang dikenal oleh masyarakat luas seperti action, adventure, horror, komedi, thriller, romance, dan masih banyak lagi [1]. Perkembangan film terutama di era digital saat ini mulai berkembang dengan cepat seiring dengan munculnya berbagai macam film yang mana hal tersebut menjadi alasan mengapa sulit bagi masyarakat luas atau pengguna dalam mencari suatu film yang sesuai dengan minat mereka. Hal tersebut dapat diatasi dengan membuat model sistem rekomendasi untuk sistem pada film. Sistem rekomendasi merupakan sebuah sistem yang memprediksi rating atau preferensi pengguna terhadap suatu item tertentu. Rekomendasi tersebut dibuat berdasarkan perilaku pengguna di masa lalu atau perilaku pengguna lainnya sehingga sistem tersebut akan merekomendasikan sesuatu berdasarkan data perilaku atau preferensi dari waktu ke waktu pengguna. Satu hal penting yang perlu diketahui mengenai sistem rekomendasi adalah sistem tersebut tidak merekomendasikan secara spesifik di mana hanya merekomendasikan sejumlah item yang mungkin cocok dengan preferensi pengguna sehingga keluaran dari sistem rekomendasi berupa top-N recommendation yang berarti mesin memberikan sejumlah rekomendasi dengan peringkat teratas sesuai dengan preferensi masing-masing pengguna [2]. Dengan adanya sistem rekomendasi, maka pengguna dapat menelusuri informasi apa saja yang ingin dicari sehingga tidak kewalahan dengan berbagai informasi yang bertebaran di mana-mana. Pada proyek ini akan dilakukan pembangunan model sistem rekomendasi film berdasarkan dataset Movie Recommendation System di Kaggle untuk memberikan daftar rekomendasi film apa saja yang relevan dengan minat atau preferensi pengguna. 

[1] C. Nugraha, I. F. Astuti, and A. H. Kridalaksana, "Movie Organizer Menggunakan Teknik Web Scrapping", Jurnal Informatika Mulawarman, vol. 9, no. 3, pp. 56-61, Oktober 2014. 

[2] F. Kane, "Building Recommender Systems with Machine Learning and AI", O'Reilly, Januari 2021.


## Business Understanding

### Problem Statements

- Bagaimana membuat sistem rekomendasi yang relevan dengan minat pengguna dengan teknik content-based filtering berdasarkan dataset Movie Recommendation System?
- Bagaimana sistem rekomendasi dapat mengukur tingkat relevansi rekomendasi terhadap pengguna berdasarkan metrik evaluasi presisi sistem rekomendasi? 

### Goals

- Menghasilkan sejumlah rekomendasi film berdasarkan judul dan katergori film terhadap minat pengguna dengan menggunakan teknik content-based filtering.
- Mengevaluasi performa sistem rekomendasi menggunakan metrik evaluasi presisi sistem rekomendasi. 

### Solution Statements 

- Membangun model sistem rekomendasi berbasis konten dengan mengekstrak fitur-fitur dari file dataset film, kemudian mengubah fitur tertentu menjadi representasi vektor dengan menggunakan TF-IDF serta menghitung tingkat kemiripan fitur tertentu dengan menggunakan cosine similarity.
- Melakukan evaluasi kerja sistem rekomendasi dengan menggunakan metrik presisi untuk mengetahui seberapa relevan dan akurat rekomendasi yang dihasilkan terhadap minat pengguna. 


## Data Understanding

Pada proyek membangun model sistem rekomendasi ini akan menggunakan Movie Recommendation System Dataset yang memiliki 2 file dataset terpisah yang masing-masing berisi informasi tentang film dan rating. Dataset ini dimiliki oleh Manas Parashar yang tersedia secara publik untuk keperluan riset dan edukasi bagi siapa pun terutama untuk membuat sistem rekomendasi. Dataset movies memiliki 62423 entri dengan 3 kolom varibel berupa 'movieId', 'title', dan 'genres' yang menunjukkan lebih dari 62 ribu jenis film dalam bentuk judul dan kategori sedangkan dataset ratings memiliki 25000095 entri dengan 4 kolom variabel berupa 'userId', 'movieId', 'rating', dan 'timestamp' yang menunjukkan lebih dari 25 juta pengguna dalam bentuk ulasan. 

Berikut merupakan tautan dataset yang diunduh dari Kaggle: [Movie Recommendation System](https://www.kaggle.com/datasets/parasharmanas/movie-recommendation-system)

Variabel-variabel pada Movie Recommendation System dataset adalah sebagai berikut:

- movieId: merupakan tanda pengenal unik untuk setiap film.  
- title: merupakan judul film yang sesuai dengan tanda pengenal unik film. 
- genres: merupakan kategori film. 
- userId: merupakan tanda pengenal unik pengguna. 
- rating: merupakan nilai rating pengguna terhadap film dengan skala 0.5 hingga 5.0. 
- timestamp: merupakan waktu ketika pengguna memberikan ulasan.

Berikut merupakan tahapan yang dilakukan pada Data Understanding: 
- Memuat dataset Movies dan Ratings dengan penjelasan jumlah masing-masing data serta penjelasan kolom variabel telah dijelaskan di atas. 
- Melakukan Univariate Exploratory Data Analysis yang memuat deskripsi variabel dan univariate analysis.

Deskripsi Variabel: 
- Yang dilakukan adalah memuat informasi dataset movies dan ratings, memuat deskripsi statistik dataset movies dan ratings, memeriksa duplikasi data pada dataset movies dan ratings, serta memeriksa missing value pada dataset movies dan ratings.
- Berdasarkan hasil pada deskripsi variabel, didapatkan informasi bahwa terdapat dua tipe data, yaitu numerikal dan kategorikal di mana untuk variabel numerik terletak pada kolom variabel 'movieId', 'userId', 'rating', dan 'timestamp' sedangkan variabel kategorik terletak pada kolom variabel 'title' dan 'genres'.
- Berdasarkan hasil pada pemeriksaan dupliksasi data , tidak terdapat data duplikat sehingga tidak perlu melakukan penanganan duplikasi data. Hal tersebut menunjukkan bahwa setiap entri data memiliki sifat unik serta tidak mengulangi informasi yang sama. 
- Berdasarkan hasil pada pemeriksaan missing value dan jumlah entri informasi dataset, tidak terdapat missing value sehingga tidak perlu melakukan penanganan missing value. Hal tersebut menunjukkan bahwa setiap entri data telah terisi dengan baik.
- Berdasarkan hasil pada deskripsi statistik dataset, didapatkan bahwa nilai minimum rating sebesar 0.5 sedangkan nilai maksimum rating sebesar 5.0 dengan nilai rata-rata sebesar 3.53 atau kalau dibulatkan ke atas menjadi 3.6 yang berarti pengguna cenderung memberikan ulasan yang cukup tinggi. 

Univariate Analysis: 
- Yang dilakukan adalah memeriksa berapa banyak 


## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

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
