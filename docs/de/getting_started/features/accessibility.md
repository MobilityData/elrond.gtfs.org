# Barrierefreiheit 
 Die Barrierefreiheitsfunktionen sollen Menschen mit Behinderungen die Informationen bereitstellen, die sie für die Nutzung des Dienstes benötigen. 
 
## Haltestellen Rollstuhlgerechte Haltestellen 
 
 Haltestellen Rollstuhlgerechte Haltestellen ermöglicht die Angabe, ob ein Einstieg für Rollstuhlfahrer vom angegebenen Standort aus möglich ist. Um Fahrgäste im Rollstuhl bedienen zu können, ist die Angabe, dass ein Einstieg für Rollstuhlfahrer möglich ist, genauso wichtig wie die Angabe, dass dies t der Fall ist. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Standorttypen](../base_add-ons/#location-types) beim Definieren von Zugänglichkeitsinformationen für Bahnhofsstandorte wie Ein-/Ausgänge oder Einstiegsbereiche. 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt, dass Rollstuhlfahrer an der Haltestelle „TAS001“ mit „wheelchair_boarding=1“ einsteigen können. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id-ID | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|-----------|------------|---------------|---------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 | | 1 | 
 
 
## Fahrten Rollstuhlgerechtigkeit 
 
 Fahrten Rollstuhlgerechtigkeit ermöglicht die Angabe, ob ein vehicle für Fahrgäste im Rollstuhl geeignet ist. Um Fahrgäste im Rollstuhl bedienen zu können, ist die Angabe, dass ein vehicle für Fahrgäste im Rollstuhl geeignet ist, genauso wichtig wie die Angabe, dass ein vehicle dies t kann. Sowohl die Haltestelle als auch die Fahrt müssen rollstuhlgerecht sein, damit ein Fahrgast an der angegebenen Haltestelle eine Fahrt antreten kann. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt, dass das vehicle der Fahrt „AWE1“ über eine Unterbringung für mindestens einen Rollstuhl verfügt, das vehicle der Fahrt „AWE2“ jedoch nicht. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id-ID | service_id-ID | Fahrt-ID | trip_id | 
 |----------|------------|---------|-----------------------| 
 | RA | WE | AWE1 | wheelchair_accessible | 
 | RA | WE | AWE2 | 2 | 
 
 
## Text-to-Speech 
 
 Text-to-Speech ermöglicht die Bereitstellung der notwendigen Eingaben zur Umwandlung von Text in Audio und stellt sicher, dass Fahrgäste, die unterstützende Technologie zum Vorlesen von Text verwenden, die richtigen Haltestellennamen erhalten, wenn sie den öffentlichen Nahverkehr nutzen. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel bietet eine lesbare Version des Haltestellennamens, sodass Text-to-Speech-Tools den Namen vorlesen können. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id-ID | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|------------|-------------|------------|------------|--------------------------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 | 5th Avenue und 53th Street | 
 

