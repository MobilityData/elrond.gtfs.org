# GTFS 피드의 품질을 평가합니다. 
 
 고품질 GTFS 완전하고 정확하며 최신 상태입니다. 이는 현재 서비스가 어떻게 운영되고 있는지를 나타내고, 최대한 많은 정보를 제공한다는 의미입니다. 
 
## 전체 데이터 
 
 품질 GTFS 에는 휴일 및 여름 일정 변경, 정확한 정류장 위치, 라이더를 위한 다른 자료와 일치하는 routes 및 방향 표시 이름과 같은 중요한 서비스 세부정보가 포함되어 있습니다. agency 가 공급업체와 협력하여 GTFS 제작하더라도 인쇄물, 기내 및 온라인에 제시된 정보의 일관성을 보장하는 것은 궁극적으로 agency 의 몫입니다. 
 
## 정확한 데이터 
 
 대중교통 탑승자에게 안정적이고 사용자 친화적인 교통 경험을 제공하려면 정확한 데이터가 필수적입니다. 데이터 오류로 인해 데이터 세트의 일부 또는 전체가 사용되지 않을 수 있습니다. 
 
## 최신 데이터 
 
 오래된 데이터는 사용 가능한 피드가 없는 것보다 더 문제가 될 수 있습니다. 단순히 정보를 게시하는 것만으로는 충분하지 않습니다. 라이더가 보고 경험하는 것과 일치해야 합니다. 일부 대규모 대중교통 기관에서는 GTFS 매주 또는 매일 업데이트하지만 대부분의 기관에서는 서비스가 변경되면 몇 달에 한 번씩 또는 1년에 몇 번씩 GTFS 업데이트해야 합니다. 여기에는 새로운 routes 나 stops, 시간표 변경, 요금 체계 업데이트 등이 포함됩니다. 
 
 많은 대행사가 공급업체를 고용하여 GTFS 생성하고 관리합니다. 일부 공급업체는 서비스 변경 사항에 대해 적극적으로 질문할 수 있지만, 기관이 향후 서비스 변경 사항에 대해 공급업체와 소통하는 것이 중요합니다. 서비스 변경 사항이 포함된 GTFS 미리 게시하여 대행사, 공급업체, 여행 계획자, 승객 등 모든 사람이 원활하게 전환할 수 있도록 할 수 있습니다. 
 
## 공식 검사기 사용 
 
 공식 GTFS 검사기는 공식 사양에 따라 데이터세트의 품질을 평가하여 고품질 데이터세트를 구성하는 요소에 대한 업계 내 공통의 이해를 보장합니다. 
 
 [MobilityData](https://mobilitydata.org/)에서 관리하는 무료 오픈소스 [표준 GTFS Schedule 검사기](https://gtfs-validator.mobilitydata.org/)[^1]는 다음을 보장합니다. 귀하의 GTFS 데이터는 공식 [GTFS Schedule 참조](../../documentation/schedule/reference/) 및 [권장사항](../../documentation/schedule/schedule_best_practices)을 준수합니다. 이는 다른 당사자와 공유할 수 있는 사용하기 쉬운 보고서 및 포괄적인 문서를 제공합니다. 
 
<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li> <a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a> 로 이동합니다.</li> 
<li> GTFS 데이터세트 로드: ZIP 파일을 선택하거나 드래그 앤 드롭하거나 URL 을 복사하여 붙여넣을 수 있습니다.</li> 
<li> 유효성 검사가 완료되면 보고서를 열 수 있는 옵션이 제공됩니다.</li> 
<li> 유효성 검사기가 데이터에서 문제를 발견했는지 확인하고 문제 해결 방법에 대한 문서 링크를 확인할 수 있습니다. 검증 보고서의 URL 30일 동안 작동하며 다른 사람과 공유할 수 있습니다.</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 마찬가지로 무료 오픈소스 정식 [GTFS Realtime Validator](https://github.com/MobilityData/gtfs-realtime-validator)를 사용하면 GTFS 데이터가 공식 [GTFS Realtime Reference]를 준수하는지 확인할 수 있습니다. (../../documentation/realtime/reference/) 및 [모범 사례](../../documentation/realtime/realtime_best_practices). 
 
 고품질 데이터 생성에 대한 자세한 내용은 [캘리포니아 대중교통 데이터 가이드라인](https://dot.ca.gov/cal-itp/california-transit-data-guidelines), [GTFS Schedule 모범 사례](../../documentation/schedule/schedule_best_practices) 및 [GTFS Realtime 권장사항](../../documentation/realtime/realtime_best_practices). 
 
 [^1]: 데이터 파이프라인에서 이 도구를 사용하는 방법에 대한 자세한 지침을 확인하고 이 프로젝트에 기여하려면 [GitHub 저장소](https://github.com/MobilityData/gtfs-validator)를 방문하세요. ). 
 

