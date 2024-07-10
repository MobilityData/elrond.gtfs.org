# Menjadikan feed GTFS Anda tersedia untuk publik## Manfaat Membagikan GTFS Anda 
 
 Data GTFS dapat digunakan dalam banyak cara, dan membagikan data GTFS biro iklan Anda secara publik memberikan banyak manfaat bagi pengendara dan agency Anda secara keseluruhan. Hal ini mencakup: 
 
 - Mengintegrasikan feed Anda ke dalam aplikasi perencanaan perjalanan berbasis seluler dan web, memungkinkan penumpang merencanakan perjalanan di sistem Anda- Mengirimkan feed Anda ke agregator GTFS seperti Mobility Database, yang menyediakan informasi lebih luas audiens dan lebih banyak visibilitas untuk agency Anda- Menggunakan alat yang memungkinkan data GTFS divisualisasikan dan dianalisis dalam Sistem Informasi Geografis (GIS) dan program analisis berbasis peta lainnya### Aplikasi Perencanaan Perjalanan 
 
 Kapan Jika data GTFS biro iklan Anda dibagikan secara publik, data tersebut dapat digunakan oleh berbagai aplikasi perencanaan perjalanan selain Google Maps. Ini dapat mencakup aplikasi navigasi lain seperti Bing Maps, Apple Maps, serta platform khusus transit seperti Transit, Moovit, Transportr, dan Citymapper. Selain itu, akses ke data feed terbuka memungkinkan pengembang membuat aplikasi yang ditujukan untuk wilayah tertentu atau dapat memiliki fitur yang tidak disertakan dalam perencana perjalanan standar seperti: Vamos (San Joaquin &amp; Stanislaus Counties, California), MetroHero (Washington DC area), Entur (Norwegia), dan banyak lagi. 
 
### Agregator Feed 
 
 Berbagi data GTFS Anda juga memungkinkan data tersebut diindeks oleh platform agregasi feed GTFS, yang dapat mencakup direktori feed GTFS tingkat negara bagian atau kawasan, serta agregator feed internasional seperti [Database Mobilitas](https://database.mobilitydata.org/) dan [Transitland](https://www.transit.land/) (lihat agregator feed lainnya [di sini](../../resources/data)). Diindeks pada agregator feed akan meningkatkan visibilitas agensi Anda dan memungkinkan pengembang, peneliti, dan pihak berkepentingan lainnya mengakses data agensi Anda dengan mudah untuk berbagai tujuan, termasuk pengembangan aplikasi baru. 
 
### Integrasi dengan GIS, Analisis, serta Platform dan Alat lainnya 
 
 Data GTFS juga dapat diimpor dan digunakan pada berbagai platform analisis geospasial. Program Sistem Informasi Geografis (GIS) seperti ArcGIS Esri, serta QGIS sumber terbuka, memiliki plugin dan ekstensi sendiri yang dapat import dan memvisualisasikan data perhentian dan rute GTFS. 
 
 - Esri memiliki [berbagai macam alat dan plugin](https://github.com/Esri/public-transit-tools) yang menggunakan data GTFS, termasuk memvisualisasikan data jadwal- Di QGIS, [GTFS-GO](https://plugins.qgis.org/plugins/GTFS-GO-master/) dan [GTFS Loader](https://plugins.qgis.org/plugins/GTFS_Loader/) memungkinkan Anda memvisualisasikan routes + stops dalam platform- [Alat analisis tambahan](../../resources/agency-tools) 
 
 Platform lain memungkinkan Anda memvisualisasikan dan menganalisis data GTFS dengan cara yang unik: 
 
 - [Menyampaikan](https://conveyal.com/) adalah program sumber terbuka yang memungkinkan pengguna import data GTFS untuk memvisualisasikan jadwal, routes, dan pola, serta menganalisis dampak potensi perubahan layanan. Pengguna juga dapat import dan bekerja dengan data demografi untuk melakukan analisis, misalnya, bagaimana routes atau jadwal yang berbeda akan mempengaruhi akses terhadap pekerjaan di wilayah perkotaan tertentu. 
 - [GTFS ke HTML](https://gtfstohtml.com/) adalah alat sumber terbuka yang memungkinkan konversi data jadwal GTFS menjadi jadwal HTML. Hal ini memungkinkan lembaga untuk secara otomatis mempublikasikan dan memperbarui jadwal mereka di situs web mereka dalam format yang juga dapat dibaca oleh pembaca layar, sehingga data dapat diakses oleh orang-orang tunanetra. 
 
## Berbagi Data Anda: Tips &amp; Praktik Terbaik### Membuat dan Memelihara Tautan Pengambilan Permanen 
 
 Tautan pengambilan adalah URL permanen tempat file GTFS Schedule agensi Anda disimpan. Biasanya, ini dihosting di situs biro iklan Anda atau oleh vendor Anda, jika Anda membuat kontrak dengan vendor tersebut untuk produksi GTFS. Inilah cara aplikasi perencanaan perjalanan seperti Google Maps mengakses data Anda. Idealnya, file GTFS Schedule Anda dapat diunduh langsung dari URL ini tanpa perlu login. Namun, jika hal ini tidak dapat dilakukan karena pembatasan lisensi, agency Anda dapat mengontrol akses ke data dengan menggunakan dan menerbitkan kunci API kepada pengguna data. 
 
### URL dan Nama File 
 
 Tautan pengambilan dan nama file GTFS yang konsisten sangat penting untuk memastikan akses ke data feed Anda. Jika agency Anda tidak menggunakan URL dan nama file yang konsisten untuk datanya, itu berarti aplikasi perencanaan perjalanan, agregator feed, dan pengguna lain tidak akan mendapatkan data paling akurat dan terkini, sehingga akan cause masalah dalam jangka panjang..
 
 Setelah Anda menetapkan URL untuk tautan pengambilan permanen Anda, JANGAN MENGUBAHNYA. Artinya, nama URL harus tetap konsisten, meskipun filenya sendiri diperbarui. Oleh karena itu, buatlah URL Anda sesederhana dan seumum mungkin, dan hindari penggunaan URL yang memiliki tanggal atau nomor versi di dalamnya. 
 
 - **BAIK:** http://www.bart.gov/dev/schedules/google_transit.zip, 
 - **HINDARI:** http://www.bart.gov/dev/schedules/google_transit_Fall_2021.zip 
 
 Demikian pula, jaga konsistensi nama folder ZIP yang berisi file GTFS Schedule, meskipun Anda membuat pembaruan apa pun pada feed itu sendiri. Misalnya, saat Anda memperbarui feed, Anda tidak boleh menambahkan date atau nomor versi apa pun ke nama folder ZIP. Jika Anda ingin memasukkan data versi feed atau tanggal mulai dan akhir feed ke dalam feed, Anda dapat memasukkannya ke dalam file feed_info.txt. 
 
 - **BAIK:** “YourAgency_gtfs.zip”, “google_transit.zip”, “gtfs.zip”, 
 - **HINDARI:** “YourAgency_gtfs_092921.zip”, “YourAgency_Fall2021.zip” § § 
 
### Konfigurasi dan Integritas File 
 
 GTFS Anda adalah file zip yang berisi beberapa file teks yang saling berhubungan (.txt). Untuk memastikan formatnya benar, selalu lakukan hal berikut: 
 
 1. Saat membuka file teks, pastikan Anda menyimpan nilainya sebagai teks. Ada banyak kolom di GTFS yang salah dibaca atau disingkat oleh aplikasi seperti Excel. 
 2. File dibatasi koma, bukan dibatasi tab. Ini berarti setiap file berisi catatan dalam baris, dan bidang berbeda dipisahkan dengan koma. 
 3. Baris atau kolom yang berlebih akan cause kesalahan dalam mengonsumsi aplikasi, jadi pastikan tidak ada baris atau kolom kosong saat menyimpan file. 
 4. Jangan membuang file apa pun di GTFS Anda- file tersebut bekerja sama dan file apa pun yang hilang dapat cause kesalahan saat menggunakan aplikasi. 
 5. Saat melakukan zip ulang file, pastikan untuk meng-zip file tersebut, bukan folder yang memuatnya. Anda dapat yakin bahwa Anda telah melakukan ini dengan benar dengan membuka ritsleting file Anda dan segera melihat file di folder tersebut, bukan folder lain yang berisi file tersebut. 
 
 
### Pertimbangan Tambahan 
 
 Jika beberapa lembaga berbagi perhentian yang sama dengan nama atau kode berbeda, aplikasi seperti Google Maps mungkin perlu memilih salah satu. Untuk menghindari kebingungan, berkoordinasilah dengan instansi lain untuk menyepakati nama dan kode. Hal ini meminimalkan konflik antar set data GTFS yang berbeda. 
 
 Jika Anda memiliki beberapa set data GTFS yang tersedia untuk Anda —biasanya hasil dari satu set data yang dibuat untuk aplikasi publik seperti Aplikasi Transit, dan set data lainnya dibuat untuk sistem CAD/AVL operasional internal— Anda mungkin perlu memutuskan mana yang akan digunakan.menjadi GTFS yang dipublikasikan. Disarankan agar Anda memilih untuk mempromosikan feed yang berisi informasi yang paling banyak dilihat pengendara. Jika memungkinkan, usahakan agar kumpulan data GTFS Anda cocok (ID yang sama untuk hal-hal seperti stops dan perjalanan) sehingga kumpulan data internal tidak bertentangan dengan kumpulan data publik, dan pengintegrasian feed lain seperti GTFS-RT dapat dilakukan. 
 

