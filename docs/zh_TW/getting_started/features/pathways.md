# Pathways 
 Pathways 功能可以模擬大型公車站，引導乘客從車站入口到達他們上vehicle或下車的位置。其中一些功能可以傳達路徑的物理特徵和估計的導航時間，以及車站中使用的現實世界尋路系統。 
 
## 路徑連接 
 
 在基礎層面，路徑提供了連接站點內位置類型中定義的關鍵區域的基本功能。這些連接形成pathways，使用戶能夠獲得精確的方向（例如從入口到登機區），這在導航大型且複雜的公車站時特別有用。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`pathway_id、`from_stop_id、`to_stop_id、`pathway_mode、`is_bidirectional | 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [位置類型](../base_add-ons/#location-types) 
 
 ？注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例定義了預先建立的位置（定義為stops）之間的多個連接（也稱為pathways ）：走道 (` pathway_mode=1)、樓梯 (`pathway_mode=2) 和檢票口( `pathway_mode=6）。也指定了雙向性。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 

|pathway_id |from_stop_id |to_stop_id |pathway_mode|is_bidirectional的| 
 |------------|--------------|------------|----------------|------------------| 
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
 
 
## 通道詳細資訊 
 
 可以添加有關車站pathways物理特徵的更多詳細信息，包括長度、寬度和坡度（對於坡道）或樓梯數量（對於樓梯）。這有助於騎士預測他們需要行駛的道路的條件和可及性。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`max_slope`、`min_width`、`length`、`stair_count`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [通路連結](#pathway-connections) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例定義了預先建立的pathways的其他詳細信息，包括最小寬度、樓梯的步數以及人行道的長度和最大坡度。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 

|pathway_id |max_slope|min_width|長度|stair_count| 
 |------------|------------|------------|--------|-------------| 
 | MainSt-001 | 0 | 4.3 | 3.6 | | 
 | MainSt-002 | | 2.2 | 2.2 | 15 | 15 
 | MainSt-003 | 0.06 | 0.06 4 | 3.1| | 
 | MainSt-004 | | 0.9 | 0.9 2.9 | 2.9 | 
 | MainSt-005 | 0 | 3.5 | 3.5 5 | | 
 | MainSt-006 | | 2.2 | 2.2 | 18 | 
 | MainSt-007 | 0 | 3.5 | 3.5 5 | | 
 | MainSt-008 | | 2.2 | 2.2 | 18 | 
 | MainSt-009 | 0 | 6 | 2 | | 
 | MainSt-010 | 0 | 6 | 2 | | 
 
 
## 級別 
 
 級別可用於列出站點內的所有不同級別，為使用者提供站點的額外資訊層。此功能還可將電梯與通道連接功能結合使用。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[levels.txt](../../../documentation/schedule/reference/#levelstxt)|`level_id`, `level_index`, `level_name`| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`level_id`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [位置類型](../base_add-ons/#location-types) 
 
 ？注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了網站中的不同層級。然後將位置（定義為stops）指派到其對應的層級。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

|level_id |level_index|level_name| 
 |--------------------|-------------|------------| 
 | level_0_street | 0 |街上| 
 |級別_-1_大廳 |-1 |大堂| 
 | level_-2_platform |-2 |平台| 


！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 

|stop_id |level_id | 
 |--------------|----------| 
 |站_A102 | | 
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
 
 
## 站內遍歷時間 
 
 站內遍歷時間為站內方向提供了額外的詳細信息，為用戶提供導航車站所需的估計時間，從而獲得更好的行進方向和旅行時間。 

|包含的文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`traversal_time`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [通路連結](#pathway-connections) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示了導航每條路徑所需的估計行駛時間（以秒為單位）。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 

|pathway_id |traversal_time| 
 |------------------------|----------------| 
 | MainSt-001 | 3 | 
 | MainSt-002 | 20 | 20 
 | MainSt-003 | 2 | 
 | MainSt-004 | 2 | 
 | MainSt-005 | 4 | 
 | MainSt-006 | 25 | 25 
 | MainSt-007 | 4 | 
 | MainSt-008 | 25 | 25 
 | MainSt-009 | 2 | 
 | MainSt-010 | 2 | 
 
 
## 通道標誌 
 
 通道標誌可以將旅行計畫中顯示的資訊與現實世界的標誌連結起來。如果這在提要中得到體現，旅行計劃者可以提供諸如“按照標誌前往”之類的指示。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`signposted_as,`reversed_signposted_as| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [通路連結](#pathway-connections) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例指定了與預先建立的pathways相關的導航信息，反映了車站物理標誌上顯示的文本。 
</p> 
！筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 

|pathway_id |signposted_as|reversed_signposted_as| 
 |------------|------------------|-------------------------------------| 
 | MainSt-001 |到大廳 |退出 | 
 | MainSt-002 | | | 
 | MainSt-003 |前往平台 |退出 | 
 | MainSt-004 | | | 
 | MainSt-005 |西行列車 |退出 | 
 | MainSt-006 | | | 
 | MainSt-007 |東行列車 |退出 | 
 | MainSt-008 | | | 
 | MainSt-009 |西行列車 |前往大堂 | 
 | MainSt-010 |東行列車 |前往大堂 | 

 

