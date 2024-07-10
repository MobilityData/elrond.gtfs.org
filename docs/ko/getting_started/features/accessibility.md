# 접근성 
 접근성 기능은 장애인이 서비스에 접근하는 데 필요한 정보를 제공하기 위한 것입니다. 
 
## 휠체어 접근 중지 
 
 휠체어 접근 중지는 지정된 위치에서 휠체어 탑승이 가능한지 여부를 나타냅니다. 휠체어를 사용하는 승객에게 서비스를 제공하려면 휠체어 탑승이 가능하다고 명시하는 것이 그렇지 t 명시하는 것만큼 중요합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [위치 유형](../base_add-ons/#location-types) 입구/출구 또는 탑승 구역과 같은 역 위치. 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 `wheelchair_boarding=1`을 사용하여 `TAS001` 정류장에서 휠체어 탑승이 가능함을 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|------------|------------|---------------|---------| 
 | TAS001 | 5 Av/53 스트리트 | 40.760167 |-73.975224 | | 1 | 
 
 
## Trips 휠체어 접근성 
 
 Trips 휠체어 접근성을 통해 vehicle 휠체어를 사용하는 승객이 탑승할 수 있는지 여부를 표시할 수 있습니다. 휠체어를 사용하는 승객에게 서비스를 제공하려면 vehicle 휠체어를 사용하는 승객을 수용할 수 있다고 지정하는 것이 vehicle 이 휠체어를 사용하는 승객을 수용할 수 t 지정하는 것만큼 중요합니다. 승객이 지정된 정류장에서 여행에 접근할 수 있으려면 정류장과 여행 모두 휠체어로 접근할 수 있어야 합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible `| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 ’ AWE1 ’ 여행에 사용된 vehicle 휠체어 1대 이상을 수용할 수 있는 장비가 갖춰져 있고, ’ AWE2 ’ 여행에 사용된 vehicle 에는 그렇지 않음을 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | wheelchair_accessible | 
 |----------|------------|---------|-----------------------| 
 | 라 | 우리 | AWE1 | 1 | 
 | 라 | 우리 | AWE2 | 2 | 
 
 
## 텍스트 음성 변환 
 
 텍스트 음성 변환은 텍스트를 오디오로 변환하는 데 필요한 입력을 제공하고 보조 기술을 사용하여 텍스트를 소리내어 읽는 라이더가 올바른 정류장 이름을 얻을 수 있도록 보장합니다. 대중교통 이용시. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 읽기 가능한 버전의 정류장 이름을 제공하므로 텍스트 음성 변환 도구를 통해 이름을 소리내어 읽을 수 있습니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|------------|-------------|-------------|---------------| 
 | TAS001 | 5 Av/53 스트리트 | 45.5035680 |-73.587079 | 5번가 및 53번가 | 
 

