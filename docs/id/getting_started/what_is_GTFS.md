# GTFS: Membuat Data Angkutan Umum Dapat Diakses Secara Universal## Standar data terbuka untuk informasi penumpang angkutan umum 
 
 General Transit Feed Specification, juga dikenal sebagai GTFS, adalah format data standar yang menyediakan struktur untuk angkutan umum lembaga untuk menjelaskan rincian layanan mereka seperti jadwal, stops, tarif, dll. 
 
 Hal ini memungkinkan lembaga angkutan umum untuk mempublikasikan data angkutan umum mereka dalam format yang dapat digunakan oleh berbagai macam aplikasi perangkat lunak, paling umum perjalanan perencana. Artinya, pengguna dapat dengan mudah mendapatkan informasi perjalanan untuk mengakses layanan angkutan umum hanya dengan menggunakan ponsel pintar atau perangkat sejenisnya. 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 Saat ini, GTFS adalah [Standar Terbuka](https://www.interoperablemobility.org/definitions/#open_standard) yang digunakan oleh ribuan penyedia transportasi umum di seluruh dunia. Beberapa lembaga menghasilkan data ini sendiri, sementara lembaga lainnya mempekerjakan vendor untuk membuat dan memelihara data bagi mereka. 
 
## Dukungan untuk data statis dan dinamis 
 
 GTFS terdiri dari dua bagian utama: [GTFS Schedule](../../documentation/schedule/reference) dan [GTFS Realtime](../../dokumentasi/waktu nyata/referensi). 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 GTFS Schedule berisi informasi tentang routes, jadwal, tarif, dan detail transit geografis di antara banyak fitur lainnya, dan disajikan dalam file teks sederhana[^1]. Format sederhana ini memungkinkan pembuatan dan pemeliharaan yang mudah tanpa bergantung pada perangkat lunak yang rumit atau berpemilik. 
 
 GTFS Realtime berisi pembaruan perjalanan, posisi vehicle, dan peringatan layanan, menggunakan format [Protokol Buffer](https://developers.google.com/protocol-buffers/). Bagian GTFS ini bekerja sama dengan GTFS Schedule untuk memberi tahu penumpang tentang gangguan layanan dan informasi waktu arrival terkini. 
 
 GTFS Schedule dan dokumentasi referensi GTFS Realtime tersedia di [bagian Dokumentasi Teknis](../../documentation/overview). 
 
 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="Pemutar video YouTube" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Ikon oleh Freepik">Ikon yang dibuat oleh Freepik- Flaticon</a> 
 
 [^1]: Selain file teks, format [GeoJSON](https://geojson.org/) kini juga didukung di GTFS untuk mewakili elemen tertentu layanan yang responsif terhadap permintaan. 
 

