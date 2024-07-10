# Fitur GTFS Schedule 
 
 Seiring dengan berkembangnya format Referensi GTFS untuk memenuhi kebutuhan sistem transportasi umum saat ini, fungsinya dapat menjadi semakin kompleks. **Fitur GTFS ** dimaksudkan untuk memberikan penjelasan yang jelas dan pasti tentang fungsi yang diaktifkan oleh format Referensi GTFS. Hal ini membantu lembaga angkutan umum, vendor, konsumen, dan peneliti memahami kemampuan GTFS dan menjawab pertanyaan: **Apa yang dapat saya lakukan dengan GTFS?** 
 
 Kelompok fitur berikut menjelaskan tujuan setiap fitur serta tujuan file dan bidang yang terkait dengannya, membantu pengguna memahami data mana yang diperlukan untuk mendukung fitur tertentu. 
 
## Dasar 
 Fitur-fitur penting ini membentuk inti feed GTFS. Mereka adalah elemen minimal yang diperlukan untuk mewakili layanan transportasi umum. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 Komunikasikan detail tentang lembaga yang bertanggung jawab atas layanan transit. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Stops__ 
 
 Tentukan lokasi di mana layanan transit mengambil dan menurunkan penumpang. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Rute__ 
 
 Tentukan elemen rute transit seperti nama dan jenis layanan. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __Tanggal Layanan__ 
 
 Buat struktur untuk menjadwalkan perjalanan dan pengecualian layanan. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trips__ 
 § § Mewakili kendaraan transit yang melakukan perjalanan sepanjang rute tertentu pada waktu yang dijadwalkan. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Stop Times__ 
 
 Tentukan waktu arrival dan departure setiap perjalanan untuk setiap pemberhentian. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base/#stop-times) 
 
</div> 
 
## Add-on dasar 
 Fitur-fitur ini menyempurnakan set data GTFS, meningkatkan pengalaman pengguna, dan memfasilitasi kolaborasi antar agensi, vendor, dan pengguna kembali data. Ini mungkin melibatkan penambahan kolom baru ke file yang sudah ada atau membuat file baru. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Informasi Umpan__ 
 
 Komunikasikan informasi penting tentang umpan itu sendiri. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ § § 
 Menentukan jalur geografis yang diikuti oleh vehicle sepanjang perjalanan. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __Warna Rute__ 
 
 Secara akurat menggambarkan dan mengomunikasikan skema warna yang ditetapkan untuk routes tertentu. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __Sepeda Diizinkan__ 
 
 Komunikasikan apakah kendaraan mampu menampung sepeda atau tidak. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 Komunikasikan tanda yang digunakan oleh kendaraan yang menunjukkan tujuan perjalanan. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __Jenis Lokasi__ 
 
 Klasifikasikan area utama dalam stasiun transit seperti pintu masuk dan keluar. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frequencies__ § § 
 Mewakili layanan yang beroperasi pada frekuensi reguler atau kemajuan tertentu. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/# layanan berbasis frekuensi) 
 
 - :material-subway-variant:{ .lg.middle } __Transfer__ 
 
 Jelaskan transfers yang diperbolehkan antar layanan transit yang berbeda. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Translations__ 
 § § Komunikasikan informasi layanan dalam berbagai bahasa. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Attributions__ 
 § § Komunikasikan siapa saja yang terlibat dalam pembuatan dataset. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../base_add-ons/# attributions) 
 
</div> 
 
 
## Aksesibilitas 
 Fitur aksesibilitas memberikan informasi penting bagi penyandang disabilitas untuk mengakses layanan. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Menghentikan Aksesibilitas Kursi Roda__ 
 
 Tunjukkan apakah menaiki kursi roda dapat dilakukan dari suatu lokasi. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Trips Kursi Roda Aksesibilitas__ 
 
 Tunjukkan apakah vehicle dapat menampung pengendara yang menggunakan kursi roda. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Teks- to-Speech__ 
 
 Berikan input yang diperlukan untuk mengubah teks untuk nama perhentian menjadi audio. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Tarif 
 GTFS dapat memodelkan berbagai struktur tarif, seperti tarif berdasarkan zona, jarak, atau waktu. Ini memberi tahu penumpang tentang harga perjalanan dan metode pembayaran. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Fare Products__ 
 
 Menentukan daftar tiket atau jenis tarif yang tersedia bagi pengguna. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ 
 
 Menentukan media yang dapat digunakan untuk menampung dan/atau memvalidasi produk tarif. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __Tarif Berbasis Rute__ 
 
 Jelaskan aturan yang digunakan untuk menerapkan tarif yang berbeda untuk kelompok routes tertentu. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Time- Berdasarkan Tarif__ 
 
 Jelaskan tarif yang dibedakan berdasarkan waktu atau hari dalam seminggu. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone- Berdasarkan Tarif__ 
 
 Jelaskan tarif yang dibedakan ketika bepergian dari satu daerah ke daerah lain. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Fares Transfers__ 
 
 Menentukan biaya yang berlaku saat berpindah dari satu perjalanan ke perjalanan lainnya. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 Fitur lama yang memungkinkan representasi informasi tarif yang lebih sederhana. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../fares/#fares-v1) 
 
</div> 
 
 
## Jalur 
 
 Fitur jalur memungkinkan untuk memodelkan stasiun transit besar, sehingga pengendara dipandu dari pintu masuk ke area keberangkatan. Mereka memberikan rincian jalur, perkiraan waktu navigasi, dan sistem pencarian arah. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Koneksi Jalur__ 
 
 Model jalur yang menghubungkan titik-titik relevan dalam stasiun transit. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../pathways/#jalur-koneksi) 
 
 - :material-subway-variant:{ .lg.middle } __Detail Jalur__ 
 
 Memberikan rincian tambahan mengenai karakteristik fisik suatu jalur. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Levels__ 
 § § Jelaskan dan buat daftar semua tingkatan yang berbeda dalam stasiun transit. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __Waktu Traversal Dalam Stasiun__ § § 
 Komunikasikan perkiraan waktu untuk menavigasi jalur dalam stasiun transit. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../pathways/#di-stasiun-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __Rambu Jalur__ 
 
 Komunikasikan rambu di stasiun yang terkait dengan jalur. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../pathways/#tanda-jalur) 
 
</div> 
 
## Layanan fleksibel 
 Layanan fleksibel, atau layanan yang responsif terhadap permintaan, yang tidak mengikuti jadwal reguler atau routes tetap. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Pemberhentian Berkelanjutan__ 
 
 Tunjukkan apakah pengguna dapat dijemput dan/atau diturunkan di antara stops. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __Peraturan Pemesanan__ 
 
 Tunjukkan jika pengguna dapat memesan perjalanan pada layanan yang responsif terhadap permintaan. 
 
 [:octicons-arrow-right-24: Pelajari lebih lanjut](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __Rute yang Telah Ditentukan dengan Deviasi__ 
 
 Kendaraan yang dapat menyimpang sebentar dari rute untuk mengambil atau menurunkan. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../flexible_services/#predefinisi-rute-dengan-deviasi) 
 
 - :varian-kereta bawah tanah:{ .lg.middle } __Layanan Responsif Permintaan Berbasis Zona__ 
 
 Layanan yang memungkinkan penjemputan/pengantaran di lokasi mana pun dalam area tertentu. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.tengah } __Layanan Responsif Permintaan Perhentian Tetap__ 
 
 Layanan yang memungkinkan penjemputan/pengantaran di lokasi mana pun dalam kelompok stops. 
 
 [:octicons-panah-kanan-24: Pelajari lebih lanjut](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

