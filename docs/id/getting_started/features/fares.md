# Tarif 
 GTFS memungkinkan untuk secara tepat memodelkan berbagai macam struktur tarif yang digunakan oleh berbagai agen transportasi umum di seluruh dunia, seperti tarif berdasarkan zona, jarak perjalanan, atau waktu. Tarif GTFS memberi tahu penumpang tentang price yang berlaku untuk perjalanan mereka dan media yang dapat mereka gunakan untuk membayar. 
 
## Produk Tarif 
 
 Produk Tarif mencantumkan jenis tiket atau tarif (yaitu tarif sekali jalan, tiket bulanan, biaya transfer, dll.) yang ditawarkan oleh agency transit untuk mengakses layanan. Produk Tarif berfungsi sebagai landasan untuk memodelkan struktur tarif suatu lembaga, dan produk tersebut terhubung dengan layanan transportasi umum melalui mekanisme yang diuraikan dalam `fare_leg_rules.txt`. Keterkaitan Produk Tarif dengan berbagai kondisi perjalanan, seperti routes, area, dan waktu, menentukan biaya tarif untuk masing-masing segmen perjalanan dan transfers. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menyajikan produk tarif sederhana (sekali perjalanan $2,75 USD). 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | 
 |------------------|--------------------|---|---| 
 | perjalanan_tunggal | Tarif Sekali Perjalanan | 2.75 | USD | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id | 
 |------------------| 
 | perjalanan_tunggal | 
 
 
## Media Tarif 
 
 Media Tarif mendefinisikan media yang didukung yang dapat digunakan untuk menyimpan dan/atau memvalidasi produk tarif. Hal ini mengacu pada wadah fisik atau virtual seperti tiket kertas, kartu transit yang dapat diisi ulang, atau bahkan pembayaran nirsentuh dengan kartu kredit atau ponsel pintar. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan cuplikan Fare Media yang berbeda di San Francisco Bay Area. `Clipper` digambarkan sebagai kartu transit fisik dengan `fare_media_type=2`. `SFMTA Munimobile` digambarkan sebagai aplikasi seluler dengan `fare_media_type=2`. `Uang tunai` yang diberikan langsung kepada pengemudi tanpa tiket adalah `fare_media_type=0`. 
</p> 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>tarif_media.txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------------------|-----------------| 
 | gunting | Pemotong | 2 | 
 | mobil muni | SFMTA MuniMobile | 4 | 
 | uang tunai | Tunai | 0 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|--------------------|---|---|---| 
 | perjalanan_tunggal | Tarif Sekali Perjalanan | 2.75 | USD | mobil muni | 
 
 
 
 
## Tarif Berbasis Rute 
 
 Tarif Berbasis Rute digunakan untuk menetapkan tarif berbeda untuk kelompok routes tertentu, seperti tarif khusus untuk layanan ekspres atau membedakan tarif antar Bus Rapid Layanan transit versus layanan bus tradisional. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../basis) 
 - [Fitur Produk Tarif](#produk-tarif) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan sistem yang mengkategorikan routes ke dalam kategori ekspres dan lokal, masing-masing terkait dengan produk tarif yang berbeda.</p> 
 
<p style="font-size:16px"> **Menggunakan `jaringan.txt` + `route_networks.txt`**</p> 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#networkstxt"><b>jaringan.txt</b></a><br> 
</p> 
 
 | network_id | network_name | 
 |------------|-----------------| 
 | mengungkapkan | Ekspres | 
 | lokal | Lokal | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#route_networkstxt"><b>rute_jaringan.txt</b></a><br> 
</p> 
 
 | network_id | route_id | 
 |------------|-----------| 
 | mengungkapkan | ekspres_a | 
 | mengungkapkan | ekspres_b | 
 | lokal | lokal_1 | 
 | lokal | lokal_2 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | mengungkapkan | ekspres_single_ride | 
 | lokal | perjalanan_tunggal_lokal | 
 
<p style="font-size:16px"> **ATAU menggunakan `routes.networks_id`**</p> 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | ekspres_a | mengungkapkan | 
 | ekspres_b | mengungkapkan | 
 | lokal_1 | lokal | 
 | lokal_2 | lokal | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | mengungkapkan | ekspres_single_ride | 
 | lokal | perjalanan_tunggal_lokal | 
 
 
## Tarif Berbasis Waktu 
 
 Tarif Berbasis Waktu digunakan untuk menetapkan tarif pada waktu tertentu dalam sehari atau hari dalam seminggu, misalnya tarif pada jam sibuk dan di luar jam sibuk dan/atau tarif akhir pekan. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[jangka waktu.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Fitur Produk Tarif](../fares/#fare-products) 
 
 ?? ? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menyajikan sistem di mana jam sibuk adalah dari pukul 8:00 hingga 10:00, dan jam sisanya di luar jam sibuk.</p> 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#timeframestxt"><b>jangka waktu.txt</b></a><br> 
</p> 
 
 | timeframe_group_id | start_time | end_time | service_id | 
 |-----|------------|----------|------------| 
 | puncak | 08:00:00 | 10:00:00 | sepanjang_hari | 
 | reguler | 0:00:00 | 08:00:00 | sepanjang_hari | 
 | reguler | 10:00:00 | 24:00:00 | sepanjang_hari | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id | 
 |-------------------------|---------------------| 
 | puncak | puncak_single_ride | 
 | reguler | perjalanan_tunggal_reguler | 
 
 
## Tarif Berbasis Zona 
 
 Tarif Berbasis Zona digunakan untuk mewakili sistem berbasis zona di mana tarif tertentu berlaku ketika melakukan perjalanan dari satu zona tertentu ke zona lainnya. Sebuah zona ditentukan oleh sekelompok stops. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id`, `area_name`| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Fitur Produk Tarif](../fares/#fare-products) 
 
 ?? ? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut menunjukkan tarif dari Zona A ke Zona B.</p> 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id | area_name | 
 |---------|-----------| 
 | zona_a | Zona A | 
 | zona_b | Zona B | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id | stop_id | 
 |---------|---------| 
 | zona_a | berhenti_a | 
 | zona_a | berhenti_b | 
 | zona_b | berhenti_c | 
 | zona_b | berhenti_d | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id | 
 |--------------|------------|-----------------| 
 | zona_a | zona_b | zona_a_b_tunggal | 
 
## Transfer Tarif 
 
 Transfer Tarif digunakan untuk menentukan peraturan yang berlaku ketika melakukan transfer antar jalur (atau segmen perjalanan individu). Hal ini memungkinkan untuk memodelkan total biaya perjalanan multi-perjalanan, dengan memperhitungkan kebijakan transfer khusus, seperti transfers gratis untuk batas waktu tertentu, atau menerapkan diskon tarif berdasarkan perjalanan yang sudah ditempuh. 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id`, `transfer_count`, `duration_limit`, `duration_limit_type`, `fare_transfer_type`, `fare_product_id`| 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 - [Fitur Produk Tarif](../fares/#fare-products) 
 
 ?? ? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mengilustrasikan bahwa dalam jangka waktu 2 jam, transfers gratis tanpa batas diperbolehkan antara Leg A dalam sistem.</p> 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |---------------| 
 | sebuah | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|----------------|---------------------|--------------------|-----------------| 
 | sebuah | sebuah |-1 | 7200 | 1 | 0 | transfer_gratis | 
 
 
## Tarif v1 
 
 Tarif v1 adalah alternatif lama terhadap fitur Tarif lainnya yang dijelaskan di atas. Hal ini memungkinkan untuk memodelkan informasi tarif dasar seperti harga tarif, transfers metode pembayaran, dan tarif berdasarkan zona menggunakan file `fare_rules.txt dan `fare_attributes.txt. Meskipun lebih sederhana untuk diproduksi, fitur ini kurang mumpuni atau memodelkan struktur tarif yang lebih kompleks dan mungkin tidak lagi digunakan karena dukungan yang memadai terhadap fitur Tarif lainnya (yang merupakan bagian dari apa yang disebut Tarif v2). 
 
 | File disertakan | Bidang disertakan | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **Prasyarat**: 
 
 - [Fitur dasar](../base) 
 
 ??? catatan "Contoh Data" 
 
<p style="font-size:16px"> 
 Contoh berikut mengilustrasikan bahwa perjalanan di jaringan dikenakan biaya $3,20 CAD menggunakan kartu prabayar, sehingga memungkinkan transfers gratis dalam jangka waktu 2 jam.</p> 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 | fare_id | price | currency_type | payment_method | transfers | transfer_duration | 
 |-------------------|-------|---------------|----------------|-----------|-------------------| 
 | tarif_kartu prabayar | 3.2 | CAD | 1 | | 7200 | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 | fare_id | route_id | origin_id | destination_id | 
 |-------------------|----------|-----------------|-----------------| 
 | tarif_kartu prabayar | baris1 | stasiun_kereta bawah tanah | stasiun_kereta bawah tanah | 
 | tarif_kartu prabayar | baris2 | stasiun_kereta bawah tanah | stasiun_kereta bawah tanah | 
 
!!! catatan "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | SEBUAH | berhentiA | 43.670049 |-79.385389 | stasiun_kereta bawah tanah | 
 | B | berhentiB | 43.671049 |-79.386789 | stasiun_kereta bawah tanah | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | SEBUAH | berhentiA | 43.670049 |-79.385389 | stasiun_kereta bawah tanah | 
 | B | berhentiB | 43.671049 |-79.386789 | stasiun_kereta bawah tanah | 
 
 

