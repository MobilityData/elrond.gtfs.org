# 无障碍 
 无障碍功能旨在向残障人士提供他们使用服务所需的信息。
 
## 站点轮椅无障碍 
 
 站点轮椅无障碍可以指示是否可以使用轮椅从指定位置登车。为了服务使用轮椅的乘客，指定可以使用轮椅与指定t轮椅同样重要。
 
 | 包含的文件 | 包含的字段 |
 |----------------------------------|----------------------------------|
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **先决条件**：
 
 - [基本功能](../base) 
 - [位置类型](../base_add-ons/#location-types) 定义车站位置（如入口/出口或登车区）的无障碍信息时。
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例显示，使用“wheelchair_boarding=1”，可以在站点“TAS001”搭乘轮椅。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|-----------|------------|-----------|---------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 | | 1 | 
 
 
## 行程轮椅无障碍功能 
 
 行程轮椅无障碍功能可以指示vehicle是否可容纳使用轮椅的乘客。为了服务使用轮椅的乘客，指定vehicle可容纳使用轮椅的乘客与指定vehiclet同样重要。站点和行程都必须适合轮椅通行，乘客才能在给定站点进入行程。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible `| 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例显示，行程“ AWE1 ”中使用的vehicle可容纳至少一辆轮椅，而行程“ AWE2 ”中使用的vehicle则不能。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | wheelchair_accessible | 
 |----------|------------|---------|-----------| 
 | RA | WE | AWE1 | 1 | 
 | RA | WE | AWE2 | 2 | 
 
 
## 文本转语音 
 
 文本转语音允许提供将文本转换为音频所需的输入，确保使用辅助技术大声朗读文本的乘客在使用交通服务时获得正确的站点名称。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **先决条件**：
 
 - [基本特征](../base) 
 
 ??? 注意“样本数据”
 
<p style="font-size:16px"> 
 以下示例提供了站点名称的可读版本，允许文本转语音工具大声读出该名称。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|------------|-------------|------------|-----------------------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 | 第五大道和 53 街 | 
 

