# 票價 
 GTFS可以對世界各地不同交通機構使用的各種票價結構進行精確建模，例如按區域、按行駛距離或按一天中的時間劃分的票價。 GTFS票價告知乘客適用於其行程的price以及他們可以用來支付的媒體。 
 
## 票價產品 
 
 票價產品列出了交通agency為取得服務而提供的車票或票價類型（即單程票價、月票、轉乘費等）。票價產品是對代理商的票價結構建模的基礎，它們透過`fare_leg_rules.txt`中概述的機制連結到公車服務。票價產品與各種旅行條件（例如routes、區域和時間）的關聯決定了各個旅行航段和transfers的票價成本。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`、`fare_product_name`、` amount `、` currency` 、` fare_product_name `、`amount`、`currency、`fare_media_id| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例展示了一個簡單的票價產品（單程 2.75 美元）。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 

|fare_product_idfare_product_name|amount|currency| 
 |------------------|--------------------|---|---| 
 |單人騎行 |單程票價 | 2.75 | 2.75美元 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

|fare_product_id 
 |------------------| 
 |單人騎行 | 
 
 
## 票價媒體 
 
 票價媒體定義了可用於保存和/或驗證票價產品的受支援媒體。這是指實體或虛擬容器，例如紙本機票、可充值交通卡，甚至信用卡或智慧型手機的非接觸式支付。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`、`fare_media_name`、`fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了舊金山灣區不同票價媒體的片段。 `Clipper`被描述為`fare_media_type=2`的實體交通卡。 `SFMTA Munimobile`被描述為具有`fare_media_type=2`的行動應用程式。無需門票直接給予司機的`現金`為`fare_media_type=0`。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>fare_media.txt</b></a><br> 
</p> 

|fare_media_idfare_media_name|fare_media_type| 
 |---------------|--------------------|-----------------| 
 |快船 |快船| 2 | 
 |市政汽車 | SFMTA 市政移動 | 4 | 
 |現金 |現金| 0 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 

|fare_product_idfare_product_name|amount|currency|fare_media_id 
 |------------------|--------------------|---|---|---| 
 |單人騎行 |單程票價 | 2.75 | 2.75美元 |市政汽車 | 
 
 
 
 
## 基於路線的票價 
 
 基於路線的票價用於為特定的routes組分配不同的票價，例如快速服務的特殊票價或快速公交之間的差別票價公車服務與傳統巴士服務。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id,`network_name| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [票價產品功能](#fare-products) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了一個系統，該系統將routes分為快速和本地類別，每個類別都與不同的票價產品相關聯。</p> 

<p style="font-size:16px"> **使用 `.txt+ `.txt**</p> 

!!!筆記 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#networkstxt"><b>網路.txt</b></a><br> 
</p> 

|network_id |network_name| 
 |------------|-----------------| 
 |快遞|快遞| 
 |本地|本地| 

!!!筆記 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#route_networkstxt"><b>路線網.txt</b></a><br> 
</p> 

|network_id |route_id | 
 |------------|------------| 
 |快遞|快遞_a | 
 |快遞|快遞_b | 
 |本地|本地_1 | 
 |本地|本地_2 | 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

|network_id |fare_product_id 
 |------------|-----------------| 
 |快遞|特快單程 | 
 |本地|本地單程 | 

<p style="font-size:16px"> **或使用 `routes**</p> 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

|route_id |network_id | 
 |------------|------------| 
 |快遞_a |快遞| 
 |快遞_b |快遞| 
 |本地_1 |本地| 
 |本地_2 |本地| 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

|network_id |fare_product_id 
 |------------|-----------------| 
 |快遞|特快單程 | 
 |本地 |本地單程 | 
 
 
## 基於時間的票價 
 
 基於時間的票價用於指定一天中或一周中特定時間的票價，例如高峰和非高峰票價和/或週末票價。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[時間範圍.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`、 `start_time`、`end_time`、`service_id`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [票價產品功能](../fares/#fare-products) 
 
 ?? ？注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例展示了一個系統，其中高峰時間為 8:00 到 10:00，其餘時間為非高峰時間。</p> 

！筆記 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#timeframestxt"><b>時間框架.txt</b></a><br> 
</p> 

|timeframe_group_id |start_time|end_time|service_id | 
 |--------------------|------------|----------|------------| 
 |高峰| 8:00:00 | 10:00:00 | 10:00:00全天 | 
 |常規| 0:00:00 | 0:00:00 08:00:00 | 08:00:00全天 | 
 |常規| 10:00:00 | 10:00:00 24:00:00 | 24:00:00全天 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

|from_timeframe_group_id |fare_product_id 
 |------------------------|---------------------| 
 |高峰|高峰單程 | 
 |常規|常規單程 | 
 
 
## 基於區域的票價 
 
 基於區域的票價用於表示基於區域的系統，其中從一個特定區域旅行到另一個區域時適用特定票價。區域由一組stops定義。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id,`area_name| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [票價產品功能](../fares/#fare-products) 
 
 ?? ？注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了從 A 區到 B 區的票價。</p> 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 

|area_id |area_name| 
 |---------|------------| 
 |區域_a | A區| 
 |區域_b | B區 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 

|area_id |stop_id | 
 |---------|---------| 
 |區域_a |停止_a | 
 |區域_a |停止_b | 
 |區域_b |停止_c | 
 |區域_b |停止_d | 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

|from_area_id |to_area_id |fare_product_id 
 |--------------|------------|-----------------| 
 |區域_a |區域_b |區域_a_b_單| 
 
## 票價轉乘 
 
 票價轉乘用於定義在航段（或各個旅行航段）之間轉乘時適用的規則。這允許對多段旅行旅程的總成本進行建模，考慮特殊的轉乘政策，例如特定時間限制內的免費transfers，或根據已旅行的航段應用票價折扣。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id、`to_leg_group_id、`transfer_count、`duration_limit、`"_id` 、_` transfer_count` 、`duration_limit_type、_`s_&amp;Fy_oo _`h、``fare_transfer_type( `, `fare_product_id`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [票價產品功能](../fares/#fare-products) 
 
 ?? ？注意`樣本資料` 
 
<p style="font-size:16px"> 
 下面的範例說明了在2小時視窗內，系統內A段之間允許無限制的自由transfers。</p> 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

|leg_group_id | 
 |---------------| 
 |一個 | 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 

|from_leg_group_id |to_leg_group_id |transfer_count|duration_limit|duration_limit_type|fare_transfer_type|fare_product_id 
 |--------------------|-----------------|--------- -------|----------------|------------------------|-------------------|-----------------| 
 |一個 |一個 |-1 | 7200 | 7200 1 | 0 |免費轉讓 | 
 
 
## 票價 v1 
 
 票價 v1 是上述其他票價功能的傳統替代方案。它允許使用` fare_rules.txt`和`fare_attributes.txt `檔案對基本票價資訊進行建模，例如票價定價、支付方式transfers和基於區域的票價。雖然生成更簡單，但它的能力較差或建模更複雜的票價結構，並且可能會因其他票價功能（屬於所謂的票價 v2 的一部分）的充分認可而被棄用。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` ` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例說明使用預付卡在網路上旅行的費用為 3.20CAD元，允許在 2 小時內免費transfers。</p> 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 

|fare_id |price|currency_type|payment_method|transfers|transfer_duration| 
 |--------------------|--------|----------------|---------------|---------|--------------------| 
 |預付卡票價 | 3.2 |CAD| 1 | | 7200 | 7200 

!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 

|fare_id |route_id |origin_id |destination_id | 
 |--------------------|----------|---------------- -|-----------------| 
 |預付卡票價 |第 1 行 |地鐵站 |地鐵站 | 
 |預付卡票價 |第 2 行 |地鐵站 |地鐵站 | 

！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

|stop_id |stop_name|stop_lat|stop_lon|zone_id | 
 |---------|------------|------------|------------|-----------------| 
 |一個 |停止A | 43.670049 | 43.670049-79.385389 |-79.385389地鐵站 | 
 |乙|停止B | 43.671049 | 43.671049-79.386789 |-79.386789地鐵站 | 


|stop_id |stop_name|stop_lat|stop_lon|zone_id | 
 |---------|------------|------------|------------|-----------------| 
 |一個 |停止A | 43.670049 | 43.670049-79.385389 |-79.385389地鐵站 | 
 |乙|停止B | 43.671049 | 43.671049-79.386789 |-79.386789地鐵站 | 

 

