# Fahrpreise 
 GTFS ermöglicht die präzise Modellierung verschiedenster Fahrpreisstrukturen, die von unterschiedlichen Verkehrsunternehmen weltweit verwendet werden, wie beispielsweise Fahrpreise auf Zonen-, Distanz- oder Tageszeitbasis. GTFS Fahrpreise informieren Fahrgäste über den für ihre Fahrt geltenden price und die zur Zahlung verfügbaren Zahlungsmittel. 
 
## Fahrpreisprodukte 
 
 „Fahrpreisprodukte“ listet die Ticket- oder Fahrpreisarten (z. B. Einzelfahrtentarife, Monatskarten, Umsteigegebühren etc.) auf, die von einem agency für die Nutzung eines Dienstes angeboten werden. Fahrpreisprodukte dienen als Grundlage zur Modellierung der Fahrpreisstruktur eines Unternehmens und sind über in „fare_leg_rules.txt“ beschriebene Mechanismen mit dem Verkehrsunternehmen verknüpft. Die Verknüpfung von Fahrpreisprodukten mit verschiedenen Reisebedingungen wie routes, Gebieten und Zeiten bestimmt die Fahrpreiskosten für einzelne Reiseabschnitte und transfers. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel stellt ein einfaches Fahrpreisprodukt dar (Einzelfahrt 2,75 USD). 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | 
 |------------------|-----------------|---|---| 
 | single_ride | Fahrpreis für Einzelfahrt | 2,75 | USD | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id | 
 |------------------| 
 | single_ride | 
 
 
## Fare Media 
 
 Fare Media definiert die unterstützten Medien, die zum Halten und/oder Validieren eines Fahrpreisprodukts verwendet werden können. Dies bezieht sich auf physische oder virtuelle Behälter wie ein Papierticket, eine wiederaufladbare Fahrkarte oder auch kontaktloses Bezahlen mit Kreditkarten oder Smartphones. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt einen Ausschnitt verschiedener Fahrkartenmedien in der San Francisco Bay Area. „Clipper“ wird als physische Fahrkarte mit „fare_media_type=2“ beschrieben. „SFMTA Munimobile“ wird als mobile App mit „fare_media_type=2“ beschrieben. „Bargeld“, das ohne Ticket direkt an den Fahrer gegeben wird, ist „fare_media_type=0“. 
</p> 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>fare_media.txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------------------|-----------------| 
 | Clipper | Clipper | 2 | 
 | Munimobile | SFMTA MuniMobile | 4 | 
 | Bargeld | Bargeld | 0 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|-----------------|---|---|---| 
 | single_ride | Fahrpreis für Einzelfahrt | 2,75 | USD | munimobile | 
 
 
 
 
## Routenbasierte Fahrpreise 
 
 Routenbasierte Fahrpreise werden verwendet, um bestimmte routes mit unterschiedlichen Fahrpreisen zu versehen, wie etwa Sondertarife für Expressdienste oder differenzierende Fahrpreise zwischen einem Bus Rapid Transit-Dienst und herkömmlichen Busdiensten. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Fare Products-Funktion](#fare-products) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt ein System, das routes in Express- und Nahverkehrskategorien einteilt, denen jeweils unterschiedliche Tarifprodukte zugeordnet sind.</p> 
 
<p style="font-size:16px"> **Verwenden von `.txt` + `.txt`**</p> 
 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#networkstxt"><b>Netzwerke.txt</b></a><br> 
</p> 
 
 | network_id-ID | network_name | 
 |------------|-----------------| 
 | express | Express | 
 | lokal | Lokal | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#route_networkstxt"><b>Routennetzwerke.txt</b></a><br> 
</p> 
 
 | network_id-ID | route_id-ID | 
 |------------|-----------| 
 | express | express_a | 
 | express | express_b | 
 | lokal | local_1 | 
 | lokal | local_2 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id-ID | fare_product_id-ID | 
 |------------|-----------------| 
 | Express | Express-Einzelfahrt | 
 | lokal | lokale_Einzelfahrt | 
 
<p style="font-size:16px"> **ODER mit `routes**</p> 
 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | express_a | express | 
 | express_b | express | 
 | local_1 | local | 
 | local_2 | local | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | express | express_single_ride | 
 | local | local_single_ride | 
 
 
## Zeitbasierte Fahrpreise 
 
 Zeitbasierte Fahrpreise werden verwendet, um Fahrpreise für bestimmte Tageszeiten oder Wochentage zuzuweisen, wie etwa Fahrpreise für Hauptverkehrszeiten und Nebenverkehrszeiten und/oder Wochenendfahrpreise. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Tarifproduktfunktion](../fares/#fare-products) 
 
 ??? Hinweis "Beispieldaten" 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt ein System, bei dem die Spitzenzeiten von 8:00 bis 10:00 Uhr liegen und die übrigen Stunden Nebenzeiten sind.</p> 
 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#timeframestxt"><b>Zeitrahmen.txt</b></a><br> 
</p> 
 
 | timeframe_group_id-ID | start_time | end_time | service_id-ID | 
 |--------------------|------------|----------|------------| 
 | Spitzenzeit | 8:00:00 | 10:00:00 | ganztägig | 
 | regulär | 0:00:00 | 08:00:00 | ganztägig | 
 | regulär | 10:00:00 | 24:00:00 | ganztägig | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id | 
 |-------------------------|---------------------| 
 | peak | peak_single_ride | 
 | regular | regular_single_ride | 
 
 
## Zonenbasierte Fahrpreise 
 
 Zonenbasierte Fahrpreise werden verwendet, um zonenbasierte Systeme darzustellen, bei denen für die Fahrt von einer bestimmten Zone in eine andere ein bestimmter Fahrpreis gilt. Eine Zone wird durch eine Gruppe von stops definiert. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id`, `area_name`| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Fare Products-Funktion](../fares/#fare-products) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt den Fahrpreis von Zone A nach Zone B.</p> 
 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id-ID | area_name | 
 |---------|-----------| 
 | Zone_a | Zone A | 
 | Zone_b | Zone B | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id-ID | stop_id-ID | 
 |---------|---------| 
 | Zone_a | Haltestelle_a | 
 | Zone_a | Haltestelle_b | 
 | Zone_b | Haltestelle_c | 
 | Zone_b | Haltestelle_d | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id | 
 |--------------|------------|-----------------| 
 | zone_a | zone_b | zone_a_b_single | 
 
## Fares Transfers 
 
 Fares Transfers wird verwendet, um Regeln zu definieren, die beim Umsteigen zwischen Teilstrecken (oder einzelnen Reisesegmenten) gelten. Dies ermöglicht die Modellierung der Gesamtkosten einer Reise mit mehreren Teilstrecken unter Berücksichtigung spezieller Umsteigerichtlinien, wie z. B. kostenlose transfers für eine bestimmte Zeitspanne, oder die Anwendung von Fahrpreisnachlässen auf Grundlage bereits zurückgelegter Teilstrecken. 
 
 | Eingeschlossene Dateien | Eingeschlossene Felder | 
 |----------------------------------|-------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id`, `transfer_count`, `duration_limit`, `duration_limit_type`, `fare_transfer_type`, `fare_product_id`| 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 - [Fare Products-Funktion](../fares/#fare-products) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel veranschaulicht, dass innerhalb eines 2-Stunden-Fensters unbegrenzte kostenlose transfers zwischen Leg A innerhalb des Systems zulässig sind.</p> 
 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |---------------| 
 | a | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|----------------|---------------------|-----------------|-----------------| 
 | a | a |-1 | 7200 | 1 | 0 | free_transfer | 
 
 
## Fares v1 
 
 Fares v1 ist eine Legacy-Alternative zu den anderen oben beschriebenen Fares-Funktionen. Es ermöglicht die Modellierung grundlegender Fahrpreisinformationen wie Fahrpreispreise, Zahlungsmethoden, transfers und zonenbasierte Fahrpreise mithilfe der Dateien „fare_rules.txt“ und „fare_attributes.txt“. Es ist zwar einfacher zu erstellen, kann jedoch keine komplexeren Tarifstrukturen modellieren und wird möglicherweise verworfen, wenn andere Tariffunktionen (die Teil der sogenannten Tarife v2 sind) ausreichend unterstützt werden. 
 
 | Enthaltene Dateien | Enthaltene Felder | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **Voraussetzungen**: 
 
 - [Basisfunktionen](../base) 
 
 ??? Hinweis „Beispieldaten“ 
 
<p style="font-size:16px"> 
 Das folgende Beispiel zeigt, dass eine Fahrt in einem Netzwerk mit einer Prepaid-Karte 3,20 CAD kostet und innerhalb eines 2-Stunden-Fensters kostenlose transfers möglich sind.</p> 
 
 !!! Notiz "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 | fare_id-ID | price | currency_type | payment_method | transfers | transfer_duration | 
 |-------------------|----------|---------------|----------------|-----------|-------------------| 
 | Prepaid-Kartentarif | 3,2 | CAD | 1 | | 7200 | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 | fare_id-ID | route_id-ID | origin_id-ID | destination_id-ID | 
 |-------------------|----------|-----------------|-----------------| 
 | Prepaid-Kartentarif | Linie1 | U-Bahn-Stationen | U-Bahn-Stationen | 
 | Prepaid-Kartentarif | Linie2 | U-Bahn-Stationen | U-Bahn-Stationen | 
 
 !!! Hinweis "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id-ID | stop_name | stop_lat | stop_lon | zone_id-ID | 
 |---------|-----------|-----------|------------|-----------------| 
 | A | HaltestelleA | 43,670049 |-79,385389 | U-Bahn-Stationen | 
 | B | HaltestelleB | 43,671049 |-79,386789 | U-Bahn-Stationen | 
 
 
 | stop_id-ID | stop_name | stop_lat | stop_lon | zone_id-ID | 
 |---------|-----------|-----------|------------|-----------------| 
 | A | HaltestelleA | 43,670049 |-79,385389 | U-Bahn-Stationen | 
 | B | HaltestelleB | 43.671049 |-79.386789 | U-Bahn-Stationen | 
 
 

