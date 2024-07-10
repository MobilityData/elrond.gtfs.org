# 基础 
 以下功能提供了GTFS表示交通服务所需的最基本和最必要的元素。 GTFS由routes组成，每条路线都有相关的行程。这些行程在特定时间访问一个或多个stops。行程仅包含一天中的时间信息，其运营日期由日历决定。 
 必须一起实现所有这些功能才能启用有效的GTFS供稿。 
 
## 机构 
 
 机构包含有关负责交通服务的机构的基本信息，例如其名称、网站URL以及服务运营的语言和时区。这允许将特定服务与其相应的agency相匹配。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url`, `agency_email` | 
 
 **先决条件**: 
 
 - 所有其他基本功能 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 
 
 | agency_id | agency_name | agency_url | agency_timezone | agency_lang | agency_phone | agency_fare_url | agency_email | 
 |-----------|-------------|----------------------------|---------------------|-------------|----------------|----------------------------------|------------------------| 
 | tb | Transit Bus | https://www.transitbus.org | America/Los_Angeles | EN | (777) 555-7777 | https://www.transitbus.org/fares | contact@transitbus.org | 
 
 
 
## 站点 
 
 站点是用于识别交通服务接送乘客地点的基本元素。这可能是地铁站或公交车站。除其他属性外，每个站点都具有地理坐标（用于在地图上精确定位其位置）和与机构面向乘客的材料相匹配的名称。站点通过停止时间与行程相关联。
 使用GTFS，还可以使用 [Pathways](/getting_started/features/pathways) 描述较大车站（如火车站或公交车站）的内部。
 
 | 包含的文件 | 包含的字段 |
 |----------------------------------|----------------------------------|
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`、`stop_code、` stop_name`、`stop_name、`stop_desc、`stop_lat、`stop_lon、`stop_url 、` platform_code |
 
 **先决条件**：
 
 - 所有其他基本功能
 
 ??? 注意“示例数据”
 stop_timezone<p style="font-size:16px"> 
 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_code | stop_desc | stop_name | stop_lat | stop_lon | stop_url | stop_timezone | platform_code | 
 |---------|---------------|--------------------------------------------|------------|------------|------------|-----------------------------------------|------------------|------------------| 
 | TAS001 | TAS001 | 第 5 大道与 第 53 街西南角 | 5 Av/53 St | 45.503568 |-73.587079 | https://www.transitbus.org/stops/TAS001 | | | 
 
 
##stops
 
 路线是同一品牌下的一组行程，作为单一服务显示给乘客。除其他属性外，每条路线都有一个与机构面向乘客的材料相匹配的名称，以及所代表的服务类型（例如公共汽车、地铁、渡轮等）。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`，`agency_id`，`route_desc`，`route_type`，`route_url`，`route_sort_order`，`route_short_name`，`route_long_name`| 
 
 **先决条件**：
 
 - 所有其他基本功能
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例定义了一条公交路线（`route_type=3 `）。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |----------|-----------|------------------|--------------------------------|-------------------------------------------------------------------|------------|---------------------------------------------------|--------------------------------| 
 | RA | tb | 17 | 米申 - 市中心 | “A”路线从下米申开往市中心。 | 3 | https://www.transitbus.org/routes/ra | 12 | 
 
 
## 服务日期 
 
 服务日期表示服务运行的日期范围，以及在特定日期创建服务豁免，例如假期和其他特殊服务。
 它的工作原理是在 `calendars.txt ` 中定义开始date和结束date，然后为它运行的每一天定义一个标记。如果在此期间发生单日调度变更，那么可以使用`calendar_dates.txt`文件覆盖这些天的调度。
 
 | 包含的文件 | 包含的字段 |
 |----------------------------------|----------------------------------|
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`|
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **先决条件**：
 
 - 所有其他基本功能
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例定义了 2024 年 7 月的两项服务（工作日和周末），其中包括 7 月 4 日的特殊假日服务，作为周末服务运营。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 
 
 | service_id |monday|tuesday|wednesday|thursday|friday|saturday|sunday| start_date | end_date | 
 |------------|--------|---------|-----------|-----------|--------|-----------|--------|------------|-------| 
 | WE | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | WD | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 
 
 | service_id |date| exception_type | 
 |------------|-----------|----------------| 
 | WD | 20240704 | 2 | 
 | WE | 20240704 | 1 | 
 
## 行程 
 
 行程汇集路线和服务日期以创建乘客可以进行的旅程。行程通过停止时间与停止相关联。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **先决条件**：
 
 - 所有其他基本功能
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例定义了 RA 路线的两次双向行程。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |----------|------------|---------|-----------------|--------------|----------| 
 | RA | WE | AWE1 | 3885 | 0 | 1 | 
 | RA | WE | AWE2 | 3887 | 1 | 2 | 
 
## 停靠时间 
 
 停靠时间用于表示每次行程的各个`stop_times.txt`站的arrival和departure时间，让乘客准确知道公交车、火车或渡轮到达和离开特定地点的时间。`stop_times.txt`文件通常是GTFS供稿中最大的文件。
 某些服务以固定频率运行（例如每 5 分钟一班的地铁线路），而不是有具体的arrival和departure时间。这可以使用[基于频率的服务](../base_add-ons/#frequency-based-service) 进行建模，并且可以与`stop_times.txt`结合进行建模。
 
 | 包含的文件 | 包含的字段 |
 |----------------------------------|----------------------------------|
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`，`arrival_time， `departure_time`， `stop_id`， `stop_sequence`，`pickup_type，`drop_off_type，`timepoint|
 
 **先决条件**：
 
 - 所有其他基本功能
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例定义了 5 个stops的行程安排。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id |arrival_time|departure_time| stop_id | stop_sequence | pickup_type | drop_off_type |timepoint| 
 |---------|-----------|----------------|---------|--------------|-------------|-------------|-----------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 | 6:23:00 TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 0 | 0 | 1 | 
 

