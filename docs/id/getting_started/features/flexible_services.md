# Layanan Fleksibel 
 Layanan fleksibel, juga disebut layanan tanggung jawab permintaan, adalah layanan yang tidak mengikuti perilaku umum layanan terjadwal dan/atau tetap. 
 
## Pemberhentian Berkelanjutan 
 
 Pemberhentian Berkelanjutan digunakan ketika pengendara dapat dijemput dan/atau diturunkan di antara stops yang dijadwalkan. 
 Hal ini dapat ditentukan di `routes.txt, yang menunjukkan bahwa pengendara dapat dijemput atau diturunkan kapan saja di sepanjang jalur perjalanan kendaraan untuk setiap perjalanan dalam rute tersebut, atau di `stop_times.txt` untuk bagian tertentu dari sebuah rute. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off` | 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan dua cara untuk merepresentasikan Berhenti Berkelanjutan. 
</p> 
 
<p style="font-size:16px"> 
 Sampel pertama menunjukkan bahwa penjemputan dan pengantaran diperbolehkan di titik mana pun sepanjang rute `RA`. 
</p> 
 
<p style="font-size:16px"> 
 Sampel kedua menunjukkan bahwa penjemputan dan pengantaran diperbolehkan antara stops ketiga dan kelima perjalanan `AWE1`, dilakukan dengan menetapkan nilai `continuous_pickup` dan `continuous_drop_off` ke `stop_sequence=3` dan `stop_sequence=4`. 
</p> 
 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | route_short_name | route_type | continuous_pickup | continuous_drop_off | 
 |----------|------------------|------------|-------------------|---------------------| 
 | RA | 17 | 3 | 0 | 0 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | continuous_pickup | continuous_drop_off | 
 |---------|--------------|----------------|---------|---------------|-------------------|---------------------| 
 | AWE1 | 06:10:00 | 06:10:00 | TAS001 | 1 | | | 
 | AWE1 | 06:14:00 | 06:14:00 | TAS002 | 2 | | | 
 | AWE1 | 06:20:00 | 06:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 06:23:00 | 06:23:00 | TAS004 | 4 | 0 | 0 | 
 | AWE1 | 06:25:00 | 06:25:00 | TAS005 | 5 | | | 
 
## Aturan Pemesanan 
 
 Aturan Pemesanan dapat digunakan untuk memungkinkan pengguna memesan perjalanan pada layanan yang responsif terhadap permintaan. Aturan ini menguraikan prasyarat yang diperlukan agar pemesanan berhasil dan memberikan informasi kontak di mana pengguna dapat melakukan reservasi perjalanan. Fitur ini harus digunakan bersama dengan [Rute yang Telah Ditentukan dengan Deviasi](#rute-yang-ditentukan-dengan-deviasi), [Layanan Responsif Permintaan Berbasis Zona](#layanan-layanan-responsif-permintaan berbasis-zona) dan [Perhentian-Tetap Layanan Responsif Permintaan](#layanan-permintaan-responsif-permintaan-tetap) fitur, jika layanan tersebut require pemesanan. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`, `booking_type`, `prior_notice_duration_min`, `prior_notice_duration_max`, `prior_notice_last_day`, `prior_notice_last_time `, `prior_notice_start_day`, `prior_notice_start_time`, `prior_notice_service_id`, `message, `pickup_message`, `drop_off_message`, `phone_number`, `info_url`, `booking_url` | 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan dua rangkaian aturan pemesanan yang berbeda, yang pertama untuk perjalanan yang harus dipesan setidaknya satu hari sebelumnya (sebelum jam 1 siang) dan tidak lebih dari 14 hari sebelumnya, dan yang kedua untuk perjalanan yang bisa dipesan setidaknya 45 menit sebelum perjalanan dan tidak lebih dari 5 jam sebelumnya. 
 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 
 
 | booking_rule_id | tipe_pemesanan | prior_notice_duration_min | prior_notice_duration_max | sebelumnya_pemberitahuan_hari_terakhir | sebelumnya_pemberitahuan_waktu_terakhir | sebelumnya_pemberitahuan_mulai_hari | waktu_mulai_pemberitahuan_sebelumnya | prior_notice_service_id | message | pesan_ambilan | drop_off_message | nomor_telepon | info_url | pemesanan_url | 
 |-----------------|--------------|---------------------------|---------------------------|-----------------------|------------------------|------------------------|-------------------------|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------|----------------|----------------------|-----------| 
 | rute_br_1818 | 2 | | | 1 | 13:00 | 14 | 9:00 | | Untuk meminta tumpangan, hubungi 123-111-2233 sebelum jam 1 siang setidaknya satu hari kerja sebelum perjalanan Anda. Anda dapat memesan perjalanan hingga 14 hari kerja sebelumnya. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | rute_br_4545 | 1 | 45 | 300 | | | | | | Untuk meminta tumpangan, gunakan sistem pemesanan resmi di website kami, perjalanan harus dipesan setidaknya 45 menit sebelumnya | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## Rute yang Telah Ditentukan dengan Deviasi 
 
 Rute yang Telah Ditentukan dengan Deviasi dapat digunakan untuk memodelkan layanan fleksibel di mana kendaraan dapat menyimpang sebentar dari rute tertentu untuk menjemput pengguna yang memesan perjalanan dalam area tertentu di sepanjang rute. Ini menggunakan kombinasi stops tradisional (seperti layanan terjadwal reguler) dan zona yang menggunakan `locations.geojson`. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Jenis`, `Fitur`, `Fitur:Jenis`, `Fitur:Id`, `Fitur :Properties`, `Fitur:Properti:Stop_name`, `Fitur:Properti:Stop_description`, `Fitur:Geometri`, `Fitur:Geometri:Jenis`, `Fitur:Geometri:Koordinat` | 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Aturan Pemesanan](#aturan-booking) jika layanan memerlukan pemesanan 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan perjalanan dengan tiga stops tetap yang juga dapat menurunkan penumpang di mana saja dalam area tertentu yang ditentukan di antara stops tetap tersebut. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | lokasi_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|--------------|----------------|---------|-----------------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------------------|---------|--------------------------| 
 | 4545_001 | 10:00:00 | 10:00:00 | S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | zona_S50122_to_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | zona_S50123_to_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "type": "FeatureCollection", 
 "features": [
 { 
 "id": "zone_S50122_to_S50123", 
 "type": "Fitur", 
 "geometri": { 
 "type": "Polygon", 
# Disederhanakan, disini hanya menampilkan 3 koordinat. 
 "koordinat": [
 [
 [
 -73.575952, 
 45.514974 
], 
 [
 -73.577314, 
 45.513433 
], 
 [
 -73.5 69794, 
 45.5098370 
] 
] 
] 
 }, 
 "properti": {} 
 }, 
 { 
 "id": "zone_S50123_to_S50124", 
 "type": "Fitur", § § "geometri": { 
 "type": "Polygon", 
# Disederhanakan, disini hanya menampilkan 3 koordinat. 
 "koordinat": [
 [
 [
 -73.561332, 
 45.5085599 
], 
 [
 -73.5701298, 
 45.5124057 
], 
 [
 -7 3.571302, 
 45.5105563 
] 
] 
] 
 }, 
 "properti": {} 
 } 
] 
 } 
 ~~~ 
 
## Layanan Responsif Permintaan Berbasis Zona 
 
 Layanan Responsif Permintaan Berbasis Zona digunakan untuk memodelkan layanan yang memungkinkan penjemputan dan/atau pengantaran di lokasi mana pun dalam area tertentu bagi pengguna yang memesan perjalanan. Area ini ditentukan menggunakan `locations.geojson` sehingga tidak require penggunaan `stops.txt` atau `stop_times.arrival_time` &amp; `stop_times.departure_time`. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Jenis`, `Fitur`, `Fitur:Jenis`, `Fitur:Id`, `Fitur :Properti`, `Fitur:Properti:Stop_name`, `Fitur:Properti:Stop_description`, `Fitur:Geometri`, `Fitur:Geometri:Jenis`, `Fitur:Geometri:Koordinat` | 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Aturan Pemesanan](#aturan-booking) jika layanan memerlukan pemesanan 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan layanan yang dapat menjemput dan menurunkan penumpang yang telah dipesan sebelumnya di mana saja antara area tertentu antara pukul 09.00 dan 18.00. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | lokasi_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2708_001 | daerah_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | daerah_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "type": "FeatureCollection", 
 "features": [
 { 
 "id": "area_001", 
 "type": "Fitur", 
 "geometri": { 
 "type": "Polygon", 
# Disederhanakan, disini hanya menampilkan 3 koordinat. 
 "koordinat": [
 [
 [
 -73.644437, 
 45.5023960 
], 
 [
 -73.641593, 
 45.5054392 
], 
 [
 -73 .636580, 
 45.5081683 
] 
] 
] 
 }, 
 "properties": {} 
 } 
] 
 } 
 ~~~ 
 
## Layanan Responsif Permintaan Penghentian Tetap 
 Layanan Responsif Permintaan Perhentian Tetap digunakan untuk memodelkan layanan yang memungkinkan penjemputan dan/atau pengantaran di lokasi mana pun dalam grup stops yang telah ditentukan sebelumnya bagi pengguna yang memesan perjalanan. Grup stops ini ditentukan menggunakan `location_groups.txt` dan `location_group_stops.txt`. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Aturan Pemesanan](#aturan-booking) jika layanan memerlukan pemesanan 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan layanan yang dapat menjemput dan menurunkan penumpang yang telah dipesan sebelumnya di 4 stops berbeda antara pukul 7 pagi dan 10 pagi. 
 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_groupstxt"><b>lokasi_grup.txt</b></a><br> 
</p> 
 
 | location_group_id | lokasi_nama_grup | 
 |-------------------|-------------------------------| 
 | r27_stop | stops Rute 27 Sektor Kuning | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>location_group_stops.txt</b></a><br> 
</p> 
 
 | location_group_id | stop_id | 
 |-------------------|---------| 
 | r27_stop | syb029 | 
 | r27_stop | syb030 | 
 | r27_stop | syb031 | 
 | r27_stop | syb032 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | location_group_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2714_002 | r27_stop | 1 | 07:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_stop | 2 | 07:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

