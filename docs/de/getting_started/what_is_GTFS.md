# GTFS: Daten zum öffentlichen Nahverkehr allgemein zugänglich machen## Ein offener Datenstandard für Fahrgastinformationen 
 
 Die General Transit Feed Specification, auch bekannt als GTFS, ist ein standardisiertes Datenformat, das öffentlichen Nahverkehrsunternehmen eine Struktur bietet, um die Details ihrer Dienstleistungen wie Fahrpläne, stops, Fahrpreise usw.zu beschreiben. 
 
 Es ermöglicht öffentlichen Nahverkehrsunternehmen, ihre Nahverkehrsdaten in einem Format zu veröffentlichen, das von einer großen Bandbreite von Softwareanwendungen genutzt werden kann, am häufigsten von Reiseplanern. Dies bedeutet, dass Benutzer problemlos Reiseinformationen abrufen können, um mit ihrem Smartphone oder ähnlichen Geräten auf Dienstleistungen des öffentlichen Nahverkehrs zuzugreifen. 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 Heute ist GTFS der bevorzugte [offene Standard](https:) für Tausende von öffentlichen Verkehrsbetrieben weltweit. Einige Unternehmen erstellen diese Daten selbst, während andere einen Anbieter damit beauftragen, die Daten für sie zu erstellen und zu pflegen. 
 
## Unterstützung für statische und dynamische Daten 
 
 GTFS besteht aus zwei Hauptteilen: [GTFS Schedule](../../documentation/schedule/reference) und [GTFS Realtime](../../documentation/realtime/reference). 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 Der GTFS Schedule enthält neben vielen anderen Informationen zu routes, Fahrplänen, Fahrpreisen und geografischen Transitdetails und wird in einfachen Textdateien dargestellt[^1]. Dieses unkomplizierte Format ermöglicht eine einfache Erstellung und Wartung ohne Verwendung komplexer oder proprietärer Software. 
 
 GTFS Realtime enthält Fahrtaktualisierungen, vehicle und Servicewarnungen im Format [Protocol Buffers](https:). Dieser Teil von GTFS arbeitet mit dem GTFS Schedule zusammen, um Fahrgäste über Servicestörungen und aktualisierte arrival zu informieren. 
 
 Die Referenzdokumentation zu GTFS Schedule und GTFS Realtime finden Sie im [Abschnitt „Technische Dokumentation“](../../documentation/overview). 
 
 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="YouTube-Videoplayer" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Icons von Freepik">Von Freepik erstellte Icons – Flaticon</a> 
 
 [^1]: Zusätzlich zu Textdateien wird in GTFS jetzt auch das Format [GeoJSON](https://geojson.org/) unterstützt, um bestimmte Elemente von Demand-Responsive-Diensten darzustellen. 
 

