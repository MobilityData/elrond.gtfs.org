# Base 附加组件 
 这些功能扩展了 Base 中描述的功能，用于增强GTFS数据集的全面性以提供更好的乘客体验，或促进机构、数据供应商和数据重复使用者之间的协作。这些增强功能可能需要在 Base 中描述的文件中引入新字段，或者创建新文件。
 
## Feed 信息 
 
 Feed 信息传达有关 feed 的重要信息，例如其有效性（开始和结束date）、发布组织以及有关GTFS数据集和数据发布实践的查询的联系信息。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`, `feed_publisher_url`, `feed_lang`, `default_lang`, `feed_start_date`, `feed_end_date`, `feed_version`, `feed_contact_email`, `feed_contact_url` | 
 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 
 
 | feed_publisher_name | feed_publisher_url | feed_lang | default_lang | feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |--------------------------|--------------------------|---------------|---------------|-----------------|---------------|--------------------|---------------| 
 | 大区域运输 | https://www.gra1.org | en | en | 20240101 | 20241231 | 3.1 | support@gra1.org | https://www.gra1.org/support | 
 
## 形状 
 可以定义形状并将其与行程相关联，从而使行程计划应用程序能够在地图上显示行程并告知乘客乘坐vehicle需要行驶的距离。 `shape_dist_traveled字段用于以编程方式确定向乘客展示地图时要绘制多少shape。
 定义形状时，需要在细节程度（例如，遵循道路的精确曲率）和仅有效传达必要信息之间取得平衡。
 
 |包含的文件 |包含的字段 |
 |----------------------------------|----------------------------------|
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`、`shape_pt_lat、`shape_pt_lon、`shape_pt_sequence、`shape_dist_traveled|
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled `| 
 
 
 **先决条件**: 
 
 - [基本特征](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例展示了 TriMet GTFS提要中shape的一部分（<a     href="https://developer.trimet.org/GTFS.shtml">在此处</a>下载）。<br><br> 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 
 
 | shape_id | shape_pt_lat | shape_pt_lon | shape_pt_sequence | shape_dist_traveled | 
 |---------|-------------|-------------|------------------|-------------------| 
 | 558674 | 45.47623 |-122.721885 | 1 | 0.0 | 
 | 558674 | 45.476235 |-122.72236 | 2 | 121.9 | 
 | 558674 | 45.476237 |-122.722523 | 3 | 163.7 | 
 | 558674 | 45.476242 |-122.723024 | 4 | 292.2 | 
 558674 | 45.476244 |-122.72316 | 5 | 327.1 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 
 
 | trip_id | shape_id| 
 |--------|--------| 
 |13302375|558674 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 
 
 | trip_id | stop_sequence| shape_dist_traveled| 
 |--------|-------------|-------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## 路线颜色 
 
 使用路线颜色可以准确描述和传达机构设计指南分配给特定routes的配色方案。这使用户能够通过官方颜色轻松识别交通服务。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`, `route_text_color` | 
 
 
 **先决条件**：
 
 - [基本特征](../base) 
 
 ??? 注意“样本数据”
 
<p style="font-size:16px"> 
 以下示例显示路线“RA”使用十六进制颜色代码“D95700”呈现为橙色，并且文本应使用十六进制颜色代码“0”呈现为黑色。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |----------|-----------|------------------|--------------------|------------|----------|------------------| 
 | RA | agency001 | 17 | Mission- Downtown | 3 | D95700 | 0 | 
 
## Bike Allowed 
 
 Bike Allowed 表示服务于特定行程的车辆是否能够容纳自行车，帮助用户计划和访问使他们能够进行多式联运行程的服务。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed ` | 
 
 
 **先决条件**：
 
 - [基本特征](../base) 
 
 ??? 注意“样本数据”
 
<p style="font-size:16px"> 
 以下示例指定行程` AWE1 `中使用的vehicle可容纳至少一辆自行车（` bikes_allowed =1`），行程` AWE2 `中使用的vehicle（` bikes_allowed=2`）。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|------------|---------|---------------| 
 | RA | WE | AWE1 | 1 | 
 | RA | WE | AWE2 | 2 | 
 
## 头标 
 
 头标允许传达车辆用来指示行程目的地的标志，使用户更容易识别正确的交通服务。此功能支持沿特定路线的头标变化。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **先决条件**: 
 
 - [基本特征](../base) 
 
 ??? 注意“样本数据”
 
<p style="font-size:16px"> 
 以下示例中，第一个表格指定了行程 `AWE1` 和 `AWE2` 要使用的车头标志，第二个表格表示 `AWE1` 的车头标志将在停止 `TAS004` 后被修改，从而覆盖 `trips.txt` 中指定的车头标志。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_headsign | 
 |----------|------------|---------|---------------| 
 | RA | WE | AWE1 | 市中心 | 
 | RA | WE | AWE2 | 任务 | 
 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id |arrival_time|departure_time| stop_id | stop_sequence | stop_headsign | 
 |---------|-----------|----------------|---------|-----------|------------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 市中心 - 主广场 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 市中心 - 主广场 | 
 
## 位置类型 
 
 位置类型用于对交通站内的关键区域（例如出口/入口、节点或登车区）及其关系进行分类。位置类型是使用 Pathways 为交通站建模的基础。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **先决条件**：
 
 - [基本特征](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例在“`stops.txt`”中显示了交通站内的多个位置：代表主要位置的父站，以及其子位置，例如平台、入口/出口和通用节点。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | location_type | parent_station | 
 |--------------|------------------------------------------|---------------|----------------| 
 | Station_A102 | Main Street 站 | 1 | | 
 | A102_B01 | Main Street 站 - 北站台 | 0 | Station_A102 | 
 | A102_B02 | Main Street 站 - 南站台 | 0 | Station_A102 | 
 | A102_E01 | Main Street 站 - 入口/出口 | 2 | Station_A102 | 
 | A102_S01 | Main Street 站 - 入口楼梯顶部 | 3 | Station_A102 | 
 | A102_S02 | Main Street 站 - 入口楼梯底部 | 3 | Station_A102 | 
 | A102_S03 |主街站 - 北站台楼梯顶部 | 3 | Station_A102 | 
 | A102_S04 | 主街站 - 北站台楼梯底部 | 3 | Station_A102 | 
 | A102_S05 | 主街站 - 南站台楼梯顶部 | 3 | Station_A102 | 
 | A102_S06 | 主街站 - 南站台楼梯底部 | 3 | Station_A102 | 
 | A102_F01 | 主街站 - 检票口付费侧 | 3 | Station_A102 | 
 | A102_F02 | 主街站 - 检票口未付费侧 | 3 | Station_A102 | 
 
## 基于频率的服务 
 
 基于频率的服务可用于对以固定频率运行的服务进行建模，例如每 10 分钟一班的公交车或在指定时间间隔内每 2 分钟运行一次的地铁服务。 
 在对基于频率的服务进行建模时， `stop_times.txt`包含stops之间的相对时间，以确定要向乘客显示的时间。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| `trip_id`, `start_time`, `end_time`, `headway_secs`, `exact_times` | 
 
 
 **先决条件**： 
 
 - [基本功能](../base) 
 
 ???注意“样本数据”

<p style="font-size:16px"> 
 以下示例显示两个不同的行程：每 30 分钟运行一次的行程“AWE1”（`headway_secs=1800 `）和每 15 分钟运行一次的行程“AWE2”（`headway_secs=900 `）。
<p style="font-size:16px"> 
 “`exact_times`”字段表示时间表是否遵循“start_time”字段中输入的精确开始时间：
 - 行程“AWE1”从上午 6:10 到下午 12:00 每 30 分钟出发一次。
 - 行程“AW2”于上午 6:00、上午 6:15、上午 6:30 等出发。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 
 
 | trip_id | start_time | end_time | headway_secs | exact_times | 
 ---------|------------|-----------|--------------|-------------| 
 AWE1 | 6:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 6:00:00 | 19:50:00 | 900 | 1 | 
 
## 中转 
 
 中转提供不同旅行段（或航程）之间过渡的详细信息，使旅行计划者能够确定包含transfers的旅程的可行性。指定transfers并不意味着乘客t在其他地方中转，它只是表明某些transfers是否不可行或require最短中转时间。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, `from_trip_id`, `to_trip_id`, `transfer_type`, `min_transfer_time` | 
 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例显示了三种不同的transfers：一种是在stops之间，需要最短 5 分钟的换乘时间，一种是在两条routes之间定时换乘点，一种是在同一辆vehicle的两次行程之间进行的座位内换乘。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 
 
 | from_stop_id | to_stop_id | from_route_id | to_route_id | from_trip_id | to_trip_id | transfer_type | min_transfer_time | 
 |--------------|------------|--------------|--------------|--------------|-----------|-------------------| 
 | s6 | s7 | | | | | 2 | 300 | 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## 翻译 
 
 翻译允许以多种语言提供服务信息（例如车站名称），从而使旅行计划者能够根据用户的语言和位置设置以特定语言显示信息。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`language`,`translation`,`record_id`,`record_sub_id`,`field_value` | 
 
 
 **先决条件**： 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例显示了 `routes.txt中使用的两个字段的法语和西班牙语翻译：`route_long_name和 `route_desc</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 
 
 |table_name|field_name| 语言 | 翻译 |record_id |record_sub_id |field_value| 
 |------------|-----------------|----------|------------------------------------------------------------------|---------------|---------------|-------------| 
 |routes|route_long_name| ES | 米申 - 市中心 | RA | | | 
 |routes|route_long_name| FR | 米申 - 市中心 | RA | | | 
 |routes|route_desc| ES | 从 Lower Mission 出发的“A”路线到市中心 | RA | | | 
 |routes|route_desc| FR | 从 Lower Mission 出发的“A”路线到市中心。 | RA | | | 
 
## 归因 
 
 归因可以共享有关参与创建数据集的组织（生产者、运营商和/或当局等）的更多详细信息。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`, `agency_id`, `route_id`, `trip_id`, `organization_name`, `is_producer`, `is_operator`, `is_authority`, `attribution_url`, `attribution_email`, `attribution_phone` | 
 
 
 **先决条件**： 
 
 - [基本功能](../base) 
 
 ???注意“样本数据”

<p style="font-size:16px"> 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 
 
 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |----------------|--------------|---------|---------|-------------|-------------|-------------|--------------|---------------------------------|-------------------------|-------------------| 
 | op01 | tb | | | 过境巴士 | | 1 | | https://www.transitbus.org/fares | contact@transitbus.org | (777) 555-7777 | 
 | au01 | gra | | | 大区域交通 | 1 | | 1 | https://www.gra1.org | contact@gra1.org | (555) 555-5555 | 
 | op02 | | rtd023 | | 巴士公司 A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | op03 | | rtd025 | | 巴士公司 B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

