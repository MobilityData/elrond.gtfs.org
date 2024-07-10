# GTFS : 대중교통 데이터를 누구나 액세스할 수 있도록 만들기 
 
## 대중교통 승객 정보에 대한 개방형 데이터 표준 
 
 GTFS 라고도 알려진 General Transit Feed Specification 대중교통의 구조를 제공하는 표준화된 데이터 형식입니다. 기관은 일정, stops, 요금 등과 같은 서비스 세부 사항을 설명합니다. 
 
 이를 통해 대중 교통 기관은 다양한 소프트웨어 응용 프로그램에서 사용할 수 있는 형식으로 대중 교통 데이터를 게시할 수 있습니다. 기획자. 이는 사용자가 스마트폰이나 유사한 장치를 사용하여 대중교통 서비스에 액세스하기 위한 여행 정보를 쉽게 얻을 수 있음을 의미합니다. 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 현재 GTFS 전 세계 수천 개의 대중교통 제공업체가 선호하는 [개방형 표준](https://www.interoperablemobility.org/definitions/#open_standard)입니다. 일부 기관에서는 이 데이터를 직접 생성하고 다른 기관에서는 공급업체를 고용하여 데이터를 생성하고 유지 관리합니다. 
 
## 정적 및 동적 데이터 지원 
 
 GTFS [GTFS Schedule](../../documentation/schedule/reference) 및 [GTFS Realtime](../../문서/실시간/참조). 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 GTFS Schedule 다양한 기능 중에서 routes, 일정, 요금, 지리적 대중교통 세부정보에 대한 정보가 포함되어 있으며 간단한 텍스트 파일로 표시됩니다[^1]. 이 간단한 형식을 사용하면 복잡하거나 독점 소프트웨어에 의존하지 않고도 쉽게 생성하고 유지 관리할 수 있습니다. 
 
 GTFS Realtime [프로토콜 버퍼](https://developers.google.com/protocol-buffers/) 형식을 사용하여 이동 업데이트, vehicle 위치, 서비스 알림이 포함됩니다. GTFS 의 이 부분은 승객에게 서비스 중단 및 업데이트된 arrival 시간을 알리기 위해 GTFS Schedule 과 함께 작동합니다. 
 
 GTFS Schedule 및 GTFS Realtime 참조 문서는 [기술 문서 섹션](../../documentation/overview)에서 확인할 수 있습니다. 
 
 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="유튜브 비디오 플레이어" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Freepik의 아이콘">Freepik에서 만든 아이콘 - Flaticon</a> 
 
 [^1]: 이제 텍스트 파일 외에도 [GeoJSON](https://geojson.org/) 형식도 GTFS 에서 지원되어 특정 요소를 나타냅니다. 수요 대응 서비스. 
 

