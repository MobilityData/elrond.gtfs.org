# 灵活服务 
 灵活服务，也称为需求响应服务，是不遵循预定和/或固定服务的常见行为的服务。
 
## 连续停靠 
 
 当乘客可以在预定的stops之间上下车时，使用连续停靠。
 这可以在 `routes.txt` 中指定，表示可以在路线的每次行程中在车辆行驶路径上的任何一点接送乘客，也可以在`stop_times.txt`中指定，表示在路线的​​特定部分。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off ` | 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例展示了表示连续停止的两种方式。
</p> 
 
<p style="font-size:16px"> 
 第一个示例显示，允许在路线“RA”沿线的任何地点接送乘客。
</p> 
 
<p style="font-size:16px"> 
 第二个示例显示，允许在行程“ AWE1 ”的第三stops之间上下车，通过将“ continuous_pickup”和“continuous_drop_off”值分配给“stop_sequence=3 ”和“stop_sequence=4 ”来实现。
</p> 
 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | route_short_name | route_type | continuous_pickup | continuous_drop_off | 
 |----------|------------------|------------|-------------------|---------------------| 
 | RA | 17 | 3 | 0 | 0 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id |arrival_time|departure_time| stop_id | stop_sequence |continuous_pickup|continuous_drop_off下车 | 
 |---------|-----------|----------------|---------|---------------|----------------------|---------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | | | 
 
## 预订规则 
 
 预订规则可用于让用户预订需求响应服务的行程。这些规则概述了成功预订的必要先决条件，并提供了用户预订行程的联系信息。如果此类服务需要预订，则此功能应与 [带偏差的预定义路线](#predefined-routes-with-deviation)、[基于区域的需求响应服务](#zone-based-demand-responsive-services) 和 [固定站点需求响应服务](#fixed-stops-demand-responsive-services) 功能require使用。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`, `booking_type`, `prior_notice_duration_min`, `prior_notice_duration_max`, `prior_notice_last_day`, `prior_notice_last_time`, `prior_notice_start_day`, `prior_notice_start_time`, `prior_notice_service_id`, `message, `pickup_message`, `drop_off_message`, `phone_number`, `info_url`, `booking_url` | 
 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例显示了两组不同的预订规则，第一组适用于必须至少提前一天（下午 1 点之前）且不超过 14 天预订的行程，第二组适用于可以在行程前至少 45 分钟且不超过 5 小时预订的行程。
 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 
 
 | booking_rule_id | booking_type | Prior_notice_duration_min | Prior_notice_duration_max | Prior_notice_last_day | Prior_notice_last_time | Prior_notice_start_day | Prior_notice_start_time | Prior_notice_service_id |message| pickup_message | drop_off_message | phone_number | info_url | booking_url | 
 |-----------------|--------------|-----------------------------|-------------------------------|-----------------------------|------------------------|------------------------|-------------------------|-------------------------|-------------------------|------------------------------------------------------------------------------------------------------------------------|----------------|-------------------|----------------|--------------------------| 
 | route_br_1818 | 2 | | | 1 | 13:00 | 14 | 9:00 | |要叫车，请在行程前至少一个工作日下午 1 点之前拨打 123-111-2233。您最多可以提前 14 个工作日预订行程。| | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | route_br_4545 | 1 | 45 | 300 | | | | | | 要叫车，请使用我们网站上的官方预订系统，行程必须至少提前 45 分钟预订 | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## 带偏差的预定义路线
 
 带偏差的预定义路线可用于模拟灵活的服务，其中车辆可以短暂偏离特定路线来接载在沿途特定区域内预订行程的用户。这使用了传统stops（如定期的预定服务）和使用`locations.geojson`的区域的组合。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Type`, `Features`, `Features:Type`, `Features:Id`, `Features:Properties`, `Features:Properties:Stop_name`, `Features:Properties:Stop_description`, `Features:Geometry`, `Features:Geometry:Type`, `Features:Geometry:Coordinates` | 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [预订规则](#booking-rules) 如果服务需要预订 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例显示了具有三个固定stops的行程，该行程也可以在固定stops之间定义的特定区域内的任何地方下车。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id |arrival_time|departure_time| stop_id | location_id | stop_sequence |start_pickup_drop_off_window|end_pickup_drop_off_window| pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|--------------|----------------|---------|--------------------------|-----------------------------|-----------------------------|----------------------------|-------------|-------------|---------------------|------------------------|-------------------------| 
 | 4545_001 | 10:00:00 | 10:00:00 | S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | zone_S50122_to_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | zone_S50123_to_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
 !!! 注意“”
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
# 简化，这里只显示 3 个坐标。 
 "coordinates": [
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
 "properties": {} 
 }, 
 { 
 "id": "zone_S50123_to_S50124", 
 "type": "Feature", 
 "geometry": { 
 "type": "Polygon", 
# 简化，这里只展示 3 个坐标。 
 "coordinates": [
 [
 [
 -73.561332, 
 45.5085599 
], 
 [
 -73.5701298, 
 45.5124057 
], 
 [
 -73.571302, 
 45.5105563 
] 
] 
] 
 }, 
 "properties": {} 
 } 
] 
 } 
 ~~~ 
 
## 基于区域的需求响应服务
 
基于区域的需求响应服务用于为预订行程的用户模拟允许在特定区域内的任何地点接送的服务。这些区域是使用`locations.geojson`定义的，因此不需要使用`stops.txt` ，也不require使用 ` stop_times.arrival_time` 和`stop_times.departure_time`。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Type`, `Features`, `Features:Type`, `Features:Id`, `Features:Properties`, `Features:Properties:Stop_name`, `Features:Properties:Stop_description`, `Features:Geometry`, `Features:Geometry:Type`, `Features:Geometry:Coordinates` | 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [预订规则](#booking-rules) 如果服务需要预订 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例展示了一项可以在上午 9 点到下午 6 点之间在特定区域内接送预订乘客的服务。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | location_id | stop_sequence |start_pickup_drop_off_window|end_pickup_drop_off_window| pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|---------------|-----------------------------|----------------------------|-------------|-------------|------------------------|-------------------------| 
 | 2708_001 | area_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | area_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
 !!! 注意“”
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
# 简化，这里只展示 3 个坐标。 
 "coordinates": [
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
 -73.636580,
 45.5081683
]
]
]
},
 "properties": {}
}
]
}
~~~

##固定站点需求响应服务
固定站点需求响应服务用于为预订行程的用户模拟允许在预定义stops组内的任何位置接送的服务。这些stops组是使用 `location_groups.txt` 和 `location_group_stops.txt` 定义的。
 
 | 包含的文件 | 包含的字段 |
 |----------------------------------|----------------------------------|
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`|
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [预订规则](#booking-rules) 如果服务需要预订 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例展示了一项可以在上午 7 点到 10 点之间在 4 个不同stops接送预订乘客的服务。
 
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#location_groupstxt"><b>位置组.txt</b></a><br> 
</p> 
 
 | location_group_id | location_group_name | 
 |-------------------|-------------------------------| 
 | r27_stops | 黄色行政区 27 号路线stops| 
 
 !!! 注意“”
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>位置组停靠点.txt</b></a><br> 
</p> 
 
 | location_group_id | stop_id | 
 |-------------------|---------| 
 | r27_stops | syb029 | 
 | r27_stops | syb030 | 
 | r27_stops | syb031 | 
 | r27_stops | syb032 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | location_group_id | stop_sequence |start_pickup_drop_off_window|end_pickup_drop_off_window| pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------------|------------------------------|-----------------------------|----------------------------|-------------|-------------|------------------------|---------------------------| 
 | 2714_002 | r27_stops | 1 | 7:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_stops | 2 | 7:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

