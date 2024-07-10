# Jalur 
 Fitur jalur dapat memodelkan stasiun transit besar, memandu pengendara dari pintu masuk stasiun dan berada ke lokasi di mana mereka naik atau turun dari vehicle transit. Beberapa fitur ini memungkinkan untuk mengomunikasikan karakteristik fisik jalur dan perkiraan waktu navigasi, serta sistem pencarian jalan di dunia nyata yang digunakan di stasiun. 
 
## Koneksi Jalur 
 
 Pada tingkat dasar, Pathways menawarkan fungsionalitas dasar untuk menghubungkan area utama yang ditentukan dalam Tipe Lokasi di dalam stasiun. Koneksi ini membentuk pathways, yang memungkinkan pengguna memperoleh petunjuk arah yang tepat (misalnya dari pintu masuk ke area keberangkatan), yang khususnya berguna dalam menavigasi stasiun transit yang besar dan kompleks. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`pathway_id`, `from_stop_id`, `to_stop_id`, `pathway_mode`, `is_bidirectional` | 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Jenis Lokasi](../base_add-ons/#location-types) 
 
 ? ?? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mendefinisikan beberapa koneksi (juga disebut sebagai pathways) antara lokasi yang telah ditentukan sebelumnya (didefinisikan sebagai stops): jalan setapak (`pathway_mode=1`), tangga (`pathway_mode=2`), dan gerbang tarif (`pathway_mode=6`). Dua arah juga ditentukan. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | from_stop_id | to_stop_id | pathway_mode | is_bidirectional | 
 |------------|--------------|------------|--------------|------------------| 
 | MainSt-001 | A102_E01 | A102_S01 | 1 | 1 | 
 | MainSt-002 | A102_S01 | A102_S02 | 2 | 1 | 
 | MainSt-003 | A102_S02 | A102_F02 | 1 | 1 | 
 | MainSt-004 | A102_F02 | A102_F01 | 6 | 1 | 
 | MainSt-005 | A102_F01 | A102_S03 | 1 | 1 | 
 | MainSt-006 | A102_S03 | A102_S04 | 2 | 1 | 
 | MainSt-007 | A102_F01 | A102_S05 | 1 | 1 | 
 | MainSt-008 | A102_S05 | A102_S06 | 2 | 1 | 
 | MainSt-009 | A102_S04 | A102_B01 | 1 | 1 | 
 | MainSt-010 | A102_S06 | A102_B02 | 1 | 1 | 
 
 
## Detail Jalur 
 
 Detail lebih lanjut dapat ditambahkan mengenai karakteristik fisik pathways stasiun, termasuk panjang, lebar dan kemiringan (untuk jalur landai) atau jumlah tangga (untuk tangga). Hal ini membantu pengendara mengantisipasi kondisi dan aksesibilitas jalur yang perlu mereka lalui. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`max_slope`, `min_width`, `length`, `stair_count`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Koneksi Jalur](#koneksi jalur) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mendefinisikan detail tambahan pada pathways yang telah ditentukan sebelumnya termasuk lebar minimum, jumlah langkah untuk tangga dan panjang serta kemiringan maksimum untuk jalan setapak. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | max_slope | min_width | panjang | stair_count | 
 |------------|-----------|-----------|--------|-------------| 
 | MainSt-001 | 0 | 4.3 | 3.6 | | 
 | MainSt-002 | | 2.2 | | 15 | 
 | MainSt-003 | 0,06 | 4 | 3.1 | | 
 | MainSt-004 | | 0,9 | 2.9 | | 
 | MainSt-005 | 0 | 3,5 | 5 | | 
 | MainSt-006 | | 2.2 | | 18 | 
 | MainSt-007 | 0 | 3,5 | 5 | | 
 | MainSt-008 | | 2.2 | | 18 | 
 | MainSt-009 | 0 | 6 | 2 | | 
 | MainSt-010 | 0 | 6 | 2 | | 
 
 
## Level 
 
 Level dapat digunakan untuk membuat daftar semua level berbeda dalam suatu stasiun, sehingga memberi pengguna lapisan informasi tambahan ke stasiun. Fitur ini juga memungkinkan penggunaan elevator bersamaan dengan fitur koneksi Pathways. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[levels.txt](../../../documentation/schedule/reference/#levelstxt)|`level_id`, `level_index`, `level_name`| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`level_id`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Jenis Lokasi](../base_add-ons/#location-types) 
 
 ? ?? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan berbagai level di sebuah stasiun. Lokasi (didefinisikan sebagai stops) kemudian ditetapkan ke tingkat yang sesuai. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | level_id | level_index | level_name | 
 |-------------------|-------------|------------| 
 | level_0_jalan | 0 | Di jalan | 
 | level_-1_lobi |-1 | Lobi | 
 | level_-2_platform |-2 | Peron | 
 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | stop_id | level_id | 
 |--------------|----------| 
 | Stasiun_A102 | | 
 | A102_B01 |-2 | 
 | A102_B02 |-2 | 
 | A102_E01 | 0 | 
 | A102_S01 | 0 | 
 | A102_S02 |-1 | 
 | A102_S03 |-1 | 
 | A102_S04 |-2 | 
 | A102_S05 |-1 | 
 | A102_S06 |-2 | 
 | A102_F01 |-1 | 
 | A102_F02 |-1 | 
 
 
## Waktu Traversal Dalam Stasiun 
 
 Waktu Traversal Dalam Stasiun memberikan tingkat detail tambahan pada petunjuk arah dalam stasiun, memberi pengguna perkiraan waktu yang diperlukan untuk menavigasi stasiun, sehingga menghasilkan arah perjalanan yang lebih baik dan waktu perjalanan. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`traversal_time`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Koneksi Jalur](#koneksi jalur) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan perkiraan waktu perjalanan (dalam detik) yang diperlukan untuk menavigasi setiap jalur. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | traversal_time | 
 |------------|----------------| 
 | MainSt-001 | 3 | 
 | MainSt-002 | 20 | 
 | MainSt-003 | 2 | 
 | MainSt-004 | 2 | 
 | MainSt-005 | 4 | 
 | MainSt-006 | 25 | 
 | MainSt-007 | 4 | 
 | MainSt-008 | 25 | 
 | MainSt-009 | 2 | 
 | MainSt-010 | 2 | 
 
 
## Rambu Jalur 
 
 Rambu Jalur dapat menjembatani informasi yang ditampilkan dalam perencana perjalanan dengan rambu di dunia nyata. Jika hal ini ditampilkan dalam feed, perencana perjalanan dapat memberikan petunjuk seperti ’ikuti rambu ke’. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`signposted_as`, `reversed_signposted_as`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Koneksi Jalur](#koneksi jalur) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menentukan informasi navigasi yang terkait dengan pathways yang telah ditentukan sebelumnya, yang mencerminkan teks yang ditampilkan pada rambu fisik stasiun. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | signposted_as | reversed_signposted_as | 
 |------------|------------------|------------------------| 
 | MainSt-001 | untuk melobi | Keluar | 
 | MainSt-002 | | | 
 | MainSt-003 | Ke platform | Keluar | 
 | MainSt-004 | | | 
 | MainSt-005 | Kereta api arah barat | Keluar | 
 | MainSt-006 | | | 
 | MainSt-007 | Kereta api arah timur | Keluar | 
 | MainSt-008 | | | 
 | MainSt-009 | Kereta api arah barat | Ke Lobi | 
 | MainSt-010 | Kereta api arah timur | Ke Lobi | 
 
 

