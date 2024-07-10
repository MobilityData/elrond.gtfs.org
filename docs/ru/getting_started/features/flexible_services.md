# Гибкие услуги 
 Гибкие услуги, также называемые услугами по требованию, — это услуги, которые не следуют обычному поведению плановых и/или фиксированных услуг. 
 
## Непрерывные остановки 
 
 Непрерывные остановки используются, когда гонщиков можно забрать и/или высадить между запланированными stops. 
 Это можно указать либо в `routes.txt, указывая, что пассажиров можно забрать или высадить в любой точке пути движения транспортного средства для каждой поездки по маршруту, либо в `stop_times.txt` для определенного участка.маршрута. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off` | 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показаны два способа представления непрерывной остановки. 
</p> 
 
<p style="font-size:16px"> 
 Первый пример показывает, что посадка и высадка разрешены в любой точке маршрута RA. 
</p> 
 
<p style="font-size:16px"> 
 Второй пример показывает, что посадки и высадки разрешены между третьей и пятой stops рейса `AWE1, что достигается путем присвоения значений `continuous_pickup и `continuous_drop_off значениям `stop_sequence=3` и `stop_sequence=4`. 
</p> 
 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | route_short_name | route_type | continuous_pickup | continuous_drop_off | 
 |----------|------------------|------------|-------------------|---------------------| 
 | РА | 17 | 3 | 0 | 0 | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | continuous_pickup | continuous_drop_off | 
 |---------|--------------|----------------|---------|---------------|-------------------|---------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | ТАС001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 | ТАС002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | ТАС003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 | ТАС004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 | ТАС005 | 5 | | | 
 
## Правила бронирования 
 
 Правила бронирования могут использоваться для того, чтобы пользователи могли бронировать поездку с использованием услуги, реагирующей на спрос. Эти правила определяют необходимые предпосылки для успешного бронирования и предоставляют контактную информацию, по которой пользователи могут забронировать поездку. Эту функцию следует использовать вместе с [Предопределенными маршрутами с отклонением](#predefine-routes-with-deviation), [Услугами реагирования на запросы на основе зон](#услуги реагирования на запросы на основе зон) и [Фиксированные остановки Услуги, реагирующие на спрос](#fixed-stops-demand-responsive-services), если такие услуги require бронирования. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`, `booking_type`, `prior_notice_duration_min`, `prior_notice_duration_max`, `prior_notice_last_day`, `prior_notice_last_time` `, `prior_notice_start_day`, `prior_notice_start_time`, `prior_notice_service_id`, `message`, `pickup_message`, `drop_off_message`, `phone_number`, `info_url`, `booking_url` | 
 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показаны два разных набора правил бронирования: первый для поездок, которые необходимо бронировать минимум за день (до 13:00) и не более чем за 14 дней, а второй для поездок, которые можно забронировать.минимум за 45 минут до поездки и не более чем за 5 часов. 
 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 
 
 | booking_rule_id | тип_бронирования | Prior_notice_duration_min | Prior_notice_duration_max | Prior_notice_last_day | Prior_notice_last_time | Prior_notice_start_day | Prior_notice_start_time | Prior_notice_service_id | message | пикап_сообщение | drop_off_message | номер_телефона | info_url | адрес_бронирования | 
 |-----------------|--------------|---------------------------|---------------------------|-----------------------|------------------------|------------------------|-------------------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------|----------------|----------------------|-------------------------| 
 | маршрут_br_1818 | 2 | | | 1 | 13:00 | 14 | 9:00 | | Чтобы заказать поездку, позвоните по телефону 123-111-2233 до 13:00, по крайней мере, за один рабочий день до поездки. Вы можете забронировать поездки за 14 рабочих дней заранее. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | маршрут_br_4545 | 1 | 45 | 300 | | | | | | Чтобы заказать поездку, воспользуйтесь официальной системой бронирования на нашем сайте, поездки необходимо бронировать минимум за 45 минут | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## Предопределенные маршруты с отклонением 
 
 Предопределенные маршруты с отклонением можно использовать для моделирования гибких услуг, при которых транспортные средства могут ненадолго отклоняться от определенного маршрута, чтобы подобрать пользователей, забронировавших поездку в пределах определенной области вдоль маршрут. При этом используется комбинация традиционных stops (например, обычного регулярного рейса) и зон с использованием `locations.geojson`. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Тип`, `Функции`, `Функции:Тип`, `Функции:Идентификатор`, `Функции :Свойства`, `Функции:Свойства:Stop_name`, `Функции:Свойства:Stop_description`, `Функции:Геометрия`, `Функции:Геометрия:Тип`, `Функции:Геометрия:Координаты` | 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Правила бронирования](#booking-rules), если услуга требует бронирования 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показана поездка с тремя фиксированными stops, при которой пассажиры также могут высаживаться в любом месте в пределах определенных зон, определенных между фиксированными stops. 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | location_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|--------------|----------------|---------|-----------------------|---------------|------------------------------|----------------------------|-------------|---------------|---------------------|------------------------|--------------------------| 
 | 4545_001 | 10:00:00 | 10:00:00 | S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | зона_S50122_to_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | зона_S50123_to_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "type": "FeatureCollection", 
 "features": [
 { 
 "id": "zone_S50122_to_S50123", 
 "type": "Feature", 
 "geometry": { 
 "type": "Polygon", 
# Упрощено, здесь представлены только 3 координаты. 
 «координаты»: [
 [
 [
 -73.575952, 
 45.514974 
], 
 [
 -73.577314, 
 45.513433 
], 
 [
 -73.569794, 
 45.5098370 
] 
] 
] 
 }, 
 «свойства»: {} 
 }, 
 { 
 «id»: «zone_S50123_to_S50124», 
 «тип»: «Функция», § § "geometry": { 
 "type": "Polygon", 
# Упрощено, здесь представлены только 3 координаты. 
 «координаты»: [
 [
 [
 -73.561332, 
 45.5085599 
], 
 [
 -73.5701298, 
 45.5124057 
], 
 [
 -73.571302, 
 45.5105563 
] 
] 
] 
 }, 
 «свойства»: {} 
 } 
] 
 } 
 ~~~ 
 
## Зональные услуги реагирования на спрос 
 
 Зональные услуги реагирования на спрос используются для моделирования услуг, которые позволяют забирать и/или высаживать пассажиров в любом месте в пределах определенной области для пользователей, бронирующих поездку. Эти области определяются с помощью «`locations.geojson`», поэтому не require использование «`stops.txt`» или «stop_times». arrival_time` &amp; `stop_times.departure_time`. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Тип`, `Функции`, `Функции:Тип`, `Функции:Идентификатор`, `Функции :Свойства`, `Функции:Свойства:Stop_name`, `Функции:Свойства:Stop_description`, `Функции:Геометрия`, `Функции:Геометрия:Тип`, `Функции:Геометрия:Координаты` | 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Правила бронирования](#booking-rules), если услуга требует бронирования 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показана служба, которая может забирать и вывозить заранее забронированных пассажиров в любом месте между определенным районом с 9:00 до 18:00. 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | location_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2708_001 | область_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | область_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "type": "FeatureCollection", 
 "features": [
 { 
 "id": "area_001", 
 "type": "Feature", 
 "geometry": { 
 "type": "Polygon", 
# Упрощено, здесь представлены только 3 координаты. 
 «координаты»: [
 [
 [
 -73.644437, 
 45.5023960 
], 
 [
 -73.641593, 
 45.5054392 
], 
 [
 -73.636580, 
 45.5081683 
] 
] 
] 
 }, 
 «свойства»: {} 
 } 
] 
 } 
 ~~~ 
 
## Фиксированные остановки Требуемые услуги реагирования 
 Службы реагирования на спрос с фиксированными остановками используются для моделирования услуг, которые позволяют забирать и/или высаживать пассажиров в любом месте в пределах группы заранее определенных stops для пользователей, которые заказывают поездку. Эти группы stops определяются с помощью `.txt и `.txt. 
 
 | Файлы включены | Поля включены | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **Предварительные требования**: 
 
 - [Базовые функции](../base) 
 - [Правила бронирования](#booking-rules), если услуга требует бронирования 
 
 ??? примечание «Пример данных» 
 
<p style="font-size:16px"> 
 В следующем примере показан сервис, который может забирать и высаживать предварительно забронированных пассажиров на 4 разных stops с 7 до 10 утра. 
 
</p> 
 !!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_groupstxt"><b>location_groups.txt</b></a><br> 
</p> 
 
 | location_group_id | location_group_name | 
 |-------------------|-------------------------------| 
 | r27_stops | Маршрут Желтого района 27 stops | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>location_group_stops.txt</b></a><br> 
</p> 
 
 | location_group_id | stop_id | 
 |-------------------|---------| 
 | r27_stops | сиб029 | 
 | r27_stops | сиб030 | 
 | r27_stops | сиб031 | 
 | r27_stops | сиб032 | 
 
!!! примечание "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | location_group_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2714_002 | r27_stops | 1 | 7:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_stops | 2 | 7:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

