# GTFS Schedule 
 
 Während sich das GTFS Referenzformat weiterentwickelt, um den aktuellen Anforderungen von Verkehrssystemen gerecht zu werden, können seine Funktionen zunehmend komplexer werden. Die ** GTFS Funktionen** sollen eine klare und eindeutige Erklärung der durch das GTFS Referenzformat ermöglichten Funktionen bieten. Auf diese Weise können Verkehrsbetriebe, Anbieter, Verbraucher und Forscher die Fähigkeiten von GTFS verstehen und die Frage beantworten: **Was kann ich mit GTFS tun?** 
 
 Die folgenden Funktionsgruppen erläutern den Zweck jeder Funktion sowie die ihnen zugehörigen Dateien und Felder und helfen Benutzern zu verstehen, welche Daten zur Unterstützung einer bestimmten Funktion benötigt werden. 
 
## Basis 
 Diese wesentlichen Funktionen bilden den Kern eines GTFS Feeds. Sie sind die minimalen Elemente, die zur Darstellung eines Verkehrsdienstes erforderlich sind. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 Geben Sie Einzelheiten zu den für den Verkehrsdienst verantwortlichen Agenturen an. 
 
 [:octicons-arrow-right-24: Weitere Informationen](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Stops__ 
 
 Definieren Sie die Standorte, an denen ein Verkehrsdienst Fahrgäste aufnimmt und absetzt. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Routen__ 
 
 Definieren Sie die Elemente einer Transitroute wie Name und Serviceart. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __Servicedaten__ 
 
 Erstellen Sie die Struktur zum Planen von Fahrten und Serviceausnahmen. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trips__ 
 
 Stellen Transitfahrzeuge dar, die zu geplanten Zeiten entlang einer festgelegten Route fahren. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Stop Times__ 
 
 Definieren Sie die arrival und departure jeder Fahrt für jede Haltestelle. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base/#stop-times) 
 
</div> 
 
## Basis-Add-ons 
 Diese Funktionen erweitern einen GTFS Datensatz, verbessern das Fahrerlebnis und erleichtern die Zusammenarbeit zwischen Agenturen, Anbietern und Datenwiederverwendern. Sie können das Hinzufügen neuer Felder zu vorhandenen Dateien oder das Erstellen neuer Dateien beinhalten. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Feed-Informationen__ 
 
 Kommunizieren Sie wichtige Informationen über den Feed selbst. 
 
 [:octicons-arrow-right-24: Weitere Informationen](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ 
 
 Definieren Sie den geografischen Pfad, dem ein vehicle während einer Fahrt folgt. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __Routenfarben__ 
 
 Stellen Sie das bestimmten routes zugewiesene Farbschema genau dar und kommunizieren Sie es. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __Fahrräder erlaubt__ 
 
 Teilen Sie mit, ob Fahrzeuge Fahrräder mitnehmen können oder nicht. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ 
 
 Kommunizieren Sie die Beschilderung der Fahrzeuge, die das Ziel der Fahrt anzeigen. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __Standorttypen__ 
 
 Klassifizieren Sie wichtige Bereiche innerhalb von Transitstationen wie Eingänge und Ausgänge. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frequenzen__ 
 
 Stellen Dienste dar, die in regelmäßigen Abständen oder mit bestimmten Taktzeiten verkehren. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __Umstiege__ 
 
 Beschreiben Sie die zulässigen transfers zwischen verschiedenen Verkehrsmitteln. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Translations__ 
 
 Serviceinformationen in mehreren Sprachen kommunizieren. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Attributions__ 
 
 Teilen Sie mit, wer an der Erstellung des Datensatzes beteiligt war. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../base_add-ons/# attributions) 
 
</div> 
 
 
## Barrierefreiheit 
 Barrierefreiheitsfunktionen bieten Menschen mit Behinderungen wichtige Informationen für den Zugriff auf den Dienst. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Haltestellen für Rollstuhlfahrer__ 
 
 Geben Sie an, ob ein Rollstuhlfahrer von einem Standort aus einsteigen kann. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Fahrten für Rollstuhlfahrer__ 
 
 Geben Sie an, ob ein vehicle für Rollstuhlfahrer geeignet ist. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Text-to-Speech__ 
 
 Stellen Sie die notwendigen Eingaben bereit, um Text für Haltestellennamen in Audio umzuwandeln. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Fahrpreise 
 GTFS kann verschiedene Fahrpreisstrukturen modellieren, wie z. B. zonen-, entfernungs- oder tageszeitabhängige Fahrpreise. Es informiert Fahrgäste über Fahrtpreise und Zahlungsmethoden. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Fahrpreisprodukte__ 
 
 Definieren Sie die Liste der für Benutzer verfügbaren Tickets oder Fahrpreisarten. 
 
 [:octicons-arrow-right-24: Weitere Informationen](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fahrpreismedien__ 
 
 Definieren Sie die Medien, die zum Halten und/oder Validieren eines Fahrpreisprodukts verwendet werden können. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __Routenbasierte Fahrpreise__ 
 
 Beschreiben Sie die Regeln, die für die Anwendung unterschiedlicher Fahrpreise für bestimmte routes verwendet werden. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zeitbasierte Fahrpreise__ 
 
 Beschreiben Sie Fahrpreise, die nach Tageszeit oder Wochentag differenziert sind. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zonenbasierte Fahrpreise__ 
 
 Beschreiben Sie differenzierte Fahrpreise für Reisen von einem Gebiet in ein anderes. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Fahrpreisumstiege__ 
 
 Definieren Sie die Gebühren, die beim Umsteigen von einer Fahrtstrecke auf eine andere anfallen. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 Legacy-Funktion, die eine einfachere Darstellung von Fahrpreisinformationen ermöglicht. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../fares/#fares-v1) 
 
</div> 
 
 
## Wege 
 
 Die Funktion „Wege“ ermöglicht die Modellierung großer Transitstationen, sodass Fahrgäste von den Eingängen zu den Einstiegsbereichen geleitet werden. Sie bietet Wegdetails, geschätzte Navigationszeiten und Wegfindungssysteme. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Wegverbindungen__ 
 
 Modellieren Sie Wege, die relevante Punkte innerhalb einer Transitstation verbinden. 
 
 [:octicons-arrow-right-24: Weitere Informationen](../pathways/#Wegverbindungen) 
 
 - :material-subway-variant:{ .lg.middle } __Wegdetails__ 
 
 Geben Sie zusätzliche Details zu den physischen Eigenschaften eines Weges an. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Ebenen__ 
 
 Beschreiben und listen Sie alle verschiedenen Ebenen innerhalb einer Transitstation auf. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __Besuchszeit in der Station__ 
 
 Teilen Sie die geschätzte Zeit mit, die zum Navigieren der Wege innerhalb einer Transitstation benötigt wird. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __Wegeschilder__ 
 
 Kommunizieren Sie die mit einem Weg verbundene Beschilderung im Bahnhof. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../pathways/#pathway-signs) 
 
</div> 
 
## Flexible Dienste 
 Flexible Dienste oder bedarfsgesteuerte Dienste, die keinen regelmäßigen Fahrplänen oder festen routes folgen. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Dauerhafte Haltestellen__ 
 
 Geben Sie an, ob ein Benutzer zwischen stops abgeholt und/oder abgesetzt werden kann. 
 
 [:octicons-arrow-right-24: Weitere Informationen](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __Buchungsregeln__ 
 
 Geben Sie an, ob Benutzer eine Fahrt mit einem Bedarfsservice reservieren können. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __Vordefinierte Routen mit Abweichung__ 
 
 Fahrzeuge, die zum Abholen oder Absetzen kurz von einer Route abweichen können. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __Zonenbasierte bedarfsgesteuerte Dienste__ 
 
 Dienste, die das Abholen/Absetzen an jedem beliebigen Ort innerhalb eines bestimmten Gebiets ermöglichen. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.middle } __Fixed-Stops Demand Responsive Services__ 
 
 Dienste, die das Ein- und Aussteigen an jedem beliebigen Ort innerhalb einer Gruppe von stops ermöglichen. 
 
 [:octicons-arrow-right-24: Mehr erfahren](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

