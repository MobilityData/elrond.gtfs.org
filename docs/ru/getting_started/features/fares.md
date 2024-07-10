# Тарифы 
 GTFS позволяет точно моделировать широкий спектр структур тарифов, используемых различными транспортными агентствами по всему миру, например тарифы по зонам, по пройденному расстоянию или по времени суток. GTFS Fares информирует пассажиров о price, применимой к их поездке, и о средствах массовой информации, которые они могут использовать для оплаты. 
 
## Fare Products 
 
 Fare Products перечисляет типы билетов или тарифов (т.е.тариф на одну поездку, месячный проездной, плата за трансфер и т.д.), предлагаемых транзитным agency для доступа к услуге. Тарифные продукты служат основой для моделирования структуры тарифов агентства и связаны с транзитными услугами посредством механизмов, описанных в `fare_leg_rules.txt. Привязка тарифных продуктов к различным условиям путешествия, таким как routes, районы и время, определяет стоимость тарифа для отдельных сегментов путешествия и transfers. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере представлен простой тариф (2,75 доллара США за одну поездку). 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | 
 |------------------|--------------------|---|---| 
 | одиночная поездка | Стоимость одной поездки | 2,75 | доллары США | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id | 
 |------------------| 
 | одиночная поездка | 
 
 
## Fare Media 
 
 Fare Media определяет поддерживаемые носители, которые можно использовать для хранения и/или проверки тарифного продукта. Это относится к физическим или виртуальным контейнерам, таким как бумажный билет, пополняемая транспортная карта или даже бесконтактная оплата с помощью кредитных карт или смартфонов. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показан фрагмент различных средств Fare Media в районе залива Сан-Франциско. `Clipper` описывается как физическая транспортная карта с `fare_media_type=2`. `SFMTA Munimobile` описывается как мобильное приложение с `fare_media_type=2`. «Наличными», которые выдаются непосредственно водителю без билета, является «fare_media_type=0». 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>Fare_media.txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------------------|-----------------| 
 | машинка для стрижки | Клипер | 2 | 
 | мунимобиль | СФМТА МуниМобайл | 4 | 
 | наличные | Наличные | 0 | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|--------------------|---|---|---| 
 | одиночная поездка | Стоимость одной поездки | 2,75 | доллары США | мунимобиль | 
 
 
 
 
## Тарифы на основе маршрута 
 
 Тарифы на основе маршрута используются для назначения различных тарифов для определенных групп routes, например, специальных тарифов на экспресс-услуги или дифференциации тарифов между автобусами Rapid Транзитные перевозки по сравнению с традиционными автобусными перевозками. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Функция тарифных продуктов](#fare-products) 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показана система, которая классифицирует routes на экспресс- и местные категории, каждая из которых связана с отдельными тарифными продуктами.</p> 
 
<p style="font-size:16px"> **Использование `.txt+ `.txt**</p> 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#networkstxt"><b>сети.txt</b></a><br> 
</p> 
 
 | network_id | network_name | 
 |------------|-----------------| 
 | экспресс | Экспресс | 
 | местный | Местный | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#route_networkstxt"><b>Route_networks.txt</b></a><br> 
</p> 
 
 | network_id | route_id | 
 |------------|-----------| 
 | экспресс | экспресс_а | 
 | экспресс | экспресс_б | 
 | местный | местный_1 | 
 | местный | местный_2 | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | экспресс | express_single_ride | 
 | местный | local_single_ride | 
 
<p style="font-size:16px"> **ИЛИ используя `routes.networks_id`**</p> 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | экспресс_а | экспресс | 
 | экспресс_б | экспресс | 
 | местный_1 | местный | 
 | местный_2 | местный | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | экспресс | express_single_ride | 
 | местный | local_single_ride | 
 
 
## Тарифы, основанные на времени 
 
 Тарифы, основанные на времени, используются для назначения тарифов для определенного времени суток или дня недели, например, тарифы в пиковое и внепиковое время и/или тарифы выходного дня. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Функция тарифных продуктов](../fares/#fare-products) 
 
 ?? ? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере представлена ​​система, в которой часы пик приходится на период с 8:00 до 10:00, а остальные часы — внепиковое время.</p> 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#timeframestxt"><b>таймфреймы.txt</b></a><br> 
</p> 
 
 | timeframe_group_id | start_time | end_time | service_id | 
 |--------------------|------------|----------|------------| 
 | пик | 8:00:00 | 10:00:00 | весь день | 
 | обычный | 0:00:00 | 08:00:00 | весь день | 
 | обычный | 10:00:00 | 24:00:00 | весь день | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id | 
 |-------------------------|---------------------| 
 | пик | пик_single_ride | 
 | обычный | регулярная_одиночная_поездка | 
 
 
## Тарифы на основе зон 
 
 Тарифы на основе зон используются для обозначения зональных систем, в которых при путешествии из одной конкретной зоны в другую применяется определенный тариф. Зона определяется группой stops. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id, `area_name| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id, `stop_id`| 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Функция тарифных продуктов](../fares/#fare-products) 
 
 ?? ? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показана стоимость проезда из зоны A в зону B.</p> 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id | area_name | 
 |---------|-----------| 
 | зона_а | Зона А | 
 | зона_b | Зона Б | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id | stop_id | 
 |---------|---------| 
 | зона_а | стоп_а | 
 | зона_а | стоп_б | 
 | зона_b | стоп_с | 
 | зона_b | стоп_д | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id | 
 |--------------|------------|-----------------| 
 | зона_а | зона_b | зона_a_b_single | 
 
## Переносы тарифов 
 
 Переносы тарифов используются для определения правил, применимых при пересадке между этапами (или отдельными сегментами путешествия). Это позволяет моделировать общую стоимость поездки с несколькими этапами, учитывая специальные политики трансфера, такие как бесплатные transfers в течение определенного периода времени, или применяя скидки на тарифы на основе уже пройденных этапов. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id, `transfer_count, `duration_limit, `duration_limit_type, `fare_transfer_type`, `fare_product_id`| 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Функция тарифных продуктов](../fares/#fare-products) 
 
 ?? ? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 Следующий пример показывает, что в течение двухчасового окна разрешены неограниченные бесплатные transfers между этапом А внутри системы.</p> 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |---------------| 
 | а | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|----------------|---------------------|----|---------------------------------| 
 | а | а |-1 | 7200 | 1 | 0 | бесплатный_трансфер | 
 
 
## Fares v1 
 
 Fares v1 — это устаревшая альтернатива другим функциям Fares, описанным выше. Это позволяет моделировать базовую информацию о тарифах, такую ​​как цены на проезд, способы transfers и тарифы на основе зон, используя файлы `fare_rules.txt и `fare_attributes.txt. Несмотря на то, что его проще создать, он менее эффективен или моделирует более сложные структуры тарифов и может быть признан устаревшим при достаточном одобрении других функций Fare (которые являются частью так называемой Fares v2). 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id``destination_id` `contains_id`| 
 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 Следующий пример показывает, что поездка по сети стоит 3,20 CAD долларов при использовании предоплаченной карты, что позволяет совершать бесплатные transfers в течение двух часов.</p> 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 | fare_id | price | currency_type | payment_method | transfers | transfer_duration | 
 |---|-----------------------|---------------|----------------|-----------|-------------------| 
 | предоплаченная карта_тариф | 3.2 | CAD | 1 | | 7200 | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 | fare_id | route_id | origin_id | destination_id | 
 |-------------------|----------|-----------------|-----------------| 
 | предоплаченная карта_тариф | линия1 | станции_метро | станции_метро | 
 | предоплаченная карта_тариф | линия2 | станции_метро | станции_метро | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | А | стопА | 43.670049 |-79,385389 | станции_метро | 
 | Б | стопБ | 43,671049 |-79,386789 | станции_метро | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | А | стопА | 43.670049 |-79,385389 | станции_метро | 
 | Б | стопБ | 43.671049 |-79,386789 | станции_метро | 
 
 

