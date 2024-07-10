# Aksesibilitas 
 Fitur Aksesibilitas dimaksudkan untuk memberikan informasi yang dibutuhkan penyandang disabilitas untuk mengakses layanan. 
 
## Berhenti Aksesibilitas Kursi Roda 
 
 Berhenti Aksesibilitas Kursi Roda memungkinkan untuk menunjukkan apakah naik kursi roda dapat dilakukan dari lokasi yang ditentukan. Untuk melayani pengendara yang menggunakan kursi roda, menentukan bahwa menaiki kursi roda dapat dilakukan sama pentingnya dengan menentukan bahwa hal tersebut tidak t. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Jenis Lokasi](../base_add-ons/#location-types) saat menentukan informasi aksesibilitas untuk lokasi stasiun seperti pintu masuk/keluar atau area pemberangkatan. 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan boarding kursi roda tersedia di halte `TAS001` menggunakan `wheelchair_boarding=1`. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|-----------|------------|---------------|---------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 | | 1 | 
 
 
## Perjalanan Aksesibilitas Kursi Roda 
 
 Perjalanan Aksesibilitas Kursi Roda memungkinkan untuk menunjukkan apakah vehicle dapat mengakomodasi pengendara yang menggunakan kursi roda. Untuk melayani pengendara yang menggunakan kursi roda, menentukan bahwa suatu vehicle dapat mengakomodasi pengendara yang menggunakan kursi roda sama pentingnya dengan menetapkan bahwa suatu vehicle tidak dapat mengakomodasi. Perhentian dan perjalanan harus dapat diakses oleh kursi roda agar penumpang dapat mengakses perjalanan di perhentian tersebut. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan bahwa vehicle yang digunakan dalam perjalanan `AWE1 dilengkapi untuk menampung setidaknya satu kursi roda, dan vehicle yang digunakan dalam perjalanan `AWE2 tidak. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | wheelchair_accessible | 
 |----------|------------|---------|-----------------------| 
 | RA | KAMI | AWE1 | 1 | 
 | RA | KAMI | AWE2 | 2 | 
 
 
## Text-to-Speech 
 
 Text-to-Speech memungkinkan untuk memberikan masukan yang diperlukan untuk mengubah teks menjadi audio, memastikan bahwa pengendara yang menggunakan teknologi bantu untuk membaca teks dengan keras mendapatkan nama perhentian yang tepat saat menggunakan layanan transit. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menyediakan versi nama perhentian yang dapat dibaca, sehingga alat text-to-speech dapat membacakan nama tersebut dengan lantang. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|------------|-------------|------------|-----------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 | Jalan 5 dan Jalan 53 | 
 

