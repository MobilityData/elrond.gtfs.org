# 유연한 서비스 
 수요 대응 서비스라고도 불리는 유연한 서비스는 예정된 서비스 및/또는 고정된 서비스의 일반적인 동작을 따르지 않는 서비스입니다. 
 
## 연속 정차 
 
 연속 정차는 예정된 stops 사이에 승객을 태우거나 내릴 수 있는 경우에 사용됩니다. 
 이는 경로의 모든 이동에 대해 차량의 이동 경로를 따라 어느 지점에서나 탑승자를 태우거나 내릴 수 있음을 나타내는 `routes.txt` 또는 특정 구간에 대한 `stop_times.txt` 에 지정할 수 있습니다. 경로의. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off ` | 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 연속 정지를 나타내는 두 가지 방법을 보여줍니다. 
</p> 
 
<p style="font-size:16px"> 
 첫 번째 샘플은 ’RA’ 경로를 따라 어느 지점에서나 승하차가 허용된다는 것을 보여줍니다. 
</p> 
 
<p style="font-size:16px"> 
 두 번째 샘플은 ’ AWE1 ’의 세 번째 정류장과 다섯 번째 stops 사이에서 승하차가 허용됨을 보여줍니다. 이는 ` continuous_pickup` 및 `continuous_drop_off` 값을 `stop_sequence=3` 및 `stop_sequence=4`에 할당하여 수행됩니다. 
</p> 
 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | route_short_name | route_type | continuous_pickup | continuous_drop_off | 
 |----------|------|------------|-------------------|---------| 
 | 라 | 17 | 3 | 0 | 0 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | continuous_pickup | continuous_drop_off | 
 |---------|---------------|---|---------|---------------|------|---------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | | | 
 
## 예약 규칙 
 
 예약 규칙은 사용자가 수요 대응 서비스에서 여행을 예약할 수 있도록 하는 데 사용될 수 있습니다. 이러한 규칙은 성공적인 예약을 위해 필요한 전제 조건을 간략하게 설명하고 사용자가 여행을 예약할 수 있는 연락처 정보를 제공합니다. 이 기능은 [편차가 있는 사전 정의된 경로](#predefine-routes-with-deviation), [영역 기반 수요 반응 서비스](#zone-based-demand-Response-services) 및 [고정 정지]와 함께 사용해야 합니다. 수요 대응 서비스](#fixed-stops-demand-responsive-services) 기능(해당 서비스에 예약이 require 경우). 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`, `booking_type`, `prior_notice_duration_min`, `prior_notice_duration_max`, `prior_notice_last_day`, `prior_notice_last_time `, `prior_notice_start_day`, `prior_notice_start_time`, `prior_notice_service_id`, `message`, `pickup_message`, `drop_off_message`, `phone_number`, `info_url`, `booking_url` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 두 가지 예약 규칙 세트를 보여줍니다. 첫 번째는 최소 하루 전(오후 1시 이전), 최대 14일 전에 예약해야 하는 여행에 대한 것이고, 두 번째는 예약할 수 있는 여행에 대한 것입니다. 여행 출발 최소 45분 전, 최대 5시간 전. 
 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 
 
 | 예약_규칙_ID | 예약 유형 | before_notice_duration_min | before_notice_duration_max | before_notice_last_day | before_notice_last_time | before_notice_start_day | before_notice_start_time | prior_notice_service_id | message | 픽업_메시지 | drop_off_message | 전화번호 | info_url | 예약_URL | 
 |----|---------------|------------------------|---------------|-----------------------|------------|------------------------|------------|-------------------------|-------------------------------------------------------------------------------------------------------------|----------------|------------------|---|---------|------------| 
 | Route_br_1818 | 2 | | | 1 | 13:00 | 14 | 9:00 | | 차량 서비스를 요청하려면 영업일 기준으로 여행 하루 전 오후 1시 이전에 123-111-2233으로 전화하세요. 사전에 영업일 기준 최대 14일까지 여행을 예약할 수 있습니다. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | Route_br_4545 | 1 | 45 | 300 | | | | | | 차량 서비스를 요청하려면 당사 웹사이트의 공식 예약 시스템을 이용하세요. 여행은 최소 45분 전에 예약해야 합니다 | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## 편차가 있는 사전 정의된 경로 
 
 편차가 있는 사전 정의된 경로는 차량이 특정 경로에서 잠시 벗어나 특정 지역 내에서 여행을 예약한 사용자를 태울 수 있는 유연한 서비스를 모델링하는 데 사용할 수 있습니다. 노선. 이는 기존 stops (예: 정기 정기 서비스)과 `locations.geojson` 사용하는 구역의 조합을 사용합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`유형`, `기능`, `기능:유형`, `기능:ID`, `기능 :속성`, `특징:속성:정지_이름`, `특징:속성:정지_설명`, `특징:기하학`, `특징:기하학:유형`, `특징:기하학:좌표` | 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [예약 규칙](#booking-rules) 서비스에 예약이 필요한 경우 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 고정 stops 사이에 정의된 특정 지역 내 어디에서나 승객을 내릴 수 있는 세 개의 고정 stops 있는 여행을 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | 위치_ID | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |------------|---------------|---|--------|------------|---------------|---------------|---------------|-------------|---------------|-------------------|------------|-------------| 
 | 4545_001 | 10:00:00 | 10:00:00 | S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | zone_S50122_to_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | zone_S50123_to_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "유형": "FeatureCollection", 
 "기능": [
 { 
 "id": "zone_S50122_to_S50123", 
 "유형": "기능", 
 "geometry": { 
 "type": "Polygon", 
# 단순화되었으며 여기에는 3개의 좌표만 표시됩니다. 
 "좌표": [
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
 "속성": {} 
 }, 
 { 
 "id": "zone_S50123_to_S50124", 
 "유형": "기능", § § "geometry": { 
 "type": "Polygon", 
# 단순화되었으며 여기에는 3개의 좌표만 표시됩니다. 
 "좌표": [
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
 "속성": {} 
 } 
] 
 } 
 ~~~ 
 
## 영역 기반 수요 응답 서비스 
 
 구역 기반 수요 반응 서비스는 여행을 예약한 사용자를 위해 특정 지역 내의 모든 위치에서 픽업 및/또는 하차를 허용하는 서비스를 모델링하는 데 사용됩니다. 이러한 영역은 `locations.geojson` 사용하여 정의되므로 `stops.txt` 또는 `stop_times 사용할 require 가 없습니다. arrival_time` &amp; `stop_times.departure_time`. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`유형`, `기능`, `기능:유형`, `기능:ID`, `기능 :속성`, `특징:속성:정지_이름`, `특징:속성:정지_설명`, `특징:기하학`, `특징:기하학:유형`, `특징:기하학:좌표` | 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [예약 규칙](#booking-rules) 서비스에 예약이 필요한 경우 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 오전 9시에서 오후 6시 사이 특정 지역 어디에서나 사전 예약된 승객을 태우고 내려줄 수 있는 서비스를 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | 위치_ID | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|---------------|-----------------|---------------|---------------|---------------|---------|-------------| 
 | 2708_001 | 지역_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | 지역_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "유형": "FeatureCollection", 
 "기능": [
 { 
 "id": "area_001", 
 "유형": "기능", 
 "geometry": { 
 "type": "Polygon", 
# 단순화되었으며 여기에는 3개의 좌표만 표시됩니다. 
 "좌표": [
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
 "속성": {} 
 } 
] 
 } 
 ~~~ 
 
## 고정 정지 수요 반응 서비스 
 고정 정류장 수요 반응 서비스는 여행을 예약하는 사용자를 위해 사전 정의된 stops 그룹 내의 모든 위치에서 승하차를 허용하는 서비스를 모델링하는 데 사용됩니다. 이러한 stops 그룹은 `location_groups.txt` 및 `location_group_stops.txt 를 사용하여 정의됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [예약 규칙](#booking-rules) 서비스에 예약이 필요한 경우 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 오전 7시부터 오전 10시까지 4개의 다른 stops 에서 사전 예약된 승객을 태우고 내려줄 수 있는 서비스를 보여줍니다. 
 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_groupstxt"><b>위치_그룹 .txt</b></a><br> 
</p> 
 
 | 위치_그룹_ID | 위치_그룹_이름 | 
 |------|-------------------| 
 | r27_stops | Yellow Borough Route 27 stops | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>location_group_stops.txt</b></a><br> 
</p> 
 
 | 위치_그룹_ID | stop_id | 
 |------|---------| 
 | r27_stops | syb029 | 
 | r27_stops | syb030 | 
 | r27_stops | syb031 | 
 | r27_stops | syb032 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | 위치_그룹_ID | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |------------|------|---------------|-----------------|---------------|-------------|---------------|----------------------|-------------| 
 | 2714_002 | r27_stops | 1 | 7:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_stops | 2 | 7:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

