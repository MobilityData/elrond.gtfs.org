# 運賃 
 GTFS を使用すると、世界中のさまざまな交通機関で使用されている、ゾーン別、移動距離別、または時間帯別の運賃など、さまざまな運賃体系を正確にモデル化できます。GTFS 運賃は、旅行に適用されるpriceと、支払いに使用できる媒体を乗客に通知します。
 
## 運賃商品 
 
 運賃商品には、交通agencyがサービスにアクセスするために提供するチケットまたは運賃の種類 (つまり、片道運賃、月間パス、乗り換え料金など) がリストされます。運賃商品は、機関の運賃構造をモデル化するための基盤として機能し、`fare_leg_rules.txt` で概説されているメカニズムを通じて交通サービスにリンクされています。運賃商品をroutes、エリア、時間などのさまざまな旅行条件に関連付けることで、個々の旅行区間とtransfersの運賃コストが決まります。
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`、`fare_product_name`、`amount`、`currency`、`fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、単純な運賃商品 (片道 2.75 米ドル) を示しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | 
 |------------------|--------------------|---|---| 
 | single_ride | 片道料金 | 2.75 | USD | 
 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id | 
 |------------------| 
 | single_ride | 
 
 
## 運賃メディア 
 
 運賃メディアは、運賃商品の保持や検証に使用できるサポートされているメディアを定義します。これは、紙のチケット、再チャージ可能な交通カード、さらにはクレジットカードやスマートフォンによる非接触型決済などの物理または仮想のコンテナーを指します。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`、`fare_media_name`、`fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、サンフランシスコ ベイエリアのさまざまな運賃メディアのスニペットを示しています。`Clipper` は、`fare_media_type=2` の物理的な交通カードとして説明されています。`SFMTA Munimobile` は、`fare_media_type=2` のモバイル アプリとして説明されています。チケットなしで運転手に直接渡される `Cash` は、`fare_media_type=0` です。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>運賃_メディア.txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |--------------|------------------|-----------------| 
 | clipper | Clipper | 2 | 
 | munimobile | SFMTA MuniMobile | 4 | 
 | cas​​h | Cash | 0 | 
 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|--------------------|---|---|---| 
 | single_ride | 片道運賃 | 2.75 | USD | munimobile | 
 
 
 
 
 
## 路線ベースの運賃 
 
 路線ベースの運賃は、急行サービスの特別運賃や、バス高速輸送サービスと従来のバスサービスの運賃を区別するなど、特定のroutesグループに異なる運賃を割り当てるために使用されます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`、`network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`、`network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`、 `route_id`| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 - [運賃製品機能](#fare-products) 
 
 ???注記`サンプルデータ`

<p style="font-size:16px"> 
 次のサンプルは、routesをエクスプレス カテゴリとローカル カテゴリに分類し、それぞれが異なる運賃商品に関連付けられているシステムを示しています。</p> 
 
<p style="font-size:16px"> **`networks.txt` + `route_networks.txt` を使用する**</p> 
 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#networkstxt"><b>ネットワーク.txt</b></a><br> 
</p> 
 
 | network_id | network_name | 
 |-----------|-----------------| 
 | express | Express | 
 | local | Local | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#route_networkstxt"><b>ルートネットワーク.txt</b></a><br> 
</p> 
 
 | network_id | route_id | 
 |-----------|-----------| 
 | express | express_a | 
 | express | express_b | 
 | local | local_1 | 
 | local | local_2 | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |-----------|-----------------| 
 | express | express_single_ride | 
 | local | local_single_ride | 
 
<p style="font-size:16px"> **または`routesを使用する**</p> 
 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | express_a | express | 
 | express_b | express | 
 | local_1 | local | 
 | local_2 | local | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |-----------|-----------------| 
 | express | express_single_ride | 
 | local | local_single_ride | 
 
 
## 時間ベース運賃 
 
 時間ベース運賃は、ピーク運賃やオフピーク運賃、週末運賃など、特定の時間帯や曜日の運賃を割り当てるために使用されます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`、`from_timeframe_group_id`、`to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`、 `start_time`、`end_time`、`service_id`| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 - [運賃商品機能](../fares/#fare-products) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、ピーク時間が 8:00 から 10:00 で、残りの時間がオフピークであるシステムを示しています。</p> 
 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#timeframestxt"><b>時間枠.txt</b></a><br> 
</p> 
 
 | timeframe_group_id | start_time | end_time | service_id | 
 |--------------------|------------|-----------|------------| 
 | ピーク | 8:00:00 | 10:00:00 | all_day | 
 | 通常 | 0:00:00 | 08:00:00 | all_day | 
 | 通常 | 10:00:00 | 24:00:00 | all_day | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id | 
 |------------------------|---------------------| 
 |peak |peak_single_ride | 
 |regular |regular_single_ride | 
 
 
## ゾーンベースの運賃 
 
 ゾーンベースの運賃は、特定のゾーンから別のゾーンに移動するときに特定の運賃が適用されるゾーンベースのシステムを表すために使用されます。ゾーンは、stopsのグループによって定義されます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`、`from_area_id`、`to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id`、`area_name`| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`、 `stop_id`| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 - [運賃商品機能](../fares/#fare-products) 
 
 ??? `サンプルデータ`の注記 
 
<p style="font-size:16px"> 
 次のサンプルは、ゾーン A からゾーン B までの運賃を示しています。</p> 
 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id | area_name | 
 |--------|-----------| 
 | zone_a | ゾーン A | 
 | zone_b | ゾーン B | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id | stop_id | 
 |--------|---------| 
 | zone_a | stop_a | 
 | zone_a | stop_b | 
 | zone_b | stop_c | 
 | zone_b | stop_d | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id | 
 |--------------|-----------|-----------------| 
 | zone_a | zone_b | zone_a_b_single | 
 
## 運賃の乗り換え 
 
 運賃の乗り換えは、区間（または個々の旅行セグメント）間の乗り換え時に適用されるルールを定義するために使用されます。これにより、特定の時間制限での無料transfersや、すでに旅行した区間に基づいた運賃割引の適用などの特別な乗り換えポリシーを考慮して、複数区間の旅行行程の合計コストをモデル化できます。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`、`to_leg_group_id`、`transfer_count`、`duration_limit`、`duration_limit_type`、`fare_transfer_type`、`fare_product_id`| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 - [運賃商品機能](../fares/#fare-products) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、2 時間のウィンドウ内で、システム内の Leg A 間で無制限の無料transfersが許可されていることを示しています。</p> 
 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |--------------| 
 | a | 
 
 !!! 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|---------------------|--------------------|-----------------| 
 | a | a |-1 | 7200 | 1 | 0 | free_transfer | 
 
 
## Fares v1 
 
 Fares v1 は、上で説明した他の Fares 機能の従来の代替手段です。` fare_rules.txt` および `fare_attributes.txt ` ファイルを使用して、運賃設定、支払い方法のtransfers、ゾーンベースの運賃などの基本的な運賃情報をモデル化できます。生成は簡単ですが、より複雑な運賃構造をモデル化する能力が低く、他の運賃機能 (いわゆる Fares v2 の一部) の十分な承認があれば廃止される可能性があります。
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? note "サンプルデータ" 
 
<p style="font-size:16px"> 
 次のサンプルは、プリペイド カードを使用してネットワークを移動すると 3.20CADドルかかり、2 時間以内であれtransfersが無料になることを示しています。</p> 
 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 |fare_id |price|currency_type|payment_method|transfers|transfer_duration| 
 |-------------------|-------|---------------|----------------|----------|-------------------| 
 | プリペイドカード運賃 | 3.2 | CAD | 1 | | 7200 | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 | fare_id | route_id | origin_id | destination_id | 
 |-------------------|---------|-----------------|-----------------| 
 | prepaid-card_fare | line1 | subway_stations | subway_stations | 
 | prepaid-card_fare | line2 | subway_stations | subway_stations | 
 
 !!! 注 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | A | stopA | 43.670049 |-79.385389 | 地下鉄駅 | 
 | B | stopB | 43.671049 |-79.386789 | 地下鉄駅 | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|------------|------------|------------|-----------------| 
 | A | 停留所A | 43.670049 |-79.385389 | 地下鉄駅 | 
 | B | 停留所B | 43.671049 |-79.386789 | 地下鉄駅 | 
 
 

