# 路径 
 路径功能可模拟大型交通站，引导乘客从车站入口和出口到达他们登上或下车的地点。其中一些功能可以传达路径的物理特性和预计导航时间，以及车站中使用的真实世界寻路系统。
 
## 路径连接 
 
 在基础层面上，路径提供基本功能来连接vehicle内位置类型中定义的关键区域。这些连接形成pathways，使用户能够获得精确的方向（例如从入口到登车区），这在导航大型和复杂的交通站时特别有用。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`pathway_id`, `from_stop_id`, `to_stop_id`, `pathway_mode`, `is_bidirectional ` | 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [位置类型](../base_add-ons/#location-types) 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例定义了预定位置（定义为stops）之间的多个连接（也称为pathways）：人行道（` pathway_mode=1）、楼梯（`pathway_mode=2）和检票口（`pathway_mode=6）。还指定了双向性。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 |pathway_id |from_stop_id |to_stop_id |pathway_mode|is_bidirectional的| 
 |------------|-----------|------------|--------------|------------------| 
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
 
 
## 路径详情
 
 可以添加有关车站pathways的物理特性的更多详细信息，包括长度、宽度和坡度（对于坡道）或楼梯数量（对于楼梯）。这有助于乘客预测他们需要通行的路径的状况和可达性。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`max_slope`, `min_width`, `length`, `stair_count`| 
 
 **先决条件**: 
 
 - [基本特征](../base) 
 - [通路连接](#pathway-connections) 
 
 ??? 注意“样本数据” 
 
<p style="font-size:16px"> 
 以下示例定义了预先设定的pathways的附加细节，包括最小宽度、楼梯的步数以及人行道的长度和最大坡度。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 |pathway_id |max_slope|min_width| 长度 |stair_count| 
 |------------|-----------|--------|-----------| 
 | MainSt-001 | 0 | 4.3 | 3.6 | | 
 | MainSt-002 | | 2.2 | | 15 | 
 | MainSt-003 | 0.06 | 4 | 3.1 | | 
 | MainSt-004 | | 0.9 | 2.9 | | 
 | MainSt-005 | 0 | 3.5 | 5 | | 
 | MainSt-006 | | 2.2 | | 18 | 
 | MainSt-007 | 0 | 3.5 | 5 | | 
 | MainSt-008 | | 2.2 | | 18 | 
 MainSt-009 | 0 | 6 | 2 | | 
 | MainSt-010 | 0 | 6 | 2 | | 
 
 
## 楼层 
 
 楼层可用于列出车站内的所有不同楼层，为用户提供有关车站的额外信息。此功能还可将电梯与 Pathways 连接功能结合使用。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[levels.txt](../../../documentation/schedule/reference/#levelstxt)|`level_id`, `level_index`, `level_name`| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`level_id`| 
 
 **先决条件**：
 
 - [基本功能](../base) 
 - [位置类型](../base_add-ons/#location-types) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例显示了车站的不同级别。然后，位置（定义为stops）被分配到其相应的级别。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | level_id | level_index | level_name | 
 |-------------------|-------------|------------| 
 | level_0_street | 0 | 在街道上 | 
 | level_-1_lobby |-1 | 大厅 | 
 | level_-2_platform |-2 | 平台 | 
 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | stop_id | level_id | 
 |--------------|----------| 
 | Station_A102 | | 
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
 | A102_F02 |-1## 站内遍历时间 
 
 站内遍历时间为站内路线提供了额外的详细信息，为用户提供了导航站点所需的预计时间，从而提供了更好的旅行路线和旅行时间。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`traversal_time`| 
 
 **先决条件**： 
 
 - [基本特征](../base) 
 - [路径连接](#pathway-connections) 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例显示了导航每条路径所需的预计行程时间（以秒为单位）。
</p> 
 ！！！ 笔记 ”” 
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
 
 
## 路径标志 
 
 路径标志可以将行程规划器中显示的信息与现实世界的标志联系起来。如果将其显示在信息流中，行程规划器可以提供“按照标志前往”等指示。
 
 |包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`signposted_as`, `reversed_signposted_as`| 
 
 **先决条件**: 
 
 - [基本特征](../base) 
 - [通路连接](#pathway-connections) 
 
 ??? 注意“样本数据” 
 
<p style="font-size:16px"> 
 以下示例指定了与预先建立的pathways相关的导航信息，反映了车站物理标志上显示的文字。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | signposted_as | reversed_signposted_as | 
 |------------|------------------|------------------------| 
 | MainSt-001 | 前往大厅 | 出口 | 
 | MainSt-002 | | | 
 | MainSt-003 | 前往站台 | 出口 | 
 | MainSt-004 | | | 
 | MainSt-005 | 西行列车 | 出口 | 
 | MainSt-006 | | | 
 | MainSt-007 | 东行列车 | 出口 | 
 | MainSt-008 | | | 
 | MainSt-009 | 西行列车 | 前往大厅 | 
 | MainSt-010 | 东行列车 | 前往大厅 | 
 
 

