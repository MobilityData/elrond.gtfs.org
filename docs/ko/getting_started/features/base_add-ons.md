# Base 추가 기능 
 이러한 기능은 Base에 설명된 기능을 확장하여 GTFS 데이터세트의 포괄성을 향상하여 탑승자에게 더 나은 경험을 제공하거나 대행사, 데이터 공급업체 및 데이터 재사용자 간의 협업을 촉진하는 데 사용됩니다. 이러한 개선 사항에는 Base에 설명된 파일 내에 새 필드를 도입하거나 새 파일을 생성하는 작업이 포함될 수 있습니다. 
 
## 피드 정보 
 
 피드 정보는 유효성(시작 및 종료 date), 게시 조직, GTFS 데이터세트 및 데이터 게시 관행에 관한 문의 연락처 정보 등 피드에 대한 중요한 정보를 전달합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`, `feed_publisher_url`, `feed_lang`, `default_lang`, `feed_start_date`, `feed_end_date`, `feed_version`, `feed_contact_email`, `feed_contact_url` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 
 
 | feed_publisher_name | feed_publisher_url | feed_lang | default_lang | feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |---------------|---------|------------|---------------|----|-------------|---------------|-------|-----------------| 
 | 광역 교통 | https://www.gra1.org | ko | ko | 20240101 | 20241231 | 3.1 | support@gra1.org | https://www.gra1.org/support | 
 
## 모양 
 모양을 정의하고 여행과 연관시킬 수 있으므로 여행 계획 애플리케이션이 지도에 여행을 표시하고 승객에게 대중교통 vehicle 으로 이동해야 하는 거리를 알려줄 수 있습니다. `shape_dist_traveled 필드는 라이더에게 지도를 보여줄 때 그릴 shape 의 양을 프로그래밍 방식으로 결정하는 데 사용됩니다. 
 모양을 정의할 때 세부 수준(예: 도로의 정확한 곡률 따르기)과 필요한 정보만 효율적으로 전달하는 것 사이에 균형이 있습니다. 
 
 |포함된 파일 |포함된 필드 | 
 |---------|-------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`, `shape_pt_lat, `shape_pt_lon, `shape_pt_sequence, `shape_dist_traveled| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled `| 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 TriMet GTFS 피드( <a     href="https://developer.trimet.org/GTFS.shtml">여기에서</a> 다운로드)의 shape 일부를 보여줍니다.<br><br> 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 
 
 | shape_id | shape_pt_lat | shape_pt_lon | shape_pt_sequence | shape_dist_traveled | 
 |---------|-------------|-------------|------------------|------| 
 | 558674 | 45.47623 |-122.721885 | 1 | 0.0 | 
 | 558674 | 45.476235 |-122.72236 | 2 | 121.9 | 
 | 558674 | 45.476237 |-122.722523 | 3 | 163.7 | 
 | 558674 | 45.476242 |-122.723024 | 4 | 292.2 | 
 | 558674 | 45.476244 |-122.72316 | 5 | 327.1 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 
 
 | trip_id | shape_id| 
 |---------|---------| 
 |13302375|558674 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 
 
 | trip_id | stop_sequence| shape_dist_traveled| 
 |---------|-------------|------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## 경로 색상 
 
 경로 색상을 사용하면 기관의 설계 지침에 따라 특정 routes 에 할당된 색상 구성표를 정확하게 묘사하고 전달할 수 있습니다. 이를 통해 사용자는 공식 색상으로 대중교통 서비스를 쉽게 식별할 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`, `route_text_color` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 ’RA’ 경로가 HEX 색상 코드 ’D95700’을 사용하여 주황색이고 해당 텍스트가 HEX 색상 코드 ’0’을 사용하여 검정색으로 렌더링되어야 함을 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |------------|------------|------|--------------------|------------|---------------|------------------| 
 | 라 | 에이전시001 | 17 | 미션 - 다운타운 | 3 | D95700 | 0 | 
 
## 자전거 허용 
 
 자전거 허용은 특정 여행을 제공하는 차량이 자전거를 수용할 수 있는지 여부를 나타내며, 사용자가 복합 여행을 할 수 있는 서비스를 계획하고 액세스하는 데 도움이 됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed ` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 ` AWE1 ` 여행에 사용된 vehicle 최소한 한 대의 자전거를 탑승할 수 있고(` bikes_allowed =1`) 여행 ` AWE2 `에 사용된 vehicle 은 탑승할 수 없음(` bikes_allowed=2`)을 지정합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|------------|---------|---------------| 
 | 라 | 우리 | AWE1 | 1 | 
 | 라 | 우리 | AWE2 | 2 | 
 
## Headsigns 
 
 Headsigns를 사용하면 여행 목적지를 나타내는 차량에 사용되는 표지판을 전달할 수 있어 사용자가 올바른 대중교통 서비스를 더 쉽게 식별할 수 있습니다. 이 기능은 특정 경로를 따라 행선지 변경을 지원합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플에서 첫 번째 테이블은 `AWE1` 및 `AWE2` 여행에 사용될 행선지를 지정하고, 두 번째 테이블은 `AWE1`의 행선지가 `TAS004` 정류장 이후 수정되어 하나를 재정의함을 나타냅니다. `trips.txt 에 지정됩니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_headsign | 
 |----------|------------|---------|---------------| 
 | 라 | 우리 | AWE1 | 시내 | 
 | 라 | 우리 | AWE2 | 미션 | 
 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | stop_headsign | 
 |---------|---------------|---|---------|---------------|----------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 다운타운 - 메인 스퀘어 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 다운타운 - 메인 스퀘어 | 
 
## 위치 유형 
 
 위치 유형은 출구/입구, 노드 또는 탑승 구역과 같은 환승역 내의 주요 구역과 이들의 관계를 분류하는 데 사용됩니다. 위치 유형은 Pathways를 사용하여 대중교통 정류장을 모델링하기 위한 기초 역할을 합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 `stops.txt` 의 대중교통 역 내의 여러 위치를 보여줍니다. 즉, 주요 위치를 나타내는 상위 역과 플랫폼, 입구/존재, 일반 노드와 같은 하위 위치입니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | location_type | parent_station | 
 |---------------|---------------------------|---------------|----------------| 
 | 역_A102 | 메인 스트리트 역 | 1 | | 
 | A102_B01 | 메인 스트리트 역 - 북쪽 플랫폼 | 0 | 역_A102 | 
 | A102_B02 | 메인 스트리트 역 - 남쪽 플랫폼 | 0 | 역_A102 | 
 | A102_E01 | 메인 스트리트 역 - 입구/출구 | 2 | 역_A102 | 
 | A102_S01 | 메인 스트리트 역 - 입구 계단 상단 | 3 | 역_A102 | 
 | A102_S02 | 메인 스트리트 역 - 입구 계단 하단 | 3 | 역_A102 | 
 | A102_S03 | 메인 스트리트 역 - 북쪽 플랫폼 계단 상단 | 3 | 역_A102 | 
 | A102_S04 | 메인 스트리트 역 - 북쪽 플랫폼 계단 아래 | 3 | 역_A102 | 
 | A102_S05 | 메인 스트리트 역 - 남쪽 플랫폼 계단 상단 | 3 | 역_A102 | 
 | A102_S06 | 메인 스트리트 역 - 남쪽 플랫폼 계단 아래 | 3 | 역_A102 | 
 | A102_F01 | 메인 스트리트 역 - 개찰구 유료 쪽 | 3 | 역_A102 | 
 | A102_F02 | 메인 스트리트 역 - 개찰구의 무료 쪽 | 3 | 역_A102 | 
 
## 주파수 기반 서비스 
 
 주파수 기반 서비스는 10분마다 운행하는 버스나 지정된 시간 간격 내에서 2분마다 운행하는 지하철 서비스와 같이 정기적으로 운행되는 서비스를 모델링하는 데 사용할 수 있습니다. 
 빈도 기반 서비스를 모델링할 때 ’`stop_times.txt`’ 에는 탑승자에게 표시할 시간을 결정하기 위해 stops 사이의 상대적 시간이 포함되어 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequencytxt)| `trip_id`, `start_time`, `end_time`, `headway_secs`, `exact_times` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 30분마다 실행되는 `AWE1` 이동(`headway_secs=1800`)과 15분마다 실행되는 `AWE2` 이동(`headway_secs=900`)이라는 두 가지 별개의 이동을 보여줍니다. 
<p style="font-size:16px"> 
 `exact_times` 필드는 일정이 ’ start_time’ 필드에 입력된 정확한 시작 시간을 따르는지 여부를 나타냅니다. 
 - 여행 `AWE1`은 오전 6시 10분부터 오후 12시까지 30분마다 출발합니다. 
 - ’AW2’ 여행은 오전 6시, 오전 6시 15분, 오전 6시 30분 등에 출발합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 
 
 | trip_id | start_time | end_time | headway_secs | exact_times | 
 ---------|------------|----------|-------------|-------------| 
 AWE1 | 6:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 6:00:00 | 19:50:00 | 900 | 1 | 
 
## 환승 
 
 환승은 다양한 여행 구간(또는 구간) 간의 전환에 대한 세부 정보를 제공하므로 여행 계획자가 transfers 포함하는 여행의 타당성을 결정할 수 있습니다. transfers 지정한다고 해서 승객이 다른 곳으로 환승할 수 t 의미는 아니며 특정 transfers 불가능하거나 환승하는 데 최소 시간이 require 여부만 표시됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, `from_trip_id`, `to_trip_id`, `transfer_type`, `min_transfer_time` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 세 가지 다른 transfers 보여줍니다. 최소 5분의 환승 시간이 필요한 stops 간 환승, 두 routes 사이의 정시 환승 지점, 동일한 vehicle 으로 이루어진 두 이동 간의 좌석 내 환승. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 
 
 | from_stop_id | to_stop_id | from_route_id | to_route_id | from_trip_id | to_trip_id | transfer_type | min_transfer_time | 
 |---------------|------------|---------------|-------------|---------------|------------|---------------|------| 
 | s6 | s7 | | | | | 2 | 300 | 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## 번역 
 
 번역은 역 이름과 같은 서비스 정보를 다국어로 제공하여 여행 계획자가 사용자의 언어 및 위치 설정에 따라 특정 언어로 정보를 표시할 수 있도록 합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`언어`,`translation`,`record_id`,`record_sub_id`,`field_value` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 `routes.txt ` 및 ` route_desc `에 사용되는 두 필드에 route_long_name 제공되는 프랑스어 및 스페인어 번역을 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 
 
 | table_name | field_name | 언어 | 번역 | record_id | record_sub_id | field_value | 
 |------------|----|------------|------------------------------------------|------------|---------------|-------------| 
 | routes | route_long_name | ES | 미션 - 센트로 | 라 | | | 
 | routes | route_long_name | 프랑스 | 미션 - 센터빌 | 라 | | | 
 | routes | route_desc | ES | La ruta "A" viaja desde 하부 임무 hasta el centro | 라 | | | 
 | routes | route_desc | 프랑스 | La Route « A »는 Lower Mission au Centre-ville을 따릅니다. | 라 | | | 
 
## 속성 
 
 속성을 사용하면 데이터 세트 생성과 관련된 조직(생산자, 운영자 및/또는 당국 등)에 관한 추가 세부 정보를 공유할 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`, `agency_id`, `route_id`, `trip_id`, `organization_name`, `is_producer`, `is_operator`, `is_authority`, `attribution_url`, `attribution_email`, `attribution_phone` | 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 
 
 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |---|------------|----------|----------|---------------|-------------|-------------|----------------|----------------------|------------|------| 
 | op01 | 결핵 | | | 대중교통 버스 | | 1 | | https://www.transitbus.org/fares | contact@transitbus.org | (777) 555-7777 | 
 | au01 | 그래 | | | 광역 교통 | 1 | | 1 | https://www.gra1.org | contact@gra1.org | (555) 555-5555 | 
 | op02 | | RTD023 | | 버스 회사 A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | 작전03 | | RTD025 | | 버스회사 B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

