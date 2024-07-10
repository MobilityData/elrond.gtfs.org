## Referensi General Transit Feed Specification 
 
 **Direvisi 22 Mei 2024. Lihat [Riwayat Revisi](../change_history/revision_history) untuk detail lebih lanjut.** 
 
 Dokumen ini menjelaskan format dan struktur file yang terdiri dari set data GTFS. 
 
## Daftar Isi 
 
 1. [Konvensi Dokumen](#konvensi-dokumen) 
 2. [File Kumpulan Data](#file-dataset) 
 3. [Persyaratan File](#file-persyaratan) 
 4. [Penerbitan Kumpulan Data &amp; Praktik Umum](#penerbitan-dataset-praktik umum) 
 5. [Definisi Bidang](#definisi-bidang) 
 - [agency.txt](#agencytxt) 
 - [stops.txt](#stopstxt) 
 - [routes.txt](#routestxt) 
 - [trips.txt](#tripstxt) 
 - [stop\_times.txt](#stop_timestxt) 
 - [calendar.txt](#calendartxt) 
 - [kalender\_tanggal.txt](#calendar_datestxt) 
 - [tarif\_attributes.txt](#fare_attributestxt) 
 - [tarif\_aturan.txt](#fare_rulestxt) 
 - [jangka waktu.txt](#timeframestxt) 
 - [tarif\_media.txt](#fare_mediatxt) 
 - [tarif\_produk.txt](#fare_productstxt) 
 - [tarif\ _leg\_rules.txt](#fare_leg_rulestxt) 
 - [tarif\_transfer\_rules.txt](#fare_transfer_rulestxt) 
 - [areas.txt](#areastxt) 
 - [stop_areas.txt](#stop_areastxt) 
 - [jaringan.txt](#networkstxt) 
 - [route_networks.txt](#route_networkstxt) 
 - [shapes.txt](#bentuktxt) 
 - [frequencies.txt](#frequenciestxt) 
 - [transfers.txt](#transferstxt) 
 - [pathways.txt](#pathwaystxt) 
 - [levels.txt](#levelstxt) 
 - [grup_lokasi.txt](#lokasi_grupstxt) 
 - [location_group_stops.txt](#location_group_stopstxt) 
 - [locations.geojson](#locationsgeojson) 
 - [booking_rules.txt](#booking_rulestxt) 
 - [translations.txt](#translationstxt) 
 - [umpan\ _info.txt](#feed_infotxt) 
 - [attributions.txt](#attributionstxt) 
 
## Konvensi Dokumen 
 Kata kunci "HARUS", "TIDAK BOLEH", "WAJIB", "HARUS", “TIDAK BOLEH”, “HARUS”, “TIDAK BOLEH”, “DIANJURKAN”, “BOLEH”, dan “OPSIONAL” dalam dokumen ini harus ditafsirkan sebagaimana dijelaskan dalam [RFC 2119](https://tools.ietf.org/html/rfc2119). 
 
 
### Definisi Istilah 
 
 Bagian ini mendefinisikan istilah-istilah yang digunakan di seluruh dokumen ini. 
 
 * **Dataset** - Satu set file lengkap yang ditentukan oleh referensi spesifikasi ini. Mengubah kumpulan data akan membuat versi kumpulan data baru. Kumpulan data harus dipublikasikan di URL publik dan permanen, termasuk nama file zip. (misalnya, https: agency.org/gtfs/gtfs.zip). 
 * **Rekaman** - Struktur data dasar yang terdiri dari sejumlah nilai bidang berbeda yang menggambarkan satu entity (misalnya agency angkutan umum, pemberhentian, rute, dll.). Diwakili, dalam sebuah tabel, sebagai sebuah baris. 
 * **Field** - Properti objek atau entity. Diwakili, dalam tabel, sebagai kolom. Bidang ini ada jika ditambahkan dalam file sebagai header. Ini mungkin atau mungkin tidak memiliki nilai bidang yang ditentukan. 
 * **Nilai bidang** - Entri individual dalam suatu bidang. Diwakili, dalam sebuah tabel, sebagai satu sel. 
 * **Hari layanan** - Hari layanan adalah periode waktu yang digunakan untuk menunjukkan penjadwalan rute. Definisi pasti hari layanan bervariasi dari agency ke agency, namun hari layanan sering kali tidak sesuai dengan hari kalender. Suatu hari layanan dapat melebihi pukul 24:00:00 jika layanan dimulai pada suatu hari dan berakhir pada hari berikutnya. Misalnya, layanan yang berjalan mulai pukul 08:00:00 pada hari Jumat hingga 02:00:00 pada hari Sabtu, dapat dinyatakan berjalan mulai pukul 08:00:00 hingga 26:00:00 pada satu hari layanan. 
 * **Bidang Text-to-speech** - Bidang harus berisi informasi yang sama dengan bidang induknya (yang akan digunakan kembali jika kosong). Hal ini bertujuan untuk dibaca sebagai text-to-speech, oleh karena itu, singkatan harus dihilangkan ("St" harus dibaca sebagai "Street" atau "Saint"; "Elizabeth I" harus menjadi "Elizabeth yang pertama") atau tetap dibaca apa adanya ("Bandara JFK" katanya disingkat). 
 * **Kaki** - Perjalanan di mana pengendara naik dan turun di antara sepasang lokasi berikutnya sepanjang perjalanan. 
 * **Perjalanan** - Keseluruhan perjalanan dari asal ke tujuan, termasuk semua perjalanan dan transfers di antaranya. 
 * **Sub-perjalanan** - Dua bagian atau lebih yang membentuk subset perjalanan. 
 * **Produk tarif** - Produk tarif yang dapat dibeli dan dapat digunakan untuk membayar atau memvalidasi perjalanan. 
 
### Kehadiran 
 Ketentuan kehadiran berlaku untuk bidang dan file: 
 
 * **Wajib** - Bidang atau file harus disertakan dalam kumpulan data dan berisi nilai yang valid untuk setiap catatan. 
 * **Opsional** - Bidang atau file dapat dihilangkan dari kumpulan data. 
 * **Wajib Bersyarat** - Bidang atau file harus disertakan berdasarkan ketentuan yang diuraikan dalam deskripsi bidang atau file. 
 * **Dilarang Bersyarat** - Bidang atau file tidak boleh disertakan berdasarkan ketentuan yang diuraikan dalam deskripsi bidang atau file. 
 * **Direkomendasikan** - Bidang atau file dapat dihilangkan dari kumpulan data, namun merupakan praktik terbaik untuk menyertakannya. Sebelum menghilangkan bidang atau file ini, praktik terbaik harus dievaluasi secara cermat dan implikasi penuh dari kelalaian harus dipahami. 
 
### Jenis Bidang- **Warna** - Warna yang dikodekan sebagai angka heksadesimal enam digit. Lihat [https://htmlcolorcodes.com](https://htmlcolorcodes.com) untuk menghasilkan nilai yang valid (awalan "#" tidak boleh disertakan).<br> *Contoh: `FFFFFF` untuk warna putih, `000000` untuk warna hitam, atau `0039A6` untuk garis A,C,E di NYMTA.* 
 - **Kode mata uang** - Kode currency menurut abjad ISO 4217. Untuk daftar currency saat ini, lihat [https://en.wikipedia.org/wiki/ISO_4217#Active\_codes](https://en.wikipedia.org/wiki/ISO_4217#Active_codes).<br> *Contoh: `CAD untuk dolar Kanada, `EUR untuk euro, atau `JPY untuk yen Jepang.* 
 - ** amount mata uang ** - Nilai desimal yang menunjukkan amount currency. Jumlah tempat desimal ditentukan oleh [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217#Active_codes) untuk kode Mata Uang yang menyertainya. Semua perhitungan keuangan harus diproses sebagai desimal, currency, atau jenis setara lainnya yang sesuai untuk perhitungan keuangan tergantung pada bahasa pemrograman yang digunakan untuk menggunakan data. Memproses jumlah currency sebagai float tidak disarankan karena ada keuntungan atau kerugian uang selama perhitungan. 
 - **Tanggal** - Hari layanan dalam format YYYYMMDD. Karena waktu dalam suatu hari layanan mungkin di atas pukul 24:00:00, maka hari layanan tersebut mungkin berisi informasi untuk hari berikutnya.<br> *Contoh: `20180913` untuk 13 September 2018.* 
 - ** Email** - Alamat email.<br> *Contoh: `example@example.com`* 
 - **Enum** - Opsi dari sekumpulan konstanta yang telah ditentukan sebelumnya yang ditentukan di kolom "Deskripsi".<br> *Contoh: Bidang `route_type berisi `0` untuk trem, `1` untuk kereta bawah tanah...* 
 - **ID** - Nilai bidang ID adalah ID internal, tidak dimaksudkan untuk ditampilkan kepada pengendara, dan merupakan urutan karakter UTF-8 apa pun. Disarankan hanya menggunakan karakter ASCII yang dapat dicetak. ID diberi label "ID unik" jika ID tersebut harus unik di dalam file. ID yang ditentukan dalam satu file.txt sering kali direferensikan di file.txt lainnya. ID yang mereferensikan ID di tabel lain diberi label "ID asing".<br> *Contoh: Bidang `stop_id` di [stops.txt](#stopstxt) adalah "ID unik". Bidang `parent_station` di [stops.txt](#stopstxt) adalah "ID asing yang mereferensikan `stops.stop_id`".* 
 - **Kode bahasa** - Kode bahasa IETF BCP 47. Untuk pengenalan IETF BCP 47, lihat [http://www.rfc-editor.org/rfc/bcp/bcp47 .txt](http://www.rfc-editor.org/rfc/bcp/bcp47 .txt) dan [http://www.w3.org/International/articles/bahasa-tags/](http://www.w3.org/International/articles/bahasa-tags/).<br> *Contoh: `en` untuk bahasa Inggris, `en-US` untuk bahasa Inggris Amerika, atau `de` untuk bahasa Jerman.* 
 - **Lintang** - latitude WGS84 dalam derajat desimal. Nilainya harus lebih besar atau sama dengan-90,0 dan kurang dari atau sama dengan 90,0. *<br> Contoh: `41.890169` untuk Colosseum di Roma.* 
 - **Bujur** - longitude WGS84 dalam derajat desimal. Nilainya harus lebih besar atau sama dengan-180.0 dan kurang dari atau sama dengan 180.0.<br> *Contoh: `12.492269` untuk Colosseum di Roma.* 
 - ** Float** - Angka floating point. 
 - **Bilangan Bulat** - Bilangan bulat. 
 - ** Phone number** - Nomor telepon. 
 - **Waktu** - Waktu dalam format HH:MM:SS (H:MM:SS juga diterima). Waktu diukur dari "tengah hari dikurangi jam 12" pada hari layanan (efektif tengah malam kecuali pada hari-hari di mana terjadi perubahan waktu musim panas). Untuk waktu yang terjadi setelah tengah malam pada hari layanan, masukkan waktu dengan nilai yang lebih besar dari 24:00:00 dalam JJ:MM:SS.<br> *Contoh: `14:30:00` untuk pukul 14:30 atau `25:35:00` untuk pukul 01:35 keesokan harinya.* 
 - ** Text** - string karakter UTF-8, yang dimaksudkan untuk ditampilkan dan oleh karena itu harus dapat dibaca manusia. 
 - **Zona Waktu** - Zona waktu TZ dari [https://www.iana.org/time-zones](https://www.iana.org/time-zones). Nama zona waktu tidak pernah mengandung karakter spasi tetapi mungkin mengandung garis bawah. Lihat [http://en.wikipedia.org/wiki/List\_of\_tz\_zones](http://en.wikipedia.org/wiki/List\_of\_tz\_zones) untuk daftar nilai yang valid .<br> *Contoh: `Asia/Tokyo, `America/Los_Angeles atau `Africa/Cairo.* 
 - ** URL** - URL yang sepenuhnya memenuhi syarat yang mencakup http://atau https://, dan khusus apa pun karakter dalam URL harus di-escape dengan benar. Lihat [http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html](http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html) berikut ini untuk mengetahui deskripsi tentang cara membuat nilai URL yang sepenuhnya memenuhi syarat. 
 
### Tanda Bidang 
 Tanda yang berlaku untuk jenis bidang Float atau Integer: 
 
 * **Non-negatif** - Lebih besar dari atau sama dengan 0. 
 * **Bukan nol** - Tidak sama dengan 0. 
 * **Positif** - Lebih besar dari 0. 
 
 _Contoh: **Non-negative float** - Bilangan floating point yang lebih besar atau sama dengan 0._ 
 
### Atribut Kumpulan Data 
 **kunci utama** kumpulan data adalah bidang atau kombinasi bidang yang secara unik mengidentifikasi suatu baris. `Primary key (*)` digunakan ketika semua bidang yang disediakan untuk suatu file digunakan untuk mengidentifikasi suatu baris secara unik. `Primary key (none)` berarti file tersebut hanya mengizinkan satu baris. 
 
 _Contoh: kolom `trip_id` dan `stop_sequence` menjadi kunci utama [stop_times.txt](#stop_timestxt)._ 
 
## File Kumpulan Data 
 
 Spesifikasi ini mendefinisikan file berikut: 
 
 | Nama File | Kehadiran | Deskripsi | 
 |------|------|------| 
 | [agency.txt](#agencytxt) | **Wajib** | Agen angkutan umum dengan layanan terwakili dalam kumpulan data ini. | 
 | [stops.txt](#stopstxt) | **Wajib** | Berhenti di tempat kendaraan menaikkan atau menurunkan pengendara. Juga mendefinisikan stasiun dan pintu masuk stasiun. | 
 | [routes.txt](#routestxt) | **Wajib** | routes transit. Rute adalah sekelompok perjalanan yang ditampilkan kepada pengendara sebagai satu layanan. | 
 | [trips.txt](#tripstxt) | **Wajib** | Perjalanan untuk setiap rute. Perjalanan adalah rangkaian dua stops atau lebih yang terjadi dalam jangka waktu tertentu. | 
 | [stop_times.txt](#stop_timestxt) | **Wajib** | Waktu vehicle tiba dan berangkat dari stops untuk setiap perjalanan. | 
 | [calendar.txt](#calendartxt) | **Wajib Bersyarat** | Tanggal layanan ditentukan menggunakan jadwal mingguan dengan tanggal mulai dan berakhir.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** kecuali semua tanggal layanan ditentukan di [calendar_dates.txt](#calendar_datestxt).<br> - Opsional sebaliknya. | 
 | [calendar_dates.txt](#tanggal_kalendertxt) | **Wajib Bersyarat** | Pengecualian untuk layanan yang ditentukan di [calendar.txt](#calendartxt).<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika [calendar.txt](#calendartxt) dihilangkan. Dalam hal ini [calendar_dates.txt](#calendar_datestxt) harus berisi semua tanggal layanan.<br> - Opsional sebaliknya. | 
 | [fare_attributes.txt](#fare_attributestxt) | Opsional | Informasi tarif untuk routes agen transit. | 
 | [fare_rules.txt](#fare_rulestxt) | Opsional | Aturan untuk menerapkan tarif untuk rencana perjalanan. | 
 | [jangka waktu.txt](#jangka waktutxt) | Opsional | Periode tanggal dan waktu yang digunakan dalam aturan tarif untuk tarif yang bergantung pada faktor date dan waktu. | 
 | [tarif_media.txt](#tarif_mediatxt) | Opsional | Untuk mendeskripsikan media tarif yang dapat digunakan untuk menggunakan produk tarif.<br><br> File [fare_media.txt](#fare_mediatxt) menjelaskan konsep yang tidak terwakili dalam [fare_attributes.txt](#fare_attributestxt) dan [fare_rules.txt](#fare_rulestxt). Dengan demikian, penggunaan [fare_media.txt](#fare_mediatxt) sepenuhnya terpisah dari file [fare_attributes.txt](#fare_attributestxt) dan [fare_rules.txt](#fare_rulestxt). | 
 | [fare_products.txt](#fare_productstxt) | Opsional | Untuk menjelaskan berbagai jenis tiket atau tarif yang dapat dibeli oleh penumpang.<br><br> File [fare_products.txt](#fare_productstxt) menjelaskan produk tarif yang tidak terwakili dalam [fare_attributes.txt](#fare_attributestxt) dan [fare_rules.txt](#fare_rulestxt). Dengan demikian, penggunaan [fare_products.txt](#fare_productstxt) sepenuhnya terpisah dari file [fare_attributes.txt](#fare_attributestxt) dan [fare_rules.txt](#fare_rulestxt). | 
 | [fare_leg_rules.txt](#fare_leg_rulestxt) | Opsional | Aturan tarif untuk masing-masing tahap perjalanan.<br><br> File [fare_leg_rules.txt](#fare_leg_rulestxt) menyediakan metode yang lebih rinci untuk memodelkan struktur tarif. Dengan demikian, penggunaan [fare_leg_rules.txt](#fare_leg_rulestxt) sepenuhnya terpisah dari file [fare_attributes.txt](#fare_attributestxt) dan [fare_rules.txt](#fare_rulestxt). | 
 | [fare_transfer_rules.txt](#fare_transfer_rulestxt) | Opsional | Aturan tarif untuk transfers antar jalur perjalanan.<br><br> Bersama dengan [fare_leg_rules.txt](#fare_leg_rulestxt), file [fare_transfer_rules.txt](#fare_transfer_rulestxt) menyediakan metode yang lebih detail untuk memodelkan struktur tarif. Dengan demikian, penggunaan [fare_transfer_rules.txt](#fare_transfer_rulestxt) sepenuhnya terpisah dari file [fare_attributes.txt](#fare_attributestxt) dan [fare_rules.txt](#fare_rulestxt). | 
 | [areas.txt](#areastxt) | Opsional | Pengelompokan area lokasi. | 
 | [stop_areas.txt](#stop_areastxt) | Opsional | Aturan untuk menetapkan stops di suatu area. | 
 | [jaringan.txt](#networkstxt) | **Dilarang Bersyarat** | Pengelompokan jaringan routes.<br><br> Dilarang Bersyarat:<br> - **Dilarang** jika `network_id ada di [routes.txt](#routestxt).<br> - Opsional sebaliknya. | 
 | [route_networks.txt](#route_networkstxt) | **Dilarang Bersyarat** | Aturan untuk menetapkan routes ke jaringan.<br><br> Dilarang Bersyarat:<br> - **Dilarang** jika `network_id ada di [routes.txt](#routestxt).<br> - Opsional sebaliknya. | 
 | [shapes.txt](#bentuktxt) | Opsional | Aturan untuk memetakan jalur perjalanan vehicle, kadang-kadang disebut sebagai alinyemen rute. | 
 | [frequencies.txt](#frequenciestxt) | Opsional | Headway (waktu antar perjalanan) untuk layanan berbasis headway atau representasi terkompresi dari layanan jadwal tetap. | 
 | [transfers.txt](#transferstxt) | Opsional | Aturan untuk membuat koneksi di titik transfer antar routes. | 
 | [pathways.txt](#pathwaystxt) | Opsional | Jalur yang menghubungkan lokasi-lokasi di dalam stasiun. | 
 | [levels.txt](#levelstxt) | **Wajib Bersyarat** | Level dalam stasiun.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** saat menjelaskan pathways dengan elevator (`pathway_mode=5).<br> - Opsional sebaliknya. | 
 | [grup_lokasi.txt](#lokasi_grupstxt) | Opsional | Sekelompok stops yang bersama-sama menunjukkan lokasi di mana pengendara dapat meminta penjemputan atau pengantaran. | 
 | [location_group_stops.txt](#location_group_stopstxt) | Opsional | Aturan untuk menetapkan stops ke grup lokasi. | 
 | [locations.geojson](#locationsgeojson) | Opsional | Zona untuk permintaan penjemputan atau pengantaran penumpang oleh layanan sesuai permintaan, direpresentasikan sebagai poligon GeoJSON. | 
 | [booking_rules.txt](#booking_rulestxt) | Opsional | Informasi pemesanan untuk layanan yang diminta pengendara. | 
 | [translations.txt](#translationstxt) | Opsional | Terjemahan nilai kumpulan data yang berhubungan dengan pelanggan. | 
 | [feed_info.txt](#feed_infotxt) | Opsional | Metadata set data, termasuk penerbit, versi, dan informasi masa berlaku. | 
 | [attributions.txt](#attributionstxt) | Opsional | attributions kumpulan data. | 
 
## Persyaratan File 
 
 Persyaratan berikut berlaku untuk format dan konten file kumpulan data: 
 
 * Semua file harus disimpan sebagai teks yang dipisahkan koma. 
 * Baris pertama setiap file harus berisi nama field. Setiap subbagian pada bagian [Definisi Kolom](#definisi kolom) berkaitan dengan salah satu file dalam kumpulan data GTFS dan mencantumkan nama kolom yang dapat digunakan dalam file tersebut. 
 * Semua nama file dan field peka huruf besar-kecil. 
 * Nilai bidang tidak boleh berisi tab, pengangkutan kembali, atau baris baru. 
 * Nilai field yang mengandung tanda kutip atau koma harus diapit oleh tanda kutip. Selain itu, setiap tanda petik pada kolom nilai harus diawali dengan tanda petik. Hal ini konsisten dengan cara Microsoft Excel mengeluarkan file yang dibatasi koma (CSV). Untuk informasi lebih lanjut tentang format file CSV, lihat [http://tools.ietf.org/html/rfc4180](http://tools.ietf.org/html/rfc4180). 
 Contoh berikut menunjukkan bagaimana nilai bidang akan muncul dalam file yang dipisahkan koma: 
 * **Nilai bidang asli:** `Contains "quotes", commas and text` 
 * **Nilai bidang dalam file CSV :** `"Contains ""quotes"", commas and text"` 
 * Nilai bidang tidak boleh berisi tag HTML, komentar, atau rangkaian escape. 
 * Spasi ekstra antar kolom atau nama kolom harus dihilangkan. Banyak parser yang menganggap spasi sebagai bagian dari nilai, sehingga dapat cause kesalahan. 
 * Setiap baris harus diakhiri dengan karakter linebreak CRLF atau LF. 
 * File harus dikodekan dalam UTF-8 untuk mendukung semua karakter Unicode. File yang menyertakan karakter Unicode byte-order mark (BOM) dapat diterima. Lihat [http://unicode.org/faq/utf_bom.html#BOM](http://unicode.org/faq/utf_bom.html#BOM) untuk informasi lebih lanjut tentang karakter BOM dan UTF-8. 
 * Semua file kumpulan data harus di-zip menjadi satu. File harus berada di tingkat root secara langsung, bukan di subfolder. 
 * Semua string teks yang menghadap pelanggan (termasuk nama perhentian, nama rute, dan rambu depan) harus menggunakan Huruf Campuran (bukan HURUF BESAR SEMUA), mengikuti konvensi lokal untuk penggunaan huruf besar pada nama tempat pada tampilan yang mampu menampilkan karakter huruf kecil (misalnya “Brighton Churchill Square”, “Villiers-sur-Marne”, “Market Street”). 
 * Penggunaan singkatan harus dihindari di seluruh feed untuk nama dan teks lainnya (misalnya St.untuk Jalan) kecuali suatu lokasi disebut dengan nama singkatannya (misalnya “Bandara JFK”). Singkatan mungkin bermasalah untuk aksesibilitas oleh perangkat lunak pembaca layar dan antarmuka pengguna suara. Mengonsumsi perangkat lunak dapat direkayasa untuk mengonversi kata lengkap menjadi singkatan secara andal untuk ditampilkan, namun mengonversi dari singkatan menjadi kata lengkap rentan terhadap risiko kesalahan yang lebih besar. 
 
## Penerbitan Kumpulan Data &amp; Praktik Umum 
 
 * Kumpulan data harus dipublikasikan di URL publik dan permanen, termasuk nama file zip. (misalnya, agency.org/gtfs/gtfs.zip). Idealnya, URL harus dapat langsung diunduh tanpa memerlukan login untuk mengakses file, untuk memfasilitasi pengunduhan dengan menggunakan aplikasi perangkat lunak. Meskipun disarankan (dan merupakan praktik yang paling umum) untuk membuat set data GTFS dapat didownload secara terbuka, jika penyedia data memang perlu mengontrol akses ke GTFS karena alasan lisensi atau lainnya, disarankan untuk mengontrol akses ke set data GTFS menggunakan kunci API. yang akan memfasilitasi pengunduhan otomatis. 
 * Data GTFS harus dipublikasikan secara berulang sehingga satu file di lokasi yang stabil selalu berisi deskripsi resmi terbaru tentang layanan untuk agency (atau lembaga) angkutan umum. 
 * Kumpulan data harus mempertahankan pengidentifikasi persisten (bidang id ) untuk `stop_id`, `route_id`, dan `agency_id` di seluruh iterasi data bila memungkinkan. 
 * Satu set data GTFS harus berisi layanan saat ini dan yang akan datang (terkadang disebut set data “gabungan”). Ada beberapa [alat penggabungan](../../../resources/gtfs/#gtfs-merge-tools) yang tersedia yang dapat digunakan untuk membuat kumpulan data gabungan dari dua feed GTFS berbeda. 
 * Kapan saja, kumpulan data GTFS yang dipublikasikan harus valid setidaknya selama 7 hari ke depan, dan idealnya selama operator yakin bahwa jadwal tersebut akan terus dijalankan. 
 * Jika memungkinkan, kumpulan data GTFS harus mencakup setidaknya layanan 30 hari ke depan. 
 * Layanan lama (kalender kedaluwarsa) harus dihapus dari feed. 
 * Jika modifikasi layanan akan berlaku dalam 7 hari atau kurang, perubahan layanan ini harus dinyatakan melalui feed GTFS-realtime (nasihat layanan atau pembaruan perjalanan) dan bukan set data GTFS statis. 
 * Server web yang menghosting data GTFS harus dikonfigurasi untuk melaporkan date modifikasi file dengan benar (lihat [HTTP/1.1- Permintaan Komentar 2616, pada Bagian 14.29](https://tools.ietf.org/html/rfc2616#bagian-14.29)). 
 
## Definisi Bidang### agency.txt 
 
 File: **Wajib** 
 
 Kunci utama (`agency_id`) 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `agency_id| ID Unik | **Wajib Bersyarat** | Mengidentifikasi merek angkutan umum yang sering kali identik dengan agency angkutan umum. Perlu diperhatikan bahwa dalam beberapa kasus, seperti ketika satu agency mengoperasikan beberapa layanan terpisah, agensi dan merek akan berbeda. Dokumen ini menggunakan istilah "agency" sebagai pengganti "merek". Kumpulan data mungkin berisi data dari beberapa lembaga.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika kumpulan data berisi data untuk beberapa perusahaan transportasi umum.<br> - Direkomendasikan sebaliknya. | 
 | `agency_name| Text | **Wajib** | Nama lengkap agency transit. | 
 | `agency_url| URL | **Wajib** | URL agency transportasi umum. | 
 | `agency_timezone| Zona Waktu | **Wajib** | Zona waktu tempat agency transportasi umum berada. Jika beberapa agensi ditentukan dalam kumpulan data, masing-masing agensi harus memiliki `agency_timezone yang sama. | 
 | `agency_lang| Kode bahasa | Opsional | Bahasa utama yang digunakan oleh agency transit ini. Harus disediakan untuk membantu konsumen GTFS memilih aturan kapitalisasi dan setelan khusus bahasa lainnya untuk set data. | 
 | `agency_phone| Phone number | Opsional | Nomor telepon suara untuk agency yang ditentukan. Bidang ini merupakan nilai string yang menyajikan nomor telepon sebagai tipikal area layanan lembaga. Ini mungkin berisi tanda baca untuk mengelompokkan digit-digit nomor tersebut. Teks yang dapat dihubungi (misalnya, "503-238-RIDE" TriMet) diperbolehkan, namun bidang tersebut tidak boleh berisi teks deskriptif lainnya. | 
 | `agency_fare_url| URL | Opsional | URL halaman web yang memungkinkan penumpang membeli tiket atau instrumen tarif lainnya untuk agency tersebut secara online. | 
 | `agency_email| Email | Opsional | Alamat Email dipantau secara aktif oleh departemen layanan pelanggan agensi. Alamat email ini harus menjadi titik kontak langsung di mana penumpang angkutan umum dapat menghubungi perwakilan layanan pelanggan di agency tersebut. | 
 
### stops.txt 
 
 File: **Wajib** 
 
 Kunci utama (`stop_id`) 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `stop_id` | ID Unik | **Wajib** | Mengidentifikasi lokasi: perhentian/platform, stasiun, pintu masuk/keluar, simpul umum atau area keberangkatan (lihat `location_type).<br><br> ID harus unik di semua nilai `stops.stop_id, locations.geojson `id`, dan `location_groups.location_group_id`.<br><br> Beberapa routes mungkin menggunakan `stop_id` yang sama. | 
 | `stop_code| Text | Opsional | Teks pendek atau nomor yang mengidentifikasi lokasi pengendara. Kode-kode ini sering digunakan dalam sistem informasi angkutan umum berbasis telepon atau dicetak pada papan tanda untuk memudahkan pengendara mendapatkan informasi untuk lokasi tertentu. `stop_code mungkin sama dengan `stop_id` jika bersifat publik. Bidang ini harus dibiarkan kosong untuk lokasi tanpa kode yang diberikan kepada pengendara. | 
 | `stop_name| Text | **Wajib Bersyarat** | Nama lokasi. `stop_name` harus sesuai dengan nama lokasi yang dilihat pengendara dari agen tersebut seperti yang tercetak pada jadwal, dipublikasikan secara online, atau ditunjukkan pada papan tanda. Untuk terjemahan ke bahasa lain, gunakan [translations.txt](#translationstxt).<br><br> Bila lokasinya adalah area kos (`location_type=4), maka `stop_name harus berisi nama area kost seperti yang ditampilkan oleh agency. Bisa berupa satu huruf saja (seperti di beberapa stasiun kereta api antar kota di Eropa), atau teks seperti “Area naik kursi roda” (Kereta Bawah Tanah NYC) atau “Kepala kereta pendek” (RER Paris).<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** untuk lokasi yang merupakan stops (`location_type=0`), stasiun (`location_type=1`) atau pintu masuk/keluar (`location_type=2`).<br> - Opsional untuk lokasi yang merupakan simpul umum (`location_type=3`) atau area keberangkatan (`location_type=4`).| 
 | `tts_stop_name| Text | Opsional | Versi `stop_name yang dapat dibaca. Lihat "Bidang Text-to-speech" di [Definisi Istilah](#definisi-istilah) untuk mengetahui lebih lanjut. | 
 | `stop_desc| Text | Opsional | Deskripsi lokasi yang memberikan informasi berguna dan berkualitas. Tidak boleh merupakan duplikat dari `stop_name.| 
 | `berhenti

lat` | Lintang | **Wajib Bersyarat** | Lintang lokasi.<br><br> Untuk stops/platform (`location_type=0`) dan boarding area (`location_type=4`), koordinatnya harus berupa tiang bus — jika ada — dan lokasi penumpang menaiki vehicle (di trotoar atau peron, dan bukan pada jalan raya atau lintasan dimana vehicle stops).<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** untuk lokasi yang merupakan stops (`location_type=0`), stasiun (`location_type=1`) atau pintu masuk/keluar (`location_type=2`).<br> - Opsional untuk lokasi yang merupakan simpul umum (`location_type=3`) atau area keberangkatan (`location_type=4`).| 
 | `stop_lon| Bujur | **Wajib Bersyarat** | Bujur lokasi.<br><br> Untuk stops/platform (`location_type=0`) dan boarding area (`location_type=4`), koordinatnya harus berupa tiang bus — jika ada — dan lokasi penumpang menaiki vehicle (di trotoar atau peron, dan bukan pada jalan raya atau lintasan dimana vehicle stops).<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** untuk lokasi yang merupakan stops (`location_type=0`), stasiun (`location_type=1`) atau pintu masuk/keluar (`location_type=2`).<br> - Opsional untuk lokasi yang merupakan simpul umum (`location_type=3`) atau area keberangkatan (`location_type=4`). | 
 | `zone_id| tanda pengenal | Opsional | Mengidentifikasi zona tarif untuk berhenti. Jika catatan ini mewakili stasiun atau pintu masuk stasiun, `zone_id akan diabaikan.| 
 | `stop_url` | URL | Opsional | URL halaman web tentang lokasi. Nilai ini harus berbeda dengan nilai kolom `agency.agency_url dan `routes.route_url. | 
 | `location_type` | Jumlah | Opsional | Jenis lokasi. Opsi yang valid adalah:<br><br> `0` (atau kosong) - **Stop** (atau **Platform**). Lokasi di mana penumpang naik atau turun dari vehicle transit. Disebut platform ketika didefinisikan dalam `parent_station.<br> `1` - **Stasiun**. Struktur fisik atau area yang berisi satu atau lebih platform.<br> `2` - **Pintu Masuk/Keluar**. Lokasi di mana penumpang dapat masuk atau keluar stasiun dari jalan. Jika pintu masuk/keluar dimiliki oleh beberapa stasiun, maka stasiun tersebut dapat dihubungkan melalui pathways ke keduanya, namun penyedia data harus memilih salah satu dari stasiun tersebut sebagai induk.<br> `3` - **Node Generik**. Lokasi dalam stasiun, tidak cocok dengan `location_type` lainnya, yang dapat digunakan untuk menghubungkan pathways yang ditentukan di [pathways.txt](#pathwaystxt).<br> `4` - **Area Keberangkatan**. Lokasi tertentu pada suatu peron, tempat penumpang dapat menaiki dan/atau menurunkan kendaraan.| 
 | `parent_station| Referensi ID asing `stops.stop_id| **Wajib Bersyarat** | Mendefinisikan hierarki antara lokasi berbeda yang ditentukan di [stops.txt](#stopstxt). Ini berisi ID lokasi induk, sebagai berikut:<br><br> - **Stop/platform** (`location_type=0`): kolom `parent_station` berisi ID stasiun.<br> - **Stasiun** (`location_type=1`): kolom ini harus kosong.<br> - **Pintu masuk/keluar** (`location_type=2`) atau **generic node** (`location_type=3`): kolom `parent_station` berisi ID stasiun (`location_type=1`)<br> - **Boarding Area** (`location_type=4`): kolom `parent_station` berisi ID platform.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** untuk lokasi yang merupakan pintu masuk (`location_type=2`), node umum (`location_type=3`) atau area keberangkatan (`location_type=4`).<br> - Opsional untuk stops/platform (`location_type=0`).<br> - Dilarang untuk stasiun (`location_type=1`).| 
 | `stop_timezone| Zona Waktu | Opsional | Zona waktu lokasi. Jika lokasi memiliki stasiun induk, lokasi tersebut akan mewarisi zona waktu stasiun induk dan bukan menerapkan zona waktunya sendiri. Stasiun dan stops tanpa orang tua dengan `stop_timezone kosong mewarisi zona waktu yang ditentukan oleh `agency.agency_timezone. Waktu yang disediakan di [stop_times.txt](#stop_timestxt) berada dalam zona waktu yang ditentukan oleh `agency.agency_timezone`, bukan `stop_timezone`. Hal ini memastikan bahwa nilai waktu dalam perjalanan selalu meningkat selama perjalanan, terlepas dari zona waktu mana perjalanan tersebut dilintasi. | 
 | `wheelchair_boarding| Jumlah | Opsional | Menunjukkan apakah penumpangan kursi roda dapat dilakukan dari lokasi. Opsi yang valid adalah:<br><br> Untuk stops tanpa orang tua :<br> `0` atau kosong- Tidak ada informasi aksesibilitas untuk perhentian.<br> `1` - Beberapa kendaraan di halte ini dapat dinaiki oleh pengendara kursi roda.<br> `2` - Naik kursi roda tidak dapat dilakukan di halte ini.<br><br> Untuk stops anak :<br> `0` atau kosong- Berhenti akan mewarisi perilaku `wheelchair_boarding dari stasiun induk, jika ditentukan di stasiun induk.<br> `1` - Terdapat beberapa jalur yang dapat diakses dari luar stasiun ke pemberhentian/peron tertentu.<br> `2` - Tidak ada jalur yang dapat diakses dari luar stasiun ke halte/peron tertentu.<br><br> Untuk pintu masuk/keluar stasiun:<br> `0` atau kosong- Pintu masuk stasiun akan mewarisi perilaku `wheelchair_boarding dari stasiun induk, jika ditentukan untuk stasiun induk.<br> `1` - Pintu masuk stasiun dapat diakses oleh kursi roda.<br> `2` - Tidak ada jalur yang dapat diakses dari pintu masuk stasiun ke stops/platform. | 
 | `level_id| ID asing merujuk pada `levels.level_id| Opsional | Tingkat lokasi. Level yang sama dapat digunakan oleh beberapa stasiun yang tidak terhubung.| 
 | `platform_code| Text | Opsional | Pengidentifikasi peron untuk perhentian peron (perhentian milik suatu stasiun). Ini seharusnya hanya pengidentifikasi platform (mis. "G" atau "3"). Kata-kata seperti “platform” atau “track” (atau padanannya dalam bahasa tertentu pada feed) tidak boleh disertakan. Hal ini memungkinkan konsumen feed untuk lebih mudah menginternasionalkan dan melokalisasi pengidentifikasi platform ke dalam bahasa lain. | 
 
 
### routes.txt 
 
 File: **Wajib** 
 
 Kunci utama (`route_id`) 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `route_id` | ID Unik | **Wajib** | Mengidentifikasi rute. | 
 | `agency_id| ID asing yang merujuk pada `agency.agency_id| **Wajib Bersyarat** | Badan untuk rute yang ditentukan.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika beberapa agensi ditentukan di [agency.txt](#agencytxt).<br> - Direkomendasikan sebaliknya. | 
 | `route_short_name` | Text | **Wajib Bersyarat** | Nama pendek suatu rute. Seringkali merupakan pengidentifikasi singkat dan abstrak (misalnya, "32", "100X", "Hijau") yang digunakan pengendara untuk mengidentifikasi suatu rute. Baik `route_short_name dan `route_long_name dapat ditentukan.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika `routes.route_long_name kosong.<br> - Direkomendasikan jika ada peruntukan layanan singkat. Ini harus merupakan nama layanan yang umum diketahui penumpang, dan tidak boleh lebih dari 12 karakter. | 
 | `route_long_name` | Text | **Wajib Bersyarat** | Nama lengkap suatu rute. Nama ini umumnya lebih deskriptif daripada `route_short_name dan sering kali menyertakan tujuan atau perhentian rute. Baik `route_short_name dan `route_long_name dapat ditentukan.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika `routes.route_short_name kosong.<br> - Opsional sebaliknya. | 
 | `route_desc` | Text | Opsional | Deskripsi rute yang memberikan informasi berguna dan berkualitas. Tidak boleh merupakan duplikat dari `route_short_name atau `route_long_name.<hr> _Contoh: Kereta "A" beroperasi antara Inwood-207 St, Manhattan dan Far Rockaway-Mott Avenue, Queens setiap saat. Juga dari sekitar jam 6 pagi hingga sekitar tengah malam, kereta "A" tambahan beroperasi antara Inwood-207 St dan Lefferts Boulevard (kereta biasanya bergantian antara Lefferts Blvd dan Far Rockaway)._ | 
 | `route_type` | Jumlah | **Wajib** | Menunjukkan jenis transportasi yang digunakan pada suatu rute. Opsi yang valid adalah:<br><br> `0` - Trem, Trem, Kereta ringan. Sistem kereta api ringan atau jalan apa pun di wilayah metropolitan.<br> `1` - Kereta bawah tanah, Metro. Setiap sistem kereta bawah tanah dalam wilayah metropolitan.<br> `2` - Rel. Digunakan untuk perjalanan antar kota atau jarak jauh.<br> `3` - Bis. Digunakan untuk routes bus jarak pendek dan jarak jauh.<br> `4` - Feri. Digunakan untuk layanan perahu jarak pendek dan jarak jauh.<br> `5` - Trem kabel. Digunakan untuk gerbong kereta di permukaan jalan yang kabelnya dipasang di bawah vehicle (misalnya, kereta gantung di San Francisco).<br> `6` - Lift udara, kereta gantung (misalnya lift gondola, trem udara). Transportasi kabel dimana kabin, mobil, gondola atau kursi terbuka digantung dengan menggunakan satu atau lebih kabel.<br> `7` - Kereta kabel. Sistem rel apa pun yang dirancang untuk tanjakan curam.<br> `11` - Bus troli. Bus listrik yang mengambil tenaga dari kabel di atas kepala menggunakan tiang.<br> `12` - Monorel. Kereta api yang lintasannya terdiri dari satu rel atau balok. | 
 | `route_url` | URL | Opsional | URL halaman web tentang rute tertentu. Harus berbeda dengan nilai `agency.agency_url. | 
 | `route_color| Warna | Opsional | Penunjukan warna rute yang sesuai dengan material yang menghadap ke publik. Defaultnya berwarna putih (`FFFFFF) jika dihilangkan atau dibiarkan kosong. Perbedaan warna antara `route_color dan `route_text_color harus memberikan kontras yang cukup bila dilihat pada layar hitam putih. | 
 | `route_text_color` | Warna | Opsional | Warna yang dapat dibaca untuk digunakan pada teks yang digambar dengan latar belakang `route_color. Defaultnya berwarna hitam (`000000`) jika dihilangkan atau dibiarkan kosong. Perbedaan warna antara `route_color dan `route_text_color harus memberikan kontras yang cukup bila dilihat pada layar hitam putih. | 
 | `route_sort_order` | Bilangan bulat non-negatif | Opsional | Memesan routes dengan cara yang ideal untuk presentasi kepada pelanggan. Rute dengan nilai `route_sort_order yang lebih kecil harus ditampilkan terlebih dahulu. | 
 | `continuous_pickup` | Jumlah | **Dilarang Bersyarat** | Menunjukkan bahwa pengendara dapat menaiki vehicle transit kapan saja di sepanjang jalur perjalanan kendaraan seperti yang dijelaskan oleh [shapes.txt](#shapestxt), pada setiap perjalanan rute tersebut. Opsi yang valid adalah:<br><br> `0` - Pengambilan berhenti terus menerus.<br> `1` atau kosong- Tidak ada pengambilan yang berhenti terus menerus.<br> `2` - Harus menelepon agency untuk mengatur pengambilan berhenti terus menerus.<br> `3` - Harus berkoordinasi dengan pengemudi untuk mengatur penjemputan berhenti terus menerus.<br><br> Nilai untuk `routes.continuous_pickup dapat diganti dengan menentukan nilai dalam `stop_times.continuous_pickup untuk `stop_time tertentu di sepanjang rute.<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** jika `stop_times.start_pickup_drop_off_window` atau `stop_times.end_pickup_drop_off_window` ditentukan untuk setiap perjalanan pada rute ini.<br> - Opsional sebaliknya. | 
 | `continuous_drop_off| Jumlah | **Dilarang Bersyarat** | Menunjukkan bahwa pengendara dapat turun dari vehicle transit di titik mana pun di sepanjang jalur perjalanan kendaraan seperti yang dijelaskan oleh [shapes.txt](#shapestxt), pada setiap perjalanan rute tersebut. Opsi yang valid adalah:<br><br> `0` - Penghentian terus menerus.<br> `1` atau kosong- Tidak ada penghentian terus menerus.<br> `2` - Harus menelepon agency untuk mengatur penghentian terus menerus.<br> `3` - Harus berkoordinasi dengan pengemudi untuk mengatur penghentian terus menerus.<br><br> Nilai untuk `routes.continuous_drop_off dapat diganti dengan menentukan nilai dalam `stop_times.continuous_drop_off untuk `stop_time tertentu di sepanjang rute.<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** jika `stop_times.start_pickup_drop_off_window` atau `stop_times.end_pickup_drop_off_window` ditentukan untuk setiap perjalanan pada rute ini.<br> - Opsional sebaliknya. | 
 | `network_id| tanda pengenal | **Dilarang Bersyarat** | Mengidentifikasi sekelompok routes. Beberapa baris di [routes.txt](#routestxt) mungkin memiliki `network_id yang sama.<br><br> Dilarang Bersyarat:<br> - **Dilarang** jika file [route_networks.txt](#route_networkstxt) ada.<br> - Opsional sebaliknya. 
 
### trips.txt 
 
 File: **Wajib** 
 
 Kunci utama (`trip_id`) 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `route_id` | ID asing yang merujuk pada `routes.route_id| **Wajib** | Mengidentifikasi rute. | 
 | `service_id| Tanda pengenal asing yang merujuk pada `calendar.service_id atau `calendar_dates.service_id| **Wajib** | Mengidentifikasi serangkaian tanggal ketika layanan tersedia untuk satu atau lebih routes. | 
 | `trip_id` | ID Unik | **Wajib** | Mengidentifikasi perjalanan. | 
 | `trip_headsign| Text | Opsional | Text yang muncul pada papan tanda yang mengidentifikasi tujuan perjalanan bagi pengendara. Harus digunakan untuk membedakan pola pelayanan yang berbeda pada rute yang sama.<br><br> Jika tanda kepala berubah selama perjalanan, nilai untuk `trip_headsign dapat diganti dengan menentukan nilai dalam `stop_times.stop_headsign untuk `stop_time tertentu di sepanjang perjalanan. | 
 | `trip_short_name` | Text | Opsional | Teks yang menghadap publik digunakan untuk mengidentifikasi perjalanan penumpang, misalnya untuk mengidentifikasi nomor kereta untuk perjalanan kereta komuter. Jika pengendara biasanya tidak mengandalkan nama perjalanan, `trip_short_name harus kosong. Nilai `trip_short_name`, jika diberikan, harus secara unik mengidentifikasi perjalanan dalam hari layanan; ini tidak boleh digunakan untuk nama tujuan atau sebutan terbatas/tersurat. | 
 | `direction_id` | Jumlah | Opsional | Menunjukkan arah perjalanan untuk suatu perjalanan. Bidang ini tidak boleh digunakan dalam perutean; ini menyediakan cara untuk memisahkan perjalanan berdasarkan arah saat menerbitkan tabel waktu. Opsi yang valid adalah:<br><br> `0` - Perjalanan dalam satu arah (misalnya perjalanan keluar).<br> `1` - Bepergian ke arah berlawanan (misalnya perjalanan masuk).<hr> *Contoh: Bidang `trip_headsign` dan `direction_id` dapat digunakan bersama untuk menetapkan nama perjalanan di setiap arah untuk serangkaian perjalanan. File [trips.txt](#tripstxt) dapat berisi catatan berikut untuk digunakan dalam tabel waktu:*<br> `trip_id,...,trip_headsign,direction_id`<br> `1234,...,Airport,0`<br> `1505,...,Downtown,1` | 
 | `block_id| tanda pengenal | Opsional | Mengidentifikasi blok tempat perjalanan tersebut berada. Sebuah blok terdiri dari satu perjalanan atau beberapa perjalanan berurutan yang dilakukan menggunakan vehicle yang sama, ditentukan oleh hari layanan bersama dan `block_id. `block_id mungkin memiliki perjalanan dengan hari layanan berbeda, sehingga membuat blok berbeda. Lihat [contoh di bawah](#contoh-blok-dan-hari-layanan). Untuk memberikan informasi transfers di kursi, [transfers](#transferstxt) dari `transfer_type` `4` harus disediakan. | 
 | `shape_id` | ID asing yang merujuk pada `shapes.shape_id| **Wajib Bersyarat** | Mengidentifikasi shape geospasial yang menggambarkan jalur perjalanan vehicle untuk suatu perjalanan.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika perjalanan memiliki perilaku penjemputan atau pengantaran berkelanjutan yang ditentukan di [routes.txt](#routestxt) atau di [stop_times.txt](#stop_timestxt).<br> - Opsional sebaliknya. | 
 | `wheelchair_accessible| Jumlah | Opsional | Menunjukkan aksesibilitas kursi roda. Opsi yang valid adalah:<br><br> `0` atau kosong- Tidak ada informasi aksesibilitas untuk perjalanan.<br> `1` - Kendaraan yang digunakan pada perjalanan khusus ini dapat menampung setidaknya satu pengendara kursi roda.<br> `2` - Pengendara kursi roda tidak dapat diakomodasi dalam perjalanan ini. | 
 | `bikes_allowed| Jumlah | Opsional | Menunjukkan apakah sepeda diperbolehkan. Opsi yang valid adalah:<br><br> `0` atau kosong- Tidak ada informasi sepeda untuk perjalanan.<br> `1` - Kendaraan yang digunakan pada perjalanan khusus ini dapat menampung setidaknya satu sepeda.<br> `2` - Sepeda tidak diperbolehkan dalam perjalanan ini. | 
 
#### Contoh: Blok dan hari layanan 
 
 Contoh di bawah ini valid, dengan blok berbeda setiap hari dalam seminggu. 
 
 | route_id | trip_id | service_id | block_id | <span style="font-weight:normal">*(waktu perhentian pertama)*</span> | <span style="font-weight:normal">*(waktu perhentian terakhir)*</span> | 
 |----------|---------|--------------------------------|----------|-----------------------------------------|-------------------------| 
 | merah | trip_1 | Senin-Selasa-Rabu-Kamis-Jumat-Sabtu-Minggu | lingkaran_merah | 22:00:00 | 22:55:00 | 
 | merah | trip_2 | Jumat-Sabtu-Minggu | lingkaran_merah | 23:00:00 | 23:55:00 | 
 | merah | trip_3 | jumat-sabtu | lingkaran_merah | 24:00:00 | 24:55:00 | 
 | merah | trip_4 | Senin-Selasa-Rabu-Kamis | lingkaran_merah | 20:00:00 | 20:50:00 | 
 | merah | trip_5 | Senin-Selasa-Rabu-Kamis | lingkaran_merah | 21:00:00 | 21:50:00 | 
 
 Catatan pada tabel di atas: 
 
 * Pada hari Jumat hingga Sabtu pagi, misalnya, satu vehicle mengoperasikan `trip_1, `trip_2, dan `trip_3(22:00 hingga 12:55). Perhatikan bahwa perjalanan terakhir dilakukan pada hari Sabtu, pukul 00:00 hingga 00:55, namun merupakan bagian dari “hari kebaktian” hari Jumat karena waktunya adalah pukul 24:00:00 hingga 24:55:00. 
 * Pada hari Senin, Selasa, Rabu, dan Kamis, satu vehicle mengoperasikan `trip_1, `trip_4, dan `trip_5 dalam satu blok mulai pukul 20.00 hingga 22.55. 
 
### stop_times.txt 
 
 File: **Wajib** 
 
 Kunci utama (`trip_id`, `stop_sequence`) 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `trip_id` | ID asing yang merujuk pada `trips.trip_id` | **Wajib** | Mengidentifikasi perjalanan. | 
 | `arrival_time| Waktu | **Wajib Bersyarat** | Waktu tiba di halte (ditentukan oleh `stop_times.stop_id) untuk perjalanan tertentu (ditentukan oleh `stop_times.trip_id) dalam zona waktu yang ditentukan oleh `agency.agency_timezone, bukan `stops.stop_timezone.<br><br> Jika tidak ada waktu terpisah untuk arrival dan departure di halte, `arrival_time dan `departure_time` harus sama.<br><br> Untuk waktu yang terjadi setelah tengah malam pada hari layanan, masukkan waktu dengan nilai yang lebih besar dari 24:00:00 dalam JJ:MM:SS.<br><br> Jika waktu arrival dan departure yang tepat (`timepoint=1` atau kosong) tidak tersedia, perkiraan atau waktu arrival dan departure yang diinterpolasi (`timepoint=0`) harus diberikan.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** untuk perhentian pertama dan terakhir dalam sebuah perjalanan (ditentukan oleh `stop_times.stop_sequence`).<br> - **Wajib** untuk `timepoint=1`.<br> - **Dilarang** ketika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - Opsional sebaliknya.| 
 | `departure_time` | Waktu | **Wajib Bersyarat** | Waktu keberangkatan dari perhentian (ditentukan oleh `stop_times.stop_id) untuk perjalanan tertentu (ditentukan oleh `stop_times.trip_id) dalam zona waktu yang ditentukan oleh `agency.agency_timezone, bukan `stops.stop_timezone.<br><br> Jika tidak ada waktu terpisah untuk arrival dan departure di halte, `arrival_time dan `departure_time` harus sama.<br><br> Untuk waktu yang terjadi setelah tengah malam pada hari layanan, masukkan waktu dengan nilai yang lebih besar dari 24:00:00 dalam JJ:MM:SS.<br><br> Jika waktu arrival dan departure yang tepat (`timepoint=1` atau kosong) tidak tersedia, perkiraan atau waktu arrival dan departure yang diinterpolasi (`timepoint=0`) harus diberikan.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** untuk `timepoint=1`.<br> - **Dilarang** ketika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - Opsional sebaliknya. | 
 | `stop_id` | Referensi ID asing `stops.stop_id| **Wajib Bersyarat** | Mengidentifikasi perhentian yang dilayani. Semua stops yang dilayani selama perjalanan harus memiliki catatan di [stop_times.txt](#stop_timestxt). Lokasi yang direferensikan harus berupa stops/platform, yaitu nilai `stops.location_type harus `0` atau kosong. Sebuah perhentian dapat dilayani beberapa kali dalam perjalanan yang sama, dan beberapa perjalanan serta routes dapat melayani pemberhentian yang sama.<br><br> Layanan berdasarkan permintaan yang menggunakan stops harus direferensikan dalam urutan layanan yang tersedia di stops tersebut. Konsumen data harus berasumsi bahwa perjalanan dapat dilakukan dari satu perhentian atau lokasi ke perhentian atau lokasi mana pun di kemudian hari dalam perjalanan, dengan ketentuan bahwa `pickup/drop_off_type` dari setiap stop_time dan batasan waktu dari setiap `start/end_pickup_drop_off_window` tidak melarangnya .<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika `stop_times.location_group_id` DAN `stop_times.location_id` TIDAK ditentukan.<br> - **Dilarang** jika `stop_times.location_group_id` atau `stop_times.location_id` ditentukan. | 
 | `lokasi_grup_id` | ID asing yang merujuk pada `location_groups.location_group_id` | **Dilarang Bersyarat** | Mengidentifikasi grup lokasi yang dilayani yang menunjukkan grup stops di mana pengendara dapat meminta penjemputan atau pengantaran. Semua grup lokasi yang dilayani selama perjalanan harus memiliki catatan di [stop_times.txt](#stop_timestxt). Beberapa perjalanan dan routes mungkin melayani grup lokasi yang sama.<br><br> Layanan berdasarkan permintaan yang menggunakan grup lokasi harus direferensikan dalam urutan layanan yang tersedia di grup lokasi tersebut. Konsumen data harus berasumsi bahwa perjalanan dapat dilakukan dari satu perhentian atau lokasi ke perhentian atau lokasi mana pun di kemudian hari dalam perjalanan, dengan ketentuan bahwa `pickup/drop_off_type` dari setiap stop_time dan batasan waktu dari setiap `start/end_pickup_drop_off_window` tidak melarangnya .<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** jika `stop_times.stop_id` atau `stop_times.location_id` ditentukan. | 
 | `lokasi_id` | ID asing yang mereferensikan `id` dari `locations.geojson` | **Dilarang Bersyarat** | Mengidentifikasi lokasi GeoJSON yang sesuai dengan zona layanan tempat pengendara dapat meminta penjemputan atau pengantaran. Semua lokasi GeoJSON yang dilayani selama perjalanan harus memiliki catatan di [stop_times.txt](#stop_timestxt). Beberapa perjalanan dan routes mungkin melayani lokasi GeoJSON yang sama.<br><br> Layanan berdasarkan permintaan di lokasi harus dirujuk sesuai urutan layanan yang tersedia di lokasi tersebut. Konsumen data harus berasumsi bahwa perjalanan dapat dilakukan dari satu perhentian atau lokasi ke perhentian atau lokasi mana pun di kemudian hari dalam perjalanan, dengan ketentuan bahwa `pickup/drop_off_type` dari setiap stop_time dan batasan waktu dari setiap `start/end_pickup_drop_off_window` tidak melarangnya .<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** jika `stop_times.stop_id atau `stop_times.location_group_id` ditentukan. | 
 | `stop_sequence` | Bilangan bulat non-negatif | **Wajib** | Urutan stops, grup lokasi, atau lokasi GeoJSON untuk perjalanan tertentu. Nilainya harus meningkat sepanjang perjalanan tetapi tidak harus berturut-turut.<hr> *Contoh: Lokasi pertama dalam perjalanan dapat memiliki `stop_sequence`= `1`, lokasi kedua dalam perjalanan dapat memiliki `stop_sequence`=`23`, lokasi ketiga dapat memiliki `stop_sequence`=`40`, dan seterusnya.*<br><br> Perjalanan dalam grup lokasi atau lokasi GeoJSON yang sama memerlukan dua catatan di [stop_times.txt](#stop_timestxt) dengan `location_group_id` atau `location_id` yang sama. | 
 | `stop_headsign` | Text | Opsional | Text yang muncul pada papan tanda yang mengidentifikasi tujuan perjalanan bagi pengendara. Bidang ini menggantikan `trips.trip_headsign default ketika tanda kepala berubah di antara stops. Jika tanda kepala ditampilkan untuk seluruh perjalanan, `trips.trip_headsign harus digunakan.<br><br> Nilai `stop_headsign` yang ditentukan untuk satu `stop_time` tidak berlaku untuk `stop_time` berikutnya dalam perjalanan yang sama. Jika Anda ingin mengganti `trip_headsign untuk beberapa `stop_time dalam perjalanan yang sama, nilai `stop_headsign harus repeated di setiap baris `stop_time. | 
 | `start_pickup_drop_off_window` | Waktu | **Wajib Bersyarat** | Waktu saat layanan sesuai permintaan tersedia di lokasi GeoJSON, grup lokasi, atau perhentian.<br><br> **Diwajibkan Secara Bersyarat**:<br> - **Wajib** jika `stop_times.location_group_id` atau `stop_times.location_id` ditentukan.<br> - **Wajib** jika `end_pickup_drop_off_window` ditentukan.<br> - **Dilarang** jika `arrival_time atau `departure_time` ditentukan.<br> - Opsional sebaliknya. | 
 | `end_pickup_drop_off_window` | Waktu | **Wajib Bersyarat** | Waktu saat layanan sesuai permintaan berakhir di lokasi GeoJSON, grup lokasi, atau perhentian.<br><br> **Diwajibkan Secara Bersyarat**:<br> - **Wajib** jika `stop_times.location_group_id` atau `stop_times.location_id` ditentukan.<br> - **Wajib** jika `start_pickup_drop_off_window` ditentukan.<br> - **Dilarang** jika `arrival_time atau `departure_time` ditentukan.<br> - Opsional sebaliknya. | 
 | `pickup_type` | Jumlah | **Dilarang Bersyarat** | Menunjukkan metode pengambilan. Opsi yang valid adalah:<br><br> `0` atau kosong- Pengambilan terjadwal secara rutin.<br> `1` - Tidak tersedia penjemputan.<br> `2` - Harus menelepon agency untuk mengatur penjemputan.<br> `3` - Harus berkoordinasi dengan pengemudi untuk mengatur penjemputan.<br><br> **Dilarang Bersyarat**:<br> - `pickup_type=0` **dilarang** jika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - `pickup_type=3` **dilarang** jika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - Opsional sebaliknya. | 
 | `drop_off_type` | Jumlah | **Dilarang Bersyarat** | Menunjukkan metode pengantaran. Opsi yang valid adalah:<br><br> `0` atau kosong- Pengantaran yang dijadwalkan secara rutin.<br> `1` - Tidak tersedia pengantaran.<br> `2` - Harus menelepon agency untuk mengatur pengantaran.<br> `3` - Harus berkoordinasi dengan pengemudi untuk mengatur pengantaran.<br><br> **Dilarang Bersyarat**:<br> - `drop_off_type=0` **dilarang** jika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - Opsional sebaliknya. | 
 | `continuous_pickup` | Jumlah | **Dilarang Bersyarat** | Menunjukkan bahwa pengendara dapat menaiki vehicle transit kapan saja di sepanjang jalur perjalanan kendaraan seperti yang dijelaskan oleh [shapes.txt](#shapestxt), dari `stop_time` ini ke `stop_time` berikutnya dalam `stop_sequence` perjalanan. Opsi yang valid adalah:<br><br> `0` - Pengambilan berhenti terus menerus.

br> `1` atau kosong- Tidak ada pengambilan yang berhenti terus menerus.<br> `2` - Harus menelepon agency untuk mengatur pengambilan berhenti terus menerus.<br> `3` - Harus berkoordinasi dengan pengemudi untuk mengatur penjemputan berhenti terus menerus.<br><br> Jika bidang ini diisi, bidang ini akan menggantikan perilaku pengambilan berkelanjutan yang ditentukan di [routes.txt](#routestxt). Jika kolom ini kosong, `stop_time` mewarisi perilaku pengambilan berkelanjutan yang ditentukan di [routes.txt](#routestxt).<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** jika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - Opsional sebaliknya. | 
 | `continuous_drop_off| Jumlah | **Dilarang Bersyarat** | Menunjukkan bahwa pengendara dapat turun dari vehicle transit di titik mana pun di sepanjang jalur perjalanan kendaraan seperti yang dijelaskan oleh [shapes.txt](#shapestxt), dari `stop_time` ini ke `stop_time` berikutnya dalam `stop_sequence` perjalanan. Opsi yang valid adalah:<br><br> `0` - Penghentian terus menerus.<br> `1` atau kosong- Tidak ada penghentian terus menerus.<br> `2` - Harus menelepon agency untuk mengatur penghentian terus menerus.<br> `3` - Harus berkoordinasi dengan pengemudi untuk mengatur penghentian terus menerus.<br><br> Jika bidang ini diisi, bidang ini akan menggantikan perilaku pengantaran terus-menerus yang ditentukan di [routes.txt](#routestxt). Jika bidang ini kosong, `stop_time` mewarisi perilaku pengantaran terus-menerus yang ditentukan di [routes.txt](#routestxt).<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** jika `start_pickup_drop_off_window` atau `end_pickup_drop_off_window` ditentukan.<br> - Opsional sebaliknya. | 
 | `shape_dist_traveled| float non-negatif | Opsional | Jarak sebenarnya yang ditempuh sepanjang shape terkait, dari perhentian pertama hingga perhentian yang ditentukan dalam rekaman ini. Bidang ini menentukan seberapa banyak shape yang akan ditarik di antara dua stops selama perjalanan. Harus dalam satuan yang sama dengan yang digunakan di [shapes.txt](#bentuktxt). Nilai yang digunakan untuk `shape_dist_traveled` harus bertambah seiring dengan `stop_sequence`; mereka tidak boleh digunakan untuk menunjukkan perjalanan mundur sepanjang suatu rute.<br><br> Direkomendasikan untuk routes yang memiliki looping atau inlining ( vehicle melintasi atau melewati bagian alinyemen yang sama dalam satu perjalanan). Lihat [`shapes.shape_dist_traveled`](#shapestxt).<hr> *Contoh: Jika sebuah bus menempuh jarak 5,25 kilometer dari awal shape hingga berhenti,`shape_dist_traveled`=`5.25`.*| 
 | `timepoint` | Jumlah | Direkomendasikan | Menunjukkan apakah waktu arrival dan departure untuk pemberhentian benar-benar dipatuhi oleh vehicle atau justru merupakan perkiraan dan/atau waktu interpolasi. Kolom ini memungkinkan produsen GTFS memberikan waktu perhentian yang diinterpolasi, sekaligus menunjukkan bahwa waktunya merupakan perkiraan. Opsi yang valid adalah:<br><br> `0` - Waktu dianggap perkiraan.<br> `1` atau kosong- Waktu dianggap tepat. | 
 | `pickup_booking_rule_id` | ID merujuk pada `booking_rules.booking_rule_id` | Opsional | Mengidentifikasi aturan pemesanan boarding pada waktu perhentian ini.<br><br> Direkomendasikan ketika `pickup_type=2`. | 
 | `drop_off_booking_rule_id` | ID merujuk pada `booking_rules.booking_rule_id` | Opsional | Mengidentifikasi aturan pemesanan turun pada waktu perhentian ini.<br><br> Direkomendasikan ketika `drop_off_type=2`. | 
 
#### Perilaku Perutean Layanan Berdasarkan Permintaan- Saat menyediakan perutean atau waktu perjalanan antara asal dan tujuan, konsumen data harus mengabaikan catatan stop_times.txt perantara dengan `trip_id` yang sama yang memiliki `start_pickup_drop_off_window` dan `end_pickup_drop_off_window` ditentukan. Untuk contoh yang menunjukkan apa yang harus diabaikan, lihat [halaman contoh data](../examples/flex/#ignoring-intermediate-stop-times-records-with-pickupdrop-off-windows). 
 - Tumpang tindih secara bersamaan geometri locations.geojson `id`, `start/end_pickup_drop_off_window` waktu, dan `pickup_type` atau `drop_off_type` antara dua atau lebih catatan stop_times.txt dengan `trip_id` yang sama dilarang. Untuk contoh yang menunjukkan apa yang dilarang, lihat [halaman contoh data](../examples/flex/#zone-overlap-constraint). 
 
### calendar.txt 
 
 File: **Diperlukan Secara Bersyarat** 
 
 Kunci utama (`service_id`) 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `service_id| ID Unik | **Wajib** | Mengidentifikasi serangkaian tanggal ketika layanan tersedia untuk satu atau lebih routes. | 
 | `monday| Jumlah | **Wajib** | Menunjukkan apakah layanan beroperasi setiap hari Senin dalam rentang date yang ditentukan oleh kolom `start_date` dan `end_date. Perhatikan bahwa pengecualian untuk tanggal tertentu mungkin tercantum di [calendar_dates.txt](#calendar_datestxt). Opsi yang valid adalah:<br><br> `1` - Layanan tersedia untuk semua hari Senin dalam rentang date tersebut.<br> `0` - Layanan tidak tersedia untuk hari Senin dalam rentang date tersebut. | 
 | `tuesday| Jumlah | **Wajib** | Fungsinya sama seperti `monday` kecuali berlaku pada hari Selasa | 
 | `wednesday` | Jumlah | **Wajib** | Fungsinya sama seperti `monday` kecuali berlaku pada hari Rabu | 
 | `thursday| Jumlah | **Wajib** | Fungsinya sama seperti `monday` kecuali berlaku pada hari Kamis | 
 | `friday| Jumlah | **Wajib** | Fungsinya sama seperti `monday` kecuali berlaku pada hari Jumat | 
 | `saturday` | Jumlah | **Wajib** | Fungsinya sama seperti `monday` kecuali berlaku pada hari Sabtu. | 
 | `sunday` | Jumlah | **Wajib** | Fungsinya sama seperti `monday` kecuali berlaku pada hari Minggu. | 
 | `start_date` | Tanggal | **Wajib** | Mulai hari servis untuk interval servis. | 
 | `end_date| Tanggal | **Wajib** | Akhiri hari servis untuk interval servis. Hari pelayanan ini termasuk dalam interval tersebut. | 
 
### calendar_dates.txt 
 
 File: **Diperlukan Secara Bersyarat** 
 
 Kunci utama (`service_id, `date) 
 
 [calendar_dates.txt](#calendar_datestxt ) tabel secara eksplisit mengaktifkan atau menonaktifkan layanan berdasarkan date. Ini dapat digunakan dalam dua cara. 
 
 * Direkomendasikan: Gunakan [calendar_dates.txt](#calendar_datestxt) bersama dengan [calendar.txt](#calendartxt) untuk menentukan pengecualian terhadap pola layanan default yang ditentukan dalam [calendar.txt](#calendartxt). Jika layanan umumnya teratur, dengan sedikit perubahan pada tanggal tertentu (misalnya, untuk mengakomodasi acara khusus, atau jadwal sekolah), ini merupakan pendekatan yang baik. Dalam hal ini `calendar_dates.service_id adalah ID asing yang merujuk pada `calendar.service_id. 
 * Alternatif: Hilangkan [calendar.txt](#calendartxt), dan tentukan setiap date layanan di [calendar_dates.txt](#calendar_datestxt). Hal ini memungkinkan adanya variasi layanan yang cukup besar dan mengakomodasi layanan tanpa jadwal mingguan normal. Dalam hal ini `service_id adalah ID. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `service_id| ID asing yang merujuk pada `calendar.service_id atau ID | **Wajib** | Mengidentifikasi serangkaian tanggal ketika pengecualian layanan terjadi untuk satu atau lebih routes. Setiap pasangan (`service_id`, `date`) hanya dapat muncul satu kali dalam [calendar_dates.txt](#calendar_datestxt) jika menggunakan [calendar.txt](#calendartxt) dan [calendar_dates.txt](#calendar_datestxt) bersamaan. Jika nilai `service_id muncul di [calendar.txt](#calendartxt) dan [calendar_dates.txt](#calendar_datestxt), informasi di [calendar_dates.txt](#calendar_datestxt) mengubah informasi layanan yang ditentukan dalam [calendar.txt](#kalendertxt). | 
 | `date| Tanggal | **Wajib** | Tanggal ketika pengecualian layanan terjadi. | 
 | `exception_type` | Jumlah | **Wajib** | Menunjukkan apakah layanan tersedia pada date yang ditentukan di kolom date. Opsi yang valid adalah:<br><br> `1` - Layanan telah ditambahkan untuk date yang ditentukan.<br> `2` - Layanan telah dihapus untuk date yang ditentukan.<hr> *Contoh: Misalkan suatu rute memiliki satu rangkaian perjalanan yang tersedia pada hari libur dan rangkaian perjalanan lainnya yang tersedia pada hari lainnya. Satu `service_id bisa berhubungan dengan jadwal layanan reguler dan `service_id lainnya bisa berhubungan dengan jadwal hari libur. Untuk hari libur tertentu, file [calendar_dates.txt](#calendar_datestxt) dapat digunakan untuk menambahkan hari libur ke hari libur `service_id dan untuk menghapus hari libur dari jadwal `service_id reguler.* | 
 
### fare_attributes.txt 
 
 File: **Opsional** 
 
 Kunci utama (`fare_id`) 
 
 **Versi**<br> 
 Ada dua opsi pemodelan untuk mendeskripsikan tarif. GTFS- Fares V1 adalah opsi lama untuk menjelaskan informasi tarif minimal. GTFS- Fares V2 adalah metode terbaru yang memungkinkan penghitungan lebih detail mengenai struktur tarif suatu biro iklan. Keduanya diperbolehkan untuk ada dalam kumpulan data, namun hanya satu metode yang boleh digunakan oleh konsumen data untuk kumpulan data tertentu. Direkomendasikan agar GTFS- Fares V2 diutamakan dibandingkan GTFS- Fares V1.<br><br> File yang terkait dengan GTFS- Fares V1 adalah:<br> - [fare_attributes.txt](#fare_attributestxt)<br> - [fare_rules.txt](#fare_rulestxt)<br><br> File yang terkait dengan GTFS- Fares V2 adalah:<br> - [tarif_media.txt](#tarif_mediatxt)<br> - [fare_products.txt](#fare_productstxt)<br> - [fare_leg_rules.txt](#fare_leg_rulestxt)<br> - [fare_transfer_rules.txt](#fare_transfer_rulestxt) 
 
<br> 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `fare_id| ID Unik | **Wajib** | Mengidentifikasi kelas tarif. | 
 | `price| float non-negatif | **Wajib** | price tarif, dalam satuan yang ditentukan oleh `currency_type. | 
 | `currency_type` | Kode mata uang | **Wajib** | Mata uang yang digunakan untuk membayar ongkos. | 
 | `payment_method| Jumlah | **Wajib** | Menunjukkan kapan tarif harus dibayar. Opsi yang valid adalah:<br><br> `0` - Tarif dibayar di pesawat.<br> `1` - Tarif harus dibayar sebelum naik ke pesawat. | 
 | `transfers| Jumlah | **Wajib** | Menunjukkan jumlah transfers yang diizinkan pada tarif ini. Opsi yang valid adalah:<br><br> `0` - Tidak ada transfers yang diizinkan pada tarif ini.<br> `1` - Pengendara dapat berpindah satu kali.<br> `2` - Pengendara dapat berpindah dua kali.<br> kosong- transfers tanpa batas diperbolehkan. | 
 | `agency_id| ID asing yang merujuk pada `agency.agency_id| **Wajib Bersyarat** | Mengidentifikasi agency terkait untuk tarif.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika beberapa agensi ditentukan di [agency.txt](#agencytxt).<br> - Direkomendasikan sebaliknya. | 
 | `transfer_duration| Bilangan bulat non-negatif | Opsional | Durasi waktu dalam detik sebelum transfer berakhir. Ketika `transfers`=`0` kolom ini dapat digunakan untuk menunjukkan berapa lama tiket berlaku atau mungkin dibiarkan kosong. | 
 
### fare_rules.txt 
 
 File: **Opsional** 
 
 Kunci utama (`*`) 
 
 Tabel [fare_rules.txt](#fare_rulestxt) menentukan tarif di [fare_attributes.txt](#fare_attributestxt) berlaku untuk rencana perjalanan. Kebanyakan struktur tarif menggunakan beberapa kombinasi aturan berikut: 
 
 * Tarif bergantung pada stasiun asal atau tujuan. 
 * Tarif tergantung pada zona mana yang dilalui rencana perjalanan. 
 * Tarif tergantung pada rute mana yang digunakan rencana perjalanan. 
 
 Untuk contoh yang menunjukkan cara menentukan struktur tarif dengan [fare_rules.txt](#fare_rulestxt) dan [fare_attributes.txt](#fare_attributestxt), lihat [FareExamples](https://web.archive.org/web/20111207224351/https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) di wiki proyek sumber terbuka GoogleTransitDataFeed. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `fare_id| ID asing yang merujuk pada `fare_attributes.fare_id` | **Wajib** | Mengidentifikasi kelas tarif. | 
 | `route_id` | ID asing yang merujuk pada `routes.route_id| Opsional | Mengidentifikasi rute yang terkait dengan kelas tarif. Jika ada beberapa routes dengan atribut tarif yang sama, buat catatan di [fare_rules.txt](#fare_rulestxt) untuk setiap rute.<hr> *Contoh: Jika kelas tarif "b" valid pada rute "TSW" dan "TSE", file [fare_rules.txt](#fare_rulestxt) akan berisi catatan kelas tarif berikut:*<br> ` fare_id,route_id`<br> `b,TSW<br> `b,TSE| 
 | `origin_id| Referensi ID asing `stops.zone_id| Opsional | Mengidentifikasi zona asal. Jika kelas tarif memiliki beberapa zona asal, buat catatan di [fare_rules.txt](#fare_rulestxt) untuk setiap `origin_id`.<hr> *Contoh: Jika kelas tarif "b" berlaku untuk semua perjalanan yang berasal dari zona "2" atau zona "8", file [fare_rules.txt](#fare_rulestxt) akan berisi catatan kelas tarif berikut:*<br> `fare_id,...,origin_id`<br> `b,...,2<br> `b,...,8| 
 | `destination_id| Referensi ID asing `stops.zone_id| Opsional | Mengidentifikasi zona tujuan. Jika kelas tarif memiliki beberapa zona tujuan, buat catatan di [fare_rules.txt](#fare_rulestxt) untuk setiap `destination_id`.<hr> *Contoh: Bidang `origin_id` dan `destination_id` dapat digunakan bersama-sama untuk menentukan bahwa kelas tarif "b" berlaku untuk perjalanan antara zona 3 dan 4, dan untuk perjalanan antara zona 3 dan 5, [fare_rules.txt]( File#fare_rulestxt) akan berisi catatan berikut untuk kelas tarif:*<br> `fare_id,...,origin_id,destination_id`<br> `b,...,3,4<br> `b,...,3,5| 
 | `contains_id` | Referensi ID asing `stops.zone_id| Opsional | Mengidentifikasi zona yang akan dimasuki penumpang saat menggunakan kelas tarif tertentu. Digunakan di beberapa sistem untuk menghitung kelas tarif yang benar.<hr> *Contoh: Jika kelas tarif "c" dikaitkan dengan semua perjalanan pada rute GRT yang melewati zona 5, 6, dan 7, maka [fare_rules.txt](#fare_rulestxt) akan berisi catatan berikut:*<br> `fare_id,route_id,...,contains_id`<br> `c,GRT,...,5<br> `c,GRT,...,6<br> `c,GRT,...,7<br> *Karena semua zona `contains_id harus cocok agar tarif dapat diterapkan, rencana perjalanan yang melewati zona 5 dan 6 namun bukan zona 7 tidak akan memiliki kelas tarif "c". Untuk detail selengkapnya, lihat [https://code.google.com/p/googletransitdatafeed/wiki/FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) di wiki proyek GoogleTransitDataFeed.* | 
 
### jangka waktu.txt 
 
 File: **Opsional** 
 
 Kunci utama (`*`) 
 
 Digunakan untuk mendeskripsikan tarif yang dapat bervariasi berdasarkan waktu, hari dalam seminggu, atau hari tertentu dalam setahun. Jangka waktu dapat dikaitkan dengan produk tarif di [fare_leg_rules.txt](#fare_leg_rulestxt).<br> 
 Tidak boleh ada interval waktu yang tumpang tindih untuk nilai `timeframe_group_id dan `service_id yang sama. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `timeframe_group_id` | tanda pengenal | **Wajib** | Mengidentifikasi jangka waktu atau serangkaian jangka waktu. | 
 | `start_time` | Waktu | **Wajib Bersyarat** | Mendefinisikan awal jangka waktu. Interval tersebut mencakup waktu mulai.<br> Nilai yang lebih besar dari `24:00:00` dilarang. Nilai kosong di `start_time` dianggap `00:00:00`.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika `timeframes.end_time` ditentukan.<br> - **Dilarang** jika tidak | 
 | `end_time| Waktu | **Wajib Bersyarat** | Mendefinisikan akhir jangka waktu. Intervalnya tidak termasuk waktu berakhirnya.<br> Nilai yang lebih besar dari `24:00:00` dilarang. Nilai kosong di `end_time dianggap `24:00:00`.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika `timeframes.start_time` ditentukan.<br> - **Dilarang** jika tidak | 
 | `service_id| Tanda pengenal asing yang merujuk pada `calendar.service_id atau `calendar_dates.service_id| **Wajib** | Mengidentifikasi serangkaian tanggal di mana jangka waktu berlaku. | 
 
#### Semantik Waktu Lokal Jangka Waktu- Saat mengevaluasi waktu kejadian tarif terhadap [jangka waktu.txt](#timeframestxt), waktu kejadian dihitung dalam waktu lokal menggunakan zona waktu lokal, sebagaimana ditentukan oleh `stop_timezone`, jika ditentukan, dari pemberhentian atau stasiun induk untuk acara tarif. Jika tidak ditentukan, zona waktu agency feed harus digunakan. 
 - “Hari ini” adalah date saat ini dari waktu kejadian tarif, dihitung relatif terhadap zona waktu lokal. “Hari ini” mungkin berbeda dengan hari layanan perjalanan dengan tarif, terutama untuk perjalanan yang melebihi tengah malam. 
 - “Waktu dalam sehari” untuk peristiwa tarif dihitung relatif terhadap “hari ini” menggunakan semantik jenis kolom Waktu GTFS. 
 
### fare_media.txt 
 
 File: **Opsional** 
 
 Kunci utama (`fare_media_id`) 
 
 Untuk menjelaskan berbagai media tarif yang dapat digunakan untuk menggunakan produk tarif. Media tarif adalah pemegang fisik atau virtual yang digunakan untuk representasi dan/atau validasi suatu produk tarif. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `fare_media_id| ID Unik | **Wajib** | Mengidentifikasi media tarif. | 
 | `fare_media_name| Text | Opsional | Nama media tarif.<br><br> Untuk media tarif yang merupakan kartu transit (`fare_media_type =2`) atau aplikasi seluler (`fare_media_type =4`), `fare_media_name` harus disertakan dan harus sesuai dengan nama penumpang yang digunakan oleh organisasi yang mengantarkannya. | 
 | `fare_media_type` | Jumlah | **Wajib** | Jenis media tarif. Opsi yang valid adalah:<br><br> `0` - Tidak ada. Digunakan ketika tidak ada media tarif yang terlibat dalam pembelian atau validasi produk tarif, seperti membayar tunai kepada pengemudi atau kondektur tanpa menyediakan tiket fisik.<br> `1` - Tiket kertas fisik yang memungkinkan penumpang melakukan sejumlah perjalanan yang telah dibeli sebelumnya atau perjalanan tak terbatas dalam jangka waktu tertentu.<br> `2` - Kartu transit fisik yang menyimpan tiket, tiket masuk, atau nilai uang.<br> `3` - cEMV (Europay, Mastercard, dan Visa nirkontak) sebagai wadah token loop terbuka untuk tiket berbasis akun.<br> `4` - Aplikasi seluler yang menyimpan kartu transit virtual, tiket, tiket masuk, atau nilai uang.| 
 
### fare_products.txt 
 
 File: **Opsional** 
 
 Kunci utama (`fare_product_id`, `fare_media_id`) 
 
 Digunakan untuk menggambarkan kisaran tarif yang tersedia untuk dibeli oleh penumpang atau diperhitungkan saat menghitung total tarif untuk perjalanan dengan banyak jalur, seperti biaya transfer. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `fare_product_id| tanda pengenal | **Wajib** | Mengidentifikasi produk tarif atau serangkaian produk tarif.<br><br> Beberapa catatan di [fare_products.txt](#fare_productstxt) dapat berbagi `fare_product_id` yang sama, dalam hal ini semua catatan dengan ID tersebut akan diambil ketika direferensikan dari file lain.<br><br> Beberapa catatan mungkin memiliki `fare_product_id yang sama tetapi dengan `fare_media_id yang berbeda, yang menunjukkan berbagai metode yang tersedia untuk menggunakan produk tarif, kemungkinan dengan harga berbeda. | 
 | `fare_product_name| Text | Opsional | Nama produk tarif yang ditampilkan kepada penumpang. | 
 | `fare_media_id| Referensi ID asing `fare_media.fare_media_id` | Opsional | Mengidentifikasi media tarif yang dapat digunakan untuk menggunakan produk tarif selama perjalanan. Jika `fare_media_id kosong, media tarif dianggap tidak diketahui.| 
 | `amount` | amount mata uang | **Wajib** | Biaya produk tarif. Mungkin negatif untuk mewakili diskon transfer. Mungkin nol untuk mewakili produk tarif yang gratis. | 
 | `currency| Kode mata uang | **Wajib** | currency biaya produk tarif. | 
 
 
### fare_leg_rules.txt 
 
 File: **Opsional** 
 
 Kunci utama (`network_id, from_area_id, to_area_id, from_timeframe_group_id, to_timeframe_group_id, fare_product_id`) 
 
 Aturan tarif untuk perjalanan individu. 
 
 Tarif di [`fare_leg_rules.txt`](#fare_leg_rulestxt) harus ditanyakan dengan memfilter semua catatan dalam file untuk menemukan aturan yang cocok dengan jalur yang akan dilalui oleh pengendara. 
 
 Untuk memproses biaya perjalanan: 
 
 1. File [fare_leg_rules.txt](#fare_leg_rulestxt) harus disaring berdasarkan kolom yang menentukan karakteristik perjalanan, kolom tersebut adalah: 
 - `fare_leg_rules.network_id` 
 - `fare_leg_rules.from_area_id` 
 - `fare_leg_rules.to_area_id` 
 - `fare_leg_rules.from_timeframe_group_id` 
 - `fare_leg_rules.to_timeframe_group_id` 
<br/> 
 
 2. Jika perjalanan sama persis dengan catatan di [fare_leg_rules.txt](#fare_leg_rulestxt) berdasarkan karakteristik perjalanan, catatan tersebut harus diproses untuk menentukan biaya perjalanan. File ini menangani entri kosong dengan dua cara: semantik kosong ATAU prioritas_aturan. 
<br/> 
 
 3. Jika tidak ditemukan kecocokan persis DAN field `rule_priority` tidak ada, maka entri kosong di `fare_leg_rules.network_id`, `fare_leg_rules.from_area_id`, dan `fare_leg_rules.to_area_id` harus dicentang untuk memproses biaya perjalanan: 
 - Entri kosong di `fare_leg_rules.network_id` sesuai dengan semua jaringan yang ditentukan di [routes.txt](#routestxt) atau [jaringan.txt](#networkstxt) kecuali jaringan yang terdaftar di `fare_leg_rules.network_id` 
 
 - Entri kosong di `fare_leg_rules.from_area_id` sesuai dengan semua area yang ditentukan di `areas.area_id` kecuali yang terdaftar di `fare_leg_rules.from_area_id` 
 - Entri kosong di `fare_leg_rules.to_area_id` sesuai ke semua area yang ditentukan di `areas.area_id` kecuali area yang tercantum di `fare_leg_rules.to_area_id` 
<br/> 
 
 4. Jika kolom `rule_priority` ada, maka- Entri kosong di `fare_leg_rules.network_id` menunjukkan jaringan pada kaki tersebut tidak mempengaruhi pencocokan aturan ini. 
 - Entri kosong di `fare_leg_rules.from_area_id menunjukkan area departure kaki tidak mempengaruhi pencocokan aturan ini. 
 - Entri kosong di `fare_leg_rules.to_area_id menunjukkan area arrival pada leg tidak mempengaruhi pencocokan aturan ini. 
<br/> 
 
 5. Jika jalurnya tidak sesuai dengan salah satu aturan yang dijelaskan di atas, maka tarifnya tidak diketahui. 
 
<br/> 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `leg_group_id| tanda pengenal | Opsional | Mengidentifikasi sekelompok entri di [fare_leg_rules.txt](#fare_leg_rulestxt).<br><br> Digunakan untuk menjelaskan aturan transfer tarif antara `fare_transfer_rules.from_leg_group_id dan `fare_transfer_rules.to_leg_group_id.<br><br> Beberapa entri di [fare_leg_rules.txt](#fare_leg_rulestxt) mungkin termasuk dalam `fare_leg_rules.leg_group_id` yang sama.<br><br> Entri yang sama di [fare_leg_rules.txt](#fare_leg_rulestxt) (tidak termasuk `fare_leg_rules.leg_group_id`) tidak boleh tergabung dalam beberapa `fare_leg_rules.leg_group_id`.| 
 | `network_id` | ID asing yang mereferensikan `routes.network_id atau `networks.network_id`| Opsional | Mengidentifikasi jaringan rute yang menerapkan aturan tarif tarif.<br><br> Jika kolom `rule_priority` tidak ada DAN tidak ada nilai `fare_leg_rules.network_id` yang cocok dengan `network_id` yang sedang difilter, `fare_leg_rules.network_id` yang kosong akan dicocokkan secara default.<br><br> Entri kosong di `fare_leg_rules.network_id` sesuai dengan semua jaringan yang ditentukan di [routes.txt](#routestxt) atau [jaringan.txt](#networkstxt) tidak termasuk jaringan yang terdaftar di `fare_leg_rules.network_id`<br><br> Jika bidang `rule_priority` ada dalam file, `fare_leg_rules.network_id yang kosong menunjukkan bahwa jaringan rute pada bagian tersebut tidak memengaruhi pencocokan aturan ini. | 
 | `from_area_id| ID asing yang merujuk pada `areas.area_id| Opsional | Mengidentifikasi area departure .<br><br> Jika bidang `rule_priority` tidak ada DAN tidak ada nilai `fare_leg_rules.from_area_id` yang cocok dengan `area_id` yang difilter, `fare_leg_rules.from_area_id` yang kosong akan dicocokkan secara default.<br><br> Entri kosong di `fare_leg_rules.from_area_id` sesuai dengan semua area yang ditentukan di `areas.area_id` kecuali yang terdaftar di `fare_leg_rules.from_area_id`<br><br> Jika bidang `rule_priority` ada dalam file, `fare_leg_rules.from_area_id yang kosong menunjukkan bahwa area departure pada bagian tersebut tidak mempengaruhi pencocokan aturan ini. | 
 | `to_area_id| ID asing yang merujuk pada `areas.area_id| Opsional | Mengidentifikasi area arrival .<br><br> Jika bidang `rule_priority` tidak ada DAN tidak ada nilai `fare_leg_rules.to_area_id` yang cocok dengan `area_id` yang sedang difilter, `fare_leg_rules.to_area_id` yang kosong akan dicocokkan secara default.<br><br> Entri kosong di `fare_leg_rules.to_area_id` sesuai dengan semua area yang ditentukan di `areas.area_id` kecuali yang terdaftar di `fare_leg_rules.to_area_id`<br><br> Jika bidang `rule_priority` ada dalam file, `fare_leg_rules.to_area_id yang kosong menunjukkan bahwa area arrival pada bagian tersebut tidak mempengaruhi pencocokan aturan ini. | 
 | `from_timeframe_group_id` | Referensi ID asing `timeframes.timeframe_group_id` | Opsional | Menentukan kerangka waktu untuk peristiwa validasi tarif pada awal babak tarif.<br><br> “Waktu mulai” dari babak tarif adalah waktu di mana peristiwa tersebut dijadwalkan terjadi. Misalnya, waktu dapat berupa waktu departure bus yang dijadwalkan pada awal babak tarif saat penumpang naik dan memvalidasi tarifnya. Untuk semantik pencocokan aturan di bawah ini, waktu mulai dihitung dalam waktu lokal, sebagaimana ditentukan oleh [Semantik Waktu Lokal](#timeframe-local-time-semantics) dari [timeframe.txt](#timeframestxt). Perhentian atau stasiun acara departure bagian tarif harus digunakan untuk resolusi zona waktu, jika diperlukan.<br><br> Untuk aturan tarif yang menentukan `from_timeframe_group_id, aturan tersebut akan cocok dengan segmen tertentu jika t

di sini terdapat setidaknya satu catatan dalam [jangka waktu.txt](#timeframestxt) dengan semua kondisi berikut ini benar<br> - Nilai `timeframe_group_id sama dengan nilai `from_timeframe_group_id.<br> - Kumpulan hari yang diidentifikasi oleh `service_id catatan berisi “hari ini” dari waktu mulai bagian tarif.<br> - “Waktu hari” dari waktu mulai bagian tarif lebih besar atau sama dengan nilai `timeframes.start_time` pada catatan dan kurang dari nilai `timeframes.end_time`.<br><br> `fare_leg_rules.from_timeframe_group_id yang kosong menunjukkan bahwa waktu mulai babak tidak mempengaruhi pencocokan aturan ini. | 
 | `to_timeframe_group_id` | Referensi ID asing `timeframes.timeframe_group_id` | Opsional | Menentukan kerangka waktu untuk peristiwa validasi tarif di akhir babak tarif.<br><br> “Waktu berakhir” dari babak tarif adalah waktu di mana peristiwa tersebut dijadwalkan terjadi. Misalnya, waktu dapat berupa waktu arrival bus yang dijadwalkan pada akhir bagian tarif saat penumpang turun dan memvalidasi tarifnya. Untuk semantik pencocokan aturan di bawah ini, waktu berakhir dihitung dalam waktu lokal, sebagaimana ditentukan oleh [Semantik Waktu Lokal](#timeframe-local-time-semantics) dari [timeframes.txt](#timeframestxt). Perhentian atau stasiun arrival bagian tarif harus digunakan untuk resolusi zona waktu, jika diperlukan.<br><br> Untuk aturan tarif tarif yang menentukan `to_timeframe_group_id`, aturan tersebut akan cocok dengan segmen tertentu jika terdapat setidaknya satu catatan dalam [timeframes.txt](#timeframestxt) yang seluruh kondisi berikut ini benar<br> - Nilai `timeframe_group_id sama dengan nilai `to_timeframe_group_id.<br> - Kumpulan hari yang diidentifikasi oleh `service_id catatan berisi “hari ini” dari waktu berakhir bagian tarif.<br> - “Waktu hari” dari waktu akhir babak tarif lebih besar atau sama dengan nilai `timeframes.start_time` pada catatan dan kurang dari nilai `timeframes.end_time`.<br><br> `fare_leg_rules.to_timeframe_group_id yang kosong menunjukkan bahwa waktu berakhirnya leg tidak memengaruhi pencocokan aturan ini. | 
 | `fare_product_id| ID asing yang merujuk pada `fare_products.fare_product_id` | **Wajib** | Produk tarif yang diperlukan untuk melakukan perjalanan. | 
 | `prioritas_aturan` | Bilangan bulat non-negatif | Opsional | Mendefinisikan urutan prioritas aturan pencocokan yang diterapkan pada bagian kaki, sehingga aturan tertentu dapat didahulukan dibandingkan aturan lainnya. Jika beberapa entri di `fare_leg_rules.txt` cocok, aturan atau kumpulan aturan dengan nilai `rule_priority` tertinggi akan dipilih.<br><br> Nilai kosong untuk `rule_priority` dianggap nol. | 
 
### fare_transfer_rules.txt 
 
 File: **Opsional** 
 
 Kunci utama (`from_leg_group_id, to_leg_group_id, fare_product_id, transfer_count, duration_limit`) 
 
 Aturan tarif untuk transfers antar kaki perjalanan yang ditentukan dalam [`fare_leg_rules.txt`](#fare_leg_rulestxt). 
 
 Untuk memproses biaya perjalanan multi-kaki: 
 
 1. Kelompok tarif yang berlaku yang ditentukan dalam `fare_leg_rules.txt` harus ditentukan untuk semua bagian perjalanan individual berdasarkan perjalanan pengendara. 
 2. File [fare_transfer_rules.txt](#fare_transfer_rulestxt) harus disaring berdasarkan kolom yang menentukan karakteristik transfer, kolom ini adalah: 
 - `fare_transfer_rules.from_leg_group_id` 
 - `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 
 3. Jika transfer sama persis dengan catatan di [fare_transfer_rules.txt](#fare_transfer_rulestxt) berdasarkan karakteristik transfer, maka catatan tersebut harus diproses untuk menentukan biaya transfer. 
 4. Jika tidak ditemukan kecocokan persis, maka entri kosong di `from_leg_group_id atau di `to_leg_group_id harus dicentang untuk memproses biaya transfer: 
 - Entri kosong di `fare_transfer_rules.from_leg_group_id sesuai dengan semua grup leg yang ditentukan di bawah `fare_leg_rules.leg_group_id` tidak termasuk yang terdaftar di `fare_transfer_rules.from_leg_group_id` 
 - Entri kosong di `fare_transfer_rules.to_leg_group_id` sesuai dengan semua grup leg yang ditentukan di `fare_leg_rules.leg_group_id` tidak termasuk yang terdaftar di `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 5. Jika perpindahan tidak sesuai dengan salah satu aturan yang dijelaskan di atas, maka tidak ada pengaturan perpindahan dan kaki dianggap terpisah. 
 
<br/> 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `from_leg_group_id| Referensi ID asing `fare_leg_rules.leg_group_id` | Opsional | Mengidentifikasi sekelompok aturan tarif pra-transfer.<br><br> Jika tidak ada nilai `fare_transfer_rules.from_leg_group_id` yang cocok dengan `leg_group_id` yang difilter, `fare_transfer_rules.from_leg_group_id` yang kosong akan dicocokkan secara default.<br><br> Entri kosong di `fare_transfer_rules.from_leg_group_id` sesuai dengan semua grup leg yang ditentukan dalam `fare_leg_rules.leg_group_id` kecuali grup yang terdaftar di `fare_transfer_rules.from_leg_group_id`| 
 | `to_leg_group_id` | Referensi ID asing `fare_leg_rules.leg_group_id` | Opsional | Mengidentifikasi sekelompok aturan tarif pasca transfer.<br><br> Jika tidak ada nilai `fare_transfer_rules.to_leg_group_id` yang cocok dengan `leg_group_id` yang difilter, `fare_transfer_rules.to_leg_group_id` yang kosong akan dicocokkan secara default.<br><br> Entri kosong di `fare_transfer_rules.to_leg_group_id` sesuai dengan semua grup leg yang ditentukan dalam `fare_leg_rules.leg_group_id` kecuali yang terdaftar di `fare_transfer_rules.to_leg_group_id` | 
 | `transfer_count| Bilangan bulat bukan nol | **Dilarang Bersyarat** | Menentukan berapa banyak transfers berturut-turut yang dapat diterapkan aturan transfer.<br><br> Opsi yang valid adalah:<br> `-1` - Tanpa batas.<br> `1` atau lebih- Menentukan berapa banyak transfers yang dapat dilakukan oleh aturan transfer.<br><br> Jika sub-perjalanan cocok dengan beberapa catatan dengan `transfer_count yang berbeda, maka aturan dengan `transfer_count` minimum yang lebih besar atau sama dengan jumlah transfer sub-perjalanan saat ini yang akan dipilih.<br><br> Dilarang Bersyarat:<br> - **Dilarang** jika `fare_transfer_rules.from_leg_group_id` tidak sama dengan `fare_transfer_rules.to_leg_group_id`.<br> - **Wajib** jika `fare_transfer_rules.from_leg_group_id` sama dengan `fare_transfer_rules.to_leg_group_id`. | 
 | `duration_limit` | Bilangan bulat positif | Opsional | Menentukan batas durasi transfer.<br><br> Harus dinyatakan dalam kelipatan bilangan bulat detik.<br><br> Jika tidak ada batasan durasi, `fare_transfer_rules.duration_limit harus kosong. | 
 | `duration_limit_type| Jumlah | **Wajib Bersyarat** | Menentukan awal dan akhir relatif dari `fare_transfer_rules.duration_limit.<br><br> Opsi yang valid adalah:<br> `0` - Antara validasi tarif departure pada tahap saat ini dan validasi tarif arrival pada tahap berikutnya.<br> `1` - Antara validasi tarif departure pada tahap saat ini dan validasi tarif departure pada tahap berikutnya.<br> `2` - Antara validasi tarif arrival pada tahap saat ini dan validasi tarif departure pada tahap berikutnya.<br> `3` - Antara validasi tarif arrival pada tahap saat ini dan validasi tarif arrival pada tahap berikutnya.<br><br> Diperlukan Secara Bersyarat:<br> - **Wajib** jika `fare_transfer_rules.duration_limit` ditentukan.<br> - **Dilarang** jika `fare_transfer_rules.duration_limit kosong. | 
 | `fare_transfer_type` | Jumlah | **Wajib** | Menunjukkan metode pemrosesan biaya perpindahan antar kaki dalam sebuah perjalanan:<br> ![](../../assets/2-leg.svg)<br> Opsi yang valid adalah:<br> `0` - Dari kaki `fare_leg_rules.fare_product_id` ditambah `fare_transfer_rules.fare_product_id`; SEBUAH + AB.<br> `1` - Dari kaki `fare_leg_rules.fare_product_id` ditambah `fare_transfer_rules.fare_product_id` ditambah ke kaki `fare_leg_rules.fare_product_id`; A+AB+B.<br> `2` - `fare_transfer_rules.fare_product_id`; AB.<br><br> Interaksi pemrosesan biaya antara beberapa transfers dalam satu perjalanan:<br> ![](../../assets/3-leg.svg)<br><table><thead><tr><th> `fare_transfer_type</th><th> Memproses A > B</th><th> Memproses B > C</th></tr></thead><tbody><tr><td> `0`</td><td> SEBUAH + AB</td><td> S + SM</td></tr><tr><td> `1`</td><td> A+AB+B</td><td> S+BC+C</td></tr><tr><td> `2`</td><td> AB</td><td> S + SM</td></tr></tbody></table> Dimana S menunjukkan total biaya proses dari bagian dan transfer sebelumnya. | 
 | `fare_product_id| ID asing yang merujuk pada `fare_products.fare_product_id` | Opsional | Produk tarif diperlukan untuk ditransfer antara dua kaki tarif. Jika kosong, biaya aturan transfer adalah 0.| 
 
 
### areas.txt 
 
 File: **Opsional** 
 
 Kunci utama (`area_id`) 
 
 Mendefinisikan pengidentifikasi area. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `area_id| ID Unik | **Wajib** | Mengidentifikasi suatu area. Harus unik di [areas.txt](#areastxt). | 
 | `area_name| Text | **Opsional** | Nama area seperti yang ditampilkan kepada pengendara. | 
 
### stop_areas.txt 
 
 File: **Opsional** 
 
 Kunci utama (`*`) 
 
 Menetapkan stops dari [stops.txt](#stopstxt) ke area. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `area_id| ID asing yang merujuk pada `areas.area_id| **Wajib** | Mengidentifikasi area yang memiliki satu atau beberapa `stop_id`. `stop_id` yang sama dapat ditentukan di banyak `area_id. | 
 | `stop_id` | Referensi ID asing `stops.stop_id| **Wajib** | Mengidentifikasi perhentian. Jika sebuah stasiun (yaitu perhentian dengan `stops.location_type=1`) didefinisikan dalam kolom ini, diasumsikan bahwa semua platformnya (yaitu semua stops dengan `stops.location_type=0` yang stasiunnya didefinisikan sebagai `stops.parent_station`) adalah bagian dari area yang sama. Perilaku ini dapat diatasi dengan menugaskan platform ke area lain. | 
 
### jaringan.txt 
 
 File: **Dilarang Bersyarat** 
 
 Kunci utama (`network_id`) 
 
 Mendefinisikan pengidentifikasi jaringan yang berlaku untuk aturan tarif tarif. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `network_id| ID Unik | **Wajib** | Mengidentifikasi jaringan. Harus unik di [networks.txt](#networkstxt). | 
 | `network_name| Text | **Opsional** | Nama jaringan yang menerapkan aturan tarif, seperti yang digunakan oleh agency lokal dan penumpangnya. 
 
### rute_networks.txt 
 
 File: **Dilarang Bersyarat** 
 
 Kunci utama (`route_id`) 
 
 Menetapkan routes dari [routes.txt](#routestxt) ke jaringan. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `network_id| Referensi ID asing `networks.network_id| **Wajib** | Mengidentifikasi jaringan yang memiliki satu atau beberapa `route_id`. `route_id` hanya dapat ditentukan dalam satu `network_id. | 
 | `route_id` | ID asing yang merujuk pada `routes.route_id| **Wajib** | Mengidentifikasi rute. | 
 
### shapes.txt 
 
 File: **Opsional** 
 
 Kunci utama (`shape_id`, `shape_pt_sequence`) 
 
 Bentuk mendeskripsikan jalur yang dilalui vehicle di sepanjang penyelarasan rute, dan ditentukan dalam file shapes.txt. Bentuk diasosiasikan dengan Perjalanan, dan terdiri dari rangkaian titik yang dilalui vehicle secara berurutan. Bentuk tidak perlu memotong lokasi Perhentian secara tepat, namun semua Perhentian pada suatu perjalanan harus terletak dalam jarak kecil dari shape perjalanan tersebut, yaitu dekat dengan segmen garis lurus yang menghubungkan titik-titik shape tersebut. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `shape_id` | tanda pengenal | **Wajib** | Mengidentifikasi suatu shape. | 
 | `shape_pt_lat| Lintang | **Wajib** | Garis lintang suatu titik shape. Setiap rekaman di [shapes.txt](#bentuktxt) mewakili titik shape yang digunakan untuk menentukan shape. | 
 | `shape_pt_lon| Bujur | **Wajib** | Bujur suatu titik shape. | 
 | `shape_pt_sequence| Bilangan bulat non-negatif | **Wajib** | Urutan titik-titik shape yang terhubung membentuk shape. Nilai harus meningkat sepanjang perjalanan tetapi tidak perlu berturut-turut.<hr> *Contoh: Jika shape "A_shp" memiliki tiga titik dalam definisinya, file [shapes.txt](#shapestxt) mungkin berisi catatan berikut untuk menentukan shape:*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence<br> `A_shp,37.61956,-122.48161,0<br> `A_shp,37.64430,-122.41070,6<br> `A_shp,37.65863,-122.30839,11| 
 | `shape_dist_traveled| float non-negatif | Opsional | Jarak sebenarnya yang ditempuh sepanjang shape dari titik shape pertama ke titik yang ditentukan dalam rekaman ini. Digunakan oleh perencana perjalanan untuk menunjukkan bagian shape yang benar pada peta. Nilai harus bertambah seiring dengan `shape_pt_sequence`; mereka tidak boleh digunakan untuk menunjukkan perjalanan mundur sepanjang suatu rute. Satuan jarak harus konsisten dengan yang digunakan di [stop_times.txt](#stop_timestxt).<br><br> Direkomendasikan untuk routes yang memiliki looping atau inlining ( vehicle melintasi atau melewati bagian alinyemen yang sama dalam satu perjalanan). <br><img src="../../../assets/inlining.svg" width=200px style="display: block; margin-left: auto; margin-right: auto;"><br> Jika vehicle menelusuri kembali atau melintasi penyelarasan rute pada titik-titik selama perjalanan, `shape_dist_traveled` penting untuk memperjelas bagaimana bagian-bagian titik dalam garis [shapes.txt](#bentuktxt) sesuai dengan catatan di [stop_times.txt](#stop_timestxt).<hr> *Contoh: Jika sebuah bus berjalan di sepanjang tiga titik yang ditentukan di atas untuk A_shp, nilai tambahan `shape_dist_traveled` (ditampilkan di sini dalam kilometer) akan terlihat seperti ini:*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shape_dist_traveled`<br> `A_shp,37.61956,-122.48161,0,0`<br> `A_shp,37.64430,-122.41070,6,6.8310`<br> `A_shp,37.65863,-122.30839,11,15.8765` | 
 
### frequencies.txt 
 
 File: **Opsional** 
 
 Kunci utama (`trip_id`, `start_time`) 
 
 [Frequencies.txt](#frequenciestxt) mewakili perjalanan yang beroperasi pada headways reguler (waktu antar perjalanan). File ini dapat digunakan untuk mewakili dua jenis layanan yang berbeda. 
 
 * Layanan berbasis frekuensi (`exact_times`=`0`) yang layanannya tidak mengikuti jadwal tetap sepanjang hari. Sebaliknya, operator berusaha untuk secara ketat mempertahankan kecepatan perjalanan yang telah ditentukan sebelumnya. 
 * Representasi terkompresi dari layanan berbasis jadwal (`exact_times`= `1`) yang memiliki headway yang sama persis untuk perjalanan selama periode waktu tertentu. Dalam layanan berbasis jadwal, operator berusaha untuk secara ketat mematuhi jadwal. 
 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `trip_id` | ID asing yang merujuk pada `trips.trip_id` | **Wajib** | Mengidentifikasi perjalanan yang menerapkan kemajuan layanan tertentu. | 
 | `start_time` | Waktu | **Wajib** | Waktu keberangkatan vehicle pertama dari perhentian pertama perjalanan dengan headway yang ditentukan. | 
 | `end_time| Waktu | **Wajib** | Waktu di mana layanan berubah ke headway yang berbeda (atau berhenti) pada perhentian pertama perjalanan. | 
 | `headway_secs` | Bilangan bulat positif | **Wajib** | Waktu, dalam detik, antara keberangkatan dari pemberhentian yang sama (headway) untuk perjalanan tersebut, selama interval waktu yang ditentukan oleh `start_time` dan `end_time. Beberapa headway dapat ditentukan untuk perjalanan yang sama, namun tidak boleh tumpang tindih. Kemajuan baru dapat dimulai tepat pada saat kemajuan sebelumnya berakhir. | 
 | `exact_times` | Jumlah | Opsional | Menunjukkan jenis layanan untuk perjalanan. Lihat deskripsi file untuk informasi lebih lanjut. Opsi yang valid adalah:<br><br> `0` atau kosong- Perjalanan berbasis frekuensi.<br> `1` - Perjalanan berbasis jadwal dengan waktu tempuh yang sama persis sepanjang hari. Dalam hal ini, nilai `end_time harus lebih besar dari `start_time` perjalanan terakhir yang diinginkan, namun lebih kecil dari start_time perjalanan + `headway_secs` yang terakhir diinginkan. | 
 
### transfers.txt 
 
 File: **Opsional** 
 
 Kunci utama (`from_stop_id`, `to_stop_id`, `from_trip_id`, `to_trip_id`, `from_route_id`, `to_route_id`) 
 
 Saat menghitung rencana perjalanan, aplikasi yang menggunakan GTFS menginterpolasi transfers berdasarkan waktu yang diperbolehkan dan jarak perhentian. [Transfers.txt](#transferstxt) menetapkan aturan tambahan dan penggantian untuk transfers yang dipilih. 
 
 Bidang `from_trip_id`, `to_trip_id`, `from_route_id` dan `to_route_id` memungkinkan tingkat kekhususan yang lebih tinggi untuk aturan transfer. Bersama dengan `from_stop_id dan `to_stop_id, peringkat kekhususannya adalah sebagai berikut: 
 
 1. Kedua `trip_id` didefinisikan: `from_trip_id dan `to_trip_id. 
 2. Satu set `trip_id` dan `route_id` ditentukan: (`from_trip_id` dan `to_route_id`) atau (`from_route_id` dan `to_trip_id`). 
 3. Satu `trip_id` ditentukan: `from_trip_id` atau `to_trip_id. 
 4. Kedua `route_id` ditentukan: `from_route_id` dan `to_route_id`. 
 5. Satu `route_id` ditentukan: `from_route_id` atau `to_route_id`. 
 6. Hanya `from_stop_id` dan `to_stop_id` yang ditentukan: tidak ada kolom terkait rute atau perjalanan yang disetel. 
 
 Untuk pasangan perjalanan tiba dan perjalanan berangkat tertentu, perpindahan dengan kekhususan terbesar yang berlaku di antara kedua perjalanan ini dipilih. Untuk setiap pasangan perjalanan, tidak boleh ada dua transfers dengan kekhususan maksimal yang sama yang dapat diterapkan. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `from_stop_id| Referensi ID asing `stops.stop_id| **Wajib Bersyarat** | Mengidentifikasi perhentian atau stasiun tempat koneksi antar routes dimulai. Jika bidang ini mengacu pada sebuah stasiun, aturan transfer berlaku untuk semua stops turunannya. Merujuk ke suatu stasiun dilarang untuk `transfer_types 4 dan 5. | 
 | `to_stop_id| Referensi ID asing `stops.stop_id| **Wajib Bersyarat** | Mengidentifikasi perhentian atau stasiun di mana koneksi antar routes berakhir. Jika bidang ini mengacu pada stasiun, aturan transfer berlaku untuk semua stops turunan. Merujuk ke stasiun dilarang untuk `transfer_types 4 dan 5. | 
 | `from_route_id| ID asing yang merujuk pada `routes.route_id| Opsional | Mengidentifikasi rute di mana koneksi dimulai.<br><br> Jika `from_route_id ditentukan, transfer akan berlaku untuk perjalanan tiba pada rute untuk `from_stop_id yang ditentukan.<br><br> Jika `from_trip_id` dan `from_route_id` keduanya ditentukan, `trip_id` harus termasuk dalam `route_id`, dan `from_trip_id` akan diutamakan. | 
 | `to_route_id| ID asing yang merujuk pada `routes.route_id| Opsional | Mengidentifikasi rute di mana koneksi berakhir.<br><br> Jika `to_route_id` ditentukan, transfer akan berlaku untuk perjalanan keberangkatan pada rute untuk `to_stop_id` yang ditentukan.<br><br> Jika `to_trip_id` dan `to_route_id` keduanya ditentukan, `trip_id` harus termasuk dalam `route_id`, dan `to_trip_id` akan diutamakan. | 
 | `from_trip_id| ID asing yang merujuk pada `trips.trip_id` | **Wajib Bersyarat** | Mengidentifikasi perjalanan di mana koneksi antar routes dimulai.<br><br> Jika `from_trip_id ditentukan, transfer akan berlaku untuk perjalanan kedatangan untuk `from_stop_id yang ditentukan.<br><br> Jika `from_trip_id` dan `from_route_id` keduanya ditentukan, `trip_id` harus termasuk dalam `route_id`, dan `from_trip_id` akan diutamakan. DIPERLUKAN jika `transfer_type adalah `4` atau `5`. | 
 | `to_trip_id| ID asing yang merujuk pada `trips.trip_id` | **Wajib Bersyarat** | Mengidentifikasi perjalanan di mana koneksi antar routes berakhir.<br><br> Jika `to_trip_id` ditentukan, transfer akan berlaku untuk perjalanan keberangkatan untuk `to_stop_id` yang ditentukan.<br><br> Jika `to_trip_id` dan `to_route_id` keduanya ditentukan, `trip_id` harus termasuk dalam `route_id`, dan `to_trip_id` akan diutamakan. DIPERLUKAN jika `transfer_type adalah `4` atau `5`. | 
 | `transfer_type| Jumlah | **Wajib** | Menunjukkan jenis koneksi untuk pasangan (`from_stop_id`, `to_stop_id`) yang ditentukan. Opsi yang valid adalah:<br><br> `0` atau kosong- Rekomendasi titik transfer antar routes.<br> `1` - Titik transfer berjangka waktu antara dua routes.vehicle yang berangkat diharapkan menunggu kedatangannya dan memberikan waktu yang cukup bagi pengendara untuk berpindah antar routes.<br> `2` - Transfer memerlukan amount waktu minimum antara arrival dan departure untuk memastikan koneksi. Waktu yang diperlukan untuk transfer ditentukan oleh `min_transfer_time.<br> `3` - Transfer antar routes di lokasi tidak dapat dilakukan.<br> `4` - Penumpang dapat berpindah dari satu perjalanan ke perjalanan lainnya dengan tetap berada di dalam vehicle yang sama ("transfer di kursi"). Detail selengkapnya tentang jenis transportasi ini [di bawah](#linked-trips).<br> `5` - transfers di kursi tidak diperbolehkan antar perjalanan berurutan. Penumpang harus turun dari vehicle dan naik kembali. Detail selengkapnya tentang jenis transportasi ini [di bawah](#linked-trips). | 
 | `min_transfer_time` | Bilangan bulat non-negatif | Opsional | Jumlah waktu, dalam detik, yang harus tersedia untuk memungkinkan perpindahan antar routes pada stops yang ditentukan. `min_transfer_time harus cukup untuk memungkinkan pengendara biasa berpindah di antara dua stops, termasuk waktu buffer untuk memungkinkan perbedaan jadwal pada setiap rute. | 
 
#### Perjalanan tertaut 
 
 Hal berikut ini berlaku untuk `transfer_type=4` dan `=5`, yang digunakan untuk menghubungkan perjalanan bersama-sama, dengan atau tanpa transfers di kursi. 
 
 Perjalanan yang dihubungkan bersama HARUS dioperasikan oleh vehicle yang sama.vehicle DAPAT digabungkan dengan, atau dipisahkan dari, kendaraan lain. 
 
 Jika transfer perjalanan tertaut dan block_id disediakan dan menghasilkan hasil yang bertentangan, maka transfer perjalanan tertaut harus digunakan. 
 
 Pemberhentian terakhir `from_trip_id` HARUS secara geografis dekat dengan pemberhentian pertama `to_trip_id`, dan waktu arrival terakhir `from_trip_id` HARUS lebih awal tetapi mendekati waktu departure pertama `to_trip_id. Waktu arrival terakhir `from_trip_id` MUNGKIN lebih lambat dari waktu departure pertama `to_trip_id` jika perjalanan `to_trip_id` terjadi pada hari layanan berikutnya. 
 
 Perjalanan MUNGKIN dihubungkan 1-ke-1 dalam kasus biasa, namun MUNGKIN juga dihubungkan 1-ke-n, n-ke-1, atau n-ke-n untuk mewakili kelanjutan perjalanan yang lebih kompleks. Misalnya, dua perjalanan kereta api (perjalanan A dan perjalanan B pada diagram di bawah) dapat digabungkan menjadi satu perjalanan kereta api (perjalanan C) setelah operasi penggandengan vehicle di stasiun yang sama: 
 
 - Dalam perjalanan 1-ke-n lanjutannya, `trips.service_id untuk setiap `to_trip_id HARUS sama. 
 - Dalam kelanjutan n-ke-1, `trips.service_id untuk setiap `from_trip_id HARUS identik. 
 - kelanjutan n-ke-n harus memenuhi kedua batasan. 
 - Perjalanan dapat dihubungkan bersama sebagai bagian dari beberapa kelanjutan yang berbeda, dengan ketentuan bahwa `trip.service_id` TIDAK BOLEH tumpang tindih pada hari layanan mana pun. 
 
<pre> 
 Perjalanan A 
 ────────────────────\ 
 \ Perjalanan C 
 ────────────── 
 Perjalanan B/
 ────────────────────/
</pre> 
 
### pathways.txt 
 
 File: **Opsional** 
 
 Kunci utama (`pathway_id`) 
 
 File [pathways.txt](#pathwaystxt) dan [levels.txt](#levelstxt) menggunakan representasi grafik untuk menggambarkan stasiun kereta bawah tanah atau kereta api, dengan node mewakili lokasi dan tepi mewakili pathways. 
 
 Untuk melakukan navigasi dari pintu masuk/keluar stasiun (node ​​yang direpresentasikan sebagai lokasi dengan `location_type=2) ke platform (node ​​yang direpresentasikan sebagai lokasi dengan `location_type=0 atau kosong), pengendara akan berpindah melalui jalan setapak, gerbang tarif, tangga, dan tepi lainnya yang direpresentasikan sebagai pathways. Node generik (node ​​yang diwakili dengan `location_type=3`) dapat digunakan untuk menghubungkan pathways di seluruh stasiun. 
 
 Jalur harus didefinisikan secara mendalam di sebuah stasiun. Jika ada pathways yang ditentukan, diasumsikan bahwa semua pathways di seluruh stasiun terwakili. Oleh karena itu, pedoman berikut ini berlaku: 
 
 - Tidak boleh ada lokasi yang menjuntai: Jika ada lokasi di dalam stasiun yang memiliki jalur, maka semua lokasi di dalam stasiun tersebut harus memiliki pathways, kecuali peron yang memiliki area keberangkatan (`location_type=4, lihat pedoman di bawah). 
 - Tidak ada pathways untuk platform dengan area boarding: Platform (`location_type=0` atau kosong) yang memiliki area boarding (`location_type=4`) diperlakukan sebagai objek induk, bukan titik. Dalam kasus seperti ini, platform tidak boleh memiliki pathways yang ditetapkan. Semua pathways harus ditetapkan untuk masing-masing area keberangkatan peron. 
 - Tidak ada platform yang terkunci: Setiap platform (`location_type=0` atau kosong) atau area boarding (`location_type=4`) harus terhubung ke setidaknya satu pintu masuk/keluar (`location_type=2`) melalui beberapa pathways. Jarang ada stasiun yang tidak mengizinkan jalur ke luar stasiun dari peron tertentu. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `pathway_id| ID Unik | **Wajib** | Mengidentifikasi jalur. Digunakan oleh sistem sebagai pengidentifikasi internal untuk catatan. Harus unik dalam kumpulan data.<br><br> pathways yang berbeda mungkin memiliki nilai yang sama untuk `from_stop_id dan `to_stop_id.<hr> _Contoh: Ketika dua eskalator berdampingan dalam arah yang berlawanan, atau ketika tangga dan elevator bergerak dari tempat yang sama ke tempat yang sama, `pathway_id yang berbeda mungkin memiliki nilai `from_stop_id dan `to_stop_id yang sama._ | 
 | `from_stop_id| Referensi ID asing `stops.stop_id| **Wajib** | Lokasi di mana jalur dimulai.<br><br> Harus berisi `stop_id` yang mengidentifikasi platform (`lo

cation_type=0` atau kosong), pintu masuk/keluar (`location_type=2`), node generik (`location_type=3`) atau area boarding (`location_type=4`).<br><br> Nilai untuk `stop_id` yang mengidentifikasi stasiun (`location_type=1`) dilarang.| 
 | `to_stop_id| Referensi ID asing `stops.stop_id| **Wajib** | Lokasi di mana jalur berakhir.<br><br> Harus berisi `stop_id` yang mengidentifikasi platform (`location_type=0` atau kosong), pintu masuk/keluar (`location_type=2`), simpul umum (`location_type=3`) atau area keberangkatan (`location_type=4`) .<br><br> Nilai untuk `stop_id` yang mengidentifikasi stasiun (`location_type=1`) dilarang.| 
 | `pathway_mode| Jumlah | **Wajib** | Jenis jalur antara pasangan (`from_stop_id`, `to_stop_id`) yang ditentukan. Opsi yang valid adalah:<br><br> `1` - Jalan setapak.<br> `2` - Tangga.<br> `3` - Memindahkan trotoar/wisatawan.<br> `4` - Eskalator.<br> `5` - Lift.<br> `6` - Gerbang tarif (atau gerbang pembayaran): Jalur yang melintasi area stasiun yang memerlukan bukti pembayaran untuk menyeberang. Gerbang tarif dapat memisahkan area stasiun berbayar dari area tidak berbayar, atau memisahkan area pembayaran berbeda dalam stasiun yang sama satu sama lain. Informasi ini dapat digunakan untuk menghindari mengarahkan penumpang melewati stasiun dengan menggunakan jalan pintas yang require penumpang melakukan pembayaran yang tidak perlu, seperti mengarahkan penumpang untuk berjalan melalui peron kereta bawah tanah untuk mencapai busway.<br> `7`- Gerbang keluar: Jalur keluar dari area berbayar ke area tidak berbayar yang tidak memerlukan bukti pembayaran untuk melintasinya.| 
 | `is_bidirectional| Jumlah | **Wajib** | Menunjukkan arah jalur yang dapat diambil:<br><br> `0` - Jalur searah yang hanya dapat digunakan dari `from_stop_id ke `to_stop_id.<br> `1` - Jalur dua arah yang dapat digunakan di kedua arah.<br><br> Gerbang keluar (`pathway_mode=7`) tidak boleh dua arah.| 
 | `panjang` | float non-negatif | Opsional | Panjang horizontal jalur dalam meter dari lokasi asal (didefinisikan dalam `from_stop_id) ke lokasi tujuan (didefinisikan dalam `to_stop_id).<br><br> Kolom ini disarankan untuk jalur pejalan kaki (`pathway_mode=1), gerbang tarif (`pathway_mode=6) dan gerbang keluar (`pathway_mode=7).| 
 | `traversal_time| Bilangan bulat positif | Opsional | Waktu rata-rata dalam hitungan detik yang diperlukan untuk berjalan melalui jalur dari lokasi asal (didefinisikan dalam `from_stop_id) ke lokasi tujuan (didefinisikan dalam `to_stop_id).<br><br> Bidang ini direkomendasikan untuk trotoar bergerak (`pathway_mode=3), eskalator (`pathway_mode=4) dan elevator (`pathway_mode=5).| 
 | `stair_count` | Bilangan bulat bukan nol | Opsional | Jumlah tangga jalur.<br><br> `stair_count` yang positif menyiratkan bahwa pengendara berjalan dari `from_stop_id` ke `to_stop_id`. Dan `stair_count yang negatif menyiratkan bahwa pengendara berjalan turun dari `from_stop_id ke `to_stop_id.<br><br> Bidang ini direkomendasikan untuk tangga (`pathway_mode=2).<br><br> Jika hanya perkiraan jumlah tangga yang dapat diberikan, disarankan untuk memperkirakan 15 anak tangga untuk 1 lantai.| 
 | `max_slope| Float | Opsional | Rasio kemiringan maksimum jalur. Opsi yang valid adalah:<br><br> `0` atau kosong- Tidak ada kemiringan.<br> `Float` - Rasio kemiringan jalur, positif untuk ke atas, negatif untuk ke bawah.<br><br> Bidang ini hanya boleh digunakan dengan jalur pejalan kaki (`pathway_mode=1) dan trotoar bergerak (`pathway_mode=3).<hr> _Contoh: Di AS, 0,083 (juga ditulis 8,3%) adalah rasio kemiringan maksimum untuk kursi roda yang digerakkan dengan tangan, yang berarti peningkatan sebesar 0,083m (jadi 8,3cm) untuk setiap 1m._| 
 | `min_width` | float positif | Opsional | Lebar minimum jalur dalam meter.<br><br> Bidang ini direkomendasikan jika lebar minimum kurang dari 1 meter.| 
 | `signposted_as` | Text | Opsional | Teks yang menghadap publik dari papan tanda fisik yang dapat dilihat oleh pengendara.<br><br> Dapat digunakan untuk memberikan petunjuk arah teks kepada pengendara, seperti ’ikuti rambu ke’. Teks di `singposted_as akan tampak persis seperti yang dicetak pada tanda.<br><br> Jika signage fisik bersifat multibahasa, kolom ini dapat diisi dan diterjemahkan mengikuti contoh `stops.stop_name dalam definisi kolom `feed_info.feed_lang.| 
 | `reversed_signposted_as| Text | Opsional | Sama seperti `signposted_as, namun bila digunakan jalur dari `to_stop_id ke `from_stop_id.| 
 
### levels.txt 
 
 File: **Diperlukan Secara Bersyarat** 
 
 Kunci utama (`level_id`) 
 
 Menjelaskan level dalam sebuah stasiun. Berguna jika digabungkan dengan [pathways.txt](#pathwaystxt). 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `level_id| ID Unik | **Wajib** | Mengidentifikasi level di stasiun.| 
 | `level_index` | Float | **Wajib** | Indeks numerik tingkat yang menunjukkan position relatifnya.<br><br> Permukaan tanah harus memiliki indeks `0`, dengan permukaan tanah di atasnya ditandai dengan indeks positif dan permukaan tanah di bawah tanah dengan indeks negatif.| 
 | `level_name| Text | Opsional | Nama level yang dilihat oleh pengendara di dalam gedung atau stasiun.<hr> _Contoh: Naik lift ke "Mezzanine" atau "Platform" atau "-1"._| 
 
### location_groups.txt 
 
 File: **Opsional** 
 
 Kunci utama (`location_group_id`) 
 
 Mendefinisikan grup lokasi, yaitu grup stops yang dapat diminta oleh pengendara penjemputan atau pengantaran. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |----------|----|------------|-----------| 
 | `lokasi_grup_id` | ID Unik | **Wajib** | Mengidentifikasi grup lokasi. ID harus unik di semua nilai `stops.stop_id, locations.geojson `id`, dan `location_groups.location_group_id`.<br><br> Grup lokasi adalah sekelompok stops yang bersama-sama menunjukkan lokasi di mana pengendara dapat meminta penjemputan atau pengantaran. | 
 | `nama_grup_lokasi` | Text | Opsional | Nama grup lokasi seperti yang ditampilkan kepada pengendara. | 
 
### location_group_stops.txt 
 
 File: **Opsional** 
 
 Kunci utama (`*`) 
 
 Menetapkan stops dari stops.txt ke grup lokasi. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |----------|----|------------|-----------| 
 | `lokasi_grup_id` | ID asing yang merujuk pada `location_groups.location_group_id` | **Wajib** | Mengidentifikasi grup lokasi yang memiliki satu atau beberapa `stop_id`. `stop_id` yang sama dapat ditentukan di banyak `location_group_id`s. | 
 | `stop_id` | Referensi ID asing `stops.stop_id| **Wajib** | Mengidentifikasi perhentian milik grup lokasi. | 
 
 
### locations.geojson 
 
 File: **Opsional** 
 
 Mendefinisikan zona di mana pengendara dapat meminta penjemputan atau pengantaran melalui layanan sesuai permintaan. Zona ini direpresentasikan sebagai poligon GeoJSON. 
 
 - File ini menggunakan subset format GeoJSON, yang dijelaskan dalam [RFC 7946](https://tools.ietf.org/html/rfc7946). 
 - File `locations.geojson` harus berisi `FeatureCollection`. 
 - `FeatureCollection` menentukan berbagai lokasi perhentian di mana pengendara dapat meminta penjemputan atau pengantaran. 
 - Setiap `Fitur` GeoJSON harus memiliki `id`. `id` harus unik di semua nilai `stops.stop_id, locations.geojson `id`, dan `location_group_id`. 
 - Setiap `Fitur` GeoJSON harus memiliki objek dan kunci terkait sesuai tabel di bawah: 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 |- `ketik` | Tali | **Wajib** | `"FeatureCollection"` lokasi. | 
 |- `fitur` | Himpunan | **Wajib** | Kumpulan objek `"Fitur"` yang menjelaskan lokasi. | 
 |     \- `ketik` | Tali | **Wajib** | `"Fitur"` | 
 |     \- `id` | Tali | **Wajib** | Mengidentifikasi lokasi. ID harus unik di semua nilai `stops.stop_id, locations.geojson `id`, dan `location_groups.location_group_id`. | 
 |     \- `properti` | Objek | **Wajib** | Kunci properti lokasi. | 
 |         \- `stop_name| Tali | Opsional | Menunjukkan nama lokasi seperti yang ditampilkan kepada pengendara. | 
 |         \- `stop_desc| Tali | Opsional | Deskripsi lokasi yang bermakna untuk membantu mengarahkan pengendara. | 
 |     \- `geometri` | Objek | **Wajib** | Geometri lokasi. | 
 |         \- `ketik` | Tali | **Wajib** | Harus bertipe:<br> - `"Polygon"`<br> - `"MultiPoligon"` | 
 |         \- `koordinat` | Himpunan | **Wajib** | Koordinat geografis (latitude dan longitude) menentukan geometri lokasi. | 
 
### booking_rules.txt 
 
 File: **Opsional** 
 
 Kunci utama (`booking_rule_id`) 
 
 Mendefinisikan aturan pemesanan untuk layanan yang diminta pengendara 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `id_aturan_pemesanan` | ID Unik | **Wajib** | Mengidentifikasi suatu aturan. | 
 | `tipe_pemesanan` | Jumlah | **Wajib** | Menunjukkan seberapa jauh sebelumnya pemesanan dapat dilakukan. Opsi yang valid adalah:<br><br> `0` - Pemesanan waktu nyata.<br> `1` - Pemesanan hingga hari yang sama dengan pemberitahuan terlebih dahulu.<br> `2` - Pemesanan hingga hari sebelumnya. | 
 | `pemberitahuan_sebelumnya_durasi_menit` | bilangan bulat | **Wajib Bersyarat** | Jumlah minimum menit sebelum perjalanan untuk membuat permintaan.<br><br> **Diwajibkan Secara Bersyarat**:<br> - **Wajib** untuk `booking_type=1`.<br> - **Dilarang** sebaliknya. | 
 | `pemberitahuan_sebelumnya_durasi_maks` | bilangan bulat | **Dilarang Bersyarat** | Jumlah menit maksimum sebelum perjalanan untuk membuat permintaan pemesanan.<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** untuk `booking_type=0` dan `booking_type=2`.<br> - Opsional untuk `booking_type=1`.| 
 | `pemberitahuan_sebelumnya_hari_terakhir` | bilangan bulat | **Wajib Bersyarat** | Hari terakhir sebelum perjalanan untuk membuat permintaan pemesanan.<br><br> Contoh: “Perjalanan harus dipesan 1 hari sebelumnya sebelum jam 17.00” akan dikodekan sebagai `prior_notice_last_day=1`.<br><br> **Diwajibkan Secara Bersyarat**:<br> - **Wajib** untuk `booking_type=2`.<br> - **Dilarang** sebaliknya. | 
 | `pemberitahuan_sebelumnya_waktu_terakhir` | Waktu | **Wajib Bersyarat** | Terakhir kali pada hari terakhir sebelum perjalanan untuk membuat permintaan pemesanan.<br><br> Contoh: “Perjalanan harus dipesan 1 hari sebelumnya sebelum jam 17.00” akan dikodekan sebagai `prior_notice_last_time=17:00:00`.<br><br> **Diwajibkan Secara Bersyarat**:<br> - **Wajib** jika `prior_notice_last_day` ditentukan.<br> - **Dilarang** sebaliknya. | 
 | `pemberitahuan_sebelumnya_hari_mulai` | bilangan bulat | **Dilarang Bersyarat** | Sehari paling awal sebelum perjalanan untuk membuat permintaan pemesanan.<br><br> Contoh: “Perjalanan dapat dipesan paling cepat satu minggu sebelumnya pada tengah malam” akan dikodekan sebagai `prior_notice_start_day=7`.<br><br> **Dilarang Bersyarat**:<br> - **Dilarang** untuk `booking_type=0`.<br> - **Dilarang** untuk `booking_type=1` jika `prior_notice_duration_max` ditentukan.<br> - Opsional sebaliknya. | 
 | `sebelum_pemberitahuan_waktu_mulai` | Waktu | **Wajib Bersyarat** | Waktu paling awal pada hari paling awal sebelum perjalanan untuk membuat permintaan pemesanan.<br><br> Contoh: “Perjalanan dapat dipesan paling cepat satu minggu sebelumnya pada tengah malam” akan dikodekan sebagai `prior_notice_start_time=00:00:00`.<br><br> **Diwajibkan Secara Bersyarat**:<br> - **Wajib** jika `prior_notice_start_day` ditentukan.<br> - **Dilarang** sebaliknya. | 
 | `pemberitahuan_sebelumnya_layanan_id` | ID mereferensikan `calendar.service_id| **Dilarang Bersyarat** | Menunjukkan hari layanan di mana `prior_notice_last_day` atau `prior_notice_start_day` dihitung.<br><br> Contoh: Jika kosong, `prior_notice_start_day=2` akan menjadi dua hari kalender sebelumnya. Jika didefinisikan sebagai `service_id yang hanya berisi hari kerja (hari kerja tanpa hari libur), `prior_notice_start_day=2` akan menjadi dua hari kerja sebelumnya.<br><br> **Dilarang Bersyarat**:<br> - Opsional jika `booking_type=2`.<br> - **Dilarang** sebaliknya. | 
 | `message| Text | Opsional | Pesan kepada pengendara yang menggunakan layanan pada `stop_time saat memesan penjemputan dan pengantaran sesuai permintaan. Dimaksudkan untuk memberikan informasi minimal untuk dikirimkan dalam antarmuka pengguna tentang tindakan yang harus diambil pengendara untuk memanfaatkan layanan. | 
 | `pesan_penjemputan` | Text | Opsional | Berfungsi dengan cara yang sama seperti `message tetapi digunakan ketika pengendara hanya memiliki penjemputan berdasarkan permintaan. | 
 | `pesan_drop_off` | Text | Opsional | Berfungsi dengan cara yang sama seperti `message tetapi digunakan ketika pengendara hanya melakukan pengantaran sesuai permintaan. | 
 | `nomor_telepon` | Phone number | Opsional | Phone number yang dapat dihubungi untuk membuat permintaan pemesanan. | 
 | `info_url` | URL | Opsional | URL yang memberikan informasi tentang aturan pemesanan. | 
 | `url_pemesanan` | URL | Opsional | URL ke antarmuka online atau aplikasi tempat permintaan pemesanan dapat dibuat. | translations.txt​​​​​`) 
 
 Di wilayah yang memiliki beberapa bahasa resmi, agen/operator angkutan umum biasanya memiliki nama dan halaman web dengan bahasa tertentu. Untuk memberikan pelayanan terbaik kepada penumpang di wilayah tersebut, ada gunanya jika kumpulan data menyertakan nilai-nilai yang bergantung pada bahasa ini. 
 
 Jika kedua metode referensi (`record_id, `record_sub_id) dan `field_value digunakan untuk menerjemahkan nilai yang sama dalam 2 baris berbeda, terjemahan yang disediakan dengan (`record_id, `record_sub_id) akan diutamakan. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `table_name| Jumlah | **Wajib** | Mendefinisikan tabel yang berisi bidang yang akan diterjemahkan. Nilai yang diperbolehkan adalah:<br><br> - `agency<br> - `stops<br> - `routes<br> - `perjalanan`<br> - `stop_times<br> - `pathways<br> - `tingkat`<br> - `feed_info<br> - `attributions<br><br> File apa pun yang ditambahkan ke GTFS akan memiliki nilai `table_name` yang setara dengan nama file, seperti yang tercantum di atas (yaitu, tidak termasuk ekstensi file `.txt`). | 
 | `field_name| Text | **Wajib** | Nama bidang yang akan diterjemahkan. Bidang dengan jenis `Text dapat diterjemahkan, bidang dengan jenis `URL, `Email dan `Phone number juga dapat “diterjemahkan” untuk menyediakan sumber daya dalam bahasa yang benar. Bidang dengan tipe lain tidak boleh diterjemahkan. | 
 | `bahasa` | Kode bahasa | **Wajib** | Bahasa terjemahan.<br><br> Jika bahasanya sama dengan `feed_info.feed_lang, nilai asli kolom tersebut akan dianggap sebagai nilai default untuk digunakan dalam bahasa tanpa terjemahan tertentu (jika `default_lang tidak menentukan sebaliknya).<hr> _Contoh: Di Swiss, sebuah kota di kanton resmi bilingual secara resmi disebut “Biel/Bienne”, namun hanya akan disebut “Bienne” dalam bahasa Prancis dan “Biel” dalam bahasa Jerman._ | 
 | `terjemahan` | Text atau URL atau Email atau Phone number | **Wajib** | Nilai yang diterjemahkan. | 
 | `record_id| ID Asing | **Wajib Bersyarat** | Mendefinisikan catatan yang sesuai dengan bidang yang akan diterjemahkan. Nilai dalam `record_id harus merupakan field pertama atau satu-satunya dari kunci utama tabel, sebagaimana ditentukan dalam atribut kunci utama untuk setiap tabel dan di bawah ini:<br><br> - `agency_id` untuk [agency.txt](#agencytxt)<br> - `stop_id` untuk [stops.txt](#stopstxt);<br> - `route_id` untuk [routes.txt](#routestxt);<br> - `trip_id` untuk [trips.txt](#tripstxt);<br> - `trip_id` untuk [stop_times.txt](#stop_timestxt);<br> - `pathway_id untuk [pathways.txt](#pathwaystxt);<br> - `level_id` untuk [levels.txt](#levelstxt);<br> - `attribution_id untuk [attributions.txt](#attributionstxt).<br><br> Bidang dalam tabel yang tidak ditentukan di atas tidak boleh diterjemahkan. Namun produsen terkadang menambahkan kolom tambahan yang berada di luar spesifikasi resmi dan kolom tidak resmi ini dapat diterjemahkan. Di bawah ini adalah cara yang disarankan untuk menggunakan `record_id untuk tabel tersebut:<br><br> - `service_id untuk [calendar.txt](#calendartxt);<br> - `service_id untuk [calendar_dates.txt](#calendar_datestxt);<br> - `fare_id untuk [fare_attributes.txt](#fare_attributestxt);<br> - `fare_id untuk [fare_rules.txt](#fare_rulestxt);<br> - `shape_id` untuk [shapes.txt](#shapestxt);<br> - `trip_id` untuk [frequencies.txt](#frequenciestxt);<br> - `from_stop_id untuk [transfers.txt](#transferstxt).<br><br> Diperlukan Secara Bersyarat:<br> - **Dilarang** jika `table_name adalah `feed_info.<br> - **Dilarang** jika `field_value` ditentukan.<br> - **Wajib diisi** jika `field_value kosong. | 
 | `record_sub_id| ID Asing | **Wajib Bersyarat** | Membantu record yang berisi field untuk diterjemahkan ketika tabel tidak memiliki ID unik. Oleh karena itu, nilai dalam `record_sub_id` adalah ID sekunder dari tabel, seperti yang ditentukan oleh tabel di bawah:<br><br> - Tidak ada untuk [agency.txt](#agencytxt);<br> - Tidak ada untuk [stops.txt](#stopstxt);<br> - Tidak ada untuk [routes.txt](#routestxt);<br> - Tidak ada untuk [trips.txt](#tripstxt);<br> - `stop_sequence` untuk [stop_times.txt](#stop_timestxt);<br> - Tidak ada untuk [pathways.txt](#pathwaystxt);<br> - Tidak ada untuk [levels.txt](#levelstxt);<br> - Tidak ada untuk [attributions.txt](#attributionstxt).<br><br> Bidang dalam tabel yang tidak ditentukan di atas tidak boleh diterjemahkan. Namun produsen terkadang menambahkan kolom tambahan yang berada di luar spesifikasi resmi dan kolom tidak resmi ini dapat diterjemahkan. Di bawah ini adalah cara yang disarankan untuk menggunakan `record_sub_id` untuk tabel tersebut:<br><br> - Tidak ada untuk [calendar.txt](#calendartxt);<br> - `date untuk [calendar_dates.txt](#tanggal_kalendertxt);<br> - Tidak ada untuk [fare_attributes.txt](#fare_attributestxt);<br> - `route_id` untuk [fare_rules.txt](#fare_rulestxt);<br> - Tidak ada untuk [shapes.txt](#bentuktxt);<br> - `start_time` untuk [frequencies.txt](#frequenciestxt);<br> - `to_stop_id untuk [transfers.txt](#transferstxt).<br><br> Diperlukan Secara Bersyarat:<br> - **Dilarang** jika `table_name adalah `feed_info.<br> - **Dilarang** jika `field_value` ditentukan.<br> - **Wajib** jika `table_name=stop_times` dan `record_id` ditentukan. | 
 | `field_value| Text atau URL atau Email atau Phone number | **Wajib Bersyarat** | Daripada menentukan record mana yang harus diterjemahkan dengan menggunakan `record_id dan `record_sub_id, bidang ini dapat digunakan untuk menentukan nilai yang harus diterjemahkan. Saat digunakan, terjemahan akan diterapkan ketika bidang yang diidentifikasi oleh `table_name dan `field_name berisi nilai yang sama persis yang ditentukan dalam field_value.<br><br> Bidang tersebut harus memiliki **persis** dengan nilai yang ditentukan dalam `field_value. Jika hanya sebagian nilai yang cocok dengan `field_value, terjemahan tidak akan diterapkan.<br><br> Jika dua aturan terjemahan cocok dengan record yang sama (satu dengan `field_value, dan yang lainnya dengan `record_id), aturan dengan `record_id akan diutamakan.<br><br> Diperlukan Secara Bersyarat:<br> - **Dilarang** jika `table_name adalah `feed_info.<br> - **Dilarang** jika `record_id` ditentukan.<br> - **Wajib diisi** jika `record_id kosong. | 
 
### feed_info.txt 
 
 File: **Direkomendasikan** (**Wajib** jika [translations.txt](#translationstxt) disediakan) 
 
 Primary key (none) § § 
 File berisi informasi tentang kumpulan data itu sendiri, bukan layanan yang dijelaskan dalam kumpulan data tersebut. Dalam beberapa kasus, penerbit kumpulan data adalah entity yang berbeda dari lembaga mana pun. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `feed_publisher_name| Text | **Wajib** | Nama lengkap organisasi yang menerbitkan kumpulan data. Ini mungkin sama dengan salah satu nilai `agency.agency_name. | 
 | `feed_publisher_url` | URL | **Wajib** | URL situs web organisasi penerbitan kumpulan data. Ini mungkin sama dengan salah satu nilai `agency.agency_url. | 
 | `feed_lang` | Kode bahasa | **Wajib** | Bahasa default yang digunakan untuk teks dalam kumpulan data ini. Setelan ini membantu konsumen GTFS memilih aturan kapitalisasi dan setelan khusus bahasa lainnya untuk set data. File `translations.txt dapat digunakan jika teks perlu diterjemahkan ke bahasa selain bahasa default.<br><br> Bahasa default mungkin multibahasa untuk kumpulan data dengan teks asli dalam beberapa bahasa. Dalam kasus seperti ini, bidang `feed_lang` harus berisi kode bahasa `mul` yang ditentukan oleh standar ISO 639-2, dan terjemahan untuk setiap bahasa yang digunakan dalam kumpulan data harus disediakan di `translations.txt`. Jika semua teks asli dalam kumpulan data menggunakan bahasa yang sama, maka `mul tidak boleh digunakan.<hr> _Contoh: Misalkan kumpulan data dari negara multibahasa seperti Swiss, dengan kolom asli `stops.stop_name diisi dengan nama perhentian dalam berbagai bahasa. Setiap nama perhentian ditulis sesuai dengan bahasa dominan di lokasi geografis perhentian tersebut, misalnya `Genève untuk kota Geneva yang berbahasa Perancis, `Zürich untuk kota Zurich yang berbahasa Jerman, dan `Biel/Bienne untuk kota bilingual kota Biel/Bienne. Kumpulan data `feed_lang` harus `mul` dan terjemahan akan disediakan dalam `translations.txt`, dalam bahasa Jerman: `Genf`, `Zürich` dan `Biel`; dalam bahasa Perancis: `Genève, `Zurich dan `Bienne; dalam bahasa Italia: `Ginevra, `Zurigo dan `Bienna; dan dalam bahasa Inggris: `Geneva`, `Zurich` dan `Biel/Bienne`._ | 
 | `default_lang| Kode bahasa | Opsional | Menentukan bahasa yang harus digunakan ketika konsumen data tidak mengetahui bahasa pengendara. Seringkali berupa `en` (Bahasa Inggris). | 
 | `feed_start_date| Tanggal | Direkomendasikan | Dataset tersebut memberikan informasi jadwal layanan yang lengkap dan dapat diandalkan dalam periode dari awal hari `feed_start_date hingga akhir hari `feed_end_date. Kedua hari tersebut mungkin dibiarkan kosong jika tidak tersedia.date ` feed_end_date tidak boleh mendahului date ` feed_start_date jika keduanya diberikan. Direkomendasikan agar penyedia kumpulan data memberikan data jadwal di luar periode ini untuk memberi saran tentang kemungkinan layanan di masa mendatang, namun konsumen kumpulan data harus memperhatikan status non-otoritatifnya. Jika ` feed_start_date` atau `feed_end_date` melampaui tanggal kalender aktif yang ditentukan dalam [calendar.txt](#calendartxt) dan [calendar_dates.txt](#calendar_datestxt), kumpulan data membuat pernyataan eksplisit bahwa tidak ada layanan untuk tanggal dalam rentang `feed_start_date atau `feed_end_date tetapi tidak termasuk dalam tanggal kalender aktif. | 
 | `feed_end_date` | Tanggal | Direkomendasikan | (lihat di atas) | 
 | `feed_version| Text | Direkomendasikan | String yang menunjukkan versi set data GTFS saat ini. Aplikasi yang menggunakan GTFS dapat menampilkan nilai ini untuk membantu penerbit set data menentukan apakah set data terbaru telah dimasukkan. | 
 | `feed_contact_email` | Email | Opsional | Alamat Email untuk komunikasi mengenai set data GTFS dan praktik publikasi data. `feed_contact_email` adalah kontak teknis untuk aplikasi yang menggunakan GTFS. Berikan informasi kontak layanan pelanggan melalui [agency.txt](#agencytxt). Disarankan agar setidaknya salah satu dari `feed_contact_email` atau `feed_contact_url` disediakan. | 
 | `feed_contact_url` | URL | Opsional | URL untuk informasi kontak, formulir web, meja dukungan, atau alat komunikasi lainnya mengenai set data GTFS dan praktik publikasi data. `feed_contact_url` adalah kontak teknis untuk aplikasi yang menggunakan GTFS. Berikan informasi kontak layanan pelanggan melalui [agency.txt](#agencytxt). Disarankan agar setidaknya salah satu dari `feed_contact_url` atau `feed_contact_email` disediakan. | 
 
### attributions.txt 
 
 File: **Opsional** 
 
 Kunci utama (`attribution_id`) 
 
 File mendefinisikan attributions yang diterapkan pada kumpulan data. 
 
 | Nama Bidang | Ketik | Kehadiran | Deskripsi | 
 |------|------|------|------| 
 | `attribution_id` | ID Unik | Opsional | Mengidentifikasi atribusi untuk kumpulan data atau subkumpulannya. Ini sebagian besar berguna untuk terjemahan. | 
 | `agency_id| ID asing yang merujuk pada `agency.agency_id| Opsional | Agensi tempat atribusi tersebut berlaku.<br><br> Jika salah satu atribusi `agency_id, `route_id`, atau `trip_id` ditentukan, atribusi lainnya harus kosong. Jika tidak ada satu pun yang ditentukan, atribusi akan diterapkan ke seluruh kumpulan data. | 
 | `route_id` | ID asing yang merujuk pada `routes.route_id| Opsional | Berfungsi dengan cara yang sama seperti `agency_id kecuali atribusi berlaku untuk suatu rute. Beberapa attributions mungkin berlaku untuk rute yang sama. | 
 | `trip_id` | ID asing yang merujuk pada `trips.trip_id` | Opsional | Berfungsi dengan cara yang sama seperti `agency_id kecuali atribusi berlaku untuk perjalanan. Beberapa attributions mungkin berlaku untuk perjalanan yang sama. | 
 | `organization_name| Text | **Wajib** | Nama organisasi tempat kumpulan data dikaitkan. | 
 | `is_producer| Jumlah | Opsional | Peran organisasi adalah produser. Opsi yang valid adalah:<br><br> `0` atau kosong- Organisasi tidak memiliki peran ini.<br> `1` - Organisasi memang memiliki peran ini.<br><br> Setidaknya salah satu bidang `is_producer`, `is_operator`, atau `is_authority` harus disetel pada `1`. | 
 | `is_operator| Jumlah | Opsional | Berfungsi dengan cara yang sama seperti `is_producer kecuali peran organisasi adalah operator. | 
 | `is_authority| Jumlah | Opsional | Berfungsi dengan cara yang sama seperti `is_producer kecuali peran organisasi adalah otoritas. | 
 | `attribution_url| URL | Opsional | URL organisasi. |

 
 | `attribution_email` | Email | Opsional | Email organisasi. | 
 | `attribution_phone| Phone number | Opsional | Phone number organisasi. | 
 

