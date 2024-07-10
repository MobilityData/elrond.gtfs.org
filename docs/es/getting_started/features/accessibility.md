# Accesibilidad 
 Las funciones de Accesibilidad están destinadas a proporcionar a las personas con discapacidad la información que necesitan para acceder al servicio. 
 
## Paradas Accesibilidad para sillas de ruedas 
 
 Paradas Accesibilidad para sillas de ruedas permite indicar si es posible el embarque para sillas de ruedas desde la ubicación especificada. Para atender a los pasajeros que utilizan sillas de ruedas, especificar que el embarque en silla de ruedas es posible es tan importante como especificar que no lo es. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 - [Tipos de ubicación](../base_add-ons/#location-types) al definir la información de accesibilidad para ubicaciones de las estaciones, como entradas/salidas o áreas de embarque. 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra que el embarque para sillas de ruedas está disponible en la parada `TAS001` usando `wheelchair_boarding=1`. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

 | stop_id | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|-----------|------------|---------------|---------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 | | 1 | 
 
 
## Viajes Accesibilidad para sillas de ruedas 
 
 Viajes Accesibilidad para sillas de ruedas permiten indicar si un vehicle puede acomodar pasajeros que usan sillas de ruedas. Para atender a los pasajeros que usan sillas de ruedas, especificar que un vehicle puede acomodar a los pasajeros que usan sillas de ruedas es tan importante como especificar que un vehicle no puede. Tanto la parada como el viaje deben ser accesibles para sillas de ruedas para que un pasajero pueda acceder a un viaje en la parada determinada. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible`| 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo muestra que el vehicle utilizado en el viaje `AWE1` está equipado para acomodar al menos una silla de ruedas, y el vehicle utilizado en el viaje `AWE2` no. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 

 | route_id | service_id | trip_id | wheelchair_accessible | 
 |----------|------------|---------|-----------------------| 
 | RA | NOSOTROS | AWE1 | 1 | 
 | RA | NOSOTROS | AWE2 | 2 | 
 
 
## Texto a Voz 
 
 Texto a Voz permite proporcionar las entradas necesarias para convertir texto en audio y garantiza que los usuarios que utilizan tecnología de asistencia para leer texto en voz alta obtengan los nombres de paradas correctos.al utilizar el servicio de tránsito. 

 | Archivos incluidos | Campos incluidos | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **Requisitos previos**: 
 
 - [Funciones Base](../base) 
 
 ??? nota "Datos de muestra" 
 
<p style="font-size:16px"> 
 El siguiente ejemplo proporciona una versión legible del nombre de la parada, lo que permite que las herramientas de conversión de texto a voz lean el nombre en voz alta. 
</p> 
 !!! nota "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 

 | stop_id | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|------------|----------------------|------------|--------------------------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 | 5ta avenida y calle 53 | 
 

