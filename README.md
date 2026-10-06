Capstone Project Module 2
Judul : Analysis Data Transaksi E-Commerce Tokopedia
Oleh : Annisa Andez Aunillah

Dalam repository ini, terdapat proses data analysis end-to-end mencakup proses extract, transform, dan load data. Proses extract dilakukan dengan mengimport **dataset dummy** e-commerce Tokopedia yang terdiri dari 3 tabel, yaitu tabel users, transactions, dan delivery.
Analisis data ini dilakukan karena terdapat masalah utama, yaitu penurunan efisiensi profitabilitas dan tingkat retensi pengguna akibat distribusi promo yang tidak tepat sasaran serta adanya bottleneck pada proses pemenuhan pesanan (logistik). Adapun, 6 masalah turunan yaitu sebagai berikut.
1. Segmen user mana yang memiliki kecenderungan menjadi promo-hunter (hanya belanja saat ada promo lalu churn)?
2. Seberapa besar dampak keterlambatan pengiriman (SLA miss) terhadap kemungkinan user melakukan repeat order?
3. Metode pembayaran apa yang paling sering mengalami anomali transaksi atau drop-off?
4. Bagaimana korelasi antara lokasi user dan durasi pengiriman terhadap total nilai transaksi (GMV)?
5. Apakah ada anomali data sistem (seperti tanggal transaksi mendahului tanggal registrasi) yang mengindikasikan kebocoran atau bug pada platform?
6. Berapa persentase budget promo yang sebenarnya terbuang untuk transaksi-transaksi yang secara bisnis tidak valid (outliers & fraud)?

Goals yang akan dicapai pada analisis ini adalah optimalisasi budget promo, peningkatan SLA logistic, data reliability, dan peningkatan retensi.

Tahapan dalam analisis data yang dilakukan sebagai berikut.
1. Cleaning data dari tabel users, transactions, dan delivery. Cleaning data yang dilakukan adalah:
   - Pengecekan dan treatment data missing value
   - Penyeragaman data agar tidak terdapat data duplikat
   - Transform tipe data untuk mempermudah dalam eksplorasi data
   - Pengecekan data anomali atau yang tidak valid
2. Explorasi Data Analisis.
  - Tahap ini dilakukan dengan pengecekan distribusi data dan menampilkan data visualisasi dari semua tabel
3. Analisis data.
  - Tahap ini dilakukan dengan melakukan analisis data sesuai kebutuhan dari rumusan masalah yang telah dibuat.
4. Load tabel yang sudah clean ke bigQuery agar dapat digunakan one source untuk pembuatan dashboard

Dari analisis data yang telah dilakukan, hasil analisis data berdasarkan rumusan masalah yang diatas sebagai berikut.
1. Segmen promo hunter promo relatif tersebar merata, berada di sekitaran 3%. Tidak ada perbedaan pada segmen gender. Berdasarkan lokasi user, Surabaya (3,52%) dan Makassar (3,51%) cenderung tinggi, namun selisih dengan kota lainnya masih kecil. Karakteristik promo hunter mungkin lebih terlihat dari perilaku user seperti frekuensi order.
2. Ada dampak SLA miss (Pengiriman lebih dari 3 hari) ke repeat order namun hanya kecil. Pengiriman yang terlambat (SLA miss) memiliki peluang repeat order sebesar 40,01%. Pengiriman tepat waktu (SLA tidak miss) memiliki peluang repeat order sebesar 42,62%. Perbedaan peluang repea order dari pengiriman tepat waktu dan terlambat hanya 2% saja.
3. Ada anomali tiap metode pembayaran namun relatif sama.Tingkat anomali transaksi di tiap metode pembayaran berada di sekitaran angka 1% untuk anomali nilai total transaksi (nilai promo > nilai transaksi). Tingkat anomali transaksi di tiap metode pembayaran berada di sekitaran 3% untuk anomali tanggal transaksi yang tidak sesuai.
4. Korelasi antara lokasi dan durasi pengiriman dengan GMV hanya 0,00148. Artinya, tidak ada korelasi antara lokasi dan durasi pengiriman dengan GMV. Tiap kota memiliki pola durasi pengiriman dan nilai transaksi yang mirip.
5. Terdapat anomali data sistem. Anomali data pada bagian promo amount dengan total amount sebesar 1,01% dari total order secara keseluruhan order. Anomali data pada tanggal orderan yang tidak valid sebesar 4,85% dari total order secara keseluruhan.
6. Persentase orderan yang budget promonya terbuang sebesar 5.81% dan persentase budget promo yang terbuang sebesar 5.89%. Persentase budget promo terbuang tiap metode pembayaran berada di kisaran 5.89% juga. Artinya, budget promo terbuang merata di semua metode pembayaran, tidak ada budget promo berdasarkan metode pembayaran yang menonjol.

Kesimpulan yang diperoleh dari tahap analisis yang telah dilakukan sebagai berikut.
1. Promo hunter tidak dapat dikenali dari gender, lokasi, dan metode pembayaran. Karakteristik promo hunter mungkin lebih terlihat dari perilaku user seperti frekuensi order, proporsi order promo, dan jeda antarorder.
2. Keterlambatan pengiriman berdampak kecil pada peluang repeat order. Perbedaan peluang repeat order berdasarkann terlambat atau tidaknya pengiriman hanya sebesar 2% tetapi skalanya besar.
3. Anomali tiap metode pembayaran namun relatif sama untuk anomali nilai total transaksi (nilai promo > nilai transaksi) dan anomali tanggal transaksi yang tidak sesuai. Anomali ini bersifat sistematik. Sumber masalah adanya anomali ini kemungkinan ada di aplikasi.
4. Tidak ada korelasi antara lokasi dan durasi pengiriman dengan GMV. Artinya, lokasi dan durasi pengiriman tidak menentukan nilai transaksi sehingga GMV tidak perlu dibedakan tiap lokasi.
5. Terdapat anomali data sistem, yaitu bagian nilai promo yang lebih besar dari nilai transaksi dan data tanggal transaksi. Walaupun persentase anomali datanya cenderung kecil, namun banyak budget promo yang terbuang. Anomali data ini mengindikasikan lemahnya validasi di sistem.

Rekomendasi yang dapat diberikan ke stakeholder :
1. Perbaiki kebocoran atau bug pada platform ada bagian nilai promo yang lebih besar dari nilai total transaksi dan tanggal order yang tidak valid. Perbaikan ini penting dilakukan agar dapat mencegah budget promo yang terbuang, optimalisasi budget promo, dan mempermudah data analyst untuk menganalisis data lebih lanjut.
2. Targetkan promo berdasarkan perilaku user
3. Peningkatan SLA logistik dengan evaluasi kurir/rekanan jasa kirim dengan SLA miss tertinggi
4. Pemberian kompensasi apabila terdapat SLA miss untuk meningkatkan repeat order user seperti memberi voucher yang berlaku untuk order berikutnya.
5. Mengumpulkan ulasan atau tiket komplain untuk menemukan faktor-faktor repeat order user.

Stakeholder yang sesuai dengan rekomendasi:
1. Optimalisasi Budget Promo = Marketing
2. Peningkatan SLA Logistik = Supply Chain Operations
3. Data realibility = Data Engineering, IT
4. Peningkatan retensi : Customer Service

Link dashboard : https://datastudio.google.com/reporting/df8c833e-c69d-447d-b7aa-434e6964b2b2
Link PPT : https://canva.link/twe90thw9fa8nvu
