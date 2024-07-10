# Pfade 
 Pfade-Funktionen können große Transitstationen modellieren und Passagiere von Stationseingängen und-ausgängen zu dem Ort leiten, an dem sie in ein vehicle ein- oder aussteigen. Einige dieser Funktionen ermöglichen die Übermittlung der physischen Eigenschaften und der geschätzten Navigationszeit eines Pfades sowie realer Wegfindungssysteme, die in Stationen verwendet werden. 
 
## Pfadverbindungen 
 
 Auf der grundlegenden Ebene bietet Pfade die Basisfunktionen, um wichtige Bereiche, die in den Standorttypen definiert sind, innerhalb einer Station zu verbinden. Diese Verbindungen bilden pathways und ermöglichen Benutzern genaue Wegbeschreibungen (z. B. von einem Eingang zum Einstiegsbereich), was besonders bei der Navigation in großen und komplexen Transitstationen nützlich ist. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`pathway_id`, `from_stop_id`, `to_stop_id`, `pathway_mode`, `is_bidirectional` | 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Standorttypen](../base_add-ons/#location-types) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel definiert mehrere Verbindungen (auch als pathways bezeichnet) zwischen vordefinierten Orten (definiert als stops): Gehwege (`pathway_mode=1`), Treppen (`pathway_mode=2`) und Fahrkartenschranken (`pathway_mode=6`). Bidirektionalität ist ebenfalls angegeben. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | from_stop_id | to_stop_id | pathway_mode | is_bidirectional | 
 |------------|-----------|------------|----------|------------------| 
 | MainSt-001 | A102_E01 | A102_S01 | 1 | 1 | 
 | MainSt-002 | A102_S01 | A102_S02 | 2 | 1 | 
 | MainSt-003 | A102_S02 | A102_F02 | 1 | 1 | 
 | MainSt-004 | A102_F02 | A102_F01 | 6 | 1 | 
 | MainSt-005 | A102_F01 | A102_S03 | 1 | 1 | 
 | MainSt-006 | A102_S03 | A102_S04 | 2 | 1 | 
 | MainSt-007 | A102_F01 | A102_S05 | 1 | 1 | 
 | MainSt-008 | A102_S05 | A102_S06 | 2 | 1 | 
 | MainSt-009 | A102_S04 | A102_B01 | 1 | 1 | 
 | MainSt-010 | A102_S06 | A102_B02 | 1 | 1 | 
 
 
## Wegdetails 
 
 Es können weitere Details zu den physikalischen Eigenschaften der pathways einer Station hinzugefügt werden, einschließlich Länge, Breite und Neigung (bei Rampen) oder Anzahl der Stufen (bei Treppen). So können die Fahrgäste die Bedingungen und die Zugänglichkeit des Weges, den sie zurücklegen müssen, besser einschätzen. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`max_slope`, `min_width`, `length`, `stair_count`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Pfadverbindungen](#pathway-connections) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel definiert zusätzliche Details zu vordefinierten pathways, einschließlich Mindestbreite, Stufenanzahl bei Treppen und Länge und maximaler Neigung bei Gehwegen. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id-ID | min_width.max_slope | min. Breite | Länge | stair_count | 
 |------------|-----------|-----------|--------|-------------| 
 | MainSt-001 | 0 | 4,3 | 3,6 | | 
 | MainSt-002 | | 2,2 | | 15 | 
 | MainSt-003 | 0,06 | 4 | 3,1 | | 
 | MainSt-004 | | 0,9 | 2,9 | | 
 | MainSt-005 | 0 | 3,5 | 5 | | 
 | MainSt-006 | | 2,2 | | 18 | 
 | MainSt-007 | 0 | 3,5 | 5 | | 
 | MainSt-008 | | 2.2 | | 18 | 
 | MainSt-009 | 0 | 6 | 2 | | 
 | MainSt-010 | 0 | 6 | 2 | | 
 
 
## Ebenen 
 
 Ebenen können verwendet werden, um alle verschiedenen Ebenen innerhalb einer Station aufzulisten und Benutzern so eine zusätzliche Informationsebene zu Stationen bereitzustellen. Diese Funktion ermöglicht auch die Verwendung von Aufzügen in Verbindung mit der Funktion „Pathways-Verbindungen“. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[levels.txt](../../../documentation/schedule/reference/#levelstxt)|`level_id`, `level_index`, `level_name`| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`level_id`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Standorttypen](../base_add-ons/#location-types) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt die verschiedenen Ebenen in einer Station. Standorte (definiert als stops) werden dann der entsprechenden Ebene zugeordnet. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | level_id | level_index | level_name | 
 |-------------------|-------------|---------| 
 | level_0_street | 0 | Auf der Straße | 
 | level_-1_lobby |-1 | Lobby | 
 | level_-2_platform |-2 | Plattform | 
 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | stop_id-ID | level_id-ID | 
 |--------------|----------| 
 | Station_A102 | | 
 | A102_B01 |-2 | 
 | A102_B02 |-2 | 
 | A102_E01 | 0 | 
 | A102_S01 | 0 | 
 | A102_S02 |-1 | 
 | A102_S03 |-1 | 
 | A102_S04 |-2 | 
 | A102_S05 |-1 | 
 | A102_S06 |-2 | 
 | A102_F01 |-1 | 
 | A102_F02 |-1 | 
 
 
## Reisezeit innerhalb der Station 
 
 Die Reisezeit innerhalb der Station bietet eine zusätzliche Detailebene für Wegbeschreibungen innerhalb der Stationen und gibt Benutzern eine geschätzte Zeit an, die zum Navigieren innerhalb der Stationen benötigt wird. Dadurch sind bessere Wegbeschreibungen und Reisezeiten möglich. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`traversal_time`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Wegverbindungen](#pathway-connections) 
 
 ??? Hinweis "Beispieldaten" 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt die geschätzte Reisezeit (in Sekunden), die zum Navigieren jedes Pfades benötigt wird. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | traversal_time | 
 |------------|----------------| 
 | MainSt-001 | 3 | 
 | MainSt-002 | 20 | 
 | MainSt-003 | 2 | 
 | MainSt-004 | 2 | 
 | MainSt-005 | 4 | 
 | MainSt-006 | 25 | 
 | MainSt-007 | 4 | 
 | MainSt-008 | 25 | 
 | MainSt-009 | 2 | 
 | MainSt-010 | 2 | 
 
 
## Wegweiser 
 
 Wegweiser können die in Routenplanern angezeigten Informationen mit realen Schildern verknüpfen. Wenn dies in einem Feed dargestellt wird, können Routenplaner Anweisungen wie „Folgen Sie den Schildern nach “ bereitstellen. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`signposted_as`, `reversed_signposted_as`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Wegverbindungen](#pathway-connections) 
 
 ??? Hinweis "Beispieldaten" 
 
<p style="font-size:16px"> 
 Das folgende Beispiel gibt die Navigationsinformationen für vordefinierte pathways an und spiegelt den auf den physischen Schildern der Station angezeigten Text wider. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | signposted_as | reversed_signposted_as | 
 |------------|------------------|------------------------| 
 | MainSt-001 | zur Lobby | Ausgang | 
 | MainSt-002 | | | 
 | MainSt-003 | Zu den Bahnsteigen | Ausgang | 
 | MainSt-004 | | | 
 | MainSt-005 | Züge in westlicher Richtung | Ausgang | 
 | MainSt-006 | | | 
 | MainSt-007 | Züge in östlicher Richtung | Ausgang | 
 | MainSt-008 | | | 
 | MainSt-009 | Züge in westlicher Richtung | Zur Lobby | 
 | MainSt-010 | Züge in östlicher Richtung | Zur Lobby | 
 
 

