# Serviços Flexíveis 
 Os serviços flexíveis, também chamados de serviços de resposta à demanda, são serviços que não seguem o comportamento comum do serviço programado e/ou fixo. 
 
## Paradas Contínuas 
 
 Paradas Contínuas são usadas quando os passageiros podem ser recolhidos e/ou deixados entre as stops programadas. 
 Isso pode ser especificado em `routes.txt, indicando que os passageiros podem ser recolhidos ou deixados em qualquer ponto ao longo do trajeto do veículo para cada viagem da rota, ou em `stop_times.txt` para uma seção específica de um percurso. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off` | 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra duas maneiras de representar a Parada Contínua. 
</p> 
 
<p style="font-size:16px"> 
 A primeira amostra mostra que embarques e desembarques são permitidos em qualquer ponto ao longo da rota `RA`. 
</p> 
 
<p style="font-size:16px"> 
 A segunda amostra mostra que pickups e dropoffs são permitidos entre a terceira e a quinta stops da viagem `AWE1`, realizado atribuindo-se os valores `continuous_pickup` e `continuous_drop_off` a `stop_sequence=3` e `stop_sequence=4`. 
</p> 
 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | route_short_name | route_type | continuous_pickup | continuous_drop_off | 
 |----------|------------------|------------|-------------------|---------------------| 
 | RA | 17 | 3 | 0 | 0 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | continuous_pickup | continuous_drop_off | 
 |--------|--------------|----------------|---------|---------------|-------------------|---------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | | | 
 
## Regras de reserva 
 
 As regras de reserva podem ser usadas para permitir que os usuários reservem uma viagem em um serviço que responda à demanda. Estas regras descrevem os pré-requisitos necessários para reservas bem-sucedidas e fornecem informações de contato onde os usuários podem fazer reservas de viagens. Este recurso deve ser usado em conjunto com [Rotas predefinidas com desvio](#rotas-predefinidas-com-desvio), [Serviços responsivos à demanda baseados em zona](#serviços responsivos à demanda baseados em zona) e [Paradas fixas Recursos de serviços responsivos à demanda](#fixed-stops-demand-responsive-services), se tais serviços require reserva. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`, `booking_type`, `prior_notice_duration_min`, `prior_notice_duration_max`, `prior_notice_last_day`, `prior_notice_last_time `, `prior_notice_start_day`, `prior_notice_start_time`, `prior_notice_service_id`, `message`, `pickup_message`, `drop_off_message`, `phone_number`, `info_url`, `booking_url` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra dois conjuntos diferentes de regras de reserva, o primeiro para viagens que devem ser reservadas com pelo menos um dia de antecedência (antes das 13h) e não mais de 14 dias antes, e um segundo para viagens que podem ser reservadas pelo menos 45 minutos antes da viagem e não mais de 5 horas antes. 
 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 
 
 | booking_rule_id | tipo_de_reserva | prior_notice_duration_min | prior_notice_duration_max | prior_notice_last_day | prior_notice_last_time | prior_notice_start_day | prior_notice_start_time | prior_notice_service_id | message | mensagem_de_recolhimento | drop_off_message | número_telefone | info_url | URL_da_reserva | 
 |-----------------|-------------|---------------------------|---------------------------|-----------------------|-------------|------------------------|--------------|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------|----------------|----------------------|-------------------------| 
 | rota_br_1818 | 2 | | | 1 | 13h00 | 14 | 9:00 | | Para solicitar uma viagem, ligue para 123-111-2233 antes das 13h, pelo menos um dia útil antes da sua viagem. Você pode reservar viagens com até 14 dias úteis de antecedência. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | rota_br_4545 | 1 | 45 | 300 | | | | | | Para solicitar uma carona, utilize o sistema de reservas oficial em nosso site, as viagens devem ser reservadas com pelo menos 45 minutos de antecedência | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## Rotas predefinidas com desvio 
 
 Rotas predefinidas com desvio podem ser usadas para modelar serviços flexíveis onde os veículos podem desviar-se brevemente de uma rota específica para pegar usuários que reservaram uma viagem dentro de uma área específica ao longo do rota. Isso usa uma combinação de stops tradicionais (como um serviço regular programado) e zonas usando `locations.geojson`. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Tipo`, `Recursos`, `Recursos:Tipo`, `Recursos:Id`, `Recursos :Propriedades`, `Features:Propriedades:Stop_name`, `Features:Propriedades:Stop_description`, `Features:Geometria`, `Features:Geometria:Tipo`, `Features:Geometria:Coordenadas` | 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Regras de reserva](#booking-rules) se o serviço exigir reserva 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra uma viagem com três stops fixas que também pode deixar passageiros em qualquer lugar dentro de áreas específicas definidas entre as stops fixas. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | local_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|----------------|---------|------------|---------------|------------------------------|----------------------------|------------|---------------|---------------------|------------------------|--------------------------| 
 | 4545_001 | 10:00:00 | 10:00:00 | S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | zona_S50122_to_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | zona_S50123_to_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
!!! observação "" 
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
 "geometria": { 
 "tipo": "Polygon", 
# Simplificado, apresentando aqui apenas 3 coordenadas. 
 "coordenadas": [
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
 "propriedades": {} 
 }, 
 { 
 "id": "zone_S50123_to_S50124", 
 "tipo": "Recurso", § § "geometria": { 
 "tipo": "Polygon", 
# Simplificado, apresentando aqui apenas 3 coordenadas. 
 "coordenadas": [
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
 "propriedades": {} 
 } 
] 
 } 
 ~~~ 
 
## Serviços responsivos à demanda baseados em zona 
 
 Serviços responsivos à demanda baseados em zona são usados ​​para modelar serviços que permitem coleta e/ou entrega em qualquer local dentro de uma área específica para usuários que reservam uma viagem. Essas áreas são definidas usando `locations.geojson` portanto não require o uso de `stops.txt`, nem `stop_times.arrival_time` &amp; `stop_times.departure_time`. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Tipo`, `Recursos`, `Recursos:Tipo`, `Recursos:Id`, `Recursos :Propriedades`, `Features:Propriedades:Stop_name`, `Features:Propriedades:Stop_description`, `Features:Geometria`, `Features:Geometria:Tipo`, `Features:Geometria:Coordenadas` | 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Regras de reserva](#booking-rules) se o serviço exigir reserva 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra um serviço que pode retirar e entregar passageiros pré-agendados em qualquer lugar entre uma área específica entre 9h e 18h. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | local_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|---------------|------------------------------|-------------------------------|------------|---------------|------------------------|--------------------------| 
 | 2708_001 | área_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | área_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
!!! observação "" 
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
 "geometria": { 
 "tipo": "Polygon", 
# Simplificado, apresentando aqui apenas 3 coordenadas. 
 "coordenadas": [
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
 "propriedades": {} 
 } 
] 
 } 
 ~~~ 
 
## Paradas fixas exigem serviços responsivos 
 Os serviços responsivos à demanda de paradas fixas são usados ​​para modelar serviços que permitem embarque e/ou desembarque em qualquer local dentro de um grupo de stops predefinidas para usuários que reservam uma viagem. Esses grupos de stops são definidos usando `location_groups.txt` e `location_group_stops.txt`. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Regras de reserva](#booking-rules) se o serviço exigir reserva 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra um serviço que pode buscar e entregar passageiros pré-agendados em 4 stops diferentes entre 7h e 10h. 
 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_groupstxt"><b>.txt</b></a><br> 
</p> 
 
 | location_group_id | location_group_name | 
 |-------------------|-------------------------------| 
 | r27_paradas | stops da Yellow Borough Route 27 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>.txt</b></a><br> 
</p> 
 
 | location_group_id | stop_id | 
 |-------------------|--------| 
 | r27_paradas | syb029 | 
 | r27_paradas | syb030 | 
 | r27_paradas | syb031 | 
 | r27_paradas | syb032 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | location_group_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------------|---------------|-----------------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2714_002 | r27_paradas | 1 | 7:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_paradas | 2 | 7:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

