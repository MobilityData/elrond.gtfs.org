# Tarifas 
 GTFS permite modelar con precisión una amplia variedad de estructuras de tarifas utilizadas por diferentes agencias de tránsito en todo el mundo, como tarifas basadas por zona, distancia recorrida o hora del día. GTFS Tarifas informa a los pasajeros sobre el price aplicable a su viaje y los medios que pueden utilizar para pagar. 
 
## Productos de Tarifa 
 
 Productos de Tarifa enumera los tipos de boletos o tarifas (es decir, tarifa de viaje sencillo, pase mensual, tarifas de transferencia, etc.) que ofrece una agency de tránsito para acceder a un servicio. Los Productos de Tarifa sirven como base para modelar la estructura tarifaria de una agencia y están vinculados al servicio de tránsito a través de mecanismos descritos en `fare_leg_rules.txt`. La asociación de Productos de Tarifa a diversas condiciones de viaje, como routes, áreas y horarios, determina los costos de tarifa para segmentos de viaje y transfers individuales. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo presenta un producto de tarifa simple (viaje sencillo $2.75 USD). 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 

 | fare_product_id | fare_product_name | amount | currency | 
 |------------------|--------------------|---|---| 
 | viaje_único | Tarifa de viaje sencillo | 2,75 | USD | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

 | fare_product_id | 
 |------------------| 
 | viaje_único | 
 
 
## Medios de Tarifa 
 
 Medios de Tarifa define los medios admitidos que se pueden utilizar para retener y/o validar un producto de tarifa. Se trata de contenedores físicos o virtuales, como un billete de papel, una tarjeta de transporte recargable o incluso el pago sin contacto con tarjetas de crédito o teléfonos inteligentes. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra un fragmento de diferentes Medios de Tarifa en el Área de la Bahía de San Francisco. `Clipper` se describe como una tarjeta de transporte física con `fare_media_type=2`. `SFMTA Munimobile` se describe como una aplicación móvil con `fare_media_type=2`. El "efectivo" que se entrega directamente al conductor sin billete es "fare_media_type=0". 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>tarifa_media.txt</b></a><br> 
</p> 

 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------------------|-----------------| 
 | cortadora | Clíper | 2 | 
 | munimóvil | SFMTA MuniMóvil | 4 | 
 | efectivo | Efectivo | 0 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 

 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|--------------------|---|---|---| 
 | viaje_único | Tarifa de viaje sencillo | 2,75 | USD | munimóvil | 
 
 
 
 
## Tarifas Basadas en Rutas 
 
 Tarifas Basadas en Rutas se utiliza para asignar diferentes tarifas para grupos específicos de routes, como tarifas especiales para servicios expresos o diferenciar tarifas entre un Bus Rapid Servicio de tránsito versus servicios de autobús tradicionales. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Función de Productos de Tarifa](#productos-de tarifa) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra un sistema que clasifica las routes en categorías expresas y locales, cada una asociada con distintos productos tarifarios.</p> 
 
<p style="font-size:16px"> **Usando `redes.txt` + `ruta_redes.txt`**</p> 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#networkstxt"><b>redes.txt</b></a><br> 
</p> 

 | network_id | network_name | 
 |------------|-----------------| 
 | expresar | Expreso | 
 | locales | Locales | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#route_networkstxt"><b>rutas_redes.txt</b></a><br> 
</p> 

 | network_id | route_id | 
 |------------|-----------| 
 | expresar | expresar_a | 
 | expresar | expreso_b | 
 | locales | local_1 | 
 | locales | local_2 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

 | network_id | fare_product_id | 
 |------------|-----------------| 
 | expresar | viaje_expreso_single | 
 | locales | local_single_ride | 
 
<p style="font-size:16px"> **O usando `routes.networks_id`**</p> 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

 | route_id | network_id | 
 |------------|------------| 
 | expresar_a | expresar | 
 | expreso_b | expresar | 
 | local_1 | locales | 
 | local_2 | locales | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

 | network_id | fare_product_id | 
 |------------|-----------------| 
 | expresar | viaje_expreso_single | 
 | locales | local_single_ride | 
 
 
## Tarifas Basadas en Tiempo 
 
 Tarifas Basadas en Tiempo se utiliza para asignar tarifas para una hora específica del día o día de la semana, como tarifas pico y valle y/o tarifas de fin de semana. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Función de Productos de Tarifa](../fares/#fare-products) 
 
 ?? ? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo presenta un sistema donde las horas pico son de 8:00 a 10:00 y el resto de horas son valle.</p> 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#timeframestxt"><b>plazos.txt</b></a><br> 
</p> 

 | timeframe_group_id | start_time | end_time | service_id | 
 |--------------------|------------|----------|------------| 
 | pico | 8:00:00 | 10:00:00 | todo el día | 
 | regulares | 0:00:00 | 08:00:00 | todo el día | 
 | regulares | 10:00:00 | 24:00:00 | todo el día | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

 | from_timeframe_group_id | fare_product_id | 
 |-------------------------|---------------------| 
 | pico | pico_single_ride | 
 | regulares | viaje_single_regular | 
 
 
## Tarifas Basadas en Zonas 
 
 Tarifas Basadas en Zonas se utiliza para representar sistemas basados ​​en zonas donde se aplica una tarifa específica cuando se viaja de una zona particular a otra. Una zona está definida por un grupo de stops. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id`, `area_name`| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Función de Productos de Tarifa](../fares/#fare-products) 
 
 ?? ? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra la tarifa de la Zona A a la Zona B.</p> 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 

 | area_id | area_name | 
 |---------|-----------| 
 | zona_a | Zona A | 
 | zona_b | Zona B | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 

 | area_id | stop_id | 
 |---------|---------| 
 | zona_a | parada_a | 
 | zona_a | parada_b | 
 | zona_b | parada_c | 
 | zona_b | detener_d | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

 | from_area_id | to_area_id | fare_product_id | 
 |--------------|------------|-----------------| 
 | zona_a | zona_b | zona_a_b_single | 
 
## Transferencias de Tarifas 
 
 Transferencias de Tarifas se utiliza para definir las reglas aplicables al realizar transferencias entre tramos (o segmentos de viaje individuales). Esto permite modelar el costo total de un viaje de varios tramos, teniendo en cuenta políticas de transferencia especiales, como transfers gratuitas durante un límite de tiempo específico, o aplicando descuentos en tarifas según los tramos ya recorridos. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id`, `transfer_count`, `duration_limit`, `duration_limit_type`, `fare_transfer_type`, `fare_product_id`| 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Función de Productos de Tarifa](../fares/#fare-products) 
 
 ?? ? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo ilustra que dentro de un período de 2 horas, se permiten transfers gratuitas ilimitadas entre la Etapa A dentro del sistema.</p> 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 

 | leg_group_id | 
 |---------------| 
 | un | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 

 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|----------------|---------------------|--------------------|-----------------| 
 | un | un |-1 | 7200 | 1 | 0 | transferencia_gratuita | 
 
 
## Tarifas v1 
 
 Tarifas v1 es una alternativa heredada a otras funciones de Tarifas descritas anteriormente. Permite modelar información básica de tarifas, como precios de tarifas, transfers de métodos de pago y tarifas basadas en zonas utilizando los archivos `fare_rules.txt y `fare_attributes.txt. Si bien es más simple de producir, es menos capaz de modelar estructuras de tarifas más complejas y puede quedar obsoleto con el respaldo suficiente de otras características de Fare (que son parte de lo que se llama Tarifas v2). 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo ilustra que un viaje en una red cuesta $3,20 CAD usando una tarjeta prepaga, lo que permite transfers gratuitas dentro de un período de 2 horas.</p> 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 

 | fare_id | price | currency_type | payment_method | transfers | transfer_duration | 
 |-------------------|-------|---------------|----------------|-----------|-------------------| 
 | tarifa-tarjeta-prepago | 3.2 | CAD | 1 | | 7200 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 

 | fare_id | route_id | origin_id | destination_id | 
 |-------------------|----------|-----------------|------------------| 
 | tarifa-tarjeta-prepago | línea1 | estaciones_de_metro | estaciones_de_metro | 
 | tarifa-tarjeta-prepago | línea2 | estaciones_de_metro | estaciones_de_metro | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | Un | paradaA | 43.670049 |-79.385389 | estaciones_de_metro | 
 | B | paradaB | 43.671049 |-79.386789 | estaciones_de_metro | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | Un | paradaA | 43.670049 |-79.385389 | estaciones_de_metro | 
 | B | paradaB | 43.671049 |-79.386789 | estaciones_de_metro | 
 
 

