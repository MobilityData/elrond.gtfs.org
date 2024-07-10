##General Transit Feed Specification參考
 
 **2024 年5 月22 日修訂。定義了組成GTFS資料集的檔案。 
 
## 目錄 
 
 1. [文檔約定](#document-conventions) 
 2. [資料集文件](#dataset-files) 
 3. [文件要求](#file-要求） 
 4. [資料集發布和一般實踐](#dataset-publishing-general-practices) 
 5. [字段定義](#field-definitions) 
 - [agency.txt](#agencytxt) 
 - [stops.txt](#stopstxt) 
 - [routes.txt](#routestxt) 
 - [trips.txt](#tripstxt) 
 - [stop\_times.txt](#stop_timestxt) 
 - [calendar.txt](#calendartxt) 
 - [calendar\_dates.txt](#calendar_datestxt) 
 - [fare\_attributes.txt](#fare_attributestxt) 
 - [fare\_rules.txt](#fare_rulestxt) 
 - [時間範圍.txt](#timeframestxt) 
 - [票價\_media.txt](#fare_mediatxt) 
 - [票價\_產品.txt](#fare_productstxt) 
 - [票價\ _leg\_rules.txt](#fare_leg_rulestxt) 
 - [fare\_transfer\_rules.txt](#fare_transfer_rulestxt) 
 - [areas.txt](#areastxt) 
 - [stop_areas.txt](#stop_areastxt) 
 - [網路.txt](#networkstxt) 
 - [route_networks.txt](#route_networkstxt) 
 - [shapes.txt](#shapestxt) 
 - [frequencies.txt](#frequenciestxt) 
 - [transfers.txt](#transferstxt) 
 - [pathways.txt](#pathwaystxt) 
 - [levels.txt](#levelstxt) 
 - [location_groups.txt](#location_groupstxts ) 
 - [location_group_stops.txt](#location_group_stopstxt) 
 - [locations.geojson](#locationsgeojson) 
 - [booking_rules.txt](#booking_rulestxt) 
 - [translations.txt](translationstxt](translationstxt) 
 - [Translations。 § - [feed\ _info.txt](#feed_infotxt) 
 - [attributions.txt](#attributionstxt) 
 
## 文件約定
 關鍵字`MUST`、`MUST NOT`、`REQUIRED`、 `SHALL`、本文檔中的`不得`、`應該`、`不應該`、`建議`、`可以`和`可選`應按 [RFC 2119](https:中的描述進行解釋)/html/rfc2119）。 
 
 
### 術語定義 
 
 本節定義了本文檔中使用的術語。 
 
 * **資料集** - 本規範參考定義的完整文件集。變更資料集會建立資料集的新版本。資料集應發佈在公共的永久URL上，包括 zip 檔案名稱。 （例如，https: agency）。 
 * **記錄** - 一種基本資料結構，由描述單一entity（例如公車agency、車站、路線等）的多個不同欄位值組成。在表中表示為一行。 
 * **字段** - 物件或entity的屬性。在表中表示為一列。如果作為header新增至文件中，則該欄位存在。它可能有也可能沒有定義欄位值。 
 * **字段值** - 字段中的單一條目。在表中表示為單一儲存格。 
 * **服務日** - 服務日是用來指示路線安排的時間段。服務日的確切定義因agency而異，但服務日通常與日曆日不一致。如果服務在某一天開始並在第二天結束，則服務日可能會超過 24:00:00。例如，從週五 08:00:00 運行到週六 02:00:00 的服務可以表示為在單一服務日從 08:00:00 運行到 26:00:00。 
 * **文字轉語音欄位** - 此欄位應包含與其父欄位相同的資訊（如果為空，則返回父欄位）。它的目的是閱讀文字到語音，因此，縮寫應該被刪除（“St”應該讀作“街道”或“聖人”；“伊麗莎白一世”應該是“伊麗莎白一世”）或保持原樣閱讀（“JFK 機場”據說是縮寫）。 
 * **航程** - 乘客在行程中的兩個後續地點之間上下車的行程。 
 * **旅程** - 從出發地到目的地的整體旅行，包括所有航段和中間的transfers。 
 * **子旅程** - 構成旅程子集的兩條或多條航段。 
 * **票價產品** - 可用於支付或驗證旅行的可購買票價產品。 
 
### 存在 
 適用於欄位和文件的存在條件： 
 
 * **必需** - 欄位或文件必須包含在資料集中，並包含每筆記錄的有效值。 
 * **可選** - 資料集中可以省略欄位或檔案。 
 * **有條件要求** - 必須在欄位或文件描述中概述的條件下包含該欄位或文件。 
 * **有條件禁止** - 在欄位或文件描述中概述的條件下不得包含該欄位或文件。 
 * **推薦** - 欄位或文件可以從資料集中省略，但最佳實踐是包含它。在省略此欄位或文件之前，應仔細評估最佳實踐，並理解省略的全部含義。 
 
### 欄位類型 
 
 - **顏色** - 編碼為六位十六進位數字的顏色。請參考[https://htmlcolorcodes.com](https:)產生有效值（不能包含前導`#`）。<br> *範例：`FFFFFF` 表示白色，`000000` 表示黑色，或 `0039A6` 表示 NYMTA 中的A 、C、E 行。目前currency清單請參考[https://en.wikipedia.org/wiki/ISO_4217#Active\_codes](https://en.wikipedia.org/wiki/ISO_4217#Active_codes )。<br> *範例：`CAD`代表加幣，`EUR `amountamount，` JPY `currency日圓。小數位數由隨附貨幣代碼的 [ISO 4217](https:) 指定。所有財務計算都應以十進制、currency或其他適合財務計算的等效類型進行處理，具體取決於用於使用資料的程式語言。由於計算過程中會產生金錢收益或損失，因此不鼓勵將currency金額處理為float。 
 - **日期** - YYYYMMDD 格式的服務日。由於服務日內的時間可能高於 24:00:00，因此服務日可能包含後續日期的資訊。<br> *範例：`20180913`表示 2018 年 9 月 13 日。 * 
 - **Email** - 電子郵件地址。<br> *範例：`example@example.com`* 
 - **Enum** - `描述`欄中定義的一組預定義常數中的選項。<br> *範例：`route_type`欄位包含`0`（表示電車）、 ``1`` （表示地鐵）...* 
 - **ID** - ID 欄位值是內部 ID，不用於顯示riders，並且是任意UTF-8 字元的序列。建議僅使用可列印的 ASCII 字元。當 ID 在檔案中必須是唯一的時，它被標記為`唯一 ID`。在一個.txt檔案中定義的 ID 通常會在另一.txt檔案中引用。引用另一個表中的 ID 的 ID 被標記為`外部 ID`。<br> *範例：[stops.txt](#stopstxt) 中的`stop_id`欄位是一個`唯一 ID`。 [stops.txt](#stopstxt) 中的 ` parent_station欄位是`引用 ` stops.stop_id的外部 ID`。有關 IETF BCP 47 的介紹，請參閱 [http://www.rfc-editor.org/rfc/bcp/bcp47 .txt](http: .txt)和[http://www.w3.org/International/articles/language-tags/](http:)。<br> *範例：`en`代表英語，`en-US`代表美式英語，`de`代表德語。 * 
 - **緯度** - WGS84latitude（以十進制為單位）。該值必須大於或等於-90.0且小於或等於90.0。 *<br>例：羅馬羅馬競技場的` longitude `。該值必須大於或等於-180.0且小於或等於180.0。<br> *範例：羅馬羅馬競技場的`12.492269 `。 
 - **整數** - 整數。 
 - **Phone number** - 電話號碼。 
 - **時間** - HH:MM:SS 格式的時間（也接受 H:MM:SS）。該時間從服務日的`中午減去 12 小時`開始計算（實際上是午夜，夏令時發生變化的日子除外）。對於服務日午夜之後發生的時間，請以 HH:MM:SS 格式輸入大於 24:00:00 的時間值。<br> *範例：`14:30:00` 表示下午 2:30，或 `25:35:00` 表示string凌晨 1:35 。 ，其中旨在顯示，因此必須是人類可讀的。 
 - **時區** - 來自 [https://www.iana.org/time-zones](https:) 的 TZ 時區。時區名稱從不包含空格字符，但可以包含底線。請參閱 [http://en.wikipedia.org/wiki/List\_of\_tz\_zones](http: ) 以取得有效值清單。<br> *URL：` Asia/Asia/Tokyo`、`America/Los_Angeles` 或 `Africa/Cairo `。 URL URL中的字元必須正確轉義。請參閱以下 [](http: URL/4\_URI\_Recommentations.html](http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html)有關如何建立完全限定URL值的說明。 
 
### 欄位符號 
 適用於Float或整數欄位類型的符號： 
 
 * **非負** - 大於或等於 0。float0。屬性
 資料集的**主鍵**是唯一標識一行的欄位或欄位組合。當文件的所有提供的欄位都用於唯一標識行時，請使用Primary key (*)。 `Primary key (none)` 表示檔案只允許一行。 
 
 _範例： `trip_id`和`stop_sequence`欄位構成 [stop_times.txt](#stop_timestxt) 的主鍵。 
§|檔案名稱 |存在 |描述 | 
 |------|------|------| 
 | [agency.txt](#agencytxt) | **必填** |此資料集中提供服務的交通機構。 | 
 | [stops.txt](#stopstxt) | **必填** |在車輛接送乘客的地方停靠。也定義了車站和車站入口。 | 
 | [routes.txt](#routestxt) | **必填** |過境routes。路線是作為單一服務向乘客顯示的一組行程。 | 
 | [trips.txt](#tripstxt) | **必填** |每條路線的行程。行程是在特定時間內發生的兩次或多次stops的序列。 | 
 | [stop_times.txt](#stop_timestxt) | **必填** |每次行程vehicle到達和離開stops的時間。 | 
 | [calendar.txt](#calendartxt) | **有條件要求** |使用包含開始日期和結束日期的每週計畫指定服務日期。<br><br>有條件要求：<br> - **必需**，除非所有服務日期均在 [calendar_dates.txt](#calendar_datestxt) 中定義。<br> - 否則可選。 | 
 | [calendar_dates.txt](#calendar_datestxt) | **有條件要求** | [calendar.txt](#calendartxt) 中定義的服務的例外情況。<br><br>有條件要求：<br> - **必需** 如果省略 [calendar.txt](#calendartxt)。在這種情況下，[calendar_dates.txt](#calendar_datestxt) 必須包含所有服務日期。<br> - 否則可選。 | 
 | [fare_attributes.txt](#fare_attributestxt) |可選|公車機構routes的票價資訊。 | 
 | [fare_rules.txt](#fare_rulestxt) |可選|適用行程票價的規則。 | 
 | [時間範圍.txt](#timeframestxt) |可選|票價規則中使用的日期和時間段取決於date和時間因素。 | 
 | [fare_media.txt](#fare_mediatxt) |可選|描述可用於使用票價產品的票價媒體。<br><br>檔案 [fare_media.txt](#fare_mediatxt) 描述了 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 中未表示的概念。因此， [fare_media.txt](#fare_mediatxt) 的使用與檔案 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全分開。 | 
 | [fare_products.txt](#fare_productstxt) |可選|描述乘客可以購買的不同類型的車票或票價。<br><br>檔案 [fare_products.txt](#fare_productstxt) 描述 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 中未表示的票價產品。因此，[fare_products.txt](#fare_productstxt) 的使用與檔案 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全分開。 | 
 | [fare_leg_rules.txt](#fare_leg_rulestxt) |可選|個別旅行段的票價規則。<br><br>文件 [fare_leg_rules.txt](#fare_leg_rulestxt) 提供了更詳細的票價結構建模方法。因此，[fare_leg_rules.txt](#fare_leg_rulestxt) 的使用與檔案 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全分開。 | 
 | [fare_transfer_rules.txt](#fare_transfer_rulestxt) |可選|旅行航段之間transfers的票價規則。<br><br>與 [fare_leg_rules.txt](#fare_leg_rulestxt) 一起，檔案 [fare_transfer_rules.txt](#fare_transfer_rulestxt) 提供了更詳細的票價結構建模方法。因此，[fare_transfer_rules.txt](#fare_transfer_rulestxt) 的使用完全獨立於檔案 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt)。 | 
 | [areas.txt](#areastxt) |可選|地點的區域分組。 | 
 | [stop_areas.txt](#stop_areastxt) |可選|將stops指派給區域的規則。 | 
 | [網路.txt](#networkstxt) | **有條件禁止** |routes的網路分組。<br><br>有條件禁止：<br> - 如果 [routes.txt](#routestxt) 中存在` network_id ，則**禁止**。<br> - 否則可選。 | 
 | [.txt](#route_networkstxt) | **有條件禁止** |為網路分配routes的規則。<br><br>有條件禁止：<br> - 如果 [routes.txt](#routestxt) 中存在` network_id ，則**禁止**。<br> - 否則可選。 | 
 | [shapes.txt](#shapestxt) |可選|繪製vehicle行駛路徑的規則，有時稱為路線對齊。 | 
 | [frequencies.txt](#frequenciestxt) |可選|基於車頭時距的服務的車頭時距（行程之間的時間）或固定時間表服務的壓縮表示。 | 
 | [transfers.txt](#transferstxt) |可選|routes間轉乘點轉接的規則。 | 
 | [pathways.txt](#pathwaystxt) |可選|連接車站內各地點的通道。 | 
 | [levels.txt](#levelstxt) | **有條件要求** |車站內的樓層。<br><br>有條件要求：<br> - **必要** 描述電梯pathways時（`pathway_mode=5）。<br> - 否則可選。 | 
 | [.txt](#location_groupstxt) |可選|一組stops，共同指示乘客可以要求上車或下車的位置。 | 
 | [.txt](#location_group_stopstxt) |可選|將stops指派給地點群組的規則。 | 
 | [locations.geojson](#locationsgeojson) |可選|按需服務的乘客接送請求區域，表示為 GeoJSON 多邊形。 | 
 | [booking_rules.txt](#booking_rulestxt) |可選|乘客要求的服務的預訂資訊。 | 
 | [translations.txt](#translationstxt) |可選|面向客戶的資料集值的翻譯。 | 
 | [feed_info.txt](#feed_infotxt) |可選|資料集元數據，包括發布者、版本和過期資訊。 | 
 | [attributions.txt](#attributionstxt) |可選|數據集attributions。 | 
 
## 文件要求 
 
 以下要求適用於資料集文件的格式和內容： 
 
 * 所有文件必須保存為逗號分隔的文本。 
 * 每個文件的第一行必須包含欄位名稱。 [Field Definitions](#field-definitions) 部分的每個小節對應於GTFS資料集中的一個文件，並列出了該文件中可能使用的欄位名稱。 
 * 所有文件和欄位名稱區分大小寫。 
 * 欄位值不得包含製表符、回車符或換行符。 
 * 包含引號或逗號的欄位值必須以引號引起來。此外，欄位值中的每個引號前面都必須有引號。這與 Microsoft Excel 輸出逗號分隔 (CSV) 檔案的方式一致。有關 CSV 檔案格式的更多信息，請參閱 [http://tools.ietf.org/html/rfc4180](http:)。 
 以下範例示範了欄位值如何出現在逗號分隔檔中： 
 * **原始欄位值：** `Contains "quotes", commas and text` 
 * **CSV 檔案中的欄位值:* * `"Contains ""quotes"", commas and text"` 
 * 欄位值不得包含 HTML 標記、註解或轉義序列。 
 * 應刪除欄位或欄位名稱之間的多餘空格。許多解析器認為空格是值的一部分，這可能cause錯誤。 
 * 每行必須以 CRLF 或 LF 換行符號結束。 
 * 文件應採用 UTF-8 編碼以支援所有 Unicode 字元。包含 Unicode 位元組順序標記 (BOM) 字元的檔案是可接受的。有關 BOM 字元和 UTF-8 的更多信息，請參閱 [http://unicode.org/faq/utf_bom.html#BOM](http://unicode.org/faq/utf_bom.html#BOM )。 
 * 所有資料集檔案必須壓縮在一起。這些檔案必須直接位於根級別，而不是子資料夾中。 
 * 所有面向客戶的文字字串（包括車站名稱、路線名稱和車頭標誌）應使用混合大小寫（不是全部大寫），遵循能夠顯示小寫字符的顯示器上地名大寫的當地慣例（例如“Brighton” ）邱吉爾廣場`、`馬恩河畔維利耶`、`市場街`）。 
 * 在整個提要中應避免使用縮寫名稱和其他文本（例如 St. 代表街道），除非某個地點以縮寫名稱稱呼（例如“JFK 機場”）。縮寫可能會為螢幕閱讀器軟體和語音使用者介面的可訪問性帶來問題。消費軟體可以被設計為可靠地將完整單字轉換為縮寫以供顯示，但從縮寫轉換為完整單字更容易出現更大的錯誤風險。 
 
## 資料集發布和一般實踐 
 
 * 資料集應發佈在公共、永久URL上，包括 zip 檔名。 （例如， agency/gtfs/gtfs.zip）。理想情況下， URL應可直接下載，無需登入即可存取文件，以便於透過使用軟體應用程式進行下載。雖然建議（也是最常見的做法）公開下載GTFS資料集，但如果資料提供者確實需要出於許可或其他原因控制對GTFS的訪問，則建議使用 API 金鑰控制對GTFS資料集的訪問，這將有助於自動下載。 
 * GTFS資料應迭代發布，以便穩定位置的單一文件始終包含交通agency（或多個機構）的最新官方服務描述。 
 * 資料集應盡可能在資料迭代中維護``stop_id``、 ``route_id``和`agency_id `的持久標識符（ id欄位）。 
 * 一個GTFS資料集應包含目前和即將推出的服務（有時稱為`合併`資料集）。有多個可用的[合併工具](../../../resources/gtfs/#gtfs-merge-tools)可用於從兩個不同的GTFS來源建立合併資料集。 
 * 在任何時候，發布的GTFS資料集應至少在接下來的 7 天內有效，理想情況下只要運營商確信時間表將繼續運行即可。 
 * 如果可能， GTFS資料集應至少涵蓋接下來 30 天的服務。 
 * 舊服務（過期日曆）應從 Feed 中刪除。 
 * 如果服務修改將在 7 天或更短的時間內生效，則此服務變更應透過GTFS即時來源（服務建議或行程更新）而不是靜態GTFS資料集來表達。 
 * 託管GTFS資料的 Web 伺服器應配置為正確報告文件修改date（請參閱 [HTTP/1.1- Request for Comments 2616，第 14.29 節](https:#section-14.29))。 
 
## 欄位定義 
 
### agency.txt 
 
 檔案：**必填** 
 
 主鍵 (`agency_id`) 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `agency_id` |唯一ID | **有條件要求** |標示一個交通品牌，通常與交通agency同義。請注意，在某些情況下，例如當一個agency運作多個單獨的服務時，機構和品牌是不同的。本文件使用術語“agency”代替“品牌”。資料集可能包含來自多個機構的資料。<br><br>有條件要求：<br> - 當資料集包含多個交通機構的資料時，*​​必需**。<br> - 另有推薦。 | 
 | `agency_name` |Text| **必填** |運輸agency的全名。 | 
 | `agency_url` |URL| **必填** |運輸agency的URL 。 | 
 | `agency_timezone` |時區 | **必填** |公車agency所在的時區。如果資料集中指定了多個機構，則每個機構必須具有相同的`agency_timezone`。 | 
 | `agency_lang` |語言代碼 |可選|該公交agency使用的主要語言。應提供幫助GTFS使用者為資料集選擇大寫規則和其他特定於語言的設定。 | 
 | `agency_phone` |Phone number|可選|指定agency的語音電話號碼。此欄位是一個string值，表示代理服務區域的典型電話號碼。它可能包含標點符號來對數字的數字進行分組。允許使用可撥號文字（例如 TriMet 的“503-238-RIDE”），但該欄位不得包含任何其他描述性文字。 | 
 | `agency_fare_url` |URL|可選|允許乘客在線上購買該agency的車票或其他票價工具的網頁URL 。 | 
 | `agency_email` |Email|可選|Email地址由該機構的客戶服務部門主動監控。這個電子郵件地址應該是一個直接聯絡點，乘客可以透過該地址聯繫該agency的客戶服務代表。 | 
 
### stops.txt 
 
 檔案：**必需** 
 
 主鍵 (`stop_id`) 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `stop_id` |唯一ID | **必填** |標識位置：車站/月台、車站、入口/出口、通用節點或登機區域（請參閱`location_type`）。<br><br>所有 `stops.stop_id、 locations.geojson和 `location_groups.location_group_id` 值中的ID 必須是唯一的。<br><br>多條routes可以使用相同的`stop_id`。 | 
 | `stop_code` |Text|可選|識別騎士位置的短文字或數字。這些代碼通常用於基於電話的交通資訊系統或列印在標誌上，以便乘客更輕鬆地獲取特定位置的資訊。如果面向公眾，`stop_code`可能與``stop_id``相同。對於沒有向乘客提供代碼的地點，此欄位應留空。 | 
 | `stop_name` |Text| **有條件要求** |地點名稱。 `stop_name` 應與印在時間表、線上發布或標誌上的機構面向乘客的位置名稱相符。若要翻譯成其他語言，請使用 [translations.txt](#translationstxt)。<br><br>當位置是登機區（`location_type=4）時，`stop_name應包含agency顯示的登機區名稱。它可能只是一個字母（就像一些歐洲城際火車站一樣），也可能是“輪椅登機區”（紐約地鐵）或“短途列車頭”（巴黎 RER）之類的文字。<br><br>有條件要求：<br> - 對於stops(`location_type=0`)、車站 (`location_type=1`) 或入口/出口 (`location_type=2`) 的位置，**必要**。<br> - 對於通用節點 (`location_type=3) 或登機區域 (`location_type=4) 的位置是可選的。 
 | `tts_stop_name` |Text|可選| `stop_name` 的可讀版本。有關詳細信息，請參閱[術語定義](#term-definitions) 中的`文字轉語音欄位`。 | 
 | `stop_desc` |Text|可選|提供有用、優質資訊的位置描述。不應與 `stop_name` 重複。 
 | `停止

緯度` |緯度 | **有條件要求** |位置的緯度。<br><br>對於stops/平台（`location_type=0）和登機區域（`location_type=4），座標必須是公車桿的座標（如果存在），否則是旅客上vehicle的位置（在人行道上）或平台上，而不是在vehiclestops的道路或軌道上）。<br><br>有條件要求：<br> - 對於stops(`location_type=0`)、車站 (`location_type=1`) 或入口/出口 (`location_type=2`) 的位置，**必要**。<br> - 對於通用節點 (`location_type=3) 或登機區域 (`location_type=4) 的位置是可選的。 
 | `stop_lon` |經度 | **有條件要求** |位置的經度。<br><br>對於stops/平台（`location_type=0）和登機區域（`location_type=4），座標必須是公車桿的座標（如果存在），否則是旅客上vehicle的位置（在人行道上）或平台上，而不是在vehiclestops的道路或軌道上）。<br><br>有條件要求：<br> - 對於stops(`location_type=0`)、車站 (`location_type=1`) 或入口/出口 (`location_type=2`) 的位置，**必要**。<br> - 對於通用節點（`location_type=3）或登機區（`location_type=4）的位置是可選的。 | 
 | `zone_id|身分證 |可選|標識停靠站的票價區域。如果此記錄代表車站或車站入口，則忽略 `zone_id。 
 | `stop_url` |URL|可選|有關該位置的網頁的URL 。這應該與`agency.agency_url和`routes.route_url欄位值不同。 | 
 | `location_type` |枚舉 |可選|位置類型。有效選項有：<br><br> `0`（或空白）- **停止**（或 **平台**）。乘客上下交通vehicle的地點。在`parent_station`中定義時稱為平台。<br> `1` - **站**。包含一個或多個平台的實體結構或區域。<br> `2` - **入口/出口**。乘客可以從街道進出車站的地方。如果一個入口/出口屬於多個車站，則它可以透過pathways連結到兩個車站，但資料提供者必須選擇其中一個作為父站。<br> `3` - **通用節點**。車站內的位置，不符合任何其他`location_type ，可用於將[pathways.txt](#pathwaystxt)中定義的pathways連結在一起。<br> `4` - **登機區**。月台上乘客可以上下車輛的特定位置。 
 | `parent_station` |外部 ID 引用 `stops.stop_id| **有條件要求** |定義 [stops.txt](#stopstxt) 中定義的不同位置之間的層次結構。它包含父位置的 ID，如下所示：<br><br> - **車站/平台** (`location_type=0)：`parent_station欄位包含車站的 ID。<br> - **車站** (`location_type=1`)：此欄位必須為空。<br> - **入口/出口**（`location_type=2）或**通用節點**（`location_type=3）：`parent_station欄位包含網站的ID（`location_type=1）<br> - **登機區**（`location_type=4）：`parent_station欄位包含平台的ID。<br><br>有條件要求：<br> - 對於入口 (`location_type=2)、通用節點 (`location_type=3) 或登機區 (`location_type=4) 的位置，**必要**。<br> -stops/月台可選（`location_type=0）。<br> - 禁止進入車站（`location_type=1）。 
 | `stop_timezone` |時區 |可選|位置的時區。如果該位置有父電台，它將繼承父電台的時區，而不是應用自己的時區。具有空 ` stop_timezone的車站和無父stops繼承由 ` agency.agency_timezone指定的時區。 [stop_times.txt](#stop_timestxt) 中提供的時間是由`agency.agency_timezone指定的時區，而不是`stop_timezone。這可確保行程中的時間值在行程過程中始終增加，無論行程跨越哪個時區。 | 
 | `wheelchair_boarding` |枚舉 |可選|指示是否可以從該位置搭乘輪椅。有效選項有：<br><br>對於無父母stops：<br> `0`或空 - 沒有停靠點的無障礙訊息。<br> `1` - 該站的部分車輛可供輪椅乘客搭乘。<br> “2” - 此站無法搭乘輪椅。<br><br>對於兒童stops：<br> `0` 或空 - Stop 將從父站繼承其 `wheelchair_boarding行為（如果在父站中指定）。<br> `1` - 存在從車站外到特定車站/月台的一些無障礙路徑。<br> `2` - 不存在從車站外到特定車站/月台的無障礙路徑。<br><br>車站出入口：<br> `0` 或空 - 車站入口將從父車站繼承其 `wheelchair_boarding行為（如果為父車站指定）。<br> “`1`” - 車站入口可供輪椅通行。<br> `2` - 從車站入口到stops/月台沒有無障礙路徑。 | 
 | `level_id` |外部 ID 引用 `levels.level_id|可選|位置的等級。多個未連結的站可以使用相同的等級。 
 | `platform_code` |Text|可選|月台車站（屬於車站的車站）的月台識別碼。這應該只是平台標識符（例如“G”或“3”）。不應包含“平台”或“軌道”（或提要的特定語言的等效詞）之類的詞。這使得 Feed 消費者能夠更輕鬆地將平台標識符國際化和在地化為其他語言。 | 
 
 
### routes.txt 
 
 文件：**必需** 
 
 主鍵 (`route_id`) 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `route_id` |唯一ID | **必填** |標識一條路線。 | 
 | `agency_id` |外部 ID 引用 `agency.agency_id| **有條件要求** |代理指定航線。<br><br>有條件要求：<br> - **必要** 如果在 [agency.txt](#agencytxt) 中定義了多個機構。<br> - 另有推薦。 | 
 | `route_short_name` |Text| **有條件要求** |路線的簡稱。通常是騎士用來識別路線的簡短抽象標識符（例如“32”、“100X”、“綠色”）。可以定義`route_short_name和`route_long_name。<br><br>有條件要求：<br> - 如果`routes.route_long_name為空，則**必需**。<br> - 如果有簡短的服務名稱，則建議使用。這應該是該服務的常見乘客姓名，並且不應超過 12 個字元。 | 
 | `route_long_name|Text| **有條件要求** |路線的全名。這個名稱通常比`route_short_name`更具描述性，並且通常包含路線的目的地或停靠點。可以定義`route_short_name和`route_long_name。<br><br>有條件要求：<br> - 如果`routes.route_short_name為空，則**必要**。<br> - 否則可選。 | 
 | `route_desc|Text|可選|提供有用、優質資訊的路線描述。不應與 `route_short_name或 `route_long_name重複。<hr> _範例：`A`列車始終在曼哈頓 Inwood-207 St 和皇后區 Far Rockaway-Mott Avenue 之間運行。另外，從上午 6 點左右到午夜左右，Inwood-207 St 和 Lefferts Boulevard 之間還有額外的`A`列車運行（列車通常在 Lefferts Blvd 和 Far Rockaway 之間交替運行）。 
 | `route_type` |枚舉 | **必填** |指示路線上使用的交通類型。有效選項有：<br><br> `0` - 有軌電車、有軌電車、輕軌。大都會區內的任何輕軌或街道系統。<br> `1` - 地鐵，地鐵。大都會區內的任何地下鐵路系統。<br> `2` - 鐵路。用於城際或長途旅行。<br> `3` - 公共汽車。用於短途和長途巴士routes。<br> `4` - 渡輪。用於短途和長途船隻服務。<br> `5` - 纜車。用於電纜在vehicle下方運行的街道級軌道車（例如舊金山的纜車）。<br> `6` - 空中升降機、懸吊式纜車（例如纜車、空中纜車）。纜索運輸，其中船艙、汽車、吊船或開放式椅子透過一條或多根纜索懸掛。<br> `7` - 纜車。任何專為陡坡設計的鐵路系統。<br> `11` - 無軌電車。電動公車使用電線桿從架空電線取得電力。<br> `12` - 單軌鐵路。軌道由單根鋼軌或梁組成的鐵路。 | 
 | `route_url|URL|可選|有關特定路線的網頁的URL 。應與`agency.agency_url值不同。 | 
 | `route_color` |顏色 |可選|與面向公眾的材料相符的路線顏色指定。省略或留空時預設為白色 (`FFFFFF`)。在黑白螢幕上查看時，`route_color`和`route_text_color`之間的色差應提供足夠的對比度。 | 
 | `route_text_color` |顏色 |可選|用於在`route_color`背景下繪製的文字的清晰顏色。省略或留空時預設為黑色 (`000000`)。在黑白螢幕上查看時，`route_color`和`route_text_color`之間的色差應提供足夠的對比度。 | 
 | `route_sort_order` |非負整數 |可選|以最適合向客戶展示的方式訂購routes。應先顯示 `route_sort_order值較小的路由。 | 
 | `continuous_pickup` |枚舉 | **有條件禁止** |表示乘客可以在路線的每次行程中沿著車輛行駛路徑（如 [shapes.txt](#shapestxt) 中所述）的任何點登上公車vehicle。有效選項有：<br><br> `0` - 連續停止拾取。<br> “`1`”或空 - 沒有連續停止拾取。<br> `2` - 必須致電agency安排連續停車取件。<br> `3` - 必須與司機協調安排連續停車接送。<br><br>可以透過在` stop_times.continuous_pickup`中為路線沿線的特定`stop_time `定義值來覆蓋` routes.continuous_pickup `的值。<br><br> **有條件禁止**：<br> - **禁止** 如果 ` stop_times。 start_pickup_drop_off_window` 或 `stop_times。 end_pickup_drop_off_window` 是為此路線的任何行程定義的。<br> - 否則可選。 | 
 | `continuous_drop_off` |枚舉 | **有條件禁止** |表示乘客可以在路線的每次行程中沿著車輛行駛路徑的任意點vehicle，如 [shapes.txt](#shapestxt) 中所述。有效選項有：<br><br> `0` - 連續停止下降。<br> “`1`”或空 - 沒有連續停止下降。<br> `2` - 必須致電agency安排連續停止還車。<br> `3` - 必須與司機協調安排連續停車下車。<br><br>可以透過在` stop_times.continuous_drop_off`中為路線沿線的特定`stop_time `定義值來覆寫` routes.continuous_drop_off `的值。<br><br> **有條件禁止**：<br> - **禁止** 如果 ` stop_times。 start_pickup_drop_off_window` 或 `stop_times。 end_pickup_drop_off_window` 是為此路線的任何行程定義的。<br> - 否則可選。 | 
 | `network_id` |身分證 | **有條件禁止** |標識一組routes。 [routes.txt](#routestxt) 中的多行可能具有相同的`network_id`。<br><br>有條件禁止：<br> - 如果 [route_networks.txt](#route_networkstxt) 檔案存在，則**禁止**。<br> - 否則可選。 
 
### trips.txt 
 
 文件：**必需** 
 
 主鍵 (`trip_id`) 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `route_id` |外部 ID 引用 `routes.route_id| **必填** |標識一條路線。 | 
 | `service_id|外部 ID 引用 `calendar.service_id或 `calendar_dates.service_id| **必填** |標識一條或多條routes提供服務的一組日期。 | 
 | `trip_id` |唯一ID | **必填** |標識一次行程。 | 
 | `trip_headsign` |Text|可選|標示牌上顯示的Text，向乘客標識行程的目的地。應用於區分同一路線上的不同服務模式。<br><br>如果在行程期間路標發生變化，則可以透過在行程中特定的stop_time的stop_times.stop_headsign中定義值來覆寫trip_headsign的值。 | 
 | ` trip_short_name` |Text|可選|面向公眾的文字用於識別乘客的行程，例如，識別通勤鐵路旅行的火車號碼。如果乘客通常不依賴行程名稱，則 `trip_short_name` 應為空。 `trip_short_name` 值（若有提供）應唯一標識服務天內的行程；它不應用於目的地名稱或有限/明確指定。 | 
 | `direction_id` |枚舉 |可選|指示行程的行駛方向。該欄位不應該在路由中使用；它提供了一種在發佈時間表時按方向分隔行程的方法。有效選項有：<br><br> `0` - 朝一個方向行駛（例如出境旅行）。<br> ``1`` - 沿著相反方向行駛（例如入境行駛）。<hr> *範例：`trip_headsign和`direction_id`欄位可以一起使用來為一組行程的每個方向上的行進分配名稱。 [trips.txt](#tripstxt) 檔案可以包含這些用於時間表的記錄：*<br> `trip_id,...,trip_headsign,direction_id`<br> `1234,...,Airport,0`<br> `1505,...,Downtown,1` | 
 | `block_id` |身分證 |可選|標識行程所屬的區塊。一個區塊由單次行程或使用同一vehicle進行的多次連續行程組成，由共享服務天數和`block_id`定義。 `block_id` 可能有不同服務天數的行程，從而形成不同的區塊。請參閱[下面的範例](#example-blocks-and-service-day)。要提供座位內transfers訊息，應提供 ` transfer_type的 [transfers](#transferstxt)。 | 
 | `shape_id` |外部 ID 引用 `shapes.shape_id | **有條件要求** |標示描述行程的vehicle行駛路徑的地理空間shape。<br><br>有條件要求：<br> - 如果行程具有在 [routes.txt](#routestxt) 或 [stop_times.txt](#stop_timestxt) 中定義的連續上車或下車行為，則為**必需**。<br> - 否則可選。 | 
 | `wheelchair_accessible` |枚舉 |可選|表示輪椅可通行。有效選項有：<br><br> `0`或空 - 沒有行程的無障礙資訊。<br> “`1`” - 此特定行程中使用的車輛可容納至少一名坐輪椅的乘客。<br> `2` - 此行程不接待使用輪椅的乘客。 | 
 | `bikes_allowed` |枚舉 |可選|指示是否允許自行車。有效選項有：<br><br> `0`或空 - 行程中沒有自行車資訊。<br> “`1`” - 此特定行程中使用的車輛可容納至少一輛自行車。<br> “2” - 此行程不允許攜帶自行車。 | 
 
#### 範例：區塊和服務日 
 
 下面的範例有效，一週中的每一天都有不同的區塊。 

|route_id |trip_id |service_id |block_id | <span style="font-weight:normal">*（首站時間）*</span> | <span style="font-weight:normal">*（最後一站時間）*</span> | 
 |----------|---------|--------------------------------|----------|--------------------------------------|-------------------------| 
 |紅色|trip_1 |週一、週二、週三、週四、週五、週六、週日 |紅環 | 22:00:00 | 22:00:00 22:55:00 | 22:55:00 
 |紅色|trip_2 |週五-週六-週日 |紅環 | 23:00:00 | 23:00:00 23:55:00 | 23:55:00 
 |紅色|trip_3 |週五至週六 |紅環 | 24:00:00 | 24:00:00 24:55:00 | 24:55:00 
 |紅色|trip_4 |星期一、星期二、星期三、星期四 |紅環 | 20:00:00 | 20:00:00 20:50:00 | 20:50:00 
 |紅色|trip_5 |星期一、星期二、星期三、星期四 |紅環 | 21:00:00 | 21:00:00 21:50:00 | 21:50:00 
 
 上表註： 
 
 * 例如，週五到週六早上，單vehicle運行 `trip_1`、`trip_2` 和 `trip_3`（晚上 10:00 到凌晨 12:55） 。請注意，最後一班發生在周六中午 12:00 至 12:55，但屬於週五“服務日”的一部分，因為時間為 24:00:00 至 24:55:00。 
 * 週一、週二、週三和週四，單vehicle在晚上 8:00 至晚上 10:55 期間在一個街區內運行“trip_1”、“trip_4”和“trip_5”。 
 
### stop_times.txt 
 
 檔案：**必需** 
 
 主鍵 (`trip_id`, `stop_sequence`) 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `trip_id` |引用`trips.trip_id` 的外部 ID | **必填** |標識一次行程。 | 
 | `arrival_time` |時間 | **有條件要求** |在` agency.agency_timezone`（而非`stops.stop_timezone `）指定的時區中，特定行程（由` stop_times.stop_id`定義）到達停靠點（由`stop_times.trip_id `定義）的時間。<br><br>如果停靠點沒有單獨的arrival和departure時間，則 `arrival_time和`departure_time`應相同。<br><br>對於服務日午夜之後發生的時間，請以 HH:MM:SS 格式輸入大於 24:00:00 的時間值。<br><br>如果無法獲得準確的arrival和departure時間（`timepoint=1` 或空），則應提供估計或插值的arrival和departure時間（`timepoint=0`）。<br><br>有條件要求：<br> - **對於行程中的第一站和最後一站來說是必需的**（由 `stop_times.stop_sequence` 定義）。<br> - **必需**`timepoint=1`。<br> - 定義了`start_pickup_drop_off_window`或`end_pickup_drop_off_window`時**禁止**。<br> - 否則可選。 
 | `departure_time` |時間 | **有條件要求** |在` agency.agency_timezone`（而非`stops.stop_timezone `）指定的時區中，從特定行程（由` stop_times.stop_id`定義）的停靠點（由`stop_times.trip_id `定義）出發的時間。<br><br>如果停靠點沒有單獨的arrival和departure時間，則 `arrival_time和`departure_time`應相同。<br><br>對於服務日午夜之後發生的時間，請以 HH:MM:SS 格式輸入大於 24:00:00 的時間值。<br><br>如果無法獲得準確的arrival和departure時間（`timepoint=1` 或空），則應提供估計或插值的arrival和departure時間（`timepoint=0`）。<br><br>有條件要求：<br> - **必需**`timepoint=1`。<br> - **定義了`start_pickup_drop_off_window`或`end_pickup_drop_off_window`時禁止**。<br> - 否則可選。 | 
 | `stop_id` |外部 ID 引用 `stops.stop_id| **有條件要求** |標識服務站點。行程期間提供服務的所有stops都必須在 [stop_times.txt](#stop_timestxt) 中具有記錄。引用的位置必須是stops/平台，即它們的“stops.location_type”值必須為“0”或為空。在同一行程中，一個站點可能會提供多次服務，並且多個行程和routes可能會為同一站點提供服務。<br><br>使用stops的隨選服務應按照這些stops提供服務的順序引用。資料消費者應假設可以從一個網站或地點到行程中稍後的任何網站或地點，前提是每個stop_time的 `pickup/drop_off_type和每個 ` end_pickup_drop_off_window的時間限制不禁止它。<br><br>有條件要求：<br> - 如果未定義“stop_times.location_group_id”和“stop_times.location_id”，則**必要**。<br> - 如果定義了 `stop_times.location_group_id` 或 `stop_times.location_id`，則**禁止**。 | 
 | `位置群組 ID` |外部 ID 引用 `location_groups.location_group_id` | **有條件禁止** |標識服務位置組，指示乘客可以要求上車或下車的stops組。行程期間提供服務的所有地點群組必須在 [stop_times.txt](#stop_timestxt) 中具有記錄。多個行程和routes可能會服務於同一位置群組。<br><br>使用位置組的隨選服務應按照這些位置組提供服務的順序引用。資料消費者應假設可以從一個網站或地點到行程中稍後的任何網站或地點，前提是每個stop_time的 `pickup/drop_off_type和每個 ` end_pickup_drop_off_window的時間限制不禁止它。<br><br> **有條件禁止**：<br> - 如果定義了 `stop_times.stop_id` 或 `stop_times.location_id`，則**禁止**。 | 
 | `位置 ID` |外部 ID 從“`locations.geojson`”引用“`id`” | **有條件禁止** |標識與乘客可以請求上車或下車的服務區域相對應的 GeoJSON 位置。行程期間提供服務的所有 GeoJSON 位置都必須在 [stop_times.txt](#stop_timestxt) 中具有記錄。多個行程和routes可能會服務於同一 GeoJSON 位置。<br><br>應依照這些位置中提供服務的順序引用位置內的隨選服務。資料消費者應假設可以從一個網站或地點到行程中稍後的任何網站或地點，前提是每個stop_time的 `pickup/drop_off_type和每個 ` end_pickup_drop_off_window的時間限制不禁止它。<br><br> **有條件禁止**：<br> - 若定義了 `stop_times.stop_id` 或 `stop_times.location_group_id`，則**禁止**。 | 
 | `stop_sequence` |非負整數 | **必填** |特定行程的stops、位置群組或 GeoJSON 位置的順序。這些值必須沿著行程增加，但不必是連續的。<hr> *範例：行程中的第一個位置可能有“`stop_sequence`”= “`1`”，行程中的第二個位置可能有“`stop_sequence`”=“23”，第三個位置可能有“`stop_sequence`”=“40” ， 等等。<br><br>在相同位置群組或 GeoJSON 位置內旅行需要 [stop_times.txt](#stop_timestxt) 中的兩筆記錄具有相同的 `location_group_id` 或 `location_id`。 | 
 | `stop_headsign` |Text|可選|標示牌上顯示的Text，向乘客標識行程的目的地。當車頭標誌在stops之間發生變化時，此欄位將覆蓋預設的` trips.trip_headsign `。如果在整個行程中顯示車頭標誌，則應使用` trips.trip_headsign `。<br><br>為一個 ` stop_time指定的 ` stop_headsign值不適用於同一行程中的後續 ` stop_time 。如果您想在同一行程中覆寫多個“ stop_time ”的“ trip_headsign ”，則必須在每個“ stop_time ”行中repeated“ stop_headsign ”值。 | 
 | `start_pickup_drop_off_window` |時間 | **有條件要求** |按需服務在 GeoJSON 位置、位置群組或停靠點可用的時間。<br><br> **有條件要求**：<br> - 如果定義了 `stop_times.location_group_id` 或 `stop_times.location_id`，則**必要**。<br> - 如果定義了``end_pickup_drop_off_window`` ，則**必要**。<br> - 如果定義了`arrival_time`或``departure_time`` ，則**禁止**。<br> - 否則可選。 | 
 | `end_pickup_drop_off_window` |時間 | **有條件要求** |點播服務在 GeoJSON 位置、位置群組或停止處結束的時間。<br><br> **有條件要求**：<br> - 如果定義了 `stop_times.location_group_id` 或 `stop_times.location_id`，則**必要**。<br> - 如果定義了``start_pickup_drop_off_window`` ，則**必要**。<br> - 如果定義了`arrival_time`或``departure_time`` ，則**禁止**。<br> - 否則可選。 | 
 | `pickup_type` |枚舉 | **有條件禁止** |表示拾取方式。有效選項有：<br><br> `0`或空 - 定期安排取貨。<br> “`1`” - 沒有可用的接送服務。<br> `2` - 必須致電agency安排取貨。<br> `3` - 必須與司機協調安排接送。<br><br> **有條件禁止**：<br> - 如果定義了“`start_pickup_drop_off_window`”或“`end_pickup_drop_off_window`”，則“ pickup_type =0” **禁止**。<br> - 如果定義了“`start_pickup_drop_off_window`”或“`end_pickup_drop_off_window`”，則“ pickup_type =3” **禁止**。<br> - 否則可選。 | 
 | ` drop_off_type` |枚舉 | **有條件禁止** |表示投放方式。有效選項有：<br><br> `0`或空 - 定期安排投放。<br> “`1`” - 不提供下車服務。<br> `2` - 必須致電agency安排送機。<br> `3` - 必須與司機協調安排還車。<br><br> **有條件禁止**：<br> - 如果定義了``start_pickup_drop_off_window``或``end_pickup_drop_off_window`` ，則` drop_off_type =0` **禁止**。<br> - 否則可選。 | 
 | `continuous_pickup` |枚舉 | **有條件禁止** |指示乘客可以在 [shapes.txt](#shapestxt) 所描述的車輛行駛路徑上的任何點登上交通vehicle，從當前 ` stop_time ` 到行程`stop_sequence`中的下一個 ` stop_time ` 。有效選項有：<br><br> `0` - 連續停止拾取。

br> `1`或空 - 沒有連續停止拾取。<br> `2` - 必須致電agency安排連續停車取件。<br> `3` - 必須與司機協調安排連續停車接送。<br><br>如果填入此字段，它將覆寫 [routes.txt](#routestxt) 中定義的任何連續接送行為。如果此欄位為空，則 `stop_time` 將繼承 [routes.txt](#routestxt) 中定義的任何連續接送行為。<br><br> **有條件禁止**：<br> - 如果定義了``start_pickup_drop_off_window``或``end_pickup_drop_off_window`` ，則**禁止**。<br> - 否則可選。 | 
 | `continuous_drop_off ` |枚舉 | **有條件禁止** |指示乘客可以在 [shapes.txt](#shapestxt) 所描述的車輛行駛路徑上的任何點從交通vehicle下車，從該` stop_time `到行程``stop_sequence` `中的下一個` stop_time `。有效選項有：<br><br> `0` - 連續停止下降。<br> “`1`”或空 - 沒有連續停止下降。<br> `2` - 必須致電agency安排連續停止還車。<br> `3` - 必須與司機協調安排連續停車下車。<br><br>如果填充此字段，它將覆蓋 [routes.txt](#routestxt) 中定義的任何連續下車行為。如果此欄位為空，則 `stop_time繼承 [routes.txt](#routestxt) 中定義的任何連續下車行為。<br><br> **有條件禁止**：<br> - 如果定義了``start_pickup_drop_off_window``或``end_pickup_drop_off_window`` ，則**禁止**。<br> - 否則可選。 | 
 | `shape_dist_traveled` |非負float|可選|沿著關聯shape行駛的實際距離，從第一個停靠點到此記錄中指定的停靠點。此欄位指定在行程期間任兩個stops之間要繪製多少shape。必須採用與 [shapes.txt](#shapestxt) 中使用的單位相同的單位。用於 `shape_dist_traveled的值必須隨`stop_sequence`一起增加；它們不得用於顯示沿路線的反向行駛。<br><br>建議用於具有循環或內聯的routes（vehicle在一次行程中穿過或行駛過路線的同一部分）。請參閱[`shapes.shape_dist_traveled](#shapestxt)。<hr> *範例：如果公車從shape起點到終點的行駛距離為 5.25 公里，則`shape_dist_traveled`=`5.25`。 
 | `timepoint` |枚舉 |推薦|指示vehicle是否嚴格遵守停靠點的arrival和departure時間，或這些時間是否為近似時間和/或插值時間。此欄位允許GTFS生產者提供插值停止時間，同時指示時間為近似值。有效選項有：<br><br> “0” - 時間被視為近似值。<br> `1`或空 - 時間被認為是準確的。 | 
 | `pickup_booking_rule_id` | ID 引用 `booking_rules.booking_rule_id` |可選|確定該停止時間的登機預訂規則。<br><br>當`pickup_type=2`時推薦。 | 
 | `drop_off_booking_rule_id` | ID 引用 `booking_rules.booking_rule_id` |可選|確定該停靠時間的下車預訂規則。<br><br>當 `drop_off_type =2` 時推薦。 | 
 
#### 按需服務路由行為 
 - 在提供出發地和目的地之間的路由或旅行時間時，資料消費者應忽略具有相同`trip_id`stop_times.txt具有`start_pickup_drop_off_window`和定義了“`end_pickup_drop_off_window`” 。有關演示應忽略哪些內容的範例，請參閱[資料範例頁](../examples/flex/#ignoring-intermediate-stop-times-records-with-pickupdrop-off-windows)。 
 - 禁止在兩個或多個具有相同``trip_id``的stop_times.txt記錄之間同時重疊locations.geojson “`id`”幾何、“start/end_pickup_drop_off_window”時間以及“pickup_type”或“drop_off_type ”。有關示範禁止內容的範例，請參閱[資料範例頁面](../examples/flex/#zone-overlap-constraint)。 
 
### calendar.txt 
 
 檔案：**有條件必需** 
 
 主鍵 (`service_id`) 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `service_id|唯一ID | **必填** |標識一條或多條routes提供服務的一組日期。 | 
 | `monday` |枚舉 | **必填** |指示服務是否在``start_date``和`end_date `欄位指定的date範圍內的所有星期一執行。請注意，特定日期的例外情況可能會在 [calendar_dates.txt](#calendar_datestxt) 中列出。有效選項有：<br><br> “`1`” -date範圍內的所有星期一均提供服務。<br> `0` -date範圍內的星期一不提供服務。 | 
 | `tuesday` |枚舉 | **必填** |功能與“monday”相同，但適用於星期二 | 
 | `wednesday` |枚舉 | **必填** |功能與“monday”相同，但適用於星期三 | 
 | `thursday` |枚舉 | **必填** |功能與“monday”相同，但適用於星期四 | 
 | `friday` |枚舉 | **必填** |功能與“monday”相同，但適用於星期五 | 
 | `saturday` |枚舉 | **必填** |功能與“monday”相同，但適用於星期六。 | 
 | `sunday` |枚舉 | **必填** |功能與“monday”相同，但適用於星期日。 | 
 | `start_date` |日期 | **必填** |服務間隔的開始服務日。 | 
 | `end_date` |日期 | **必填** |服務間隔的結束服務日。該服務日包含在間隔內。 | 
 
### calendar_dates.txt 
 
 檔案：**有條件需要** 
 
 主鍵（`service_id`、`date`） 
 
 [calendar_dates.txt](#calendar_datestxt )表按date明確啟動或停用服務。它可以以兩種方式使用。 
 
 * 建議：將 [calendar_dates.txt](#calendar_datestxt) 與 [calendar.txt](#calendartxt) 結合使用來定義 [calendar.txt](#calendartxt) 中定義的預設服務模式的例外情況。如果服務總體上是定期的，並且在明確的日期上有一些變化（例如，為了適應特殊活動服務或學校時間表），那麼這是一個很好的方法。在本例中，`calendar_dates.service_id`是引用`calendar.service_id`的外部 ID。 
 * 替代：省略 [calendar.txt](#calendartxt)，並在 [calendar_dates.txt](#calendar_datestxt) 中指定每個服務date。這允許相當大的服務變化並適應沒有正常每週時間表的服務。在本例中 ` service_id是一個 ID。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `service_id|外部 ID 引用 `calendar.service_id或 ID | **必填** |標識一條或多條routes發生服務異常時的一組日期。如果結合使用 [calendar_dates.txt](#calendartxt) 和 [calendar_dates.txt](#calendar_datestxt) ，每個 (` service_id、`date ) 對只能在[calendar_dates.txt](#calendar_datestxt) 中出現一次。如果 ` service_id值同時出現在 [calendar.txt](#calendartxt) 和 [calendar_dates.txt](#calendar_datestxt) 中，則 [calendar_dates.txt](#calendar_datestxt) 中的資訊將會修改[calendar.txt](#calendar_datestxt) 中指定的服務資訊。| 
 | `date` |日期 | **必填** |服務異常發生的日期。 | 
 | `exception_type` |枚舉 | **必填** |指示服務在date欄位中指定的date是否可用。有效選項有：<br><br> `1` - 已在指定date新增服務。<br> `2` - 指定date的服務已被刪除。<hr> *範例：假設一條路線在假日有一組行程，在所有其他日期有另一組行程。一個`service_id`可以對應到常規服務時間表，另一個`service_id`可以對應假期時間表。對於特定假期，[calendar_dates.txt](#calendar_datestxt) 檔案可用於將假期新增至假期“service_id”，並從常規“service_id”時間表中刪除該假期。 
 
### fare_attributes.txt 
 
 檔案：**可選** 
 
 主鍵 (`fare_id`) 
 
 **版本**<br> 
 有兩種描述票價的建模選項。 GTFS-Fares V1是用來描述最低票價資訊的傳統選項。 GTFS-Fares V2是一種更新的方法，可以更詳細地說明代理商的票價結構。兩者都可以出現在資料集中，但對於給定的資料集，資料使用者只能使用一種方法。建議GTFS- Fares V2優先於GTFS- Fares V1。<br><br>與GTFS- Fares V1相關的文件有：<br> - [fare_attributes.txt](#fare_attributestxt)<br> - [fare_rules.txt](#fare_rulestxt)<br><br>與GTFS- Fares V2相關的文件有：<br> - [fare_media.txt](#fare_mediatxt)<br> - [fare_products.txt](#fare_productstxt)<br> - [fare_leg_rules.txt](#fare_leg_rulestxt)<br> - [fare_transfer_rules.txt](#fare_transfer_rulestxt) 
 
<br> 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `fare_id` |唯一ID | **必填** |標示票價等級。 | 
 | `price` |非負float| **必填** |price，以 `currency_type指定的單位表示。 | 
 | `currency_type` |貨幣代碼 | **必填** |用於支付票價的貨幣。 | 
 | `payment_method` |枚舉 | **必填** |指示何時必須支付票價。有效選項有：<br><br> `0` - 車資在船上支付。<br> `1` - 必須在登機前支付票價。 | 
 | `transfers` |枚舉 | **必填** |表示該票價允許的transfers次數。有效選項有：<br><br> “0” - 此票價不允許transfers。<br> `1` - 乘客可以轉移一次。<br> `2` - 乘客可以換乘兩次。<br>空 - 允許無限制transfers。 | 
 | `agency_id` |外部 ID 引用 `agency.agency_id| **有條件要求** |識別票價的相關agency。<br><br>有條件要求：<br> - **必要** 如果在 [agency.txt](#agencytxt) 中定義了多個機構。<br> - 另有推薦。 | 
 | `transfer_duration` |非負整數 |可選|傳輸到期之前的時間長度（以秒為單位）。當 `transfers`=`0` 時，此欄位可用於指示票證的有效時間，也可留空。 | 
 
### fare_rules.txt 
 
 文件：**可選** 
 
 主鍵 (`*`) 
 
 [fare_rules.txt](#fare_rulestxt) 表指定票價如何[fare_attributes.txt](#fare_attributestxt) 中適用於行程。大多數票價結構使用以下規則的某種組合： 
 
 * 票價取決於出發站或目的地站。 
 * 票價取決於行程經過的區域。 
 * 票價取決於行程使用的路線。 
 
 有關示範如何使用 [fare_rules.txt](#fare_rulestxt) 和 [fare_attributes.txt](#fare_attributestxt) 指定票價結構的範例，請參閱 [FareExamples](https: web/20111207224351/https://code.google.com/p/googletransitdatafeed/wiki/FareExamples）位於GoogleTransitDataFeed 開源專案wiki 中。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `fare_id` |外部 ID 引用 `fare_attributes.fare_id` | **必填** |標示票價等級。 | 
 | `route_id` |外部 ID 引用 `routes.route_id|可選|標示與票價等級關聯的路線。如果存在多個具有相同票價屬性的routes，請在 [fare_rules.txt](#fare_rulestxt) 中為每條路線建立一條記錄。<hr> *範例：如果票價類別`b`在路線`TSW`和`TSE`上有效，則 [fare_rules.txt](#fare_rulestxt) 檔案將包含該票價類別的以下記錄：*<br> `fare_id,route_id`<br> `b,TSW`<br> `b,TSE`| 
 | `origin_id` |外部 ID 引用 `stops.zone_id|可選|標識起源區域。如果票價類別有多個始發區，請在 [fare_rules.txt](#fare_rulestxt) 中為每個 `origin_id` 建立一筆記錄。<hr> *範例：如果票價類別`b`對於從區域`2`或區域`8`出發的所有行程均有效，則 [fare_rules.txt](#fare_rulestxt) 檔案將包含該票價類別的以下記錄：*<br> `fare_id,...,origin_id`<br> `b,...,2`<br> `b,...,8` | 
 | `destination_id` |外部 ID 引用 `stops.zone_id|可選|標識目標區域。如果票價類別有多個目的地區域，請在 [fare_rules.txt](#fare_rulestxt) 中為每個 `destination_id建立一筆記錄。<hr> *範例：`origin_id`和`destination_id`欄位可以一起使用，以指定票價類別`b`對於區域 3 和 4 之間的旅行有效，並且對於區域 3 和 5 之間的旅行有效，[fare_rules.txt](#fare_rulestxt) 檔案將包含票價類別的以下記錄：*<br> `fare_id,...,origin_id,destination_id`<br> `b,...,3,4`<br> `b,...,3,5` | 
 | `contains_id` |外部 ID 引用 `stops.zone_id|可選|識別乘客在使用給定票價等級時將進入的區域。在某些系統中用於計算正確的票價等級。<hr> *範例：如果票價類別`c`與經過區域 5、6 和 7 的 GRT 路線上的所有行程相關聯，則 [fare_rules.txt](#fare_rulestxt) 將包含以下記錄：*<br> `fare_id,route_id,...,contains_id`<br> `c,GRT,...,5`<br> `c,GRT,...,6`<br> `c,GRT,...,7`<br> *由於所有 `contains_id` 區域都必須匹配才能應用票價，因此經過區域 5 和 6 但不經過區域 7 的行程不會有票價類別“c”。有關更多詳細信息，請參閱 GoogleTransitDataFeed 專案 wiki 中的 [](https: )。 
 
### timeframes.txt 
 
 文件：**可選** 
 
 主鍵 (`*`) 
 
 用於描述根據一天中的時間而變化的票價，一週中的某一天，或一年中的某一天。時間範圍可以與 [fare_leg_rules.txt](#fare_leg_rulestxt) 中的票價產品相關聯。<br> 
 相同的 `timeframe_group_id和 `service_id值不得有重疊的時間間隔。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `timeframe_group_id` |身分證 | **必填** |標識一個時間範圍或一組時間範圍。 | 
 | `start_time` |時間 | **有條件要求** |定義時間範圍的開始。該間隔包括開始時間。<br>禁止大於“24:00:00”的值。 `start_time`中的空值被視為 `00:00:00`。<br><br>有條件要求：<br> - 如果定義了“timeframes.end_time”，則**必要**。<br> - **否則禁止** | 
 | `end_time` |時間 | **有條件要求** |定義時間範圍的結束。該間隔不包括結束時間。<br>禁止大於“24:00:00”的值。 `end_time` 中的空值被視為 `24:00:00`。<br><br>有條件要求：<br> - 如果定義了“timeframes.start_time”，則**必要**。<br> - **否則禁止** | 
 | `service_id|外部 ID 引用 `calendar.service_id或 `calendar_dates.service_id| **必填** |標識時間範圍生效的一組日期。 | 
 
#### 時間範圍本地時間語義 
 - 當根據 [timeframes.txt](#timeframestxt) 評估票價事件的時間時，事件時間是使用本地時區以本地時間計算的，由 `stop_timezone`（如果指定），票價事件的車站或父站的時區。如果未指定，則應使用 Feed 的agency時區。 
 - “當天”是票價事件時間的當前date，相對於當地時區計算。 `當天`可能與票價段行程的服務日不同，特別是對於持續到午夜之後的行程。 
 - 票價事件的`當日時間`是使用GTFS時間欄位類型語意相對於`當天`計算的。 
 
### fare_media.txt 
 
 檔案：**可選** 
 
 主鍵 (`fare_media_id`) 
 
 描述可用於使用票價產品的不同票價媒體。票價介質是用來表示和/或驗證票價產品的實體或虛擬持有者。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `fare_media_id` |唯一ID | **必填** |標示票價媒體。 | 
 | `fare_media_name` |Text|可選|票價媒體的名稱。<br><br>對於交通卡 (`fare_media_type =2`) 或行動應用程式 (`fare_media_type =4`) 的票價媒體，應包含 `fare_media_name`，並且應與交付它們的組織使用的面向乘客的名稱相符。 | 
 | `fare_media_type` |枚舉 | **必填** |票價媒體的類型。有效選項有：<br><br> `0` - 無。當購買或驗證票價產品時不涉及票價媒體時使用，例如在未提供實體車票的情況下向司機或售票員支付現金。<br> ``1`` - 實體紙本車票，讓乘客在固定時間內搭乘一定數量的預購行程或無限次行程。<br> `2` - 已儲存車票、通行證或貨幣價值的實體交通卡。<br> `3` - cEMV（非接觸式 Europay、Mastercard 和 Visa）作為基於帳戶的票務的開環令牌容器。<br> `4` - 已儲存虛擬交通卡、車票、通行證或貨幣價值的行動應用程式。 
 
### fare_products.txt 
 
 文件：**可選** 
 
 主鍵 (`fare_product_id`, `fare_media_id`) 
 
 用來描述可購買的票價範圍由乘客計算或在計算多段旅程的總票價時予以考慮，例如轉乘費用。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `fare_product_id` |身分證 | **必填** |標識一個票價產品或一組票價產品。<br><br> [fare_products.txt](#fare_productstxt) 中的多個記錄可能共用相同的 `fare_product_id`，在這種情況下，從另一個檔案引用時將檢索具有該 ID 的所有記錄。<br><br>多個記錄可以共享相同的“fare_product_id”，但具有不同的“fare_media_id”，指示可用於使用票價產品的各種方法，可能以不同的價格。 | 
 | `fare_product_name` |Text|可選|顯示給乘客的票價產品名稱。 | 
 | `fare_media_id` |引用 `fare_media.fare_media_id` | 的外部 ID可選|標識可用於在行程期間使用票價產品的票價媒體。當`fare_media_id為空時，認為票價媒體未知。 
 | `amount` |貨幣amount| **必填** |票價產品的成本。可能為負數，表示轉讓折扣。可以為零來表示免費的票價產品。 | 
 | `currency` |貨幣代碼 | **必填** |票價產品成本的currency。 | 
 
 
### fare_leg_rules.txt 
 
 文件：**可選** 
 
 主鍵 (`network_id, from_area_id, to_area_id, from_timeframe_group_id, to_timeframe_group_id, fare_product_id`)§du§規則適用於個人旅行。 
 
 必須透過過濾文件中的所有記錄來查詢 [`fare_leg_rules.txt`](#fare_leg_rulestxt) 中的票價，以查找與乘客要乘坐的航段相符的規則。 
 
 處理航段費用： 
 
 1.文件 [fare_leg_rules.txt](#fare_leg_rulestxt) 必須透過定義旅行特徵的欄位進行過濾，這些欄位是： 
 - `fare_leg_rules.network_id` 
 - `fare_leg_rules.from_area_id` 
 - `fare_leg_rules.to_area_id` 
 - `fare_leg_rules.from_timeframe_group_id` 
 - `fare_leg_rules.to_timeframe_group_id §frame_group_time §<br/> 
 
 2.如果該航段與 [fare_leg_rules.txt](#fare_leg_rulestxt) 中基於旅行特徵的記錄完全匹配，則必須處理該記錄以確定該航段的費用。該文件以兩種方式處理空白條目：空語義或規則優先順序。 
<br/> 
 
 3.如果未找到精確匹配且 `rule_priority` 字段不存在，則必須檢查 `fare_leg_rules.network_id`、`fare_leg_rules.from_area_id` 和 `fare_leg_rules.to_area_id` 中的空條目以處理航段費用： §id ` 中的空條目§ - `fare_leg_rules.network_id` 中的空條目對應於 [routes.txt](#routestxt) 或 [networks.txt](#networkstxt) 中定義的所有網絡，不包括 `fare_leg_rules.network_id。 § 
 - `fare_leg_rules.from_area_id` 中的空條目對應於 `areas.area_id` 中定義的所有區域，不包括 `fare_leg_rules.from_area_id` 中列出的區域，不包括 `fare_leg_rules.to_area_id` 中列出的區域對應於前往`areas.area_id`中定義的所有區域，不包括`fare_leg_rules.to_area_id`中列出的區域 
<br/> 
 
 4.如果 `rule_priority` 欄位存在，則 
 - `fare_leg_rules.network_id` 中的空條目表示該航段的網路不影響該規則的符合。 
 - `fare_leg_rules.from_area_id` 中的空條目表示該航段的departure區域不影響該規則的匹配。 
 - `fare_leg_rules.to_area_id` 中的空條目表示該航段的arrival區域不影響該規則的匹配。 
<br/> 
 
 5.如果航段不符合上述任何規則，則票價未知。 

<br/> 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `leg_group_id|身分證 |可選|標識 [fare_leg_rules.txt](#fare_leg_rulestxt) 中的一組條目。<br><br>用於描述`fare_transfer_rules.from_leg_group_id和`fare_transfer_rules.to_leg_group_id之間的票價轉移規則。<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt) 中的多個條目可能屬於同一個 `fare_leg_rules.leg_group_id`。<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt) 中的相同條目（不包括 `fare_leg_rules.leg_group_id`）不得屬於多個 `fare_leg_rules.leg_group_id`。 
 | `network_id` |引用 `routes.network_id或 `networks.network_id的外部 ID可選|標識適用票價航段規則的航線網絡。<br><br>如果`rule_priority`欄位不存在，且沒有與正在過濾的` network_id `相符的` fare_leg_rules.network_id `值，則預設會符合空的` fare_leg_rules.network_id`。<br><br> `fare_leg_rules.network_id`中的空條目對應於 [routes.txt](#routestxt) 或 [.txt](#networkstxt) 中定義的所有網絡，不包括`fare_leg_rules.network_id`下列出的網絡<br><br>如果檔案中存在`rule_priority`字段，則`fare_leg_rules.network_id為空，表示該航段的航線網路不影響該規則的匹配。 | 
 | `from_area_id` |外部 ID 引用 `areas.area_id|可選|標識departure區域。<br><br>如果`rule_priority`欄位不存在，且沒有與正在過濾的` area_id `相符的` fare_leg_rules.from_area_id `值，則預設將符合空的` fare_leg_rules.from_area_id`。<br><br> `fare_leg_rules.from_area_id`中的空白條目對應於`areas.area_id`中定義的所有區域，不包括`fare_leg_rules.from_area_id`下列出的區域<br><br>如果文件中存在rule_priority字段，則為空的fare_leg_rules.from_area_id表示該航段的departure區域不影響該規則的匹配。 | 
 | `to_area_id` |外部 ID 引用 `areas.area_id|可選|標識arrival區域。<br><br>如果`rule_priority`欄位不存在，且沒有與正在過濾的` area_id `相符的` fare_leg_rules.to_area_id `值，則預設會符合空的` fare_leg_rules.to_area_id`。<br><br> `fare_leg_rules.to_area_id`中的空白條目對應於`areas.area_id`中定義的所有區域，不包括`fare_leg_rules.to_area_id`下列出的區域<br><br>如果檔案中存在rule_priority字段，則為空的fare_leg_rules.to_area_id表示該航段的arrival區域不影響該規則的匹配。 | 
 | `from_timeframe_group_id` |外部 ID 引用 `timeframes.timeframe_group_id|可選|定義票價段開始時票價驗證事件的時間範圍。<br><br>票價段的`開始時間`是指事件計畫發生的時間。例如，該時間可以是乘客在票價段開始時上車並驗證其票價的巴士的預定departure時間。對於下面的規則匹配語義，開始時間以本地時間計算，由 [timeframes.txt](#timeframestxt) 的 [Local Time Semantics](#timeframe-local-time-semantics) 決定。在適當的情況下，應使用票價航段departure事件的停靠站或站點進行時區解析。<br><br>對於指定`from_timeframe_group_id`的票價航段規則，該規則將符合特定航段，如果t

[timeframes.txt](#timeframestxt) 中至少存在一筆記錄，其中以下所有條件均成立<br>- `timeframe_group_id的值等於`from_timeframe_group_id值。<br> - 由記錄的 `service_id標識的日期集包含票價段開始時間的“當前日期”。<br> - 票價段的開始時間的`當天時間`大於或等於記錄的 `timeframes.start_time值並小於 `timeframes.end_time值。<br><br>空的fare_leg_rules.from_timeframe_group_id表示該航段的開始時間不影響該規則的匹配。 | 
 | `to_timeframe_group_id` |外部 ID 引用 `timeframes.timeframe_group_id|可選|定義票價段結束時票價驗證事件的時間範圍。<br><br>票價段的`結束時間`是事件計畫發生的時間。例如，該時間可以是公共汽車在票價段末端的預定arrival時間，乘客在此下車並驗證其票價。對於下面的規則匹配語義，結束時間以當地時間計算，由 [timeframes.txt](#timeframestxt) 的 [Local Time Semantics](#timeframe-local-time-semantics) 決定。在適當的情況下，應使用票價段arrival事件的停靠站或車站來進行時區解析。<br><br>對於指定`to_timeframe_group_id`的票價航段規則，如果 [timeframes.txt](#timeframestxt) 中至少存在一條記錄，並且滿足以下所有條件，則該規則將匹配特定航段<br>- `timeframe_group_id的值等於`to_timeframe_group_id值。<br> - 由記錄的 `service_id標識的日期集包含票價段結束時間的“當前日期”。<br> - 票價段結束時間的`當天時間`大於或等於記錄的 `timeframes.start_time值並小於 `timeframes.end_time值。<br><br>空的fare_leg_rules.to_timeframe_group_id表示該航段的結束時間不影響該規則的匹配。 | 
 | `fare_product_id` |外部 ID 引用 `fare_products.fare_product_id` | **必填** |行程所需的票價產品。 | 
 | `規則優先權` |非負整數 |可選|定義匹配規則應用於支線的優先順序，允許某些規則優先於其他規則。當`fare_leg_rules.txt`中的多個條目符合時，將選擇`rule_priority`值最高的規則或規則集。<br><br> “rule_priority”的空值被視為零。 | 
 
### fare_transfer_rules.txt 
 
 文件：**可選** 
 
 主鍵（`from_leg_group_id, to_leg_group_id, fare_product_id, transfer_count, duration_limit`） 
 
 航段之間transfers的票價規則[`fare_leg_rules.txt`](#fare_leg_rulestxt) 中定義的旅行。 
 
 處理多段旅程的費用： 
 
 1.應根據乘客的旅程確定所有單獨旅行段的`fare_leg_rules.txt`中定義的適用票價段組。 
 2.檔案 [fare_transfer_rules.txt](#fare_transfer_rulestxt) 必須透過定義轉帳特徵的欄位進行過濾，這些欄位是： 
 - `fare_transfer_rules.from_leg_group_id` 
 - `fare_transfer_rules.to_leg_group_id<br/> 
<br/> 
 
 3.如果根據轉帳特徵，轉帳與 [fare_transfer_rules.txt](#fare_transfer_rulestxt) 中的記錄完全匹配，則必須處理該記錄以確定轉帳費用。 
 4.如果未找到精確匹配，則必須檢查 `from_leg_group_id` 或 `to_leg_group_id` 中的空條目以處理轉乘費用： 
 - `fare_transfer_rules.from_leg_group_id` 中的空條目對應於定義的所有航段組`fare_leg_rules.leg_group_id` 下，不包括 `fare_transfer_rules.from_leg_group_id` 下列出的 
 - `fare_transfer_rules.to_leg_group_id` 中的空條目對應於 `fare_leg_rules.leg_group_id` 下定義的所有航段組，不包括 `fare_transfer_rules.to_leg_group_id` 下列出的航段組<br/>
<br/> 
 5.如果轉會不符合上述任何規則，則不存在轉會安排，並且各賽段被視為分開。 

<br/> 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `from_leg_group_id` |外部 ID 引用 `fare_leg_rules.leg_group_id ` |可選|標識一組轉乘前票價航段規則。<br><br>如果沒有與正在過濾的` leg_group_id `相符的` fare_transfer_rules.from_leg_group_id `值，則預設符合空的` fare_transfer_rules.from_leg_group_id`。<br><br> `fare_transfer_rules.from_leg_group_id` 中的空條目對應於 `fare_leg_rules.leg_group_id` 下定義的所有航段組，不包括 `fare_transfer_rules.from_leg_group_id`| 下列出的航段組。 
 | `to_leg_group_id` |外部 ID 引用 `fare_leg_rules.leg_group_id ` |可選|標識一組轉乘後票價航段規則。<br><br>如果沒有與正在過濾的` leg_group_id `相符的` fare_transfer_rules.to_leg_group_id `值，則預設符合空的` fare_transfer_rules.to_leg_group_id`。<br><br> `fare_transfer_rules.to_leg_group_id` 中的空條目對應於 `fare_leg_rules.leg_group_id` 下定義的所有航段組，不包括 `fare_transfer_rules.to_leg_group_id` 下列出的航段組。 
 | `transfer_count` |非零整數 | **有條件禁止** |定義傳輸規則可以套用到多少個連續transfers。<br><br>有效選項有：<br> `-1` - 沒有限制。<br> “`1`”或更多 - 定義傳輸規則可以跨越的transfers數量。<br><br>如果子旅程符合了多個不同的transfer_count的記錄，則選擇最小的transfer_count大於或等於該子旅程的目前轉移計數的規則。<br><br>有條件禁止：<br> - 如果`fare_transfer_rules.from_leg_group_id不等於`fare_transfer_rules.to_leg_group_id，則**禁止**。<br> - **必要**，如果 `fare_transfer_rules.from_leg_group_id` 等於 `fare_transfer_rules.to_leg_group_id`。 | 
 | `duration_limit` |正整數|可選|定義傳輸的持續時間限制。<br><br>必須以秒的整數增量表示。<br><br>如果沒有持續時間限制，`fare_transfer_rules.duration_limit必須為空。 | 
 | `duration_limit_type` |枚舉 | **有條件要求** |定義`fare_transfer_rules.duration_limit的相對開始和結束。<br><br>有效選項有：<br> `0` - 目前航段的departure票價驗證和下一航段的arrival票價驗證之間。<br> ``1`` - 目前航段的departure票價驗證與下一航段的departure票價驗證之間。<br> `2` - 目前航段的arrival票價驗證和下一航段的departure票價驗證之間。<br> `3` - 目前航段的arrival票價驗證和下一個航段的arrival票價驗證之間。<br><br>有條件要求：<br> - 如果定義了“fare_transfer_rules.duration_limit”，則**必需**。<br> - 如果 `fare_transfer_rules.duration_limit` 為空，則**禁止**。 | 
 | `fare_transfer_type` |枚舉 | **必填** |旅程中各航段之間換乘的費用處理方法：<br> ![](../../assets/2-leg.svg)<br>有效選項有：<br> `0` - 起始航段 `fare_leg_rules.fare_product_id` 加 `fare_transfer_rules.fare_product_id`； A+AB。<br> `1` - 始發航段 `fare_leg_rules.fare_product_id` 加上 `fare_transfer_rules.fare_product_id` 加上終點航段 `fare_leg_rules.fare_product_id`； A+AB+B。<br> `2` - `fare_transfer_rules.fare_product_id`; AB。<br><br>旅程中多次transfers之間的成本處理交互作用：<br> ![](../../assets/3-leg.svg)<br><table><thead><tr><th> `fare_transfer_type`</th><th>加工A>B</th><th>加工 B > C</th></tr></thead><tbody><tr><td> `0`</td><td>甲+乙</td><td>S+BC</td></tr><tr><td> `1`</td><td> A+AB+B</td><td> S+BC+C</td></tr><tr><td> `2`</td><td> AB</td><td> S+BC</td></tr></tbody></table>其中S表示前面航段和轉乘的總處理成本。 | 
 | `fare_product_id` |外部 ID 引用 `fare_products.fare_product_id` |可選|在兩個票價段之間轉乘所需的票價產品。如果為空，則傳輸規則的成本為0。 
 
 
### areas.txt 
 
 檔案：**可選** 
 
 主鍵 (`area_id) 
 
 定義區域識別碼。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `area_id` |唯一ID | **必填** |標識一個區域。在 [areas.txt](#areastxt) 中必須是唯一的。 | 
 | `area_name` |Text| **可選** |顯示給騎士的區域名稱。 | 
 
### stop_areas.txt 
 
 檔案：**可選** 
 
 主鍵 (`*`) 
 
 將 [stops.txt](#stopstxt) 中的stops分配給區域。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `area_id` |外部 ID 引用 `areas.area_id| **必填** |標識一個或多個``stop_id` `所屬的區域。可以在多個“ area_id ”中定義相同的“`stop_id`” 。 | 
 | `stop_id` |外部 ID 引用 `stops.stop_id| **必填** |標識停靠點。如果在此欄位中定義了一個車站（即帶有 `stops.location_type=1的車站），則假定其所有平台（即所有stops`stops.location_type=0且將此車站定義為 `stops 的車站） stops.parent_station`) 是同一區域的一部份。可以透過將平台分配給其他區域來覆蓋此行為。 | 
 
### .txt 
 
 文件：**有條件禁止** 
 
 主鍵 (`network_id`) 
 
 定義適用於票價規則的網路識別碼。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `network_id` |唯一ID | **必填** |標識一個網路。在 [networks.txt](#networkstxt) 中必須是唯一的。 | 
 | `network_name` |Text| **可選** |適用票價段規則的網路名稱，由當地agency及其乘客使用。 
 
### route_networks.txt 
 
 檔案：**有條件禁止** 
 
 主鍵 (`route_id` ) 
 
 將 [routes.txt](#routestxt) 中的routes分配給網路。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `network_id` |外部 ID 引用 `networks.network_id| **必填** |標識一個或多個``route_id``所屬的網路。一個`route_id`只能定義在一個`network_id中。 | 
 | `route_id` |外部 ID 引用 `routes.route_id| **必填** |標識一條路線。 | 
 
### shapes.txt 
 
 文件：**可選** 
 
 主鍵 (`shape_id`, `shape_pt_sequence`) 
 
 形狀描述了vehicle沿著特定路徑行駛的路徑路線對齊，並在檔案shapes.txt中定義。形狀與行程相關聯，由vehicle按順序經過的一系列點組成。形狀不需要精確截取停靠點的位置，但行程中的所有停靠點都應位於該行程shape的一小段距離內，即靠近連接shape點的直線段。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `shape_id` |身分證 | **必填** |識別shape。 | 
 | `shape_pt_lat` |緯度 | **必填** |shape點的緯度。 [shapes.txt](#shapestxt) 中的每筆記錄都代表一個用來定義shape的shape點。 | 
 | ` shape_pt_lon` |經度 | **必填** |shape點的經度。 | 
 | `shape_pt_sequence` |非負整數 | **必填** |shape點連接形成shape的順序。值必須隨著行程而增加，但不必是連續的。<hr> *範例：如果shape`A_shp`的定義中有三個點，則 [shapes.txt](#shapestxt) 檔案可能包含這些記錄來定義shape：*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence`<br> `A_shp,37.61956,-122.48161,0`<br> `A_shp,37.64430,-122.41070,6`<br> `A_shp,37.65863,-122.30839,11` | 
 | `shape_dist_traveled` |非負float|可選|沿著shape從第一個shape點到此記錄中指定的點行進的實際距離。旅行規劃者用來在地圖上顯示shape的正確部分。值必須隨著`shape_pt_sequence一起增加；它們不得用於顯示沿路線的反向行駛。距離單位必須與 [stop_times.txt](#stop_timestxt) 中使用的一致。<br><br>建議用於具有循環或內聯的routes（vehicle在一次行程中穿過或行駛過路線的同一部分）。 <br><img src="../../../assets/inlining.svg" width=200px style="display: block; margin-left: auto; margin-right: auto;"><br>如果vehicle在行程過程中的某一點折回或穿過路線路線，`shape_dist_traveled`對於闡明 [shapes.txt](#shapestxt) 中的部分點如何與 [stop_times.txt中的記錄相對應](#stop_timestxt )。<hr> *範例：如果公車沿著上面為 A_shp 定義的三個點行駛，則附加的 `shape_dist_traveled` 值（此處以公里為單位顯示）將如下所示：*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shape_dist_traveled`<br> `A_shp,37.61956,-122.48161,0,0`<br> `A_shp,37.64430,-122.41070,6,6.8310`<br> `A_shp,37.65863,-122.30839,11,15.8765` | 
 
### frequencies.txt 
 
 檔案：**可選** 
 
 主鍵 (`trip_id`, `start_time`) 
 
 [Frequencies.txt](#frequenciestxt) 代表以固定發車間隔（行程之間的時間）運行的行程。該文件可用於表示兩種不同類型的服務。 
 
 * 基於頻率的服務 (`exact_times`=`0`)，其中服務全天不遵循固定時間表。相反，操作員試圖嚴格保持預定的行程發車時間。 
 * 基於時間表的服務的壓縮表示（`exact_times`= `1`），在指定時間段內的行程具有完全相同的發車間隔。在基於時間表的服務中，運營商盡量嚴格遵守時間表。 


|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `trip_id` |引用`trips.trip_id` 的外部 ID | **必填** |標識適用指定服務發車間隔的行程。 | 
 | `start_time` |時間 | **必填** |第一vehicle以指定的發車時距從行程的第一個站點出發的時間。 | 
 | `end_time` |時間 | **必填** |服務在行程中的第一個站點變更為不同發車間隔（或停止）的時間。 | 
 | `headway_secs` |正整數| **必填** |在``start_time``和`end_time`指定的時間間隔內，行程中同一站點（車頭時距）出發之間的時間（以秒為單位）。可為同一行程定義多個車頭時距，但不得重疊。新的車頭時刻可能會在前一個車頭時刻結束的確切時間開始。 | 
 | `exact_times` |枚舉 |可選|指示旅行的服務類型。請參閱文件說明以取得更多資訊。有效選項有：<br><br> “0”或空 - 以頻率為基礎的行程。<br> ``1`` - 基於時間表的行程，全天發車時間完全相同。在這種情況下，`end_time`值必須大於最後一個所需行程``start_time`` ，但小於最後一個所需行程start_time + “`headway_secs``。 | 
 
### transfers.txt 
 
 檔案：**可選** 
 
 主鍵 (`from_stop_id`, `to_stop_id`, `from_trip_id`, `to_trip_id`, `from_route_id`, `to_route_id`) 
 
 計算行程時，使用GTFS的應用程式會根據允許的時間和停靠點鄰近程度插入transfers。 [Transfers.txt](#transferstxt) 指定所選transfers的附加規則和覆寫。 
 
 欄位`from_trip_id、`to_trip_id、`from_route_id和`to_route_id允許傳輸規則的更高層級的特定性。與 `from_stop_id` 和 `to_stop_id` 一起，特異性的排名如下： 
 
 1.定義了兩個`trip_id`：`from_trip_id` 和 `to_trip_id`。 
 2.定義一組`trip_id`和`route_id` ：(`from_trip_id和`to_route_id)或(`from_route_id和`to_trip_id)。 
 3.定義一個``trip_id`` ：`from_trip_id`或`to_trip_id`。 
 4.定義了兩個`route_id`：`from_route_id和`to_route_id。 
 5.定義一個`route_id` ：`from_route_id或`to_route_id。 
 6.僅定義了 `from_stop_id` 和 `to_stop_id`：未設定路線或行程相關欄位。 
 
 對於給定的一對有序的到達行程和出發行程，選擇適用於這兩個行程之間的具有最大特異性的轉乘。對於任何一對旅行，不應有兩次具有相同最大特異性的transfers。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `from_stop_id` |外部 ID 引用 `stops.stop_id| **有條件要求** |標示routes之間連接開始的停靠站或車站。如果此欄位指的是車站，則轉乘規則適用於其所有子stops。禁止引用`transfer_types`4 和5. 的電台。 
 | `to_stop_id` |外部 ID 引用 `stops.stop_id| **有條件要求** |標示routes之間連接的終點站。如果此欄位指的是車站，則轉乘規則適用於所有子stops。禁止引用`transfer_types`4 和5. 的電台。 
 | `from_route_id` |外部 ID 引用 `routes.route_id|可選|標識連線開始的路由。<br><br>如果定義了“from_route_id”，則轉乘將套用於給定“from_stop_id”路線上的到達行程。<br><br>如果同時定義了`from_trip_id和`from_route_id，則`trip_id`必須屬於`route_id`，且`from_trip_id優先。 | 
 | `to_route_id` |外部 ID 引用 `routes.route_id|可選|標識連線結束的路由。<br><br>如果定義了“to_route_id”，則轉乘將套用於給定“to_stop_id”路線上的出發行程。<br><br>如果同時定義了`to_trip_id和`to_route_id，則`trip_id`必須屬於`route_id`，並且`to_trip_id優先。 | 
 | `from_trip_id` |引用`trips.trip_id` 的外部 ID | **有條件要求** |標示routes之間連接開始的行程。<br><br>如果定義了“from_trip_id”，則接送服務將套用於給定“from_stop_id”的到達行程。<br><br>如果同時定義了`from_trip_id和`from_route_id，則`trip_id`必須屬於`route_id`，且`from_trip_id優先。如果“transfer_type”是“4”或“5”，則為必要。 | 
 | `to_trip_id` |引用`trips.trip_id` 的外國 ID | **有條件要求** |標識routes之間的連接結束的行程。<br><br>如果定義了“to_trip_id”，則轉乘將套用於給定“to_stop_id”的出發行程。<br><br>如果同時定義了`to_trip_id和`to_route_id，則`trip_id`必須屬於`route_id`，並且`to_trip_id優先。如果“transfer_type”是“4”或“5”，則為必要。 | 
 | `transfer_type` |枚舉 | **必填** |指示指定（`from_stop_id`, `to_stop_id`）對的連線類型。有效選項有：<br><br> `0`或空 -routes之間建議的轉乘點。<br> `1` - 兩條routes之間的定時換乘點。出發vehicle預計會等待到達車輛，並為乘客在routes之間換乘留出足夠的時間。<br> `2` - 轉乘需要arrival和departure之間的最短amount，以確保轉機。傳輸所需的時間由` min_transfer_time指定。<br> `3` - 無法在該地點的routes之間換乘。<br> `4` - 乘客可以透過留在同一vehicle上從一個行程換乘到另一個行程（`座位內換乘`）。有關此類傳輸的更多詳細資訊[如下](#linked-trips)。<br> `5` - 連續行程之間不允許座位transfers。乘客必須下車並重新上vehicle。有關此類傳輸的更多詳細資訊[如下](#linked-trips)。 | 
 | `min_transfer_time ` |非負整數 |可選|允許在指定stops的routes之間換乘所必需的時間量（以秒為單位）。 ` min_transfer_time` 應足以允許典型的乘客在兩個stops之間移動，包括允許每條路線的時間表變化的緩衝時間。 | 
 
#### 連結行程 
 
 以下內容適用於“transfer_type=4”和“=5”，它們用於將行程連結在一起，無論是否有座位內transfers。 
 
 連接在一起的行程必須由同一vehicle運作。vehicle可以與其他車輛耦合或脫開。 
 
 如果同時提供了連結行程傳輸和block_id且它們產生衝突的結果，則應使用連結行程傳輸。 
 
 `from_trip_id` 的最後一站在地理上應該靠近 `to_trip_id ` 的第一個站，並且 ` from_trip_id ` 的最後arrival時間應該早於但接近 ` to_trip_id ` 的第一個departure時間。如果` to_trip_id `行程發生在後續服務日，` from_trip_id `的最後arrival時間可能晚於` to_trip_id `的首次departure時間。 
 
 在常規情況下，行程可以一對一鏈接，但也可以一對一、n對1或n對n鏈接以表示更複雜的行程延續。例如，兩個列車行程（下圖中的行程 A 和行程 B）可以在公共車站進行vehicle耦合操作後合併為單一列車行程（行程 C）： 
 
 - 在 1 對 n 中繼續，每個` to_trip_id `的` trips.service_id `必須相同。 
 - 在 n-to-1 延續中，每個 ` from_trip_id ` 的 ` trips.service_id ` 必須相同。 
 - n 到 n 的延續必須遵守這兩個限制。 
 - 行程可以作為多個不同延續的一部分連結在一起，前提是 ` trip.service_id` 不得在任何服務日重疊。 

<pre> 
 行程 A 
 ──────────────────\ 
 \ 行程 C 
 ────────────── 
 行程 B/
 ────────────────────/
</pre> 
 
### pathways.txt 
 
 檔案：**可選** 
 
 主鍵 (`pathway_id) 
 
 檔案 [pathways.txt](#pathwaystxt) 和 [levels.txt) 。 
 
 從車站入口/出口（以`location_type=2表示的位置的節點）導航到站台（用`location_type=0表示的位置或空的節點），騎手將移動通過人行道、檢票口、樓梯和其他表示為pathways的邊緣。通用節點（以 `location_type=3表示的節點）可用來連接整個車站的pathways。 
 
 車站中的路徑必須被詳盡地定義。如果定義了任何pathways，則假定表示整個站的所有pathways。因此，適用以下準則： 
 
 - 無懸掛位置：如果車站內的任何位置都有通道，則該車站內的所有位置都應有pathways，但有登機區的站台除外（`location_type=4`，請參閱下面的指南）。 
 - 具有登機區域的平台沒有pathways：具有登機區域（`location_type = location_type=4= 0`或空）被視為父對象，而不是點。在這種情況下，平台不得分配pathways。所有pathways應分配給月台的每個登機區域。 
 - 無鎖定平台：每個平台（`location_type=0或空）或登機區（`location_type=4 ）必須透過一些pathways鏈連接到至少一個入口/出口（` location_type=2 ） 。不允許從特定月台通往車站外部的車站很少見。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | ` pathway_id|唯一ID | **必填** |標識一條路徑。系統將其用作記錄的內部識別碼。在資料集中必須是唯一的。<br><br>不同的pathways可能具有相同的“from_stop_id”和“to_stop_id”值。<hr> _範例：當兩個自動扶梯並排朝相反方向時，或當樓梯和電梯從同一地點前往同一地點時，不同的 `pathway_id可能具有相同的 `from_stop_id和 `to_stop_id值。 
 | `from_stop_id` |外部 ID 引用 `stops.stop_id| **必填** |路徑開始的位置。<br><br>必須包含標識平台的“`stop_id`” （“lo

cation_type=0`或空）、入口/出口（`location_type=2）、通用節點（`location_type=3）或登機區（`location_type=4）。<br><br>禁止使用標識車站的`stop_id`值 (`location_type=1`)。 
 | `to_stop_id` |外部 ID 引用 `stops.stop_id | **必填** |路徑結束的位置。<br><br>必須包含識別平台（` location_type=0或空）、入口/出口（`location_type=2）、通用節點（`location_type=3）或登機區域（`location_type=4 ）的`stop_id` 。<br><br>禁止使用標識車站的`stop_id`值 (`location_type=1`)。 
 | `pathway_mode|枚舉 | **必填** |指定 (`from_stop_id`, `to_stop_id`) 對之間的路徑類型。有效選項有：<br><br> `1` - 走道。<br> `2` - 樓梯。<br> `3` - 移動人行道/自動人行道。<br> `4` - 自動扶梯。<br> `5` - 電梯。<br> `6` - 票價門（或付款門）：穿過車站區域的通道，需要付款證明才能通過。檢票口可以將車站的付費區域與未付費區域分開，或將同一車站內的不同付費區域分開。這些資訊可用於避免使用捷徑引導乘客通過車站，因為捷徑會require乘客支付不必要的費用，例如引導乘客穿過地鐵月台到達公車道。<br> `7`- 出口門：從付費區域進入非付費區域的通道，無需支付證明。 
 | `is_bidirectional的` |枚舉 | **必填** |指示該路徑可以採取的方向：<br><br> `0` - 只能用於從 `from_stop_id` 到 `to_stop_id` 的單向路徑。<br> `1` - 雙向路徑，可以在兩個方向上使用。<br><br>出口門 (`pathway_mode=7) 不得是雙向的。 
 | `長度` |非負float|可選|從起始位置（在`from_stop_id`中定義）到目的地位置（在`to_stop_id`中定義）的路徑水平長度（以公尺為單位）。<br><br>建議將此欄位用於通道 (`pathway_mode=1)、檢票口 (`pathway_mode=6) 和出口門 (`pathway_mode=7)。 
 | `traversal_time` |正整數|可選|從起始位置（在`from_stop_id`中定義）到目標位置（在`to_stop_id`中定義）走過路徑所需的平均時間（以秒為單位）。<br><br>建議將此欄位用於移動人行道 (`pathway_mode=3)、自動扶梯 (`pathway_mode=4) 和電梯 (`pathway_mode=5)。 
 | `stair_count` |非空整數 |可選|通道的樓梯數量。<br><br>正的 `stair_count表示騎士從 `from_stop_id走到 `to_stop_id。負的`stair_count`表示騎士從`from_stop_id`走到`to_stop_id`。<br><br>建議樓梯使用此欄位（`pathway_mode=2）。<br><br>如果只能提供估計的樓梯數，建議1層大約15個樓梯。 
 | `max_slope` |Float|可選|路徑的最大坡度比。有效選項有：<br><br> “0”或空 - 無斜率。<br> `Float` - 路徑的坡度比，向上為正，向下為負。<br><br>此欄位只能與人行道 (`pathway_mode=1) 和移動人行道 (`pathway_mode=3) 一起使用。<hr> _例：在美國，0.083（也寫為 8.3%）是手推輪椅的最大坡度比，這意味著每 1m 增加 0.083m（即 8.3cm）。 
 | `min_width` |正float|可選|路徑的最小寬度（以公尺為單位）。<br><br>如果最小寬度小於 1 米，建議使用此欄位。 
 | `signposted_as` |Text|可選|來自騎士可見的實體標誌的面向公眾的文本。<br><br>可用於向乘客提供文字指示，例如`按照標誌前往`。 `singposted_as `中的文字應與標示牌上列印的內容完全相同。<br><br>當實體標誌是多語言時，可以依照` feed_info.feed_lang `欄位定義中的` stops.stop_name `範例填入和翻譯該欄位。 
 | ` reversed_signposted_as|Text|可選|與`signposted_as相同，但當使用從`to_stop_id到`from_stop_id的路徑時。 
 
### levels.txt 
 
 檔案：**有條件必需** 
 
 主鍵 (`level_id`) 
 
 描述工作站中的層級。與 [pathways.txt](#pathwaystxt) 結合使用很有用。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `level_id` |唯一ID | **必填** |標識車站中的等級。 
 | `level_index` |Float| **必填** |指示其相對position的等級的數字索引。<br><br>地面水平應具有索引“0”，地面以上水平以正指數表示，地面以下水平由負指數表示。 
 | `level_name` |Text|可選|建築物或車站內的乘客所看到的等級名稱。<hr> _範例：搭乘電梯到`夾層`或`月台`或`-1`。 
 
### location_groups.txt 
 
 文件：**可選** 
 
 主鍵 (`location_group_id`) 
 
 定義位置組，即乘客可能要求的stops組接送或送機。 

|字段名稱 |類型 |存在 |描述 | 
 |----------|----|------------|-----------| 
 | `位置群組 ID` |唯一ID | **必填** |標識位置組。所有 `stops.stop_id、 locations.geojson和 `location_groups.location_group_id` 值中的ID 必須是唯一的。<br><br>位置組是一組stops，它們共同指示乘客可以請求上車或下車的位置。 | 
 | `位置群組名稱` |Text|可選|顯示給騎士的位置群組名稱。 | 
 
### location_group_stops.txt 
 
 檔案：**可選** 
 
 主鍵 (`*`) 
 
 將stops.txt中的stops指派給地點群組。 

|字段名稱 |類型 |存在 |描述 | 
 |----------|----|------------|-----------| 
 | `位置群組 ID` |外部 ID 引用 `location_groups.location_group_id` | **必填** |標識一個或多個``stop_id``所屬的位置群組。可以在多個“location_group_id”中定義相同的“`stop_id`” 。 | 
 | `stop_id` |外部 ID 引用 `stops.stop_id| **必填** |標識屬於位置組的停靠點。 | 
 
 
### locations.geojson 
 
 文件：**可選** 
 
 定義乘客可以透過按需服務請求接送的區域。這些區域表示為 GeoJSON 多邊形。 
 
 - 此文件使用 GeoJSON 格式的子集，如 [RFC 7946](https:) 所述。 
 - `locations.geojson`檔案必須包含 `FeatureCollection`。 
 - “FeatureCollection”定義了乘客可以要求上車或下車的各種停靠位置。 
 - 每個 GeoJSON `Feature` 必須有一個`id`。 ``id``在所有`stops.stop_id`、 locations.geojson ``id``和`location_group_id`值中必須是唯一的。 
 - 每個 GeoJSON `Feature` 應具有物件和關聯鍵，如下表所示： 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 |- `類型` |字串| **必填** |位置的“特徵集合”。 | 
 |- `特點` |數組 | **必填** |描述位置的`特徵`物件的集合。 | 
 |     \- `類型` |字串| **必填** | `“功能”` | 
 |     \- `id` |字串| **必填** |標識一個位置。所有 `stops.stop_id、 locations.geojson和 `location_groups.location_group_id` 值中的ID 必須是唯一的。 | 
 |     \- `屬性` |對象| **必填** |位置屬性鍵。 | 
 |         \- `stop_name` |字串|可選|表示向乘客顯示的位置名稱。 | 
 |         \- `stop_desc` |字串|可選|對位置進行有意義的描述，以幫助騎士確定方向。 | 
 |     \- `幾何` |對象| **必填** |位置的幾何形狀。 | 
 |         \- `類型` |字串| **必填** |必須屬於以下類型：<br> - ``Polygon``<br> - ``多多邊形`` | 
 |         \- `坐標` |數組 | **必填** |定義位置幾何形狀的地理座標（latitude和longitude）。 | 
 
### booking_rules.txt 
 
 文件：**可選** 
 
 主鍵 (`booking_rule_id`) 
 
 定義乘客請求的服務的預訂規則 
 
 |字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `booking_rule_id` |唯一ID | **必填** |標識一條規則。 | 
 | `預訂類型` |枚舉 | **必填** |表示可以提前多久預訂。有效選項有：<br><br> “0”-即時預訂。<br> `1` - 最多可在當天預訂並提前通知。<br> `2` - 截至前一天的預訂。 | 
 | `prior_notice_duration_min` |整數 | **有條件要求** |出行前至少需要幾分鐘時間提出請求。<br><br> **有條件要求**：<br> - “booking_type=1”**必需**。<br> - **否則禁止**。 | 
 | `prior_notice_duration_max` |整數 | **有條件禁止** |出發前提出預訂請求的最多分鐘數。<br><br> **有條件禁止**：<br> - **禁止**“booking_type=0”和“booking_type=2”。<br> - `booking_type=1` 可選。 
 | `前通知最後一天` |整數 | **有條件要求** |出遊前最後一天提出預訂要求。<br><br>範例：`乘車必須在下午 5 點之前提前 1 天預訂`將編碼為 `prior_notice_last_day=1`。<br><br> **有條件要求**：<br> - “booking_type=2”的**必要**。<br> - **否則禁止**。 | 
 | `事先通知_最後時間` |時間 | **有條件要求** |最後一次在旅行前最後一天提出預訂要求。<br><br>範例：`乘車必須在下午 5 點之前提前 1 天預訂`將編碼為 `prior_notice_last_time=17:00:00`。<br><br> **有條件要求**：<br> - 如果定義了“prior_notice_last_day”，則**必要**。<br> - **否則禁止**。 | 
 | `事先通知_開始日` |整數| **有條件禁止** |最早在旅行前一天提出預訂要求。<br><br>範例：`最早可以提前一周午夜預訂乘車`將編碼為 `prior_notice_start_day=7`。<br><br> **有條件禁止**：<br> - **禁止**“booking_type=0”。<br> - 如果定義了“prior_notice_duration_max”，則“booking_type=1”**禁止**。<br> - 否則可選。 | 
 | `事先通知開始時間` |時間 | **有條件要求** |最早提出預訂請求的時間為出發前最早一天。<br><br>範例：`最早可以提前一周午夜預訂乘車`將編碼為 `prior_notice_start_time=00:00:00`。<br><br> **有條件要求**：<br> - 如果定義了“prior_notice_start_day”，則**必要**。<br> - **否則禁止**。 | 
 | `prior_notice_service_id` | ID 引用 `calendar.service_id| **有條件禁止** |指示`prior_notice_last_day`或`prior_notice_start_day`的服務天數。<br><br>範例：如果為空，則`prior_notice_start_day=2`將提前兩個日曆天。如果定義為僅包含工作日（沒有假日的工作日）的`service_id，則`prior_notice_start_day=2`將提前兩個工作天。<br><br> **有條件禁止**：<br> - 如果 `booking_type=2` 則可選。<br> - **否則禁止**。 | 
 | `message` |Text|可選|在預訂按需接送服務時向在`stop_time`使用服務的乘客發送的訊息。旨在提供在使用者介面中傳輸的關於騎手為了使用該服務而必須採取的操作的最少資訊。 | 
 | `拾取訊息` |Text|可選|功能與`message`相同，但僅在乘客僅按需接送時使用。 | 
 | `drop_off_message` |Text|可選|功能與“message”相同，但僅在乘客按需下車時使用。 | 
 | `電話號碼` |Phone number|可選|用於提出預訂請求的Phone number。 | 
 | `info_url` |URL|可選|提供有關預訂規則資訊的URL 。 | 
 | `booking_url` |URL|可選|可以發出預訂請求的線上介面或應用程式的URL 。 | 
 
### translations.txt 
 
 檔案：**可選** 
 
 主鍵（`table_name、`field_name、`language`、`record_id、`record_sub_id、`field_value`) 
 
 在有多種官方語言的地區，交通機構/業者通常具有特定於語言的名稱和網頁。為了更好地為這些地區的乘客提供服務，資料集包含這些與語言相關的值非常有用。 
 
 如果使用兩種引用方法 (`record_id`、`record_sub_id`) 和 `field_value來翻譯 2 個不同行中的相同值，則 (`record_id`、`record_sub_id`) 提供的翻譯優先。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `table_name` |枚舉 | **必填** |定義包含要翻譯的欄位的表。允許的值為：<br><br> -`agency`<br> -`stops`<br> -`routes`<br> - `旅行`<br> - `stop_times`<br> -`pathways`<br> - `級別`<br> - `feed_info`<br> -`attributions`<br><br>新增至GTFS的任何檔案都會具有與檔案名稱等效的`table_name`值，如上面所列（即，不包括`.txt`檔案副檔名）。 | 
 | `field_name` |Text| **必填** |要翻譯的欄位的名稱。類型為`Text`的欄位可以翻譯，類型為`URL`、`Email`和`Phone number`的欄位也可以`翻譯`以提供正確語言的資源。其他類型的欄位不應被翻譯。 | 
 | `語言` |語言代碼 | **必填** |翻譯語言。<br><br>如果語言與`feed_info.feed_lang`中的語言相同，則該欄位的原始值將被假定為在沒有特定翻譯的語言中使用的預設值（如果`default_lang`t另外指定）。<hr> _例：在瑞士，官方雙語州的城市的正式名稱為“Biel/Bienne”，但在法語中簡稱為“Bienne”，在德語中簡稱為“Biel”。 
 | `翻譯` |Text或URL或Email或Phone number| **必填** |翻譯後的值。 | 
 | `record_id` |外國身分證 | **有條件要求** |定義與要翻譯的欄位對應的記錄。 `record_id`中的值必須是表主鍵的第一個或唯一字段，如每個表的主鍵屬性中所定義，如下所示：<br><br> - `agency_id為 [agency.txt](#agencytxt)<br> - [stops.txt](#stopstxt) 的`stop_id` ；<br> - [routes.txt](#routestxt) 的`route_id` ；<br> - [trips.txt](#tripstxt) 的`trip_id` ；<br> - [stop_times.txt](#stop_timestxt) 的`trip_id` ；<br> - [pathways.txt](#pathwaystxt) 的` pathway_id ；<br> - [levels.txt](#levelstxt) 的 ` level_id ；<br> - [attributions.txt](#attributionstxt) 的 ` attribution_id 。<br><br>上面未定義的表格中的欄位不應被翻譯。然而，生產者有時會添加官方規範之外的額外字段，而這些非官方字段可能會被翻譯。以下是對這些表使用 ` record_id的建議方法：<br><br> - `service_id for [calendar.txt](#calendartxt);<br> - `service_id for [calendar_dates.txt](#calendar_datestxt);<br> - `fare_id` for [fare_attributes.txt](#fare_attributestxt);<br> - `fare_id` for [fare_rules.txt](#fare_rulestxt);<br> - [shapes.txt](#shapestxt) 的`shape_id` ；<br> - [frequencies.txt](#frequenciestxt) 的`trip_id` ；<br> - [transfers.txt](#transferstxt) 的 ` from_stop_id 。<br><br>有條件要求：<br> - 如果 ` table_name是 `feed_info，則**禁止**。<br> - 如果定義了“field_value”，則**禁止**。<br> - 如果`field_value為空，則**必需**。 | 
 | `record_sub_id` |外國身分證 | **有條件要求** |當表格t唯一 ID 時，幫助包含要翻譯的欄位的記錄。因此，`record_sub_id中的值是表格的輔助ID，如下表所定義：<br><br> - [agency.txt](#agencytxt) 無；<br> - [stops.txt](#stopstxt) 無；<br> - [routes.txt](#routestxt) 無；<br> - [trips.txt](#tripstxt) 無；<br> - [stop_times.txt](#stop_timestxt) 的`stop_sequence` ；<br> - [pathways.txt](#pathwaystxt) 無；<br> - [levels.txt](#levelstxt) 無；<br> - [attributions.txt](#attributionstxt) 無。<br><br>上面未定義的表格中的欄位不應被翻譯。然而，生產者有時會添加官方規範之外的額外字段，而這些非官方字段可能會被翻譯。以下是對這些表使用 `record_sub_id的建議方法：<br><br> - [calendar.txt](#calendartxt) 無；<br> - `date為 [calendar_dates.txt](#calendar_datestxt);<br> - [fare_attributes.txt](#fare_attributestxt) 無；<br> - [fare_rules.txt](#fare_rulestxt) 的`route_id` ；<br> - [shapes.txt](#shapestxt) 無；<br> - [frequencies.txt](#frequenciestxt) 的`start_time` ；<br> - [transfers.txt](#transferstxt) 的` to_stop_id 。<br><br>有條件要求：<br> - 如果 ` table_name是 `feed_info，則**禁止**。<br> - 如果定義了“field_value”，則**禁止**。<br> - 如果定義了“table_name=stop_times”和“record_id”，則**必要**。 | 
 | `field_value` |Text或URL或Email或Phone number| **有條件要求** |此欄位可用於定義應翻譯的值，而不是使用`record_id`和`record_sub_id`來定義應翻譯的記錄。使用時，當`table_name`和`field_name`所識別的欄位包含與field_value中定義的完全相同的值時，將會套用翻譯。<br><br>該欄位必須**精確**在`field_value中定義的值。如果只有值的子集與`field_value`匹配，則t套用翻譯。<br><br>如果兩個翻譯規則符合相同的記錄（一個帶有“field_value”，另一個帶有“record_id”），則帶有“record_id”的規則優先。<br><br>有條件要求：<br> - 如果 `table_name是 `feed_info，則**禁止**。<br> - 如果定義了 `record_id，則**禁止**。<br> - **必需** 如果 `record_id` 為空。 | 
 
### feed_info.txt 
 
 檔案：**推薦**（如果提供了 [translations.txt](#translationstxt)，則**必要**） 
 
Primary key (none) § § 
 該文件包含有關資料集本身的信息，而不是資料集描述的服務的資訊。在某些情況下，資料集的發布者是與任何機構不同的entity。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `feed_publisher_name` |Text| **必填** |發布資料集的組織的全名。這可能與`agency.agency_name`值之一相同。 | 
 | `feed_publisher_url` |URL| **必填** |資料集發布組織網站的URL 。這可能與`agency.agency_url`值之一相同。 | 
 | `feed_lang` |語言代碼 | **必填** |此資料集中文字使用的預設語言。此設定可協助GTFS使用者為資料集選擇大寫規則和其他特定於語言的設定。如果文字需要翻譯成預設語言以外的語言，則可以使用檔案`translations.txt`。<br><br>對於原始文字為多種語言的資料集，預設語言可以是多語言的。在這種情況下，“feed_lang”欄位應包含由 ISO 639-2 規範定義的語言代碼“mul”，並且應在“translations.txt”中提供資料集中使用的每種語言的翻譯。如果資料集中的所有原始文字都是同一種語言，則不應使用`mul。<hr> _範例：考慮來自瑞士等多語言國家的資料集，原始`stops.stop_name`欄位填入了不同語言的停靠點名稱。每個站點名稱均根據該站點地理位置的主要語言編寫，例如“Genève”代表法語城市Geneva，“Zürich”代表德語城市Zurich，“Biel/Bienne”代表雙語城市Biel/Bienne市。資料集 `feed_lang應該是 `mul`，翻譯將在 `translations.txt中提供，德語：`Genf、`Zürich和 `Biel；法語：`Genève、`Zurich和`Bienne；義大利語：`Ginevra`、`Zurigo`和`Bienna`；以及英文：`Geneva、`Zurich和`Biel/Bienne。 
 | `default_lang|語言代碼 |可選|定義當資料使用者t知道騎士的語言時應使用的語言。通常是“en”（英語）。 | 
 | `feed_start_date` |日期 |推薦|此資料集提供了從`feed_start_date`日開始到`feed_end_date`日結束期間的完整、可靠的服務時間表資訊。如果沒有空的話，這兩天可能會空著。如果同時給出了`feed_end_date`日期，則`feed_end_date`date不得早於`feed_start_date`date。建議資料集提供者在此期間之外提供時間表數據，以建議未來可能的服務，但資料集使用者應注意其非權威狀態。如果 `feed_start_date或 `feed_end_date超出了 [calendar.txt](#calendartxt) 和 [calendar_dates.txt](#calendar_datestxt) 中定義的活動日曆日期，則資料集明確斷言沒有日期服務在`feed_start_date`或`feed_end_date`範圍內，但不包含在活動日曆日期中。 | 
 | `feed_end_date` |日期 |推薦| （見上文）| 
 | `feed_version` |Text|推薦|指示GTFS資料集目前版本的字串。使用GTFS的應用程式可以顯示此值，以協助資料集發布者確定是否已合併最新資料集。 | 
 | `feed_contact_email` |Email|可選|用於就GTFS資料集和資料發布實務進行交流的Email地址。 ` feed_contact_email` 是GTFS消費應用程式的技術聯絡人。透過[agency.txt](#agencytxt)提供客戶服務聯絡資訊。建議至少提供 `feed_contact_email` 或 `feed_contact_url` 之一。 | 
 | `feed_contact_url` |URL|可選|聯絡資訊、網頁表單、支援台或其他有關GTFS資料集和資料發布實務的溝通工具的URL 。 ` feed_contact_url` 是GTFS消費應用程式的技術聯絡人。透過[agency.txt](#agencytxt)提供客戶服務聯絡資訊。建議至少提供 `feed_contact_url` 或 `feed_contact_email` 之一。 | 
 
### attributions.txt 
 
 文件：**可選** 
 
 主鍵 (`attribution_id`) 
 
 此文件定義應用於資料集的attributions。 

|字段名稱 |類型 |存在 |描述 | 
 |------|------|------|------| 
 | `attribution_id` |唯一ID |可選|標識資料集或其子集的屬性。這對於翻譯來說最有用。 | 
 | `agency_id` |外部 ID 引用 `agency.agency_id|可選|歸屬所適用的機構。<br><br>如果定義了`agency_id`、 ``route_id``或``trip_id``屬性之一，則其他屬性必須為空。如果未指定任何一個，則歸因將應用於整個資料集。 | 
 | `route_id` |外部 ID 引用 `routes.route_id|可選|功能與`agency_id相同，只是屬性適用於路線。多個attributions可能適用於同一條路線上。 | 
 | `trip_id` |引用`trips.trip_id` 的外部 ID |可選|功能與`agency_id`相同，只不過屬性適用於旅行。多個attributions可能適用於同一次旅行。 | 
 | `organization_name` |Text| **必填** |資料集所屬組織的名稱。 | 
 | `is_producer` |枚舉 |可選|組織的角色是生產者。有效選項有：<br><br> `0`或空 - 組織t此角色。<br> `1` - 組織確實有這個角色。<br><br>至少應將`is_producer`、`is_operator`或`is_authority`欄位之一設為` `1` `。 | 
 | `is_operator` |枚舉 |可選|功能與 `is_producer` 相同，只是組織的角色是操作員。 | 
 | `is_authority` |枚舉 |可選|除了組織的角色是權威之外，其功能與`is_producer`相同。 | 
 | `attribution_url` |URL|可選|組織的URL 。 |

 
 | `attribution_email` |Email|可選|組織的Email。 | 
 | `attribution_phone` |Phone number|可選|組織的Phone number。 | 
 

