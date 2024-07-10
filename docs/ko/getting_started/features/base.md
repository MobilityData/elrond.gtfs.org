# 기본 
 다음 기능은 GTFS 대중교통 서비스를 나타내는 데 필요한 가장 기본적이고 필수적인 요소를 제공합니다. GTFS 각각 관련 이동이 포함된 routes 로 구성됩니다. 이 여행은 특정 시간에 하나 이상의 stops 방문합니다. 여행에는 시간 정보만 포함되며, 운행 요일은 달력에 따라 결정됩니다. 
 GTFS 피드가 작동하려면 이러한 모든 기능을 함께 구현해야 합니다. 
 
## 기관 
 
 기관에는 이름, 웹사이트 URL, 서비스가 운영되는 언어 및 시간대 등 대중교통 서비스를 담당하는 기관에 대한 기본 정보가 포함되어 있습니다. 이를 통해 특정 서비스를 해당 agency 과 일치시킬 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url`, `agency_email` | 
 
 **전제 조건**: 
 
 - 기타 모든 기본 기능 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 
 
 | agency_id | agency_name | agency_url | agency_timezone | agency_lang | agency_phone | agency_fare_url | agency_email | 
 |------------|-------------|----------------|---------|-------------|--------------|---------|-----------| 
 | 결핵 | 대중교통 버스 | https://www.transitbus.org | America/Los_Angeles | KO | (777) 555-7777 | https://www.transitbus.org/fares | contact@transitbus.org | 
 
 
 
## 정류장 
 
 정류장은 대중교통 서비스가 승객을 태우고 내리는 위치를 식별하는 데 사용되는 기본 요소를 나타냅니다. 지하철 역일 수도 있고 버스 정류장일 수도 있습니다. 각 정류장은 무엇보다도 지도에서 해당 위치를 정확히 표시할 수 있는 지리적 좌표와 기관의 승객이 접하는 자료와 일치하는 이름을 가지고 있습니다. 정류장은 정차 시간을 사용하여 이동과 연결됩니다. 
 GTFS 사용하면 [경로](/getting_started/features/pathways)를 사용하여 기차역이나 버스 정거장과 같은 대규모 역의 내부를 설명하는 것도 가능합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`, `stop_code`, `stop_name`, `stop_desc`, `stop_lat`, `stop_lon`, `stop_url`, `stop_timezone`, `platform_code` | 
 
 **전제 조건**: 
 
 - 기타 모든 기본 기능 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_code | stop_desc | stop_name | stop_lat | stop_lon | stop_url | stop_timezone | platform_code | 
 |---------|------------|------------------|------------|---------|------------|---------------|---------------|---------------| 
 | TAS001 | TAS001 | 5번가와 53번가의 남서쪽 모퉁이 | 5 Av/53 스트리트 | 45.503568 |-73.587079 | https://www.transitbus.org/stops/TAS001 | | | 
 
 
## 경로 
 
 경로는 라이더에게 단일 서비스로 표시되는 동일한 브랜드의 이동 그룹입니다. 각 경로에는 여러 속성 중에서 기관의 승객 대상 자료와 일치하는 이름과 표시되는 서비스 유형(예: 버스, 지하철 또는 지하철, 페리 등)이 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`, `agency_id, `route_desc, `route_type, `route_url, `route_sort_order, `route_short_name, `route_long_name| 
 
 **전제 조건**: 
 
 - 기타 모든 기본 기능 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 버스 경로(`route_type=3`)를 정의합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |------------|------------|------|--------------------|-----------------|------------|------------------------------------|------| 
 | 라 | 결핵 | 17 | 미션 - 다운타운 | "A" 경로는 낮은 미션에서 다운타운까지 이동합니다. | 3 | https://www.transitbus.org/routes/ra | 12 | 
 
 
## 서비스 날짜 
 
 서비스 날짜는 서비스가 실행되는 날짜 범위를 나타내며 특정 날짜에 휴일 및 기타 특별 서비스와 같은 서비스 면제를 생성합니다. 
 ` .txt 에 시작 date 와 완료 date 정의한 다음 해당 요일에 대한 표시를 정의하여 작동합니다. 이 기간 동안 하루 일정 변경이 발생하는 경우 ’`calendar_dates.txt`’ 파일을 사용하여 각 날짜의 일정을 재정의할 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **전제 조건**: 
 
 - 기타 모든 기본 기능 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 2024년 7월 한 달 동안 주말 서비스로 운영되는 7월 4일 특별 공휴일 서비스를 포함하여 두 가지 서비스(주중 및 주말)를 정의합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 
 
 | service_id | monday | tuesday | wednesday | thursday | friday | saturday | sunday | start_date | end_date | 
 |------------|---------|---------|------------|----------|----------|----------|---------|------------|----------| 
 | 우리 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | WD | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 
 
 | service_id | date | exception_type | 
 |------------|----------|---| 
 | WD | 20240704 | 2 | 
 | 우리 | 20240704 | 1 | 
 
## 여행 
 
 여행은 경로와 서비스 날짜를 결합하여 승객이 이용할 수 있는 여행을 만듭니다. 여행은 정차 시간을 사용하여 정류장과 연결됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **전제 조건**: 
 
 - 기타 모든 기본 기능 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 RA 경로에 대해 양방향으로 실행되는 두 가지 이동을 정의합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |----------|------------|---------|-----------------|---------------|----------| 
 | 라 | 우리 | AWE1 | 3885 | 0 | 1 | 
 | 라 | 우리 | AWE2 | 3887 | 1 | 2 | 
 
## 정차 시간 
 
 정차 시간은 각 여행의 개별 정류장 arrival 및 departure 시간을 나타내는 데 사용되므로 승객은 버스, 기차 또는 페리가 특정 위치에 도착하고 출발하는 시간을 정확하게 알 수 있습니다..`stop_times.txt` 파일은 일반적으로 GTFS 피드에서 가장 큽니다. 
 특정 서비스는 특정 arrival 및 departure 시간이 아닌 정기적인 빈도(예: 5분마다 운행하는 지하철 노선)로 운영됩니다. 이는 [빈도 기반 서비스](../base_add-ons/#주파수-기반-서비스)를 사용하여 모델링할 수 있으며 `stop_times.txt` 와 함께 모델링할 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`, `arrival_time`, `departure_time`, `stop_id`, `stop_sequence`, `pickup_type, `drop_off_type, `timepoint` | 
 
 **전제 조건**: 
 
 - 기타 모든 기본 기능 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 5개 stops 의 여행 일정을 정의합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | pickup_type | drop_off_type | timepoint | 
 |---------|---------------|---|---------|---------------|------------|---------------|------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 0 | 0 | 1 | 
 

