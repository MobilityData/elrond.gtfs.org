# Membuat set data GTFS## Ikhtisar feed GTFS 
 Semua feed GTFS dimulai dengan set data dalam format Referensi GTFS, yang merupakan rangkaian file CSV yang disimpan dengan ekstensi file.txt [^1]. Pada implementasi paling dasar, kumpulan data GTFS biasanya dimulai dengan tujuh file dasar, digabungkan menjadi file.zip yang dihosting di URL stabil dan publik : ini adalah feed GTFS. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_001.png"> 
 
 Setiap file terdiri dari daftar beberapa catatan (baris data) dengan beberapa bidang informasi. Misalnya, setiap baris yang tercantum di [routes.txt](../../documentation/schedule/reference/#routestxt) mewakili rute angkutan umum dan kolomnya menjelaskan beberapa elemen rute tersebut, seperti nama, deskripsi, pengoperasian agency, dll. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_002.png"> 
 
 File dasar untuk kumpulan data GTFS dapat dijelaskan sebagai berikut: Kumpulan data jadwal GTFS memiliki satu atau beberapa routes ([routes.txt](../../documentation/schedule/reference/#routestxt)), setiap rute memiliki satu atau lebih perjalanan ([trips.txt](../../documentation/schedule/reference/#tripstxt)), setiap perjalanan mengunjungi serangkaian stops ([stops.txt](../../documentation/schedule/reference/#stopstxt)) pada waktu tertentu ([stop_times.txt](../../documentation/schedule/reference/#stop_timestxt)). Waktu perjalanan dan pemberhentian hanya berisi informasi waktu; kalender digunakan untuk menentukan hari apa perjalanan berlangsung ([calendar.txt](../../documentation/schedule/reference/#calendartxt) dan [calendar_dates.txt](../../documentation/jadwal/referensi/#calendar_datestxt)). Selain itu, beberapa agensi ([agency.txt](../../documentation/schedule/reference/#agencytxt)) dapat mengoperasikan beberapa routes. File-file ini dihubungkan satu sama lain dengan bidang-bidang yang direferensikan silang di antara mereka. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_003.png"> 
 
 Setelah file-file ini disiapkan untuk membuat set data GTFS dasar, file tambahan (optional) dapat ditambahkan untuk mengaktifkan fungsi lain atau kebutuhan khusus antara agen transportasi umum dan vendor. Beberapa contoh file ini meliputi: 
 
 - [shapes.txt](../../documentation/schedule/reference/#shapestxt) yang memungkinkan untuk merepresentasikan jalur perjalanan secara grafis, 
 - [pathways.txt](../../documentation/schedule/reference/#pathwaystxt) yang memberikan informasi yang memungkinkan untuk menghasilkan petunjuk arah untuk membantu pengguna menavigasi stasiun, 
 - [frequencies.txt](../../documentation/schedule/reference/#frequenciestxt) yang menyediakan cara alternatif untuk menentukan waktu berhenti. 
 
 Untuk informasi selengkapnya tentang semua fungsi GTFS yang dapat diaktifkan, lihat bagian [“Apa yang dapat dilakukan GTFS ?”](../features/overview/). 
 
 Kumpulan data GTFS Schedule dapat dilengkapi dengan informasi real-time seperti posisi vehicle dan pembaruan layanan. Untuk melakukan hal ini, feed GTFS Realtime perlu dibuat secara terpisah dari set data GTFS Schedule yang ada. 
 
 Feed GTFS Realtime terdiri dari file biner biasa yang disajikan melalui HTTP dan sering diperbarui. Semua jenis server web dapat menghosting dan menyajikan file tersebut. Format pertukaran data GTFS Realtime didasarkan pada [Protocol Buffer](https://developers.google.com/protocol-buffers/), mekanisme netral bahasa dan platform untuk membuat serial data terstruktur. GTFS Realtime dapat memberikan tiga jenis informasi: Pembaruan perjalanan, Peringatan Layanan, dan Posisi Kendaraan, semuanya dapat digabungkan bergantung pada informasi layanan yang perlu dikomunikasikan. 
 
 Karena GTFS Realtime memungkinkan untuk menampilkan status armada yang sebenarnya, feed perlu diperbarui secara berkala- sebaiknya setiap kali data baru masuk dari sistem Lokasi Kendaraan Otomatis layanan. Gabungan kumpulan data GTFS Schedule dan feed GTFS Realtime memungkinkan aplikasi yang digunakan untuk memberikan informasi yang akurat dan terkini kepada pengendara. Untuk informasi lebih lanjut, bacalah Dokumentasi Teknis. 
 
## Memproduksi feed GTFS pertama Anda? 
 
 Jika Anda adalah agency yang ingin memproduksi feed GTFS pertama Anda, hal pertama yang perlu Anda lakukan adalah membaca dokumentasi yang ada. 
 
 Mulailah dengan mempelajari kemampuan GTFS di bagian ["Apa yang dapat dilakukan GTFS ?"](../features/overview) dan menentukan berbagai fitur layanan transportasi umum yang ingin Anda wakili menggunakan format GTFS. Untuk eksplorasi lebih mendalam, dokumentasi referensi resmi untuk [GTFS Schedule](../../documentation/schedule/reference) dan [GTFS Realtime](../../documentation/realtime/reference) menawarkan rincian panduan untuk memodelkan fitur-fitur ini dan memastikan kepatuhan. 
 
 Selanjutnya, kumpulkan semua data yang diperlukan dari sistem Anda. Ini mencakup informasi semua stops, routes, jadwal, tarif, dll., karena banyak dari detail ini akan menjadi masukan yang akan mengisi kumpulan data GTFS. 
 
 Bergantung pada ukuran dan kompleksitas sistem, Anda memiliki opsi untuk membuat data sendiri atau mendatangkan vendor GTFS eksternal untuk mengubah data ke dalam format GTFS. 
 
 Dalam beberapa kasus, lembaga kecil dengan beberapa routes membuat datanya sendiri menggunakan perangkat lunak yang tersedia secara umum seperti spreadsheet dan editor teks. 
 
 Saat menangani cakupan sistem yang lebih besar, sebagian besar agensi memperoleh perangkat lunak pengelolaan GTFS khusus dari vendor khusus, namun beberapa agensi mungkin memilih untuk mengembangkan alat internal mereka sendiri. Terakhir, jika karakteristik sistem terbukti menyulitkan lembaga untuk menulis kumpulan data mereka sendiri, produksi GTFS dapat dialihdayakan sepenuhnya ke perusahaan yang khusus memproduksi data GTFS. 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Ikon oleh Freepik">Ikon yang dibuat oleh Freepik- Flaticon</a> 
 
 [^1]: Selain file teks, format [GeoJSON](https://geojson.org/) kini juga didukung di GTFS untuk mewakili elemen tertentu layanan yang responsif terhadap permintaan. 
 

