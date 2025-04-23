# Laporan Proyek Machine Learning - Rafif Idris Ardhana

## Project Overview: Sistem Rekomendasi Film
Kebiasaan menonton acara televisi dan film kini menjadi jauh lebih mudah berkat kemajuan internet. Layanan streaming seperti Netflix, Disney+ Hotstar, Vidio, Vision+, dan sejenisnya  memberikan kemudahan bagi pengguna untuk menikmati tayangan favorit mereka kapan saja dan melalui berbagai perangkat. Masing-masing platform ini menyediakan ribuan pilihan tontonan, misalnya Netflix yang memiliki banyak koleksi judul film dari segala penjuru dunia. Contoh lain seperti Vidio yang juga memiliki banyak koleksi film serta akses ke tontonan olahraga favorit. Dengan banyaknya konten yang tersedia, keberadaan sistem rekomendasi menjadi sangat krusial. Sistem ini membantu pengguna menemukan tayangan yang sesuai dengan preferensi mereka, sehingga pengalaman menonton menjadi lebih personal. Dari sisi bisnis, sistem rekomendasi juga berperan dalam memperpanjang waktu interaksi pengguna dengan platform melalui penyajian konten yang relevan. Hal ini berpotensi meningkatkan loyalitas pengguna sekaligus berdampak positif pada pendapatan platform. Oleh karena itu, fitur rekomendasi menjadi elemen esensial yang wajib dimiliki oleh layanan streaming film dan televisi.

**Rubrik/Kriteria Tambahan**:\
Proyek ini penting karena mengembangkan sistem rekomendasi film berbasis konten dapat memberikan beberapa manfaat, di antaranya:
- Personalisasi Pengalaman Pengguna, dapat meningkatkan kepuasan pengguna dengan menyajikan rekomendasi film yang sesuai dengan minat mereka. Selain itu dapat membantu pengguna menemukan film-film yang mungkin belum mereka pertimbangkan sebelumnya
- Membantu Pengambilan Keputusan, sistem rekomendasi dapat meningkatkan retensi pengguna, hal ini berkaitan dalam pengambilan keputusan pengguna yang mana dapat merasa terbantu dalam menemukan konten yang menarik di dalam platform

Referensi:
- Fajriansyah, M., Adikara, P. P., & Widodo, A. W. (2021). Sistem Rekomendasi Film Menggunakan Content Based Filtering. Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, 5(6), 2188-2199.
- Arfisko, H. H., & Wibowo, A. T. (2022). Sistem Rekomendasi Film Menggunakan Metode Hybrid Collaborative Filtering Dan Content-Based Filtering. eProceedings of Engineering, 9(3).

## Business Understanding
Dengan semakin banyaknya konten yang tersedia di platform streaming film, pengguna dihadapkan pada pilihan yang sangat beragam. Tanpa bantuan sistem yang tepat, pengguna mungkin kesulitan menemukan konten yang sesuai dengan preferensi mereka, yang dapat berdampak pada pengalaman pengguna (user experience) dan keterlibatan mereka dengan platform. Dari sudut pandang bisnis, menampilkan konten yang relevan secara konsisten dapat meningkatkan waktu tayang pengguna (watch time), retensi pelanggan, dan pada akhirnya meningkatkan pendapatan melalui langganan yang lebih lama atau konsumsi konten berbayar yang lebih banyak.

### Problem Statements
- Bagaimana solusi bagi pengguna agar tidak kesulitan dalam menemukan konten film sesuai dengan preferensi mereka pada platform streaming?  
- Bagaimana memberikan suatu pertimbangan bagi pengguna untuk bertahan dalam menggunakan platform streaming?

### Goals
- Mengembangkan sistem rekomendasi film berbasis content-based filtering.
- Memberikan output top-N rekomendasi film yang mirip dengan film yang dipilih pengguna.

**Rubrik/Kriteria Tambahan**:
### Solution statements
- Menggunakan pendekatan Content-Based Filtering, hal ini dilakukan dengan memanfaatkan deskripsi film, genre, aktor, dan sutradara sebagai fitur konten. Kemiripan antar film akan diukur berdasarkan kesamaan fitur-fitur ini.
- Menggunakan teknik pemrosesan bahasa alami (NLP) seperti tokenization, formatting text, lowercasing, dan lemmatization pada deskripsi film.
- Menggunakan algoritma Term Frequency-Inverse Document Frequency (TF-IDF) untuk mengubah teks deskripsi menjadi vektor numerik.
- Menghitung cosine similarity antara vektor representasi film untuk mengukur kemiripan konten.

## Data Understanding
Dataset yang digunakan merupakan dataset yang berisikan informasi detail mengenai berbagai film, termasuk judul, tanggal rilis, genre, sinopsis, aktor, sutradara, rating, dan lain-lain. Dataset ini diperoleh dari Kaggle.
- Dataset ini terdiri dari dua file yaitu `movies.csv` dan `credits.csv`
- Dataset memiliki 4800+ baris
- Link Dataset: [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

Variabel-variabel pada TMDB 500 Movie Dataset adalah sebagai berikut. Variabel yang dijelaskan merupakan variabel yang dipilih sebab dianggap penting dalam pembangunan model sistem rekomendasi.
- id : kode unik dari masing-masing film
- title : judul film
- genres : pengelompokan film berdasarkan kesamaan gaya atau tema
- keywords : kata kunci yang menunjukkan identikal dari film
- overview : deskripsi gambaran umum dari film
- cast : aktor/aktris yang berperan dalam film
- crew : sekelompok orang yang berada di balik layar pembuatan film

**Rubrik/Kriteria Tambahan**:\
Melakukan Exploratory Data Analysis:
1. Univariate Data Analysis\
    a. Movies Dataset\
        - Mengeksplor bagan (baris dan kolom) dari dataset menggunakan fungsi `head()`\
        - Mengecek info dataset menggunakan fungsi `info()`\
        - Mengecek jumlah judul film pada dataset

    b. Credits Dataset\
        - Mengeksplor bagan (baris dan kolom) dari dataset menggunakan fungsi `head()`\
        - Mengecek info dataset menggunakan fungsi `info()`

2. Data Preprocessing\
    a. Mengubah dan Memastikan Nama Kolom\
        - Mengubah nama kolom pada salah satu dataset guna menyelaraskan nama sebelum penggabungan dengan `rename()`\
        - Melakukan drop pada kolom judul pada salah satu dataset yang serupa di dataset lainnya dengan `drop()`

    b. Menggabungkan Dataset \
        - Membuat dataset baru dengan melakukan penggabungan dataset movie dan dataset credits menggunakan `merge()` sebelum memasuki tahap persiapan data

## Data Preparation
Melakukan tiga tahap persiapan data, yaitu:
1. Melakukan Seleksi Fitur, Pengananan Missing Value, Pengecekan Duplikasi
2. Mengekstrak, Menggabungkan, dan Memberi Bobot List pada Isi Fitur
3. Normalisasi Teks (Cleaning Text) pada Isi Fitur

**Rubrik/Kriteria Tambahan**:
- Tahap 1:
    - Membuat dataset baru, dengan memilih fitur yang dibutuhkan saja
    - Melakukan pengecekan terhadap missing value dan duplikasi pada fitur. Terindikasi 3 missing value pada overview
    - Sebab gambaran umum (overview) dari film tidak kita ketahui, lebih baik baris missing value di hapus. Sehingga dataset terdiri dari 4800 baris dan 7 kolom penting
- Tahap 2:
    - Beberapa kolom seperti genres, keywords, cast, dan crew berisi data dalam format JSON. Perlu dilakukan ekstraksi untuk mendapatkan daftar genre, kata kunci, nama aktor, dan nama sutradara
    - Menggabungkan teks dari kolom overview, daftar genre, keywords, nama aktor, dan nama sutradara menjadi satu representasi teks (kolom "tags") untuk setiap film. Ini akan menjadi input utama untuk perhitungan kemiripan konten
    - Memberikan pembobotan pada fitur yang dianggap berpengaruh seperti fitur keywords, cast, dan crew
    - Membuat dataset final yang terdiri dari id film, judul film, dan representasi film ("tags")
- Tahap 3:
    - Melakukan pembersihan (normalisasi) teks pada kolom "tags" sebelum masuk ke tahap modeling. Hal ini dilakukan agar model dapat mengolah representasi film untuk memperoleh hasil konten yang serupa
        - Lowercase: Mengubah teks menjadi huruf kecil
        - Re.sub: Menghilangkan karakter yang bukan spasi dan huruf
        - Tokenisasi: Memecah teks menjadi unit-unit kata (token)
        - Stopword Removal: Menghapus kata-kata umum dalam bahasa inggris yang tidak memiliki banyak informasi semantik
        - Lemmatization: Mengembalikan kata-kata ke dalam bentuk dasarnya, misalnya stories menjadi story

Tahapan ini sangat penting karena:
- Meningkatkan Kualitas Data, menghilangkan atau mengatasi data yang kotor atau tidak lengkap.
- Memudahkan Pemrosesan, mengubah data ke dalam format yang dapat dipahami dan diolah oleh algoritma machine learning.
- Meningkatkan Kinerja Model, data yang bersih dan relevan akan menghasilkan model yang lebih akurat dan efektif dalam memberikan rekomendasi.

## Modeling
Pada tahap ini, pengembangan model dilakukan dengan menggunakan:
- Representasi Fitur (kolom "tags") yaitu gabungan antara fitur overview, genres, keywords, cast, dan crew
- Menerapkan algoritma TF-IDF terhadap fitur gabungan untuk mengubahnya menjadi vektor numerik
- Menghitung cosine similarity antara vektor TF-IDF dari setiap pasangan film. Cosine similarity mengukur sudut antara dua vektor, dengan nilai 1 menunjukkan kemiripan sempurna dan nilai 0 menunjukkan tidak ada kemiripan
- Untuk memberikan rekomendasi untuk film tertentu, sistem akan mencari film-film lain dengan nilai cosine similarity tertinggi terhadap film tersebut (menapilkan 10 teratas). 

**Rubrik/Kriteria Tambahan**: 
- Kelebihan:
    - Sistem dapat memberikan rekomendasi bahkan untuk pengguna baru tanpa riwayat interaksi
    - Alasan rekomendasi dapat dijelaskan berdasarkan kemiripan fitur konten
    - Rekomendasi didasarkan pada preferensi eksplisit terhadap konten tertentu

- Kekurangan:
    - Sistem cenderung merekomendasikan item yang sangat mirip dengan item yang disukai atau sedang ditonton, sehingga kurang dalam penemuan konten baru yang berbeda yang mungkin menarik.

## Evaluation
**Metode Evaluasi**\
Evaluasi ini tidak menggunakan metrik numerik, sebab evaluasi sistem rekomendasi content-based filteting lebih difokuskan terhadap relevansi rekomendasi berdasarkan fitur metadata.\
Evaluasi ini hanya dapat dilihat dari cosine similarity (skor kemiripan) terhadap film yang dipilih.
|    Kategori    |   Skor        |   Definisi                                           |
|----------------|---------------|------------------------------------------------------|
| Sangat Tinggi  |  > 0.60       | Sangat Mirip banget (biasanya sekuel atau satu seri) |
| Tinggi         |  0.50 - 0.60  | Masih sangat relevan                                 |
| Sedang         |  0.30 - 0.50  | Mirip secara tema/genre/universe                     |
| Rendah         |  < 0.30       | Sudah mulai kurang relevan                           |

**Evaluasi penggunaan sistem rekomendasi 1 (satu):**\
**Film yang dipilih: Iron Man**
- Top 5 rekomendasi sangat baik — semuanya berada dalam narasi atau konflik yang dekat dengan Tony Stark/Iron Man.
- Skor cosine similarity di atas 0.4 bisa dianggap cukup bagus untuk TF-IDF sederhana.
- Film seperti Iron Man 2, Iron Man 3, dan Civil War memang secara narasi dan karakter sangat dekat.
- Urutan 6 ke bawah memang memiliki skor cosine rendah tetapi masih ada relevansi tema dan universe yang sama dari alur film Iron Man

**Evaluasi penggunaan sistem rekomendasi 2 (dua)**\
**Film yang dipilih: The Fast and the Furious**
- Top 3 rekomendasi sangat baik - semuanya relevan sebab berasal dari produksi yang sama, memiliki karakter utama yang sama, tema dan gaya penyutradaraan mirip.
- Rekomendasi film urutan 3 ke atas memiliki narasi yang sangat dekat sebab film-film ini merupakan bagian dari cerita sekuensial film yang dipilih
- Urutan 4 ke bawah memiliki skor cosine sedang ke rendah, sebab relevansi nya hanya pemeran utama, genre, dan aksi yang sama. Tidak memiliki relevansi yang kuat dengan cerita Fast & Furious

**Evaluasi Deskriptif**\
Tanpa penerapan model machine learning seperti sistem rekomendasi, platform streaming akan mengalami berbagai tantangan dalam aspek bisnis. Pengguna akan kesulitan menemukan konten yang sesuai dengan preferensi mereka, sehingga menciptakan pengalaman pengguna yang buruk dan berpotensi menurunkan waktu tayang (watch time). Ketika pengguna merasa tidak puas, kemungkinan besar mereka tidak akan kembali, yang berdampak pada rendahnya retensi pelanggan. Akibatnya, peluang monetisasi juga menurun karena sedikitnya konsumsi konten berbayar dan tidak maksimalnya strategi penawaran konten. Tanpa sistem cerdas yang mampu mempersonalisasi rekomendasi, platform kesulitan bersaing dalam industri yang sangat kompetitif.

**1. Evaluasi terhadap Problem Statement**
- **Bagaimana solusi bagi pengguna agar tidak kesulitan dalam menemukan konten film sesuai dengan preferensi mereka pada platform streaming?**
  Masalah ini telah berhasil dijawab dengan melakukan pengembangan model menggunakan pendekatan content-based filtering telah terbukti mampu menyarankan film-film yang relevan dengan preferensi pengguna. Hasil evaluasi dengan contoh film Iron Man dan The Fast and the Furious menunjukkan bahwa sistem ini secara efektif menyarankan film yang memiliki kesamaan narasi, genre, dan karakteristik utama.
- **Bagaimana memberikan suatu pertimbangan bagi pengguna untuk bertahan dalam menggunakan platform streaming?**
  Masalah ini telah berhasil dijawab dengan menyediakan Top-N rekomendasi film yang relevan dan personal, sistem ini memberikan pengalaman menonton yang lebih menyenangkan dan membuat pengguna lebih engaged.

**2. Evaluasi terhadap Goals**
- **Mengembangkan sistem rekomendasi film berbasis content-based filtering.**
  Tujuan ini tercapai dengan berhasilnya membangun model menggunakan kombinasi metadata film (genre, kata kunci, aktor, sutradara, dan deskripsi) yang diproses dengan TF-IDF dan Cosine Similarity. Evaluasi pada dua skenario film membuktikan sistem rekomenadi bekerja dengan baik dalam menyarankan film-film yang relevan.
- **Memberikan output top-N rekomendasi film yang mirip dengan film yang dipilih pengguna.**
  Tujuan ini tercapai dengan berhasil memperoleh output dalam menyajikan daftar film yang memiliki skor cosine similarity tinggi dan sedang, menandakan relevansi yang cukup kuat. Dalam kedua kasus uji (Iron Man dan Fast and Furious), rekomendasi teratas sangat relevan, bahkan melibatkan sekuel atau film dengan universe yang sama.

**3. Evaluasi terhadap Solution Statements**
- **Menggunakan pendekatan Content-Based Filtering, hal ini dilakukan dengan memanfaatkan deskripsi film, genre, aktor, dan sutradara sebagai fitur konten. Kemiripan antar film akan diukur berdasarkan kesamaan fitur-fitur ini**
  Pendekatan ini berhasil mengukur atau memetakan kemiripan antara film berdasarkan fitur-fitur terpilih, yang memungkinkan sistem memahami konten film secara mendalam
- **Menggunakan teknik pemrosesan bahasa alami (NLP) seperti tokenization, formatting text, lowercasing, dan lemmatization pada deskripsi film**
  Teknik ini berhasil memastikan bahwa text pada fitur diolah menjadi text yang konsisten dan dapat diproses secara efisien dengan TF-IDF
- **Menggunakan algoritma Term Frequency-Inverse Document Frequency (TF-IDF) untuk mengubah teks deskripsi menjadi vektor numerik**
  TF-IDF telah efektif dalam merepresentasikan pentingnya kata-kata (mengubah teks menjadi vektor numerik) dalam fitur "tags" pada dataset final, sehingga membantu sistem menangkap karakteristik unik dari setiap film.
- **Menghitung cosine similarity antara vektor representasi film untuk mengukur kemiripan konten**
  Cosine Similarity mampu memberikan skor numerik kemiripan antar film. Kategori skor kemiripan yang digunakan memberikan interpretasi yang mudah dipahami untuk mengevaluasi hasil.

Dengan menggunakan Content-Based Filtering menggunakan algoritma TF-IDF dan penilaian Cosine Similarity dalam membangun sistem rekomendasi, diharapkan model ini dapat membantu memberikan dampak signifikan terhadap pemahaman bisnis dan potensi pertumbuhan platform streaming film.
- Peningkatan user experience, membantu pengguna agar tidak kebingungan memilih film sebab sistem telah memberikan rekomendasi sesuai dengan preferensi mereka
- Meningkatkan _watch time_ pengguna, dengan memberikan rekomendasi yang relevan, pengguna mungkin lebih cenderung untuk menghabiskan waktu lebih lama dalam platform
- Meningkatkan retensi pelanggan, dapat mempertahankan pengguna di platform karena mereka merasa konten yang ditawarkan sesuai dengan selera mereka.
- Peluang monetasi lebih besar/ dapat meningkat, peningkatan watch time dan loyalitas dapat memberikan peluang konsumsi konten berbayar juga meningkat. Hal ini dapat memberikan peningkatan pendapatan platform.
