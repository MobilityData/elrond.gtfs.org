# Erstellen eines GTFS Datensatzes## Übersicht über einen GTFS Feed 
 Alle GTFS Feeds beginnen mit einem Datensatz im GTFS Referenzformat, einer Reihe von CSV-Dateien, die mit der Dateierweiterung.txt gespeichert sind[^1]. In seiner einfachsten Implementierung beginnt ein GTFS-Datensatz normalerweise mit sieben Basisdateien, die in einer.zip-Datei zusammengefasst sind, die unter einer stabilen und öffentlichen URL gehostet wird: Dies ist der GTFS Feed. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_001.png"> 
 
 Jede Datei besteht aus einer Liste mehrerer Datensätze (Datenzeilen) mit mehreren Informationsfeldern. Beispielsweise stellt jede Zeile in [routes.txt](../../documentation/schedule/reference/#routestxt) eine öffentliche Verkehrsroute dar und ihre Felder beschreiben mehrere Elemente dieser Route, wie Name, Beschreibung, agency usw. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_002.png"> 
 
 Die Basisdateien eines GTFS Datensatzes können wie folgt beschrieben werden: Ein GTFS-Fahrplandatensatz enthält eine oder mehrere routes ([routes.txt](../../documentation/schedule/reference/#routestxt)), jede Route enthält eine oder mehrere Fahrten ([trips.txt](../../documentation/schedule/reference/#tripstxt)), jede Fahrt führt zu einer Reihe von stops ([stops.txt](../../documentation/schedule/reference/#stopstxt)) zu festgelegten Zeiten ([stop_times.txt](../../documentation/schedule/reference/#stop_timestxt)). Fahrten und Haltestellenzeiten enthalten nur Informationen zur Tageszeit; Der Kalender wird verwendet, um zu bestimmen, an welchen Tagen eine bestimmte Fahrt stattfindet ([calendar.txt](../../documentation/schedule/reference/#calendartxt) und [calendar_dates.txt](../../documentation/schedule/reference/#calendar_datestxt)). Darüber hinaus können mehrere Agenturen ([agency.txt](../../documentation/schedule/reference/#agencytxt)) mehrere routes betreiben. Diese Dateien sind durch Felder miteinander verknüpft, die untereinander referenzieren. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_003.png"> 
 
 Nachdem diese Dateien zur Erstellung eines grundlegenden GTFS Datensatzes eingerichtet wurden, können weitere (optional) Dateien hinzugefügt werden, um andere Funktionen oder spezielle Anforderungen zwischen Verkehrsbetrieben und Anbietern zu ermöglichen. Beispiele für diese Dateien: 
 
 - [shapes.txt](../../documentation/schedule/reference/#shapestxt) ermöglicht die grafische Darstellung der Route einer Fahrt, 
 - [pathways.txt](../../documentation/schedule/reference/#pathwaystxt) enthält Informationen zur Generierung von Wegbeschreibungen, die Benutzern die Navigation zu Bahnhöfen erleichtern, 
 - [frequencies.txt](../../documentation/schedule/reference/#frequenciestxt) bietet eine alternative Möglichkeit zur Angabe von Haltestellenzeiten. 
 
 Weitere Informationen zu allen GTFS Funktionen, die aktiviert werden können, finden Sie im Abschnitt [„Was kann GTFS ?“](../features/overview/). 
 
 Ein GTFS Schedule kann mit Echtzeitinformationen wie vehicle und Serviceaktualisierungen ergänzt werden. Dazu muss ein GTFS Realtime Feed separat vom vorhandenen GTFS Schedule Fahrplandatensatz erstellt werden. 
 
 Ein GTFS Realtime-Feed besteht aus einer normalen Binärdatei, die über HTTP bereitgestellt und häufig aktualisiert wird. Jeder Webservertyp kann die Datei hosten und bereitstellen. Das GTFS Realtime-Datenaustauschformat basiert auf [Protocol Buffers](https://developers.google.com/protocol-buffers/), einem sprach- und plattformneutralen Mechanismus zur Serialisierung strukturierter Daten. GTFS Realtime kann drei Arten von Informationen bereitstellen: Fahrtaktualisierungen, Servicewarnungen und Fahrzeugpositionen. Diese können je nach den zu kommunizierenden Serviceinformationen kombiniert werden. 
 
 Da GTFS Realtime die Darstellung des aktuellen Status einer Flotte ermöglicht, muss der Feed regelmäßig aktualisiert werden – vorzugsweise immer dann, wenn neue Daten vom automatischen Fahrzeugortungssystem des Dienstes eingehen. Der GTFS Schedule und ein GTFS Realtime Feed ermöglichen es den nutzenden Anwendungen, den Fahrgästen genaue und aktuelle Informationen bereitzustellen. Weitere Informationen finden Sie in der technischen Dokumentation. 
 
## Sie erstellen Ihren ersten GTFS Feed? 
 
 Wenn Sie eine agency sind, die Ihren ersten GTFS Feed erstellen möchte, müssen Sie als Erstes die vorhandene Dokumentation lesen. 
 
 Erkunden Sie zunächst die Funktionen von GTFS im Abschnitt [„Was kann GTFS ?“](../features/overview) und legen Sie die verschiedenen Funktionen Ihres Transitdienstes fest, die Sie im GTFS Format darstellen möchten. Für eine ausführlichere Untersuchung bietet die offizielle Referenzdokumentation für [GTFS Schedule](../../documentation/schedule/reference) und [GTFS Realtime](../../documentation/realtime/reference) detaillierte Anleitungen zur Modellierung dieser Funktionen und zur Sicherstellung der Konformität. 
 
 Erfassen Sie als Nächstes alle erforderlichen Daten aus Ihrem System. Dazu gehören Informationen zu allen stops, routes, Fahrplänen, Fahrpreisen usw., da viele dieser Details die Eingaben sein werden, mit denen der GTFS Datensatz gefüllt wird. 
 
 Je nach Größe und Komplexität Ihres Systems haben Sie die Möglichkeit, die Daten entweder intern zu erstellen oder einen externen GTFS Anbieter mit der Konvertierung der Daten in das GTFS Format zu beauftragen. 
 
 In manchen Fällen erstellen kleine Agenturen mit einer Handvoll routes die Daten selbst und verwenden dazu allgemein verfügbare Software wie Tabellenkalkulationen und Texteditoren. 
 
 Wenn es um einen größeren Systemumfang geht, erwerben die meisten Agenturen spezielle GTFS Verwaltungssoftware von spezialisierten Anbietern, einige entscheiden sich jedoch für die Entwicklung eigener interner Tools. Wenn sich die Systemeigenschaften für Agenturen als Herausforderung erweisen, selbst Datensätze zu schreiben, kann die GTFS Produktion vollständig an Unternehmen ausgelagert werden, die auf die Produktion von GTFS Daten spezialisiert sind. 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Icons von Freepik">Von Freepik erstellte Symbole – Flaticon</a> 
 
 [^1]: Zusätzlich zu Textdateien wird in GTFS jetzt auch das [GeoJSON](https://geojson.org/)-Format unterstützt, um bestimmte Elemente von bedarfsgesteuerten Diensten darzustellen. 
 

