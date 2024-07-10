# Flexible Dienste 
 Flexible Dienste, auch bedarfsgesteuerte Dienste genannt, sind Dienste, die nicht dem üblichen Verhalten von planmäßigen und/oder festen Diensten folgen. 
 
## Kontinuierliche Haltestellen 
 
 Kontinuierliche Haltestellen werden verwendet, wenn Fahrgäste zwischen planmäßigen stops ein- und/oder aussteigen können. 
 Dies kann entweder in „routes.txt“ angegeben werden, um anzuzeigen, dass Fahrgäste bei jeder Fahrt der Route an jedem Punkt entlang der Fahrtroute des Fahrzeugs ein- oder aussteigen können, oder in „`stop_times.txt`“ für einen bestimmten Abschnitt einer Route. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`continuous_pickup`, `continuous_drop_off` | 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`continuous_pickup`, `continuous_drop_off` | 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt zwei Möglichkeiten zur Darstellung von Continuous Stop. 
</p> 
 
<p style="font-size:16px"> 
 Das erste Beispiel zeigt, dass Abholungen und Absetzen an jedem Punkt entlang der Route „RA“ erlaubt sind. 
</p> 
 
<p style="font-size:16px"> 
 Das zweite Beispiel zeigt, dass zwischen der dritten und fünften stops der Fahrt „AWE1“ das Abholen und Absetzen von Fahrgästen erlaubt ist. Dies wird erreicht, indem den Werten „continuous_pickup“ und „continuous_drop_off“ die Werte „stop_sequence=3“ und „stop_sequence=4“ zugewiesen werden. 
</p> 
 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | Kurzname der route_type | continuous_pickup | continuous_drop_off | 
 |----------|------------------|---------|-------------------|---------------------| 
 | RA | 17 | 3 | 0 | 0 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | kontinuierliche continuous_pickup | continuous_drop_off | 
 |---------|-----------|----------------|---------|-----------|-------------------|---------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | | | 
 
## Buchungsregeln 
 
 Buchungsregeln können verwendet werden, um Benutzern die Reservierung einer Fahrt mit einem Bedarfsservice zu ermöglichen. Diese Regeln legen die notwendigen Voraussetzungen für erfolgreiche Buchungen fest und bieten Kontaktinformationen, unter denen Benutzer Fahrten reservieren können. Diese Funktion sollte in Verbindung mit den Funktionen [Vordefinierte Routen mit Abweichung](#predefined-routes-with-deviation), [Zonenbasierte Bedarfsservices](#zone-based-demand-responsive-services) und [Bedarfsservices mit festen Haltestellen](#fixed-stops-demand-responsive-services) verwendet werden, wenn für solche Dienste eine Buchung require ist. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|------------------| 
 |[booking_rules.txt](../../../documentation/schedule/reference/#booking_rulestxt)|`Buchungsregel-ID`, `Buchungstyp`, `Mindestdauer der Vorbenachrichtigung`, `Maximale Dauer der Vorbenachrichtigung`, `Letzter Tag der Vorbenachrichtigung`, `Letzte Uhrzeit der Vorbenachrichtigung`, `Starttag der Vorbenachrichtigung`, `Startzeit der Vorbenachrichtigung`, `Service-ID der Vorbenachrichtigung`, `message`, `Abholnachricht`, `Abgabenachricht`, `Telefonnummer`, `Info-URL`, `Buchungs-URL` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt zwei verschiedene Sätze von Buchungsregeln, einen ersten für Fahrten, die mindestens einen Tag im Voraus (vor 13 Uhr) und höchstens 14 Tage vorher gebucht werden müssen, und einen zweiten für Fahrten, die mindestens 45 Minuten vor der Fahrt und höchstens 5 Stunden vorher gebucht werden können. 
 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#booking_rulestxt"><b>booking_rules.txt</b></a><br> 
</p> 
 
 | Buchungsregel-ID | Buchungstyp | Vorbenachrichtigungsdauer_min | Vorbenachrichtigungsdauer_max | Vorbenachrichtigungsletzter_Tag | Vorbenachrichtigungsletzter_Zeitpunkt | Vorbenachrichtigungsstarttag | Vorbenachrichtigungsstartzeit | Vorbenachrichtigungsservice-ID | message | Abholnachricht | Abgabenachricht | Telefonnummer | Info-URL | Buchungs-URL | 
 |-----------------|--------------|---------------------------|---------------------------|---------------------------|------------------------|------------------------|-------------------------|-------------------------|-------------------------|-------------------------|-------------------------|---------------------------------------------------------------------------------------------------------------------------------|----------------|------------------|----------------|------------------|----------------|---------------------| 
 | route_br_1818 | 2 | | | 1 | 13:00 | 14 | 9:00 | | Um eine Fahrt anzufordern, rufen Sie mindestens einen Werktag vor Ihrer Fahrt vor 13:00 Uhr die Nummer 123-111-2233 an. Sie können Fahrten bis zu 14 Werktage im Voraus buchen. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 | route_br_4545 | 1 | 45 | 300 | | | | | | Um eine Fahrt anzufordern, verwenden Sie das offizielle Buchungssystem auf unserer Website. Fahrten müssen mindestens 45 Minuten im Voraus gebucht werden. | | | (123)-111-2233 | flexservice.org/info | flexservice.org/booking | 
 
 
## Vordefinierte Routen mit Abweichung 
 
 Vordefinierte Routen mit Abweichung können verwendet werden, um flexible Dienste zu modellieren, bei denen Fahrzeuge kurz von einer bestimmten Route abweichen können, um Benutzer aufzunehmen, die eine Fahrt innerhalb eines bestimmten Gebiets entlang der Route gebucht haben. Dabei wird eine Kombination aus herkömmlichen stops (wie bei einem regulären Liniendienst) und Zonen unter Verwendung von „`locations.geojson`“ verwendet. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`Standort-ID`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Typ`, `Funktionen`, `Funktionen:Typ`, `Funktionen:Id`, `Funktionen:Eigenschaften`, `Funktionen:Eigenschaften:Haltestellenname`, `Funktionen:Eigenschaften:Haltestellenbeschreibung`, `Funktionen:Geometrie`, `Funktionen:Geometrie:Typ`, `Funktionen:Geometrie:Koordinaten` | 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Buchungsregeln](#booking-rules), wenn der Service eine Buchung erfordert 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt eine Fahrt mit drei festen stops, bei der Fahrgäste auch überall innerhalb bestimmter, zwischen den festen stops definierter Bereiche aussteigen können. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | Haltestellen- stop_id | Standort-ID | stop_sequence | start_pickup_drop_off_window und Abgabe | end_pickup_drop_off_window für Abhol- und Abgabe | pickup_type | drop_off_type | shape_dist_traveled der zurückgelegten Entfernung | pickup_booking_rule_id | drop_off_booking_rule_id | 
 |---------|-----------|----------------|---------|--------------------------|--------------------------|--------------------------|--------------------------|--------------------------|--------------------------|--------------------------|--------------------------|--------------------------|--------------------------| 4545_001 | | | | Zone_S50122_bis_S50123 | 2 | 10:00:00 | 10:06:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:06:00 | 10:06:00 | S50123 | | 3 | | | | | 983 | | | 
 | 4545_001 | | | | Zone_S50123_bis_S50124 | 4 | 10:06:00 | 10:15:00 | 1 | 3 | | br_1234 | br_1234 | 
 | 4545_001 | 10:15:00 | 10:15:00 | S50124 | | 5 | | | | | 2109 | | | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "Typ": "FeatureCollection", 
 "Features": [
 { 
 "id": "Zone_S50122_bis_S50123", 
 "Typ": "Feature", 
 "Geometrie": { 
 "Typ": "Polygon", 
# Vereinfacht, hier werden nur 3 Koordinaten dargestellt. 
 "Koordinaten": [
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
 "Eigenschaften": {} 
 }, 
 { 
 "id": "Zone_S50123_bis_S50124", 
 "Typ": "Feature", 
 "Geometrie": { 
 "Typ": "Polygon", 
# Vereinfacht, hier werden nur 3 Koordinaten dargestellt. 
 "Koordinaten": [
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
 "Eigenschaften": {} 
 } 
] 
 } 
 ~~~ 
 
## Zonenbasierte bedarfsgesteuerte Dienste 
 
 Zonenbasierte bedarfsgesteuerte Dienste werden verwendet, um Dienste zu modellieren, die Benutzern, die eine Fahrt buchen, das Abholen und/oder Absetzen an jedem beliebigen Ort innerhalb eines bestimmten Gebiets ermöglichen. Diese Gebiete werden mit `locations.geojson` definiert, sodass weder `stops.txt` noch `stop_times und `stop_times.departure_time` verwendet werden require. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`Standort-ID`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[locations.geojson](../../../documentation/schedule/reference/#locationsgeojson)|`Typ`, `Funktionen`, `Funktionen:Typ`, `Funktionen:Id`, `Funktionen:Eigenschaften`, `Funktionen:Eigenschaften:Haltestellenname`, `Funktionen:Eigenschaften:Haltestellenbeschreibung`, `Funktionen:Geometrie`, `Funktionen:Geometrie:Typ`, `Funktionen:Geometrie:Koordinaten` | 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Buchungsregeln](#booking-rules), wenn der Service eine Buchung erfordert 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt einen Service, der vorab gebuchte Fahrgäste zwischen 9 und 18 Uhr überall in einem bestimmten Gebiet abholen und wieder absetzen kann. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | Standort-ID | stop_sequence | start_pickup_drop_off_window und Abgabe | end_pickup_drop_off_window | pickup_type | drop_off_type | ID der pickup_booking_rule_id | drop_off_booking_rule_id | 
 |---------|----------|---------------|------------------------------|-------------|-------------|-------------|---------------|------------------------|--------------------------| 
 | 2708_001 | Bereich_001 | 1 | 9:00:00 | 18:00:00 | 2 | 1 | br_3289 | br_3289 | 
 | 2708_001 | Bereich_001 | 2 | 9:00:00 | 18:00:00 | 1 | 2 | br_3289 | br_3289 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#locationsgeojson"><b>locations.geojson</b></a><br> 
</p> 
 
 ~~~ 
 { 
 "Typ": "FeatureCollection", 
 "Features": [
 { 
 "id": "Bereich_001", 
 "Typ": "Feature", 
 "Geometrie": { 
 "Typ": "Polygon", 
# Vereinfacht, hier werden nur 3 Koordinaten dargestellt. 
 "Koordinaten": [
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
 "Eigenschaften": {} 
 } 
] 
 } 
 ~~~ 
 
## Feste Haltestellen Bedarfsgesteuerte Dienste 
 Fixed-Stops Demand Responsive Services wird verwendet, um Dienste zu modellieren, die das Abholen und/oder Absetzen an jedem Ort innerhalb einer Gruppe vordefinierter stops für Benutzer ermöglichen, die eine Fahrt buchen. Diese stops werden mit `location_groups.txt` und `location_group_stops.txt` definiert. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`location_group_id`, `start_pickup_drop_off_window`, `end_pickup_drop_off_window`, `pickup_booking_rule_id`, `drop_off_booking_rule_id`| 
 |[location_groups.txt](../../../documentation/schedule/reference/#location_groupstxt)|`location_group_id`, `location_group_name`| 
 |[location_group_stops.txt](../../../documentation/schedule/reference/#location_group_stopstxt)|`location_group_id`, `stop_id`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Buchungsregeln](#booking-rules), wenn der Service eine Buchung erfordert 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt einen Service, der vorab gebuchte Fahrgäste zwischen 7 und 10 Uhr an 4 verschiedenen stops abholen und wieder absetzen kann. 
 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_groupstxt"><b>Standortgruppen.txt</b></a><br> 
</p> 
 
 | Standortgruppen-ID | Standortgruppenname | 
 |-------------------|-------------------------------| 
 | r27_stops | stops der Yellow Borough Route 27 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#location_group_stopstxt"><b>Standortgruppenstopps.txt</b></a><br> 
</p> 
 
 | Standortgruppen-ID | stop_id-ID | 
 |-------------------|---------| 
 | r27_Stopps | syb029 | 
 | r27_Stopps | syb030 | 
 | r27_Stopps | syb031 | 
 | r27_Stopps | syb032 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | Standortgruppen-ID | stop_sequence | start_pickup_drop_off_window und Abgabe | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id-ID | drop_off_booking_rule_id-ID | 
 |----------|-------------------|---------------|------------------------------|-------------|-------------|-------------|---------------|------------------------|--------------------------| 
 | 2714_002 | r27_Haltestellen | 1 | 7:00:00 | 10:00:00 | 2 | 1 | br_5478 | br_5478 | 
 | 2714_002 | r27_Haltestellen | 2 | 7:00:00 | 10:00:00 | 1 | 2 | br_5478 | br_5478 | 
 

