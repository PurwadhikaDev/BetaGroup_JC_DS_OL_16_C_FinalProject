# **Hotel Overbooking Strategy using Machine Learning**

## **Deskripsi Proyek**
Proyek ini berfokus pada analisis mendalam terhadap faktor-faktor signifikan yang memengaruhi tingkat pembatalan reservasi hotel. Melalui pemanfaatan data historis pemesanan hotel dan penerapan machine learning, proyek ini bertujuan untuk mengembangkan model prediktif yang akurat dalam mengidentifikasi potensi pembatalan reservasi. Model yang dihasilkan diharapkan dapat menjadi landasan bagi hotel untuk mengoptimalkan strategi manajemen reservasi, meminimalkan dampak finansial akibat pembatalan, dan pada akhirnya meningkatkan pendapatan secara keseluruhan melalui penerapan kebijakan dan strategi mitigasi yang lebih efektif berdasarkan insight dari analisis data.

## **Tentang Dataset**
Dataset yang digunakan dalam proyek ini adalah **"Hotel Booking Demand Datasets"**, yang bersumber dari artikel ilmiah karya Nuno Antonio, Ana Almeida, dan Luis Nunes. Publikasi artikel ini terdapat dalam jurnal *Data in Brief*, Volume 22, Februari 2019.

Dataset ini menyediakan **data pemesanan dari dua jenis properti hotel di Portugal**: hotel kota (*city hotel*) dan hotel resor (*resort hotel*). Informasi yang terkandung di dalamnya sangat detail dan relevan untuk analisis mendalam, mencakup data reservasi yang dapat dimanfaatkan untuk:

* **Analisis Data Eksploratif (EDA):** Memahami karakteristik dan pola tersembunyi dalam data pemesanan hotel.
* **Pengembangan Model Prediktif:** Membangun model *machine learning* untuk memprediksi berbagai aspek terkait pemesanan hotel, terutama pola pembatalan, dinamika tarif, dan tren permintaan khusus.

Dataset ini secara spesifik mencakup informasi mengenai:

* **Waktu Pemesanan:** Catatan waktu dan tanggal ketika reservasi dilakukan.
* **Durasi Menginap:** Lama waktu tamu menginap di hotel (jumlah malam).
* **Komposisi Tamu:** Rincian jumlah tamu dewasa, anak-anak, dan bayi dalam setiap pemesanan.
* **Fasilitas Parkir:** Informasi ketersediaan tempat parkir yang dipesan oleh tamu.
* **Fitur-fitur Lain:** Berbagai informasi tambahan lainnya yang relevan dengan pemesanan hotel.

Penting untuk dicatat bahwa **seluruh informasi yang berpotensi mengidentifikasi informasi pribadi tamu telah dianonimkan** dari dataset ini, menjaga privasi dan etika penggunaan data.

**Sumber Data:**

Dataset asli dapat diakses dan diunduh melalui platform Kaggle pada tautan berikut:

[https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/data](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/data)

Dataset ini telah melalui proses pengunduhan dan pembersihan oleh Thomas Mock dan Antoine Bichat sebagai bagian dari inisiatif #TidyTuesday pada minggu ke-11 Februari 2020. Proses ini memastikan kualitas data yang lebih baik untuk keperluan analisis.

## **Struktur Proyek**
Proyek ini terdiri dari beberapa bagian utama:

1. Business Problem Understanding
2. Data Understanding
3. Data Cleaning
4. Exploratory Data Analysis
5. Data Analytics
6. Modelling
7. Kesimpulan dan Rekomendasi

### **Business Problem Understanding**

**Latar Belakang:**

Dalam industri perhotelan yang kompetitif, permintaan pemesanan kamar merupakan faktor kunci keberhasilan operasional. Kemampuan untuk memprediksi fluktuasi dan pola permintaan sangat penting untuk optimalisasi pendapatan dan stabilitas tingkat okupansi. Prediksi permintaan yang akurat memungkinkan hotel untuk memaksimalkan pendapatan dan mengurangi risiko kerugian akibat kamar kosong.

**Tantangan:**

Salah satu tantangan utama adalah risiko pembatalan pemesanan dan ketidakhadiran tamu (*no-show*). Pembatalan yang tinggi, terutama saat musim ramai, dapat menyebabkan kerugian signifikan. Hotel harus menyeimbangkan antara menjamin ketersediaan kamar untuk pemesanan terkonfirmasi dan menghindari potensi kerugian akibat kamar kosong.

**Pentingnya Prediksi Pembatalan:**

Prediksi pembatalan pemesanan menjadi sangat krusial, terutama saat musim puncak. Langkah pencegahan terhadap pelanggan yang berpotensi membatalkan pesanan sangat vital karena kerugian akibat pembatalan di periode ramai dapat berlipat ganda. Hotel dengan tingkat okupansi tinggi namun tingkat pembatalan tinggi justru dapat lebih merugi dibandingkan hotel dengan tingkat okupansi dan pembatalan yang sama-sama rendah.

**Kerugian Akibat Tingkat Pembatalan Tinggi:**

1. **Kerugian Pendapatan Signifikan:** Pembatalan saat okupansi tinggi menghilangkan potensi pendapatan maksimal dari kamar yang seharusnya terisi penuh.
2. **Biaya Operasional Tetap:** Biaya persiapan kamar dan staf tetap harus ditanggung, meskipun tamu batal hadir, memperbesar kerugian relatif.
3. **Hilangnya Peluang Pendapatan Tambahan:** Kamar yang dibatalkan, terutama menjelang tanggal menginap, menghilangkan kesempatan untuk dijual kembali pada permintaan tinggi.
4. **Gangguan Operasional dan Efisiensi:** Pembatalan massal mengacaukan manajemen inventaris dan perencanaan, menurunkan efisiensi, dan meningkatkan biaya operasional.

Hotel perlu proaktif mengelola pembatalan dan meningkatkan strategi manajemen untuk meminimalkan kerugian akibat tingkat pembatalan yang tinggi. Prediksi pembatalan pemesanan yang akurat menjadi solusi krusial untuk optimalisasi operasional dan pendapatan hotel.

## **Tabel Kesimpulan Data Analytics**

| No. | Kolom                        | Insight                                                                                                                                                                                                                                                                                                                                                       | Rekomendasi                                                                                                                                                                                                                                                                                                                                                       |
| --- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.  | Lead Time                    | **Pembatalan Lebih Sering di *Lead Time* Panjang, Meskipun Terbanyak di *Lead Time* Pendek**: Sebagian besar pembatalan terjadi pada *lead time* pendek (≤30 hari), namun persentase pembatalan tertinggi justru terdapat pada *lead time* panjang (>360 hari), mengindikasikan kerentanan pembatalan pada pemesanan jangka jauh.                                         | **Kebijakan yang fleksibel untuk pemesanan Jangka panjang**: <br> - Menawarkan opsi fleksibilitas seperti penjadwalan ulang tanpa biaya untuk pemesanan dengan lead time panjang untuk mengurangi pembatalan dengan memberikan alternatif selain membatalkan pemesanan. <br> **Kebijakan Deposit Non-Refundable yang Lebih Tinggi**: <br> - Mewajibkan pembayaran deposit yang lebih tinggi dan non-refundable untuk pemesanan dengan lead time panjang. Untuk Mengurangi insentif pembatalan karena tamu akan berpikir dua kali sebelum membatalkan pemesanan dengan deposit yang signifikan. |
| 2.  | Bulan (Tren Total Pemesanan) | **Peningkatan Pemesanan Signifikan hingga Musim Panas**: Total pemesanan hotel terus meningkat dari Januari hingga Juni, mencapai puncaknya pada bulan Juli. Lonjakan ini kemungkinan terkait dengan hari libur umum di Portugal pada tanggal 4 Juli, yang menandai puncak musim liburan musim panas.                                                                                  | **Kampanye Pemasaran Musiman & Paket Liburan Akhir Tahun**: <br> - Kembangkan kampanye pemasaran musiman yang ditargetkan untuk memaksimalkan pendapatan selama musim puncak. <br> - Ciptakan paket promosi menarik dan kebijakan pembatalan fleksibel untuk meningkatkan pemesanan di bulan Desember yang cenderung sepi namun memiliki banyak hari libur.                                                                 |
| 3.  | Bulan (Tren Pembatalan)      | **Agustus Volume Pembatalan Tertinggi, April Persentase Pembatalan Tertinggi**: Bulan Agustus mencatat jumlah pembatalan tertinggi (8.533), sementara Desember terendah (2.362). Meskipun demikian, persentase pembatalan tertinggi justru terjadi di bulan April (41,0%), mengindikasikan April sebagai bulan dengan risiko pembatalan tertinggi.                                          | **Perketat Kebijakan Pembatalan:** <br> - Pertimbangkan untuk menerapkan kebijakan pembatalan yang lebih ketat selama bulan April dan Agustus, seperti batas waktu pembatalan yang lebih awal atau biaya pembatalan yang lebih tinggi. Ini bisa mendorong tamu untuk lebih berkomitmen pada reservasi mereka.                                                                 |
| 4.  | Market Segment               | **Segmen Pasar Tertentu Berisiko Tinggi**: Pemesanan berkelompok (*Group Bookings*), melalui Agen Perjalanan/Operator Tur (*Travel Agent/Tour Operators*), tipe kamar A, dengan Setoran *Non-Refundable*, dan menggunakan Agen ID 1 sangat rentan terhadap pembatalan, mengindikasikan karakteristik segmen pasar yang perlu diwaspadai.                                                   | **Kebijakan Pembatalan Lebih Ketat untuk Segmen Berisiko**: <br> - Pertimbangkan untuk memperketat kebijakan pembatalan pada segmen pasar berisiko tinggi ini untuk meminimalisir potensi kerugian akibat pembatalan seperti Deposit Non-Refundable, Pembayaran Penuh di Muka, dan Batas Waktu Pembatalan yang Ketat.                                                                                                 |
| 5.  | Company                      | **Perusahaan Tidak Dikenal Dominasi Pembatalan**: Perusahaan dengan identitas tidak dikenal menunjukkan tingkat pembatalan yang tertinggi, bahkan melebihi rata-rata secara keseluruhan, menandakan potensi pemesanan yang kurang valid atau spekulatif.                                                                                                           | **Verifikasi Pemesanan:** <br> - Menerapkan proses verifikasi yang ketat untuk pemesanan perusahaan. Misalnya, meminta informasi perusahaan yang lebih lengkap, seperti alamat, nomor telepon, dan email resmi perusahaan. lalu menggunakan platform pihak ketiga untuk memverifikasi identitas perusahaan sebelum mengonfirmasi pemesanan. <br> **Kebijakan Pembatalan yang Lebih Ketat:** <br> - Menerapkan kebijakan pembatalan yang lebih ketat untuk pemesanan perusahaan. Misalnya, mengenakan biaya pembatalan atau meminta deposit yang tidak dapat dikembalikan untuk pemesanan perusahaan. <br> - Menetapkan batas waktu untuk pembatalan tanpa biaya, setelah itu biaya pembatalan akan dikenakan. <br> **Pelatihan Staf:** <br> - Memberikan pelatihan kepada staf resepsionis dan reservasi tentang bagaimana menangani pemesanan perusahaan dan pentingnya verifikasi yang cermat. <br> - Meningkatkan komunikasi internal untuk memastikan bahwa semua staf memahami kebijakan baru terkait pemesanan dan pembatalan perusahaan. |
| 6.  | Country                      | **Pemesan Lokal Portugal Lebih Sering Membatalkan**: Pemesan dari Portugal (lokal) menunjukkan tingkat pembatalan tertinggi dibandingkan negara lain, bahkan di atas rata-rata keseluruhan, mengisyaratkan faktor lokal yang mempengaruhi perilaku pembatalan.                                                                                                     | **Kebijakan Khusus:** <br> - Terapkan kebijakan pembatalan yang lebih ketat untuk pemesan lokal(Portugal), seperti periode pembatalan yang lebih awal atau biaya pembatalan yang lebih tinggi jika dibatalkan mendekati tanggal menginap. <br> **Opsi Non-Refundable:** <br> - Pada tamu portugal berikan opsi tarif non-refundable namun dengan diskon lebih besar untuk membuat tamu mau memilih opsi non-refundable.                                                                                                                                 |


## **Kesimpulan & Saran**

**Kesimpulan Utama:**

* **Peningkatan Keuntungan Signifikan:** Penggunaan model XGBoost untuk memprediksi pembatalan reservasi menunjukkan potensi peningkatan keuntungan yang signifikan, diperkirakan sekitar **30.73% lebih tinggi** dibandingkan tanpa menggunakan model dalam simulasi.
* **Overfitting Terindikasi:** Model saat ini menunjukkan performa baik, namun terindikasi gejala *overfitting*. Perlu dilakukan upaya generalisasi model agar lebih robust.
* **Implementasi *Overbooking* Berpotensi Meningkatkan Pendapatan:** Simulasi implementasi *overbooking* (dengan asumsi kompensasi 30% dari harga kamar) menunjukkan potensi peningkatan keuntungan. Namun, implementasi nyata perlu mempertimbangkan biaya dan risiko *overbooking* secara lebih komprehensif.

**Saran untuk Pengembangan Model:**

* **Generalisasi Model:**
    * **Tambahkan data pelatihan** yang lebih banyak dan beragam untuk meningkatkan representasi data.
    * **Eksplorasi model yang lebih kompleks** seperti *neural network* dengan hati-hati, sambil mengontrol risiko *overfitting*.

* **Validasi Model Berkala:** Lakukan validasi model secara berkala dengan data terbaru untuk memastikan akurasi dan generalisasi model terjaga seiring waktu.

**Saran untuk Hotel:**

* **Tindakan Segera Berbasis Analisis Data Cepat:**
    * **Segmentasi pembatalan** berdasarkan sumber pemesanan dan tipe paket harga untuk mengidentifikasi area masalah dan peluang perbaikan strategi harga dan distribusi.
* **Validasi Asumsi *Overbooking* dengan Data Terukur:**
    * **Kumpulkan data biaya relokasi & kompensasi aktual** untuk *overbooking* untuk memvalidasi asumsi biaya dan perhitungan kerugian yang lebih akurat.
* **Implementasi Bertahap *Overbooking* dengan *Threshold* Konservatif:**
    * **Uji coba *overbooking* terbatas** pada jenis kamar dan periode waktu tertentu dengan *threshold* prediksi pembatalan yang tinggi untuk meminimalkan risiko awal.
    * Lakukan **monitoring intensif** selama uji coba dan evaluasi hasil untuk penyesuaian *threshold* dan strategi.
* **Komunikasi Proaktif & Pelatihan Tim:**
    * **Sosialisasikan prosedur *overbooking* secara internal** dan **latih tim Front Office** untuk menangani situasi *overbooking* dengan baik dan profesional.
* **Integrasikan Prediksi Pembatalan:**
    * **Integrasikan model prediksi ke sistem operasional hotel (PMS/Reservasi)** untuk prediksi *real-time*.
    * Gunakan prediksi untuk **personalisasi strategi** seperti *dynamic pricing* dan penawaran *targeted* untuk pemesanan berisiko tinggi.
* **Monitoring dan Evaluasi Berkelanjutan:** Implementasikan sistem *monitoring* berkelanjutan untuk performa model dan dampak strategi terhadap bisnis hotel.

**Langkah Selanjutnya:**

* Lakukan penyempurnaan model berdasarkan saran pemodelan untuk meningkatkan generalisasi dan robustnes model.
* Implementasikan *actionable insight* secara bertahap di lingkungan hotel nyata, dimulai dengan uji coba terbatas dan *monitoring* ketat.
* Terus kumpulkan data dan lakukan evaluasi berkala untuk mengoptimalkan model dan strategi *overbooking* seiring waktu.

## Link Tableau Dashboard: [Tableau Dashboard](https://public.tableau.com/app/profile/rico.martin.sitorus/viz/Hotel_Booking_Demand_17403310873720/Market_Overview?publish=yes)


