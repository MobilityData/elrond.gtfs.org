# 建立GTFS資料集 
 
## GTFS feed 概述 
 所有GTFS feed 都以GTFS參考格式的資料集開始，這是一系列以.txt檔案副檔名儲存的 CSV 檔案[^1]。在最基本的實作中， GTFS資料集通常以七個基本文件開始，組合成一個 .zip 文件，該文件託管在穩定的公共URL上：這就是GTFS來源。 

<img class="center" width="560" height="100%" src="../../../assets/create_001.png"> 
 
 每個文件由具有多個資訊欄位的多個記錄（資料行）的清單組成。例如，[routes.txt](../../documentation/schedule/reference/#routestxt)中列出的每一行代表一條公共交通路線，其欄位描述該路線的多個元素，例如名稱、描述、營運agency等 
 
<img class="center" width="560" height="100%" src="../../../assets/create_002.png"> 
 
 GTFS資料集的基本檔案可以描述如下： GTFS時間表資料集具有一條或多條routes([routes.txt](../../documentation/schedule/reference/#routestxt))，每條路線都有一個或多個行程([trips.txt](../../documentation/schedule/reference/#tripstxt))，每個行程都會經過一系列stops([stops.txt](../../documentation/schedule/reference/#stopstxt)) 在指定時間 ([stop_times.txt](../../documentation/schedule/reference/#stop_timestxt))。行程和停靠時間僅包含一天中的時間資訊；日曆用於確定給定行程的運行日期（[calendar.txt](../../documentation/schedule/reference/#calendartxt) 和 [calendar_dates.txt](../../documentation/時間表/參考/#calendar_datestxt))。此外，多個代理商 ([agency.txt](../../documentation/schedule/reference/#agencytxt)) 可以運作多條routes。這些文件透過它們之間交叉引用的欄位相互連結。 

<img class="center" width="560" height="100%" src="../../../assets/create_003.png"> 
 
 一旦設定了這些文件來建立基本GTFS資料集，就可以新增其他（optional）文件以實現其他功能或交通機構和供應商之間的特定需求。這些文件的一些範例包括： 
 
 - [shapes.txt](../../documentation/schedule/reference/#shapestxt) 允許以圖形方式表示行程路徑， 
 - [pathways.txt](../../documentation/schedule/reference/#pathwaystxt) 提供的資訊可以產生方向來幫助使用者導航電台，
 - [frequencies.txt](../../documentation/schedule/reference/#frequenciestxt )，它提供了另一種指定停止時間的方法。 
 
 有關可以啟用的所有GTFS功能的更多信息，請參閱[“ GTFS可以做什麼？”](../features/overview/) 部分。 
 
 GTFS Schedule資料集可以補充即時信息，例如vehicle位置和服務更新。為此，需要與現有GTFS Schedule資料集分開建立GTFS Realtime。 
 
 GTFS Realtime來源由透過 HTTP 提供服務並經常更新的常規二進位檔案組成，任何類型的網頁伺服器都可以託管和提供該文件。 GTFS Realtime資料交換格式是基於 [協定緩衝區](https:)，這是一種用於序列化結構化資料的語言和平台中立機制。 GTFS Realtime可以提供三種類型的資訊：行程更新、服務警報和車輛位置，這些資訊可以根據需要傳達的服務資訊進行組合。 
 
 由於GTFS Realtime允許呈現車隊的實際狀態，因此需要定期更新來源 - 最好是在服務的自動車輛定位系統收到新資料時更新。 GTFS Schedule資料集和GTFS Realtime來源結合，使消費應用程式能夠為乘客提供準確和最新的資訊。如需了解更多信息，請參閱技術文件。 
 
## 製作您的第一個GTFS feed？ 
 
 如果您是一家希望製作第一個GTFS feed 的agency，您需要做的第一件事就是閱讀現有文件。 
 
 首先在 [“ GTFS能做什麼？”](../features/overview) 部分探索GTFS的功能，並確定您想要使用GTFS格式表示的交通服務的不同功能。如需更深入的探索，[GTFS Schedule](../../documentation/schedule/reference) 和 [GTFS Realtime](../../documentation/realtime/reference) 的官方參考文檔提供了詳細信息有關對這些功能進行建模並確保合規性的指導。 
 
 接下來，從您的系統收集所有必需的資料。這包括所有stops、routes、時間表、票價等的信息，因為其中許多詳細資訊將作為填充GTFS資料集的輸入。 
 
 根據系統的規模和複雜性，您可以選擇內部建立資料或聘請外部GTFS供應商將資料轉換為GTFS格式。 
 
 在某些情況下，擁有少量routes的小型機構會使用電子表格和文字編輯器等常用軟體自行建立資料。 
 
 在處理更大的系統範圍時，大多數機構從專業供應商購買專門的GTFS管理軟體，但有些機構可能會選擇開發自己的內部工具。最後，當系統特性對機構自行編寫資料集構成挑戰時， GTFS生產可以完全外包給專門生產GTFS資料的公司。 
 
<a href="https://www.flaticon.com/authors/freepik" title="Freepik 的圖標">由 Freepik- Flaticon 創建的圖標</a>
 
 [^1]：除了文本文件之外， GTFS現在還支持 [GeoJSON](https: ) 格式來表示某些元素需求響應服務。 
 

