# Final Project

### Teknologi Komputasi Awan

**Kelompok B4**
|Nama|NRP |
|--|--|
|Dimas Andhika Diputra|5027231074|
|Rafael Ega Krisaditya|5027231025|
|Rafi Afnaan Fathurrahman|5027231040|
|Kevin Anugerah Faza|5027221027|
|Aryasatya Alaauddin|5027221082|

## Permasalahan

Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah **Keampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.**

Pada suatu saat anda mendapatkan project untuk mendeploy sebuah aplikasi Sentiment Analysis dengan komponen Backend menggunakan python: sentiment-analysis.py dengan spesifikasi sebagai berikut

## Endpoints:

1. **Analyze Text**

   - **Endpoint:** `POST /analyze`
   - **Description:** This endpoint accepts a text input and returns the sentiment score of the text.
   - **Request:**
     ```json
     {
       "text": "Your text here"
     }
     ```
   - **Response:**
     ```json
     {
       "sentiment": <sentiment_score>
     }
     ```

2. **Retrieve History**
   - **Endpoint:** `GET /history`
   - **Description:** This endpoint retrieves the history of previously analyzed texts along with their sentiment scores.
   - **Response:**
     ```json
     {
      {
        "text": "Your previous text here",
        "sentiment": <sentiment_score>
      },
      ...
     }
     ```

---

Kemudian juga disediakan sebuah Frontend sederhana menggunakan [index.html](/Resources/FE/index.html) dan [styles.css](/Resources/FE/styles.css) dengan tampilan antarmuka sebagai berikut

![alt text](image.png)

Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah **1 juta rupiah per bulan (65 US$)**
konfigurasi cloud terbaik seperti apa yang bisa dibuat?

## Rancangan Arsitektur dan Tabel Harga Spesifikasi VM

Setelah melakukan berbagai pertimbangan dari segi harga hingga spesifikasi. Akhirnya kami memutuskan untuk menggunakan Digital Ocean sebagai lingkungan cloud yang akan kami gunakan.

Pertimbangan ini diambil karena Digital Ocean yang paling user friendly dan menyediakan credit gratis jika punya github education, dari semua cloud provider yang kami lihat digital ocean yang paling gampang dipahami.

**Berikut adalah rancangan arsitektur yang akan kami buat:**
<img src="./rancangan.png"/>

**Harga perkiraan yang akan kami pakai adalah seperti berikut:**
<img src="./harga.png" />

## Hasil Pengujian Setiap Endpoint

### Pengujian dengan Thunder Client

1. Get All History

<img src="./getprod.png" />

2. Create a New Text

<img src="./postprod.png" />

## Hasil Pengujian dan Analisis Loadtesting Locust

- RPS Maksimum (load testing 60 detik)

> **RPS Maksimum yang kami dapati dari beberapa stress test locust adalah 149 RPS, didapatkan ketika di test dengan menggunakan spawn rate 500 dengan Peak Concurrency Maksimum sebesar 2000 User**

- Peak Concurrency Maksimum (spawn rate 50, load testing 60 detik)

<img src="./500(50).jpg" />
> 500 PCM

- Peak Concurrency Maksimum (spawn rate 100, load testing 60 detik)

<img src="./1000(100).jpg" />
> 1000 PCM

- Peak Concurrency Maksimum (spawn rate 200, load testing 60 detik)

<img src="./1600(200).jpg" />
> 1600 PCM

- Peak Concurrency Maksimum (spawn rate 500, load testing 60 detik)

<img src="./2000(500).png" />
> 2000 PCM

## Kesimpulan dan Saran

Setelah percobaan yang kami lakukan berulang kali untuk testing locust ini, yang kami dapatkan adalah:

- Banyak hal yang mempengaruhi pengujian locust ini seperti **Koneksi internet, Peak concurrency yang diinput (bagian dari test), spawn rate yang diinput**
- Selain itu untuk spawn rate yang tinggi kami sempat beberapa kali mengalami vm backendnya ngelag. Solusi kami adalah untuk **mereset database tiap ingin menguji locust**. Hal itu sangat berpengaruh tiap kali ingin mengetest dengan uji locust, dikarenakan banyaknya data yang diinput oleh locust untuk pengujiannya

> Seperti gambar berikut, kami sempat mendapatkan bahwa data di database kami sempat ada 24k (kami mendapatkan ini sebelum menyadari bahwa data yang diinput oleh locust dalam pengujian sangat banyak)

<img src="./banyak.jpg" />
