# 基礎
 以下功能提供了GTFS代表傳輸服務所需的最基本和最重要的元素。 GTFS由routes組成，每條路線都有相關的行程。這些行程在特定時間會造訪一個或多個stops。行程僅包含一天中的時間信息，其運行日期由日曆決定。 
 所有這些功能必須一起實作才能實現有效的GTFS提要。 
 
## 機構 
 
 機構包含負責公交服務的機構的基本信息，例如其名稱、網站URL以及服務運營的語言和時區。這允許將特定服務與其相應的agency相匹配。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id、`agency_name、`agency_url、`agency_timezone、`agency_lang、`agency_phone`、`agency_fare_url、`agency_email| 
 
 **先決條件**： 
 
 - 所有其他基本功能 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 

|agency_id |agency_name|agency_url|agency_timezone|agency_lang|agency_phone| agency_fare_url |agency_email| 
 |------------|-------------|-------------------------------|---------------------|-------------|---------------|------------------------------------------------------------|------------------------| 
 | TB |公車| https://www.transitbus.org |America/Los_Angeles| CN | (777) 555-7777 | https://www.transitbus.org/fares | contact@transitbus.org | 
 
 
 
## 停靠站 
 
 停靠站代表用於識別公車服務接送乘客地點的基本要素。這可能是地鐵站或公車站。除其他屬性外，每個站點還具有用於在地圖上精確定位其位置的地理座標，以及與該機構面向乘客的材料相符的名稱。使用停止時間將停靠點與行程關聯。 
 使用GTFS，也可以使用 [Pathways](/getting_started/features/pathways) 描述較大車站的內部，例如火車站或公車站。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`、`stop_code、`stop_name、`stop_desc、`stop_lat、`stop_lon、`stop_url、`stop_timezone、`platform_code| 
 
 **先決條件**： 
 
 - 所有其他基本功能 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 

</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

|stop_id |stop_code|stop_desc|stop_name|stop_lat|stop_lon|stop_url|stop_timezone|platform_code| 
 |---------|------------|-----------------------------------------------|------------------------|------------|------------|--------------------------------------------------------|---------------|---------------| 
 | TAS001 | TAS001 | 5 大道和 53 街西南角 | 5 Av/53 St | 45.503568 |-73.587079 |-73.587079 https://www.transitbus.org/stops/TAS001 | | | 
 
 
## 路線 
 
 路線是同一品牌下的一組行程，作為單一服務向乘客顯示。除其他屬性外，每條路線都有一個與該機構面向乘客的材料相符的名稱以及所代表的服務類型（例如公共汽車、地鐵或地鐵、渡輪等）。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`、`agency_id、`route_desc、`route_type、`route_url、`route_sort_order、`route_short_name、`route_long_name| 
 
 **先決條件**： 
 
 - 所有其他基本功能 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例定義了一條總線路線 (`route_type=3`)。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

|route_id |agency_id |route_short_name|route_long_name|route_desc|route_type|route_url|route_sort_order| 
 |----------|------------|--------------------|--------------------|--------------------------------------------------------|------------------------|---------------------------------------|--------------------| 
 | RA | TB | 17 | 17使命 - 市中心 | `A`路線從下使命區前往市中心。 | 3 | routes | 12 | 12## 服務日期 
 
 服務日期表示服務運作的日期範圍，以及創造服務豁免，例如假期和特定日期的其他特殊服務。 
 它的工作原理是在` .txt `中定義開始date和結束date，然後為其運行的一周中的每一天定義一個標記。如果在此期間發生單日計劃更改，則可以使用``calendar_dates.txt``檔案覆蓋這些天的計劃。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id、`monday`、`tuesday`、`wednesday`、`thursday`、`friday`、`saturday`、`sunday`、 `start_date`、`end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id、`date、`exception_type| 
 
 **先決條件**： 
 
 - 所有其他基本功能 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例定義了 2024 年 7 月的兩種服務（工作日和週末），其中包括 7 月 4 日的特殊假期服務，作為週末服務運行。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 

|service_id |monday|tuesday|wednesday|thursday|friday|saturday|sunday|start_date|end_date| 
 |------------|--------|---------|------------|----------|--------|----------|--------|------------|----------| 
 |我們| 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 |西數 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 

|service_id |date|exception_type| 
 |------------|----------|----------------| 
 |西數 | 20240704 | 2 | 
 |我們| 20240704 | 1 | 
 
## 行程 
 
 行程匯集了路線和服務日期，以創建乘客可以採取的旅程。使用停止時間將行程與停止相關聯。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`、`service_id、 `trip_id`、`trip_short_name、 `direction_id`、`block_id| 
 
 **先決條件**： 
 
 - 所有其他基本功能 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例定義了 RA 路線雙向運行的兩個行程。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

|route_id |service_id |trip_id |trip_short_name|direction_id |block_id | 
 |----------|------------|---------|-----------------|--------------|----------| 
 | RA |我們| AWE1 | 3885 | 3885 0 | 1 | 
 | RA |我們| AWE2 | 3887| 1 | 2 | 
 
## 停靠時間 
 
 停靠時間用於代表每次行程的各個停靠arrival和departure時間，讓乘客可以準確了解公共汽車、火車或渡輪到達和離開特定地點的時間。 `stop_times.txt`檔案通常是GTFS feed 中最大的檔案。 
 某些服務以固定頻率運行（例如，地鐵線路每 5 分鐘一班），而不是有特定的arrival和departure時間。這可以使用 [基於頻率的服務](../base_add-ons/#Frequency-based-service) 進行建模，並且可以與`stop_times.txt`結合建模。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`、`arrival_time、 `departure_time`、 `stop_id`、 `stop_sequence`、`pickup_type、`drop_off_type、`timepoint| 
 
 **先決條件**： 
 
 - 所有其他基本功能 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例定義了 5 個stops的行程時間表。 
</p> 
！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

|trip_id |arrival_time|departure_time|stop_id |stop_sequence|pickup_type|drop_off_type|timepoint| 
 |---------|--------------|----------------|---------|---------------|-------------|----------------|------------| 
 | AWE1 | 6:10:00 | 6:10:00 6:10:00 | 6:10:00 TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 6:14:00 | 6:14:00 TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 | 6:23:00 6:23:00 | 6:23:00 TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 | 6:25:00 6:25:00 | 6:25:00 TAS005 | 5 | 0 | 0 | 1 | 
 

