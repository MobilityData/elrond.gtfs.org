# GTFS：讓公共交通資料普遍可存取 
 
## 過境乘客資訊的開放資料標準 
 
General Transit Feed Specification，也稱為GTFS，是一種標準化資料格式，為公共交通提供結構機構描述其服務的詳細信息，如時刻表、stops、票價等。這意味著用戶可以使用智慧型手機或類似設備輕鬆獲取旅行資訊以存取公共交通服務。 

<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 如今， GTFS已成為全球數千家公共交通提供者的首選[開放標準](https:)。有些機構自己產生這些數據，而有些機構則僱用供應商為其創建和維護數據。 
 
## 支援靜態和動態資料 
 
 GTFS由兩個主要部分組成：[GTFS Schedule](../../documentation/schedule/reference) 和 [GTFS Realtime](../../文件/即時/參考）。 

<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 GTFS Schedule包含有關routes、時刻表、票價和地理交通詳細信息以及許多其他功能的信息，並以簡單的文本文件形式呈現[^1]。這種簡單的格式可以輕鬆創建和維護，而無需依賴複雜或專有的軟體。 
 
 GTFS Realtime包含行程更新、vehicle位置和服務警報，使用 [Protocol Buffers](https:) 格式。 GTFS的這一部分與GTFS Schedule結合使用，以便通知乘客服務中斷和更新的arrival時間。 
 
 GTFS Schedule和GTFS Realtime參考文件可在 [技術文件部分](../../documentation/overview) 中找到。 

 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="YouTube 影片播放器" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
<a href="https://www.flaticon.com/authors/freepik" title="Freepik 的圖標">由 Freepik- Flaticon 創建的圖標</a>
 
 [^1]：除了文本文件之外， GTFS現在還支持 [GeoJSON](https: ) 格式來表示某些元素需求響應服務。 
 

