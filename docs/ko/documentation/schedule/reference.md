## General Transit Feed Specification 참조 
 
 **2024년 5월 22일 개정됨. 자세한 내용은 [개정 내역](../change_history/revision_history)을 참조하세요.** 
 
 이 문서는 GTFS 데이터세트를 구성하는 파일입니다. 
 
## 목차 
 
 1. [문서 규칙](#document-conventions) 
 2. [데이터 세트 파일](#dataset-files) 
 3. [파일 요구 사항](#file-요구 사항) 
 4. [데이터 세트 게시 및 일반 관행](#dataset-publishing-general-practices) 
 5. [필드 정의](#field-definitions) 
 - [agency.txt](#agencytxt) 
 - [stops.txt](#stopstxt) 
 - [routes.txt](#routestxt) 
 - [trips.txt](#tripstxt) 
 - [stop\_times.txt](#stop_timestxt) 
 - [calendar.txt](#calendartxt) 
 - [calendar\_dates.txt](#calendar_datestxt) 
 - [fare\_attributes.txt](#fare_attributestxt) 
 - [fare\_rules.txt](#fare_rulestxt) 
 - [timeframes.txt](#timeframestxt) 
 - [fare\_media.txt](#fare_mediatxt) 
 - [fare\_products.txt](#fare_productstxt) 
 - [fare\ _leg\_rules.txt](#fare_leg_rulestxt) 
 - [fare\_transfer\_rules.txt](#fare_transfer_rulestxt) 
 - [areas.txt](#areastxt) 
 - [stop_areas.txt](#stop_areastxt) 
 - [네트워크 .txt](#networkstxt) 
 - [route_networks.txt](#route_networkstxt) 
 - [shapes.txt](#shapestxt) 
 - [frequencies.txt](#frequencytxt) 
 - [transfers.txt](#transferstxt) 
 - [pathways.txt](#pathwaystxt) 
 - [levels.txt](#levelstxt) 
 - [location_groups.txt](#location_groupstxt) 
 - [location_group_stops.txt](#location_group_stopstxt) 
 - [locations.geojson](#locationsgeojson) 
 - [booking_rules.txt](#booking_rulestxt) 
 - [translations.txt](#translationstxt) 
 - [피드\ _info.txt](#feed_infotxt) 
 - [attributions.txt](#attributionstxt) 
 
## 문서 규칙 
 핵심 단어 "반드시", "반드시 금지", "필수", "반드시", 이 문서의 "하면 안 된다", "해야 한다", "하면 안 된다", "권장", "할 수 있다", "선택 사항"은 [RFC 2119](https://tools.ietf.org)에 설명된 대로 해석됩니다./html/rfc2119). 
 
 
### 용어 정의 
 
 이 섹션에서는 이 문서 전체에서 사용되는 용어를 정의합니다. 
 
 * **데이터 세트** - 이 사양 참조로 정의된 전체 파일 세트입니다. 데이터 세트를 변경하면 새 버전의 데이터 세트가 생성됩니다. 데이터 세트는 zip 파일 이름을 포함하여 공개된 영구 URL 에 게시되어야 합니다. (예: agency). 
 * **레코드** - 단일 entity (예: 대중교통 agency, 정류장, 경로 등)를 설명하는 다양한 필드 값으로 구성된 기본 데이터 구조입니다. 테이블에서 행으로 표시됩니다. 
 * **필드** - 개체 또는 entity 의 속성입니다. 테이블에서는 열로 표시됩니다. 파일에 header 로 추가된 경우 해당 필드가 존재합니다. 정의된 필드 값이 있을 수도 있고 없을 수도 있습니다. 
 * **필드 값** - 필드의 개별 항목입니다. 표에서는 단일 셀로 표시됩니다. 
 * **서비스 요일** - 서비스 요일은 경로 일정을 나타내는 데 사용되는 기간입니다. 서비스 날짜의 정확한 정의는 agency agency 다르지만 서비스 날짜는 역일과 일치하지 않는 경우가 많습니다. 서비스가 특정 날짜에 시작되어 다음 날에 종료되는 경우 서비스 날짜는 24:00:00를 초과할 수 있습니다. 예를 들어, 금요일 08:00:00부터 토요일 02:00:00까지 운영되는 서비스는 단일 서비스일의 08:00:00부터 26:00:00까지 운영되는 것으로 표시될 수 있습니다. 
 * **텍스트 음성 변환 필드** - 필드에는 상위 필드(비어 있는 경우 대체)와 동일한 정보가 포함되어야 합니다. 텍스트 음성 변환으로 읽는 것이 목적이므로 약어를 제거하거나("St"는 "Street" 또는 "Saint"로 읽어야 하며 "Elizabeth I"는 "Elizabeth the First"로 읽어야 함) 또는 그대로 읽어야 합니다("JFK Airport"는 약어로 표시됨). 
 * **다리** - 라이더가 여행 중 한 쌍의 후속 위치 사이에서 승하차하는 여행입니다. 
 * **여행** - 모든 구간과 중간 transfers 포함하여 출발지에서 목적지까지의 전체 여행입니다. 
 * **하위 여행** - 여행의 하위 집합을 구성하는 두 개 이상의 구간입니다. 
 * **운임 상품** - 여행 비용을 지불하거나 여행을 확인하는 데 사용할 수 있는 구매 가능한 운임 상품입니다. 
 
### 존재 
 필드 및 파일에 적용되는 존재 조건: 
 
 * **필수** - 필드 또는 파일은 데이터 세트에 포함되어야 하며 각 레코드에 유효한 값을 포함해야 합니다. 
 * **선택 사항** - 필드 또는 파일이 데이터세트에서 생략될 수 있습니다. 
 * **조건부 필수** - 필드 또는 파일은 필드 또는 파일 설명에 설명된 조건에 따라 포함되어야 합니다. 
 * **조건부 금지** - 필드 또는 파일 설명에 설명된 조건에 따라 필드 또는 파일이 포함되어서는 안 됩니다. 
 * **권장** - 필드 또는 파일은 데이터세트에서 생략될 수 있지만 포함하는 것이 모범 사례입니다. 이 필드나 파일을 생략하기 전에 모범 사례를 주의 깊게 평가하고 생략의 전체 의미를 이해해야 합니다. 
 
### 필드 유형 
 
 - **색상** - 6자리 16진수로 인코딩된 색상입니다. 유효한 값을 생성하려면 [https://htmlcolorcodes.com](https://htmlcolorcodes.com)을 참조하세요(앞의 "#"이 포함되어서는 안 됩니다).<br> *예: 흰색은 `FFFFFF, 검정색은 `000000`, NYMTA의 A,C,E 줄은 `0039A6`.* 
 - **통화 코드** - ISO 4217 알파벳 currency 코드입니다. 현재 currency 목록은 [https://en.wikipedia.org/wiki/ISO_4217#Active\_codes](https://en.wikipedia.org/wiki/ISO_4217#Active_codes)를 참조하세요.<br> *예: 캐나다 달러의 경우 `CAD`, 유로의 경우 `EUR`, 일본 엔의 경우 `JPY`.* 
 - **통화 amount** - currency amount 나타내는 소수 값입니다. 함께 제공되는 통화 코드에 대한 소수 자릿수는 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217#Active_codes)에 의해 지정됩니다. 모든 재무 계산은 데이터를 소비하는 데 사용되는 프로그래밍 언어에 따라 소수, currency 또는 재무 계산에 적합한 다른 동등한 유형으로 처리되어야 합니다. 계산 중 금전적 이익이나 손실로 인해 통화 currency 을 float 으로 처리하는 것은 권장되지 않습니다. 
 - **날짜** - YYYYMMDD 형식의 서비스 날짜입니다. 서비스 날짜 내의 시간이 24:00:00를 초과할 수 있으므로 서비스 날짜에는 다음 날짜에 대한 정보가 포함될 수 있습니다.<br> *예: 2018년 9월 13일의 ’20180913’.* 
 - ** Email** - 이메일 주소입니다.<br> *예: `example@example.com`* 
 - **Enum** - "설명" 열에 정의된 사전 정의된 상수 세트의 옵션입니다.<br> *예: `route_type 필드에는 트램의 경우 `0`, 지하철의 경우 `1` 포함됩니다...* 
 - **ID** - ID 필드 값은 내부 ID이며 표시할 의도가 없습니다. riders이며 UTF-8 문자의 시퀀스입니다. 인쇄 가능한 ASCII 문자만 사용하는 것이 좋습니다. ID는 파일 내에서 고유해야 하는 경우 "고유 ID"로 표시됩니다. 하나의 .txt 파일에 정의된 ID는 다른 .txt 파일에서 참조되는 경우가 많습니다. 다른 테이블의 ID를 참조하는 ID에는 "외부 ID"라는 라벨이 붙습니다.<br> *예: [stops.txt](#stopstxt)의 `stop_id` 필드는 "고유 ID"입니다. [stops.txt](#stopstxt)의 ` parent_station ` 필드는 ` stops.stop_id 를 참조하는 "외부 ID"입니다.* 
 - **언어 코드** - IETF BCP 47 언어 코드입니다. IETF BCP 47에 대한 소개는 [http://www.rfc-editor.org/rfc/bcp/bcp47 .txt](http://www.rfc-editor.org/rfc/bcp/bcp47 )를 참조하세요 .txt) 및 [http://www.w3.org/International/articles/](http://www.w3.org/International/articles/언어-tags/).<br> *예: 영어의 경우 `en`, 미국 영어의 경우 `en-US`, 독일어의 경우 `de`.* 
 - **위도** - WGS84 latitude (십진수 도)입니다. 값은 -90.0보다 크거나 같고 90.0보다 작거나 같아야 합니다. *<br> 예: 로마 콜로세움의 경우 `41.890169`.* 
 - **경도** - 소수점 단위의 WGS84 longitude 입니다. 값은 -180.0보다 크거나 같고 180.0보다 작거나 같아야 합니다.<br> *예: 로마 콜로세움의 경우 `12.492269`.* 
 - ** Float** - 부동 소수점 숫자입니다. 
 - **정수** - 정수입니다. 
 - ** Phone number** - 전화번호. 
 - **시간** - HH:MM:SS 형식의 시간입니다(H:MM:SS도 허용됨). 시간은 서비스일의 "정오 - 12시"부터 측정됩니다(일광 절약 시간이 변경되는 날을 제외하고 사실상 자정). 운행일 자정 이후의 시간은 HH:MM:SS 형식으로 24:00:00보다 큰 값으로 입력합니다.<br> *예: 오후 2시 30분은 ’14:30:00’, 다음날 오전 1시 35분은 ’25:35:00’.* 
 - ** Text** - UTF-8 문자로 구성된 string 입니다. 표시되는 것이 목적이므로 사람이 읽을 수 있어야 합니다. 
 - **시간대** - [https://www.iana.org/time-zones](https://www.iana.org/time-zones)의 TZ 시간대입니다. 시간대 이름에는 공백 문자가 포함되지 않지만 밑줄은 포함될 수 있습니다. 유효한 값 목록은 [http://en.wikipedia.org/wiki/List\_of\_tz\_zones](http://en.wikipedia.org/wiki/List\_of\_tz\_zones)를 참조하세요..<br> *예: `Asia/Tokyo`, `America/Los_Angeles` 또는 `Africa/Cairo`.* 
 - ** URL** - http://또는 https://및 특수 문자를 포함하는 정규화된 URL URL 의 문자는 올바르게 이스케이프되어야 합니다. 자세한 내용은 다음 [http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html](http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html)을 참조하세요. 정규화된 URL 값을 만드는 방법에 대한 설명입니다. 
 
### 필드 기호 
 Float 또는 정수 필드 유형에 적용 가능한 기호: 
 
 * **음수가 아님** - 0보다 크거나 같음. 
 * **0이 아님** - 0과 같지 않음. 
 * **양수** - 0보다 큼. 
 
 _예: **음수가 아닌 부동 float** - 0보다 크거나 같은 부동 소수점 숫자._ 
 
### 데이터 세트 속성 
 데이터 세트의 **기본 키**는 행을 고유하게 식별하는 필드 또는 필드 조합입니다. `Primary key (*)`는 파일에 제공된 모든 필드가 행을 고유하게 식별하는 데 사용될 때 사용됩니다. `Primary key (none)`는 파일이 하나의 행만 허용한다는 의미입니다. 
 
 _예: `trip_id` 및 `stop_sequence` 필드는 [stop_times.txt](#stop_timestxt)의 기본 키를 만듭니다._ 
 
## 데이터 세트 파일 
 
 이 사양은 다음 파일을 정의합니다. 
 
 | 파일 이름 | 존재 | 설명 | 
 |------|------|------| 
 | [agency.txt](#agencytxt) | **필수** | 이 데이터세트에 표시된 서비스를 제공하는 대중교통 기관입니다. | 
 | [stops.txt](#stopstxt) | **필수** | 차량이 승객을 태우거나 내려주는 정류장입니다. 또한 역과 역 입구를 정의합니다. | 
 | [routes.txt](#routestxt) | **필수** | 대중교통 routes 경로는 라이더에게 단일 서비스로 표시되는 이동 그룹입니다. | 
 | [trips.txt](#tripstxt) | **필수** | 각 경로의 여행. 여행은 특정 기간 동안 발생하는 두 개 이상의 stops 의 연속입니다. | 
 | [stop_times.txt](#stop_timestxt) | **필수** | 각 이동 시 vehicle stops 에 도착하고 출발하는 시간입니다. | 
 | [calendar.txt](#calendartxt) | **조건부 필수** | 시작 날짜와 종료 날짜가 포함된 주간 일정을 사용하여 지정된 서비스 날짜입니다.<br><br> 조건부 필수:<br> - 모든 서비스 날짜가 [calendar_dates.txt](#calendar_datestxt)에 정의되어 있지 않은 경우 **필수**입니다.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | [calendar_dates.txt](#calendar_datestxt) | **조건부 필수** | [calendar.txt](#calendartxt)에 정의된 서비스에 대한 예외입니다.<br><br> 조건부 필수:<br> - [calendar.txt](#calendartxt)가 생략된 경우 **필수**입니다. 이 경우 [calendar_dates.txt](#calendar_datestxt)에는 모든 서비스 날짜가 포함되어야 합니다.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | [fare_attributes.txt](#fare_attributestxt) | 선택사항 | 대중교통 기관의 routes 에 대한 요금 정보입니다. | 
 | [fare_rules.txt](#fare_rulestxt) | 선택사항 | 여정에 대한 운임을 적용하는 규정입니다. | 
 | [타임프레임 .txt](#timeframestxt) | 선택사항 | date 및 시간 요소에 따라 달라지는 운임에 대한 운임 규정에 사용할 날짜 및 시간 기간입니다. | 
 | [fare_media.txt](#fare_mediatxt) | 선택사항 | 요금 상품을 사용하기 위해 사용할 수 있는 요금 미디어를 설명합니다.<br><br> 파일 [fare_media.txt](#fare_mediatxt)는 [fare_attributes.txt](#fare_attributestxt) 및 [fare_rules.txt](#fare_rulestxt)에 표시되지 않은 개념을 설명합니다. 따라서 [fare_media.txt](#fare_mediatxt)의 사용은 [fare_attributes.txt](#fare_attributestxt) 및 [fare_rules.txt](#fare_rulestxt) 파일과 완전히 별개입니다. | 
 | [fare_products.txt](#fare_productstxt) | 선택사항 | 승객이 구매할 수 있는 다양한 유형의 티켓이나 요금을 설명합니다.<br><br> 파일 [fare_products.txt](#fare_productstxt)는 [fare_attributes.txt](#fare_attributestxt) 및 [fare_rules.txt](#fare_rulestxt)에 표시되지 않은 요금 상품을 설명합니다. 따라서 [fare_products.txt](#fare_productstxt) 사용은 [fare_attributes.txt](#fare_attributestxt) 및 [fare_rules.txt](#fare_rulestxt) 파일과 완전히 별개입니다. | 
 | [fare_leg_rules.txt](#fare_leg_rulestxt) | 선택사항 | 개별 여행 구간에 대한 운임 규정.<br><br> 파일 [fare_leg_rules.txt](#fare_leg_rulestxt)는 요금 구조를 모델링하기 위한 보다 자세한 방법을 제공합니다. 따라서 [fare_leg_rules.txt](#fare_leg_rulestxt)의 사용은 [fare_attributes.txt](#fare_attributestxt) 및 [fare_rules.txt](#fare_rulestxt) 파일과 완전히 별개입니다. | 
 | [fare_transfer_rules.txt](#fare_transfer_rulestxt) | 선택사항 | 여행 구간 간 transfers 에 대한 운임 규정입니다.<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt)와 함께 파일 [fare_transfer_rules.txt](#fare_transfer_rulestxt)는 요금 구조를 모델링하기 위한 보다 자세한 방법을 제공합니다. 따라서 [fare_transfer_rules.txt](#fare_transfer_rulestxt)의 사용은 [fare_attributes.txt](#fare_attributestxt) 및 [fare_rules.txt](#fare_rulestxt) 파일과 완전히 별개입니다. | 
 | [areas.txt](#areastxt) | 선택사항 | 위치의 영역 그룹화. | 
 | [stop_areas.txt](#stop_areastxt) | 선택사항 | 지역에 stops 할당하는 규칙입니다. | 
 | [네트워크 .txt](#networkstxt) | **조건부 금지** | routes 의 네트워크 그룹화.<br><br> 조건부 금지:<br> - `network_id`가 [routes.txt](#routestxt)에 존재하는 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | [route_networks.txt](#route_networkstxt) | **조건부 금지** | 네트워크에 routes 할당하는 규칙입니다.<br><br> 조건부 금지:<br> - `network_id`가 [routes.txt](#routestxt)에 존재하는 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | [shapes.txt](#shapestxt) | 선택사항 | vehicle 이동 경로 매핑 규칙(경로 정렬이라고도 함) | 
 | [frequencies.txt](#frequencytxt) | 선택사항 | 배차 기반 서비스의 배차(여행 간 시간) 또는 고정 일정 서비스의 압축 표현입니다. | 
 | [transfers.txt](#transferstxt) | 선택사항 | routes 간 환승 지점 연결 규칙. | 
 | [pathways.txt](#pathwaystxt) | 선택사항 | 역 내 위치를 서로 연결하는 통로입니다. | 
 | [levels.txt](#levelstxt) | **조건부 필수** | 역 내 레벨.<br><br> 조건부 필수:<br> - 엘리베이터가 있는 pathways 설명할 때 **필수**입니다(`pathway_mode=5).<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | [location_groups.txt](#location_groupstxt) | 선택사항 | 승객이 픽업 또는 하차를 요청할 수 있는 위치를 함께 나타내는 stops 그룹입니다. | 
 | [location_group_stops.txt](#location_group_stopstxt) | 선택사항 | 위치 그룹에 stops 할당하는 규칙입니다. | 
 | [locations.geojson](#locationsgeojson) | 선택사항 | GeoJSON 다각형으로 표시되는 주문형 서비스에 의한 탑승 또는 하차 요청을 위한 구역입니다. | 
 | [booking_rules.txt](#booking_rulestxt) | 선택사항 | 승객이 요청한 서비스에 대한 예약 정보입니다. | 
 | [translations.txt](#translationstxt) | 선택사항 | 고객이 접하는 데이터 세트 값의 번역입니다. | 
 | [feed_info.txt](#feed_infotxt) | 선택사항 | 게시자, 버전, 만료 정보를 포함한 데이터세트 메타데이터입니다. | 
 | [attributions.txt](#attributionstxt) | 선택사항 | 데이터세트 attributions. | 
 
## 파일 요구 사항 
 
 데이터 세트 파일의 형식과 내용에는 다음 요구 사항이 적용됩니다. 
 
 * 모든 파일은 쉼표로 구분된 텍스트로 저장되어야 합니다. 
 * 각 파일의 첫 번째 줄에는 필드 이름이 포함되어야 합니다. [필드 정의](#field-definitions) 섹션의 각 하위 섹션은 GTFS 데이터세트의 파일 중 하나에 해당하며 해당 파일에 사용될 수 있는 필드 이름을 나열합니다. 
 * 모든 파일 및 필드 이름은 대소문자를 구분합니다. 
 * 필드 값에는 탭, 캐리지 리턴 또는 새 줄이 포함되어서는 안 됩니다. 
 * 따옴표나 쉼표가 포함된 필드 값은 따옴표로 묶어야 합니다. 또한 필드 값의 각 따옴표 앞에는 따옴표가 있어야 합니다. 이는 Microsoft Excel에서 쉼표로 구분된(CSV) 파일을 출력하는 방식과 일치합니다. CSV 파일 형식에 대한 자세한 내용은 [http://tools.ietf.org/html/rfc4180](http://tools.ietf.org/html/rfc4180)을 참조하세요. 
 다음 예는 필드 값이 쉼표로 구분된 파일에 표시되는 방식을 보여줍니다. 
 * **원래 필드 값:** `"Contains "quotes", commas and text` 
 * **CSV 파일의 필드 값 :** `"Contains ""quotes"", commas and text"` 
 * 필드 값에는 HTML 태그, 주석 또는 이스케이프 시퀀스가 ​​포함되어서는 안 됩니다. 
 * 필드 또는 필드 이름 사이의 추가 공백을 제거해야 합니다. 많은 파서는 공백을 값의 일부로 간주하므로 오류가 cause 수 있습니다. 
 * 각 줄은 CRLF 또는 LF 줄바꿈 문자로 끝나야 합니다. 
 * 모든 유니코드 문자를 지원하려면 파일을 UTF-8로 인코딩해야 합니다. 유니코드 BOM(바이트 순서 표시) 문자를 포함하는 파일이 허용됩니다. BOM 문자 및 UTF-8에 대한 자세한 내용은 [http://unicode.org/faq/utf_bom.html#BOM](http://unicode.org/faq/utf_bom.html#BOM)을 참조하세요. 
 * 모든 데이터 세트 파일은 함께 압축되어야 합니다. 파일은 하위 폴더가 아닌 루트 수준에 직접 있어야 합니다. 
 * 고객이 접하는 모든 텍스트 문자열(정류장 이름, 경로 이름 및 행선지 포함)은 소문자를 표시할 수 있는 디스플레이에서 장소 이름을 대문자로 표기하는 현지 규칙에 따라 대소문자 혼합(모두 대문자 아님)을 사용해야 합니다(예: "Brighton" 처칠 광장’, ’빌리에 쉬르 마른’, ’마켓 스트리트’). 
 * 위치가 약칭(예: "JFK Airport")으로 호출되지 않는 한 이름 및 기타 텍스트(예: 거리의 경우 St.) 피드 전체에서 약어 사용을 피해야 합니다. 약어는 화면 판독기 소프트웨어 및 음성 사용자 인터페이스의 접근성에 문제가 될 수 있습니다. 소비 소프트웨어는 표시를 위해 전체 단어를 약어로 안정적으로 변환하도록 설계할 수 있지만, 약어를 전체 단어로 변환하면 오류가 발생할 위험이 더 커집니다. 
 
## 데이터 세트 게시 및 일반 관행 
 
 * 데이터 세트는 zip 파일 이름을 포함하여 영구 공개 URL 에 게시되어야 합니다. (예: agency). 이상적으로는 소프트웨어 애플리케이션을 사용하여 다운로드를 용이하게 하기 위해 파일에 액세스하기 위해 로그인하지 않고도 URL 직접 다운로드할 수 있어야 합니다. GTFS 데이터세트를 공개적으로 다운로드 가능하게 만드는 것이 가장 일반적인 관행이지만, 데이터 제공업체가 라이선스나 기타 이유로 GTFS 에 대한 액세스를 제어해야 하는 경우 API 키를 사용하여 GTFS 데이터세트에 대한 액세스를 제어하는 ​​것이 좋습니다. 자동 다운로드가 용이해집니다. 
 * GTFS 데이터는 안정적인 위치에 있는 단일 파일에 항상 대중교통 agency 서비스에 대한 최신 공식 설명이 포함되도록 반복적으로 게시되어야 합니다. 
 * 데이터 세트는 가능할 때마다 데이터 반복 전반에 걸쳐 `stop_id`, `route_id` 및 `agency_id 에 대한 영구 식별자( id 필드)를 유지해야 합니다. 
 * 하나의 GTFS 데이터세트에는 현재 및 향후 서비스(’병합’ 데이터세트라고도 함)가 포함되어야 합니다. 두 개의 서로 다른 GTFS 피드에서 병합된 데이터세트를 만드는 데 사용할 수 있는 여러 [병합 도구](../../../resources/gtfs/#gtfs-merge-tools)가 있습니다. 
 * 게시된 GTFS 데이터세트는 언제든지 최소 ​​향후 7일 동안 유효해야 하며, 이상적으로는 운영자가 일정이 계속 운영될 것이라고 확신하는 한 유효합니다. 
 * 가능하다면 GTFS 데이터세트는 향후 30일 이상의 서비스를 다루어야 합니다. 
 * 오래된 서비스(만료된 캘린더)는 피드에서 제거되어야 합니다. 
 * 서비스 수정 사항이 7일 이내에 적용되는 경우 이 서비스 변경 사항은 정적 GTFS 데이터세트가 아닌 GTFS 실시간 피드(서비스 권고 또는 여행 업데이트)를 통해 표현되어야 합니다. 
 * GTFS 데이터를 호스팅하는 웹 서버는 파일 수정 date 올바르게 보고하도록 구성되어야 합니다([HTTP/1.1- 의견 요청 2616, 섹션 14.29 참조](https://tools.ietf.org/html/rfc2616 참조).#섹션-14.29)). 
 
## 필드 정의 
 
### agency.txt 
 
 파일: **필수** 
 
 기본 키(`agency_id) 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `agency_id| 고유 ID | **조건부 필수** | 대중교통 agency 과 동의어인 경우가 많은 대중교통 브랜드를 식별합니다. 단일 agency 여러 개의 별도 서비스를 운영하는 경우와 같이 대행사와 브랜드가 구별되는 경우도 있습니다. 본 문서에서는 ’브랜드’ 대신 ’ agency’라는 용어를 사용합니다. 데이터 세트에는 여러 기관의 데이터가 포함될 수 있습니다.<br><br> 조건부 필수:<br> - 데이터세트에 여러 대중교통 기관의 데이터가 포함된 경우 **필수**입니다.<br> - 그렇지 않은 경우 권장됩니다. | 
 | `agency_name` | Text | **필수** | 대중교통 agency 의 전체 이름입니다. | 
 | `agency_url| URL | **필수** | 대중교통 agency 의 URL. | 
 | ` agency_timezone` | 시간대 | **필수** | 대중교통 agency 위치한 시간대입니다. 데이터세트에 여러 대행사가 지정된 경우 각 대행사는 동일한 ’ agency_timezone’을 가져야 합니다. | 
 | `agency_lang` | 언어 코드 | 선택사항 | 이 대중교통 agency 에서 사용하는 기본 언어입니다. GTFS 소비자가 데이터 세트의 대문자 사용 규칙 및 기타 언어별 설정을 선택하는 데 도움이 되도록 제공되어야 합니다. | 
 | `agency_phone` | Phone number | 선택사항 | 특정 agency 의 음성 전화번호입니다. 이 필드는 해당 기관의 서비스 지역에 대한 일반적인 전화번호를 나타내는 string 값입니다. 숫자의 숫자를 그룹화하기 위해 구두점을 포함할 수 있습니다. 전화를 걸 수 있는 텍스트(예: TriMet의 "503-238-RIDE")는 허용되지만 필드에는 다른 설명 텍스트가 포함되어서는 안 됩니다. | 
 | `agency_fare_url| URL | 선택사항 | 승객이 해당 agency 의 티켓이나 기타 요금 수단을 온라인으로 구매할 수 있는 웹페이지의 URL. | 
 | ` agency_email` | Email | 선택사항 | 대행사의 고객 서비스 부서에서 적극적으로 모니터링하는 Email 주소입니다. 이 이메일 주소는 대중교통 탑승자가 agency 의 고객 서비스 담당자에게 연락할 수 있는 직접적인 연락 지점이어야 합니다. | 
 
### stops.txt 
 
 파일: **필수** 
 
 기본 키(`stop_id`) 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `stop_id` | 고유 ID | **필수** | 위치를 식별합니다: 정류장/플랫폼, 역, 입구/출구, 일반 노드 또는 탑승 구역(`location_type` 참조).<br><br> ID는 모든 `stops.stop_id, locations.geojson `id` 및 `location_groups.location_group_id` 값에서 고유해야 합니다.<br><br> 여러 routes 동일한 `stop_id` 사용할 수 있습니다. | 
 | `stop_code` | Text | 선택사항 | 라이더의 위치를 ​​식별하는 짧은 텍스트 또는 숫자입니다. 이러한 코드는 승객이 특정 위치에 대한 정보를 더 쉽게 얻을 수 있도록 전화 기반 대중교통 정보 시스템에 사용되거나 표지판에 인쇄되는 경우가 많습니다. ’ stop_code’는 공개용인 경우 ’`stop_id`’ 와 동일할 수 있습니다. 승객에게 코드가 제공되지 않는 위치의 경우 이 필드를 비워 두어야 합니다. | 
 | `stop_name` | Text | **조건부 필수** | 위치의 이름입니다. `stop_name`은 시간표에 인쇄되어 있거나 온라인에 게시되거나 표지판에 표시된 위치에 대해 기관의 승객이 향하는 이름과 일치해야 합니다. 다른 언어로 번역하려면 [translations.txt](#translationstxt)를 사용하세요.<br><br> 위치가 탑승 구역(`location_type=4`)인 경우 `stop_name`에는 agency 에서 표시하는 탑승 구역의 이름이 포함되어야 합니다. 단 하나의 문자(예: 일부 유럽 도시 간 철도역)일 수도 있고 ’휠체어 탑승 구역’(NYC 지하철) 또는 ’단거리 열차 선두’(파리 RER)와 같은 텍스트일 수도 있습니다.<br><br> 조건부 필수:<br> - stops (`location_type=0`), 역(`location_type=1`) 또는 입구/출구(`location_type=2`)인 위치에 **필수**입니다.<br> - 일반 노드(`location_type=3`) 또는 탑승 구역(`location_type=4`)인 위치의 경우 선택 사항입니다.| 
 | `tts_stop_name` | Text | 선택사항 | `stop_name`의 읽을 수 있는 버전입니다. 자세한 내용은 [용어 정의](#term-definitions)의 ’텍스트 음성 변환 필드’를 참조하세요. | 
 | `stop_desc` | Text | 선택사항 | 유용하고 수준 높은 정보를 제공하는 위치에 대한 설명입니다. `stop_name`과 중복되어서는 안 됩니다.| 
 | `그만해

lat` | 위도 | **조건부 필수** | 위치의 위도입니다.<br><br> stops/플랫폼(`location_type=0`) 및 탑승 구역(`location_type=4`)의 경우 좌표는 버스 극(있는 경우)의 좌표여야 하며 그렇지 않은 경우 여행자가 vehicle 에 탑승하는 위치(보도)의 좌표여야 합니다. 또는 플랫폼이 아닌 vehicle stops 도로나 선로가 아닌 곳).<br><br> 조건부 필수:<br> - stops (`location_type=0`), 역(`location_type=1`) 또는 입구/출구(`location_type=2`)인 위치에 **필수**입니다.<br> - 일반 노드(`location_type=3`) 또는 탑승 구역(`location_type=4`)인 위치의 경우 선택 사항입니다.| 
 | `stop_lon| 경도 | **조건부 필수** | 위치의 경도입니다.<br><br> stops/플랫폼(`location_type=0`) 및 탑승 구역(`location_type=4`)의 경우 좌표는 버스 극(있는 경우)의 좌표여야 하며 그렇지 않은 경우 여행자가 vehicle 에 탑승하는 위치(보도)의 좌표여야 합니다. 또는 플랫폼이 아닌 vehicle stops 도로나 선로가 아닌 곳).<br><br> 조건부 필수:<br> - stops (`location_type=0`), 역(`location_type=1`) 또는 입구/출구(`location_type=2`)인 위치에 **필수**입니다.<br> - 일반 노드(`location_type=3`) 또는 탑승 구역(`location_type=4`)인 위치의 경우 선택 사항입니다. | 
 | `zone_id` | 아이디 | 선택사항 | 정류장 요금 구역을 식별합니다. 이 레코드가 역 또는 역 입구를 나타내는 경우 `zone_id`는 무시됩니다.| 
 | `stop_url| URL | 선택사항 | 위치에 대한 웹페이지의 URL. 이는 `agency.agency_url 및 `routes.route_url 필드 값과 달라야 합니다. | 
 | `location_type` | 열거형 | 선택사항 | 위치 유형. 유효한 옵션은 다음과 같습니다.<br><br> `0`(또는 공백) - **중지**(또는 **플랫폼**). 승객이 대중교통 vehicle 에 탑승하거나 내리는 위치입니다. `parent_station` 내에 정의되면 플랫폼이라고 합니다.<br> `1` - **역**. 하나 이상의 플랫폼을 포함하는 물리적 구조 또는 영역입니다.<br> `2` - **입구/출구**. 승객이 거리에서 역에 들어가거나 나올 수 있는 위치입니다. 입구/출구가 여러 정거장에 속해 있는 경우 두 역 모두에 pathways 로 연결될 수 있지만 데이터 제공자는 그 중 하나를 상위 역으로 선택해야 합니다.<br> `3` - **일반 노드**. [pathways.txt](#pathwaystxt)에 정의된 pathways 함께 연결하는 데 사용될 수 있는 다른 ` location_type `과 일치하지 않는 역 내 위치입니다.<br> `4` - **탑승 구역**. 승객이 차량에 탑승 및/또는 하차할 수 있는 플랫폼의 특정 위치입니다.| 
 | ` parent_station` | `stops.stop_id 를 참조하는 외부 ID | **조건부 필수** | [stops.txt](#stopstxt)에 정의된 다양한 위치 간의 계층 구조를 정의합니다. 여기에는 다음과 같이 상위 위치의 ID가 포함됩니다.<br><br> - **정류장/승강장** (`location_type=0`): `parent_station` 필드에는 역의 ID가 포함됩니다.<br> - **역**(`location_type=1`): 이 필드는 비어 있어야 합니다.<br> - **입구/출구** (`location_type=2`) 또는 **일반 노드** (`location_type=3`): `parent_station` 필드에는 역의 ID가 포함됩니다(`location_type=1`).<br> - **탑승 구역** (`location_type=4`): `parent_station` 필드에는 플랫폼의 ID가 포함됩니다.<br><br> 조건부 필수:<br> - 입구(`location_type=2`), 일반 노드(`location_type=3`) 또는 탑승 구역(`location_type=4`)인 위치에 **필수**입니다.<br> - stops/플랫폼의 경우 선택 사항입니다(`location_type=0`).<br> - 스테이션에는 금지되어 있습니다(`location_type=1`).| 
 | `stop_timezone | 시간대 | 선택사항 | 위치의 시간대. 위치에 상위 스테이션이 있는 경우 자체 시간대를 적용하는 대신 상위 스테이션의 시간대를 상속합니다. ` stop_timezone `이 비어 있는 역 및 부모 없는 stops ` agency.agency_timezone`에 지정된 시간대를 상속합니다. [stop_times.txt](#stop_timestxt)에 제공된 시간은 ` stop_timezone `이 아니라 ` agency.agency_timezone 에 지정된 시간대에 있습니다. 이렇게 하면 여행이 어느 시간대를 통과하는지에 관계없이 여행 과정에서 여행의 시간 값이 항상 증가합니다. | 
 | ` wheelchair_boarding` | 열거형 | 선택사항 | 해당 위치에서 휠체어 탑승이 가능한지 여부를 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> 부모 없는 stops 의 경우:<br> ’0’ 또는 비어 있음 - 정류장에 대한 접근성 정보가 없습니다.<br> `1` - 이 정류장에 있는 일부 차량은 휠체어를 탄 승객도 탑승할 수 있습니다.<br> `2` - 이 정류장은 휠체어 탑승이 불가능합니다.<br><br> 어린이 stops 의 경우:<br> ’0’ 또는 비어 있음 - 정류장은 상위 역에 지정된 경우 상위 역에서 ’ wheelchair_boarding’ 동작을 상속합니다.<br> `1` - 역 외부에서 특정 정류장/플랫폼까지 접근 가능한 경로가 있습니다.<br> `2` - 역 외부에서 특정 정류장/승강장까지 접근 가능한 경로가 없습니다.<br><br> 역 입구/출구의 경우:<br> ’0’ 또는 비어 있음 - 상위 역에 대해 지정된 경우 역 입구는 상위 역에서 ’ wheelchair_boarding’ 동작을 상속합니다.<br> ’`1`’ - 역 입구는 휠체어 접근이 가능합니다.<br> `2` - 역 입구에서 stops/플랫폼까지 접근 가능한 경로가 없습니다. | 
 | `level_id` | `levels.level_id 참조하는 외부 ID | 선택사항 | 위치의 수준. 연결되지 않은 여러 스테이션에서 동일한 레벨을 사용할 수 있습니다.| 
 | `platform_code` | Text | 선택사항 | 플랫폼 정류장(역에 속한 정류장)에 대한 플랫폼 식별자입니다. 이는 플랫폼 식별자(예: "G" 또는 "3")여야 합니다. ’플랫폼’ 또는 ’트랙’(또는 피드의 언어별로 이에 상응하는 단어)과 같은 단어는 포함되어서는 안 됩니다. 이를 통해 피드 소비자는 플랫폼 식별자를 다른 언어로 보다 쉽게 ​​국제화하고 현지화할 수 있습니다. | 
 
 
### routes.txt 
 
 파일: **필수** 
 
 기본 키(`route_id`) 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `route_id` | 고유 ID | **필수** | 경로를 식별합니다. | 
 | `agency_id` | `agency.agency_id 를 참조하는 외부 ID | **조건부 필수** | 지정된 경로에 대한 기관입니다.<br><br> 조건부 필수:<br> - [agency.txt](#agencytxt)에 여러 대행사가 정의된 경우 **필수**입니다.<br> - 그렇지 않은 경우 권장됩니다. | 
 | `route_short_name` | Text | **조건부 필수** | 경로의 짧은 이름입니다. 라이더가 경로를 식별하는 데 사용하는 짧고 추상적인 식별자(예: "32", "100X", "Green")인 경우가 많습니다. `route_short_name 과 `route_long_name 을 모두 정의할 수 있습니다.<br><br> 조건부 필수:<br> - `routes.route_long_name`이 비어 있는 경우 **필수**입니다.<br> - 간략한 서비스 지정이 있는 경우 추천합니다. 이는 일반적으로 알려진 승객 이름이어야 하며 12자를 초과할 수 없습니다. | 
 | `route_long_name` | Text | **조건부 필수** | 경로의 전체 이름입니다. 이 이름은 일반적으로 `route_short_name 보다 더 설명적이며 경로의 목적지나 정류장을 포함하는 경우가 많습니다. `route_short_name 과 `route_long_name 을 모두 정의할 수 있습니다.<br><br> 조건부 필수:<br> - `routes.route_short_name`이 비어 있는 경우 **필수**입니다.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `route_desc` | Text | 선택사항 | 유용하고 수준 높은 정보를 제공하는 경로에 대한 설명입니다. `route_short_name 또는 `route_long_name 과 중복되어서는 안 됩니다.<hr> _예: "A" 열차는 맨해튼의 Inwood-207 St와 Queens의 Far Rockaway-Mott Avenue 사이를 항상 운행합니다. 또한 오전 6시부터 자정까지 추가 "A" 열차가 Inwood-207 St와 Lefferts Boulevard 사이를 운행합니다(열차는 일반적으로 Lefferts Blvd와 Far Rockaway를 번갈아 운행합니다)._ | 
 | `route_type` | 열거형 | **필수** | 경로에서 사용되는 교통수단의 유형을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> `0` - 트램, 전차, 경전철. 대도시 지역 내의 모든 경전철 또는 거리 수준 시스템.<br> `1` - 지하철, 지하철. 대도시 지역 내의 모든 지하철 시스템.<br> `2` - 레일. 도시 간 또는 장거리 여행에 사용됩니다.<br> `3` - 버스. 단거리 및 장거리 버스 routes 에 사용됩니다.<br> `4` - 페리. 단거리 및 장거리 보트 서비스에 사용됩니다.<br> `5` - 케이블 트램. 케이블이 vehicle 아래로 연결되는 거리 수준의 철도 차량에 사용됩니다(예: 샌프란시스코의 케이블카).<br> `6` - 공중 리프트, 매달린 케이블카(예: 곤돌라 리프트, 공중 트램웨이). 캐빈, 자동차, 곤돌라 또는 개방형 의자가 하나 이상의 케이블에 매달려 있는 케이블 운송입니다.<br> `7` - 케이블카. 가파른 경사를 위해 설계된 모든 레일 시스템.<br> `11` - 무궤도 전차. 기둥을 이용해 가공선에서 전력을 끌어오는 전기버스.<br> `12` - 모노레일. 선로가 단일 레일 또는 빔으로 구성된 철도입니다. | 
 | `route_url` | URL | 선택사항 | 특정 경로에 대한 웹페이지의 URL. `agency.agency_url 값과 달라야 합니다. | 
 | `route_color` | 색상 | 선택사항 | 대중을 위한 자료와 일치하는 경로 색상 지정. 생략하거나 비워두면 기본값은 흰색(`FFFFFF)입니다. `route_color 와 `route_text_color 의 색상 차이는 흑백 화면에서 볼 때 충분한 대비를 제공해야 합니다. | 
 | `route_text_color` | 색상 | 선택사항 | `route_color 배경에 그려진 텍스트에 사용할 읽기 쉬운 색상입니다. 생략하거나 비워두면 기본값은 검정색(`000000`)입니다. `route_color 와 `route_text_color 의 색상 차이는 흑백 화면에서 볼 때 충분한 대비를 제공해야 합니다. | 
 | `route_sort_order` | 음수가 아닌 정수 | 선택사항 | 고객에게 제시하기에 이상적인 방식으로 routes 주문합니다. `route_sort_order 값이 더 작은 경로가 먼저 표시되어야 합니다. | 
 | `continuous_pickup ` | 열거형 | **조건부 금지** | 경로의 모든 이동 시 [shapes.txt](#shapestxt)에 설명된 대로 승객이 차량 이동 경로를 따라 어느 지점에서든 대중교통 vehicle 에 탑승할 수 있음을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ - 연속 정지 픽업.<br> ’`1`’ 또는 비어 있음 - 지속적인 정지 픽업이 없습니다.<br> `2` - 지속적인 정차 픽업을 예약하려면 agency 전화해야 합니다.<br> `3` - 운전자와 협의하여 연속 정차 픽업을 준비해야 합니다.<br><br> 경로를 따라 특정 ` stop_time `에 대해 ` stop_times.continuous_pickup `에 값을 정의하여 ` routes.continuous_pickup 값을 재정의할 수 있습니다.<br><br> **조건부 금지**:<br> - ` stop_times.start_pickup_drop_off_window` 또는 `stop_times.end_pickup_drop_off_window 는 이 경로의 모든 이동에 대해 정의됩니다.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `continuous_drop_off ` | 열거형 | **조건부 금지** | [shapes.txt](#shapestxt)에 설명된 대로 경로의 모든 이동에서 승객이 차량 이동 경로를 따라 어느 지점에서나 대중교통 vehicle 에서 내릴 수 있음을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ - 연속 정지 하차.<br> ’`1`’ 또는 비어 있음 - 연속 정지 하차가 없습니다.<br> `2` - 지속적인 정차를 위해 agency 에 전화해야 합니다.<br> `3` - 운전자와 협력하여 지속적인 정차를 준비해야 합니다.<br><br> 경로를 따라 특정 ` stop_time `에 대해 ` stop_times.continuous_drop_off `에 값을 정의하여 ` routes.continuous_drop_off ` 값을 재정의할 수 있습니다.<br><br> **조건부 금지**:<br> - ` stop_times.start_pickup_drop_off_window` 또는 `stop_times.end_pickup_drop_off_window 는 이 경로의 모든 이동에 대해 정의됩니다.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `network_id` | 아이디 | **조건부 금지** | routes 그룹을 식별합니다. [routes.txt](#routestxt)의 여러 행은 동일한 `network_id`를 가질 수 있습니다.<br><br> 조건부 금지:<br> - [route_networks.txt](#route_networkstxt) 파일이 존재하는 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. 
 
### trips.txt 
 
 파일: **필수** 
 
 기본 키(`trip_id`) 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `route_id` | `routes.route_id`를 참조하는 외부 ID | **필수** | 경로를 식별합니다. | 
 | `service_id` | `calendar.service_id` 또는 `calendar_dates.service_id`를 참조하는 외부 ID | **필수** | 하나 이상의 routes 에 대해 서비스를 이용할 수 있는 날짜 집합을 식별합니다. | 
 | `trip_id` | 고유 ID | **필수** | 여행을 식별합니다. | 
 | `trip_headsign` | Text | 선택사항 | 승객에게 여행 목적지를 알려주는 표지판에 표시되는 Text 입니다. 동일한 경로에서 다양한 서비스 패턴을 구별하는 데 사용해야 합니다.<br><br> 이동 중에 행선지가 변경되면 이동 중 특정 ` stop_time `에 대해 ` stop_times.stop_headsign `에 값을 정의하여 ` trip_headsign ` 값이 재정의될 수 있습니다. | 
 | ` trip_short_name` | Text | 선택사항 | 예를 들어 통근 열차 여행의 열차 번호를 식별하기 위해 승객의 여행을 식별하는 데 사용되는 공개 텍스트입니다. 승객이 일반적으로 여행 이름을 사용하지 않는 경우 `trip_short_name 비어 있어야 합니다. `trip_short_name` 값이 제공되는 경우 서비스 날짜 내의 이동을 고유하게 식별해야 합니다. 목적지 이름이나 제한적/명시적 명칭으로 사용해서는 안 됩니다. | 
 | `direction_id` | 열거형 | 선택사항 | 여행의 여행 방향을 나타냅니다. 이 필드는 라우팅에 사용되어서는 안 됩니다. 시간표를 게시할 때 방향별로 이동을 구분하는 방법을 제공합니다. 유효한 옵션은 다음과 같습니다.<br><br> `0` - 한 방향으로 여행합니다(예: 아웃바운드 여행).<br> `1` - 반대 방향으로 여행합니다(예: 인바운드 여행).<hr> *예: `trip_headsign 및 `direction_id` 필드를 함께 사용하여 일련의 이동에 대해 각 방향으로 이동할 이름을 할당할 수 있습니다. [trips.txt](#tripstxt) 파일에는 시간표에 사용할 수 있는 다음 레코드가 포함될 수 있습니다.*<br> `trip_id,...,trip_headsign,direction_id`<br> `1234,...,Airport,0`<br> `1505,...,Downtown,1` | 
 | `block_id ` | 아이디 | 선택사항 | 여행이 속한 블록을 식별합니다. 블록은 공유 서비스 날짜와 ’ block_id ’로 정의된 동일한 vehicle 사용하여 수행된 단일 이동 또는 여러 연속 이동으로 구성됩니다. ` block_id`는 서로 다른 서비스 날짜의 여행을 포함하여 고유한 블록을 만들 수 있습니다. [아래 예](#example-blocks-and-service-day)를 참조하세요. 좌석 transfers 정보를 제공하려면 ` transfer_type ` `4`의 [transfers](#transferstxt)을 대신 제공해야 합니다. | 
 | `shape_id` | `shapes.shape_id 참조하는 외부 ID | **조건부 필수** | 이동을 위한 vehicle 이동 경로를 설명하는 지리공간적 shape 식별합니다.<br><br> 조건부 필수:<br> - **필수** 이동에 [routes.txt](#routestxt) 또는 [stop_times.txt](#stop_timestxt)에 정의된 연속 승차 또는 하차 동작이 있는 경우.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `wheelchair_accessible` | 열거형 | 선택사항 | 휠체어 접근성을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 여행에 대한 접근성 정보가 없습니다.<br> `1` - 이 특정 여행에 사용되는 차량은 휠체어를 탄 승객 한 명 이상을 수용할 수 있습니다.<br> `2` - 이번 여행에는 휠체어를 탄 승객이 탑승할 수 없습니다. | 
 | `bikes_allowed` | 열거형 | 선택사항 | 자전거 허용 여부를 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 여행에 대한 자전거 정보가 없습니다.<br> `1` - 이 특정 여행에 사용되는 차량은 최소한 한 대의 자전거를 수용할 수 있습니다.<br> `2` - 이번 여행에는 자전거가 허용되지 않습니다. | 
 
#### 예: 블록 및 서비스 요일 
 
 아래 예는 유효하며, 주중 매일 별도의 블록이 있습니다. 
 
 | route_id | trip_id | service_id | block_id | <span style="font-weight:normal">*(첫 번째 정지 시간)*</span> | <span style="font-weight:normal">*(마지막 정차 시간)*</span> | 
 |------------|---------|-------------------|----------|---------------|------------| 
 | 빨간색 | trip_1 | 월화수목금토일 | 레드루프 | 22:00:00 | 22:55:00 | 
 | 빨간색 | trip_2 | 금-토-일 | 레드루프 | 23:00:00 | 23:55:00 | 
 | 빨간색 | trip_3 | 금-토 | 레드루프 | 24:00:00 | 24:55:00 | 
 | 빨간색 | trip_4 | 월-화-수-목 | 레드루프 | 20:00:00 | 20:50:00 | 
 | 빨간색 | trip_5 | 월-화-수-목 | 레드루프 | 21:00:00 | 21:50:00 | 
 
 위 표에 대한 참고사항: 
 
 * 예를 들어 금요일부터 토요일 오전까지 vehicle 한 대가 `trip_1`, `trip_2`, `trip_3`(오후 10시부터 오전 12시 55분까지)을 운행합니다.. 마지막 운행은 토요일 오전 12시부터 12시 55분까지 이루어지지만 시간이 24:00:00부터 24:55:00이므로 금요일 "서비스일"에 포함됩니다. 
 * 월요일, 화요일, 수요일, 목요일에는 오후 8시부터 오후 10시 55분까지 vehicle 1대가 `trip_1, `trip_4, `trip_5 를 블록으로 운행합니다. 
 
### stop_times.txt 
 
 파일: **필수** 
 
 기본 키(`trip_id`, `stop_sequence`) 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `trip_id` | ’`trips.trip_id` 참조하는 외국인 ID | **필수** | 여행을 식별합니다. | 
 | `arrival_time ` | 시간 | **조건부 필수** | ` stops.stop_timezone 이 아닌 ` agency.agency_timezone 으로 지정된 시간대의 특정 이동(` stop_times.stop_id 로 정의)에 대한 정류장(`stop_times.trip_id 로 정의)에 도착하는 시간입니다.<br><br> 정류장 arrival 과 departure 시간이 따로 있지 않은 경우 `arrival_time`과 `departure_time` 은 동일해야 합니다.<br><br> 운행일 자정 이후의 시간은 HH:MM:SS 형식으로 24:00:00보다 큰 값으로 입력합니다.<br><br> 정확한 arrival 및 departure 시간(`timepoint=1` 또는 비어 있음)을 사용할 수 없는 경우 예상 또는 보간된 arrival 및 departure 시간(`timepoint=0`)을 제공해야 합니다.<br><br> 조건부 필수:<br> - 이동의 첫 번째 및 마지막 정류장에 **필수**입니다(`stop_times.stop_sequence`로 정의됨).<br> - `timepoint=1`의 경우 **필수**입니다.<br> - `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - 그 외에는 선택사항입니다.| 
 | `departure_time` ` | 시간 | **조건부 필수** | ` stops.stop_timezone 이 아닌 ` agency.agency_timezone 에 의해 지정된 시간대에서 특정 이동(` stop_times.stop_id 로 정의됨)에 대한 정류장(`stop_times.trip_id 로 정의됨)에서 출발 시간입니다.<br><br> 정류장 arrival 과 departure 시간이 따로 있지 않은 경우 `arrival_time`과 `departure_time` 은 동일해야 합니다.<br><br> 운행일 자정 이후의 시간은 HH:MM:SS 형식으로 24:00:00보다 큰 값으로 입력합니다.<br><br> 정확한 arrival 및 departure 시간(`timepoint=1` 또는 비어 있음)을 사용할 수 없는 경우 예상 또는 보간된 arrival 및 departure 시간(`timepoint=0`)을 제공해야 합니다.<br><br> 조건부 필수:<br> - `timepoint=1`의 경우 **필수**입니다.<br> - `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `stop_id` | `stops.stop_id 를 참조하는 외부 ID | **조건부 필수** | 서비스가 제공되는 정류장을 식별합니다. 이동 중에 서비스되는 모든 stops [stop_times.txt](#stop_timestxt)에 기록이 있어야 합니다. 참조된 위치는 stops/플랫폼이어야 합니다. 즉, ’ stops.location_type’ 값은 ’0’이거나 비어 있어야 합니다. 한 정류장은 동일한 이동 내에서 여러 번 서비스될 수 있으며, 여러 이동 및 routes 동일한 정류장을 서비스할 수 있습니다.<br><br> stops 이용한 주문형 서비스는 해당 stops 에서 서비스를 이용할 수 있는 순서대로 참조되어야 합니다. 데이터 소비자는 각 stop_time 의 `pickup/drop_off_type 과 각 `start/end_pickup_drop_off_window 의 시간 제약이 이를 금지하지 않는 한, 여행 후반에 한 정거장이나 위치에서 다른 정류장이나 위치로 여행이 가능하다고 가정해야 합니다..<br><br> 조건부 필수:<br> - `stop_times.location_group_id` 및 `stop_times.location_id`가 정의되지 않은 경우 **필수**입니다.<br> - `stop_times.location_group_id` 또는 `stop_times.location_id`가 정의된 경우 **금지됨**. | 
 | `위치_그룹_ID` | ’location_groups.location_group_id’를 참조하는 외부 ID | **조건부 금지** | 승객이 픽업 또는 하차를 요청할 수 있는 stops 그룹을 나타내는 서비스 위치 그룹을 식별합니다. 이동 중에 서비스되는 모든 위치 그룹은 [stop_times.txt](#stop_timestxt)에 기록이 있어야 합니다. 여러 이동 및 routes 동일한 위치 그룹을 서비스할 수 있습니다.<br><br> 위치 그룹을 이용한 온디맨드 서비스는 해당 위치 그룹에서 서비스가 가능한 순서대로 참조되어야 합니다. 데이터 소비자는 각 stop_time 의 `pickup/drop_off_type 과 각 `start/end_pickup_drop_off_window 의 시간 제약이 이를 금지하지 않는 한, 여행 후반에 한 정거장이나 위치에서 다른 정류장이나 위치로 여행이 가능하다고 가정해야 합니다..<br><br> **조건부 금지**:<br> - `stop_times.stop_id 또는 `stop_times.location_id`가 정의된 경우 **금지됨**. | 
 | `위치_ID` | `locations.geojson` 에서 `id` 참조하는 외부 ID | **조건부 금지** | 승객이 픽업 또는 하차를 요청할 수 있는 서비스 구역에 해당하는 GeoJSON 위치를 식별합니다. 여행 중에 서비스되는 모든 GeoJSON 위치는 [stop_times.txt](#stop_timestxt)에 기록이 있어야 합니다. 여러 여행과 routes 동일한 GeoJSON 위치를 서비스할 수 있습니다.<br><br> 위치 내의 주문형 서비스는 해당 위치에서 서비스가 제공되는 순서대로 참조되어야 합니다. 데이터 소비자는 각 stop_time 의 `pickup/drop_off_type 과 각 `start/end_pickup_drop_off_window 의 시간 제약이 이를 금지하지 않는 한, 여행 후반에 한 정거장이나 위치에서 다른 정류장이나 위치로 여행이 가능하다고 가정해야 합니다..<br><br> **조건부 금지**:<br> - `stop_times.stop_id 또는 `stop_times.location_group_id`가 정의된 경우 **금지됨**. | 
 | `stop_sequence` | 음수가 아닌 정수 | **필수** | 특정 여행에 대한 stops, 위치 그룹 또는 GeoJSON 위치의 순서입니다. 값은 이동 중에 증가해야 하지만 연속적일 필요는 없습니다.<hr> *예: 이동의 첫 번째 위치는 `stop_sequence`= `1` 일 수 있고, 이동의 두 번째 위치는 `stop_sequence`=`23`일 수 있으며, 세 번째 위치는 `stop_sequence`=`40`일 수 있습니다., 등등.*<br><br> 동일한 위치 그룹 또는 GeoJSON 위치 내에서 여행하려면 [stop_times.txt](#stop_timestxt)에 동일한 `location_group_id` 또는 `location_id`가 있는 두 개의 레코드가 필요합니다. | 
 | `stop_headsign| Text | 선택사항 | 승객에게 여행 목적지를 알려주는 표지판에 표시되는 Text 입니다. 이 필드는 stops 사이에 행선지가 변경될 때 기본 ` trips.trip_headsign 재정의합니다. 행선지가 전체 여행에 대해 표시되는 경우 ` trips.trip_headsign 을 대신 사용해야 합니다.<br><br> 하나의 ` stop_time `에 지정된 ` stop_headsign ` 값은 동일한 이동의 후속 ` stop_time `에 적용되지 않습니다. 동일한 이동에서 여러 ` stop_time `에 대해 ` trip_headsign `을 재정의하려면 각 ` stop_time ` 행에서 ` stop_headsign` 값을 repeated 해야 합니다. | 
 | `start_pickup_drop_off_window` | 시간 | **조건부 필수** | GeoJSON 위치, 위치 그룹 또는 정류장에서 주문형 서비스를 사용할 수 있게 된 시간입니다.<br><br> **조건부 필수**:<br> - `stop_times.location_group_id` 또는 `stop_times.location_id`가 정의된 경우 **필수**입니다.<br> - `end_pickup_drop_off_window` 정의된 경우 **필수**입니다.<br> - `arrival_time` 또는 `departure_time` 정의된 경우 **금지**입니다.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `end_pickup_drop_off_window` | 시간 | **조건부 필수** | 주문형 서비스가 GeoJSON 위치, 위치 그룹 또는 정류장에서 종료되는 시간입니다.<br><br> **조건부 필수**:<br> - `stop_times.location_group_id` 또는 `stop_times.location_id`가 정의된 경우 **필수**입니다.<br> - `start_pickup_drop_off_window` 정의된 경우 **필수**입니다.<br> - `arrival_time` 또는 `departure_time` 정의된 경우 **금지**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `pickup_type` | 열거형 | **조건부 금지** | 픽업 방법을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 정기적으로 예약된 픽업입니다.<br> `1` - 픽업이 불가능합니다.<br> `2` - 픽업을 준비하려면 agency 전화해야 합니다.<br> `3` - 픽업을 준비하려면 운전자와 조율해야 합니다.<br><br> **조건부 금지**:<br> - `pickup_type=0` `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - `pickup_type=3` `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `drop_off_type` | 열거형 | **조건부 금지** | 하차 방법을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 정기적으로 예정된 하차입니다.<br> `1` - 하차가 불가능합니다.<br> `2` - 하차를 준비하려면 agency 전화해야 합니다.<br> `3` - 하차 준비를 위해 운전자와 조율해야 합니다.<br><br> **조건부 금지**:<br> - `drop_off_type=0` `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `continuous_pickup ` | 열거형 | **조건부 금지** | 승객이 [shapes.txt](#shapestxt)에 설명된 대로 차량 이동 경로를 따라 이동의 `stop_sequence` 에서 이 ` stop_time`부터 다음 `stop_time `까지 대중교통 vehicle 에 탑승할 수 있음을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ - 연속 정지 픽업.

br> `1` 또는 비어 있음 - 지속적인 정지 픽업이 없습니다.<br> `2` - 지속적인 정차 픽업을 예약하려면 agency 전화해야 합니다.<br> `3` - 운전자와 협의하여 연속 정차 픽업을 준비해야 합니다.<br><br> 이 필드가 채워지면 [routes.txt](#routestxt)에 정의된 연속 픽업 동작을 재정의합니다. 이 필드가 비어 있으면 `stop_time`은 [routes.txt](#routestxt)에 정의된 연속 승차 동작을 상속합니다.<br><br> **조건부 금지**:<br> - `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `continuous_drop_off ` | 열거형 | **조건부 금지** | 승객이 [shapes.txt](#shapestxt)에 설명된 대로 차량 이동 경로를 따라 이동의 `stop_sequence` 에서 이 ` stop_time`부터 다음 `stop_time `까지 대중교통 vehicle 에서 내릴 수 있음을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ - 연속 정지 하차.<br> ’`1`’ 또는 비어 있음 - 연속 정지 하차가 없습니다.<br> `2` - 지속적인 정차를 위해 agency 에 전화해야 합니다.<br> `3` - 운전자와 협력하여 지속적인 정차를 준비해야 합니다.<br><br> 이 필드가 채워지면 [routes.txt](#routestxt)에 정의된 모든 지속적인 하차 동작을 재정의합니다. 이 필드가 비어 있으면 `stop_time`은 [routes.txt](#routestxt)에 정의된 연속 하차 동작을 상속합니다.<br><br> **조건부 금지**:<br> - `start_pickup_drop_off_window` 또는 `end_pickup_drop_off_window` 가 정의된 경우 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `shape_dist_traveled` | 음수가 아닌 float 소수점 | 선택사항 | 첫 번째 정류장에서 이 기록에 지정된 정류장까지 관련 shape 따라 이동한 실제 거리입니다. 이 필드는 이동 중에 두 stops 사이에 그릴 shape 의 양을 지정합니다. [shapes.txt](#shapestxt)에 사용된 것과 동일한 단위여야 합니다. `shape_dist_traveled 에 사용되는 값은 `stop_sequence` 와 함께 증가해야 합니다. 경로를 따라 역방향 이동을 표시하는 데 사용해서는 안 됩니다.<br><br> 순환 또는 인라인이 있는 routes 에 권장됩니다( vehicle 한 번의 이동으로 선형의 동일한 부분을 건너거나 이동함). [`shapes.shape_dist_traveled](#shapestxt)를 참조하세요.<hr> *예: 버스가 shape 의 시작점에서 정류장까지 5.25km의 거리를 이동하는 경우 `shape_dist_traveled`=`5.25`.*| 
 | `timepoint ` | 열거형 | 추천 | vehicle 정차를 위한 arrival 및 departure 시간을 엄격히 준수하는지, 아니면 대략적인 시간 및/또는 보간된 시간인지를 나타냅니다. 이 필드를 사용하면 GTFS 생산자가 보간된 정지 시간을 제공하면서 해당 시간이 대략적인 것임을 나타낼 수 있습니다. 유효한 옵션은 다음과 같습니다.<br><br> `0` - 시간은 대략적인 것으로 간주됩니다.<br> ’`1`’ 또는 비어 있음 - 시간이 정확한 것으로 간주됩니다. | 
 | `pickup_booking_rule_id` | `booking_rules.booking_rule_id`를 참조하는 ID | 선택사항 | 이 정류장 시간의 탑승 예약 규칙을 식별합니다.<br><br> `pickup_type=2`인 경우 권장됩니다. | 
 | `drop_off_booking_rule_id` | `booking_rules.booking_rule_id`를 참조하는 ID | 선택사항 | 이 정류장 시간에 하차 예약 규칙을 식별합니다.<br><br> `drop_off_type =2`인 경우 권장됩니다. | 
 
#### 온디맨드 서비스 라우팅 동작 
 - 출발지와 목적지 사이의 라우팅 또는 이동 시간을 제공할 때 데이터 소비자는 `start_pickup_drop_off_window` 및 `trip_id` 가 동일한 중간 stop_times.txt 레코드를 무시해야 합니다. ’`end_pickup_drop_off_window` 정의되었습니다. 무엇을 무시해야 하는지 보여주는 예시는 [데이터 예시 페이지](../examples/flex/#ignoring-intermediate-stop-times-records-with-pickupdrop-off-windows)를 참조하세요. 
 - 동일한 `trip_id` 가진 두 개 이상의 stop_times.txt 레코드 사이에 locations.geojson `id` 지오메트리, `start/end_pickup_drop_off_window` 시간, `pickup_type 또는 `drop_off_type 이 동시에 겹치는 것은 금지됩니다. 무엇이 금지되는지 보여주는 예시는 [데이터 예시 페이지](../examples/flex/#zone-overlap-constraint)를 참조하세요. 
 
### calendar.txt 
 
 파일: **조건부 필수** 
 
 기본 키(`service_id`) 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `service_id` | 고유 ID | **필수** | 하나 이상의 routes 에 대해 서비스를 이용할 수 있는 날짜 집합을 식별합니다. | 
 | `monday ` | 열거형 | **필수** | ’`start_date`’ 및 ’ end_date ’ 필드에 지정된 date 범위의 모든 월요일에 서비스가 작동하는지 여부를 나타냅니다. 특정 날짜에 대한 예외 사항은 [calendar_dates.txt](#calendar_datestxt)에 나열되어 있을 수 있습니다. 유효한 옵션은 다음과 같습니다.<br><br> `1` - date 기간의 모든 월요일에 서비스가 제공됩니다.<br> ’0’ - date 기간의 월요일에는 서비스를 이용할 수 없습니다. | 
 | `tuesday` | 열거형 | **필수** | 화요일에 적용되는 점을 제외하면 `monday 와 동일한 기능 | 
 | `wednesday` | 열거형 | **필수** | 수요일에 적용되는 점을 제외하면 `monday 와 동일한 기능 | 
 | `thursday` | 열거형 | **필수** | 목요일에 적용된다는 점을 제외하면 `monday 와 동일한 기능 | 
 | `friday` | 열거형 | **필수** | 금요일에 적용되는 점을 제외하면 `monday 와 동일한 기능 | 
 | `saturday` | 열거형 | **필수** | 토요일에 적용되는 점을 제외하면 `monday 와 동일한 기능을 합니다. | 
 | `sunday` | 열거형 | **필수** | 일요일에 적용된다는 점을 제외하면 `monday 와 동일한 기능을 합니다. | 
 | `start_date` | 날짜 | **필수** | 서비스 간격에 대한 서비스 시작일입니다. | 
 | `end_date` | 날짜 | **필수** | 서비스 간격에 대한 서비스 종료일입니다. 이 서비스 일은 간격에 포함됩니다. | 
 
### calendar_dates.txt 
 
 파일: **조건부 필수** 
 
 기본 키(`service_id`, `date`) 
 
 [calendar_dates.txt](#calendar_datestxt ) 테이블은 date 별로 서비스를 명시적으로 활성화하거나 비활성화합니다. 두 가지 방법으로 사용될 수 있습니다. 
 
 * 권장 사항: [calendar_dates.txt](#calendartxt)와 함께 [calendar.txt](#calendar_datestxt)를 사용하여 [calendar.txt](#calendartxt)에 정의된 기본 서비스 패턴에 대한 예외를 정의하세요. 서비스가 일반적으로 정기적이고 명시적인 날짜에 몇 가지 변경(예: 특별 행사 서비스 또는 학교 일정을 수용하기 위해)이 있는 경우 이는 좋은 접근 방식입니다. 이 경우 `calendar_dates.service_id`는 `calendar.service_id`를 참조하는 외부 ID입니다. 
 * 대안: [calendar.txt](#calendartxt)를 생략하고 [calendar_dates.txt](#calendar_datestxt)에 각 서비스 date 지정하세요. 이는 상당한 서비스 변형을 허용하고 일반적인 주간 일정 없이 서비스를 수용합니다. 이 경우 ` service_id`는 ID입니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `service_id` | `calendar.service_id` 또는 ID를 참조하는 외부 ID | **필수** | 하나 이상의 routes 에 대해 서비스 예외가 발생하는 날짜 집합을 식별합니다. [calendar_dates.txt](#calendartxt) 및 [Calendar_dates.txt](#calendar_datestxt) calendar.txt 함께 사용하는 경우 각 (` service_id`, `date `) 쌍은 [calendar_dates.txt](#calendar_datestxt)에 한 번만 나타날 수 있습니다. [calendar.txt](#calendartxt)와 [calendar_dates.txt](#calendar_datestxt) 모두에 ’ service_id ’ 값이 나타나는 경우, [calendar_dates.txt](#calendar_datestxt)의 정보는 [calendar.txt](#calendartxt). | 
 | `date` | 날짜 | **필수** | 서비스 예외가 발생한 날짜입니다. | 
 | `exception_type ` | 열거형 | **필수** | date 필드에 지정된 date 에 서비스를 이용할 수 있는지 여부를 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> `1` - 지정된 date 에 서비스가 추가되었습니다.<br> `2` - 지정된 date 에 서비스가 제거되었습니다.<hr> *예: 경로에 휴일에 이용 가능한 한 세트의 여행이 있고 다른 모든 날에 이용 가능한 또 다른 여행 세트가 있다고 가정합니다. 하나의 `service_id`는 정기 서비스 일정에 해당하고 다른 `service_id`는 휴일 일정에 해당할 수 있습니다. 특정 휴일의 경우 [calendar_dates.txt](#calendar_datestxt) 파일을 사용하여 휴일 `service_id`에 휴일을 추가하고 일반 `service_id` 일정에서 휴일을 제거할 수 있습니다.* | 
 
### fare_attributes.txt 
 
 파일: **선택 사항** 
 
 기본 키(`fare_id`) 
 
 **버전**<br> 
 요금을 설명하는 데는 두 가지 모델링 옵션이 있습니다. GTFS- Fares V1 최소 요금 정보를 설명하기 위한 기존 옵션입니다. GTFS- Fares V2 기관의 요금 구조를 더욱 자세히 설명할 수 있는 업데이트된 방법입니다. 둘 다 데이터 세트에 존재할 수 있지만 데이터 소비자는 지정된 데이터 세트에 대해 한 가지 방법만 사용해야 합니다. GTFS- Fares V2 GTFS- Fares V1 보다 우선 적용되는 것이 좋습니다.<br><br> GTFS- Fares V1 과 관련된 파일은 다음과 같습니다.<br> - [fare_attributes.txt](#fare_attributestxt)<br> - [fare_rules.txt](#fare_rulestxt)<br><br> GTFS- Fares V2 와 관련된 파일은 다음과 같습니다.<br> - [fare_media.txt](#fare_mediatxt)<br> - [fare_products.txt](#fare_productstxt)<br> - [fare_leg_rules.txt](#fare_leg_rulestxt)<br> - [fare_transfer_rules.txt](#fare_transfer_rulestxt) 
 
<br> 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `fare_id` | 고유 ID | **필수** | 운임 클래스를 식별합니다. | 
 | `price` | 음수가 아닌 float 소수점 | **필수** | ` currency_type `으로 지정된 단위의 운임 price. | 
 | ` currency_type` | 통화 코드 | **필수** | 요금 지불에 사용되는 통화입니다. | 
 | `payment_method` | 열거형 | **필수** | 요금을 지불해야 하는 시기를 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ - 요금은 선상에서 지불됩니다.<br> `1` - 탑승 전 요금을 결제해야 합니다. | 
 | `transfers` | 열거형 | **필수** | 이 요금으로 허용되는 transfers 횟수를 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ - 이 요금에는 transfers 허용되지 않습니다.<br> `1` - 라이더는 한 번 환승할 수 있습니다.<br> `2` - 라이더는 두 번 환승할 수 있습니다.<br> 비어 있음 - 무제한 transfers 허용됩니다. | 
 | `agency_id` | `agency.agency_id 를 참조하는 외부 ID | **조건부 필수** | 운임 관련 agency 식별합니다.<br><br> 조건부 필수:<br> - [agency.txt](#agencytxt)에 여러 대행사가 정의된 경우 **필수**입니다.<br> - 그렇지 않은 경우 권장됩니다. | 
 | `transfer_duration` | 음수가 아닌 정수 | 선택사항 | 전송이 만료되기 전까지의 시간(초)입니다. `transfers`=`0`인 경우 이 필드는 티켓의 유효 기간을 나타내는 데 사용될 수 있거나 비어 있을 수 있습니다. | 
 
### fare_rules.txt 
 
 파일: **선택 사항** 
 
 기본 키(`*`) 
 
 [fare_rules.txt](#fare_rulestxt) 테이블은 요금이 어떻게 부과되는지 지정합니다. [fare_attributes.txt](#fare_attributestxt)에서 여정에 적용됩니다. 대부분의 요금 체계는 다음 규칙의 일부 조합을 사용합니다. 
 
 * 요금은 출발역 또는 도착역에 따라 다릅니다. 
 * 요금은 여정이 통과하는 구역에 따라 다릅니다. 
 * 요금은 여정에서 사용하는 경로에 따라 다릅니다. 
 
 [fare_rules.txt](#fare_rulestxt) 및 [fare_attributes.txt](#fare_attributestxt)를 사용하여 요금 구조를 지정하는 방법을 보여주는 예는 [FareExamples](https://web.archive.org/를 참조하세요. web/20111207224351/https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) GoogleTransitDataFeed 오픈소스 프로젝트 위키에 있습니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `fare_id` | `fare_attributes.fare_id 를 참조하는 외부 ID | **필수** | 운임 클래스를 식별합니다. | 
 | `route_id` | `routes.route_id`를 참조하는 외부 ID | 선택사항 | 요금 등급과 관련된 경로를 식별합니다. 동일한 요금 속성을 가진 routes 여러 개 존재하는 경우 각 경로에 대해 [fare_rules.txt](#fare_rulestxt)에 기록을 생성하세요.<hr> *예: 운임 클래스 "b"가 "TSW" 및 "TSE" 경로에서 유효한 경우 [fare_rules.txt](#fare_rulestxt) 파일에는 운임 클래스에 대한 다음 레코드가 포함됩니다.*<br> ` fare_id,route_id`<br> `b,TSW`<br> `b,TSE`| 
 | `origin_id` | `stops.zone_id 를 참조하는 외부 ID | 선택사항 | 원본 영역을 식별합니다. 요금 클래스에 여러 출발지 구역이 있는 경우 각 ` origin_id `에 대해 [fare_rules.txt](#fare_rulestxt)에 기록을 생성하세요.<hr> *예: 운임 클래스 "b"가 구역 "2" 또는 구역 "8"에서 출발하는 모든 여행에 유효한 경우 [fare_rules.txt](#fare_rulestxt) 파일에는 운임 클래스에 대한 다음 레코드가 포함됩니다.*<br> `fare_id,...,origin_id`<br> `b,...,2`<br> `b,...,8` | 
 | `destination_id| `stops.zone_id 를 참조하는 외부 ID | 선택사항 | 대상 영역을 식별합니다. 요금 클래스에 목적지 구역이 여러 개 있는 경우 각 ` destination_id `에 대해 [fare_rules.txt](#fare_rulestxt)에 기록을 생성하세요.<hr> *예: ` origin_id 및 `destination_id 필드를 함께 사용하면 요금 클래스 "b"가 구역 3과 4 사이의 여행에 유효하고, 구역 3과 5 사이의 여행에 유효함을 지정할 수 있으며, [fare_rules.txt](#fare_rulestxt) 파일에는 요금 등급에 대한 다음 기록이 포함됩니다.*<br> `fare_id,...,origin_id,destination_id`<br> `b,...,3,4`<br> `b,...,3,5` | 
 | `contains_id` | `stops.zone_id 를 참조하는 외부 ID | 선택사항 | 승객이 특정 요금 등급을 사용하는 동안 진입하게 될 구역을 식별합니다. 일부 시스템에서 정확한 요금 등급을 계산하는 데 사용됩니다.<hr> *예: 요금 클래스 "c"가 구역 5, 6, 7을 통과하는 GRT 경로의 모든 여행과 연결된 경우 [fare_rules.txt](#fare_rulestxt)에 다음 레코드가 포함됩니다.*<br> `fare_id,route_id,...,contains_id`<br> `c,GRT,...,5`<br> `c,GRT,...,6`<br> `c,GRT,...,7`<br> *운임이 적용되려면 모든 `contains_id` 구역이 일치해야 하기 때문에 구역 5와 6을 통과하지만 구역 7을 통과하지 않는 여정에는 운임 클래스 "c"가 없습니다. 자세한 내용은 GoogleTransitDataFeed 프로젝트 위키의 [https://code.google.com/p/googletransitdatafeed/wiki/FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples)를 참조하세요.* | 
 
### timeframes.txt 
 
 파일: **선택 사항** 
 
 기본 키(`*`) 
 
 하루 중 시간에 따라 달라질 수 있는 요금을 설명하는 데 사용됩니다. 요일 또는 일년 중 특정 날짜. 시간대는 [fare_leg_rules.txt](#fare_leg_rulestxt)의 요금 상품과 연결될 수 있습니다.<br> 
 동일한 `timeframe_group_id` 및 `service_id` 값에 대해 시간 간격이 중복되어서는 안 됩니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `timeframe_group_id` | 아이디 | **필수** | 기간 또는 기간 세트를 식별합니다. | 
 | `start_time` ` | 시간 | **조건부 필수** | 기간의 시작을 정의합니다. 간격에는 시작 시간이 포함됩니다.<br> `24:00:00`보다 큰 값은 금지됩니다. `start_time` 의 빈 값은 `00:00:00`으로 간주됩니다.<br><br> 조건부 필수:<br> - `timeframes.end_time`이 정의된 경우 **필수**입니다.<br> - **금지됨** 그렇지 않으면 | 
 | `end_time` | 시간 | **조건부 필수** | 기간의 끝을 정의합니다. 간격에는 종료 시간이 포함되지 않습니다.<br> `24:00:00`보다 큰 값은 금지됩니다. `end_time 의 빈 값은 `24:00:00`으로 간주됩니다.<br><br> 조건부 필수:<br> - `timeframes.start_time`이 정의된 경우 **필수**입니다.<br> - **금지됨** 그렇지 않으면 | 
 | `service_id` | `calendar.service_id` 또는 `calendar_dates.service_id`를 참조하는 외부 ID | **필수** | 기간이 적용되는 날짜 집합을 식별합니다. | 
 
#### 시간대 현지 시간 의미 
 - [timeframes.txt](#timeframestxt)에 대해 요금 이벤트 시간을 평가할 때 이벤트 시간은 `에 의해 결정된 현지 시간대를 사용하여 현지 시간으로 계산됩니다. stop_timezone`(지정된 경우 요금 이벤트에 대한 정류장 또는 상위 역). 지정하지 않으면 피드의 agency 시간대를 대신 사용해야 합니다. 
 - "현재 날짜"는 요금 이벤트 시간의 현재 date 이며 현지 시간대를 기준으로 계산됩니다. "현재 날짜"는 운임 구간 여행의 서비스 날짜와 다를 수 있으며, 특히 자정 이후로 연장되는 여행의 경우 더욱 그렇습니다. 
 - 요금 이벤트의 ’시간대’는 GTFS 시간 필드 유형 의미 체계를 사용하여 ’현재 날짜’를 기준으로 계산됩니다. 
 
### 운임 미디어 .txt 
 
 파일: **선택 사항** 
 
 기본 키(`fare_media_id`) 
 
 운임 상품을 사용하는 데 사용할 수 있는 다양한 운임 미디어를 설명하려면. 요금 미디어는 요금 상품의 표시 및/또는 검증에 사용되는 물리적 또는 가상 보유자입니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `fare_media_id` | 고유 ID | **필수** | 요금 미디어를 식별합니다. | 
 | `fare_media_name` | Text | 선택사항 | 요금 미디어의 이름입니다.<br><br> 교통카드(`fare_media_type =2`) 또는 모바일 앱(`fare_media_type =4`)인 요금 미디어의 경우 `fare_media_name`이 포함되어야 하며 이를 전달하는 조직에서 사용하는 승객용 이름과 일치해야 합니다. | 
 | `fare_media_type` | 열거형 | **필수** | 요금 미디어의 유형입니다. 유효한 옵션은 다음과 같습니다.<br><br> `0` - 없음. 실제 티켓을 제공하지 않고 운전사 또는 차장에게 현금을 지불하는 등 요금 상품 구매 또는 확인과 관련된 요금 매체가 없는 경우에 사용됩니다.<br> ’`1`’ - 승객이 미리 구매한 일정 횟수의 여행 또는 정해진 기간 내에 무제한 여행을 할 수 있는 실제 종이 항공권입니다.<br> `2` - 티켓, 패스 또는 금전적 가치가 저장된 실제 교통 카드입니다.<br> `3` - 계정 기반 티켓팅을 위한 개방형 루프 토큰 컨테이너인 cEMV(비접촉식 Europay, Mastercard 및 Visa).<br> `4` - 가상 교통카드, 티켓, 패스 또는 금전적 가치를 저장한 모바일 앱입니다.| 
 
### fare_products.txt 
 
 파일: **선택 사항** 
 
 기본 키(`fare_product_id`, `fare_media_id`) 
 
 구매할 수 있는 요금 범위를 설명하는 데 사용됩니다. 승객별로 또는 환승 비용과 같이 여러 구간으로 구성된 여행의 총 요금을 계산할 때 고려됩니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `fare_product_id` | 아이디 | **필수** | 요금 상품 또는 요금 상품 세트를 식별합니다.<br><br> [fare_products.txt](#fare_productstxt)의 여러 기록은 동일한 `fare_product_id`를 공유할 수 있으며, 이 경우 다른 파일에서 참조할 때 해당 ID를 가진 모든 기록이 검색됩니다.<br><br> 여러 레코드가 동일한 `fare_product_id`를 공유할 수 있지만 `fare_media_id 는 서로 다를 수 있습니다. 이는 잠재적으로 가격이 다를 수 있는 운임 제품을 사용하는 데 사용할 수 있는 다양한 방법을 나타냅니다. | 
 | `fare_product_name_이름 ` | Text | 선택사항 | 승객에게 표시되는 요금 상품의 이름입니다. | 
 | `fare_media_id` | `fare_media.fare_media_id`를 참조하는 외부 ID | 선택사항 | 여행 중 요금 상품을 사용하기 위해 사용할 수 있는 요금 미디어를 식별합니다. `fare_media_id`가 비어 있으면 요금 미디어를 알 수 없는 것으로 간주됩니다.| 
 | `amount` | 통화 amount | **필수** | 운임상품의 가격입니다. 환승 할인을 나타내기 위해 음수일 수 있습니다. 무료 요금 상품을 나타내기 위해 0이 될 수 있습니다. | 
 | `currency` | 통화 코드 | **필수** | 운임 제품 비용의 currency. | 
 
 
### fare_leg_rules.txt 
 
 파일: **선택 사항** 
 
 기본 키(`network_id, from_area_id, to_area_id, from_timeframe_group_id, to_timeframe_group_id, fare_product_id`) 
 
 요금 규정 개별 여행 구간에 적합합니다. 
 
 승객이 여행할 구간과 일치하는 규칙을 찾기 위해 파일의 모든 기록을 필터링하여 [`fare_leg_rules.txt`](#fare_leg_rulestxt)의 요금을 쿼리해야 합니다. 
 
 구간 비용을 처리하려면: 
 
 1. 파일 [fare_leg_rules.txt](#fare_leg_rulestxt)는 여행 특성을 정의하는 필드로 필터링해야 하며 이러한 필드는 다음과 같습니다. 
 - `fare_leg_rules.network_id` 
 - `fare_leg_rules.from_area_id ` 
 - ` 요금_leg_rules.to_area_id ` 
 - `fare_leg_rules.from_timeframe_group_id` 
 - `fare_leg_rules.to_timeframe_group_id` 
<br/> 
 
 2. 여행 특성에 따라 구간이 [fare_leg_rules.txt](#fare_leg_rulestxt)의 기록과 정확히 일치하는 경우 해당 기록을 처리하여 구간 비용을 결정해야 합니다. 이 파일은 빈 의미 또는 규칙_우선순위라는 두 가지 방법으로 빈 항목을 처리합니다. 
<br/> 
 
 3. 정확한 일치 항목이 발견되지 않고 `rule_priority` 필드가 존재하지 않는 경우 `fare_leg_rules.network_id`, `fare_leg_rules.from_area_id` 및 `fare_leg_rules.to_area_id`의 빈 항목을 확인하여 처리해야 합니다. 구간 비용: 
 - `fare_leg_rules.network_id`의 빈 항목은 ` Fare_leg_rules에 나열된 네트워크를 제외하고 [routes.txt](#routestxt) 또는 [networks.txt](#networkstxt)에 정의된 모든 네트워크에 해당합니다. fare_leg_rules.network_id` 
 
 - `fare_leg_rules.from_area_id `의 빈 항목은 ` fare_leg_rules.from_area_id `에 나열된 항목을 제외한 ` areas.area_id `에 정의된 모든 영역에 해당합니다. ` 
 - ` fare_leg_rules.to_area_id `의 빈 항목은 해당 ` fare_leg_rules.to_area_id 에 나열된 지역을 제외한 ` areas.area_id 에 정의된 모든 지역 
<br/> 
 
 4. ’rule_priority’ 필드가 존재하는 경우 
 - ’ fare_leg_rules.network_id’의 빈 항목은 해당 구간의 네트워크가 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. 
 - `fare_leg_rules.from_area_id 의 빈 항목은 구간의 departure 영역이 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. 
 - `fare_leg_rules.to_area_id 의 빈 항목은 구간의 arrival 지역이 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. 
<br/> 
 
 5. 구간이 위에 설명된 규칙과 일치하지 않는 경우 요금은 알 수 없습니다. 
 
<br/> 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `leg_group_id` | 아이디 | 선택사항 | [fare_leg_rules.txt](#fare_leg_rulestxt)의 항목 그룹을 식별합니다.<br><br> `fare_transfer_rules.from_leg_group_id`와 `fare_transfer_rules.to_leg_group_id` 사이의 요금 환승 규칙을 설명하는 데 사용됩니다.<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt)의 여러 항목이 동일한 `fare_leg_rules.leg_group_id`에 속할 수 있습니다.<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt)(`fare_leg_rules.leg_group_id` 제외)의 동일한 항목은 여러 `fare_leg_rules.leg_group_id`에 속해서는 안 됩니다.| 
 | `network_id` | `routes.network_id` 또는 `networks.network_id `|를 참조하는 외부 ID 선택사항 | 요금 구간 규칙이 적용되는 경로 네트워크를 식별합니다.<br><br> `rule_priority` 필드가 존재하지 않고 필터링 중인 ` network_id `와 일치하는 ` fare_leg_rules.network_id ` 값이 없는 경우 기본적으로 비어 있는 ` fare_leg_rules.network_id`가 일치됩니다.<br><br> `fare_leg_rules.network_id `의 빈 항목은 ` fare_leg_rules.network_id `에 나열된 네트워크를 제외하고 [routes.txt](#routestxt) 또는 [networks.txt](#networkstxt)에 정의된 모든 네트워크에 해당합니다.<br><br> 파일에 ’rule_priority’ 필드가 있는 경우 빈 ’ fare_leg_rules.network_id’는 해당 구간의 경로 네트워크가 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. | 
 | `from_area_id| `areas.area_id 를 참조하는 외부 ID | 선택사항 | departure 지역을 식별합니다.<br><br> `rule_priority` 필드가 존재하지 않고 필터링되는 ` area_id 와 일치하는 ` fare_leg_rules.from_area_id 값이 없으면 기본적으로 비어 있는 ` fare_leg_rules.from_area_id 가 일치됩니다.<br><br> `fare_leg_rules.from_area_id 의 빈 항목은 ` fare_leg_rules.from_area_id 에 나열된 영역을 제외하고 ` areas.area_id 에 정의된 모든 영역에 해당합니다.<br><br> 파일에 ’rule_priority’ 필드가 있는 경우 빈 ’ fare_leg_rules.from_area_id’는 구간의 departure 영역이 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. | 
 | `to_area_id| `areas.area_id 를 참조하는 외부 ID | 선택사항 | arrival 지역을 식별합니다.<br><br> `rule_priority` 필드가 존재하지 않고 필터링되는 ` area_id 와 일치하는 ` fare_leg_rules.to_area_id 값이 없으면 기본적으로 빈 ` fare_leg_rules.to_area_id 가 일치됩니다.<br><br> `fare_leg_rules.to_area_id 의 빈 항목은 ` fare_leg_rules.to_area_id 에 나열된 항목을 제외하고 ` areas.area_id 에 정의된 모든 영역에 해당합니다.<br><br> 파일에 ’rule_priority’ 필드가 있는 경우 비어 있는 ’ fare_leg_rules.to_area_id’는 구간의 arrival 지역이 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. | 
 | `from_timeframe_group_id| `timeframes.timeframe_group_id 를 참조하는 외부 ID | 선택사항 | 요금 구간 시작 시 요금 확인 이벤트의 기간을 정의합니다.<br><br> 요금 구간의 "시작 시간"은 이벤트가 발생할 예정인 시간입니다. 예를 들어, 시간은 승객이 탑승하고 요금을 확인하는 요금 구간이 시작되는 버스의 예정된 departure 시간일 수 있습니다. 아래 규칙 일치 의미 체계의 경우 시작 시간은 [timeframes.txt](#timeframestxt)의 [Local Time Semantics](#timeframe-local-time-semantics)에 따라 결정된 현지 시간으로 계산됩니다. 해당하는 경우 시간대 확인을 위해 요금 구간 departure 이벤트의 정류장 또는 역을 사용해야 합니다.<br><br> `from_timeframe_group_id`를 지정하는 요금 구간 규칙의 경우 해당 규칙은 t 같은 경우 특정 구간과 일치합니다.

여기에는 다음 조건이 모두 충족되는 [timeframes.txt](#timeframestxt)에 하나 이상의 레코드가 있습니다.<br> - `timeframe_group_id` 값은 `from_timeframe_group_id` 값과 같습니다.<br> - 기록의 `service_id`로 식별되는 날짜 세트에는 요금 구간 시작 시간의 "현재 날짜"가 포함됩니다.<br> - 요금 구간 시작 시간의 "시간대"는 기록의 `timeframes.start_time` 값보다 크거나 같고 `timeframes.end_time` 값보다 작습니다.<br><br> 비어 있는 `fare_leg_rules.from_timeframe_group_id 는 구간의 시작 시간이 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. | 
 | `to_timeframe_group_id` | `timeframes.timeframe_group_id 를 참조하는 외부 ID | 선택사항 | 요금 구간이 끝날 때 요금 확인 이벤트의 기간을 정의합니다.<br><br> 요금 구간의 "종료 시간"은 이벤트가 발생하도록 예정된 시간입니다. 예를 들어, 시간은 승객이 내리고 요금을 확인하는 요금 구간 끝에 버스가 예정된 arrival 시간일 수 있습니다. 아래 규칙 일치 의미 체계의 경우 종료 시간은 [timeframes.txt](#timeframestxt)의 [Local Time Semantics](#timeframe-local-time-semantics)에 따라 결정된 현지 시간으로 계산됩니다. 적절한 경우 시간대 확인을 위해 요금 구간 arrival 이벤트의 정류장 또는 역을 사용해야 합니다.<br><br> ’ to_timeframe_group_id’를 지정하는 요금 구간 규칙의 경우, 다음 조건이 모두 충족되는 [timeframes.txt](#timeframestxt)에 하나 이상의 기록이 있는 경우 해당 규칙은 특정 구간과 일치합니다.<br> - `timeframe_group_id` 값은 `to_timeframe_group_id` 값과 같습니다.<br> - 기록의 `service_id`로 식별되는 날짜 세트에는 요금 구간 종료 시간의 "현재 날짜"가 포함됩니다.<br> - 요금 구간 종료 시간의 "시간"은 기록의 `timeframes.start_time` 값보다 크거나 같고 `timeframes.end_time` 값보다 작습니다.<br><br> 비어 있는 `fare_leg_rules.to_timeframe_group_id 는 구간의 종료 시간이 이 규칙의 일치에 영향을 미치지 않음을 나타냅니다. | 
 | `fare_product_id` | `fare_products.fare_product_id`를 참조하는 외부 ID | **필수** | 해당 구간을 여행하는 데 필요한 운임 상품입니다. | 
 | `규칙_우선순위` | 음수가 아닌 정수 | 선택사항 | 일치 규칙이 다리에 적용되는 우선 순위를 정의하여 특정 규칙이 다른 규칙보다 우선하도록 허용합니다. `fare_leg_rules.txt 의 여러 항목이 일치하면 `rule_priority` 값이 가장 높은 규칙 또는 규칙 집합이 선택됩니다.<br><br> `rule_priority`의 빈 값은 0으로 처리됩니다. | 
 
### fare_transfer_rules.txt 
 
 파일: **선택 사항** 
 
 기본 키(`from_leg_group_id, to_leg_group_id, fare_product_id, transfer_count, duration_limit`) 
 
 구간 간 transfers 요금 규정 [`fare_leg_rules.txt`](#fare_leg_rulestxt)에 정의된 여행. 
 
 다구간 여행 비용을 처리하려면: 
 
 1. `fare_leg_rules.txt`에 정의된 해당 운임 구간 그룹은 승객의 여정을 기반으로 모든 개별 여행 구간에 대해 결정되어야 합니다. 
 2. 파일 [fare_transfer_rules.txt](#fare_transfer_rulestxt)는 환승 특성을 정의하는 필드로 필터링해야 합니다. 해당 필드는 다음과 같습니다: 
 - `fare_transfer_rules.from_leg_group_id` 
 - `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 
 3. 환승의 특성상 [fare_transfer_rules.txt](#fare_transfer_rulestxt)의 기록과 환승 내용이 정확하게 일치하는 경우 해당 기록을 처리하여 환승 비용을 결정해야 합니다. 
 4. 정확히 일치하는 항목이 없으면 `from_leg_group_id` 또는 `to_leg_group_id`의 빈 항목을 확인하여 환승 비용을 처리해야 합니다. 
 - `fare_transfer_rules.from_leg_group_id`의 빈 항목은 정의된 모든 구간 그룹에 해당합니다. `fare_leg_rules.leg_group_id`에 나열된 항목을 제외하고 `fare_transfer_rules.from_leg_group_id`에서 
 - `fare_transfer_rules.to_leg_group_id `의 빈 항목은 ` fare_transfer_rules.to_leg_group_id ` 에 정의된 모든 구간 그룹에 해당합니다.<br/> 
<br/> 
 5. 전송이 위에 설명된 규칙 중 어느 것과도 일치하지 않는 경우 전송 계약이 없으며 다리는 별개로 간주됩니다. 
 
<br/> 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `from_leg_group_id| `fare_leg_rules.leg_group_id 를 참조하는 외부 ID | 선택사항 | 환승 전 운임 구간 규칙 그룹을 식별합니다.<br><br> 필터링 중인 ` leg_group_id 와 일치하는 ` fare_transfer_rules.from_leg_group_id ` 값이 없으면 기본적으로 비어 있는 ` fare_transfer_rules.from_leg_group_id`가 일치됩니다.<br><br> `fare_transfer_rules.from_leg_group_id`의 빈 항목은 `fare_leg_rules.leg_group_id`에 나열된 항목을 제외하고 `fare_transfer_rules.from_leg_group_id`에 정의된 모든 구간 그룹에 해당합니다. 
 | `to_leg_group_id| `fare_leg_rules.leg_group_id 를 참조하는 외부 ID | 선택사항 | 환승 후 운임 구간 규칙 그룹을 식별합니다.<br><br> 필터링 중인 ` leg_group_id 와 일치하는 ` fare_transfer_rules.to_leg_group_id 값이 없으면 기본적으로 비어 있는 ` fare_transfer_rules.to_leg_group_id`가 일치됩니다.<br><br> `fare_transfer_rules.to_leg_group_id`의 빈 항목은 `fare_leg_rules.leg_group_id`에 나열된 항목을 제외하고 `fare_transfer_rules.to_leg_group_id`에 정의된 모든 구간 그룹에 해당합니다 | 
 | `transfer_count` | 0이 아닌 정수 | **조건부 금지** | 전송 규칙이 적용될 수 있는 연속 transfers 횟수를 정의합니다.<br><br> 유효한 옵션은 다음과 같습니다.<br> `-1` - 제한이 없습니다.<br> ’`1`’ 이상 - 전송 규칙이 확장될 수 있는 transfers 수를 정의합니다.<br><br> 하위 여정이 서로 다른 `transfer_count 를 가진 여러 레코드와 일치하는 경우 하위 여정의 현재 전송 횟수보다 크거나 같은 최소 `transfer_count`를 갖는 규칙이 선택됩니다.<br><br> 조건부 금지:<br> - `fare_transfer_rules.from_leg_group_id`가 `fare_transfer_rules.to_leg_group_id`와 동일하지 않은 경우 **금지됨**.<br> - `fare_transfer_rules.from_leg_group_id 가 `fare_transfer_rules.to_leg_group_id`와 동일한 경우 **필수**입니다. | 
 | `duration_limit` | 양의 정수 | 선택사항 | 전송 기간 제한을 정의합니다.<br><br> 초 단위의 정수 증분으로 표현되어야 합니다.<br><br> 기간 제한이 없는 경우 `fare_transfer_rules.duration_limit 는 비어 있어야 합니다. | 
 | `duration_limit_type` | 열거형 | **조건부 필수** | `fare_transfer_rules.duration_limit 의 상대적 시작과 끝을 정의합니다.<br><br> 유효한 옵션은 다음과 같습니다.<br> `0` - 현재 구간의 departure 요금 유효성 검사와 다음 구간의 arrival 요금 유효성 검사 사이입니다.<br> ’`1`’ - 현재 구간의 departure 요금 유효성 검사와 다음 구간의 departure 요금 유효성 검사 사이입니다.<br> `2` - 현재 구간의 arrival 요금 유효성 검사와 다음 구간의 departure 요금 유효성 검사 사이입니다.<br> `3` - 현재 구간의 arrival 요금 유효성 검사와 다음 구간의 arrival 요금 유효성 검사 사이입니다.<br><br> 조건부 필수:<br> - `fare_transfer_rules.duration_limit`가 정의된 경우 **필수**입니다.<br> - `fare_transfer_rules.duration_limit`가 비어 있는 경우 **금지됨**. | 
 | `fare_transfer_type` | 열거형 | **필수** | 여정 중 구간 간 환승 비용 처리 방법을 나타냅니다.<br> ![](../../assets/2-leg.svg)<br> 유효한 옵션은 다음과 같습니다.<br> `0` - 출발 구간 `fare_leg_rules.fare_product_id` + `fare_transfer_rules.fare_product_id`; A + AB.<br> `1` - 출발 구간 `fare_leg_rules.fare_product_id` 플러스 `fare_transfer_rules.fare_product_id` 플러스 구간 ` 요금_ fare_leg_rules.fare_product_id`; A + AB + B.<br> `2` - `fare_transfer_rules.fare_product_id`; AB.<br><br> 여정의 여러 transfers 간 비용 처리 상호 작용:<br> ![](../../assets/3-leg.svg)<br><table><thead><tr><th> `fare_transfer_type`</th><th> 처리 A > B</th><th> 처리 B > C</th></tr></thead><tbody><tr><td> `0`</td><td> A + AB</td><td> S + 기원전</td></tr><tr><td> `1`</td><td> A + AB + B</td><td> 에스 + 기원전 + C</td></tr><tr><td> `2`</td><td> AB</td><td> S + 기원전</td></tr></tbody></table> 여기서 S는 이전 구간과 이전의 총 처리 비용을 나타냅니다. | 
 | `fare_product_id` | `fare_products.fare_product_id`를 참조하는 외부 ID | 선택사항 | 두 운임 구간 간 환승에 필요한 운임 상품입니다. 비어 있으면 전송 규칙 비용은 0입니다.| 
 
 
### areas.txt 
 
 파일: **선택 사항** 
 
 기본 키(`area_id) 
 
 영역 식별자를 정의합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `area_id` | 고유 ID | **필수** | 영역을 식별합니다. [areas.txt](#areastxt)에서 고유해야 합니다. | 
 | `area_name` | Text | **선택사항** | 라이더에게 표시되는 지역의 이름입니다. | 
 
### stop_areas.txt 
 
 파일: **선택 사항** 
 
 기본 키(`*`) 
 
 [stops.txt](#stopstxt)에서 지역에 stops. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | ` area_id| `areas.area_id 를 참조하는 외부 ID | **필수** | 하나 이상의 `stop_id` 가 속하는 영역을 식별합니다. 동일한 `stop_id` 여러 `area_id 에 정의될 수 있습니다. | 
 | `stop_id` | `stops.stop_id 를 참조하는 외부 ID | **필수** | 정류장을 식별합니다. 이 필드에 역(예: `stops.location_type=1 가진 정류장)이 정의된 경우, 이 역이 ` 정류장 으로 정의된 ` stops.location_type=0 을 가진 모든 정류장(즉, `stops.location_type=0`을 가진 모든 stops )이 이 필드에 정의된 것으로 가정됩니다. stops.parent_station)은 동일한 영역의 일부입니다. 이 동작은 플랫폼을 다른 영역에 할당하여 무시할 수 있습니다. | 
 
### 네트워크 .txt 
 
 파일: **조건부 금지** 
 
 기본 키(`network_id`) 
 
 요금 구간 규칙에 적용되는 네트워크 식별자를 정의합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `network_id` | 고유 ID | **필수** | 네트워크를 식별합니다. [networks.txt](#networkstxt)에서 고유해야 합니다. | 
 | `network_name` | Text | **선택사항** | 지역 agency 및 승객이 사용하는 요금 구간 규칙을 적용하는 네트워크의 이름입니다. 
 
### Route_networks.txt 
 
 파일: **조건부 금지** 
 
 기본 키(`route_id` ) 
 
 [routes.txt](#routestxt)에서 다음으로 routes 할당합니다. 네트워크. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | ` network_id` | `networks.network_id 를 참조하는 외부 ID | **필수** | 하나 이상의 `route_id` 가 속하는 네트워크를 식별합니다. `route_id` 하나의 `network_id 에만 정의될 수 있습니다. | 
 | `route_id` | `routes.route_id`를 참조하는 외부 ID | **필수** | 경로를 식별합니다. | 
 
### shapes.txt 
 
 파일: **선택 사항** 
 
 기본 키(`shape_id`, `shape_pt_sequence`) 
 
 도형은 vehicle 도로를 따라 이동하는 경로를 설명합니다. 경로 정렬이며 shapes.txt 파일에 정의되어 있습니다. 모양은 여행과 연관되어 있으며 vehicle 순서대로 통과하는 일련의 지점으로 구성됩니다. 모양이 정류장의 위치를 ​​정확하게 가로챌 필요는 없지만 이동 중 모든 정류장은 해당 이동에 대한 shape 의 작은 거리 내에 있어야 합니다. 즉, shape 점을 연결하는 직선 세그먼트에 가깝습니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `shape_id` | 아이디 | **필수** | shape 을 식별합니다. | 
 | `shape_pt_lat| 위도 | **필수** | shape 점의 위도입니다. [shapes.txt](#shapestxt)의 각 레코드는 shape 정의하는 데 사용되는 shape 점을 나타냅니다. | 
 | ` shape_pt_lon` | 경도 | **필수** | shape 포인트의 경도입니다. | 
 | `shape_pt_sequence` | 음수가 아닌 정수 | **필수** | shape 점이 연결되어 shape 형성하는 순서입니다. 값은 이동 중에 증가해야 하지만 연속적일 필요는 없습니다.<hr> *예: "A_shp" shape 정의에 세 개의 점이 있는 경우 [shapes.txt](#shapestxt) 파일에는 shape 정의하는 다음 레코드가 포함될 수 있습니다.*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence`<br> `A_shp,37.61956,-122.48161,0`<br> `A_shp,37.64430,-122.41070,6`<br> `A_shp,37.65863,-122.30839,11` | 
 | `shape_dist_traveled` | 음수가 아닌 float 소수점 | 선택사항 | 첫 번째 shape 지점에서 이 레코드에 지정된 지점까지 shape 따라 이동한 실제 거리입니다. 여행 계획자가 지도에 shape 의 정확한 부분을 표시하는 데 사용됩니다. 값은 `shape_pt_sequence 에 따라 증가해야 합니다. 경로를 따라 역방향 이동을 표시하는 데 사용해서는 안 됩니다. 거리 단위는 [stop_times.txt](#stop_timestxt)에 사용된 단위와 일치해야 합니다.<br><br> 순환 또는 인라인이 있는 routes 에 권장됩니다( vehicle 한 번의 이동으로 선형의 동일한 부분을 건너거나 이동함). <br><img src="../../../assets/inlining.svg" width=200px style="display: block; margin-left: auto; margin-right: auto;"><br> vehicle 이동 중에 특정 지점에서 경로 정렬을 되돌리거나 교차하는 경우 `shape_dist_traveled[shapes.txt](#shapestxt) 정렬의 지점 부분이 [stop_times.txt 의 기록과 어떻게 일치하는지 명확히 하는 데 중요합니다.](#stop_timestxt).<hr> *예: 버스가 A_shp에 대해 위에 정의된 세 지점을 따라 이동하는 경우 추가 `shape_dist_traveled 값(여기에 킬로미터로 표시됨)은 다음과 같습니다.*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shape_dist_traveled`<br> `A_shp,37.61956,-122.48161,0,0`<br> `A_shp,37.64430,-122.41070,6,6.8310`<br> `A_shp,37.65863,-122.30839,11,15.8765` | 
 
### frequencies.txt 
 
 파일: **선택 사항** 
 
 기본 키(`trip_id`, `start_time`) 
 
 [Frequency.txt](#frequencytxt)는 다음을 나타냅니다. 정기적인 운행 간격(여행 간 시간)으로 운행되는 여행입니다. 이 파일은 두 가지 다른 유형의 서비스를 나타내는 데 사용될 수 있습니다. 
 
 * 서비스가 하루 종일 고정된 일정을 따르지 않는 빈도 기반 서비스(`exact_times`=`0`). 대신, 운영자는 여행을 위해 미리 결정된 간격을 엄격하게 유지하려고 시도합니다. 
 * 지정된 기간 동안 이동에 대해 정확히 동일한 운행 간격을 갖는 일정 기반 서비스(`exact_times`= `1`)의 압축 표현입니다. 일정 기반 서비스 운영자는 일정을 엄격하게 준수하려고 노력합니다. 
 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `trip_id` | ’`trips.trip_id` 참조하는 외국인 ID | **필수** | 지정된 서비스 간격이 적용되는 이동을 식별합니다. | 
 | `start_time` ` | 시간 | **필수** | 첫 번째 vehicle 지정된 간격으로 이동의 첫 번째 정류장에서 출발하는 시간입니다. | 
 | `end_time` | 시간 | **필수** | 여행의 첫 번째 정류장에서 서비스가 다른 운행 간격으로 변경(또는 중단)되는 시간입니다. | 
 | `headway_secs` | 양의 정수 | **필수** | `start_time` 및 `end_time 으로 지정된 시간 간격 동안 이동을 위해 동일한 정류장(배차 간격)에서 출발하는 사이의 시간(초)입니다. 동일한 이동에 대해 여러 배차간격을 정의할 수 있지만 중복되어서는 안 됩니다. 새로운 운행 간격은 이전 운행 간격이 끝나는 정확한 시간에 시작될 수 있습니다. | 
 | ’`exact_times`’ | 열거형 | 선택사항 | 여행에 대한 서비스 유형을 나타냅니다. 자세한 내용은 파일 설명을 참조하세요. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 빈도 기반 이동입니다.<br> `1` - 하루 종일 정확히 동일한 운행 간격을 갖는 일정 기반 이동입니다. 이 경우 `end_time 값은 마지막으로 원하는 이동 `start_time` 보다 커야 하지만 마지막으로 원하는 이동 start_time + `headway_secs` 보다 작아야 합니다. | 
 
### transfers.txt 
 
 파일: **선택 사항** 
 
 기본 키(`from_stop_id`, `to_stop_id`, `from_trip_id`, `to_trip_id`, `from_route_id`, `to_route_id`) 
 
 여행 일정을 계산할 때 GTFS 사용하는 애플리케이션은 허용 시간과 정류장 근접성을 기준으로 transfers 보간합니다. [Transfers.txt](#transferstxt)는 선택한 transfers 에 대한 추가 규칙 및 재정의를 지정합니다. 
 
 필드 `from_trip_id`, `to_trip_id`, `from_route_id` 및 `to_route_id`는 환승 규칙에 대해 더 높은 수준의 구체성을 허용합니다. `from_stop_id` 및 `to_stop_id`와 함께 특이성 순위는 다음과 같습니다. 
 
 1. `trip_id` 모두 `from_trip_id` 및 `to_trip_id`로 정의됩니다. 
 2. 하나의 `trip_id` 및 `route_id` 세트가 정의되었습니다: (`from_trip_id` 및 `to_route_id`) 또는 (`from_route_id` 및 `to_trip_id`). 
 3. 하나의 `trip_id` 정의되었습니다: `from_trip_id` 또는 `to_trip_id`. 
 4. `route_id` 모두 정의되었습니다: `from_route_id` 및 `to_route_id`. 
 5. 하나의 `route_id` 정의되었습니다: `from_route_id` 또는 `to_route_id`. 
 6. `from_stop_id` 및 `to_stop_id`만 정의됨: 경로 또는 이동 관련 필드가 설정되지 않았습니다. 
 
 도착 여행과 출발 여행의 주어진 순서 쌍에 대해 이 두 여행 사이에 적용되는 가장 구체적인 환승이 선택됩니다. 한 쌍의 여행에 대해 적용할 수 있는 최대 특이성을 동일하게 갖는 두 번의 transfers 있어서는 안 됩니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `from_stop_id| `stops.stop_id 를 참조하는 외부 ID | **조건부 필수** | routes 간 연결이 시작되는 정류장 또는 역을 식별합니다. 이 필드가 역을 참조하는 경우 환승 규칙은 해당 역의 모든 하위 stops 에 적용됩니다. `transfer_types` 4, 5. 에는 스테이션 참조가 금지되어 있습니다. | 
 | `to_stop_id| `stops.stop_id 를 참조하는 외부 ID | **조건부 필수** | routes 간 연결이 끝나는 정류장이나 역을 식별합니다. 이 필드가 역을 참조하는 경우 환승 규칙은 모든 하위 stops 에 적용됩니다. `transfer_types` 4, 5. 에는 스테이션 참조가 금지되어 있습니다. | 
 | `from_route_id| `routes.route_id`를 참조하는 외부 ID | 선택사항 | 연결이 시작되는 경로를 식별합니다.<br><br> `from_route_id`가 정의된 경우 지정된 `from_stop_id`에 대한 경로로 도착하는 이동에 환승이 적용됩니다.<br><br> `from_trip_id 와 `from_route_id 가 모두 정의된 경우 `trip_id` 는 `route_id` 에 속해야 하며 `from_trip_id 가 우선 적용됩니다. | 
 | `to_route_id` | `routes.route_id`를 참조하는 외부 ID | 선택사항 | 연결이 끝나는 경로를 식별합니다.<br><br> `to_route_id`가 정의된 경우 지정된 `to_stop_id`에 대한 경로의 출발 이동에 환승이 적용됩니다.<br><br> `to_trip_id 와 `to_route_id 가 모두 정의된 경우 `trip_id` 는 `route_id` 에 속해야 하며 `to_trip_id`가 우선 적용됩니다. | 
 | `from_trip_id` | ’`trips.trip_id` 참조하는 외국인 ID | **조건부 필수** | routes 간 연결이 시작되는 이동을 식별합니다.<br><br> `from_trip_id`가 정의된 경우 지정된 `from_stop_id`에 대해 도착하는 이동에 환승이 적용됩니다.<br><br> `from_trip_id 와 `from_route_id 가 모두 정의된 경우 `trip_id` 는 `route_id` 에 속해야 하며 `from_trip_id 가 우선 적용됩니다. `transfer_type 이 `4` 또는 `5`인 경우 필수입니다. | 
 | `to_trip_id` | ’`trips.trip_id` 참조하는 외국인 ID | **조건부 필수** | routes 간의 연결이 끝나는 이동을 식별합니다.<br><br> `to_trip_id`가 정의된 경우 지정된 `to_stop_id`에 대한 출발 이동에 환승이 적용됩니다.<br><br> `to_trip_id 와 `to_route_id 가 모두 정의된 경우 `trip_id` 는 `route_id` 에 속해야 하며 `to_trip_id`가 우선 적용됩니다. `transfer_type 이 `4` 또는 `5`인 경우 필수입니다. | 
 | `transfer_type` | 열거형 | **필수** | 지정된(`from_stop_id`, `to_stop_id`) 쌍에 대한 연결 유형을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> `0` 또는 비어 있음 - routes 간 권장 환승 지점입니다.<br> `1` - 두 routes 사이의 정기 환승 지점입니다. 출발 vehicle 도착 차량을 기다리고 승객이 routes 간 환승을 위한 충분한 시간을 확보할 것으로 예상됩니다.<br> `2` - 환승에는 연결을 보장하기 위해 arrival 과 departure 사이에 최소 시간 amount 필요합니다. 환승에 소요되는 시간은 ` min_transfer_time`으로 지정됩니다.<br> `3` - 해당 위치에서는 routes 간 환승이 불가능합니다.<br> `4` - 승객은 동일한 vehicle 에 탑승하여 한 여행에서 다른 여행으로 환승할 수 있습니다("좌석 환승"). 이 환승 유형에 대한 자세한 내용은 [아래](#linked-trips)를 참조하세요.<br> `5` - 연속 여행 사이에는 좌석 내 transfers 허용되지 않습니다. 승객은 vehicle 에서 하차한 후 다시 탑승해야 합니다. 이 환승 유형에 대한 자세한 내용은 [아래](#linked-trips)를 참조하세요. | 
 | `min_transfer_time | 음수가 아닌 정수 | 선택사항 | 지정된 stops 에서 routes 간 환승을 허용하는 데 사용할 수 있는 시간(초)입니다. ’ min_transfer_time’은 각 경로의 일정 변동을 허용하는 버퍼 시간을 포함하여 일반적인 승객이 두 stops 사이를 이동할 수 있을 만큼 충분해야 합니다. | 
 
#### 연계 여행 
 
 다음은 좌석 transfers 여부에 관계없이 여행을 함께 연결하는 데 사용되는 ` transfer_type=4 ` 및 `=5`에 적용됩니다. 
 
 함께 연결된 여행은 반드시 동일한 vehicle 으로 운행되어야 합니다. vehicle 다른 차량과 연결되거나 연결 해제될 수 있습니다. 
 
 연결된 여행 환승과 block_id 모두 제공되고 결과가 충돌하는 경우 연결된 여행 환승을 사용해야 합니다. 
 
 `from_trip_id`의 마지막 정류장은 지리적으로 `to_trip_id `의 첫 번째 정류장과 가까워야 하며 ` from_trip_id `의 마지막 arrival 시간은 ` to_trip_id `의 첫 번째 departure 시간보다 빠르지만 가까워야 합니다. ` from_trip_id `의 마지막 arrival 시간은 ` to_trip_id ` 이동이 다음 서비스일에 발생하는 경우 ` to_trip_id `의 첫 departure 시간보다 늦을 수 있습니다. 
 
 여행은 일반적인 경우 1:1로 연결될 수 있지만 더 복잡한 여행 연속을 나타내기 위해 1:n, n-1 또는 n-n으로 연결될 수도 있습니다. 예를 들어, 두 개의 기차 여행(아래 다이어그램의 여행 A와 여행 B)은 공통 역에서 vehicle 연결 작업 후 단일 기차 여행(여행 C)으로 병합될 수 있습니다. 
 
 - 1-to-n 계속해서, 각 ` to_trip_id `에 대한 ` trips.service_id `는 동일해야 합니다. 
 - n-to-1 연속에서 각 ` from_trip_id `에 대한 ` trips.service_id `는 동일해야 합니다. 
 - n 대 n 연속은 두 제약 조건을 모두 준수해야 합니다. 
 - ` trip.service_id`가 서비스 날짜에 중복되어서는 안 된다는 조건 하에 여행은 여러 개의 별개 연속의 일부로 함께 연결될 수 있습니다. 
 
<pre> 
 여행 A 
 ───────────────────\ 
 \ 여행 C 
 ───────────── 
 여행 B/
 ───────────────────/
</pre> 
 
### pathways.txt 
 
 파일: **선택 사항** 
 
 기본 키(`pathway_id) 
 
 파일 [pathways.txt](#pathwaystxt) 및 [levels.txt](#levelstxt) 그래프 표현을 사용하여 지하철이나 기차역을 설명합니다. 노드는 위치를 나타내고 가장자리는 pathways 나타냅니다. 
 
 역 입구/출구(`location_type=2`로 위치로 표시되는 노드)에서 승강장(`location_type=0`으로 위치로 표시되는 노드 또는 비어 있음)으로 이동하려면 라이더가 이동해야 합니다. 통로, 개찰구, 계단 및 pathways 로 표시된 기타 가장자리를 통과합니다. 일반 노드(`location_type=3`으로 표시되는 노드)는 역 전체의 pathways 연결하는 데 사용할 수 있습니다. 
 
 경로는 스테이션에서 철저하게 정의되어야 합니다. 어떤 pathways 정의되어 있으면 역 전체의 모든 pathways 표현되는 것으로 가정합니다. 따라서 다음 지침이 적용됩니다. 
 
 - 매달린 위치 없음: 역 내의 어느 위치에 통로가 있는 경우 탑승 구역이 있는 pathways(`location_type=4`, 아래 지침을 참조하세요). 
 - 탑승 구역이 있는 플랫폼에 대한 pathways 없음: 탑승 구역(` location_type=4 `)이 있는 플랫폼(` location_type=0 ` 또는 비어 있음)은 지점이 아닌 상위 객체로 처리됩니다. 이러한 경우 플랫폼에는 pathways 지정되어서는 안 됩니다. 모든 pathways 플랫폼의 탑승 구역 각각에 지정되어야 합니다. 
 - 잠긴 플랫폼 없음: ​​각 플랫폼(`location_type=0` 또는 비어 있음) 또는 탑승 구역(`location_type=4 `)은 일부 pathways 체인을 통해 적어도 하나의 입구/출구(` location_type=2 `)에 연결되어야 합니다.. 특정 플랫폼에서 역 외부로의 통로를 허용하지 않는 역은 거의 없습니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | ` pathway_id` | 고유 ID | **필수** | 경로를 식별합니다. 시스템에서 기록의 내부 식별자로 사용됩니다. 데이터 세트에서 고유해야 합니다.<br><br> 서로 다른 pathways `from_stop_id` 및 `to_stop_id`에 대해 동일한 값을 가질 수 있습니다.<hr> _예: 두 개의 에스컬레이터가 반대 방향으로 나란히 있거나 계단 세트와 엘리베이터가 같은 장소에서 같은 장소로 이동하는 경우 서로 다른 `pathway_id 는 동일한 `from_stop_id 및 `to_stop_id 값을 가질 수 있습니다._ | 
 | `from_stop_id| `stops.stop_id 를 참조하는 외부 ID | **필수** | 경로가 시작되는 위치입니다.<br><br> 플랫폼을 식별하는 `stop_id` 포함해야 합니다(`lo

cation_type=0` 또는 비어 있음), 입구/출구(`location_type=2`), 일반 노드(`location_type=3`) 또는 탑승 구역(`location_type=4`).<br><br> 역을 식별하는 `stop_id` 값(`location_type=1`)은 금지됩니다.| 
 | `to_stop_id| `stops.stop_id 를 참조하는 외부 ID | **필수** | 통로가 끝나는 위치.<br><br> 플랫폼(` location_type=0` 또는 비어 있음), 입구/출구(`location_type=2`), 일반 노드(`location_type=3`) 또는 탑승 구역(`location_type=4 `)을 식별하는 `stop_id` 포함해야 합니다..<br><br> 역을 식별하는 `stop_id` 값(`location_type=1`)은 금지됩니다.| 
 | `pathway_mode` | 열거형 | **필수** | 지정된(`from_stop_id`, `to_stop_id`) 쌍 사이의 경로 유형입니다. 유효한 옵션은 다음과 같습니다.<br><br> `1` - 산책로.<br> `2` - 계단.<br> `3` - 움직이는 보도/여행자.<br> `4` - 에스컬레이터.<br> `5` - 엘리베이터.<br> `6` - 개찰구(또는 정산 게이트): 정산 증명이 필요한 역 구역으로 건너가는 통로입니다. 개찰구는 역의 유료 구역과 무료 구역을 분리하거나, 같은 역 내의 서로 다른 지불 구역을 서로 분리할 수 있습니다. 이 정보는 승객이 버스 정류장에 도달하기 위해 지하철 플랫폼을 통과하도록 지시하는 것과 같이 승객에게 불필요한 지불을 require 하는 지름길을 사용하여 역을 통해 승객을 라우팅하는 것을 방지하는 데 사용될 수 있습니다.<br> `7`- 출구 게이트: 유료 구역에서 지불 증명이 필요하지 않은 무료 구역으로 넘어가는 통로입니다.| 
 | `is_bidirectional| 열거형 | **필수** | 경로를 선택할 수 있는 방향을 나타냅니다.<br><br> `0` - `from_stop_id`에서 `to_stop_id`까지만 사용할 수 있는 단방향 경로입니다.<br> `1` - 양방향으로 사용할 수 있는 양방향 경로입니다.<br><br> 출구 게이트(`pathway_mode=7`)는 양방향이어서는 안 됩니다.| 
 | ’길이’ | 음수가 아닌 float 소수점 | 선택사항 | 원래 위치(`from_stop_id`에 정의됨)에서 목적지 위치(`to_stop_id`에 정의됨)까지의 통로의 수평 길이(미터)입니다.<br><br> 이 필드는 통로(`pathway_mode=1), 개찰구(`pathway_mode=6) 및 출구 게이트(`pathway_mode=7)에 권장됩니다.| 
 | `traversal_time` | 양의 정수 | 선택사항 | 원래 위치(`from_stop_id`에 정의됨)에서 목적지 위치(`to_stop_id`에 정의됨)까지 경로를 통과하는 데 필요한 평균 시간(초)입니다.<br><br> 이 필드는 이동 인도(`pathway_mode=3), 에스컬레이터(`pathway_mode=4) 및 엘리베이터(`pathway_mode=5)에 권장됩니다.| 
 | `stair_count` | 널이 아닌 정수 | 선택사항 | 통로의 계단 수.<br><br> 긍정적인 ’ stair_count’는 탑승자가 `from_stop_id 에서 `to_stop_id 까지 걸어간다는 것을 의미합니다. 그리고 음수 `stair_count`는 탑승자가 `from_stop_id`에서 `to_stop_id`까지 걸어 내려오는 것을 의미합니다.<br><br> 이 필드는 계단에 권장됩니다(`pathway_mode=2).<br><br> 대략적인 계단수만 제공할 수 있는 경우에는 1층당 약 15계단 정도를 권장합니다.| 
 | `max_slope` | Float | 선택사항 | 통로의 최대 경사 비율. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 경사가 없습니다.<br> `Float` - 경로의 경사 비율, 위쪽은 양수, 아래쪽은 음수입니다.<br><br> 이 필드는 보도(`pathway_mode=1) 및 이동 보도(`pathway_mode=3)에만 사용해야 합니다.<hr> _예: 미국의 경우 0.083(8.3%라고도 표기)은 수동식 휠체어의 최대 경사비로, 1m당 0.083m(8.3cm)씩 증가한다는 의미입니다._| 
 | `min_width` | 긍정적인 float | 선택사항 | 통로의 최소 너비(미터)입니다.<br><br> 이 필드는 최소 너비가 1미터 미만인 경우에 권장됩니다.| 
 | `signposted_as` | Text | 선택사항 | 라이더가 볼 수 있는 물리적 표지판의 공개 텍스트입니다.<br><br> ’’표지판을 따르세요’와 같이 탑승자에게 텍스트 방향을 제공하는 데 사용될 수 있습니다. `singposted_as 의 텍스트는 표지판에 인쇄된 것과 정확히 동일하게 나타나야 합니다.<br><br> 물리적 간판이 다국어인 경우 이 필드는 ` feed_info.feed_lang 의 필드 정의에 있는 ` stops.stop_name 의 예에 따라 채워지고 번역될 수 있습니다.| 
 | ` reversed_signposted_as` | Text | 선택사항 | `signposted_as`와 동일하지만 경로가 `to_stop_id`에서 `from_stop_id`까지 사용되는 경우.| 
 
### levels.txt 
 
 파일: **조건부 필수** 
 
 기본 키(`level_id`) 
 
 스테이션의 레벨을 설명합니다. [pathways.txt](#pathwaystxt)와 함께 사용하면 유용합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `level_id` | 고유 ID | **필수** | 스테이션의 레벨을 식별합니다.| 
 | `level_index` | Float | **필수** | 상대 position 나타내는 레벨의 숫자 인덱스입니다.<br><br> 지면 수준은 인덱스 ’0’을 가져야 하며, 지면 위 수준은 양수 지수로 표시되고 지면 아래 수준은 음수 지수로 표시됩니다.| 
 | `level_name` | Text | 선택사항 | 건물이나 역 내부에서 라이더가 볼 수 있는 레벨의 이름입니다.<hr> _예: 엘리베이터를 타고 "중이층", "플랫폼" 또는 "-1"으로 가세요._| 
 
### location_groups.txt 
 
 파일: **선택 사항** 
 
 기본 키(`location_group_id`) 
 
 승객이 요청할 수 있는 stops 그룹인 위치 그룹을 정의합니다. 픽업 또는 하차. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |----------|----|------------|-----------| 
 | `위치_그룹_ID` | 고유 ID | **필수** | 위치 그룹을 식별합니다. ID는 모든 `stops.stop_id, locations.geojson `id` 및 `location_groups.location_group_id` 값에서 고유해야 합니다.<br><br> 위치 그룹은 승객이 승차 또는 하차를 요청할 수 있는 위치를 함께 나타내는 stops 그룹입니다. | 
 | `위치_그룹_이름` | Text | 선택사항 | 라이더에게 표시되는 위치 그룹의 이름입니다. | 
 
### location_group_stops.txt 
 
 파일: **선택 사항** 
 
 기본 키(`*`) 
 
 stops.txt 의 stops 위치 그룹에 할당합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |----------|----|------------|-----------| 
 | `위치_그룹_ID` | ’location_groups.location_group_id’를 참조하는 외부 ID | **필수** | 하나 이상의 `stop_id` 가 속하는 위치 그룹을 식별합니다. 동일한 `stop_id` 여러 `location_group_id`에 정의될 수 있습니다. | 
 | `stop_id` | `stops.stop_id 를 참조하는 외부 ID | **필수** | 위치 그룹에 속하는 정류장을 식별합니다. | 
 
 
### locations.geojson 
 
 파일: **선택 사항** 
 
 라이더가 주문형 서비스를 통해 픽업 또는 하차를 요청할 수 있는 구역을 정의합니다. 이러한 영역은 GeoJSON 다각형으로 표시됩니다. 
 
 - 이 파일은 [RFC 7946](https://tools.ietf.org/html/rfc7946)에 설명된 GeoJSON 형식의 하위 집합을 사용합니다. 
 - ’`locations.geojson`’ 파일에는 ’FeatureCollection’이 포함되어야 합니다. 
 - ’FeatureCollection’은 승객이 승차 또는 하차를 요청할 수 있는 다양한 정류장 위치를 ​​정의합니다. 
 - 모든 GeoJSON ’Feature’에는 ’`id` 있어야 합니다. `id` 모든 `stops.stop_id, locations.geojson `id` 및 `location_group_id` 값에서 고유해야 합니다. 
 - 모든 GeoJSON ’Feature’에는 아래 표에 따라 객체와 관련 키가 있어야 합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 |-`유형` | 문자열 | **필수** | 위치의 `"FeatureCollection"`. | 
 |-`기능` | 배열 | **필수** | 위치를 설명하는 `"Feature"` 객체의 컬렉션입니다. | 
 |     \-`유형` | 문자열 | **필수** | ``기능’` | 
 |     \ `id` | 문자열 | **필수** | 위치를 식별합니다. ID는 모든 `stops.stop_id, locations.geojson `id` 및 `location_groups.location_group_id` 값에서 고유해야 합니다. | 
 |     \-`속성` | 개체 | **필수** | 위치 속성 키. | 
 |         \- `stop_name` | 문자열 | 선택사항 | 라이더에게 표시되는 위치의 이름을 나타냅니다. | 
 |         \- `stop_desc` | 문자열 | 선택사항 | 라이더의 방향을 잡는 데 도움이 되는 위치에 대한 의미 있는 설명입니다. | 
 |     \-`기하학` | 개체 | **필수** | 위치의 기하학. | 
 |         \-`유형` | 문자열 | **필수** | 다음 유형이어야 합니다.<br> - `"Polygon"`<br> - `"다중 다각형"` | 
 |         \-`좌표` | 배열 | **필수** | 위치의 기하학적 구조를 정의하는 지리적 좌표(latitude 및 longitude)입니다. | 
 
### booking_rules.txt 
 
 파일: **선택 사항** 
 
 기본 키(`booking_rule_id`) 
 
 승객이 요청한 서비스에 대한 예약 규칙 정의 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `booking_rule_id` | 고유 ID | **필수** | 규칙을 식별합니다. | 
 | `예약_유형` | 열거형 | **필수** | 사전 예약이 가능한 기간을 나타냅니다. 유효한 옵션은 다음과 같습니다.<br><br> `0` - 실시간 예약.<br> `1` - 사전 공지 후 당일 예약까지 가능합니다.<br> `2` - 전날까지 예약 가능. | 
 | `prior_notice_duration_min` | 정수 | **조건부 필수** | 요청을 하기 위한 여행 전 최소 시간(분)입니다.<br><br> **조건부 필수**:<br> - `booking_type=1`의 경우 **필수**입니다.<br> - **금지됨**. | 
 | `prior_notice_duration_max` | 정수 | **조건부 금지** | 여행 전 예약 요청을 위한 최대 시간(분)입니다.<br><br> **조건부 금지**:<br> - `booking_type=0` 및 `booking_type=2`에는 **금지됨**.<br> - `booking_type=1`의 경우 선택 사항입니다.| 
 | `prior_notice_last_day` | 정수 | **조건부 필수** | 예약 요청을 위한 여행 마지막 날.<br><br> 예: "탑승은 오후 5시 이전에 1일 전에 예약해야 합니다."는 `prior_notice_last_day=1`로 인코딩됩니다.<br><br> **조건부 필수**:<br> - `booking_type=2`의 경우 **필수**입니다.<br> - 그렇지 않으면 **금지됨**. | 
 | `prior_notice_last_time` | 시간 | **조건부 필수** | 여행 마지막 날 예약 요청을 위한 마지막 시간입니다.<br><br> 예: "라이드는 오후 5시 이전에 1일 전에 예약해야 합니다."는 `prior_notice_last_time=17:00:00`으로 인코딩됩니다.<br><br> **조건부 필수**:<br> - `prior_notice_last_day`가 정의된 경우 **필수**입니다.<br> - **금지됨**. | 
 | `prior_notice_start_day` | 정수 | **조건부 금지** | 예약 요청을 위한 여행 전 가장 빠른 날입니다.<br><br> 예: "탑승은 빠르면 일주일 전 자정부터 예약할 수 있습니다."는 `prior_notice_start_day=7`로 인코딩됩니다.<br><br> **조건부 금지**:<br> - `booking_type=0`에는 **금지됨**.<br> - `prior_notice_duration_max`가 정의된 경우 `booking_type=1`에 **금지됨**.<br> - 그렇지 않은 경우 선택 사항입니다. | 
 | `prior_notice_start_time` | 시간 | **조건부 필수** | 예약 요청을 위한 여행 전 가장 이른 날의 가장 빠른 시간입니다.<br><br> 예: "탑승은 빠르면 일주일 전 자정에 예약할 수 있습니다."는 `prior_notice_start_time=00:00:00`으로 인코딩됩니다.<br><br> **조건부 필수**:<br> - `prior_notice_start_day`가 정의된 경우 **필수**입니다.<br> - **금지됨**. | 
 | `prior_notice_service_id` | `calendar.service_id`를 참조하는 ID | **조건부 금지** | ’prior_notice_last_day’ 또는 ’prior_notice_start_day’가 계산되는 서비스 날짜를 나타냅니다.<br><br> 예: 비어 있는 경우 `prior_notice_start_day=2`는 달력상 2일 전입니다. 영업일(공휴일을 제외한 평일)만 포함하는 `service_id 로 정의된 경우 `prior_notice_start_day=2`는 영업일 2일 전입니다.<br><br> **조건부 금지**:<br> - `booking_type=2`인 경우 선택사항입니다.<br> - **금지됨**. | 
 | `message` | Text | 선택사항 | 주문형 픽업 및 하차를 예약할 때 ’ stop_time’에 서비스를 이용하는 승객에게 보내는 메시지입니다. 승객이 서비스를 이용하기 위해 취해야 하는 조치에 대해 사용자 인터페이스 내에서 전송되는 최소한의 정보를 제공하기 위한 것입니다. | 
 | `픽업_메시지` | Text | 선택사항 | `message`와 동일한 기능을 하지만 라이더가 주문형 픽업만 할 때 사용됩니다. | 
 | `drop_off_message` | Text | 선택사항 | `message`와 동일한 방식으로 작동하지만 라이더가 주문형 하차만 하는 경우에 사용됩니다. | 
 | `전화_번호` | Phone number | 선택사항 | 예약 요청을 위해 전화할 Phone number. | 
 | `정보_URL` | URL | 선택사항 | 예약 규칙에 대한 정보를 제공하는 URL. | 
 | `예약_URL` | URL | 선택사항 | 예약 요청을 할 수 있는 온라인 인터페이스 또는 앱의 URL. | 
 
### translations.txt 
 
 파일: **선택 사항** 
 
 기본 키(`table_name`, `field_name`, `언어`, `record_id`, `record_sub_id`, `field_value`) 
 
 여러 공식 언어를 사용하는 지역의 대중교통 기관/운영자는 일반적으로 언어별 이름과 웹페이지를 가지고 있습니다. 해당 지역의 승객에게 최상의 서비스를 제공하려면 데이터세트에 이러한 언어별 값을 포함하는 것이 유용합니다. 
 
 참조 방법(`record_id, `record_sub_id)과 `field_value 를 사용하여 2개의 다른 행에서 동일한 값을 변환하는 경우 (`record_id, `record_sub_id)와 함께 제공된 변환이 우선합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `table_name` | 열거형 | **필수** | 번역할 필드가 포함된 테이블을 정의합니다. 허용되는 값은 다음과 같습니다.<br><br> - `agency`<br> - `stops`<br> - `routes`<br> - ’여행’<br> - `stop_times<br> - `pathways`<br> - ’레벨’<br> - `feed_info`<br> - `attributions`<br><br> GTFS 에 추가된 모든 파일은 위에 나열된 파일 이름과 동일한 `table_name` 값을 갖습니다(예: `.txt` 파일 확장자는 포함되지 않음). | 
 | `field_name` | Text | **필수** | 번역할 필드의 이름입니다. ’ Text’ 유형의 필드는 번역될 수 있으며, ’ URL’, ’ Email’ 및 ’ Phone number’ 유형의 필드도 "번역"되어 올바른 언어로 리소스를 제공할 수 있습니다. 다른 유형의 필드는 번역하면 안 됩니다. | 
 | ’언어’ | 언어 코드 | **필수** | 번역 언어.<br><br> 언어가 `feed_info.feed_lang 과 동일한 경우 필드의 원래 값은 특정 번역 없이 언어에서 사용할 기본값으로 간주됩니다(`default_lang 이 달리 지정하지 t 경우).<hr> _예: 스위스에서 공식적으로 이중 언어를 사용하는 주의 도시는 공식적으로 "Biel/Bienne"이라고 불리지만 프랑스어에서는 "Bienne", 독일어에서는 "Biel"이라고 간단히 부릅니다._ | 
 | `번역` | Text, URL, Email, Phone number | **필수** | 번역된 값. | 
 | `record_id| 외국인 신분증 | **조건부 필수** | 번역할 필드에 해당하는 레코드를 정의합니다. `record_id 의 값은 각 테이블 및 아래의 기본 키 속성에 정의된 대로 테이블 기본 키의 첫 번째 또는 유일한 필드여야 합니다.<br><br> - [agency.txt](#agencytxt)에 대한 ` agency_id `<br> - [stops.txt](#stopstxt)에 대한 `stop_id` ;<br> - [routes.txt](#routestxt)에 대한 `route_id` ;<br> - [trips.txt](#tripstxt)에 대한 `trip_id` ;<br> - [stop_times.txt](#stop_timestxt)에 대한 `trip_id` ;<br> - [pathways.txt](#pathwaystxt)의 경우 ` pathway_id `;<br> - [levels.txt](#levelstxt)에 대한 ` level_id `;<br> - [attributions.txt](#attributionstxt)에 대한 ` attribution_id `.<br><br> 위에 정의되지 않은 테이블의 필드는 번역되어서는 안 됩니다. 그러나 생산자는 공식 사양을 벗어나는 추가 필드를 추가하는 경우가 있으며 이러한 비공식 필드는 번역될 수 있습니다. 다음은 해당 테이블에 ` record_id 를 사용하는 권장 방법입니다.<br><br> - [calendar.txt](#calendartxt)에 대한 ` service_id `;<br> - [calendar_dates.txt](#calendar_datestxt)에 대한 ` service_id `;<br> - [fare_attributes.txt](#fare_attributestxt)에 대한 ` fare_id `;<br> - [fare_rules.txt](#fare_rulestxt)에 대한 ` fare_id `;<br> - [shapes.txt](#shapestxt)에 대한 `shape_id` ;<br> - [frequencies.txt](#frequencytxt)에 대한 `trip_id` ;<br> - [transfers.txt](#transferstxt)의 경우 ` from_stop_id `.<br><br> 조건부 필수:<br> - ` table_name`이 `feed_info`인 경우 **금지됨**.<br> - `field_value`가 정의된 경우 **금지됨**.<br> - `field_value`가 비어 있는 경우 **필수**입니다. | 
 | `record_sub_id| 외국인 신분증 | **조건부 필수** | 테이블에 고유 ID가 t 때 번역할 필드가 포함된 레코드를 돕습니다. 따라서 `record_sub_id 의 값은 아래 표에 정의된 대로 테이블의 보조 ID입니다.<br><br> - [agency.txt](#agencytxt)에는 없음;<br> - [stops.txt](#stopstxt)에는 없음;<br> - [routes.txt](#routestxt)에는 없음;<br> - [trips.txt](#tripstxt)에는 없음;<br> - [stop_times.txt](#stop_timestxt)에 대한 `stop_sequence` ;<br> - [pathways.txt](#pathwaystxt)에는 없음;<br> - [levels.txt](#levelstxt)에는 없음;<br> - [attributions.txt](#attributionstxt)에는 없음.<br><br> 위에 정의되지 않은 테이블의 필드는 번역되어서는 안 됩니다. 그러나 생산자는 공식 사양을 벗어나는 추가 필드를 추가하는 경우가 있으며 이러한 비공식 필드는 번역될 수 있습니다. 다음은 해당 테이블에 `record_sub_id 를 사용하는 권장 방법입니다.<br><br> - [calendar.txt](#calendartxt)에는 없음;<br> - [calendar_dates.txt](#calendar_datestxt)에 대한 ` date `;<br> - [fare_attributes.txt](#fare_attributestxt)에는 없음;<br> - [fare_rules.txt](#fare_rulestxt)에 대한 `route_id` ;<br> - [shapes.txt](#shapestxt)에는 없음;<br> - [frequencies.txt](#frequencytxt)에 대한 `start_time` ;<br> - [transfers.txt](#transferstxt)의 경우 ` to_stop_id `.<br><br> 조건부 필수:<br> - ` table_name`이 `feed_info`인 경우 **금지됨**.<br> - `field_value`가 정의된 경우 **금지됨**.<br> - `table_name=stop_times` 및 `record_id`가 정의된 경우 **필수**입니다. | 
 | `field_value` | Text, URL, Email, Phone number | **조건부 필수** | `record_id 및 `record_sub_id 를 사용하여 어떤 레코드를 변환해야 하는지 정의하는 대신 이 필드를 사용하여 변환해야 하는 값을 정의할 수 있습니다. 사용 시 `table_name` 및 `field_name`으로 식별된 필드에 field_value 에 정의된 것과 정확히 동일한 값이 포함된 경우 변환이 적용됩니다.<br><br> 필드에는 `field_value`에 정의된 값이 **정확히** 있어야 합니다. 값의 하위 집합만 `field_value`와 일치하는 경우 번역이 적용되지 t .<br><br> 두 개의 변환 규칙이 동일한 레코드와 일치하는 경우(하나는 `field_value`, 다른 하나는 `record_id`), `record_id`가 있는 규칙이 우선합니다.<br><br> 조건부 필수:<br> - `table_name`이 `feed_info`인 경우 **금지됨**.<br> - `record_id 가 정의된 경우 **금지됨**.<br> - `record_id 비어 있는 경우 **필수**입니다. | 
 
### feed_info.txt 
 
 파일: **권장** (**필수** [translations.txt](#translationstxt)가 제공되는 경우) 
 
 Primary key (none) § § 
 파일에는 데이터세트가 설명하는 서비스가 아닌 데이터세트 자체에 대한 정보가 포함되어 있습니다. 어떤 경우에는 데이터세트 게시자가 대행사와 다른 entity 일 수도 있습니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `feed_publisher_name` | Text | **필수** | 데이터 세트를 게시하는 조직의 전체 이름입니다. `agency.agency_name 값 중 하나와 동일할 수 있습니다. | 
 | `feed_publisher_url` | URL | **필수** | 데이터세트 게시 기관의 웹사이트 URL. `agency.agency_url 값 중 하나와 동일할 수 있습니다. | 
 | `feed_lang` | 언어 코드 | **필수** | 이 데이터 세트의 텍스트에 사용되는 기본 언어입니다. 이 설정은 GTFS 소비자가 데이터세트의 대문자 사용 규칙과 기타 언어별 설정을 선택하는 데 도움이 됩니다. 텍스트를 기본 언어가 아닌 다른 언어로 번역해야 하는 경우 `translations.txt 파일을 사용할 수 있습니다.<br><br> 기본 언어는 원본 텍스트가 여러 언어로 포함된 데이터세트의 경우 다국어일 수 있습니다. 이러한 경우 `feed_lang 필드에는 표준 ISO 639-2에 정의된 언어 코드 `mul`이 포함되어야 하며, 데이터세트에 사용된 각 언어에 대한 번역은 `translations.txt 에 제공되어야 합니다. 데이터 세트의 모든 원본 텍스트가 동일한 언어로 되어 있는 경우 `mul`을 사용하면 안 됩니다.<hr> _예: 원래 `stops.stop_name 필드가 다른 언어의 정류장 이름으로 채워진 스위스와 같은 다국어 국가의 데이터세트를 생각해 보세요. 각 정류장 이름은 해당 정류장의 지리적 위치에서 주로 사용되는 언어에 따라 작성됩니다. 예를 들어 프랑스어를 사용하는 도시인 Geneva 는 ’ Genève ’, 독일어를 사용하는 도시인 Zurich 는 ’ Zürich ’, 이중 언어를 사용하는 도시는 ’ Biel/Bienne’로 표시됩니다. Biel/Bienne 도시. 데이터세트 `feed_lang 은 `mul`이어야 하며 번역은 `translations.txt 에 제공됩니다(독일어: `Genf`, `Zürich` 및 `Biel`). 프랑스어: `Genève`, `Zurich` 및 `Bienne`; 이탈리아어: `Ginevra`, `Zurigo` 및 `Bienna`; 영어: `Geneva`, `Zurich` 및 `Biel/Bienne`._ | 
 | `default_lang| 언어 코드 | 선택사항 | 데이터 소비자가 라이더의 언어를 t 때 사용해야 하는 언어를 정의합니다. 종종 ’en’(영어)이 됩니다. | 
 | `feed_start_date` | 날짜 | 추천 | 데이터세트는 `feed_start_date`일 시작부터 `feed_end_date`일까지의 기간 동안 서비스에 대한 완전하고 신뢰할 수 있는 일정 정보를 제공합니다. 이용할 수 없는 경우 두 날 모두 비워 둘 수 있습니다. `feed_end_date` date `feed_start_date` date 둘 다 제공되는 경우 이전되어서는 안 됩니다. 데이터 세트 공급자는 향후 서비스에 대해 조언하기 위해 이 기간 외의 일정 데이터를 제공하는 것이 좋지만 데이터 세트 소비자는 신뢰할 수 없는 상태를 염두에 두고 이를 처리해야 합니다. `feed_start_date 또는 `feed_end_date 가 [calendar.txt](#calendartxt) 및 [calendar_dates.txt](#calendar_datestxt)에 정의된 활성 달력 날짜를 초과하는 경우 데이터세트는 날짜에 대한 서비스가 없다고 명시적으로 주장합니다. `feed_start_date 또는 `feed_end_date 범위 내에 있지만 활성 달력 날짜에는 포함되지 않습니다. | 
 | `feed_end_date` | 날짜 | 추천 | (위 참조) | 
 | `feed_version` | Text | 추천 | GTFS 데이터세트의 현재 버전을 나타내는 문자열입니다. GTFS 사용하는 애플리케이션은 이 값을 표시하여 데이터세트 게시자가 최신 데이터세트가 통합되었는지 여부를 판단하는 데 도움을 줄 수 있습니다. | 
 | `feed_contact_email` | Email | 선택사항 | GTFS 데이터세트 및 데이터 게시 관행에 관한 커뮤니케이션을 위한 Email 주소입니다. ` feed_contact_email 은 GTFS 사용하는 애플리케이션의 기술 담당자입니다. [agency.txt](#agencytxt)를 통해 고객 서비스 연락처 정보를 제공하세요. `feed_contact_email 또는 `feed_contact_url 중 하나 이상을 제공하는 것이 좋습니다. | 
 | `feed_contact_url| URL | 선택사항 | 연락처 정보, 웹 양식, 지원 데스크, GTFS 데이터세트 및 데이터 게시 관행과 관련된 커뮤니케이션을 위한 기타 도구의 URL. ` feed_contact_url 은 GTFS 를 사용하는 애플리케이션에 대한 기술 담당자입니다. [agency.txt](#agencytxt)를 통해 고객 서비스 연락처 정보를 제공하세요. `feed_contact_url 또는 `feed_contact_email 중 하나 이상을 제공하는 것이 좋습니다. | 
 
### attributions.txt 
 
 파일: **선택 사항** 
 
 기본 키(`attribution_id`) 
 
 파일은 데이터세트에 적용되는 attributions 정의합니다. 
 
 | 필드 이름 | 유형 | 존재 | 설명 | 
 |------|------|------|------| 
 | `attribution_id` | 고유 ID | 선택사항 | 데이터 세트 또는 그 하위 세트에 대한 속성을 식별합니다. 이는 주로 번역에 유용합니다. | 
 | `agency_id` | `agency.agency_id 를 참조하는 외부 ID | 선택사항 | 귀속이 적용되는 기관입니다.<br><br> 하나의 `agency_id, `route_id` 또는 `trip_id` 속성이 정의된 경우 다른 속성은 비어 있어야 합니다. 어느 것도 지정되지 않으면 속성이 전체 데이터 세트에 적용됩니다. | 
 | `route_id` | `routes.route_id`를 참조하는 외부 ID | 선택사항 | 속성이 경로에 적용된다는 점을 제외하면 `agency_id 와 동일한 방식으로 작동합니다. 동일한 경로에 여러 attributions 적용될 수 있습니다. | 
 | `trip_id` | ’`trips.trip_id` 참조하는 외국인 ID | 선택사항 | 여행에 속성이 적용된다는 점을 제외하면 `agency_id 와 동일한 방식으로 작동합니다. 동일한 여행에 여러 attributions 적용될 수 있습니다. | 
 | `organization_name` | Text | **필수** | 데이터세트가 속한 조직의 이름입니다. | 
 | `is_producer| 열거형 | 선택사항 | 조직의 역할은 생산자이다. 유효한 옵션은 다음과 같습니다.<br><br> ’0’ 또는 비어 있음 - 조직에 이 역할이 t .<br> `1` - 조직에는 이 역할이 있습니다.<br><br> `is_producer`, `is_operator 또는 `is_authority` 필드 중 하나 이상이 `1` 로 설정되어야 합니다. | 
 | `is_operator| 열거형 | 선택사항 | 조직의 역할이 운영자라는 점을 제외하면 `is_producer`와 동일한 방식으로 기능합니다. | 
 | `is_authority| 열거형 | 선택사항 | 조직의 역할이 권위라는 점을 제외하면 `is_producer`와 동일한 방식으로 기능합니다. | 
 | `attribution_url` | URL | 선택사항 | 조직의 URL. |

 
 | `attribution_email` | Email | 선택사항 | 조직의 Email. | 
 | `attribution_phone` | Phone number | 선택사항 | 조직의 Phone number. | 
 

