# 輔助功能 
 輔助功能旨在為殘障人士提供存取服務所需的資訊。 
 
## 停止輪椅通道 
 
 停止輪椅通道 允許指示是否可以從指定位置搭乘輪椅。為了為使用輪椅的乘客提供服務，指定可以使用輪椅登機與指定t使用輪椅同樣重要。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 - [位置類型](../base_add-ons/#location-types) 定義輔助功能資訊時車站位置，例如入口/出口或登機區。 

???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示使用 `wheelchair_boarding=1` 在車站 `TAS001` 可以使用輪椅登機。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

|stop_id |stop_name|stop_lat|stop_lon|location_type|wheelchair_boarding| 
 |---------|------------|------------|------------|--------------|---------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 |-73.975224 | 1 | 
 
 
## 行程輪椅通道 
 
 行程輪椅通道可以指示vehicle是否可以容納使用輪椅的乘客。為了為使用輪椅的乘客提供服務，指定vehicle可以容納使用輪椅的乘客與指定vehiclet同樣重要。停靠站和行程都必須可供輪椅通行，以便乘客能夠在給定的停靠站搭乘行程。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible`| 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例顯示，行程` AWE1中使用的vehicle配備有至少可容納一輛輪椅的設施，而行程` AWE2中使用的vehicle則不能。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

|route_id |service_id |trip_id |wheelchair_accessible| 
 |----------|------------|---------|-----------------------| 
 | RA |我們| AWE1 | 1 | 
 | RA |我們| AWE2 | 2 | 
 
 
## 文字轉語音 
 
 文字轉語音允許提供將文字轉換為音訊所需的輸入，確保使用輔助技術朗讀文字的乘客獲得正確的車站名稱使用轉乘服務時。 

|包含文件 |包含的字段 | 
 |------------------------------------------------|--------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **先決條件**： 
 
 - [基本功能](../base) 
 
 ???注意`樣本資料` 
 
<p style="font-size:16px"> 
 以下範例提供了車站名稱的可讀版本，允許文字轉語音工具大聲朗讀該名稱。 
</p> 
!!!筆記 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

|stop_id |stop_name|stop_lat|stop_lon| tts_stop_name | tts_stop_name | 
 |---------|------------|-------------|--------------|--------------------------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 |-73.587079第五大道和53街| 
 

