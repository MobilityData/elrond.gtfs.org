# GTFS Schedule機能 
 
 GTFSリファレンス形式は、交通システムの現在のニーズを満たすために進化していますが、その機能はますます複雑になる可能性があります。**GTFS機能** は、 GTFSリファレンス形式によって可能になる機能について明確かつ決定的な説明を提供することを目的としています。これにより、交通機関、ベンダー、消費者、研究者はGTFSの機能を理解し、` GTFSで何ができるのか`という質問に答えることができます。** 
 
 次の機能のグループでは、各機能の目的と、それに関連付けられているファイルとフィールドについて説明し、特定の機能をサポートするためにどのデータが必要かをユーザーが理解できるようにします。
 
## 基本 
 これらの重要な機能は、 GTFSフィードの中核を形成します。これらは、交通サービスを表すために必要な最小限の要素です。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __機関__ 
 
 交通サービスを担当する機関に関する詳細を伝えます。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __停留所__ 
 
 交通サービスが乗客を乗降させる場所を定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __路線__ 
 
 名前やサービスの種類など、交通ルートの要素を定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __運行日__ 
 
 旅行とサービスの免除をスケジュールするための構造を作成します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __旅行__ 
 
 定義されたルートに沿ってスケジュールされた時間に移動する交通機関の車両を表します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __停車時刻__ 
 
 各停車駅の各旅行のarrival時刻とdeparture時刻を定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base/#stop-times) 
 
</div> 
 
## 基本アドオン 
 これらの機能はGTFSデータセットを強化し、乗客のエクスペリエンスを向上させ、機関、ベンダー、およびデータ再利用者間のコラボレーションを促進します。既存のファイルに新しいフィールドを追加したり、新しいファイルを作成したりする場合があります。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __フィード情報__ 
 
 フィード自体に関する重要な情報を伝えます。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __形状__ 
 
 旅行中にvehicleがたどる地理的経路を定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __ルートの色__ 
 
 特定のroutesに割り当てられた配色を正確に描写し、伝えます。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __自転車の許可__ 
 
 車両が自転車に対応しているかどうかを伝えます。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __ヘッドサイン__ 
 
 旅行の目的地を示すために車両が使用する標識を伝えます。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __場所の種類__ 
 
 入口や出口など、交通機関の駅内の主要なエリアを分類します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __頻度__ 
 
 定期的な頻度または特定の間隔で運行するサービスを表します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __乗り換え__ 
 
 異なる交通サービス間で許可されるtransfersについて説明します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __翻訳__ 
 
 複数の言語でサービス情報を伝達します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __帰属__ 
 
 データセットの作成に関わった人物を伝えます。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../base_add-ons/# attributions) 
 
</div> 
 
 
## アクセシビリティ 
 アクセシビリティ機能は、障害のある人がサービスにアクセスするために必要な情報を提供します。 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __停留所 車椅子でのアクセス__ 
 
 場所から車椅子での乗車が可能かどうかを示します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __乗車 車椅子でのアクセス__ 
 
vehicleが車椅子を使用する乗客に対応できるかどうかを示します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __テキスト読み上げ__ 
 
 停留所名のテキストを音声に変換するために必要な入力を提供します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../accessibility/#text-to-speech) 
 
</div> 
 
 
## 運賃 
 GTFS は、ゾーン、距離、時間帯に基づく運賃など、さまざまな運賃体系をモデル化できます。乗客に旅行価格と支払い方法を通知します。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __運賃商品__ 
 
 ユーザーが利用できるチケットまたは運賃の種類のリストを定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __運賃メディア__ 
 
 運賃商品を保持および/または検証するために使用できるメディアを定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __路線ベースの運賃__ 
 
 特定のroutesグループに異なる運賃を適用するために使用するルールについて説明します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __時間ベース運賃__ 
 
 時間帯や曜日によって異なる運賃について説明します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __ゾーンベース運賃__ 
 
 あるエリアから別のエリアへ移動するときに異なる運賃について説明します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __運賃乗換__ 
 
 旅行の 1 つの区間から別の区間に乗り換えるときに適用される料金を定義します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __運賃 V1__ 
 
 運賃情報をよりシンプルに表現できるレガシー機能。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../fares/#fares-v1) 
 
</div> 
 
 
## 経路 
 
 経路機能を使用すると、大規模な交通機関の駅をモデル化して、乗客を入口から乗車エリアまで誘導できます。経路の詳細、推定ナビゲーション時間、および道案内システムが提供されます。 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __経路接続__ 
 
 交通機関の駅内の関連ポイントを接続する経路をモデル化します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __経路の詳細__ 
 
 経路の物理的特性に関する追加の詳細を提供します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __レベル__ 
 
 交通機関の駅内のすべての異なるレベルについて説明し、リストします。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __駅構内通過時間__ 
 
 駅構内の経路を移動するのに要する推定時間を伝達します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __経路標識__ 
 
 経路に関連付けられた駅構内標識を伝達します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../pathways/#pathway-signs) 
 
</div> 
 
## 柔軟なサービス 
 定期的なスケジュールや固定routesに従わない柔軟なサービス、または需要に応じたサービス。 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __連続停車地__ 
 
stops間でユーザーを乗せたり降ろしたりできるかどうかを示します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __予約ルール__ 
 
 ユーザーがデマンドレスポンシブサービスで旅行を予約できるかどうかを示します。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __逸脱を含む定義済みルート__ 
 
 乗車または降車のために一時的にルートから逸脱できる車両。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __ゾーンベースの需要対応型サービス__ 
 
 特定のエリア内の任意の場所で乗車/降車を可能にするサービス。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.middle } __固定停車駅需要応答型サービス__ 
 
stopsのグループ内の任意の場所で乗降できるサービス。 
 
 [:octicons-arrow-right-24: 詳細はこちら](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

