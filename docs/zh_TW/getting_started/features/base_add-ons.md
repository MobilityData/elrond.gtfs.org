# Base 附加元件 
 這些功能擴展了 Base 中所述的功能，可增強GTFS資料集的全面性，為乘客提供更好的體驗，或促進機構、資料供應商和資料重用者之間的協作。這些增強可能需要在 Base 中描述的文件中引入新字段，或建立新文件。 
 
## Feed 資訊 
 
 Feed 資訊傳達有關 Feed 的重要訊息，例如其有效性（開始和結束date）、發布組織以及有關GTFS資料集和資料發布實踐查詢的聯絡資訊。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`、`feed_publisher_url`、`feed_lang`、`default_lang`、`feed_start_date`、` default_lang `、`feed_end_date`、`feed_version`、`feed_contact_email`、`feed_contact_url` | 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 

| feed_publisher_name | feed_publisher_url | feed_lang |default_lang| feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |------------------------------------------------|----------------------|------------|--------------|------------------|---------------|--------------|--------------------|------------------------------------------| 
 |大區域交通| https://www.gra1.org | zh | zh | 20240101 | 20241231 | 3.1|支持@gra1.org | https://www.gra1.org/support | 
 
## 形狀 
 可以定義形狀並將其與行程關聯起來，使行程規劃應用程式能夠在地圖上顯示行程並告知乘客乘坐公車vehicle需要行駛的距離。 `shape_dist_traveled`欄位用於以程式設計方式決定在向騎手顯示地圖時要繪製多少shape。 
 定義形狀時，要在細節程度（例如遵循道路的精確曲率）和僅有效傳達必要資訊之間取得平衡。 
 
 |所包含的文件 |所包含的欄位 | 
 |------------------------------------------------|--------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`、`shape_pt_lat、`shape_pt_lon、`shape_pt_sequence、`shape_dist_traveled| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled `| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了 TriMet GTFS來源中shape的一部分（<a     href="https://developer.trimet.org/GTFS.shtml">在此處</a>下載）。<br><br> 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 

|shape_id |shape_pt_lat |shape_pt_lon |shape_pt_sequence| shape_dist_traveled | 形狀_距離_旅行
 |---------|-------------|-------------|------------------|-------------------| 
 | 558674 | 45.47623 | 45.47623-122.721885 |-122.721885 1 | 0.0 | 0.0 
 | 558674 | 45.476235 | 45.476235-122.72236 |-122.72236 2 | 121.9 | 121.9 
 | 558674 | 45.476237 | 45.476237-122.722523 |-122.722523 3 | 163.7 | 163.7 
 | 558674 | 45.476242 |-122.723024 |-122.723024 4 | 292.2 | 292.2 
 | 558674 | 45.476244 |-122.72316 |-122.72316 5 | 327.1 | 327.1 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 

|trip_id |shape_id| 
 |--------|--------| 
 |13302375|558674 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 

|trip_id |stop_sequence| shape_dist_traveled| 形狀_距離_旅行
 |--------|-------------|--------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## 路線顏色 
 
 使用路線顏色可以準確地描繪和傳達機構設計指南分配給特定routes的配色方案。這使用戶能夠透過官方顏色輕鬆識別公車服務。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color,`route_text_color| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示路線`RA`使用十六進位顏色代碼`D95700`為橘色，且該文字應使用十六進位顏色代碼`0`呈現為黑色。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

|route_id |agency_id |route_short_name|route_long_name|route_type|route_color|route_text_color| 
 |----------|------------|--------------------|--------------------|------------|-------------|--------------------| 
 | RA |機構001 | 17 | 17使命 - 市中心 | 3 | D95700 | 0 | 
 
## 允許自行車 
 
 允許自行車指示服務特定行程的車輛是否能夠容納自行車，幫助用戶規劃和訪問使他們能夠進行多式聯運旅行的服務。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed ` | 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例指定行程` AWE1 `中使用的vehicle可容納至少一輛自行車（` bikes_allowed =1`），而行程` AWE2 `中使用的vehicle則不能（` bikes_allowed=2`）。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

|route_id |service_id |trip_id |bikes_allowed| 
 |----------|------------|---------|---------------| 
 | RA |我們| AWE1 | 1 | 
 | RA |我們| AWE2 | 2 | 
 
## Headsigns 
 
 Headsigns 允許傳達車輛使用的標牌，指示行程目的地，使用戶更容易識別正確的交通服務。此功能支援沿特定路線更改車頭標誌。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 在下面的範例中，第一個表指定了行程`AWE1`和`AWE2`要使用的車頭標誌，第二個表指示`AWE1`的車頭標誌將在停靠`TAS004`後修改，覆蓋該車頭標誌在 `trips.txt中指定。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

|route_id |service_id |trip_id |trip_headsign| 
 |----------|------------|---------|---------------| 
 | RA |我們| AWE1 |市中心 | 
 | RA |我們| AWE2 |使命 | 


!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

|trip_id |arrival_time|departure_time|stop_id |stop_sequence|stop_headsign| 
 |---------|--------------|----------------|---------|---------------|------------------------| 
 | AWE1 | 6:10:00 | 6:10:00 6:10:00 | 6:10:00 TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 6:14:00 | 6:14:00 TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 6:23:00 | 6:23:00 TAS004 | 4 |市中心 - 主廣場 | 
 | AWE1 | 6:25:00 | 6:25:00 6:25:00 | 6:25:00 TAS005 | 5 |市中心 - 主廣場 | 
 
## 位置類型 
 
 位置類型用於對公車站內的關鍵區域（例如出口/入口、節點或登機區）及其關係進行分類。位置類型是使用路徑對公車站進行建模的基礎。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例在`stops.txt`中顯示了公車站內的多個位置：代表主位置的父站及其子位置，例如月台、入口/出口和通用節點。 
</p> 
！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

|stop_id |stop_name|location_type|parent_station| 
 |--------------|-------------------------------------------------------|---------------|----------------| 
 |站_A102 |主街站 | 1 | | 
 | A102_B01 |主街站 - 北月台 | 0 |站_A102 | 
 | A102_B02 |大街站 - 南月台 | 0 |站_A102 | 
 | A102_E01 |主街站 - 入口/出口 | 2 |站_A102 | 
 | A102_S01 |主街車站 - 入口樓梯頂部 | 3 |站_A102 | 
 | A102_S02 |主街車站 - 入口樓梯底部 | 3 |站_A102 | 
 | A102_S03 |主街車站 - 北月台樓梯頂 | 3 |站_A102 | 
 | A102_S04 |主街站 - 北月台樓梯底部 | 3 |站_A102 | 
 | A102_S05 |主街站 - 南月台樓梯頂部 | 3 |站_A102 | 
 | A102_S06 |主街站 - 南月台樓梯底部 | 3 |站_A102 | 
 | A102_F01 |主街車站 - 檢票口付費側 | 3 |站_A102 | 
 | A102_F02 | Main Street 車站 - 檢票口未付費一側 | 3 |站_A102 | 
 
## 基於頻率的服務
 
 基於頻率的服務可用於對按固定頻率運營的服務進行建模，例如每10 分鐘一班的公交車或在指定時間間隔內每2 分鐘一班的地鐵服務。 
 在對基於頻率的服務進行建模時， “`stop_times.txt`”包含stops之間的相對時間，以確定向乘客顯示的時間。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| `trip_id`、 `start_time`、`end_time、 `headway_secs`、 `exact_times` | 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了兩個不同的行程：每 30 分鐘運行一次的行程 `AWE1(`headway_secs=1800`) 和每 15 分鐘運行一次的行程 `AWE2(`headway_secs=900`)。 
<p style="font-size:16px"> 
 ``exact_times``欄位指示時間表是否遵循`start_time`欄位中輸​​入的精確開始時間： 
 - 行程`AWE1`從早上 6:10 到中午 12:00 每 30 分鐘一班。 
 - 行程`AW2`的出發時間為上午 6:00、上午 6:15、上午 6:30，依此類推。 
</p> 
！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 

|trip_id |start_time|end_time| headway_secs |exact_times| 
 ---------|------------|----------|----------------|-------------| 
 AWE1 | 6:10:00 | 6:10:00 12:00:00 | 12:00:00 1800 | 1800 0 | 
 AWE2 | 6:00:00 | 6:00:00 19:50:00 | 19:50:00 900 | 900 1 | 
 
## 轉乘 
 
 轉乘提供有關不同旅行段（或航段）之間轉乘的詳細信息，使旅行規劃者能夠確定包含transfers的旅程的可行性。指定transfers並不意味著乘客t轉乘其他地方，它只是表明某些transfers是否不可能或require最短轉乘時間。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, ` from_trip_id `, ``from_trip_id, ``p_id `to_trip_id_ `` `、`transfer_type、`min_transfer_time| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了三種不同的transfers：一種在stops之間，需要最少換乘時間 5 分鐘；一種在兩條routes之間的定時換乘點；一種在同一vehicle的兩次行程之間進行座位內換乘。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 

|from_stop_id |to_stop_id |from_route_id |to_route_id |from_trip_id |to_trip_id |transfer_type|min_transfer_time| 
 |--------------|------------|----------------|--- ----------|--------------|------------|----------------|--------------------| 
 | s6 | s7 | | | | | 2 | 300 | 300 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## 翻譯 
 
 翻譯允許以多種語言提供車站名稱等服務信息，使旅行規劃者能夠根據用戶的語言和位置設置以特定語言顯示信息。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`語言`,`翻譯`,`record_id`, `record_sub_id`,`field_value` | 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了為`routes.txt`中使用的兩個欄位提供的法文和西班牙文翻譯：`route_long_name`和`route_desc`。 
</p> 
！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 

|table_name|field_name|語言 |翻譯 |record_id |record_sub_id |field_value| 
 |------------|-----------------|----------|-------------------------------------------------------|------------|--------------|----------| 
 |routes|route_long_name|英語 |使命 - 中心 | RA | | | 
 |routes|route_long_name|法國 |使命 - 中心維爾 | RA | | | 
 |routes|route_desc|英語 | La ruta "A" viaja desde Lower Mission hasta el centro | 路線RA | | | 
 |routes|route_desc|法國 |路線“A”位於市中心的下使命區。 | RA | | | 
 
## 歸屬 
 
 歸屬可以分享更多有關參與資料集創建的組織（生產者、營運商和/或當局等）的詳細資訊。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id、`agency_id、 `route_id`、 ` `trip_id`、` is_id` 、`organization_name、`is_producer`、`is_operator`、`is_authority`、`attribution_url`、`attribution_email`、`attribution_phone` | 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 

|attribution_id |agency_id |route_id |trip_id |organization_name|is_producer|is_operator|is_authority|attribution_url |attribution_email|attribution_phone| 
 |----------------|------------|----------|----------|--------------------------|-------------|----- -------|--------------|-----------------------------------|-------------------------|--------------------------------| 
 | OP01 | TB | | |公車| | 1 | | https://www.transitbus.org/fares | contact@transitbus.org | (777) 555-7777 | 
 | au01 |格拉 | | |大區域交通| 1 | | 1 | https://www.gra1.org |聯絡@gra1.org | (555) 555-5555 | 
 | OP02 | | rtd023 | rtd023 | |巴士公司A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | OP03 | | rtd025 | rtd025 |巴士公司B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

