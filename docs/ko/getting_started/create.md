# GTFS 데이터세트 만들기 
 
## GTFS 피드 개요 
 모든 GTFS 피드는 .txt 파일 확장자[^1]로 저장된 일련의 CSV 파일인 GTFS 참조 형식의 데이터세트로 시작합니다. 가장 기본적인 구현에서 GTFS 데이터세트는 일반적으로 7개의 기본 파일로 시작하여 안정적인 공개 URL 에서 호스팅되는 .zip 파일로 결합됩니다. 이것이 바로 GTFS 피드입니다. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_001.png"> 
 
 각 파일은 여러 정보 필드가 있는 여러 레코드(데이터 라인) 목록으로 구성됩니다. 예를 들어 [routes.txt](../../documentation/schedule/reference/#routestxt)에 나열된 각 줄은 대중 교통 경로를 나타내며 해당 필드는 이름, 설명, 운영과 같은 해당 경로의 여러 요소를 설명합니다. agency 등 
 
<img class="center" width="560" height="100%" src="../../../assets/create_002.png"> 
 
 GTFS 데이터세트의 기본 파일은 다음과 같이 설명할 수 있습니다. GTFS 일정 데이터세트에는 하나 이상의 routes ([routes.txt](../../documentation/schedule/reference/#routestxt))가 있습니다. 각 경로에는 하나 이상의 이동([trips.txt](../../documentation/schedule/reference/#tripstxt))이 있고 각 이동은 일련의 stops ([stops.txt](../..)을 방문합니다./documentation/schedule/reference/#stopstxt)) 지정된 시간에([stop_times.txt](../../documentation/schedule/reference/#stop_timestxt)). 이동 및 정차 시간에는 시간 정보만 포함됩니다. 달력은 특정 여행이 실행되는 날짜를 결정하는 데 사용됩니다([calendar.txt](../../documentation/schedule/reference/#calendartxt) 및 [calendar_dates.txt](../../documentation/일정/참조/#calendar_datestxt)). 또한 여러 기관([agency.txt](../../documentation/schedule/reference/#agencytxt))이 여러 routes 운영할 수 있습니다. 이러한 파일은 상호 참조되는 필드를 통해 서로 연결됩니다. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_003.png"> 
 
 기본 GTFS 데이터 세트를 생성하기 위해 이러한 파일을 설정한 후에는 추가(optional) 파일을 추가하여 대중교통 기관과 공급업체 간의 다른 기능이나 특정 요구 사항을 활성화할 수 있습니다. 이러한 파일의 몇 가지 예는 다음과 같습니다: 
 
 - [shapes.txt](../../documentation/schedule/reference/#shapestxt) - 여행 경로를 그래픽으로 나타낼 수 있음, 
 - [pathways.txt](../../documentation/schedule/reference/#pathwaystxt) 사용자가 스테이션을 탐색하는 데 도움이 되는 길찾기를 생성할 수 있는 정보를 제공합니다. 
 - [frequencies.txt](../../documentation/schedule/reference/#frequencytxt)는 정지 시간을 지정하는 대체 방법을 제공합니다. 
 
 활성화할 수 있는 모든 GTFS 기능에 대한 자세한 내용은 [’ GTFS 기능은 무엇인가요?’](../features/overview/) 섹션을 참조하세요. 
 
 GTFS Schedule 데이터세트는 vehicle 위치 및 서비스 업데이트와 같은 실시간 정보로 보완될 수 있습니다. 이렇게 하려면 기존 GTFS Schedule 데이터세트와 별도로 GTFS Realtime 피드를 생성해야 합니다. 
 
 GTFS Realtime 피드는 HTTP를 통해 제공되고 자주 업데이트되는 일반 바이너리 파일로 구성되며, 모든 유형의 웹서버에서 파일을 호스팅하고 제공할 수 있습니다. GTFS Realtime 데이터 교환 형식은 구조화된 데이터를 직렬화하기 위한 언어 및 플랫폼 중립 메커니즘인 [프로토콜 버퍼](https://developers.google.com/protocol-buffers/)를 기반으로 합니다. GTFS Realtime 이동 업데이트, 서비스 알림, 차량 위치 등 세 가지 유형의 정보를 제공할 수 있으며, 이러한 정보는 전달해야 하는 서비스 정보에 따라 결합될 수 있습니다. 
 
 GTFS Realtime 사용하면 차량의 실제 상태를 표시할 수 있으므로 피드를 정기적으로 업데이트해야 합니다. 서비스의 자동 차량 위치 시스템에서 새 데이터가 들어올 때마다 업데이트하는 것이 좋습니다. GTFS Schedule 데이터세트와 GTFS Realtime 피드를 결합하면 애플리케이션을 사용하여 라이더에게 정확한 최신 정보를 제공할 수 있습니다. 자세한 내용은 기술 문서를 참조하세요. 
 
## 첫 GTFS 피드를 제작하시나요? 
 
 첫 번째 GTFS 피드를 제작하려는 agency 인 경우 가장 먼저 해야 할 일은 기존 문서를 읽는 것입니다. 
 
 [’ GTFS 무엇을 할 수 있나요?’](../features/overview) 섹션에서 GTFS 의 기능을 살펴보고 GTFS 형식을 사용하여 표현하려는 대중교통 서비스의 다양한 기능을 결정하는 것부터 시작하세요. 더 자세히 알아보려면 [GTFS Schedule](../../documentation/schedule/reference) 및 [GTFS Realtime](../../documentation/realtime/reference) 공식 참조 문서에서 자세한 내용을 확인하세요. 이러한 기능을 모델링하고 규정 준수를 보장하는 방법에 대한 지침입니다. 
 
 다음으로 시스템에서 필요한 모든 데이터를 수집합니다. 여기에는 모든 stops, routes, 시간표, 요금 등에 대한 정보가 포함됩니다. 이러한 세부정보 중 상당수는 GTFS 데이터세트를 채우는 입력이 됩니다. 
 
 시스템의 크기와 복잡성에 따라 내부에서 데이터를 생성하거나 외부 GTFS 공급업체를 통해 데이터를 GTFS 형식으로 변환할 수 있습니다. 
 
 경우에 따라 소수의 routes 가진 소규모 기관이 스프레드시트 및 텍스트 편집기와 같이 일반적으로 사용 가능한 소프트웨어를 사용하여 데이터를 직접 생성합니다. 
 
 더 큰 시스템 범위를 다룰 때 대부분의 기관은 전문 공급업체로부터 특수 GTFS 관리 소프트웨어를 구입하지만 일부 기관은 자체 내부 도구를 개발하기로 선택할 수도 있습니다. 마지막으로, 시스템 특성상 기관이 자체적으로 데이터세트를 작성하기 어려운 것으로 판명되면 GTFS 생산을 GTFS 데이터 생산 전문 회사에 전적으로 아웃소싱할 수 있습니다. 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Freepik의 아이콘">Freepik에서 만든 아이콘 - Flaticon</a> 
 
 [^1]: 이제 텍스트 파일 외에도 [GeoJSON](https://geojson.org/) 형식도 GTFS 에서 지원되어 특정 요소를 나타냅니다. 수요 대응 서비스. 
 

