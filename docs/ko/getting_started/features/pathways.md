# 통로 
 통로 기능은 대규모 대중교통 역을 모델링하여 승객을 역 입구에서 안내하고 승객이 대중교통 vehicle 에 탑승하거나 내리는 위치까지 존재합니다. 이러한 기능 중 일부는 경로의 물리적 특성과 예상 탐색 시간, 그리고 역에 사용되는 실제 길 찾기 시스템을 전달하는 것을 가능하게 합니다. 
 
## Pathway 연결 
 
 기본 수준에서 Pathways는 스테이션 내의 위치 유형에 정의된 주요 영역을 연결하는 기본 기능을 제공합니다. 이러한 연결은 pathways 형성하여 사용자가 정확한 방향(예: 탑승 구역 입구에서)을 얻을 수 있도록 하며, 이는 크고 복잡한 대중교통 역을 탐색하는 데 특히 유용합니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`pathway_id`, `from_stop_id`, `to_stop_id`, `pathway_mode`, `is_bidirectional ` | 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [위치 유형](../base_add-ons/#location-types) 
 
 ? ?? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 미리 설정된 위치( stops 으로 정의됨) 사이의 여러 연결( pathways 라고도 함)을 정의합니다: 통로(` pathway_mode=1), 계단(`pathway_mode=2) 및 개찰구(`pathway_mode=6). 양방향성도 지정됩니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | from_stop_id | to_stop_id | pathway_mode | is_bidirectional | 
 |------------|---------------|------------|------------|------| 
 | MainSt-001 | A102_E01 | A102_S01 | 1 | 1 | 
 | MainSt-002 | A102_S01 | A102_S02 | 2 | 1 | 
 | MainSt-003 | A102_S02 | A102_F02 | 1 | 1 | 
 | MainSt-004 | A102_F02 | A102_F01 | 6 | 1 | 
 | MainSt-005 | A102_F01 | A102_S03 | 1 | 1 | 
 | MainSt-006 | A102_S03 | A102_S04 | 2 | 1 | 
 | MainSt-007 | A102_F01 | A102_S05 | 1 | 1 | 
 | MainSt-008 | A102_S05 | A102_S06 | 2 | 1 | 
 | MainSt-009 | A102_S04 | A102_B01 | 1 | 1 | 
 | MainSt-010 | A102_S06 | A102_B02 | 1 | 1 | 
 
 
## 통로 세부 정보 
 
 길이, 너비, 경사(경사로의 경우) 또는 계단 수(계단의 경우)를 포함하여 역 pathways 의 물리적 특성과 관련하여 더 많은 세부 정보를 추가할 수 있습니다. 이는 라이더가 탐색해야 하는 경로의 조건과 접근성을 예측하는 데 도움이 됩니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`max_slope`, `min_width`, `length`, `stair_count`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [경로 연결](#pathway-connections) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 최소 너비, 계단의 계단 수, 통로의 길이 및 최대 경사를 포함하여 사전 설정된 pathways 에 대한 추가 세부 정보를 정의합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | max_slope | min_width | 길이 | stair_count | 
 |------------|------------|------------|---------|-------------| 
 | MainSt-001 | 0 | 4.3 | 3.6 | | 
 | MainSt-002 | | 2.2 | | 15 | 
 | MainSt-003 | 0.06 | 4 | 3.1 | | 
 | MainSt-004 | | 0.9 | 2.9 | | 
 | MainSt-005 | 0 | 3.5 | 5 | | 
 | MainSt-006 | | 2.2 | | 18 | 
 | MainSt-007 | 0 | 3.5 | 5 | | 
 | MainSt-008 | | 2.2 | | 18 | 
 | MainSt-009 | 0 | 6 | 2 | | 
 | MainSt-010 | 0 | 6 | 2 | | 
 
 
## 레벨 
 
 레벨은 스테이션 내의 모든 다른 레벨을 나열하는 데 사용될 수 있으며 사용자에게 스테이션에 대한 추가 정보 계층을 제공합니다. 이 기능을 사용하면 통로 연결 기능과 함께 엘리베이터를 사용할 수도 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[levels.txt](../../../documentation/schedule/reference/#levelstxt)|`level_id`, `level_index`, `level_name`| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`level_id`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [위치 유형](../base_add-ons/#location-types) 
 
 ? ?? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 스테이션의 다양한 레벨을 보여줍니다. 그런 다음 위치( stops 으로 정의됨)가 해당 수준에 할당됩니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | level_id | level_index | level_name | 
 |------|-------------|------------| 
 | level_0_street | 0 | 거리에서 | 
 | level_-1_lobby |-1 | 로비 | 
 | level_-2_플랫폼 |-2 | 플랫폼 | 
 
 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | stop_id | level_id | 
 |---------------|----------| 
 | 역_A102 | | 
 | A102_B01 |-2 | 
 | A102_B02 |-2 | 
 | A102_E01 | 0 | 
 | A102_S01 | 0 | 
 | A102_S02 |-1 | 
 | A102_S03 |-1 | 
 | A102_S04 |-2 | 
 | A102_S05 |-1 | 
 | A102_S06 |-2 | 
 | A102_F01 |-1 | 
 | A102_F02 |-1 | 
 
 
## 역 내 통과 시간 
 
 역 내 통과 시간은 역 내 방향에 대한 추가 세부 수준을 제공하여 사용자에게 역 탐색에 필요한 예상 시간을 제공하여 더 나은 이동 방향 및 정보를 제공합니다. 여행 시간. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`traversal_time`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [경로 연결](#pathway-connections) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 각 경로를 탐색하는 데 필요한 예상 이동 시간(초)을 보여줍니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | traversal_time | 
 |------------|---| 
 | MainSt-001 | 3 | 
 | MainSt-002 | 20 | 
 | MainSt-003 | 2 | 
 | MainSt-004 | 2 | 
 | MainSt-005 | 4 | 
 | MainSt-006 | 25 | 
 | MainSt-007 | 4 | 
 | MainSt-008 | 25 | 
 | MainSt-009 | 2 | 
 | MainSt-010 | 2 | 
 
 
## 통로 표지판 
 
 통로 표지판은 여행 계획자에 표시되는 정보를 실제 표지판과 연결할 수 있습니다. 이것이 피드에 표시되면 여행 계획자는 ’표지판을 따르세요’와 같은 안내를 제공할 수 있습니다. 
 
 | 포함된 파일 | 포함된 필드 | 
 |---------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`signposted_as`, `reversed_signposted_as`| 
 
 **전제 조건**: 
 
 - [기본 기능](../base) 
 - [경로 연결](#pathway-connections) 
 
 ??? "샘플 데이터" 참고 
 
<p style="font-size:16px"> 
 다음 샘플은 정거장의 물리적 표지판에 표시되는 텍스트를 반영하여 미리 설정된 pathways 와 관련된 내비게이션 정보를 지정합니다. 
</p> 
 !!! 메모 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | signposted_as | reversed_signposted_as | 
 |------------|------|------------------------| 
 | MainSt-001 | 로비에 | 종료 | 
 | MainSt-002 | | | 
 | MainSt-003 | 플랫폼으로 | 종료 | 
 | MainSt-004 | | | 
 | MainSt-005 | 서쪽행 열차 | 종료 | 
 | MainSt-006 | | | 
 | MainSt-007 | 동쪽행 열차 | 종료 | 
 | MainSt-008 | | | 
 | MainSt-009 | 서쪽행 열차 | 로비로 | 
 | MainSt-010 | 동쪽행 열차 | 로비로 | 
 
 

