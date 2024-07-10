# Complementos 
 Estas funciones amplían las capacidades descritas en Base y sirven para mejorar la exhaustividad de un conjunto de datos GTFS para brindar una mejor experiencia a los usuarios o facilitar la colaboración entre agencias, proveedores de datos y reutilizadores de datos. Estas mejoras pueden implicar la introducción de nuevos campos dentro de los archivos descritos en Base o la creación de nuevos archivos. 
 
## Información del Feed 
 
 Información del Feed comunica información importante sobre el feed, como su validez ( date de inicio y finalización), la organización editorial y la información de contacto para consultas sobre el conjunto de datos GTFS y las prácticas de publicación de datos. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`, `feed_publisher_url`, `feed_lang`, `default_lang`, `feed_start_date`, `feed_end_date`, `feed_version`, `feed_contact_email`, `feed_contact_url` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 

 | feed_publisher_name | feed_publisher_url | feed_lang | default_lang | feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |--------------------|----------------------|-----------|--------------|-----------------|---------------|--------------|--------------------|------------------------------| 
 | Transporte de la Gran Región | https://www.gra1.org | es | es | 20240101 | 20241231 | 3.1 | soporte@gra1.org | https://www.gra1.org/support | 
 
## Shapes 
 Las Shapes se pueden definir y asociar con viajes, lo que permite que las aplicaciones de planificación de viajes muestren los viajes en un mapa e informen a los pasajeros de la distancia que deben recorrer en un vehicle de tránsito. Los campos `shape_dist_traveled se utilizan para determinar mediante programación qué cantidad de shape dibujar al mostrar un mapa a los pasajeros. 
 Al definir Shapes, existe un equilibrio entre su nivel de detalle (por ejemplo, seguir la curvatura exacta de las carreteras) y transmitir sólo la información necesaria de manera eficiente. 
 
 |Archivos incluidos |Campos incluidos | 
 |----------------------------------|-------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`, `shape_pt_lat, `shape_pt_lon, `shape_pt_sequence, `shape_dist_traveled| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled`| 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra una parte de una shape del feed TriMet GTFS (descárguelo <a     href="https://developer.trimet.org/GTFS.shtml">aquí</a> ).<br><br> 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 

 | shape_id | shape_pt_lat | shape_pt_lon | shape_pt_sequence | shape_dist_traveled | 
 |---------|-------------|-------------|------------------|-------------------| 
 | 558674 | 45.47623 |-122.721885 | 1 | 0.0 | 
 | 558674 | 45.476235 |-122.72236 | 2 | 121,9 | 
 | 558674 | 45.476237 |-122.722523 | 3 | 163,7 | 
 | 558674 | 45.476242 |-122.723024 | 4 | 292,2 | 
 | 558674 | 45.476244 |-122.72316 | 5 | 327,1 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 

 | trip_id | shape_id| 
 |--------|--------| 
 |13302375|558674 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 

 | trip_id | stop_sequence| shape_dist_traveled| 
 |--------|-------------|-------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## Colores de Ruta 
 
 El uso de Colores de Ruta permite representar y comunicar con precisión el esquema de colores asignado a routes específicas según las pautas de diseño de la agencia. Esto permite a los usuarios identificar fácilmente los servicios de tránsito por su color oficial. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`, `route_text_color` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra que la ruta "RA" es naranja usando un código de color HEX "D95700", y que el texto debe representarse en negro usando un código de color HEX "0". 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

 | route_id | agency_id | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |----------|-----------|------------------|--------------------|------------|-------------|------------------| 
 | RA | agencia001 | 17 | Misión- Centro | 3 | D95700 | 0 | 
 
## Bicicleta Permitida 
 
 Bicicleta Permitida indica si los vehículos que sirven viajes específicos pueden acomodar bicicletas o no, ayudando a los usuarios a planificar y acceder a servicios que les permitan realizar viajes multimodales. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo especifica que el vehicle utilizado en el viaje `AWE1` puede llevar al menos una bicicleta a bordo (`bikes_allowed=1`), y el vehicle utilizado en el viaje `AWE2` no puede (`bikes_allowed=2`). 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|------------|---------|---------------| 
 | RA | NOSOTROS | AWE1 | 1 | 
 | RA | NOSOTROS | AWE2 | 2 | 
 
## Cartel de destino 
 
 Cartel de destino permite comunicar la señalización utilizada por los vehículos indicando el destino del viaje, facilitando a los usuarios identificar el servicio de tránsito correcto. Esta característica admite cambios de señales a lo largo de una ruta específica. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **Requisito previo**: 
 
 - [Características Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 En el siguiente ejemplo, la primera tabla especifica las señales de cabeza que utilizarán los viajes `AWE1` y `AWE2`, y la segunda indica que la señal de cabeza de `AWE1` se modificará después de la parada `TAS004`, anulando la especificado en `trips.txt`. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

 | route_id | service_id | trip_id | trip_headsign | 
 |----------|------------|---------|---------------| 
 | RA | NOSOTROS | AWE1 | Centro | 
 | RA | NOSOTROS | AWE2 | Misión | 
 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | stop_headsign | 
 |---------|--------------|----------------|---------|---------------|------------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | Centro- Plaza Principal | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | Centro- Plaza Principal | 
 
## Tipos de ubicación 
 
 Los Tipos de ubicación se utilizan para clasificar áreas clave dentro de las estaciones de tránsito, como salidas/entradas, nodos o áreas de embarque, así como su relación. Los Tipos de ubicación sirven como base para modelar estaciones de tránsito utilizando Recorridos. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra múltiples ubicaciones dentro de una estación de tránsito en `stops.txt`: la estación principal, que representa la ubicación principal, y sus ubicaciones secundarias, como andenes, entradas/existencias y nodos genéricos. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

 | stop_id | stop_name | location_type | parent_station | 
 |--------------|-------------------------------------------------------|---------------|----------------| 
 | Estación_A102 | Estación de la calle principal | 1 | | 
 | A102_B01 | Estación Main Street- Plataforma Norte | 0 | Estación_A102 | 
 | A102_B02 | Estación Main Street- Andén Sur | 0 | Estación_A102 | 
 | A102_E01 | Estación Main Street- Entrada/Salida | 2 | Estación_A102 | 
 | A102_S01 | Estación de Main Street- Parte superior de las escaleras de entrada | 3 | Estación_A102 | 
 | A102_S02 | Estación de Main Street- Parte inferior de las escaleras de entrada | 3 | Estación_A102 | 
 | A102_S03 | Estación de Main Street- Parte superior de las escaleras de la plataforma norte | 3 | Estación_A102 | 
 | A102_S04 | Estación de Main Street- Parte inferior de las escaleras de la plataforma norte | 3 | Estación_A102 | 
 | A102_S05 | Estación de Main Street- Parte superior de las escaleras del andén sur | 3 | Estación_A102 | 
 | A102_S06 | Estación de Main Street- Parte inferior de las escaleras del andén sur | 3 | Estación_A102 | 
 | A102_F01 | Estación de Main Street: lado de pago de la puerta de entrada | 3 | Estación_A102 | 
 | A102_F02 | Estación de Main Street: lado no pagado de la puerta de entrada | 3 | Estación_A102 | 
 
## Servicio basado en frecuencia 
 
 El servicio basado en frecuencia se puede utilizar para modelar servicios que operan en una frecuencia regular, como autobuses que circulan cada 10 minutos o servicios de metro que operan 2 minutos dentro de intervalos de tiempo específicos. 
 Al modelar un servicio basado en frecuencia, `stop_times.txt` contiene los tiempos relativos entre stops para determinar los tiempos que se mostrarán a los pasajeros. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| `trip_id`, `start_time`, `end_time, `headway_secs`, `exact_times` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra dos viajes distintos: el viaje `AWE1` que se ejecuta cada 30 min (`headway_secs=1800`) y el viaje `AWE2` que se ejecuta cada 15 min (`headway_secs=900`). 
<p style="font-size:16px"> 
 El campo `exact_times` indica si el horario sigue la hora de inicio precisa ingresada en el campo ’ start_time’: 
 - El viaje `AWE1` sale cada 30 minutos de 6:10 am a 12:00 pm. 
 - el viaje `AW2` sale a las 6:00 a.m., 6:15 a.m., 6:30 a.m., etc. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 

 | trip_id | start_time | end_time | headway_secs | exact_times | 
 ---------|------------|----------|--------------|-------------| 
 AWE1 | 6:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 6:00:00 | 19:50:00 | 900 | 1 | 
 
## Transferencias 
 
 Las Transferencias brindan detalles sobre las transiciones entre diferentes segmentos (o tramos) de viaje, lo que permite a los planificadores de viajes determinar la viabilidad de los viajes que incluyen transfers. Especificar transfers no implica que los pasajeros no puedan realizar transbordos a otro lugar, solo muestra si ciertos transfers no son posibles o require un tiempo mínimo para realizar transbordos. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, `from_trip_id`, `to_trip_id`, `transfer_type`, `min_transfer_time` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra tres transfers diferentes: uno entre stops que requiere un tiempo mínimo de transbordo de 5 minutos, un punto de transbordo cronometrado entre dos routes y un transbordo en asiento entre dos viajes realizados por el mismo vehicle. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 

 | from_stop_id | to_stop_id | from_route_id | to_route_id | from_trip_id | to_trip_id | transfer_type | min_transfer_time | 
 |--------------|------------|---------------|-------------|--------------|------------|---------------|-------------------| 
 | T6 | T7 | | | | | 2 | 300 | 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## Traducciones 
 
 Traducciones permite que la información del servicio, como los nombres de las estaciones, se proporcione en varios idiomas, lo que permite a los planificadores de viajes mostrar la información en un idioma específico según el idioma del usuario y la configuración de ubicación. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`idioma`,`traducción`,`record_id`,`record_sub_id`,`field_value` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra traducciones al francés y al español proporcionadas para dos campos utilizados en `routes.txt:`route_long_name y`route_desc. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 

 | table_name | field_name | idioma | traducción | record_id | record_sub_id | field_value | 
 |------------|-----------------|----------|-------------------------------------------------------|-----------|---------------|-------------| 
 | routes | route_long_name | ES | Misión- Centro | RA | | | 
 | routes | route_long_name | FR | Misión- Centre ville | RA | | | 
 | routes | route_desc | ES | La ruta "A" viaja desde Lower Mission hasta el centro | RA | | | 
 | routes | route_desc | FR | La ruta «A» llega hasta Lower Mission en el centro de la ciudad. | RA | | | 
 
## Atribuciones 
 
 Atribuciones permite compartir detalles adicionales sobre las organizaciones involucradas en la creación del conjunto de datos (productores, operadores y/o autoridades, etc.). 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`, `agency_id`, `route_id`, `trip_id`, `organization_name`, `is_producer`, `is_operator`, `is_authority`, `attribution_url`, `attribution_email`, `attribution_phone` | 
 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 

 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |----------------|-----------|----------|-----------------|--------------------|-------------|-------------|--------------|----------------------------|-------------------------|-------------------| 
 | op01 | tuberculosis | | | Autobús de tránsito | | 1 | | https://www.transitbus.org/fares | contacto@transitbus.org | (777) 555-7777 | 
 | au01 | gra | | | Transporte de la Gran Región | 1 | | 1 | https://www.gra1.org | contact@gra1.org | (555) 555-5555 | 
 | op02 | | rtd023 | | Empresa de autobuses A | | 1 | | https://www.buscompanya.com | contacto@buscompanya.com | (333) 333-3333 | 
 | op03 | | rtd025 | | Empresa de autobuses B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

