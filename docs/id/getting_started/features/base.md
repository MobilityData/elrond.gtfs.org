# Basis 
 Fitur berikut menyediakan elemen paling mendasar dan penting yang dibutuhkan GTFS untuk mewakili layanan transportasi umum. GTFS terdiri dari routes, yang masing-masing berisi perjalanan terkait. Perjalanan ini mengunjungi satu atau lebih stops pada waktu tertentu. Perjalanan hanya berisi informasi waktu, dan hari pengoperasiannya ditentukan oleh kalender. 
 Semua fitur ini harus diterapkan bersama-sama agar feed GTFS dapat berfungsi. 
 
## Agensi 
 
 Agen berisi informasi dasar tentang lembaga yang bertanggung jawab atas layanan transportasi umum, seperti nama, URL situs web, serta bahasa dan zona waktu di mana layanan tersebut beroperasi. Hal ini memungkinkan untuk mencocokkan layanan tertentu dengan agency terkait mereka. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url, `agency_email| 
 
 **Prasyarat**: 
 
 - Semua fitur Basis lainnya 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 
 
 | agency_id | agency_name | agency_url | agency_timezone | agency_lang | agency_phone | agency_fare_url | agency_email | 
 |-----------|-------------|----------------------------|------|-------------|-------------------------------|----------------------------------|------------------------| 
 | tb | Bus Transit | https://www.transitbus.org | America/Los_Angeles | EN | (777) 555-7777 | https://www.transitbus.org/fares | hubungi@transitbus.org | 
 
 
 
## Perhentian 
 
 Perhentian mewakili elemen dasar yang digunakan untuk mengidentifikasi di mana layanan transit mengambil dan menurunkan penumpang. Ini bisa berupa stasiun metro atau halte bus. Setiap perhentian memiliki, antara lain, koordinat geografis untuk menunjukkan lokasinya di peta, dan nama yang cocok dengan materi yang diketahui oleh pengendara dari agensi tersebut. Pemberhentian dikaitkan dengan Perjalanan menggunakan Waktu Berhenti. 
 Dengan GTFS, Anda juga dapat mendeskripsikan interior stasiun yang lebih besar, seperti stasiun kereta atau depo bus, menggunakan [Pathways](/getting_started/features/pathways). 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`, `stop_code`, `stop_name`, `stop_desc`, `stop_lat`, `stop_lon`, `stop_url`, `stop_timezone`, `platform_code` | 
 
 **Prasyarat**: 
 
 - Semua fitur Basis lainnya 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_code | stop_desc | stop_name | stop_lat | stop_lon | stop_url | stop_timezone | platform_code | 
 |---------|-----------|--------------------------------------------|------------|-----------|---------------------------|--------------------------|---------------|---------------| 
 | TAS001 | TAS001 | Sudut barat daya 5 Avenue dan 53 Street | 5 Av/53 St | 45.503568 |-73.587079 | stops| | | 
 
 
## Rute 
 
 Rute adalah sekelompok perjalanan dengan merek yang sama yang ditampilkan kepada pengendara sebagai satu layanan. Setiap rute memiliki, antara lain, atribut, nama yang sesuai dengan materi yang diketahui oleh pengendara dari agensi tersebut, dan jenis layanan yang diwakili (seperti bus, kereta bawah tanah atau metro, feri, dll.). 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`, `agency_id, `route_desc, `route_type, `route_url, `route_sort_order, `route_short_name, `route_long_name| 
 
 **Prasyarat**: 
 
 - Semua fitur Basis lainnya 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mendefinisikan rute bus (`route_type=3`). 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |----------|-----------|------------------|-----------------------------------|-------------------------------------------------------|------------|--------------------------------------|------------------| 
 | RA | tb | 17 | Misi- Pusat Kota | Rute "A" berangkat dari Mission bawah ke Pusat Kota. | 3 | https://www.transitbus.org/rute/ra | 12 | 
 
 
## Tanggal Layanan 
 
 Tanggal Layanan menunjukkan rentang tanggal di mana layanan berjalan, serta membuat pengecualian layanan seperti hari libur dan layanan khusus lainnya pada tanggal tertentu. 
 Ia bekerja dengan menentukan date mulai dan date selesai di `kalender.txt`, lalu penanda untuk setiap hari dalam seminggu di mana ia beroperasi. Jika ada perubahan penjadwalan satu hari yang terjadi selama periode ini, maka file `calendar_dates.txt` dapat digunakan untuk mengganti jadwal setiap hari tersebut. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **Prasyarat**: 
 
 - Semua fitur Basis lainnya 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mendefinisikan dua layanan (hari kerja dan akhir pekan) untuk bulan Juli 2024, termasuk layanan hari libur khusus pada tanggal 4 Juli, yang beroperasi sebagai layanan akhir pekan. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 
 
 | service_id | monday | tuesday | wednesday | thursday | friday | saturday | sunday | start_date | end_date | 
 |------------|--------|---------|-----------|----------|--------|----------|--------|------------|----------| 
 | KAMI | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | WD | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 
 
 | service_id | date | exception_type | 
 |------------|----------|----------------| 
 | WD | 20240704 | 2 | 
 | KAMI | 20240704 | 1 | 
 
## Perjalanan 
 
 Perjalanan menyatukan Rute dan tanggal Layanan untuk menciptakan perjalanan yang dapat dilakukan oleh pengendara. Perjalanan dikaitkan dengan Berhenti menggunakan Waktu Berhenti. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **Prasyarat**: 
 
 - Semua fitur Basis lainnya 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mendefinisikan dua perjalanan yang berjalan di kedua arah untuk rute RA. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |----------|------------|---------|-----------------|--------------|----------| 
 | RA | KAMI | AWE1 | 3885 | 0 | 1 | 
 | RA | KAMI | AWE2 | 3887 | 1 | 2 | 
 
## Waktu Berhenti 
 
 Waktu berhenti digunakan untuk mewakili waktu arrival dan departure untuk setiap perjalanan, sehingga penumpang dapat mengetahui dengan tepat jam berapa bus, kereta api, atau kapal feri tiba dan berangkat dari lokasi tertentu. File `stop_times.txt` biasanya merupakan file terbesar dalam feed GTFS. 
 Layanan tertentu beroperasi pada frekuensi reguler (misalnya jalur kereta bawah tanah yang beroperasi setiap 5 menit) daripada memiliki waktu arrival dan departure tertentu. Hal ini dapat dimodelkan menggunakan [Layanan berbasis frekuensi](../base_add-ons/#frekuensi-based-service), dan ini dapat dimodelkan bersama dengan `stop_times.txt`. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`, `arrival_time`, `departure_time`, `stop_id`, `stop_sequence`, `pickup_type, `drop_off_type, `timepoint| 
 
 **Prasyarat**: 
 
 - Semua fitur Basis lainnya 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menentukan jadwal perjalanan di 5 stops. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | pickup_type | drop_off_type | timepoint | 
 |---------|--------------|----------------|---------|---------------|-------------|---------------|-----------| 
 | AWE1 | 06:10:00 | 06:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 06:14:00 | 06:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 06:20:00 | 06:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 06:23:00 | 06:23:00 | TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 06:25:00 | 06:25:00 | TAS005 | 5 | 0 | 0 | 1 | 
 

