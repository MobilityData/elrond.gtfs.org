# Servicios Flexibles 
 Los servicios flexibles, también llamados servicios de demanda-responsable, son servicios que no siguen el comportamiento común del servicio programado y/o fijo. 
 
## Paradas Continuas 
 
 Paradas Continuas se utiliza cuando se puede recoger y/o dejar a los pasajeros entre stops programadas. 
 Esto se puede especificar en `routes.txt, que indica que los pasajeros pueden ser recogidos o dejados en cualquier punto a lo largo de la ruta del vehículo para cada viaje de la ruta, o en `stop_times.txt` para una sección específica de una ruta. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off` | 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra dos formas de representar la parada continua. 
</p> 
 
<p style="font-size:16px"> 
 El primer ejemplo muestra que se permiten recogidas y devoluciones en cualquier punto a lo largo de la ruta "RA". 
</p> 
 
<p style="font-size:16px"> 
 El segundo ejemplo muestra que se permiten recogidas y devoluciones entre la tercera y la quinta stops del viaje `AWE1, lo que se logra asignando los valores `continuous_pickup y `continuous_drop_off a `stop_sequence=3` y`stop_sequence=4`. 
</p> 
 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

 | route_id | route_short_name | route_type | continuous_pickup | continuous_drop_off | 
 |----------|------------------|------------|-------------------|---------------------| 
 | RA | 17 | 3 | 0 | 0 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | continuous_pickup | continuous_drop_off | 
 |---------|--------------|----------------|---------|---------------|-------------------|-----------------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | | | 
 
## Reglas de reserva 
 
 Las reglas de reserva se pueden utilizar para permitir a los usuarios reservar un viaje en un servicio que responda a la demanda. Estas reglas describen los requisitos previos necesarios para realizar reservas exitosas y brindan información de contacto donde los usuarios pueden hacer reservas de viaje. Esta función debe usarse junto con [Rutas predefinidas con desviación](#rutas-predefinidas-con-desviación), [Servicios de respuesta a la demanda basados ​​en zonas](#servicios-de respuesta a la demanda basados ​​en zonas) y [Servicios Bajo Demanda con Paradas Fijas](#servicios-de-paradas-fijas-servicios-de-respuesta a la demanda), si dichos servicios require reserva. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`booking_rule_id`, `booking_type`, `prior_notice_duration_min`, `prior_notice_duration_max`, `prior_notice_last_day`, `prior_notice_last_time `, `día_inicio_aviso_previo`, `hora_inicio_aviso_prior`, `id_servicio_aviso_prior`, `message`, `mensaje_recogida`, `mensaje_entrega`, `número_teléfono`, `url_información`, `url_reserva` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra dos conjuntos diferentes de reglas de reserva, el primero para viajes que deben reservarse con al menos un día de anticipación (antes de las 13:00 horas) y no más de 14 días antes, y un segundo para viajes que se pueden reservar.al menos 45 minutos antes del viaje y no más de 5 horas antes. 
 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 

 | reserva_rule_id | tipo_reserva | aviso_previo_duración_min | previo_notice_duration_max | aviso_anterior_último_día | aviso_anterior_última_hora | aviso_anterior_día_inicio | aviso_previo_hora_inicio | previo_notice_service_id | message | mensaje_recogida | drop_off_message | número_teléfono | URL_información | URL_reserva | 
 |-----------------|--------------|---------------------------|---------------------|-----------------------|------------------------|---------------------------------|-------------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------|----------|----------------------|-------------------------| 
 | ruta_br_1818 | 2 | | | 1 | 13:00 | 14 | 9:00 | | Para solicitar transporte, llame al 123-111-2233 antes de la 1:00 p.m. al menos un día hábil antes de su viaje. Puede reservar viajes con hasta 14 días hábiles de anticipación. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | ruta_br_4545 | 1 | 45 | 300 | | | | | | Para solicitar un viaje utilice el sistema de reservas oficial en nuestro sitio web, los viajes deben reservarse con al menos 45 min de antelación | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## Rutas predefinidas con desviación 
 
 Las Rutas predefinidas con desviación se pueden utilizar para modelar servicios flexibles en los que los vehículos pueden desviarse brevemente de una ruta específica para recoger a los usuarios que reservaron un viaje dentro de un área específica a lo largo de la ruta.ruta. Esto utiliza una combinación de stops tradicionales (como un servicio regular programado) y zonas que usan `locations.geojson`. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`ubicación_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Tipo`, `Características`, `Características:Tipo`, `Características:Id`, `Características :Propiedades`, `Características:Propiedades:Nombre_detención`, `Características:Propiedades:Descripción_detención`, `Características:Geometría`, `Características:Geometría:Tipo`, `Características:Geometría:Coordenadas` | 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Reglas de reserva](#booking-rules) si el servicio requiere reserva 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra un viaje con tres stops fijas que también puede dejar pasajeros en cualquier lugar dentro de áreas específicas definidas entre las stops fijas. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

 | trip_id | arrival_time | departure_time | stop_id | ID_ubicación | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|--------------|----------------|---------|-----------------------|---------------|------------------------|----------------------------|-------------|---------------|---------------------|------------------------|--------------------------| 
 | 4545_001 | 10:00:00 | 10:00:00 | S50122 | | 1 | | | | | 0 | | | 
 | 4545_001 | | | | zona_S50122_a_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | zona_S50123_a_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "tipo": "FeatureCollection", 
 "características": [
 { 
 "id": "zone_S50122_to_S50123", 
 "tipo": "Característica", 
 "geometría": { 
 "tipo": "Polygon", 
# Simplificado, aquí solo presenta 3 coordenadas. 
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
 "properties": {} 
 }, 
 { 
 "id": "zone_S50123_to_S50124", 
 "type": "Característica", § § "geometría": { 
 "tipo": "Polygon", 
# Simplificado, aquí solo presenta 3 coordenadas. 
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
 "properties": {} 
 } 
] 
 } 
 ~~~ 
 
## Servicios de respuesta a la demanda basados ​​en zonas 
 
 Servicios de respuesta a la demanda basados ​​en zonas se utiliza para modelar servicios que permiten recoger y/o dejar en cualquier ubicación dentro de un área específica para los usuarios que reservan un viaje. Estas áreas se definen usando `locations.geojson`, por lo que no require el uso de `stops.txt` ni `stop_times.arrival_time` &amp; `stop_times.departure_time`. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`ubicación_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Tipo`, `Características`, `Características:Tipo`, `Características:Id`, `Características :Propiedades`, `Características:Propiedades:Nombre_detención`, `Características:Propiedades:Descripción_detención`, `Características:Geometría`, `Características:Geometría:Tipo`, `Características:Geometría:Coordenadas` | 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Reglas de reserva](#booking-rules) si el servicio requiere reserva 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra un servicio que puede recoger y dejar pasajeros con reserva previa en cualquier lugar entre un área específica entre las 9 a.m. y las 6 p.m. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

 | trip_id | ID_ubicación | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2708_001 | área_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | área_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "tipo": "FeatureCollection", 
 "características": [
 { 
 "id": "area_001", 
 "tipo": "Característica", 
 "geometría": { 
 "tipo": "Polygon", 
# Simplificado, aquí solo presenta 3 coordenadas. 
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
 "properties": {} 
 } 
] 
 } 
 ~~~ 
 
## Servicios Bajo Demanda con Paradas Fijas 
 Los Servicios Bajo Demanda con Paradas Fijas se utilizan para modelar servicios que permiten recoger y/o dejar en cualquier ubicación dentro de un grupo de stops predefinidas para los usuarios que reservan un viaje. Estos grupos de stops se definen usando `location_groups.txt` y `location_group_stops.txt`. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`ubicación_grupo_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[grupos_ubicación.txt](../../../documentation/schedule/reference/#ubicación_groupstxt)|`id_grupo_ubicación`, `nombre_grupo_ubicación`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`ubicación_group_id`, `stop_id`| 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Reglas de reserva](#booking-rules) si el servicio requiere reserva 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra un servicio que puede recoger y dejar pasajeros con reserva previa en 4 stops diferentes entre las 7 a.m. y las 10 a.m. 
 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_groupstxt"><b>grupos_ubicación.txt</b></a><br> 
</p> 

 | ubicación_grupo_id | ubicación_nombre_grupo | 
 |-------------------|-------------------------| 
 | r27_paradas | stops de la ruta 27 de Yellow Borough | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>ubicación_grupo_paradas.txt</b></a><br> 
</p> 

 | ubicación_grupo_id | stop_id | 
 |-------------------|---------| 
 | r27_paradas | syb029 | 
 | r27_paradas | syb030 | 
 | r27_paradas | syb031 | 
 | r27_paradas | syb032 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

 | trip_id | ubicación_grupo_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |----------|-------------------|---------------|------------------------------|----------------------------|-------------|---------------|------------------------|--------------------------| 
 | 2714_002 | r27_paradas | 1 | 7:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_paradas | 2 | 7:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

