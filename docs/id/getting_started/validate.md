# Evaluasi kualitas feed GTFS Anda 
 
 GTFS berkualitas tinggi bersifat lengkap, akurat, dan terkini. Artinya, ini mewakili bagaimana layanan saat ini beroperasi dan memberikan informasi sebanyak mungkin. 
 
## Data lengkap 
 
 GTFS berkualitas mencakup detail layanan penting seperti perubahan jadwal hari libur dan musim panas, lokasi pemberhentian yang akurat, serta nama routes dan rambu yang cocok dengan materi lain yang dapat dilihat pengendara. Meskipun suatu agency bekerja sama dengan vendor untuk memproduksi GTFS, agency tersebut pada akhirnya bertanggung jawab untuk memastikan bahwa informasi yang disajikan dalam bentuk cetak, di pesawat, dan online adalah konsisten. 
 
## Data yang akurat 
 
 Data yang akurat sangat penting untuk memberikan pengalaman transportasi yang andal dan ramah pengguna kepada penumpang angkutan umum. Kesalahan dalam data dapat menghalangi sebagian atau keseluruhan kumpulan data untuk digunakan. 
 
## Data terkini 
 
 Data yang kedaluwarsa bisa lebih menimbulkan masalah dibandingkan tidak tersedianya feed. Tidak cukup hanya sekedar mempublikasikan informasi—informasi harus sesuai dengan apa yang dilihat dan dialami pengendara. Beberapa perusahaan transportasi umum terbesar memperbarui GTFS mereka setiap minggu, atau bahkan setiap hari, namun sebagian besar perusahaan transportasi umum perlu memperbarui GTFS mereka setiap beberapa bulan, atau beberapa kali dalam setahun ketika layanan berubah. Hal ini mencakup hal-hal seperti routes atau stops baru, perubahan jadwal, atau pembaruan struktur tarif. 
 
 Banyak agensi menyewa vendor untuk membuat dan mengelola GTFS untuk mereka. Beberapa vendor mungkin proaktif dalam menanyakan perubahan layanan, namun penting bagi agensi untuk berkomunikasi dengan vendor tentang perubahan layanan yang akan datang. Anda dapat memublikasikan GTFS dengan perubahan layanan terlebih dahulu, sehingga memastikan transisi berjalan lancar bagi semua orang—agensi, vendor, perencana perjalanan, dan penumpang! 
 
## Menggunakan validator resmi 
 
 Validator GTFS Resmi menilai kualitas set data berdasarkan spesifikasi resmi, memastikan pemahaman umum dalam industri tentang apa yang dimaksud dengan set data berkualitas tinggi. 
 
 [Validator GTFS Schedule Canonical](https://gtfs-validator.mobilitydata.org/)[^1] yang gratis dan dikelola oleh [MobilityData](https://mobilitydata.org/) memastikan data GTFS Anda mematuhi [Referensi GTFS Schedule](../../documentation/schedule/reference/) dan [Praktik Terbaik](../../documentation/schedule/schedule_best_practices). Ini memberikan laporan yang mudah digunakan yang dapat dibagikan dengan pihak lain dan dokumentasi yang komprehensif. 
 
<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li> Kunjungi <a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a> .</li> 
<li> Muat kumpulan data GTFS Anda: Anda dapat memilih atau menarik &amp; melepas file ZIP, atau menyalin/menempelkan URL.</li> 
<li> Ketika validasi selesai, opsi untuk membuka laporan akan diberikan.</li> 
<li> Anda akan melihat apakah validator menemukan masalah pada data, dan link ke dokumentasi kami untuk mengetahui cara memperbaikinya. URL laporan validasi akan berfungsi selama 30 hari dan dapat dibagikan kepada orang lain.</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 Demikian pula, menggunakan [GTFS Realtime Validator](https://github.com/MobilityData/gtfs-realtime-validator) kanonik yang gratis dan bersumber terbuka akan memastikan data GTFS Anda mematuhi [Referensi GTFS Realtime] resmi (../../documentation/realtime/reference/) dan [Praktik Terbaik](../../documentation/realtime/realtime_best_practices). 
 
 Untuk informasi tentang cara membuat data berkualitas tinggi, lihat [California Transit Data Guidelines](https://dot.ca.gov/cal-itp/california-transit-data-guidelines), [Praktik Terbaik GTFS Schedule](../../documentation/schedule/schedule_best_practices) dan [Praktik Terbaik GTFS Realtime](../../documentation/realtime/realtime_best_practices). 
 
 [^1]: Untuk melihat petunjuk selengkapnya tentang cara menggunakan alat ini di pipeline data Anda dan berkontribusi pada proyek ini, silakan kunjungi [repositori GitHub](https://github.com/MobilityData/gtfs-validator ). 
 

