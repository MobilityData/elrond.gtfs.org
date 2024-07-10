# GTFS: 公共交通機関のデータを誰でもアクセス可能にする 
 
## 交通機関の乗客情報のためのオープンデータ標準 
 
 General Transit Feed Specification( GTFS) は、公共交通機関がスケジュール、stops、運賃などのサービスの詳細を記述するための構造を提供する標準化されたデータ形式です。 
 
 これにより、公共交通機関は、さまざまなソフトウェア アプリケーション (最も一般的なのは旅行プランナー) で使用できる形式で交通データを公開できます。つまり、ユーザーはスマートフォンなどのデバイスを使用して、公共交通機関のサービスにアクセスするための旅行情報を簡単に入手できます。 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 現在、 GTFS は世界中の何千もの公共交通機関にとって頼りになる [オープン スタンダード](https://www.interoperablemobility.org/definitions/#open_standard) です。一部の機関は独自にこのデータを作成しますが、他の機関はベンダーにデータの作成と管理を委託しています。
 
## 静的データと動的データのサポート 
 
 GTFSは、[GTFS Schedule](../../documentation/schedule/reference) と [GTFS Realtime](../../documentation/realtime/reference) という 2 つの主要部分で構成されています。
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 GTFS Schedule には、routes、スケジュール、運賃、地理的な交通機関の詳細など、さまざまな機能に関する情報が含まれており、シンプルなテキスト ファイル [^1] で提供されます。このわかりやすい形式により、複雑なソフトウェアや独自のソフトウェアに頼ることなく、簡単に作成および保守できます。 
 
 GTFS Realtimeには、[プロトコル バッファ](https://developers.google.com/protocol-buffers/) 形式を使用した、旅行の更新、vehicleの位置、サービス アラートが含まれています。GTFS のこの部分は、 GTFS Scheduleと連携して、乗客にサービスの中断やarrival時刻の更新を通知します。 
 
 GTFS ScheduleとGTFS Realtime のリファレンス ドキュメントは、[技術ドキュメント セクション](../../documentation/overview) で入手できます。 
 
 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="YouTubeビデオプレーヤー" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
 <a href="https://www.flaticon.com/authors/freepik" title="アイコンはFreepikによるものです">Freepik によって作成されたアイコン - Flaticon</a> 
 
 [^1]: テキスト ファイルに加えて、[GeoJSON](https://geojson.org/) 形式もGTFSでサポートされ、デマンド レスポンシブ サービスの特定の要素を表すことができるようになりました。
 

