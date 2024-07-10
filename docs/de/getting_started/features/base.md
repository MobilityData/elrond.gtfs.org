# Basis 
 Die folgenden Funktionen stellen die grundlegendsten und wesentlichsten Elemente bereit, die ein GTFS zur Darstellung eines Verkehrsdienstes benötigt. Ein GTFS besteht aus routes mit jeweils zugehörigen Fahrten. Diese Fahrten führen zu einer oder mehreren stops zu festgelegten Zeiten. Fahrten enthalten nur Informationen zur Tageszeit und die Tage, an denen sie verkehren, sind durch Kalender bestimmt. 
 Alle diese Funktionen müssen zusammen implementiert werden, um einen funktionierenden GTFS Feed zu ermöglichen. 
 
## Agentur 
 
 Agenturen enthalten grundlegende Informationen zu den für den Verkehrsdienst verantwortlichen Agenturen, wie ihren Namen, die Website- URL und die Sprache und Zeitzone, in der der Dienst operiert. Dadurch können bestimmte Dienste den entsprechenden agency zugeordnet werden. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url`, `agency_email` | 
 
 **Voraussetzungen**: 
 
 - Alle anderen Basisfunktionen 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 
 
 | agency_id-ID | agency_name | agency_url-URL | agency_lang- agency_timezone | Agentur-Sprache | agency_fare_url- agency_phone | Agentur-Tarif-URL | Agentur-E- agency_email | 
 |-----------|-------------|-------------|---------------------|-------------|----------------|----------------------------------|------------------------| 
 | tb | Transit Bus | https://www.transitbus.org | America/Los_Angeles | EN | (777) 555-7777 | https://www.transitbus.org/fares | contact@transitbus.org | 
 
 
 
## Haltestellen 
 
 Haltestellen stellen die grundlegenden Elemente dar, die verwendet werden, um zu identifizieren, wo ein Transitdienst Passagiere aufnimmt und absetzt. Dies kann eine U-Bahn-Station oder eine Bushaltestelle sein. Jede Haltestelle verfügt, neben anderen Attributen, über geografische Koordinaten, um ihren Standort auf einer Karte zu bestimmen, und einen Namen, der mit den für Fahrgäste gedachten Materialien des Unternehmens übereinstimmt. Haltestellen werden Fahrten über Haltestellenzeiten zugeordnet. 
 Mit GTFS ist es auch möglich, das Innere größerer Stationen wie Bahnhöfen oder Busdepots über [Pathways](/getting_started/features/pathways) zu beschreiben. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`, `stop_code`, `stop_name`, `stop_desc`, `stop_lat`, `stop_lon`, `stop_url`, `stop_timezone`, `platform_code` | 
 
 **Voraussetzungen**: 
 
 - Alle anderen Basisfunktionen 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id-ID | stop_code | stop_desc | stop_name | stop_lat. | stop_lon. | stop_url-URL | stop_timezone | platform_code | 
 |---------|-----------|-----------------------------|------------|-----------|------------|---------------|------------|---------------| 
 | TAS001 | TAS001 | Südwestliche Ecke von 5 Avenue und 53 Street | 5 Av/53 St | 45.503568 |-73.587079 | https://www.transitbus.org/stops/TAS001 | | | 
 
 
## Routen 
 
 Eine Route ist eine Gruppe von Fahrten unter derselben Marke, die den Fahrgästen als einzelne Dienstleistung angezeigt werden. Jede Route hat, neben anderen Attributen, einen Namen, der mit den für Fahrgäste gedachten Materialien des Unternehmens übereinstimmt, und die Art des dargestellten Dienstes (wie etwa Bus, U-Bahn oder Metro, Fähre usw.). 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`, `agency_id`, `route_desc`, `route_type`, `route_url`, `route_sort_order`, `route_short_name`, `route_long_name`| 
 
 **Voraussetzungen**: 
 
 - Alle anderen Basisfunktionen 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel definiert eine Busroute (`route_type=3`). 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |----------|-----------|------------------|--------------------|------------|---------------------------------------|------------------| 
 | RA | tb | 17 | Mission – Downtown | Die Route „A“ führt von Lower Mission nach Downtown. | 3 | https://www.transitbus.org/routes/ra | 12 | 
 
 
## Servicedaten 
 
 Servicedaten geben den Datumsbereich an, an dem ein Service angeboten wird, und legen Serviceausnahmen fest, wie z. B. Feiertage und andere Sonderservices an bestimmten Daten. 
 Dies funktioniert, indem in ` .txt ein date und ein date und dann ein Marker für jeden Wochentag definiert werden, an dem es ausgeführt wird. Wenn während dieses Zeitraums eintägige Planungsänderungen auftreten, kann die Datei `calendar_dates.txt` verwendet werden, um den Zeitplan für jeden dieser Tage zu überschreiben. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **Voraussetzungen**: 
 
 - Alle anderen Basisfunktionen 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel definiert zwei Dienste (Werktags- und Wochenenddienste) für den Monat Juli 2024, einschließlich eines speziellen Feiertagsdienstes am 4. Juli, der als Wochenenddienst betrieben wird. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 
 
 | service_id | monday | tuesday | wednesday | thursday | friday | saturday | sunday | start_date | end_date | 
 |------------|--------|---------|----------|-----------|----------|----------|--------|----------|--------|---------| 
 | WE | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | WD | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 
 
 | service_id | date | exception_type | 
 |------------|----------|----------------| 
 | WD | 20240704 | 2 | 
 | WE | 20240704 | 1 | 
 
## Fahrten 
 
 Fahrten kombinieren Routen und Servicedaten, um Fahrten zu erstellen, die von Fahrgästen unternommen werden können. Fahrten werden Haltestellen mithilfe von Haltestellenzeiten zugeordnet. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **Voraussetzungen**: 
 
 - Alle anderen Basisfunktionen 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel definiert zwei Fahrten in beide Richtungen für die RA-Route. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |----------|------------|---------|-----------------|--------------|----------| 
 | RA | WE | AWE1 | 3885 | 0 | 1 | 
 | RA | WE | AWE2 | 3887 | 1 | 2 | 
 
## Haltestellenzeiten 
 
 Haltestellenzeiten werden verwendet, um die individuellen arrival und departure der Haltestellen für jede Fahrt darzustellen, sodass Fahrgäste genau wissen, zu welcher Zeit der Bus, Zug oder die Fähre an einem bestimmten Ort ankommt bzw.abfährt. Die Datei „`stop_times.txt`“ ist normalerweise die größte in einem GTFS Feed. 
 Manche Dienste verkehren in regelmäßigen Abständen (z. B. eine U-Bahn-Linie, die alle 5 Minuten fährt), anstatt bestimmte arrival und departure zu haben. Dies kann mithilfe von [frequenzbasierten Diensten](../base_add-ons/#frequency-based-service) und in Verbindung mit „`stop_times.txt`“ modelliert werden. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| „`trip_id`“, „arrival_time“, „ `departure_time`“, „ `stop_id`“, „ `stop_sequence`“, „pickup_type“, „drop_off_type“, „timepoint“ | 
 
 **Voraussetzungen**: 
 
 – Alle anderen Basisfunktionen 
 
 ??? Hinweis "Beispieldaten" 
 
<p style="font-size:16px"> 
 Das folgende Beispiel definiert den Fahrplan für eine Fahrt mit 5 stops. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | pickup_type | drop_off_type | timepoint | 
 |---------|-----------|----------------|---------|-----------|-------------|-----------|-----------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 Uhr | 6:23:00 Uhr | TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 Uhr | 6:25:00 Uhr | TAS005 | 5 | 0 | 0 | 1 | 
 

