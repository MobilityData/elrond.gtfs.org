# Base-Add-ons 
 Diese Funktionen erweitern die in Base beschriebenen Möglichkeiten und dienen entweder dazu, die Vollständigkeit eines GTFS Datensatzes zu erhöhen, um Fahrgästen ein besseres Erlebnis zu bieten, oder die Zusammenarbeit zwischen Agenturen, Datenanbietern und Datenwiederverwendern zu erleichtern. Diese Verbesserungen können die Einführung neuer Felder in die in Base beschriebenen Dateien oder die Erstellung neuer Dateien beinhalten. 
 
## Feed-Informationen 
 
 Feed-Informationen enthalten wichtige Angaben zum Feed, beispielsweise seine Gültigkeit (Start- und date), die veröffentlichende Organisation und Kontaktinformationen für Anfragen zum GTFS Datensatz und zu Datenveröffentlichungspraktiken. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`, `feed_publisher_url`, `feed_lang`, `default_lang`, `feed_start_date`, `feed_end_date`, `feed_version`, `feed_contact_email`, `feed_contact_url` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 
 
 | Feed- feed_publisher_name-Name | Feed-Publisher-URL | Feed-Sprache | default_lang | feed_lang- feed_start_date | Feed- feed_publisher_url | Feed- feed_version | Feed- feed_contact_email | feed_end_date feed_contact_url-URL | 
 |--------------------------|-----------|-----------|--------------|-----|-----------|--------------|-----------------|---------------|--------------|--------------------|---------------| 
 | Transport im Großraum | https://www.gra1.org | en | en | 20240101 | 20241231 | 3.1 | support@gra1.org | https://www.gra1.org/support | 
 
## Formen 
 Formen können definiert und Fahrten zugeordnet werden, sodass Fahrtplanungsanwendungen Fahrten auf einer Karte anzeigen und Fahrgäste über die Entfernung informieren können, die sie mit einem vehicle zurücklegen müssen. Die Felder „shape_dist_traveled“ werden verwendet, um programmgesteuert zu bestimmen, wie viel von einer shape gezeichnet werden soll, wenn Fahrern eine Karte angezeigt wird. 
 Beim Definieren von Formen muss ein Gleichgewicht zwischen ihrem Detaillierungsgrad (z. B. der exakten Krümmung von Straßen folgen) und der effizienten Übermittlung nur der notwendigsten Informationen gefunden werden. 
 
 |Enthaltene Dateien |Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | „`shape_id`“, „shape_pt_lat“, „shape_pt_lon“, „shape_pt_sequence“, „shape_dist_traveled“ | 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled`| 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt einen Ausschnitt einer shape aus dem TriMet GTFS Feed ( <a     href="https://developer.trimet.org/GTFS.shtml">hier</a> herunterladen).<br><br> 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 
 
 | shape_id-ID | Shape- shape_pt_lat | Shape- shape_pt_lon | Shape-Punktfolge | shape_pt_sequence shape_dist_traveled | 
 |---------|-------------|-------------|------------------|-------------------| 
 | 558674 | 45,47623 |-122,721885 | 1 | 0,0 | 
 | 558674 | 45,476235 |-122,72236 | 2 | 121,9 | 
 | 558674 | 45,476237 |-122,722523 | 3 | 163,7 | 
 | 558674 | 45,476242 |-122,723024 | 4 | 292,2 | 
 | 558674 | 45,476244 |-122,72316 | 5 | 327,1 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 
 
 | trip_id | shape_id| 
 |--------|--------| 
 |13302375|558674 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 
 
 | trip_id | stop_sequence| shape_dist_traveled| 
 |--------|----------|-------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461.7 | 
 |13302375|3 |1245 | 
 
## Routenfarben 
 
 Die Verwendung von Routenfarben ermöglicht die genaue Darstellung und Kommunikation des Farbschemas, das bestimmten routes durch die Designrichtlinien der Agentur zugewiesen wurde. Auf diese Weise können Benutzer Verkehrsmittel einfach anhand ihrer offiziellen Farbe identifizieren. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`, `route_text_color` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt, dass die Route „RA“ mit dem HEX-Farbcode „D95700“ orange ist und dass Text mit dem HEX-Farbcode „0“ schwarz dargestellt werden sollte. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id-ID | agency_id-ID | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |----------|-----------|------------------|------------|----------|------------------| 
 | RA | Agentur001 | 17 | Mission – Innenstadt | 3 | D95700 | 0 | 
 
## Fahrrad erlaubt 
 
 Fahrrad erlaubt gibt an, ob Fahrzeuge für bestimmte Fahrten Fahrräder mitnehmen können oder nicht, und hilft Benutzern dabei, Dienste zu planen und darauf zuzugreifen, die ihnen multimodale Fahrten ermöglichen. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel gibt an, dass das vehicle der Fahrt „AWE1“ mindestens ein Fahrrad mitnehmen kann (`bikes_allowed=1`), das vehicle der Fahrt „AWE2“ jedoch nicht (`bikes_allowed=2`). 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|------------|---------|-----------| 
 | RA | WE | AWE1 | 1 | 
 | RA | WE | AWE2 | 2 | 
 
## Kopfschilder 
 
 Kopfschilder ermöglichen die Mitteilung der von Fahrzeugen verwendeten Beschilderung, die das Ziel der Fahrt anzeigt, und erleichtern so den Benutzern die Identifizierung des richtigen Verkehrsmittels. Diese Funktion unterstützt Kopfschildänderungen entlang einer bestimmten Route. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **Voraussetzung**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Im folgenden Beispiel gibt die erste Tabelle die von den Fahrten „AWE1“ und „AWE2“ zu verwendenden Zielschilder an, und die zweite gibt an, dass das Zielschild von „AWE1“ nach der Haltestelle „TAS004“ geändert wird und das in „trips.txt“ angegebene überschrieben wird. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id- service_id | Service-ID | trip_id-ID | Fahrt- trip_headsign | 
 |----------|------------|---------|-----------| 
 | RA | WE | AWE1 | Innenstadt | 
 | RA | WE | AWE2 | Mission | 
 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_headsign | 
 |---------|-----------|----------------|---------|---------------|------------------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | Innenstadt – Hauptplatz | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | Innenstadt – Hauptplatz | 
 
## Standorttypen 
 
 Standorttypen werden verwendet, um wichtige Bereiche innerhalb von Transitstationen wie Ausgänge/Eingänge, Knotenpunkte oder Einstiegsbereiche sowie deren Beziehung zueinander zu klassifizieren. Standorttypen dienen als Grundlage für die Modellierung von Transitstationen mithilfe von Pfaden. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis "Beispieldaten" 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt mehrere Standorte innerhalb einer Haltestelle in „`stops.txt`“: die übergeordnete Haltestelle, die den Hauptstandort darstellt, und ihre untergeordneten Standorte wie Bahnsteige, Ein-/Ausgänge und allgemeine Knoten. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id-ID | stop_name | location_type | parent_station | 
 |--------------|----------------------------------------------------------|---------------|----------------| 
 | Station_A102 | Main Street-Station | 1 | | 
 | A102_B01 | Main Street-Station – Nordbahnsteig | 0 | Station_A102 | 
 | A102_B02 | Main Street-Station – Südbahnsteig | 0 | Station_A102 | 
 | A102_E01 | Main Street-Station – Eingang/Ausgang | 2 | Station_A102 | 
 | A102_S01 | Main Street-Station – Oberes Ende der Eingangstreppe | 3 | Station_A102 | 
 | A102_S02 | Main Street-Station – Unteres Ende der Eingangstreppe | 3 | Station_A102 | 
 | A102_S03 | Station Main Street – Oberes Ende der Treppe zum nördlichen Bahnsteig | 3 | Station_A102 | 
 | A102_S04 | Station Main Street – Unteres Ende der Treppe zum nördlichen Bahnsteig | 3 | Station_A102 | 
 | A102_S05 | Station Main Street – Oberes Ende der Treppe zum südlichen Bahnsteig | 3 | Station_A102 | 
 | A102_S06 | Station Main Street – Unteres Ende der Treppe zum südlichen Bahnsteig | 3 | Station_A102 | 
 | A102_F01 | Station Main Street – Bezahlte Seite des Fahrkartenschranks | 3 | Station_A102 | 
 | A102_F02 | Station Main Street – Unbezahlte Seite des Fahrkartenschranks | 3 | Station_A102 | 
 
## Frequenzbasierter Service 
 
 Der frequenzbasierte Service kann verwendet werden, um Services zu modellieren, die in regelmäßigen Abständen verkehren, wie z. B. Busse, die alle 10 Minuten fahren, oder U-Bahnen, die in festgelegten Zeitintervallen alle 2 Minuten verkehren. 
 Beim Modellieren eines frequenzbasierten Services enthält „`stop_times.txt`“ die relativen Zeiten zwischen den stops, um die den Fahrgästen anzuzeigenden Zeiten zu bestimmen. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| „`trip_id`“, „`start_time`“, „end_time“, „`headway_secs`“, „`exact_times` “ | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt zwei unterschiedliche Fahrten: Fahrt „AWE1“, die alle 30 Minuten stattfindet (`headway_secs=1800`) und Fahrt „AWE2“, die alle 15 Minuten stattfindet (`headway_secs=900`). 
<p style="font-size:16px"> 
 Das Feld „`exact_times`“ gibt an, ob der Fahrplan der genauen Startzeit entspricht, die im Feld „start_time“ eingegeben wurde: 
 - Fahrt „AWE1“ fährt alle 30 Minuten von 6:10 bis 12:00 Uhr ab. 
 - Fahrt „AW2“ fährt um 6:00 Uhr, 6:15 Uhr, 6:30 Uhr usw.ab. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 
 
 | trip_id | start_time | end_time | headway_secs. | exact_times Zeit | 
 ---------|------------|----------|--------------|-------------| 
 AWE1 | 6:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 6:00:00 | 19:50:00 | 900 | 1 | 
 
## Umstiege 
 
 Umstiege liefern Details zu Übergängen zwischen unterschiedlichen Reiseabschnitten (oder Etappen) und ermöglichen Reiseplanern, die Durchführbarkeit von Reisen mit transfers zu ermitteln. Die Angabe von transfers bedeutet nicht, dass Passagiere t woanders umsteigen können, es zeigt nur, ob bestimmte transfers nicht möglich sind oder eine Mindestumstiegszeit require. 
 
 | Eingeschlossene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, `from_trip_id`, `to_trip_id`, `transfer_type`, `min_transfer_time` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt drei verschiedene transfers: einen zwischen stops, der eine Mindestumsteigezeit von 5 Minuten erfordert, einen zeitgesteuerten Umsteigepunkt zwischen zwei routes und einen Umstieg im Sitz zwischen zwei Fahrten mit demselben vehicle. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 
 
 | Von-from_stop_id- to_stop_id | from_route_id- Haltestellen-ID | Von-Routen-ID | Nach- from_trip_id | Von-Fahrt-ID | Nach- to_trip_id-ID | transfer_type | min_transfer_time | 
 |--------------|------------|-----------|-------------|-----------|-------------|------------|-----------|-------------------| 
 | s6 | s7 | | | | | 2 | 300 | 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## Übersetzungen 
 
 Durch Übersetzungen können Serviceinformationen wie Bahnhofsnamen in mehreren Sprachen bereitgestellt werden, sodass Reiseplaner die Informationen je nach Sprach- und Standorteinstellungen des Benutzers in einer bestimmten Sprache anzeigen können. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`language`,`translation`,`record_id`,`record_sub_id`,`field_value` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis "Beispieldaten" 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt französische und spanische Übersetzungen für zwei in „routes.txt“ verwendete Felder: „route_long_name“ und „route_desc“. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 
 
 | table_name | field_name | Sprache | Übersetzung | record_id | record_sub_id-Unter-ID | field_value | 
 |------------|-----------------|----------|-------------------------------------------------------|-----------|---------------|---------------|-------------| 
 | routes | langer route_long_name | ES | Mission – Zentrum | RA | | | 
 | routes | route_long_name | FR | Mission – Stadtzentrum | RA | | | 
 | routes | route_desc | ES | Die Route „A“ führt von Lower Mission zum Zentrum | RA | | | 
 | routes | route_desc | FR | Die Route „A“ führt von Lower Mission zum Stadtzentrum. | RA | | | 
 
## Zuschreibungen 
 
 Durch Zuschreibungen können zusätzliche Details zu den an der Erstellung des Datensatzes beteiligten Organisationen (Produzenten, Betreiber und/oder Behörden usw.) weitergegeben werden. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`, `agency_id`, `route_id`, `trip_id`, `organization_name`, `is_producer`, `is_operator`, `is_authority`, `attribution_url`, `attribution_email`, `attribution_phone` | 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 
 
 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |----------------|-----------|----------|---------|---------|----------|-------------|----------|-------------|----------------------------------|-------------------------|-------------------| 
 | op01 | tb | | | Transit Bus | | 1 | | https://www.transitbus.org/fares | contact@transitbus.org | (777) 555-7777 | 
 | au01 | gra | | | Greater Region Transport | 1 | | 1 | https://www.gra1.org | contact@gra1.org | (555) 555-5555 | 
 | op02 | | rtd023 | | Busunternehmen A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | op03 | | rtd025 | | Busunternehmen B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

