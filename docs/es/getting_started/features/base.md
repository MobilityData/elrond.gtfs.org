# Base 
 Las siguientes características proporcionan los elementos más básicos y esenciales que un GTFS necesita para representar un servicio de tránsito. Un GTFS consta de routes, cada una con viajes asociados. Estos viajes visitan una o más stops en horarios específicos. Los Viajes solo contienen información sobre la hora del día y los días en los que operan están determinados por calendarios. 
 Todas estas funciones deben implementarse juntas para permitir un feed GTFS que funcione. 
 
## Agencia 
 
 Agencias contienen información básica sobre las agencias responsables del servicio de tránsito, como su nombre, URL del sitio web y el idioma y zona horaria en que opera el servicio. Esto permite relacionar servicios específicos con su agency correspondiente. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url`, `agency_email` | 
 
 **Requisitos previos**: 
 
 - Todas las demás funciones de la Base 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 

 | agency_id | agency_name | agency_url | agency_timezone | agency_lang | agency_phone | agency_fare_url | agency_email | 
 |-----------|-------------|----------------------------|---------------------|-------------|----------------|----------------------------------|------------------------| 
 | tuberculosis | Autobús de tránsito | https://www.transitbus.org | America/Los_Angeles | ES | (777) 555-7777 | https://www.transitbus.org/fares | contacto@transitbus.org | 
 
 
 
## Paradas 
 
 Las Paradas representan los elementos básicos utilizados para identificar dónde un servicio de tránsito recoge y deja pasajeros. Podría ser una estación de metro o una parada de autobús. Cada parada tiene, entre otros atributos, coordenadas geográficas para señalar su ubicación en un mapa y un nombre que coincide con los materiales de la agencia orientados a los pasajeros. Las Paradas se asocian a Viajes mediante Horarios de Parada. 
 Con GTFS, también es posible describir el interior de estaciones más grandes, como una estación de tren o una estación de autobuses, usando [Recorridos](/getting_started/features/pathways). 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`, `stop_code`, `stop_name`, `stop_desc`, `stop_lat`, `stop_lon`, `stop_url`, `stop_timezone`, `platform_code` | 
 
 **Requisitos previos**: 
 
 - Todas las demás funciones de la Base 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

 | stop_id | stop_code | stop_desc | stop_name | stop_lat | stop_lon | stop_url | stop_timezone | platform_code | 
 |---------|-----------|--------------------------------------------|------------|-----------|------------|-----------------------------------------|---------------|---------------| 
 | TAS001 | TAS001 | Esquina suroeste de 5 Avenida y 53 Calle | 5 Av/53 St | 45.503568 |-73.587079 | stops| | | 
 
 
## Rutas 
 
 Una ruta es un grupo de viajes bajo la misma marca que se muestran a los pasajeros como un único servicio. Cada ruta tiene, entre otros atributos, un nombre que coincide con los materiales de la agencia orientados al usuario y el tipo de servicio que se representa (como un autobús, un metro o metro, ferry, etc.). 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`, `agency_id`, `route_desc`, `route_type`, `route_url`, `route_sort_order`, `route_short_name`, `route_long_name`| 
 
 **Requisitos previos**: 
 
 - Todas las demás funciones de la Base 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo define una ruta de autobús (`route_type=3`). 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 

 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |----------|-----------|------------------|--------------------|-------------------------------------------------------|------------|--------------------------------------|------------------| 
 | RA | tuberculosis | 17 | Misión- Centro | La ruta "A" viaja desde la parte baja de Mission hasta el centro. | 3 | routes| 12 | 
 
 
## Fechas de servicio 
 
 Fechas de servicio indican el rango de fechas en las que se ejecuta un servicio, además de crear exenciones de servicio como días festivos y otros servicios especiales en fechas específicas. 
 Funciona definiendo una date de inicio y una date de finalización en `calendarios.txt`, luego un marcador para cada día de la semana en el que opera. Si se producen cambios en la programación de un solo día durante este período, entonces se puede utilizar el archivo `calendar_dates.txt` para anular la programación de cada uno de estos días. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **Requisitos previos**: 
 
 - Todas las demás funciones de la Base 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo define dos servicios (entre semana y fin de semana) para el mes de julio de 2024, incluyendo un servicio especial festivo el 4 de julio, operando como servicio de fin de semana. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 

 | service_id | monday | tuesday | wednesday | thursday | friday | saturday | sunday | start_date | end_date | 
 |------------|--------|---------|-----------|----------|--------|----------|----------------|------------|----------| 
 | NOSOTROS | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | WD | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 

 | service_id | date | exception_type | 
 |------------|----------|----------------| 
 | WD | 20240704 | 2 | 
 | NOSOTROS | 20240704 | 1 | 
 
## Viajes 
 
 Viajes reúne Rutas y Fechas de Servicio para crear viajes que puedan realizar los pasajeros. Los Viajes están asociados a Paradas utilizando Horarios de Parada. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **Requisitos previos**: 
 
 - Todas las demás funciones de la Base 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo define dos viajes que se realizan en ambas direcciones para la ruta RA. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |----------|------------|---------|-----------------|--------------|----------| 
 | RA | NOSOTROS | AWE1 | 3885 | 0 | 1 | 
 | RA | NOSOTROS | AWE2 | 3887 | 1 | 2 | 
 
## Horarios de Parada 
 
 Los horarios de parada se utilizan para representar los horarios de arrival y departure de las paradas individuales para cada viaje, lo que permite a los pasajeros saber con precisión a qué hora llega y sale el autobús, tren o ferry de un lugar específico..El archivo `stop_times.txt` suele ser el más grande en un feed GTFS. 
 Ciertos servicios funcionan con una frecuencia regular (por ejemplo, una línea de metro que pasa cada 5 minutos) en lugar de tener horarios específicos de arrival y departure. Esto se puede modelar utilizando [servicios basados ​​en frecuencia](../base_add-ons/#frequency-based-service), y se puede modelar junto con `stop_times.txt`. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`, `arrival_time`, `departure_time`, `stop_id`, `stop_sequence`, `pickup_type`, `drop_off_type`, `timepoint` | 
 
 **Requisitos previos**: 
 
 - Todas las demás funciones de la Base 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo define el horario de un viaje con 5 stops. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 

 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | pickup_type | drop_off_type | timepoint | 
 |---------|--------------|----------------|---------|---------------|-------------|---------------|-----------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 0 | 0 | 1 | 
 

