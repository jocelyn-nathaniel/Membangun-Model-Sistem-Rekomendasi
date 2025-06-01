# Laporan Proyek Machine Learning - Jocelyn Nathaniel Patricktan 

## Project Overview

Film adalah salah satu media komunikasi modern efektif yang berbentuk audio visual dan sifatnya sangat kompleks di mana mampu menuangkan gagasan dalam bentuk gambar hidup sekaligus menjadi informasi yang dapat menjadi alat penghibur, politik, propaganda, sarana rekreasi, serta edukasi yang dapat dinikmati oleh masyarakat luas. Film dapat disebut sebagai sinema atau gambar hidup yang diartikan sebagai karya seni yang lahir dari proses tuntutan kebebasan kreativitas dan merupakan bentuk populer dari hiburan, produksi industri, maupun barang bisnis. Film biasanya dikategorikan menurut genrenya di mana sebuah film dapat memiliki lebih dari satu genre. Terdapat beberapa macam genre yang dikenal oleh masyarakat luas seperti action, adventure, horror, komedi, thriller, romance, dan masih banyak lagi [1]. Perkembangan film terutama di era digital saat ini mulai berkembang dengan cepat seiring dengan munculnya berbagai macam film yang mana hal tersebut menjadi alasan mengapa sulit bagi masyarakat luas atau pengguna dalam mencari suatu film yang sesuai dengan minat mereka. Hal tersebut dapat diatasi dengan membuat model sistem rekomendasi untuk sistem pada film. Sistem rekomendasi merupakan sebuah sistem yang memprediksi rating atau preferensi pengguna terhadap suatu item tertentu. Rekomendasi tersebut dibuat berdasarkan perilaku pengguna di masa lalu atau perilaku pengguna lainnya sehingga sistem tersebut akan merekomendasikan sesuatu berdasarkan data perilaku atau preferensi dari waktu ke waktu pengguna. Satu hal penting yang perlu diketahui mengenai sistem rekomendasi adalah sistem tersebut tidak merekomendasikan secara spesifik di mana hanya merekomendasikan sejumlah item yang mungkin cocok dengan preferensi pengguna sehingga keluaran dari sistem rekomendasi berupa top-N recommendation yang berarti mesin memberikan sejumlah rekomendasi dengan peringkat teratas sesuai dengan preferensi masing-masing pengguna [2]. Dengan adanya sistem rekomendasi, maka pengguna dapat menelusuri informasi apa saja yang ingin dicari sehingga tidak kewalahan dengan berbagai informasi yang bertebaran di mana-mana. Pada proyek ini akan dilakukan pembangunan model sistem rekomendasi film berdasarkan dataset Movie Recommendation System di Kaggle untuk memberikan daftar rekomendasi film apa saja yang relevan dengan minat atau preferensi pengguna. 

[1] C. Nugraha, I. F. Astuti, and A. H. Kridalaksana, "Movie Organizer Menggunakan Teknik Web Scrapping", Jurnal Informatika Mulawarman, vol. 9, no. 3, pp. 56-61, Oktober 2014. 

[2] F. Kane, "Building Recommender Systems with Machine Learning and AI", O'Reilly, Januari 2021.


## Business Understanding

### Problem Statements

- Bagaimana membuat sistem rekomendasi yang relevan dengan minat pengguna dengan teknik content-based filtering berdasarkan dataset Movie Recommendation System?
- Bagaimana sistem rekomendasi dapat mengukur tingkat relevansi rekomendasi film terhadap pengguna berdasarkan metrik evaluasi presisi sistem rekomendasi? 

### Goals

- Menghasilkan sejumlah rekomendasi film berdasarkan judul dan katergori film terhadap minat pengguna dengan menggunakan teknik content-based filtering.
- Mengevaluasi performa sistem rekomendasi film menggunakan metrik evaluasi presisi sistem rekomendasi. 

### Solution Statements 

- Membangun model sistem rekomendasi film berbasis konten dengan mengekstrak fitur-fitur dari file dataset, kemudian mengubah fitur tertentu menjadi representasi vektor dengan menggunakan TF-IDF serta menghitung tingkat kemiripan fitur tertentu dengan menggunakan cosine similarity.
- Melakukan evaluasi kerja sistem rekomendasi film dengan menggunakan metrik presisi untuk mengetahui seberapa relevan dan akurat rekomendasi yang dihasilkan terhadap minat pengguna. 


## Data Understanding

Pada proyek membangun model sistem rekomendasi ini akan menggunakan Movie Recommendation System Dataset yang memiliki 2 file dataset terpisah yang masing-masing berisi informasi tentang film dan rating. Dataset ini dimiliki oleh Manas Parashar yang tersedia secara publik untuk keperluan riset dan edukasi bagi siapa pun terutama untuk membuat sistem rekomendasi. Dataset movies memiliki 62423 entri dengan 3 kolom variabel berupa 'movieId', 'title', dan 'genres' yang menunjukkan lebih dari 62 ribu jenis film dalam bentuk judul dan kategori sedangkan dataset ratings memiliki 25000095 entri dengan 4 kolom variabel berupa 'userId', 'movieId', 'rating', dan 'timestamp' yang menunjukkan lebih dari 25 juta pengguna dalam bentuk ulasan. 

Dataset Movies: 

![image](https://github.com/user-attachments/assets/bc697409-aa9d-4432-ab47-0f96b267e1b2)

Dataset Ratings: 

![image](https://github.com/user-attachments/assets/a02ab199-281f-4eaa-a995-cae44e12809f)

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

Duplikasi Data pada Dataset Movies: 

![image](https://github.com/user-attachments/assets/7ce5344d-5ca1-4a7d-b397-c29e6cbadafe)

Duplikasi Data pada Dataset Ratings: 

![image](https://github.com/user-attachments/assets/dbc31280-863e-4795-a772-8b312e6788c9)

- Berdasarkan hasil pada pemeriksaan missing value dan jumlah entri informasi dataset, tidak terdapat missing value sehingga tidak perlu melakukan penanganan missing value. Hal tersebut menunjukkan bahwa setiap entri data telah terisi dengan baik.

Informasi Dataset Movies: 

![image](https://github.com/user-attachments/assets/e38bb206-f966-4054-8f06-684e165de966)

Informasi Dataset Ratings: 

![image](https://github.com/user-attachments/assets/fa1c8a85-72ab-4787-afab-5a5c382c24bc)

Missing Values Dataset Movies: 

![image](https://github.com/user-attachments/assets/ff42c357-c636-4a4d-9a80-9ad3ae20d3e5)

Missing Values Dataset Ratings: 

![image](https://github.com/user-attachments/assets/f522d2d0-3a6b-4846-8d86-d832f6dcaae1)

- Berdasarkan hasil pada deskripsi statistik dataset ratings, didapatkan bahwa nilai minimum rating sebesar 0.5 sedangkan nilai maksimum rating sebesar 5.0 dengan nilai rata-rata sebesar 3.53 atau kalau dibulatkan ke atas menjadi 3.6 yang berarti pengguna cenderung memberikan ulasan yang cukup tinggi.

![image](https://github.com/user-attachments/assets/4724ca51-d898-46c6-bf45-eef4006a2024)

Univariate Analysis: 
- Yang dilakukan adalah memeriksa berapa banyak pengguna berdasarkan kolom variabel 'userId', memeriksa berapa banyak entri unik film berdasarkan 'movieId' dan 'title', memeriksa 15 contoh judul film berdasarkan 'title', memeriksa jumlah masing-masing rating berdasarkan 'rating', visualisasi distribusi rating berdasarkan 'rating', serta memeriksa berapa banyak genre berdasarkan 'genres' dan memeriksa genre apa aja yang tertera.
- Berdasarkan hasil pada univariate analysis, didapatkan bahwa dataset memiliki 162541 pengguna, 62423 film dan 62325 judul film yang menunjukkan terdapat sedikit variasi dalam penamaan pada judul film, serta tertera juga beberapa contoh judul film seperti 'Toy Story (1995)', 'Jumanji (1995)', 'Grumpier Old Men (1995)', 'Waiting to Exhale (1995)', 'Father of the Bride Part II (1995)', 'Heat (1995)', 'Sabrina (1995)', 'Tom and Huck (1995)', 'Sudden Death (1995)', 'GoldenEye (1995)', 'American President, The (1995)', 'Dracula: Dead and Loving It (1995)', 'Balto (1995)', 'Nixon (1995)', dan 'Cutthroat Island (1995)'.

![image](https://github.com/user-attachments/assets/5e9afcfc-3276-43cf-8a1a-e5975492b3d6)

![image](https://github.com/user-attachments/assets/d168e3ae-3b95-4c87-93ee-e209bdbaf399)

- Berdasarkan pemeriksaan jumlah masing-masing rating dan visualisasi distribusi rating, didapatkan bahwa rating memiliki skala antara 0.5 hingga 5.0 dengan interval 0.5 yang menunjukkan bahwa rating memiliki penilaian setengah. Didapatkan juga rating 4.0 merupakan rating tertinggi di mana mendominasi secara signifikan dengan lebih dari 6 juta ulasan.

![image](https://github.com/user-attachments/assets/f41b38fd-a0b8-4d94-8e6e-66f85a0ee982)

![image](https://github.com/user-attachments/assets/114a6ce5-bc20-4432-b829-813440b46f69)

- Berdasarkan pemeriksaan genre, didapatkan genre memiliki 20 kategori termasuk dengan data yang belum lengkap di bagian genre seperti (no genres listed), Action, Adventure, Animation, Children, Comedy, Crime, Documentary, Drama, Fantasy, Film-Noir, Horror, IMAX, Musical, Mystery, Romance, Sci-Fi, Thriller, War, dan Western. 


## Data Preparation

Sebelum melakukan data preparation, akan dilakukan satu tahapan berupa data preprocessing di mana melakukan penggabungan kedua file movies dan ratings menjadi satu kesatuan yang utuh sehingga dapat digunakan untuk tahap selanjutnya. 

![image](https://github.com/user-attachments/assets/e306b4c6-ea72-456b-a0c5-6d3a71673247)

![image](https://github.com/user-attachments/assets/8f67bbf6-a815-4766-9e75-7074ec9ae233)

Berdasarkan hasil data preprocessing di atas, didapatkan bahwa dataset telah berhasil digabung menjadi satu kesatuan dengan memiliki 25000095 baris jumlah pengamatan dan 6 kolom variabel berupa 'userId', 'movieId', 'rating', 'timestamp', 'title', dan 'genres'. Setelah data preprocessing, maka akan dilanjutkan dengan tahap data preparation. 

Sebelum membangun model sistem rekomendasi, diperlukan beberapa tahap penting untuk memastikan sekaligus mempersiapkan data yang digunakan telah bersih, konsisten, dan dalam bentuk yang sesuai untuk melakukan proses pemodelan. Ada beberapa teknik yang akan dilakukan pada data preparation ini seperti menghapus kolom variabel 'timestamp', memeriksa dan menangani missing value, memeriksa dan menangani duplikasi data, melakukan sampling pada dataset, membuat DataFrame baru mengenai fitur film, mengubah kategori film menjadi representasi vektor TF-IDF, serta menghitung tingkat kemiripan dengan cosine similarity. 

Pada awal tahap preparation, dilakukan penghapusan kolom variabel 'timestamp' karena tidak memiliki informasi yang relevan untuk pemodelan dengan content-based filtering. 

![image](https://github.com/user-attachments/assets/988e31c4-ad64-48d7-a044-76c7bcdf3e12)

![image](https://github.com/user-attachments/assets/a0a9cedf-3539-4be5-9d21-a76a9a227c2b)

Berdasarkan hasil penghapusan kolom variabel 'timestamp', didapatkan data baru dengan 25000095 baris jumlah pengamatan dengan 5 kolom variabel berupa 'userId', 'movieId', 'rating', 'title', dan 'genres'. 

Selanjutnya, akan dilakukan pemeriksaan missing values di mana berdasarkan hasil entries pada informasi dan pemeriksaan missing value pada masing-masing file dataset di data understanding, didapatkan bahwa tidak terdapat missing values tetapi untuk memastikan maka akan dilakukan pemeriksaan missing values tetapi menggunakan dataset terbaru pada data preprocessing yang kolom variabel 'timestamp' telah dihapus. 

![image](https://github.com/user-attachments/assets/ddda5d3f-da43-4434-98e6-0ff452305f6a)

![image](https://github.com/user-attachments/assets/48a7e690-0880-4053-9e5f-a612539bc732)

Berdasarkan hasil pemeriksaan missing values dataset gabungan, didapatkan informasi bahwa tidak terdapat missing values sehingga tidak akan dilakukan penanganan missing values. 

Selanjutnya, akan dilakukan pemeriksaan duplikasi data di mana berdasarkan pemeriksaan duplikasi data pada masing-masing file dataset di data understanding, didapatkan bahwa tidak terdapat duplikasi data tetapi untuk memastikan maka akan dilakukan pemeriksaan duplikasi data tetapi menggunakan dataset terbaru pada data preprocessing yang kolom variabel 'timestamp' telah dihapus. 

![image](https://github.com/user-attachments/assets/04f8e399-b27e-4824-9e5f-c9af35f23167)

![image](https://github.com/user-attachments/assets/3493a3d8-eec7-4fed-9916-852169732301)

Berdasarkan hasil pemeriksaan duplikasi data dataset gabungan, didapatkan informasi bahwa tidak terdapat duplikasi data sehingga tidak akan dilakukan penanganan duplikasi data. 

Selanjutnya, akan dilakukan sampling pada dataset. Pada dataset gabungan, didapatkan informasi bahwa terdapat 25000095 yang berarti dataset tersebut memiliki ukuran yang cukup besar. Dengan dilakukan pengambilan sampel acak ini maka diharapkan tahapan selanjutnya dapat berjalan dengan lebih efisien karena telah dilakukan pengurangan data. Pengambilan sampel acak akan dilakukan sebanyak 500000 baris dari dataset dengan pengaturan random_state untuk memastikan hasil sampling sama setiap kali cell dijalankan supaya tetap konsisten pengacakan sampelnya.

![image](https://github.com/user-attachments/assets/a4d20dc9-824a-4033-ad44-c54f07814049)

![image](https://github.com/user-attachments/assets/dc668c21-0591-4258-b209-48432c235bda)

Berdasarkan hasilnya, telah berhasil melakukan sampling pada dataset di data_sampling dengan 500000 baris jumlah pengamatan dan 5 kolom variabel berupa 'userId', 'movieId', 'rating', 'title', dan 'genres'. 

Selanjutnya, akan dilakukan pembuatan DataFrame baru mengenai fitur film. Alasan dilakukan hal ini adalah karena pada tahap pemodelan, teknik yang akan digunakan adalah content-based filtering di mana akan dilakukan rekomendasi berdasarkan konten pada data seperti judul dan kategori film sehingga perlu membuat DataFrame baru yang memuat kolom variabel 'movieId', 'title', dan 'genres'. 

![image](https://github.com/user-attachments/assets/038c333e-9152-4dd9-b690-106d0d9d25e8)

![image](https://github.com/user-attachments/assets/5cb76346-84ff-48f2-97cd-c939fe7e3060)

Berdasarkan hasil pembuatan DataFrame di atas, DataFrame baru berhasil dibuat dengan 18205 baris jumlah pengamatan dengan 3 kolom variabel berupa 'movieId', 'title', dan 'genres'. 

Terakhir, akan dilakukan pengubahan kategori film menjadi representasi fitur penting dengan menggunakan TF-IDF (Term Frequency - Inverse Document Frequency) di mana untuk TF mengukur seberapa sering muncul suatu kata dalam kategori film sedangkan untuk IDF mengurangi bobot kata yang umum muncul di kategori film dan menaikkan bobot kata yang lebih jarang muncul dikarenakan kata-kata yang umum tidak begitu banyak membantu dalam membedakan antara kategori film satu dengan kategori film yang lain. Setiap kategori film akan direpresentasikan sebagai vektor fitur angka di mana setiap dimensi menunjukkan bobot penting pada kata tertentu sehingga vektor-vektor tersebut nantinya akan digunakan untuk menghitung kemiripan antar kategori film menggunakan cosine similarity. Cosine similarity merupakan cara untuk menghitung tingkat kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. 

![image](https://github.com/user-attachments/assets/66f031c0-77d0-4e3c-95de-b9b3edaa56f3)

Metrik cosine similarity sering digunakan untuk mengukur kesamaan dokumen dalam analisis teks seperti kategori film dengan dirumuskan sebagai berikut: 

![image](https://github.com/user-attachments/assets/ca17fb34-054c-48f2-a218-08825628ff2a)

Pada bagian ini, akan dilakukan keduanya. 

![image](https://github.com/user-attachments/assets/3e12f815-6d30-425f-9e4e-9e24e19bc4f8)

![image](https://github.com/user-attachments/assets/4cbfecc0-7d69-43dc-9b2d-d8798be52192)

![image](https://github.com/user-attachments/assets/493c5214-973f-460c-9b15-2a091877a0e6)

![image](https://github.com/user-attachments/assets/63b346fa-64ee-4c04-b720-793c4add8398)

![image](https://github.com/user-attachments/assets/1d16e105-350e-4d7c-985a-409f2a6f35a9)

![image](https://github.com/user-attachments/assets/253ec380-7533-4f10-a122-d18dd0a59e70)

Berdasarkan hasil TF-IDF di atas, didapatkan bahwa kategori film telah berhasil diubah menjadi representasi vektor TF-IDF dengan token yang diambil berupa pola \b\w+\b yang berarti setiap kata dianggap sebagai satu token sehingga dihasilkan 24 fitur unik kategori film seperti 'action', 'adventure', 'animation', 'children', 'comedy', dan sebagainya sebagaimana tertera di atas dengan ukuran matriks (18205, 24) yang berarti terdapat 18205 film dan masing-masing direpresentasikan dalam 24 dimensi kategori film yang berbeda. Lalu, berhasil melakukan perhitungan cosine similarity dengan hasil matriks (18205, 18205) yang menyimpan nilai kemiripan antara kategori film untuk memungkinkan sistem menghasilkan rekomendasi film yang kontennya mirip dengan minat pengguna. 


## Modeling

Pada proyek ini, teknik yang akan digunakan untuk menghasilkan rekomendasi film sesuai dengan minat pengguna adalah content-based filtering. Ide dari content-based filtering atau sistem rekomendasi berbasis konten adalah merekomendasikan item yang mirip dengan yang disukai pengguna di masa lalu seperti sistem merekomendasikan film dengan kategori dan judul film. Content-based filtering mempelajari profil minat pada pengguna baru berdasarkan data dari objek yang telah dinilai oleh pengguna. Teknik ini bekerja dengan memberikan saran beberapa item serupa yang pernah disukai pengguna sebelumnya di masa lalu atau yang sedang dilihat di masa ini. Pada bagian ini, akan dibuatkan model sistem rekomendasi berdasarkan kategori film dan berdasarkan judul film. 

![image](https://github.com/user-attachments/assets/6b3a76d6-01bd-4b30-9983-27c858b8d94b)

![image](https://github.com/user-attachments/assets/ad60d556-aba3-454d-a1e5-13bd77d16900)

Kelebihan: 

- Rekomendasi dibuat berdasarkan minat unik pengguna, bukan dari perilaku pengguna lain.
- Tidak bergantung pada data pengguna lain sehingga cocok untuk sistem yang penggunanya tidak terlalu banyak. 
- Fitur-fitur pada data dapat dijelaskan secara logis.
- Cenderung aman dari popularitas semata di mana untuk item yang kurang begitu populer tetapi relevan tetap dapat direkomendasikan. 

Kekurangan: 

- Rekomendasi yang diberikan dapat terlalu sempit karena hanya memberikan saran berupa item serupa dengan yang sudah disukai.
- Item tertentu yang baru tanpa adanya informasi mengenai konten cukup sulit untuk direkomendasikan.
- Kualitas rekomendasi sangat bergantung pada fitur-fitur konten.
- Tidak dapat menangkap kemiripan atau kesamaan minat antar pengguna. 

Setelah teknik sistem rekomendasi tersebut dilakukan, maka akan dievaluasi dengan memunculkan top-N recommendation di mana hasil yang didapat adalah sebagai berikut: 

Evaluasi Model Sistem Rekomendasi Berdasarkan Kategori Film: 

![image](https://github.com/user-attachments/assets/87e79173-64c9-4210-9ca0-c4a9043143ab)

Evaluasi Model Sistem Rekomendasi Berdasarkan Judul Film: 

![image](https://github.com/user-attachments/assets/69aaa6ab-681a-49a3-a760-baad10a95b39)

Berdasarkan hasil top-N recommendation di atas, didapatkan bahwa teknik content-based filtering berhasil membuat model rekomendasi film berdasarkan kategori dan judul film. 


## Evaluation

Metrik evaluasi yang digunakan pada tahapan ini adalah presisi sistem rekomendasi yang menghitung jumlah rekomendasi item yang relevan dibagi dengan jumlah total item yang direkomendasikan. Presisi digunakan untuk mengukur seberapa banyak item yang direkomendasikan benar-benar relevan dengan minat pengguna. Presisi sistem rekomendasi didefinisikan dengan persamaan berikut: 

![image](https://github.com/user-attachments/assets/e9f6322a-97a8-4602-8068-ce6c4d863355)

Presisi tidak dapat dihitung dengan memanggil library pada klasifikasi karena tidak memiliki data target atau label seperti pada supervised learning. Sehingga akan dilakukan perhitungan presisi dengan melihat pada kategori item yang direkomendasikan berupa kategori yang direkomendasikan relevan/mirip dengan kategori yang dipilih atau tidak. 

![image](https://github.com/user-attachments/assets/f5649a99-c4bb-41a5-bcc2-49be5c09d21a)

![image](https://github.com/user-attachments/assets/c863ce79-3dd9-4c3a-b8ce-bf9b8cd219f8)

![image](https://github.com/user-attachments/assets/09ead541-9630-47aa-9808-0104ccb80e26)

![image](https://github.com/user-attachments/assets/2526067f-50b4-4296-b2cb-000e9cad4c98)

Berdasarkan hasil evaluasi rekomendasi berdasarkan kategori film di atas, dari 10 item yang direkomendasikan, seluruh item memiliki kategori Thriller dengan seluruh genre film berupa Horror dan Thriller. Artinya, presisi pada sistem sebesar 10/10 atau 100% di mana sesuai dengan formula yang tertera sebagai berikut: 

P = #of recommendation that are relevant/#of item we recommend = 10/10 = 1 atau 100%. 

Berdasarkan hasil evaluasi rekomendasi berdasarkan judul film di atas, dari 10 item yang direkomendasikan, seluruh item memiliki judul film dengan kategori Documentary. Artinya, presisi pada sistem sebesar 10/10 atau 100% di mana sesuai dengan formula yang tertera sebagai berikut: 

P = #of recommendation that are relevant/#of item we recommend = 10/10 = 1 atau 100%. 

Hal tersebut menunjukkan bahwa teknik yang dilakukan telah bekerja dengan efektif dalam mengenali kemiripan kategori dan judul film sehingga dapat memberikan rekomendasi film yang sesuai dengan minat pengguna. 
