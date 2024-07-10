# GTFS Schedule功能 
 
 隨著GTFS參考格式不斷發展以滿足交通系統當前的需求，其功能可能變得越來越複雜。 ** GTFS功能** 旨在為GTFS參考格式啟用的功能提供清晰且明確的解釋。這有助於交通機構、供應商、消費者和研究人員了解GTFS的功能並回答以下問題： **我可以使用GTFS做什麼？功能文件和與其關聯的字段，幫助使用者了解支援特定功能所需的資料。 
 
## 基礎 
 這些基本功能構成了GTFS feed 的核心。它們是代表公車服務所需的最小元素。 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 傳達有關負責公車服務的機構的詳細資訊。 
 
 [:octicons-arrow-right-24：了解更多](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Stops__ 
 
定義過境服務接送乘客的地點。 
 
 [:octicons-arrow-right-24: 了解更多](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Routes__ 
 
定義公車路線的元素，例如名稱和服務類型。 
 
 [:octicons-arrow-right-24：了解更多](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __服務日期_ _ 
 
創造安排旅行和服務豁免的結構。 
 
 [:octicons-arrow-right-24：了解更多](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trips__ 
 § § 表示在預定時間沿著規定路線行駛的交通車輛。 
 
 [:octicons-arrow-right-24：了解更多](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __停止時間_ _ 
 
定義每個行程每個站點的arrival和departure時間。 
 
 [:octicons-arrow-right-24：了解更多](../base/#stop-times) 
 
</div> 
 
## 基礎附加元件 
 這些功能增強了GTFS資料集，改善騎士體驗並促進機構、供應商和資料重用者之間的協作。它們可能涉及向現有文件添加新欄位或建立新文件。 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Feed Information__ 
 
 傳達有關 Feed 本身的重要訊息。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ § § 
 定義vehicle沿著行程行駛的地理路徑。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __路線顏色__ 
 
 準確地描繪和傳達分配給特定routes的配色方案。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } _ _允許騎自行車__ 
 
 溝通車輛是否能夠容納自行車。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 傳達車輛所使用的指示行程目的地的標誌。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __位置類型__ 
 
 對公車站內的入口和出口等關鍵區域進行分類。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frequencies__ § § 
 表示以固定頻率或特定發車間隔運行的服務。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#Frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __轉乘__ 
 
 描述不同交通服務之間所允許的transfers。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Translations__ 
 § § 以多種語言傳達服務訊息。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Attributions__ 
 § § 溝通誰參與了資料集的創建。 
 
 [:octicons-arrow-right-24：了解更多](../base_add-ons/#attributions) 
 
</div> 
 
 
## 輔助功能 
 輔助功能為身心障礙者提供存取服務的基本資訊。 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __停止輪椅通道__ 
 
 指示是否可以從某個位置搭乘輪椅。 
 
 [:octicons-arrow-right-24：了解更多](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Trips輪椅無障礙__ 
 
 表示vehicle是否可以容納使用輪椅的乘客。 
 
 [:octicons-arrow-right-24：了解更多](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Text- to-Speech__ 
 
 提供必要的輸入，將車站名稱的文字轉換為音訊。 
 
 [:octicons-arrow-right-24：了解更多](../accessibility/#text-to-speech) 
 
</div> 
 
 
## 票價 
 GTFS可以對各種票價結構進行建模，例如區域、距離或基於時間的票價。它告知乘客行程價格和付款方式。 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __票價產品__ 
 
 定義使用者可用的車票或票價類型清單。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ § § 
 定義可用於保存和/或驗證票價產品的媒體。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __基於路線的票價__ 
 
 描述對特定routes組套用不同票價的規則。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Time-基於票價__ 
 
 描述以一天中的時間或一週中的某天區分的票價。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone-基於票價__ 
 
 描述從一個地區旅行到另一個地區時的差異票價。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } _ _票價轉乘__ 
 
 定義從旅程的一個航段轉移到另一航段時適用的費用。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ § § 
 允許更簡單地表示票價資訊的傳統功能。 
 
 [:octicons-arrow-right-24：了解更多](../fares/#fares-v1) 
 
</div> 
 
 
## 路徑 
 
 路徑功能允許對大型公車站進行建模，以便引導乘客從入口到登機區。它們提供路徑詳細資訊、預計導航時間和尋路系統。 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Pathway Connections__ 
 
 連接公車站內相關點的模型路徑。 
 
 [:octicons-arrow-right-24：了解更多](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __Pathway Details__ §Pathway § 
 提供更多有關路徑物理特性的詳細資訊。 
 
 [:octicons-arrow-right-24：了解更多](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Levels__ 
 § § 描述並列出公車站內的所有不同樓層。 
 
 [:octicons-arrow-right-24：了解更多](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __站內穿越時間__ § § 
 傳達在公車站內導航路徑的預計時間。 
 
 [:octicons-arrow-right-24：了解更多](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __通道標誌__ 
 
 傳達與通道相關的站內標示。 
 
 [:octicons-arrow-right-24：了解更多](../pathways/#pathway-signs) 
 
</div> 
 
## 彈性服務 
 不遵循常規時間表或固定routes的彈性服務或需求回應服務。 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __連續停靠點__ 
 
 指示使用者是否可以在stops之間上車和/或下車。 
 
 [:octicons-arrow-right-24：了解更多](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __預訂規則__ 
 
 告知使用者是否可以透過需求回應服務預訂行程。 
 
 [:octicons-arrow-right-24：了解更多](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __有偏差的預定義路線__ 
 
 可能短暫偏離上車或下車路線的車輛。 
 
 [:octicons-arrow-right-24：了解更多](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __基於區域的需求回應服務__ 
 
 允許在特定區域內的任何位置接送的服務。 
 
 [:octicons-arrow-right-24：了解更多](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.middle } __固定站點需求響應服務__ 
 
 允許在一組stops內的任何位置上車/下車的服務。 
 
 [:octicons-arrow-right-24：了解更多](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

