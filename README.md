# Project : Analisis Penjualan E-Commerce

# Pendahuluan

Proyek ini bertujuan untuk mengeksplorasi dan menganalisis data penjualan dari sebuah perusahaan e-commerce dengan menggunakan Analisis Data Eksploratori (EDA). Tujuan utama EDA adalah untuk:
•	Mendapatkan wawasan awal dan mengidentifikasi pola atau tren dalam data.
•	Memahami hubungan antar variabel, yang dapat menginformasikan analisis lanjutan atau pembuatan model.
EDA menyediakan dasar bagi rekomendasi bisnis berdasarkan pola dan insight yang teramati.


# Gambaran Dataset

Dataset ini berisi 128.975 baris data dan beberapa kolom kunci, termasuk:
•	Order ID: ID unik untuk setiap pesanan.
•	Tanggal: Tanggal pemesanan.
•	Fulfillment: Menunjukkan apakah pesanan dipenuhi oleh Amazon atau merchant lain.
•	Sales Channel: Platform yang digunakan untuk transaksi.
•	Category: Kategori produk (misalnya, Kurta, Saree).
•	Size: Ukuran produk.
•	Qty: Jumlah yang dipesan.
•	Order Price: Total harga pesanan.
•	ship-service-level: Tingkat kecepatan pengiriman (misalnya, expedited, standard).
•	Status: Status pesanan (misalnya, shipped, returned, cancelled).



# Ringkasan Insight dari EDA

1.	Unik Order ID: Dataset mencakup 120.378 Order ID unik, menunjukkan ada beberapa pesanan dengan banyak item atau baris entri.
2.	Puncak Frekuensi Pesanan: Ada lonjakan frekuensi pesanan yang mencolok di awal Mei 2022.
3.	Distribusi Kuantitas dan Harga:
o	Nilai kuantitas sebagian besar terkonsentrasi di sekitar angka 1.
o	Nilai harga pesanan mengikuti distribusi mendekati normal.
4.	Pemenuhan oleh Amazon: Pesanan yang dipenuhi oleh Amazon secara signifikan lebih banyak dibandingkan yang dipenuhi oleh merchant, menunjukkan ketergantungan pada layanan logistik Amazon.
5.	Dominasi Platform Amazon.in: Amazon.in adalah platform utama untuk penjualan, menunjukkan efektivitas dalam menjangkau konsumen.
6.	Transaksi B2C: Sebagian besar transaksi adalah Business-to-Consumer (B2C), menunjukkan model bisnis yang fokus pada penjualan ritel kepada konsumen akhir.
7.	Kategori Produk Populer: Kategori Set dan Kurta adalah yang paling banyak dipesan, dengan hampir 10.000 entri.
8.	Tingkat Pengiriman Favorit: Pengiriman cepat (expedited) lebih banyak dipilih daripada pengiriman standard.
9.	Ukuran yang Paling Banyak Dipesan: Ukuran M, L, dan XL memiliki volume pemesanan tertinggi, menunjukkan dimensi produk yang paling diminati.
10.	Korelasi Lemah Antara Kuantitas dan Harga: Korelasi antara Kuantitas dan Harga Pesanan rendah (0,07), menunjukkan bahwa pesanan lebih besar tidak selalu berhubungan dengan harga yang lebih tinggi.
11.	Pengiriman yang Berhasil Berdasarkan Ukuran: Sebagian besar barang dengan ukuran M, L, XL, XXL, S, dan XS berhasil diterima oleh pembeli tanpa adanya pengembalian atau penolakan.
12.	Kategori dengan Harga Rata-rata Tinggi: Set, Saree, dan Western Dress memiliki harga rata-rata pesanan tertinggi, kemungkinan menunjukkan preferensi pelanggan atau kualitas produk yang lebih tinggi.
13.	Wilayah dengan Pesanan Tertinggi: Maharashtra dan Karnataka memiliki jumlah pesanan terbanyak, menunjukkan hotspot permintaan regional.


# Data Preprocessing untuk Dataset Penjualan Amazon

Repository ini berisi langkah-langkah preprocessing yang dilakukan pada dataset penjualan Amazon untuk mempersiapkan data sebelum analisis dan pembuatan model.

## Deskripsi Dataset
Dataset ini mencakup informasi transaksi penjualan di Amazon, dengan kolom seperti Date, Status, Category, Qty, Amount, dan lainnya. Proses preprocessing dilakukan untuk membersihkan, mentransformasi, dan meningkatkan kualitas data.

---

## Langkah-Langkah Preprocessing

### 1. Penanganan Missing Values
- Menghapus kolom dengan banyak nilai yang hilang, termasuk:
  - Courier Status, currency, Amount, ship-city, ship-state, ship-postal-code, ship-country, promotion-ids, fulfilled-by, Unnamed: 22.

    ![alt text](https://github.com/Rizqii1/Finpro_Kelompok1/blob/main/missing%20value.png?raw=true)
  
### 2. Penyesuaian Tipe Data
- Mengubah kolom Date menjadi tipe datetime untuk memudahkan manipulasi data.
- Mengonversi kolom B2B menjadi tipe numerik untuk konsistensi.

### 3. Penghapusan Duplikasi
- Menghapus baris yang duplikat untuk memastikan data unik.

### 4. Penanganan Outlier
- Menerapkan transformasi log pada kolom dengan skewness tinggi:
  - Qty → Qty_log
  - Amount → Amount_log
    ![alt text](https://github.com/Rizqii1/Finpro_Kelompok1/blob/main/outlier.png?raw=true)
### 5. Encoding Fitur
- *Ordinal Encoding*:
  - Memetakan nilai Size (contoh: XS, S, M, L, dll.) menjadi level numerik.
- *One-Hot Encoding*:
  - Melakukan encoding pada kolom Category dan Region.
- Memetakan kolom ship-state ke dalam wilayah geografis (contoh: Utara, Selatan, Timur, Barat).

### 6. Penanganan Ketidakseimbangan Kelas
- Memetakan kolom Status menjadi label numerik:
  - Shipped - Delivered to Buyer → 3
  - Shipped - Returned to Seller → 2
  - Shipped - Rejected by Buyer → 1
- Menggunakan *SMOTE* (Synthetic Minority Oversampling Technique) untuk menyeimbangkan jumlah kelas pada target.

### 7. Feature Engineering
- Menambahkan fitur tambahan yang terkait dengan tanggal:
  - Day (tanggal numerik dalam sebulan).
  - Day_Type (dikategorikan sebagai "Hari Kerja" atau "Akhir Pekan").
- Menambahkan indikator biner:
  - Is_Weekend (1 jika akhir pekan, 0 jika hari kerja).

### 8. Seleksi Fitur
- Menghapus kolom yang tidak relevan atau redundan setelah preprocessing, termasuk:
  - index, ship-postal-code, Sales Channel, dan Status.

---

## Hasil Akhir
Dataset yang sudah dibersihkan dan diproses siap digunakan untuk analisis lebih lanjut dan pembuatan model machine learning. Dataset ini memiliki representasi fitur yang lebih baik dan target kelas yang seimbang.
