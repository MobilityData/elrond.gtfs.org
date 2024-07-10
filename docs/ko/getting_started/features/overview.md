# GTFS Schedule 기능 
 
 대중교통 시스템의 현재 요구사항을 충족하기 위해 GTFS 참조 형식이 발전함에 따라 해당 기능은 점점 더 복잡해질 수 있습니다. ** GTFS 기능**은 GTFS 참조 형식으로 지원되는 기능에 대한 명확하고 명확한 설명을 제공하기 위한 것입니다. 이는 대중교통 기관, 공급업체, 소비자 및 연구원이 GTFS 의 기능을 이해하고 다음 질문에 답하는 데 도움이 됩니다. ** GTFS 로 무엇을 할 수 있습니까?** 
 
 다음 기능 그룹은 각 기능의 목적과 파일 및 이와 관련된 필드를 제공하여 사용자가 특정 기능을 지원하는 데 필요한 데이터를 이해하는 데 도움을 줍니다. 
 
## 기본 
 이러한 필수 기능은 GTFS 피드의 핵심을 형성합니다. 대중교통 서비스를 표현하는 데 필요한 최소한의 요소입니다. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 대중교통 서비스를 담당하는 기관에 대한 세부정보를 전달합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Stops__ 
 
 정의 대중교통 서비스가 승객을 태우고 내리는 위치. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Routes__ 
 
 정의 이름 및 서비스 유형과 같은 대중교통 경로의 요소입니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __서비스 날짜__ 
 
 여행 및 서비스 면제 일정을 계획하는 구조를 만듭니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __여행__ 
 § § 예정된 시간에 정의된 경로를 따라 이동하는 대중교통 차량을 나타냅니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __정차 시간__ 
 
 각 정류장에 대한 각 여행의 arrival 및 departure 시간을 정의합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base/#stop-times) 
 
</div> 
 
## 기본 추가 기능 
 이러한 기능은 GTFS 데이터 세트를 향상시켜 탑승자 경험을 개선하고 대행사, 공급업체 및 데이터 재사용자 간의 협업을 촉진합니다. 기존 파일에 새 필드를 추가하거나 새 파일을 만드는 작업이 포함될 수 있습니다. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __피드 정보__ 
 
 피드 자체에 대한 중요한 정보를 전달합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ § § 
 여행 중 vehicle 이 따르는 지리적 경로를 정의합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __경로 색상__ 
 
 특정 routes 에 할당된 색상 구성표를 정확하게 묘사하고 전달합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __자전거 허용__ 
 
 차량에 자전거를 수용할 수 있는지 여부를 알립니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 여행 목적지를 나타내는 차량에 사용되는 표지판을 전달합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __위치 유형__ 
 
 출입구 등 환승역 내 주요 구역을 분류합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frequency__ § § 
 정기적인 빈도 또는 특정 운행 간격으로 운영되는 서비스를 나타냅니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#주파수-기반-서비스) 
 
 - :material-subway-variant:{ .lg.middle } __환승__ 
 
 서로 다른 대중교통 서비스 간에 허용되는 transfers 설명합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __번역__ 
 § § 서비스 정보를 여러 언어로 전달합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __속성__ 
 § § 데이터 세트 생성에 참여한 사람을 알립니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../base_add-ons/# attributions) 
 
</div> 
 
 
## 접근성 
 접근성 기능은 장애인이 서비스에 접근하는 데 필수적인 정보를 제공합니다. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __휠체어 접근성 중지__ 
 
 해당 위치에서 휠체어 탑승이 가능한지 여부를 나타냅니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __여행 휠체어 접근성__ 
 
 vehicle 휠체어를 사용하는 승객을 수용할 수 있는지 여부를 나타냅니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Text- to-Speech__ 
 
 정류장 이름의 텍스트를 오디오로 변환하는 데 필요한 입력을 제공합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../accessibility/#text-to-speech) 
 
</div> 
 
 
## 요금 
 GTFS 구역, 거리, 시간대별 요금 등 다양한 요금 구조를 모델링할 수 있습니다. 승객에게 여행 가격과 결제 방법을 알려줍니다. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Fare Products__ 
 
 사용자가 사용할 수 있는 티켓 또는 요금 유형 목록을 정의합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ 
 
 요금 상품을 보관 및/또는 검증하는 데 사용할 수 있는 미디어를 정의합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __노선 기반 요금__ 
 
 특정 routes 그룹에 대해 서로 다른 요금을 적용하는 데 사용되는 규칙을 설명합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Time- 기준운임__ 
 
 시간대별, 요일별 요금차이를 설명합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone- 기본 요금__ 
 
 한 지역에서 다른 지역으로 여행할 때 차별화된 요금을 설명합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __요금 환승__ 
 
 여행의 한 구간에서 다른 구간으로 이동할 때 적용되는 수수료를 정의합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 요금 정보를 더 간단하게 표시할 수 있는 레거시 기능입니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../fares/#fares-v1) 
 
</div> 
 
 
## 통로 
 
 통로 기능을 사용하면 대형 환승역을 모델링하여 탑승자를 입구에서 탑승 구역까지 안내할 수 있습니다. 경로 세부 정보, 예상 탐색 시간 및 길 찾기 시스템을 제공합니다. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __경로 연결__ 
 
 대중교통 역 내 관련 지점을 연결하는 경로 모델링. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __경로 세부정보__ 
 
 경로의 물리적 특성에 관한 추가 세부 정보를 제공합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __레벨__ 
 § § 대중교통 역 내의 다양한 층을 모두 설명하고 나열하십시오. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __역 내 이동 시간__ § § 
 대중교통 역 내 경로 탐색에 소요되는 예상 시간을 알려줍니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __통로 표지판__ 
 
 통로와 관련된 역 내 표지판을 전달합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../pathways/#pathway-signs) 
 
</div> 
 
## 유연한 서비스 
 정규 일정이나 고정 routes 따르지 않는 유연한 서비스 또는 수요 대응 서비스. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __연속 정차__ 
 
 stops 사이에서 사용자를 태우거나 내릴 수 있는지 여부를 나타냅니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __예약 규칙__ 
 
 사용자가 수요 대응 서비스로 여행을 예약할 수 있는지 여부를 표시합니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __편차가 있는 사전 정의된 경로__ 
 
 승하차를 위해 경로를 잠시 이탈할 수 있는 차량. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../flexible_services/#predefine-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __구역 기반 수요 대응 서비스__ 
 
 특정 지역 내 어느 위치에서나 승하차가 가능한 서비스입니다. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../flexible_services/#zone-based-demand-Response-services) 
 
 - :material-subway-variant:{ .lg. 중간 } __고정 정류장 수요 대응 서비스__ 
 
 stops 그룹 내의 모든 위치에서 승하차를 허용하는 서비스. 
 
 [:octicons-arrow-right-24: 자세히 알아보기](../flexible_services/#fixed-stops-demand-Response-services) 
 
</div> 
 

