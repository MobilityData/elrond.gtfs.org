# Add-on dasar 
 Fitur-fitur ini memperluas kemampuan yang dijelaskan di Base, berfungsi untuk meningkatkan kelengkapan set data GTFS guna memberikan pengalaman yang lebih baik bagi pengguna, atau memfasilitasi kolaborasi antar lembaga, vendor data, dan pengguna ulang data. Peningkatan ini mungkin memerlukan pengenalan bidang baru dalam file yang dijelaskan di Base, atau membuat file baru. 
 
## Informasi Feed 
 
 Informasi Feed mengkomunikasikan informasi penting tentang feed, seperti validitasnya ( date mulai dan berakhir), organisasi penerbit, dan informasi kontak untuk pertanyaan mengenai set data GTFS dan praktik penerbitan data. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`, `feed_publisher_url`, `feed_lang`, `default_lang`, `feed_start_date`, `feed_end_date`, `feed_version`, `feed_contact_email`, `feed_contact_url` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 
 
 | feed_publisher_name | feed_publisher_url | feed_lang | default_lang | feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |--------------------------|----------------------|-----------|--------------|-----------------|---------------|--------------|--------------------|------------------------------| 
 | Transportasi Wilayah Besar | https://www.gra1.org | id | id | 20240101 | 20241231 | 3.1 | support@gra1.org | https://www.gra1.org/support | 
 
## Bentuk 
 Bentuk dapat didefinisikan dan dikaitkan dengan perjalanan, memungkinkan aplikasi perencanaan perjalanan menampilkan perjalanan pada peta dan memberi tahu pengendara tentang jarak yang harus mereka tempuh dengan vehicle transit. Bidang `shape_dist_traveled` digunakan untuk menentukan secara terprogram berapa banyak shape yang akan digambar saat menampilkan peta kepada pengendara. 
 Saat mendefinisikan Bentuk, ada keseimbangan antara tingkat detailnya (misalnya mengikuti kelengkungan jalan yang tepat) dan hanya menyampaikan informasi yang diperlukan secara efisien. 
 
 |File disertakan |Kolom disertakan | 
 |----------------------------------|----------------------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`, `shape_pt_lat`, `shape_pt_lon`, `shape_pt_sequence, `shape_dist_traveled` | 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled`| 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan sebagian shape dari feed GTFS TriMet (unduh <a     href="https://developer.trimet.org/GTFS.shtml">di sini</a> ).<br><br> 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 
 
 | shape_id | shape_pt_lat | shape_pt_lon | shape_pt_sequence | shape_dist_traveled | 
 |---------|-------------|-------------|----|-------------------| 
 | 558674 | 45.47623 |-122.721885 | 1 | 0,0 | 
 | 558674 | 45.476235 |-122.72236 | 2 | 121.9 | 
 | 558674 | 45.476237 |-122.722523 | 3 | 163,7 | 
 | 558674 | 45.476242 |-122.723024 | 4 | 292.2 | 
 | 558674 | 45.476244 |-122.72316 | 5 | 327.1 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 
 
 | trip_id | shape_id| 
 |--------|--------| 
 |13302375|558674 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 
 
 | trip_id | stop_sequence| shape_dist_traveled| 
 |--------|-------------|-------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## Warna Rute 
 
 Menggunakan Warna Rute memungkinkan untuk secara akurat menggambarkan dan mengkomunikasikan skema warna yang ditetapkan untuk routes tertentu berdasarkan pedoman desain lembaga. Hal ini memungkinkan pengguna dengan mudah mengidentifikasi layanan transportasi umum berdasarkan warna resminya. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`, `route_text_color` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan bahwa rute `RA` berwarna oranye menggunakan kode warna HEX `D95700`, dan teks tersebut harus ditampilkan hitam menggunakan kode warna HEX `0`. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |----------|-----------|------------------|--------------------|------------|-------------|------------------| 
 | RA | agensi001 | 17 | Misi- Pusat Kota | 3 | D95700 | 0 | 
 
## Sepeda Diizinkan 
 
 Sepeda Diizinkan menunjukkan apakah kendaraan yang melayani perjalanan tertentu mampu mengakomodasi sepeda atau tidak, membantu pengguna merencanakan dan mengakses layanan yang memungkinkan mereka melakukan perjalanan multimoda. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menetapkan bahwa vehicle yang digunakan dalam perjalanan `AWE1` dapat menampung setidaknya satu sepeda di dalamnya (`bikes_allowed=1`), dan vehicle yang digunakan dalam perjalanan `AWE2` tidak dapat (`bikes_allowed=2`). 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|------------|---------|---------------| 
 | RA | KAMI | AWE1 | 1 | 
 | RA | KAMI | AWE2 | 2 | 
 
## Tanda Kepala 
 
 Tanda Kepala memungkinkan untuk mengkomunikasikan tanda yang digunakan oleh kendaraan yang menunjukkan tujuan perjalanan, sehingga memudahkan pengguna untuk mengidentifikasi layanan transit yang benar. Fitur ini mendukung perubahan headsign sepanjang rute tertentu. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Dalam contoh berikut, tabel pertama menentukan tanda kepala yang akan digunakan oleh perjalanan `AWE1` dan `AWE2, dan tabel kedua menunjukkan bahwa tanda kepala `AWE1 akan diubah setelah pemberhentian `TAS004`, menggantikan yang satu ditentukan dalam `trips.txt. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_headsign | 
 |----------|------------|---------|---------------| 
 | RA | KAMI | AWE1 | Pusat kota | 
 | RA | KAMI | AWE2 | Misi | 
 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | stop_headsign | 
 |---------|--------------|----------------|---------|---------------|---------| 
 | AWE1 | 06:10:00 | 06:10:00 | TAS001 | 1 | | 
 | AWE1 | 06:14:00 | 06:14:00 | TAS002 | 2 | | 
 | AWE1 | 06:20:00 | 06:20:00 | TAS003 | 3 | | 
 | AWE1 | 06:23:00 | 06:23:00 | TAS004 | 4 | Pusat Kota- Alun-Alun Utama | 
 | AWE1 | 06:25:00 | 06:25:00 | TAS005 | 5 | Pusat Kota- Alun-Alun Utama | 
 
## Tipe Lokasi 
 
 Tipe Lokasi digunakan untuk mengklasifikasikan area utama dalam stasiun transit seperti pintu keluar/pintu, simpul atau area keberangkatan, serta hubungannya. Jenis Lokasi berfungsi sebagai dasar untuk memodelkan stasiun transit menggunakan Pathways. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan beberapa lokasi dalam stasiun transit di `stops.txt`: stasiun induk, yang mewakili lokasi utama, dan lokasi turunannya seperti peron, pintu masuk/keberadaan, dan node generik. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | location_type | parent_station | 
 |--------------|-------------------------------------------------------|---------------|----------------| 
 | Stasiun_A102 | Stasiun Jalan Utama | 1 | | 
 | A102_B01 | Stasiun Jalan Utama- Peron Utara | 0 | Stasiun_A102 | 
 | A102_B02 | Stasiun Jalan Utama- Peron Selatan | 0 | Stasiun_A102 | 
 | A102_E01 | Stasiun Jalan Utama- Pintu Masuk/Keluar | 2 | Stasiun_A102 | 
 | A102_S01 | Stasiun Jalan Utama- Puncak tangga masuk | 3 | Stasiun_A102 | 
 | A102_S02 | Stasiun Jalan Utama- Bagian bawah tangga masuk | 3 | Stasiun_A102 | 
 | A102_S03 | Stasiun Jalan Utama- Puncak tangga peron utara | 3 | Stasiun_A102 | 
 | A102_S04 | Stasiun Jalan Utama- Bawah tangga peron utara | 3 | Stasiun_A102 | 
 | A102_S05 | Stasiun Jalan Utama- Puncak tangga peron selatan | 3 | Stasiun_A102 | 
 | A102_S06 | Stasiun Jalan Utama- Bawah tangga peron selatan | 3 | Stasiun_A102 | 
 | A102_F01 | Stasiun Jalan Utama- Sisi gerbang tarif berbayar | 3 | Stasiun_A102 | 
 | A102_F02 | Stasiun Jalan Utama- Sisi gerbang tarif yang belum dibayar | 3 | Stasiun_A102 | 
 
## Layanan Berbasis Frekuensi 
 
 Layanan Berbasis Frekuensi dapat digunakan untuk memodelkan layanan yang beroperasi pada frekuensi reguler, seperti bus yang beroperasi setiap 10 menit atau layanan kereta bawah tanah yang beroperasi 2 menit dalam interval waktu tertentu. 
 Saat memodelkan Layanan Berbasis Frekuensi, `stop_times.txt` berisi waktu relatif antar stops untuk menentukan waktu yang akan ditampilkan kepada pengendara. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| `trip_id`, `start_time`, `end_time`, `headway_secs`, `exact_times` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan dua perjalanan berbeda: perjalanan `AWE1` yang berjalan setiap 30 menit (`headway_secs=1800`), dan perjalanan `AWE2` yang berjalan setiap 15 menit (`headway_secs=900`). 
<p style="font-size:16px"> 
 Bidang `exact_times` menunjukkan apakah jadwal mengikuti waktu mulai tepat yang dimasukkan dalam bidang ’ start_time’: 
 - Perjalanan `AWE1 berangkat setiap 30 menit mulai pukul 06:10 hingga 12:00. 
 - perjalanan `AW2` berangkat pukul 06.00, 06.15, 06.30, dan seterusnya. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 
 
 | trip_id | start_time | end_time | headway_secs | exact_times | 
 ---------|------------|----------|--------------|-------------| 
 AWE1 | 06:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 06:00:00 | 19:50:00 | 900 | 1 | 
 
## Transfer 
 
 Transfer memberikan rincian tentang transisi antara segmen (atau bagian) perjalanan yang berbeda, memungkinkan perencana perjalanan menentukan kelayakan perjalanan yang mencakup transfers. Menentukan transfers tidak berarti penumpang tidak dapat melakukan transfer ke tempat lain, hal ini hanya menunjukkan apakah transfers tertentu tidak dapat dilakukan atau require waktu minimum untuk transfer. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, `from_trip_id`, `to_trip_id`, `transfer_type, `min_transfer_time| 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan tiga transfers yang berbeda: satu perpindahan antar stops yang membutuhkan waktu perpindahan minimal 5 menit, satu titik perpindahan berjangka waktu antara dua routes, dan satu perpindahan di kursi antara dua perjalanan yang dilakukan dengan vehicle yang sama. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 
 
 | from_stop_id | to_stop_id | from_route_id | to_route_id | from_trip_id | to_trip_id | transfer_type | min_transfer_time | 
 |--------------|------------|---------------|-------------|--------------|------------|---------------|-------------------| 
 | s6 | s7 | | | | | 2 | 300 | 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## Terjemahan 
 
 Terjemahan memungkinkan informasi layanan seperti nama stasiun disediakan dalam berbagai bahasa sehingga perencana perjalanan dapat menampilkan informasi dalam bahasa tertentu tergantung pada pengaturan bahasa dan lokasi pengguna. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`bahasa`,`terjemahan`,`record_id`,` `record_sub_id`,`field_value| 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan terjemahan bahasa Prancis dan Spanyol disediakan untuk dua bidang yang digunakan di `routes.txt: `route_long_name dan `route_desc. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 
 
 | table_name | field_name | bahasa | terjemahan | record_id | record_sub_id | field_value | 
 |------------|-----------------|----------|--------------------------------------------------------|-----------|---------------|-------------| 
 | routes | route_long_name | ES | Misi- Pusat | RA | | | 
 | routes | route_long_name | FR | Misi- Pusat ville | RA | | | 
 | routes | route_desc | ES | Rute "A" viaja dari Lower Mission sampai ke pusat | RA | | | 
 | routes | route_desc | FR | Rute « A » bergantung pada Misi Bawah di pusat kota. | RA | | | 
 
## Atribusi 
 
 Atribusi memungkinkan untuk berbagi detail tambahan mengenai organisasi yang terlibat dalam pembuatan kumpulan data (produsen, operator dan/atau otoritas, dll.). 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`, `agency_id`, `route_id`, `trip_id`, `organization_name`, `is_producer`, `is_operator`, `is_authority`, `attribution_url`, `attribution_email`, `attribution_phone` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 
 
 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |----------------|-----------|----------|---------|-----------|-------------|-------------|--------------|----------------------------------|----------|-------------------| 
 | op01 | tb | | | Bus Transit | | 1 | | https://www.transitbus.org/fares | hubungi@transitbus.org | (777) 555-7777 | 
 | au01 | gra | | | Transportasi Wilayah Besar | 1 | | 1 | https://www.gra1.org | hubungi@gra1.org | (555) 555-5555 | 
 | op02 | | rtd023 | | Perusahaan bus A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | op03 | | rtd025 | | Perusahaan bus B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

