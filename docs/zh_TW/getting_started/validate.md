# 評估您的GTFS Feed 的品質 
 
 高品質的GTFS是完整、準確且最新的。這意味著它代表服務當前的運作方式並提供盡可能多的信息。 
 
## 完整數據 
 
 優質GTFS包括重要的服務詳細信息，例如假期和夏季時間表變更、準確的停靠位置以及與其他面向騎手的材料相匹配的routes和車頭標誌的名稱。即使agency與供應商合作生產GTFS，最終還是要由agency來確保印刷、船上和線上提供的資訊一致。 
 
## 準確的數據 
 
 準確的數據對於為公車乘客提供可靠且用戶友好的交通體驗至關重要。資料中的錯誤可能會阻止部分或整個資料集的使用。 
 
## 最新資料 
 
 過時的資料可能比沒有可用的 Feed 更成問題。僅僅發布資訊是不夠的，它必須與騎手的所見所聞相匹配。一些最大的交通機構每週甚至每天更新其GTFS ，但大多數機構需要每隔幾個月更新一次GTFS ，或在服務發生變化時每年更新幾次。這包括新routes或stops、時刻表變更或票價結構更新等。 
 
 許多機構聘請供應商來為他們創建和管理GTFS 。一些供應商可能會主動詢問服務變更，但機構與供應商就即將到來的服務變更進行溝通非常重要。可以提前發布帶有服務變更的GTFS ，確保每個人（代理商、供應商、旅行規劃者和乘客）都能順利過渡！ 
 
## 使用官方驗證器 
 
 官方GTFS驗證器根據官方規範評估資料集的質量，確保行業內對高質量資料集的構成達成共識。 
 
 由 [MobilityData](https: ) 維護的免費開源 [Canonical GTFS Schedule驗證器](https: )[^1] 確保您的GTFS資料符合官方 [GTFS Schedule參考](../../documentation/schedule/reference/) 和 [最佳實踐](../../documentation/schedule/schedule_best_practices)。它提供了易於使用的報告和全面的文檔，可以與其他方共用。 

<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li>轉至<a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a> 。</li> 
<li>載入GTFS資料集：您可以選擇或拖放 ZIP 文件，或複製/貼上URL。</li> 
<li>驗證完成後，將提供開啟報告的選項。</li> 
<li>您將看到驗證器是否發現資料問題，以及我們的文件連結以了解如何修復這些問題。驗證報告的URL有效期為 30 天，並且可以與其他人共用。</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 同樣，使用免費開源規範 [GTFS Realtime Validator](https:) 確保您的GTFS數據符合官方 [GTFS Realtime Reference](../../documentation/realtime/reference/) 和[最佳實踐](../../documentation/realtime/realtime_best_practices)。 
 
 有關創建高品質資料的信息，請參閱[加州交通資料指南](https:)、[GTFS Schedule最佳實踐](../../documentation/schedule/schedule_best_practices) 和 [GTFS Realtime最佳實踐](../../documentation/realtime/realtime_best_practices)。 
 
 [^1]：若要查看有關如何在資料管道中使用此工具並為本專案做出貢獻的更多說明，請造訪 [GitHub 儲存庫](https:）。 
 

