# Funciones del GTFS Schedule 
 
 A medida que el formato de referencia GTFS evoluciona para satisfacer las necesidades actuales de los sistemas de tránsito, sus funciones pueden volverse cada vez más complejas. Las **Características GTFS ** tienen como objetivo proporcionar una explicación clara y definitiva de las funcionalidades habilitadas por el formato de referencia GTFS. Esto ayuda a las agencias de tránsito, proveedores, consumidores e investigadores a comprender las capacidades de GTFS y responder la pregunta: **¿Qué puedo hacer con GTFS?** 
 
 Los siguientes grupos de funciones explican el propósito de cada función, así como el archivos y campos asociados con ellos, lo que ayuda a los usuarios a comprender qué datos se necesitan para respaldar una característica específica. 
 
## Base 
 Estas características esenciales forman el núcleo de un feed GTFS. Son los elementos mínimos necesarios para representar un servicio de tránsito. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 Comunicar detalles sobre las agencias responsables del servicio de tránsito. 
 
 [:octicons-arrow-right-24: Más información](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Paradas__ 
 
 Definir los lugares donde un servicio de tránsito recoge y deja pasajeros. 
 
 [:octicons-arrow-right-24: Más información](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Rutas__ 
 
 Definir los elementos de una ruta de tránsito como el nombre y el tipo de servicio. 
 
 [:octicons-arrow-right-24: Más información](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __Fechas de servicio__ 
 
 Crear la estructura para programar viajes y exenciones de servicios. 
 
 [:octicons-arrow-right-24: Más información](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Viajes__ 
 § § Representar vehículos de tránsito que viajan a lo largo de una ruta definida en horarios programados. 
 
 [:octicons-arrow-right-24: Más información](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Horarios de parada__ 
 
 Definir los horarios de arrival y departure de cada viaje para cada parada. 
 
 [:octicons-arrow-right-24: Más información](../base/#stop-times) 
 
</div> 
 
## Complementos 
 Estas características mejoran un conjunto de datos GTFS, mejorando la experiencia del usuario y facilitando la colaboración entre agencias, proveedores y reutilizadores de datos. Pueden implicar agregar nuevos campos a archivos existentes o crear archivos nuevos. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Feed Information__ 
 
 Comunicar información importante sobre el feed en sí. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ § § 
 Definir el recorrido geográfico que sigue un vehicle a lo largo de un viaje. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __Colores de ruta__ 
 
 Representar y comunicar con precisión el esquema de color asignado a routes específicas. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __Se permiten bicicletas__ 
 
 Comunicar si los vehículos tienen capacidad para bicicletas o no. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 Comunicar la señalización utilizada por los vehículos indicando el destino del viaje. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __Tipos de ubicación__ 
 
 Clasificar áreas clave dentro de las estaciones de tránsito, como entradas y salidas. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frecuencias__ § § 
 Representan servicios que operan en una frecuencia regular o en intervalos específicos. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __Traslados__ 
 
 Describa los transfers permitidos entre diferentes servicios de tránsito. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Traducciones__ 
 § § Comunicar información de servicio en múltiples idiomas. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Atribuciones__ 
 § § Comunicar quién participó en la creación del conjunto de datos. 
 
 [:octicons-arrow-right-24: Más información](../base_add-ons/# attributions) 
 
</div> 
 
 
## Accesibilidad 
 Las funciones de Accesibilidad brindan información esencial para que las personas con discapacidades accedan al servicio. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Paradas de accesibilidad para sillas de ruedas__ 
 
 Indique si es posible el embarque en silla de ruedas desde un lugar. 
 
 [:octicons-arrow-right-24: Más información](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Trips Wheelchair Accesibilidad__ 
 
 Indique si un vehicle puede acomodar pasajeros en sillas de ruedas. 
 
 [:octicons-arrow-right-24: Más información](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Text- to-Speech__ 
 
 Proporciona las entradas necesarias para convertir el texto de los nombres de las paradas en audio. 
 
 [:octicons-arrow-right-24: Más información](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Tarifas 
 GTFS puede modelar varias estructuras de tarifas, como tarifas basadas en zona, distancia o hora del día. Informa a los pasajeros sobre los precios de los viajes y los métodos de pago. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Productos Tarifarios__ 
 
 Definir la lista de boletos o tipos de tarifas disponibles para los usuarios. 
 
 [:octicons-arrow-right-24: Más información](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ 
 
 Definir los medios que pueden ser utilizados para retener y/o validar un producto tarifario. 
 
 [:octicons-arrow-right-24: Más información](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __Tarifas basadas en ruta__ 
 
 Describir las reglas utilizadas para aplicar diferentes tarifas para grupos específicos de routes. 
 
 [:octicons-arrow-right-24: Más información](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Time- Tarifas basadas__ 
 
 Describir tarifas diferenciadas por hora del día o día de la semana. 
 
 [:octicons-arrow-right-24: Más información](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone- Tarifas basadas__ 
 
 Describe las tarifas diferenciadas al viajar de un área a otra. 
 
 [:octicons-arrow-right-24: Más información](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Tarifas Transferencias__ 
 
 Definir las tarifas aplicables al transbordo de un tramo del viaje a otro. 
 
 [:octicons-arrow-right-24: Más información](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 Función heredada que permite una representación más sencilla de la información de tarifas. 
 
 [:octicons-arrow-right-24: Más información](../fares/#fares-v1) 
 
</div> 
 
 
## Recorridos 
 
 Las características de los Recorridos permiten modelar grandes estaciones de tránsito, de modo que los pasajeros sean guiados desde las entradas hasta las áreas de embarque. Proporcionan detalles de la ruta, tiempos de navegación estimados y sistemas de orientación. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Conexiones de rutas__ 
 
 Modelo de rutas que conectan puntos relevantes dentro de una estación de tránsito. 
 
 [:octicons-arrow-right-24: Más información](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __Detalles de la ruta__ 
 
 Proporcionar detalles adicionales sobre las características físicas de una vía. 
 
 [:octicons-arrow-right-24: Más información](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Niveles__ 
 § § Describir y enumerar todos los diferentes niveles dentro de una estación de tránsito. 
 
 [:octicons-arrow-right-24: Más información](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __Tiempo de recorrido en la estación__ § § 
 Comunicar el tiempo estimado para recorrer trayectos dentro de una estación de tránsito. 
 
 [:octicons-arrow-right-24: Más información](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __Señales de vía__ 
 
 Comunicar la señalización en la estación asociada con una vía. 
 
 [:octicons-arrow-right-24: Más información](../pathways/#pathway-signs) 
 
</div> 
 
## Servicios flexibles 
 Servicios flexibles, o servicios que responden a la demanda, que no siguen horarios regulares ni routes fijas. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Paradas continuas__ 
 
 Indicar si un usuario puede ser recogido y/o dejado entre stops. 
 
 [:octicons-arrow-right-24: Más información](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __Reglas de reserva__ 
 
 Indique si los usuarios pueden reservar un viaje en un servicio que responda a la demanda. 
 
 [:octicons-arrow-right-24: Más información](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } Rutas predefinidas con desviación__ 
 
 Vehículos que pueden desviarse brevemente de una ruta para recoger o dejar. 
 
 [:octicons-arrow-right-24: Más información](../flexible_services/#rutas-predefinidas-con-desviación) 
 
 - :material-subway-variant:{ .lg.middle } __Servicios de respuesta a la demanda basados ​​en zonas__ 
 
 Servicios que permiten recoger/dejar en cualquier lugar dentro de un área específica. 
 
 [:octicons-arrow-right-24: Más información](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.medio } __Servicios de respuesta a la demanda de paradas fijas__ 
 
 Servicios que permiten recoger/dejar en cualquier ubicación dentro de un grupo de stops. 
 
 [:octicons-arrow-right-24: Más información](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

