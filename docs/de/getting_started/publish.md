# Ihren GTFS Feed öffentlich zugänglich machen## Vorteile der Freigabe Ihres GTFS 
 
 GTFS Daten können auf viele Arten genutzt werden und die öffentliche Freigabe der GTFS Daten Ihres Unternehmens bietet Ihren Fahrgästen und Ihrem agency als Ganzes zahlreiche Vorteile. Hierzu zählen: 
 
 - Integrieren Ihres Feeds in mobile und webbasierte Reiseplanungsanwendungen, damit Fahrgäste Reisen auf Ihrem System planen können- Senden Ihres Feeds an einen GTFS Aggregator wie die Mobility Database, um ein größeres Publikum anzusprechen und Ihrem agency mehr Sichtbarkeit zu verleihen- Verwenden von Tools, mit denen GTFS Daten in Geografischen Informationssystemen (GIS) und anderen kartenbasierten Analyseprogrammen visualisiert und analysiert werden können### Reiseplanungs-Apps 
 
 Wenn die GTFS Daten Ihres Unternehmens öffentlich freigegeben werden, können sie neben Google Maps auch von einer Vielzahl anderer Reiseplanungsanwendungen genutzt werden. Dazu können andere Navigations-Apps wie Bing Maps, Apple Maps sowie transitspezifische Plattformen wie Transit, Moovit, Transportr und Citymapper gehören. Darüber hinaus ermöglicht der Zugriff auf offene Feed-Daten Entwicklern, Apps zu erstellen, die auf bestimmte Regionen ausgerichtet sind oder Funktionen haben können, die in den Standard-Reiseplanern t enthalten sind, wie z. B.: Vamos (San Joaquin &amp; Stanislaus Counties, Kalifornien), MetroHero (Gebiet Washington DC), Entur (Norwegen) und mehr. 
 
### Feed-Aggregatoren 
 
 Wenn Sie Ihre GTFS Daten freigeben, können sie auch durch GTFS Feed-Aggregationsplattformen indiziert werden. Dazu können Verzeichnisse von GTFS Feeds auf Bundesstaats- oder Regionalebene sowie internationale Feed-Aggregatoren wie die [Mobility Database](https://database.mobilitydata.org/) und [Transitland](https://www.transit.land/) gehören (weitere Feed-Aggregatoren finden Sie [hier](../../resources/data)). Die Indizierung auf einem Feed-Aggregator steigert die Sichtbarkeit Ihrer Agentur und ermöglicht Entwicklern, Forschern und anderen Interessierten den einfachen Zugriff auf die Daten Ihrer Agentur für eine Vielzahl von Zwecken, einschließlich der Entwicklung neuer Anwendungen. 
 
### Integration mit GIS, Analysen und anderen Plattformen und Tools 
 
 GTFS Daten können auch importiert und auf einer Vielzahl von Plattformen für georäumliche Analysen verwendet werden. Programme für geografische Informationssysteme (GIS) wie ArcGIS von Esri sowie das Open-Source-Programm QGIS verfügen über eigene Plug-Ins und Erweiterungen, die GTFS Haltestellen- und Routendaten import und visualisieren können. 
 
 - Esri verfügt über eine [große Auswahl an Tools und Plugins](https:), die GTFS Daten verwenden, einschließlich der Visualisierung von Fahrplandaten- In QGIS können Sie mit [GTFS-GO](https: GTFS-GO-master/) und [GTFS Loader](https:) routes + stops innerhalb der Plattform visualisieren- [Zusätzliche Analysetools](../../resources/agency-tools) 
 
 Andere Plattformen ermöglichen Ihnen die Visualisierung und Analyse von GTFS Daten auf einzigartige Weise: 
 
 - [Conveyal](https: ) ist ein Open-Source-Programm, mit dem Benutzer GTFS Daten import können, um Fahrpläne, routes und Muster erkennen und die Auswirkungen potenzieller Serviceänderungen analysieren. Benutzer können auch demografische Daten import und damit arbeiten, um beispielsweise Analysen durchzuführen, wie sich unterschiedliche routes oder Fahrpläne auf den Zugang zu Arbeitsplätzen in einem bestimmten Stadtgebiet auswirken würden. 
 - [GTFS to HTML](https:) ist ein Open-Source-Tool, das die Konvertierung von GTFS Fahrplandaten in HTML-Fahrpläne ermöglicht. Agenturen können damit ihre Fahrpläne automatisch auf ihrer Website in einem Format veröffentlichen und aktualisieren, das auch von Screenreadern gelesen werden kann, wodurch die Daten für sehbehinderte Menschen zugänglich werden. 
 
## Teilen Ihrer Daten: Tipps und bewährte Vorgehensweisen### Erstellen und Verwalten eines permanenten Abruflinks 
 
 Ein Abruflink ist eine permanente URL, unter der die GTFS Schedule Fahrplandateien Ihrer Agentur gespeichert sind. Normalerweise wird er entweder auf der Website Ihrer Agentur oder von Ihrem Anbieter gehostet, falls Sie einen mit der GTFS Produktion beauftragt haben. Auf diese Weise greifen Reiseplanungs-Apps wie Google Maps auf Ihre Daten zu. Im Idealfall sollten Ihre GTFS Schedule direkt von dieser URL heruntergeladen werden können, ohne dass eine Anmeldung erforderlich ist. Wenn dies jedoch aufgrund von Lizenzbeschränkungen nicht möglich ist, kann Ihre agency den Zugriff auf die Daten kontrollieren, indem sie API-Schlüssel verwendet und an die Benutzer der Daten ausgibt. 
 
### URL und Dateinamen 
 
 Einheitliche Abruflinks und GTFS Dateinamen sind entscheidend, um den Zugriff auf Ihre Feed-Daten sicherzustellen. Wenn Ihre agency keine einheitlichen URLs und Dateinamen für ihre Daten verwendet, bedeutet dies, dass Reiseplanungs-Apps, Feed-Aggregatoren und andere Benutzer nicht die genauesten und aktuellsten Daten erhalten, was auf lange Sicht zu Problemen cause wird. 
 
 Wenn Sie eine URL für Ihren permanenten Abruflink festgelegt haben, ÄNDERN SIE SIE NICHT. Das bedeutet, dass der URL Name konsistent bleiben sollte, auch wenn die Dateien selbst aktualisiert werden. Halten Sie Ihre URLs daher so einfach und allgemein wie möglich und vermeiden Sie URLs, die Daten oder Versionsnummern enthalten. 
 
 - **GUT:** http://www.bart.gov/dev/schedules/google_transit.zip, 
 - **VERMEIDEN:** http://www.bart.gov/dev/schedules/google_transit_Fall_2021.zip 
 
 Achten Sie auch darauf, dass der Name des ZIP-Ordners, der die GTFS Schedule Fahrplandateien enthält, konsistent bleibt, selbst wenn Sie Aktualisierungen am Feed selbst vornehmen. Wenn Sie beispielsweise einen Feed aktualisieren, sollten Sie dem Namen des ZIP-Ordners keinerlei date oder Versionsnummer hinzufügen. Wenn Sie Daten zur Feed-Version oder zu den Start- und Enddaten des Feeds in den Feed aufnehmen möchten, können Sie diese in die Datei feed_info.txt aufnehmen. 
 
 - **GUT:** „YourAgency_gtfs.zip“, „google_transit.zip“, „gtfs.zip“, 
 - **VERMEIDEN:** „YourAgency_gtfs_092921.zip“, „YourAgency_Fall2021.zip“ 
 
 
### Dateikonfiguration und-integrität 
 
 Ihr GTFS ist eine ZIP-Datei, die mehrere miteinander verbundene Textdateien (.txt) enthält. Um das richtige Format zu gewährleisten, gehen Sie immer wie folgt vor: 
 
 1. Wenn Sie eine Textdatei öffnen, achten Sie darauf, dass die Werte als Text erhalten bleiben. Ein GTFS enthält viele Felder, die Anwendungen wie Excel falsch lesen oder abkürzen. 
 2. Die Dateien sind durch Kommas und nicht durch Tabulatoren getrennt. Das bedeutet, dass jede Datei Datensätze in Zeilen enthält und die verschiedenen Felder durch Kommas getrennt sind. 
 3. Zusätzliche Zeilen oder Spalten cause Fehler bei verwendenden Anwendungen. Stellen Sie daher beim Speichern der Datei sicher, dass keine leeren Zeilen oder Spalten vorhanden sind. 
 4. Verwerfen Sie keine der Dateien in Ihrem GTFS – sie arbeiten zusammen und fehlende Dateien können Fehler bei verwendenden Anwendungen cause. 
 5. Achten Sie beim erneuten Zippen der Dateien darauf, alle Dateien und nicht einen enthaltenen Ordner zu zippen. Sie können sicher sein, dass Sie dies richtig gemacht haben, wenn Sie Ihre Datei entpacken und die Dateien sofort in diesem Ordner sehen und nicht in einem anderen Ordner, der die Dateien enthält. 
 
 
### Weitere Überlegungen 
 
 Wenn mehrere Agenturen dieselbe Haltestelle mit unterschiedlichen Namen oder Codes teilen, müssen Anwendungen wie Google Maps möglicherweise eine auswählen. Um Verwirrungen zu vermeiden, stimmen Sie sich mit anderen Agenturen auf die Namen und Codes ab. Dadurch werden Konflikte zwischen verschiedenen GTFS Datensätzen minimiert. 
 
 Falls Ihnen mehrere GTFS Datensätze zur Verfügung stehen – normalerweise das Ergebnis davon, dass einer für öffentliche Anwendungen wie Transit App und ein anderer für interne CAD/AVL-Betriebssysteme erstellt wird – müssen Sie möglicherweise entscheiden, welcher der veröffentlichte GTFS sein soll. Es wird empfohlen, dass Sie den Feed bewerben, der die meisten Informationen für Fahrgäste enthält. Versuchen Sie nach Möglichkeit, Ihre GTFS Datensätze aufeinander abzustimmen (dieselben IDs für Dinge wie stops und Fahrten), damit interne Datensätze nicht mit öffentlichen in Konflikt geraten und die Integration anderer Feeds wie GTFS-RT möglich ist. 
 

