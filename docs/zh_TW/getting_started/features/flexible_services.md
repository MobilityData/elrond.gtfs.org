# 彈性服務 
 彈性服務，也稱為需求回應服務，是不遵循預定和/或固定服務的常見行為的服務。 
 
## 連續停靠點 
 
 連續停靠點用於可以在預定stops之間接送乘客的情況。 
 這可以在`routes.txt中指定，表明乘客可以在路線的每次行程中沿車輛行駛路徑的任何點上車或下車，也可以在`stop_times.txt`中指定特定路段的一條路線。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off ` | 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了表示連續停止的兩種方法。 
</p> 

<p style="font-size:16px"> 
 第一個範例顯示，在`RA`路線沿線的任何地點都允許上車和下車。 
</p> 

<p style="font-size:16px"> 
 第二個範例顯示，在行程“ AWE1 ”的第三個和第五個stops之間允許上車和下車，這是透過將“ continuous_pickup”和“continuous_drop_off”值分配給“stop_sequence= 3”和“stop_sequence= 4”來實現的。 
</p> 

</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

|route_id |route_short_name|route_type|continuous_pickup|continuous_drop_off| 
 |----------|------------------|------------|-------------------|---------------------| 
 | RA | 17 | 17 3 | 0 | 0 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

|trip_id |arrival_time|departure_time|stop_id |stop_sequence|continuous_pickup|continuous_drop_off| 
 |---------|--------------|----------------|--------|---------------|--------------------|---------------------| 
 | AWE1 | 6:10:00 | 6:10:00 6:10:00 | 6:10:00 TAS001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 6:14:00 | 6:14:00 TAS002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 6:23:00 | 6:23:00 TAS004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 6:25:00 | 6:25:00 TAS005 | 5 | | | 
 
## 預訂規則 
 
 預訂規則可用於使用戶能夠預訂需求回應服務的行程。這些規則概述了成功預訂的必要先決條件，並提供了用戶可以進行旅行預訂的聯絡資訊。此功能應與[偏差的預定義路線](#predefined-routes-with-deviation)、[基於區域的需求回應服務](#zone-based-demand-responsive-services)和[固定停靠點]結合使用需求回應服務](#fixed-stops-demand-responsive-services) 功能（如果此類服務require預訂）。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`、`booking_type`、`prior_notice_duration_min`、`prior_notice_duration_max`、`prior_notice_duration_min`、`prior_notice_duration_max`、`prior_notice_duration_minor、`prior_notice_duration_max`、`prior_notice_duration_Nadice_i_le_i_le_n_leh`、`pri `、`prior_notice_start_day`、`prior_notice_start_time`、`prior_notice_service_id`、`message、`pickup_message`、`drop_off_message`、`phone_number`、`info_url`、`booking_url` | 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了兩套不同的預訂規則，第一套適用於必須至少提前一天（下午 1 點之前）且不超過 14 天預訂的行程，第二套適用於可以預訂的行程至少在出行前45 分鐘且不超過5 小時。 

</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 

|預訂規則 ID |預訂類型 |事先通知持續時間分鐘 |事先通知持續時間最長 |先前通知最後一天 |先前通知最後時間 |事先通知開始日 |事先通知開始時間 |事先通知服務 ID |message|取件訊息 | drop_off_message | 刪除訊息電話號碼 |資訊網址 |預訂網址 | 
 |-----------------|--------------|--------------------------|----------------------------|-----------------------|------------------------|------------------------|------------------------|--------- ----------------|--------------------------------- -------------------------------------------------- -------------------------------------------------- ---------------|----------------|----------------- -|----------------|--------------------------------|--------------------------| 
 |路線_br_1818 | 2 | | | 1 | 13:00 | 13:00 14 | 14 9:00 | |如需叫車，請至少在出發前一個工作日下午 1 點前致電 123-111-2233。您最多可以提前 14 個工作天預訂行程。 | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 |路線_br_4545 | 1 | 45 | 45 300 | 300 | | | | |要叫車，請使用我們網站上的官方預訂系統，行程必須至少提前 45 分鐘預訂 | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## 帶有偏差的預定義路線
 
 帶有偏差的預定義路線可用於對靈活服務進行建模，其中車輛可以短暫偏離特定路線以接載在沿線特定區域內預訂行程的用戶路線。這結合使用了傳統stops（如常規預定服務）和使用``locations.geojson``的區域。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`、 `start_pickup_drop_off_window`、 `end_pickup_drop_off_window`、` `pickup_booking_rule_id`、 `drop_off_booking_rule_id` 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`類型`、`功能`、`功能：類型`、`功能：Id`、`功能:屬性`、`特徵:屬性:Stop_name`、`特徵:屬性:Stop_description`、`特徵:幾何`、`特徵:幾何:類型`、`特徵:幾何:座標` | 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [預訂規則](#booking-rules) 如果服務需要預訂 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了具有三個固定stops的行程，該行程還可以在固定stops之間定義的特定區域內的任何地方讓乘客下車。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

|trip_id |arrival_time|departure_time|stop_id |地點 ID |stop_sequence|start_pickup_drop_off_window窗口 | end_pickup_drop_off_window | 結束拾取落下視窗pickup_type|drop_off_type| shape_dist_traveled | 形狀_距離_旅行pickup_booking_rule_id | drop_off_booking_rule_id | drop_off_booking_rule_id | 
 |----------|--------------|----------------|--------|------------------------|---------------|------------------------------|------------------------ ----|-------------|----------------|-----------------------|------------------------------------|--------------------------| 
 | 4545_001 | 10:00:00 | 10:00:00 10:00:00 | 10:00:00 S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | | zone_S50122_to_S50123 | 2 | 10:00:00 | 10:00:00 10:06:00 | 10:06:00 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 10:06:00 | 10:06:00 S50123 | | 3 | | | | | 983 | 983 | | 
 | 4545_001 | | | | | zone_S50123_to_S50124 | 4 | 10:06:00 | 10:06:00 10:15:00 | 10:15:00 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 10:15:00 | 10:15:00 S50124 | | 5 | | | | | 2109 | 2109 | | 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "type": "FeatureCollection", 
 "features": [
 { 
 "id": "zone_S50122_to_S50123", 
 "type": "Feature", 
 "geometry": { 
 "type": "Polygon", 
# 簡化，這裡只顯示 3 個座標。 
`座標`：[
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
 -73.569794, 
 45.5098370 
] 
] 
] 
 }, 
 “屬性”: {} 
 }, 
 { 
 “id”: “zone_S50123_to_S50124”, 
 “類型”: “功能”, § § "geometry": { 
 "type": "Polygon", 
# 簡化，這裡只顯示 3 個座標。 
`座標`：[
 [
 [
 -73.561332, 
 45.5085599 
], 
 [
 -73.5701298, 
 45.5124057 
], 
 [§ § -73.§ § -73.§ 45.5105563 
] 
] 
] 
 }，
`屬性`：{} 
 } 
] 
 } 
 ~~~ 
 
## 基於區域的需求回應服務
 
 基於區域的需求回應服務用於建模服務，允許在特定區域內的任何位置為預訂行程的使用者提供接送服務。這些區域是使用``locations.geojson``定義的，因此require使用``stops.txt``或`stop_times`。arrival_time`和`stop_times.departure_time`。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`、 `start_pickup_drop_off_window`、 `end_pickup_drop_off_window`、` `pickup_booking_rule_id`、 `drop_off_booking_rule_id` 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`類型`、`功能`、`功能：類型`、`功能：Id`、`功能:屬性`、`特徵:屬性:Stop_name`、`特徵:屬性:Stop_description`、`特徵:幾何`、`特徵:幾何:類型`、`特徵:幾何:座標` | 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [預訂規則](#booking-rules) 如果服務需要預訂 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例展示了一項服務，該服務可以在上午 9 點到下午 6 點之間的特定區域內的任何地方接送預訂的乘客。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

|trip_id |地點 ID |stop_sequence|start_pickup_drop_off_window窗口 | end_pickup_drop_off_window | 結束拾取落下視窗pickup_type|drop_off_type|pickup_booking_rule_id | drop_off_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|----------------|--------------------------------|----------------------------------------|-------------|----------------------------|------------------------|--------------------------| 
 | 2708_001 | 2708_001區域_001 | 1 | 9:00:00 | 18:00:00 | 18:00:00 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | 2708_001區域_001 | 2 | 9:00:00 | 18:00:00 | 18:00:00 1 | 2 | br_3289 | br_3289 | 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "type": "FeatureCollection", 
 "features": [
 { 
 "id": "area_001", 
 "type": "Feature", 
 "geometry": { 
 "type": "Polygon", 
# 簡化，這裡只顯示 3 個座標。 
`座標`：[
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
 -73.63680 
 45.5081683 
] 
] 
] 
 }, 
`屬性`：{} 
 } 
] 
 } 
 ~~~ 
 
## 固定停靠點需求回應服務
固定停靠點需求回應服務用於對允許預訂行程的使用者在一組預定義stops內的任何位置上車和/或下車的服務進行建模。這些stops點群組是使用`location_groups.txt`和`location_group_stops.txt`定義的。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`、 `start_pickup_drop_off_window`、 `end_pickup_drop_off_window`、 `pickup_booking_rule_id`、 `drop_off_booking_rule_id`| 
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [預訂規則](#booking-rules) 如果服務需要預訂 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例展示了一項服務，該服務可以在上午 7 點至 10 點之間在 4 個不同的stops接送預訂的乘客。 

</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#location_groupstxt"><b>位置組.txt</b></a><br> 
</p> 

|位置組 ID |位置組名稱 | 
 |-------------------|---------------------------- ----| 
 | r27_stops | r27_stops |黃區路線 27stops| 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>location_group_stops.txt</b></a><br> 
</p> 

|位置組 ID |stop_id | 
 |--------------------|---------| 
 | r27_stops | r27_stops | syb029 | 
 | r27_stops | r27_stops | syb030 | 
 | r27_stops | r27_stops | syb031 | 
 | r27_stops | r27_stops | syb032 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

|trip_id |位置組 ID |stop_sequence|start_pickup_drop_off_window窗口 | end_pickup_drop_off_window | 結束拾取落下視窗pickup_type|drop_off_type|pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|--------------------|----------------|------------------------------------------|----------------------------|-------------|----------------|-----------------------|--------------------------| 
 | 2714_002 | r27_stops | r27_stops | 1 | 7:00:00 | 10:00:00 | 10:00:00 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_stops | r27_stops | 2 | 7:00:00 | 10:00:00 | 10:00:00 1 | 2 | br_5478 | br_5478 | 
 

