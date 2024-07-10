# Base アドオン 
 これらの機能は、Base で説明されている機能を拡張し、 GTFSデータセットの包括性を高めて乗客の体験を向上させるか、機関、データベンダー、データ再利用者間のコラボレーションを促進します。これらの機能強化には、Base で説明されているファイル内に新しいフィールドを導入するか、新しいファイルを作成することが必要になる場合があります。
 
## フィード情報 
 
 フィード情報は、フィードに関する重要な情報を伝えます。たとえば、有効期間 (開始日と終了date)、公開組織、 GTFSデータセットとデータ公開方法に関する問い合わせの連絡先情報などです。
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`、`feed_publisher_url`、`feed_lang`、`default_lang`、`feed_start_date`、`feed_end_date`、`feed_version`、`feed_contact_email`、`feed_contact_url` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 
 
 | feed_publisher_name | feed_publisher_url | feed_lang | default_lang | feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |-------------------------|----------------------|-------------------------|--------------|-----------------|--------------|--------------------|------------------------------| 
 | Greater Region Transport | https://www.gra1.org | en | en | 20240101 | 20241231 | 3.1 | support@gra1.org | https://www.gra1.org/support | 
 
## シェイプ 
 シェイプを定義して旅行に関連付けることができるため、旅行計画アプリケーションで地図上に旅行を表示し、乗客に公共vehicleで移動する必要がある距離を通知できます。 `shape_dist_traveled` フィールドは、乗客に地図を表示するときにどの程度のshapeを描画するかをプログラムで決定するために使用されます。
 シェイプを定義するときは、その詳細レベル (道路の正確な曲率に沿うなど) と、必要な情報のみを効率的に伝えることのバランスを取ります。
 
 |含まれるファイル |含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`、`shape_pt_lat`、`shape_pt_lon`、`shape_pt_sequence`、`shape_dist_traveled` | 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled `| 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、TriMet GTFSフィード (<a     href="https://developer.trimet.org/GTFS.shtml">ここから</a>ダウンロード) のshapeの一部を示しています。<br><br> 
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 
 
 | shape_id | shape_pt_lat | shape_pt_lon | shape_pt_sequence | shape_dist_traveled | 
 |---------|-------------|-------------|------------------|-------------------| 
 | 558674 | 45.47623 |-122.721885 | 1 | 0.0 | 
 | 558674 | 45.476235 |-122.72236 | 2 | 121.9 | 
 | 558674 | 45.476237 |-122.722523 | 3 | 163.7 | 
 | 558674 | 45.476242 |-122.723024 | 4 | 292.2 | 
 | 558674 | 45.476244 |-122.72316 | 5 | 327.1 | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 
 
 | trip_id | shape_id| 
 |--------|--------| 
 |13302375|558674 | 
 
 !!! 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 
 
 | trip_id | stop_sequence| shape_dist_traveled| 
 |-------|------------|-------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## ルートの色 
 
 ルートの色を使用すると、機関の設計ガイドラインによって特定のroutesに割り当てられた配色を正確に表現および伝えることができます。これにより、ユーザーは公式の色で交通サービスを簡単に識別できます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`、`route_text_color` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、ルート `RA` が HEX カラー コード `D95700` を使用してオレンジ色で表示され、テキストが HEX カラー コード `0` を使用して黒色で表示されることを示しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |---------|----------|------------------|------------------|------------|------------|------------------| 
 | RA | agency001 | 17 | Mission- Downtown | 3 | D95700 | 0 | 
 
## 自転車の乗り入れ可 
 
 自転車の乗り入れ可は、特定の旅行を提供する車両が自転車に対応しているかどうかを示し、ユーザーがマルチモーダル旅行を可能にするサービスを計画およびアクセスするのに役立ちます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed ` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルでは、​​旅行 ` AWE1 ` で使用されるvehicleには少なくとも 1 台の自転車を搭載できること (` bikes_allowed =1`)、旅行 ` AWE2 ` で使用されるvehicleには搭載できないこと (` bikes_allowed=2`) を指定しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|-----------|---------|---------------| 
 | RA | WE | AWE1 | 1 | 
 | RA | WE | AWE2 | 2 | 
 
## ヘッドサイン 
 
 ヘッドサインを使用すると、旅行の目的地を示すために車両が使用する標識を伝えることができ、ユーザーが正しい交通サービスを識別しやすくなります。この機能は、特定のルートに沿ったヘッドサインの変更をサポートします。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルでは、​​最初のテーブルは、トリップ `AWE1` と `AWE2` で使用される行先標識を指定し、2 番目のテーブルは、`AWE1` の行先標識が停車駅 `TAS004` の後で変更され、`trips.txt` で指定された行先標識を上書きすることを示しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_headsign | 
 |----------|-----------|---------|---------------| 
 | RA | WE | AWE1 | ダウンタウン | 
 | RA | WE | AWE2 | ミッション | 
 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | 
 |--------|--------------|----------------|---------|--------------|-------------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | ダウンタウン - メイン スクエア | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | ダウンタウン - メイン スクエア | 
 
## ロケーション タイプ 
 
 ロケーション タイプは、出口/入口、ノード、搭乗エリアなどの交通機関駅内の主要エリアとそれらの関係を分類するために使用されます。ロケーション タイプは、Pathways を使用して交通機関駅をモデル化するための基盤として機能します。
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? note "サンプル データ" 
 
<p style="font-size:16px"> 
 次のサンプルは、 `stops.txt`内の交通機関の駅内の複数の場所を示しています。主要な場所を表す親駅と、プラットフォーム、入口/出口、一般的なノードなどの子の場所です。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | location_type | parent_station | 
 |--------------|-------------------------------------------------------|-----------------| 
 | Station_A102 | メインストリート駅 | 1 | | 
 | A102_B01 | メインストリート駅 - 北プラットフォーム | 0 | Station_A102 | 
 | A102_B02 | メインストリート駅 - 南プラットフォーム | 0 | Station_A102 | 
 | A102_E01 | メインストリート駅 - 入口/出口 | 2 | Station_A102 | 
 | A102_S01 | メインストリート駅 - 入口階段の上部 | 3 | Station_A102 | 
 | A102_S02 | メインストリート駅 - 入口階段の下部 | 3 | Station_A102 | 
 | A102_S03 |メイン ストリート駅 - 北側プラットフォーム階段の最上部 | 3 | Station_A102 | 
 | A102_S04 | メイン ストリート駅 - 北側プラットフォーム階段の最下部 | 3 | Station_A102 | 
 | A102_S05 | メイン ストリート駅 - 南側プラットフォーム階段の最上部 | 3 | Station_A102 | 
 | A102_S06 | メイン ストリート駅 - 南側プラットフォーム階段の最下部 | 3 | Station_A102 | 
 | A102_F01 | メイン ストリート駅 - 改札口の有料側 | 3 | Station_A102 | 
 | A102_F02 | メイン ストリート駅 - 改札口の未払い側 | 3 | Station_A102 | 
 
## 頻度ベースのサービス 
 
 頻度ベースのサービスは、10 分間隔で運行するバスや、指定された時間間隔で 2 分間隔で運行する地下鉄サービスなど、一定の頻度で運行するサービスをモデル化するために使用できます。 
 頻度ベースのサービスをモデル化する場合、乗客に表示される時間を決定するために、 `stop_times.txt`にstops間の相対時間が含まれます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| `trip_id`、 `start_time`、`end_time`、 `headway_secs`、 `exact_times` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? `サンプルデータ`の注記 
 
<p style="font-size:16px"> 
 次のサンプルは、30 分間隔で運行される`AWE1` (`headway_secs=1800`) と、15 分間隔で運行される`AWE2` (`headway_secs=900`) という 2 つの異なる運行を示しています。
<p style="font-size:16px"> 
 `exact_times`フィールドは、スケジュールが ’ start_time’ フィールドに入力された正確な開始時刻に従うかどうかを示します: 
 - 旅行 `AWE1` は、午前 6:10 から午後 12:00 まで 30 分ごとに出発します。
 - 旅行 `AW2` は、午前 6:00、午前 6:15、午前 6:30 などに出発します。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 
 
 | trip_id | start_time | end_time | headway_secs | exact_times | 
 ---------|------------|----------|--------------|-------------| 
 AWE1 | 6:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 6:00:00 | 19:50:00 | 900 | 1 | 
 
## 乗り換え 
 
 乗り換えは、異なる旅行セグメント (または区間) 間の遷移に関する詳細を提供し、旅行計画者がtransfersを含む旅程の実現可能性を判断できるようにします。transfersを指定しても、乗客が他の場所に乗り換えることがtを意味するわけではなく、特定のtransfersが不可能であるか、乗り換えに最小限の時間がrequireかを示すだけです。 
 
 |含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`、`to_stop_id`、`from_route_id`、`to_route_id`、`from_trip_id`、`to_trip_id`、`transfer_type`、`min_transfer_time` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、3 つの異なるtransfersを示しています。1 つはstops間での乗り換えで、乗り換え時間は最低 5 分です。もう 1 つは 2 つのroutes間の時間指定乗り換えポイントで、もう 1 つは同じvehicleによる 2 つの移動間の座席での乗り換えです。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 
 
 | from_stop_id | to_stop_id | from_route_id | to_route_id | from_trip_id | to_trip_id | transfer_type | min_transfer_time | 
 |--------------|------------|--------------|-------------|--------------|------------|---------------|-------------------| 
 | s6 | s7 | | | | | 2 | 300 | 
 | | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## 翻訳 
 
 翻訳により、駅名などのサービス情報を複数の言語で提供できるようになり、旅行プランナーはユーザーの言語と場所の設定に応じて特定の言語で情報を表示できるようになります。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`、`field_name`、`language`、`translation`、`record_id`、`record_sub_id`、`field_value` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? note "サンプルデータ" 
 
<p style="font-size:16px"> 
 次のサンプルは、`routes.txtで使用される 2 つのフィールド、`route_long_nameと `route_descにフランス語とスペイン語の翻訳が提供されていることを示しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 
 
 | table_name | field_name | language | translation | record_id | record_sub_id | field_value | 
 |-----------|-----------------|----------|---------------------------------------------------------|---------------|-------------| 
 |routes| route_long_name | ES | Mission- Centro | RA | | | 
 | ルート | routes | FR | Mission- Centre ville | RA | | | 
 | ルート | route_desc | ES | Lower Mission からのルート`A`は centro にあります | RA | | | 
 |routes| routes | FR | ルート`A`は Lower Mission から Centre-ville へ向かいます。 | RA | | | 
 
## 帰属 
 
 帰属により、データセットの作成に関与した組織 (プロデューサー、オペレーター、および/または当局など) に関する追加の詳細を共有できるようになります。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`、`agency_id`、 `route_id`、 `trip_id`、`organization_name`、`is_producer`、`is_operator`、`is_authority`、`attribution_url`、`attribution_email`、`attribution_phone` | 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? `サンプルデータ`の注記 
 
<p style="font-size:16px"> 
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 
 
 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |----------------|-----------|----------|----------|--------------------------|-------------|-------------|--------------|----------------------------------|--------------------------|-------------------| 
 | op01 | tb | | | Transit Bus | | 1 | | https://www.transitbus.org/fares | contact@transitbus.org | (777) 555-7777 | 
 | au01 | gra | | | Greater Region Transport | 1 | | 1 | https://www.gra1.org | contact@gra1.org | (555) 555-5555 | 
 | op02 | | rtd023 | | バス会社A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | op03 | | rtd025 | | バス会社B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

