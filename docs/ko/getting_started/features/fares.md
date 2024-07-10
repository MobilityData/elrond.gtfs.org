# 요금 
 GTFS 사용하면 구역별 요금, 이동 거리별 요금, 시간대별 요금 등 전 세계 여러 대중교통 기관에서 사용하는 다양한 요금 구조를 정확하게 모델링할 수 있습니다. GTFS 요금은 승객에게 여행에 적용되는 price 과 지불에 사용할 수 있는 미디어를 알려줍니다. 
 
## 요금 상품 
 
 요금 상품에는 대중교통 agency 서비스 이용을 위해 제공하는 티켓 또는 요금 유형(예: 편도 요금, 월간 승차권, 환승 요금 등)이 나열되어 있습니다. 요금 상품은 기관의 요금 구조를 모델링하기 위한 기반 역할을 하며 `fare_leg_rules.txt`에 설명된 메커니즘을 통해 대중교통 서비스에 연결됩니다. routes, 지역, 시간 등 다양한 여행 조건에 대한 운임 상품의 연계에 따라 개별 여행 구간 및 transfers 대한 운임 비용이 결정됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|` 요금_ fare_product_id`| 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 단순 요금 상품(1회 탑승 $2.75 USD)을 나타냅니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id _제품_ID | fare_product_name _이름 | amount | currency | 
 |------|-------|---|---| 
 | 싱글라이드 | 편도 요금 | 2.75 | USD | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id _제품_ID | 
 |------| 
 | 싱글라이드 | 
 
 
## 요금 미디어 
 
 요금 미디어는 요금 상품을 보관 및/또는 확인하는 데 사용할 수 있는 지원 미디어를 정의합니다. 이는 종이 티켓, 충전식 교통카드, 심지어 신용카드나 스마트폰을 이용한 비접촉 결제와 같은 물리적 또는 가상 용기를 의미합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|` 요금_ fare_media_id`| 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 샌프란시스코 베이 지역의 다양한 요금 미디어의 일부를 보여줍니다. `Clipper`는 `fare_media_type=2`인 실제 교통 카드로 설명됩니다. ’SFMTA Munimobile’은 ’ fare_media_type=2’인 모바일 앱으로 설명됩니다. 티켓 없이 기사에게 직접 주는 ’현금’은 ’요금 _fare_media_type=0’입니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>요금_미디어 .txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------|-----------------| 
 | 클리퍼 | 클리퍼 | 2 | 
 | 무니모빌 | SFMTA 무니모바일 | 4 | 
 | 현금 | 현금 | 0 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id _제품_ID | fare_product_name _이름 | amount | currency | fare_media_id | 
 |------|-------|---|---|---| 
 | 싱글라이드 | 편도 요금 | 2.75 | USD | 무니모빌 | 
 
 
 
 
## 노선 기반 요금 
 
 노선 기반 요금은 급행 서비스에 대한 특별 요금이나 급행 버스 간의 요금 차별화와 같이 특정 routes 그룹에 대해 서로 다른 요금을 할당하는 데 사용됩니다. 대중교통 서비스와 기존 버스 서비스 비교. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [요금 제품 기능](#fare-products) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 routes 특급 및 지역 카테고리로 분류하는 시스템을 보여주며, 각각은 고유한 요금 상품과 연결되어 있습니다.</p> 
 
<p style="font-size:16px"> **`networks.txt` + `route_networks.txt`** 사용</p> 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#networkstxt"><b>네트워크 .txt</b></a><br> 
</p> 
 
 | network_id | network_name | 
 |------------|----| 
 | 익스프레스 | 익스프레스 | 
 | 지역 | 지역 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#route_networkstxt"><b>Route_networks.txt</b></a><br> 
</p> 
 
 | network_id | route_id | 
 |------------|------------| 
 | 익스프레스 | express_a | 
 | 익스프레스 | 익스프레스_b | 
 | 지역 | 로컬_1 | 
 | 지역 | 로컬_2 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id _제품_ID | 
 |------------|----| 
 | 익스프레스 | express_single_ride | 
 | 지역 | local_single_ride | 
 
<p style="font-size:16px"> **또는 `routes.networks_id` 사용**</p> 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | express_a | 익스프레스 | 
 | 익스프레스_b | 익스프레스 | 
 | 로컬_1 | 지역 | 
 | 로컬_2 | 지역 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id _제품_ID | 
 |------------|----| 
 | 익스프레스 | express_single_ride | 
 | 지역 | local_single_ride | 
 
 
## 시간 기반 요금 
 
 시간 기반 요금은 성수기 및 비수기 요금과 같은 특정 시간대 또는 요일에 대한 요금을 할당하는 데 사용됩니다. 주말요금. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id_ 제품_id `, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [요금 상품 기능](../fares/#fare-products) 
 
 ?? ? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 피크시간이 8시부터 10시까지이고 나머지 시간은 비피크인 시스템을 나타냅니다.</p> 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#timeframestxt"><b>기간 .txt</b></a><br> 
</p> 
 
 | timeframe_group_id | start_time | end_time | service_id | 
 |---------|------------|----------|------------| 
 | 피크 | 8:00:00 | 10:00:00 | 하루종일 | 
 | 일반 | 0:00:00 | 08:00:00 | 하루종일 | 
 | 일반 | 10:00:00 | 24:00:00 | 하루종일 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id _제품_ID | 
 |------------|-------| 
 | 피크 | peak_single_ride | 
 | 일반 | Regular_single_ride | 
 
 
## 구역 기반 요금 
 
 구역 기반 요금은 특정 구역에서 다른 구역으로 여행할 때 특정 요금이 적용되는 구역 기반 시스템을 나타내는 데 사용됩니다. 구역은 stops 그룹으로 정의됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id_ 제품_id `, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id,`area_name| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [요금 상품 기능](../fares/#fare-products) 
 
 ?? ? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 A 구역에서 B 구역까지의 요금을 보여줍니다.</p> 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id | area_name | 
 |---------|------------| 
 | zone_a | 구역 A | 
 | zone_b | B 구역 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id | stop_id | 
 |---------|---------| 
 | zone_a | stop_a | 
 | zone_a | stop_b | 
 | zone_b | stop_c | 
 | zone_b | stop_d | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id _제품_ID | 
 |---------------|------------|----| 
 | zone_a | zone_b | zone_a_b_single | 
 
## 요금 환승 
 
 요금 환승은 구간(또는 개별 여행 구간) 간 환승 시 적용 가능한 규칙을 정의하는 데 사용됩니다. 이를 통해 특정 시간 제한 동안의 무료 transfers 과 같은 특별 환승 정책을 고려하거나 이미 여행한 구간을 기준으로 요금 할인을 적용하여 다구간 여행 여행의 총 비용을 모델링할 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id`, `transfer_count`, `duration_limit`, `duration_limit_type`, `fare_transfer_type`, `fare_product_id`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [요금 상품 기능](../fares/#fare-products) 
 
 ?? ? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 2시간 이내에 시스템 내 Leg A 간에 무제한 무료 transfers 허용됨을 보여줍니다.</p> 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |---------------| 
 | | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id _제품_ID | 
 |------|------|----------------|---|---------|--------------------|-----------------| 
 | | |-1 | 7200 | 1 | 0 | free_transfer | 
 
 
## Fares v1 
 
 Fares v1은 위에 설명된 다른 Fares 기능에 대한 기존 대안입니다. ` fare_rules.txt` 및 `fare_attributes.txt ` 파일을 사용하여 운임 가격 책정, 결제 방법 transfers 및 구역 기반 운임과 같은 기본 운임 정보를 모델링할 수 있습니다. 생성하기는 더 간단하지만 더 복잡한 요금 구조를 모델링하거나 성능이 떨어지며 다른 Fare 기능(Fares v2라고 하는 기능의 일부)에 대한 충분한 승인으로 더 이상 사용되지 않을 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 선불 카드를 사용하여 네트워크 여행에 $3.20 CAD 가 소요되며 2시간 이내에 무료 transfers 가능함을 보여줍니다.</p> 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 | fare_id | price | currency_type | payment_method | transfers | transfer_duration | 
 |------|-------|---------------|----------------|------------|------| 
 | 선불카드요금 | 3.2 | CAD | 1 | | 7200 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 | fare_id | route_id | origin_id | destination_id | 
 |------|----------|----|-----------------| 
 | 선불카드요금 | 1호선 | 지하철 역 | 지하철 역 | 
 | 선불카드요금 | 2호선 | 지하철 역 | 지하철 역 | 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|------------|------------|------------|-----------------| 
 | A | 정지A | 43.670049 |-79.385389 | 지하철 역 | 
 | 비 | 정지B | 43.671049 |-79.386789 | 지하철 역 | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|------------|------------|------------|-----------------| 
 | A | 정지A | 43.670049 |-79.385389 | 지하철 역 | 
 | 비 | 정지B | 43.671049 |-79.386789 | 지하철 역 | 
 
 

