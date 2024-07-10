# 票价 
 GTFS可以精确模拟世界各地不同交通运输机构使用的各种票价结构，例如基于区域、行驶距离或一天中GTFS时间的票价。GTFS 票价会告知乘客适用于其行程的price以及他们可以用来支付的媒介。
 
## 票价产品 
 
 票价产品列出了交通运输agency提供的用于访问服务的票证或票价类型（即单程票价、月票、换乘费等）。票价产品是模拟机构票价结构的基础，并通过 `fare_leg_rules.txt` 中概述的机制与交通服务相链接。票价产品与各种旅行条件（例如routes、区域和时间）的关联决定了各个旅行段和transfers的票价成本。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例展示的是简单的票价产品（单程 2.75 美元）。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name |amount|currency| 
 |------------------|--------------------|---|---|---| 
 | single_ride | 单程票价 | 2.75 | 美元 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id | 
 |------------------| 
 | single_ride | 
 
 
## 票价媒体 
 
 票价媒体定义了可用于保存和/或验证票价产品的支持媒体。这指的是物理或虚拟容器，例如纸质车票、可充值的交通卡，甚至使用信用卡或智能手机的非接触式付款。 
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例展示了旧金山湾区不同票价媒体的片段。`Clipper` 被描述为具有 `fare_media_type=2` 的实体交通卡。`SFMTA Munimobile` 被描述为具有 `fare_media_type=2` 的移动应用程序。无需票证即可直接交给司机的 `Cash` 为 `fare_media_type=0`。
</p> 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>票价媒体.txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------------------|-----------------| 
 | clipper | Clipper | 2 | 
 | munimobile | SFMTA MuniMobile | 4 | 
 | cas​​h | Cash | 0 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|--------------------|---|---|---| 
 | single_ride | 单程票价 | 2.75 | USD | munimobile | 
 
 
 
 
## 基于路线的票价
 
 基于路线的票价用于为特定routes组分配不同的票价，例如特快服务的特殊票价或区分快速公交服务与传统公交服务的票价。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **先决条件**：
 
 - [基本功能](../base) 
 - [票价产品功能](#fare-products) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例展示了routes分为特快路线和本地路线的系统，每种路线都与不同的票价产品相关联。</p> 
 
<p style="font-size:16px"> **使用 `.txt+ `.txt**</p> 
 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#networkstxt"><b>网络.txt</b></a><br> 
</p> 
 
 |network_id |network_name| 
 |------------|-----------------| 
 | 快递 | 快递 | 
 | 本地 | 本地 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#route_networkstxt"><b>路线网络.txt</b></a><br> 
</p> 
 
 | network_id | route_id | 
 |------------|-----------| 
 | express | express_a | 
 | express | express_b | 
 | 本地 | local_1 | 
 | 本地 | local_2 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | 特快 | 特快单程票 | 
 | 本地 | 本地单程票 | 
 
<p style="font-size:16px"> **或使用 `routes**</p> 
 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | express_a | express | 
 | express_b | express | 
 | local_1 | local | 
 | local_2 | local | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | express | express_single_ride | 
 | local | local_single_ride | 
 
 
## 基于时间的票价
 
基于时间的票价用于分配特定时间或一周中某天的票价，如高峰和非高峰票价和/或周末票价。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [票价产品功能](../fares/#fare-products) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例展示了一个系统，其中高峰时段为 8:00 至 10:00，其余时段为非高峰时段。</p> 
 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
<a href="../../../documentation/schedule/reference/#timeframestxt"><b>时间框架.txt</b></a><br> 
</p> 
 
 | timeframe_group_id |start_time|end_time|service_id | 
 |--------------------|------------|----------|------------| 
 | 高峰 | 8:00:00 | 10:00:00 | 全天 | 
 | 常规 | 0:00:00 | 08:00:00 | 全天 | 
 | 常规 | 10:00:00 | 24:00:00 | 全天 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id | 
 |-------------------------|---------------------| 
 | peak | peak_single_ride | 
 | regular | regular_single_ride | 
 
 
## 基于区域的票价
 
基于区域的票价用于表示基于区域的系统，当从一个特定区域到另一个区域旅行时适用特定的票价。区域由一组stops定义。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id`, `area_name`| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [票价产品功能](../fares/#fare-products) 
 
 ??? 注意“示例数据”
 
<p style="font-size:16px"> 
 以下示例显示了从 A 区到 B 区的票价。</p> 
 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id | area_name | 
 |---------|-----------| 
 | zone_a | 区域 A | 
 | zone_b | 区域 B | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id | stop_id | 
 |---------|---------| 
 | zone_a | stop_a | 
 | zone_a | stop_b | 
 | zone_b | stop_c | 
 | zone_b | stop_d | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id | 
 |--------------|------------|-----------------| 
 | zone_a | zone_b | zone_a_b_single | 
 
## 票价转乘 
 
 票价转乘用于定义在航段（或各个旅行段）之间转乘时适用的规则。这可以模拟多航段旅行的总费用，考虑特殊转乘政策，例如特定时间限制内的免费transfers，或根据已旅行的航段应用票价折扣。
 
 | 包含的文件 | 包含的字段 | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id`, `transfer_count`, `duration_limit`, `duration_limit_type`, `fare_transfer_type`, `fare_product_id`| 
 
 **先决条件**: 
 
 - [基本功能](../base) 
 - [票价产品功能](../fares/#fare-products) 
 
 ??? 注意“示例数据” 
 
<p style="font-size:16px"> 
 以下示例说明在 2 小时内，系统内的 A 段之间允许无限制免费transfers。</p> 
 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |---------------| 
 | a | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|----------------|---------------------|--------------------------------|-----------------| 
 | a | a |-1 | 7200 | 1 | 0 | free_transfer | 
 
 
## Fares v1 
 
 Fares v1 是上述其他 Fares 功能的传统替代方案。它允许使用 ` fare_rules.txt` 和 `fare_attributes.txt ` 文件对基本票价信息（如票价定价、支付方式transfers和基于区域的票价）进行建​​模。虽然制作起来更简单，但它在建模更复杂的票价结构方面能力较弱，并且可能会因其他票价功能（属于所谓的 Fares v2 的一部分）的充分认可而被弃用。
 
 |包含的文件 | 包含的字段 | 
 |----------------------------------|----------------------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **先决条件**：
 
 - [基本特征](../base) 
 
 ??? 注意“样本数据”
 
<p style="font-size:16px"> 
 以下示例说明使用预付卡进行网络行程的费用为 3.20CAD元，允许在 2 小时内免费transfers。</p> 
 
 ！！！ 笔记 ”” 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 |fare_id |price|currency_type|payment_method|transfers|transfer_duration| 
 |-------------------|-------------------|---------------------------|----------------|-----------|-------------------| 
 | 预付卡票价 | 3.2 |CAD| 1 | | 7200 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 |fare_id |route_id |origin_id |destination_id | 
 |-------------------|-----------------|-----------------|-----------------|
 | 预付卡票价 | 线路 1 | 地铁站 | 地铁站 | 
 | 预付卡票价 | 线路 2 | 地铁站 | 地铁站 | 
 
 !!! 注意“”
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-------------|------------|-----------------| 
 | A | stopA | 43.670049 |-79.385389 | subway_stations | 
 | B | stopB | 43.671049 |-79.386789 | subway_stations | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | A | stopA | 43.670049 |-79.385389 | subway_stations | 
 | B | stopB | 43.671049-79.386789 | 地铁站 | 
 
 

