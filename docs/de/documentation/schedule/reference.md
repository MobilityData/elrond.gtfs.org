## General Transit Feed Specification 
 
 **Überarbeitet am 22. Mai 2024. Weitere Einzelheiten finden Sie im [Revisionsverlauf](../change_history/revision_history).** 
 
 Dieses Dokument definiert das Format und die Struktur der Dateien, aus denen ein GTFS Datensatz besteht. 
 
## Inhaltsverzeichnis 
 
 1. [Dokumentkonventionen](#document-conventions) 
 2. [Datensatzdateien](#dataset-files) 
 3. [Dateianforderungen](#file-requirements) 
 4. [Datensatzveröffentlichung und allgemeine Vorgehensweisen](#dataset-publishing-general-practices) 
 5. [Felddefinitionen](#field-definitions) 
 - [agency.txt](#agencytxt) 
 - [stops.txt](#stopstxt) 
 - [routes.txt](#routestxt) 
 - [trips.txt](#tripstxt) 
 - [stop\_times.txt](#stop_timestxt) 
 - [calendar.txt](#calendartxt) 
 - [Kalender\_Daten.txt](#calendar_datestxt) 
 - [Tarif\_Attribute.txt](#fare_attributestxt) 
 - [Tarif\_Regeln.txt](#fare_rulestxt) 
 - [Zeitrahmen.txt](#timeframestxt) 
 - [Tarif\_Medien.txt](#fare_mediatxt) 
 - [Tarif\_Produkte.txt](#fare_productstxt) 
 - [Tarif\_Leg\_Regeln.txt](#fare_leg_rulestxt) 
 - [Fahrpreis\_Transfer\_Regeln.txt](#Fahrpreis_Transfer_Regeln) 
 - [areas.txt](#Bereichext) 
 - [stop_areas.txt](#Haltestellen_Bereiche) 
 - [Netzwerke.txt](#Netzwerktxt) 
 - [Routennetzwerke.txt](#Routennetzwerktxt) 
 - [shapes.txt](#Formestxt) 
 - [frequencies.txt](#Frequenzentxt) 
 - [transfers.txt](#Transferstxt) 
 - [pathways.txt](#Wegestxt) 
 - [levels.txt](#Ebenenstxt) 
 - [location_groups.txt](#location_groupstxt) 
 - [location_group_stops.txt](#location_group_stopstxt) 
 - [locations.geojson](#locationsgeojson) 
 - [booking_rules.txt](#booking_rulestxt) 
 - [translations.txt](#translationstxt) 
 - [feed\_info.txt](#feed_infotxt) 
 - [attributions.txt](#attributionstxt) 
 
## Dokumentkonventionen 
 Die Schlüsselwörter "MUSS", "DARF NICHT", "ERFORDERLICH", "SOLL", "SOLL NICHT", "SOLLTE", "SOLLTE NICHT", "EMPFOHLEN", "KANN" und „OPTIONAL“ in diesem Dokument ist wie in [RFC 2119](https:) beschrieben zu interpretieren. 
 
 
### Begriffsdefinitionen 
 
 Dieser Abschnitt definiert Begriffe, die in diesem Dokument verwendet werden. 
 
 * **Datensatz** – Ein vollständiger Satz von Dateien, die in dieser Spezifikationsreferenz definiert sind. Durch Ändern des Datensatzes wird eine neue Version des Datensatzes erstellt. Datensätze sollten unter einer öffentlichen, permanenten URL veröffentlicht werden, einschließlich des ZIP-Dateinamens (z. B. agency). 
 * **Datensatz** – Eine grundlegende Datenstruktur, die aus mehreren verschiedenen Feldwerten besteht, die eine einzelne entity beschreiben (z. B. agency, Haltestelle, Route usw.). In einer Tabelle als Zeile dargestellt. 
 * **Feld** – Eine Eigenschaft eines Objekts oder einer entity. In einer Tabelle als Spalte dargestellt. Das Feld ist vorhanden, wenn es einer Datei als header hinzugefügt wird. Es können Feldwerte definiert sein, aber das muss nicht sein. 
 * **Feldwert** – Ein einzelner Eintrag in einem Feld. In einer Tabelle als einzelne Zelle dargestellt. 
 * **Betriebstag** – Ein Betriebstag ist ein Zeitraum zur Angabe der Routenplanung. Die genaue Definition eines Betriebstags ist von agency zu agency unterschiedlich, aber Betriebstage entsprechen oft nicht den Kalendertagen. Ein Betriebstag kann 24:00:00 überschreiten, wenn der Betrieb an einem Tag beginnt und am folgenden Tag endet. So könnte beispielsweise ein Betrieb, der freitags von 08:00:00 bis samstags von 02:00:00 fährt, als ein einziger Betriebstag von 08:00:00 bis 26:00:00 fahrend gekennzeichnet werden. 
 * **Text-to-Speech-Feld** – Das Feld sollte dieselben Informationen enthalten wie sein übergeordnetes Feld (auf das es zurückgreift, wenn es leer ist). Es soll als Text-to-Speech gelesen werden, daher sollten Abkürzungen entweder entfernt werden („St“ sollte entweder als „Street“ oder „Saint“ gelesen werden; „Elizabeth I“ sollte als „Elizabeth the First“ gelesen werden) oder beibehalten werden, damit sie so gelesen werden, wie sie sind („JFK Airport“ wird abgekürzt gesagt). 
 * **Teilstrecke** – Reise, bei der ein Fahrgast während einer Reise zwischen zwei aufeinanderfolgenden Orten ein- und aussteigt. 
 * **Reise** – Gesamtreise vom Ausgangs- zum Zielort, einschließlich aller Teilstrecken und transfers dazwischen. 
 * **Teilreise** – Zwei oder mehr Teilstrecken, die eine Teilmenge einer Reise bilden. 
 * **Fahrpreisprodukt** – Kaufbare Fahrpreisprodukte, die zum Bezahlen oder Validieren von Reisen verwendet werden können. 
 
### Vorhandensein 
 Für Felder und Dateien geltende Vorhandenseinsbedingungen: 
 
 * **Erforderlich** – Das Feld oder die Datei muss im Datensatz enthalten sein und für jeden Datensatz einen gültigen Wert enthalten. 
 * **Optional** – Das Feld oder die Datei kann aus dem Datensatz weggelassen werden. 
 * **Bedingt erforderlich** – Das Feld oder die Datei muss unter den in der Feld- oder Dateibeschreibung beschriebenen Bedingungen enthalten sein. 
 * **Bedingt verboten** – Das Feld oder die Datei darf nicht unter den in der Feld- oder Dateibeschreibung beschriebenen Bedingungen enthalten sein. 
 * **Empfohlen** – Das Feld oder die Datei kann aus dem Datensatz weggelassen werden, es hat sich jedoch bewährt, sie aufzunehmen. Vor dem Weglassen dieses Felds oder dieser Datei sollte die bewährte Vorgehensweise sorgfältig geprüft und die gesamten Auswirkungen des Weglassens verstanden werden. 
 
### Feldtypen- **Farbe** - Eine Farbe, die als sechsstellige Hexadezimalzahl kodiert ist. Informationen zum Generieren eines gültigen Werts finden Sie unter [https://htmlcolorcodes.com](https://htmlcolorcodes.com) (das führende „#“ darf nicht enthalten sein).<br> *Beispiel: `FFFFFF für Weiß, `000000` für Schwarz oder `0039A6 für die Zeilen A, C, E in NYMTA.* 
 - **Währungscode** - Ein alphabetischer currency nach ISO 4217. Die Liste der aktuellen currency finden Sie unter [https://en.wikipedia.org/wiki/ISO_4217#Active\_codes](https://en.wikipedia.org/wiki/ISO_4217#Active_codes).<br> *Beispiel: „CAD“ für Kanadische Dollar, „EUR“ für Euro oder „JPY“ für Japanische Yen.* 
 - ** amount ** - Ein Dezimalwert, der einen currency angibt. Die Anzahl der Dezimalstellen wird durch [ISO 4217](https:) für den zugehörigen Währungscode angegeben. Alle Finanzberechnungen sollten als Dezimalzahlen, currency oder einen anderen gleichwertigen, für Finanzberechnungen geeigneten Typ verarbeitet werden, je nach der zum Verwenden der Daten verwendeten Programmiersprache. Von der Verarbeitung von currency als float wird abgeraten, da während der Berechnungen Geldgewinne oder-verluste auftreten können. 
 - **Datum** - Werktag im Format JJJJMMTT. Da die Zeit innerhalb eines Werktags über 24:00:00 liegen kann, kann ein Werktag Informationen für den/die darauffolgenden Tag(e) enthalten.<br> *Beispiel: „20180913“ für den 13. September 2018.* 
 – ** Email** – Eine E-Mail-Adresse.<br> *Beispiel: `example@example.com`* 
 - **Enum** - Eine Option aus einer Reihe vordefinierter Konstanten, die in der Spalte „Beschreibung“ definiert sind.<br> *Beispiel: Das Feld `route_type enthält eine `0` für Straßenbahn, eine `1` für U-Bahn...* 
 - **ID** - Ein ID-Feldwert ist eine interne ID, die nicht für die Anzeige an Fahrgäste vorgesehen ist, und ist eine Folge beliebiger UTF-8-Zeichen. Es wird empfohlen, nur druckbare ASCII-Zeichen zu verwenden. Eine ID wird als „eindeutige ID“ bezeichnet, wenn sie innerhalb einer Datei eindeutig sein muss. Auf IDs, die in einer.txt Datei definiert sind, wird häufig in einer anderen.txt Datei verwiesen. IDs, die auf eine ID in einer anderen Tabelle verweisen, werden als „fremde ID“ bezeichnet.<br> *Beispiel: Das Feld `stop_id` in [stops.txt](#stopstxt) ist eine „eindeutige ID“. Das Feld `parent_station in [stops.txt](#stopstxt) ist eine „fremde ID, die auf `stops.stop_id verweist“.* 
 - **Sprachcode** - Ein IETF BCP 47-Sprachcode. Eine Einführung in IETF BCP 47 finden Sie unter [http://www.rfc-editor.org/rfc/bcp/bcp47 .txt](http://www.rfc-editor.org/rfc/bcp/bcp47 .txt) und [http://www.w3.org/International/articles/language-tags/](http://www.w3.org/International/articles/language-tags/).<br> *Beispiel: `en` für Englisch, `en-US` für amerikanisches Englisch oder `de` für Deutsch.* 
 - **Latitude** - WGS84- latitude in Dezimalgrad. Der Wert muss größer oder gleich-90,0 und kleiner oder gleich 90,0 sein. *<br> Beispiel: `41.890169` für das Kolosseum in Rom.* 
 - **Längengrad** - WGS84- longitude in Dezimalgrad. Der Wert muss größer oder gleich-180,0 und kleiner oder gleich 180,0 sein.<br> *Beispiel: `12.492269` für das Kolosseum in Rom.* 
 - ** Float** - Eine Gleitkommazahl. 
 - ** Integer** - Eine Ganzzahl. 
 - ** Phone number** - Eine Telefonnummer. 
 - ** Zeit** - Zeit im Format HH:MM:SS (H:MM:SS wird ebenfalls akzeptiert). Die Zeit wird von „Mittag minus 12 Uhr“ des Werktags (tatsächlich Mitternacht, außer an Tagen mit Sommerzeitumstellung) gemessen. Für Zeiten nach Mitternacht am Werktag geben Sie die Zeit als Wert größer als 24:00:00 im Format HH:MM:SS ein.<br> *Beispiel: `14:30:00` für 14:30 Uhr oder `25:35:00` für 1:35 Uhr am nächsten Tag.* 
 - ** Text** - Eine string aus UTF-8-Zeichen, die angezeigt werden soll und daher für Menschen lesbar sein muss. 
 - **Zeitzone** - TZ-Zeitzone aus [https://www.iana.org/time-zones](https://www.iana.org/time-zones). Zeitzonennamen enthalten niemals Leerzeichen, können aber einen Unterstrich enthalten. Eine Liste gültiger Werte finden Sie unter [http://en.wikipedia.org/wiki/List\_of\_tz\_zones](http://en.wikipedia.org/wiki/List\_of\_tz\_zones).<br> *Beispiel: `Asia/Tokyo`, `America/Los_Angeles` oder `Africa/Cairo`.* 
 - ** URL** - Eine vollqualifizierte URL, die http://oder https://enthält, und alle Sonderzeichen in der URL müssen korrekt maskiert werden. Eine Beschreibung zum Erstellen vollqualifizierter URL Werte finden Sie unter [http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html](http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html). 
 
### Feldzeichen 
 Für die Feldtypen Float oder Integer geltende Zeichen: 
 
 * **Nicht-negativ** – Größer oder gleich 0. 
 * **Ungleich 0** – Ungleich 0. 
 * **Positiv** – Größer als 0. 
 
 _Beispiel: **Nicht-negativer float** – Eine Gleitkommazahl größer oder gleich 0._ 
 
### Datensatzattribute 
 Der **Primärschlüssel** eines Datensatzes ist das Feld oder die Kombination von Feldern, die eine Zeile eindeutig identifizieren. „Primary key (*)“ wird verwendet, wenn alle bereitgestellten Felder einer Datei zur eindeutigen Identifizierung einer Zeile verwendet werden. „Primary key (none)“ bedeutet, dass die Datei nur eine Zeile zulässt. 
 
 _Beispiel: Die Felder „`trip_id`“ und „`stop_sequence`“ bilden den Primärschlüssel von [stop_times.txt](#stop_timestxt)._ 
 
## Datensatzdateien 
 
 Diese Spezifikation definiert die folgenden Dateien: 
 
 | Dateiname | Vorhandensein | Beschreibung | 
 |------|------|------| 
 | [agency.txt](#agencytxt) | **Erforderlich** | Verkehrsunternehmen mit Service, die in diesem Datensatz vertreten sind. | 
 | [stops.txt](#stopstxt) | **Erforderlich** | Haltestellen, an denen Fahrzeuge Fahrgäste aufnehmen oder absetzen. Definiert außerdem Bahnhöfe und Bahnhofseingänge. | 
 | [routes.txt](#routestxt) | **Erforderlich** | routes. Eine Route ist eine Gruppe von Fahrten, die Fahrgästen als einzelne Dienstleistung angezeigt werden. | 
 | [trips.txt](#tripstxt) | **Erforderlich** | Fahrten für jede Route. Eine Fahrt ist eine Abfolge von zwei oder mehr stops, die während eines bestimmten Zeitraums erfolgen. | 
 | [stop_times.txt](#stop_timestxt) | **Erforderlich** | Ankunfts- und Abfahrtszeiten eines vehicle bei jeder Fahrt an stops. | 
 | [calendar.txt](#calendartxt) | **Bedingt erforderlich** | Dienstleistungsdaten, die anhand eines Wochenplans mit Start- und Enddatum angegeben werden.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, sofern nicht alle Leistungsdaten in [calendar_dates.txt](#calendar_datestxt) definiert sind.<br> – Andernfalls optional. | 
 | [calendar_dates.txt](#calendar_datestxt) | **Bedingt erforderlich** | Ausnahmen für die in [calendar.txt](#calendartxt) definierten Dienste.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn [calendar.txt](#calendartxt) weggelassen wird. In diesem Fall muss [calendar_dates.txt](#calendar_datestxt) alle Dienstdaten enthalten.<br> – Andernfalls optional. | 
 | [fare_attributes.txt](#fare_attributestxt) | Optional | Tarifinformationen für die routes eines Verkehrsunternehmens. | 
 | [fare_rules.txt](#fare_rulestxt) | Optional | Regeln zum Anwenden von Tarifen auf Reiserouten. | 
 | [timeframes.txt](#timeframestxt) | Optional | In Tarifregeln zu verwendende Datums- und Zeiträume für Tarife, die von date und Zeitfaktoren abhängen. | 
 | [fare_media.txt](#fare_mediatxt) | Optional | Zur Beschreibung der Tarifmedien, die zur Verwendung von Tarifprodukten eingesetzt werden können.<br><br> Die Datei [fare_media.txt](#fare_mediatxt) beschreibt Konzepte, die in [fare_attributes.txt](#fare_attributestxt) und [fare_rules.txt](#fare_rulestxt) nicht dargestellt sind. Daher ist die Verwendung von [fare_media.txt](#fare_mediatxt) völlig unabhängig von den Dateien [fare_attributes.txt](#fare_attributestxt) und [fare_rules.txt](#fare_rulestxt). | 
 | [fare_products.txt](#fare_productstxt) | Optional | Zur Beschreibung der unterschiedlichen Ticketarten oder Fahrpreise, die von Fahrgästen erworben werden können.<br><br> Die Datei [fare_products.txt](#fare_productstxt) beschreibt Tarifprodukte, die nicht in [fare_attributes.txt](#fare_attributestxt) und [fare_rules.txt](#fare_rulestxt) dargestellt sind. Daher ist die Verwendung von [fare_products.txt](#fare_productstxt) völlig unabhängig von den Dateien [fare_attributes.txt](#fare_attributestxt) und [fare_rules.txt](#fare_rulestxt). | 
 | [fare_leg_rules.txt](#fare_leg_rulestxt) | Optional | Tarifregeln für einzelne Reiseabschnitte.<br><br> Die Datei [fare_leg_rules.txt](#fare_leg_rulestxt) bietet eine detailliertere Methode zur Modellierung von Tarifstrukturen. Daher ist die Verwendung von [fare_leg_rules.txt](#fare_leg_rulestxt) völlig unabhängig von den Dateien [fare_attributes.txt](#fare_attributestxt) und [fare_rules.txt](#fare_rulestxt). | 
 | [fare_transfer_rules.txt](#fare_transfer_rulestxt) | Optional | Tarifregeln für transfers zwischen Reiseabschnitten.<br><br> Neben [fare_leg_rules.txt](#fare_leg_rulestxt) bietet die Datei [fare_transfer_rules.txt](#fare_transfer_rulestxt) eine detailliertere Methode zur Modellierung von Tarifstrukturen. Daher ist die Verwendung von [fare_transfer_rules.txt](#fare_transfer_rulestxt) völlig unabhängig von den Dateien [fare_attributes.txt](#fare_attributestxt) und [fare_rules.txt](#fare_rulestxt). | 
 | [areas.txt](#areastxt) | Optional | Bereichsgruppierung von Standorten. | 
 | [stop_areas.txt](#stop_areastxt) | Optional | Regeln zur Zuweisung von stops zu Bereichen. | 
 | [networks.txt](#networkstxt) | **Bedingt verboten** | Netzwerkgruppierung von routes.<br><br> Bedingt verboten:<br> - **Verboten**, wenn „network_id“ in [routes.txt](#routestxt) vorhanden ist.<br> – Andernfalls optional. | 
 | [route_networks.txt](#route_networkstxt) | **Bedingt verboten** | Regeln zum Zuweisen von routes zu Netzwerken.<br><br> Bedingt verboten:<br> - **Verboten**, wenn „network_id“ in [routes.txt](#routestxt) vorhanden ist.<br> – Andernfalls optional. | 
 | [shapes.txt](#shapestxt) | Optional | Regeln zum Zuordnen von vehicle, manchmal auch als Routenausrichtung bezeichnet. | 
 | [frequencies.txt](#frequenciestxt) | Optional | Taktabstand (Zeit zwischen Fahrten) für taktabstandsbasierten Service oder eine komprimierte Darstellung von Service mit festem Fahrplan. | 
 | [transfers.txt](#transferstxt) | Optional | Regeln zum Herstellen von Verbindungen an Umsteigepunkten zwischen routes. | 
 | [pathways.txt](#pathwaystxt) | Optional | Wege, die Orte innerhalb von Bahnhöfen miteinander verbinden. | 
 | [levels.txt](#levelstxt) | **Bedingt erforderlich** | Ebenen innerhalb von Bahnhöfen.<br><br> Bedingt erforderlich:<br> - **Erforderlich** bei der Beschreibung von pathways mit Aufzügen (`pathway_mode=5`).<br> – Andernfalls optional. | 
 | [location_groups.txt](#location_groupstxt) | Optional | Eine Gruppe von stops, die zusammen Standorte anzeigen, an denen ein Fahrgast eine Abholung oder einen Abtransport anfordern kann. | 
 | [location_group_stops.txt](#location_group_stopstxt) | Optional | Regeln zum Zuweisen von stops zu Standortgruppen. | 
 | [locations.geojson](#locationsgeojson) | Optional | Zonen für Abhol- oder Abtransportanfragen von Fahrgästen durch On-Demand-Dienste, dargestellt als GeoJSON-Polygone. | ​​
 | [booking_rules.txt](#booking_rulestxt) | Optional | Buchungsinformationen für vom Fahrgast angeforderte Dienste. | 
 | [translations.txt](#translationstxt) | Optional | Übersetzungen von kundenseitigen Datensatzwerten. | 
 | [feed_info.txt](#feed_infotxt) | Optional | Metadaten des Datensatzes, einschließlich Herausgeber, Version und Ablaufinformationen. | 
 | [attributions.txt](#attributionstxt) | Optional | attributions. | 
 
## Dateianforderungen 
 
 Für das Format und den Inhalt der Datensatzdateien gelten die folgenden Anforderungen: 
 
 * Alle Dateien müssen als Komma-getrennter Text gespeichert werden. 
 * Die erste Zeile jeder Datei muss Feldnamen enthalten. Jeder Unterabschnitt des Abschnitts [Felddefinitionen](#field-definitions) entspricht einer der Dateien in einem GTFS Datensatz und listet die Feldnamen auf, die in dieser Datei verwendet werden dürfen. 
 * Bei allen Datei- und Feldnamen muss die Groß-/Kleinschreibung beachtet werden. 
 * Feldwerte dürfen keine Tabulatoren, Wagenrückläufe oder neue Zeilen enthalten. 
 * Feldwerte, die Anführungszeichen oder Kommas enthalten, müssen in Anführungszeichen eingeschlossen werden. Außerdem muss jedem Anführungszeichen im Feldwert ein Anführungszeichen vorangestellt werden. Dies entspricht der Art und Weise, in der Microsoft Excel Komma-getrennte (CSV-)Dateien ausgibt. Weitere Informationen zum CSV-Dateiformat finden Sie unter [http://tools.ietf.org/html/rfc4180](http://tools.ietf.org/html/rfc4180). 
 Das folgende Beispiel zeigt, wie ein Feldwert in einer Komma-getrennten Datei aussehen würde: 
 * **Ursprünglicher Feldwert:** `Contains "quotes", commas and text` 
 * **Feldwert in CSV-Datei:** `"Contains ""quotes"", commas and text"` 
 * Feldwerte dürfen keine HTML-Tags, Kommentare oder Escape-Sequenzen enthalten. 
 * Zusätzliche Leerzeichen zwischen Feldern oder Feldnamen sollten entfernt werden. Viele Parser betrachten die Leerzeichen als Teil des Wertes, was zu Fehlern cause kann. 
 * Jede Zeile muss mit einem CRLF- oder LF-Zeilenumbruchzeichen enden. 
 * Dateien sollten in UTF-8 kodiert sein, um alle Unicode-Zeichen zu unterstützen. Dateien, die das Unicode-Byte-Order-Mark-Zeichen (BOM) enthalten, sind zulässig. Weitere Informationen zum BOM-Zeichen und zu UTF-8 finden Sie unter [http://unicode.org/faq/utf_bom.html#BOM](http://unicode.org/faq/utf_bom.html#BOM). 
 * Alle Dataset-Dateien müssen zusammen gezippt werden. Die Dateien müssen direkt auf der Stammebene liegen, nicht in einem Unterordner. 
 * Alle für Kunden sichtbaren Textzeichenfolgen (einschließlich Haltestellennamen, Routennamen und Hinweisschilder) sollten in Groß- und Kleinschreibung (nicht NUR GROSSBUCHSTABEN) geschrieben werden und den lokalen Konventionen für die Groß- und Kleinschreibung von Ortsnamen auf Displays entsprechen, die Kleinbuchstaben anzeigen können (z. B. „Brighton Churchill Square“, „Villiers-sur-Marne“, „Market Street“). 
 * Die Verwendung von Abkürzungen für Namen und anderen Text (z. B. St.für Straße) sollte im gesamten Feed vermieden werden, sofern ein Ort nicht mit seinem abgekürzten Namen bezeichnet wird (z. B. „JFK Airport“). Abkürzungen können für die Zugänglichkeit durch Bildschirmlesesoftware und Sprachbenutzeroberflächen problematisch sein. Konsumierende Software kann so konstruiert werden, dass sie vollständige Wörter für die Anzeige zuverlässig in Abkürzungen umwandelt, aber die Konvertierung von Abkürzungen in vollständige Wörter birgt ein höheres Fehlerrisiko. 
 
## Veröffentlichung von Datensätzen und allgemeine Vorgehensweisen 
 
 * Datensätze sollten unter einer öffentlichen, permanenten URL veröffentlicht werden, einschließlich des ZIP-Dateinamens. (z. B. agency). Im Idealfall sollte die URL direkt herunterladbar sein, ohne dass ein Login zum Zugriff auf die Datei erforderlich ist, um den Download durch Softwareanwendungen zu erleichtern. Obwohl es empfohlen wird (und die gängigste Vorgehensweise ist), einen GTFS Datensatz offen herunterladbar zu machen, wird empfohlen, den Zugriff auf den GTFS Datensatz mithilfe von API-Schlüsseln zu kontrollieren, wenn ein Datenanbieter den Zugriff auf GTFS aus Lizenzierungs- oder anderen Gründen kontrollieren muss, was automatische Downloads erleichtert. 
 * GTFS Daten sollten in Iterationen veröffentlicht werden, sodass eine einzelne Datei an einem stabilen Speicherort immer die neuste offizielle Servicebeschreibung eines agency (oder mehrerer Verkehrsunternehmen) enthält. 
 * Datensätze sollten wenn möglich persistente Kennungen (id Felder) für „`stop_id`“, „`route_id`“ und „agency_id“ über Dateniterationen hinweg beibehalten. 
 * Ein GTFS Datensatz sollte aktuelle und kommende Dienste enthalten (manchmal auch „zusammengeführter“ Datensatz genannt). Es stehen mehrere [Merge-Tools](../../../resources/gtfs/#gtfs-merge-tools) zur Verfügung, mit denen ein zusammengeführter Datensatz aus zwei verschiedenen GTFS Feeds erstellt werden kann. 
 * Der veröffentlichte GTFS Datensatz sollte jederzeit mindestens die nächsten 7 Tage gültig sein und im Idealfall so lange, wie der Betreiber davon überzeugt ist, dass der Fahrplan weiterhin eingehalten wird. 
 * Der GTFS Datensatz sollte nach Möglichkeit mindestens die nächsten 30 Tage des Betriebs abdecken. 
 * Alte Services (abgelaufene Kalender) sollten aus dem Feed entfernt werden. 
 * Wenn eine Serviceänderung in 7 Tagen oder weniger in Kraft tritt, sollte diese Serviceänderung über einen GTFS-Echtzeit-Feed (Servicehinweise oder Fahrtaktualisierungen) und nicht über einen statischen GTFS Datensatz ausgedrückt werden. 
 * Der Webserver, auf dem die GTFS Daten gehostet werden, sollte so konfiguriert sein, dass das date der Datei korrekt gemeldet wird (siehe [HTTP/1.1 – Request for Comments 2616, unter Abschnitt 14.29](https:)). 
 
## Felddefinitionen### agency.txt 
 
 Datei: **Erforderlich** 
 
 Primärschlüssel (`agency_id`) 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `agency_id` | Eindeutige ID | **Bedingt erforderlich** | Identifiziert eine Transitmarke, die oft gleichbedeutend mit einer agency ist. Beachten Sie, dass in manchen Fällen, z. B. wenn eine einzelne agency mehrere separate Dienste betreibt, Agenturen und Marken unterschiedlich sind. In diesem Dokument wird der Begriff „agency“ anstelle von „Marke“ verwendet. Ein Datensatz kann Daten von mehreren Agenturen enthalten.<br><br> Bedingt erforderlich:<br> – **Erforderlich**, wenn der Datensatz Daten für mehrere Verkehrsbetriebe enthält.<br> – Andernfalls empfohlen. | 
 | „agency_name“ | Text | **Erforderlich** | Vollständiger Name des agency. | 
 | „agency_url“ | URL | **Erforderlich** | URL des agency. | 
 | „agency_timezone“ | Zeitzone | **Erforderlich** | Zeitzone, in der sich das agency befindet. Wenn im Datensatz mehrere Unternehmen angegeben sind, muss jedes die gleiche „agency_timezone“ haben. | 
 | „agency_lang“ | Sprachcode | Optional | Primäre Sprache dieses agency. Sollte bereitgestellt werden, um GTFS Verbrauchern die Auswahl von Groß- und Kleinschreibungsregeln und anderen sprachspezifischen Einstellungen für den Datensatz zu erleichtern. | 
 | „agency_phone“ | Phone number | Optional | Eine Telefonummer für die angegebene agency. Dieses Feld ist ein string, der die Telefonnummer als typisch für das Servicegebiet des Unternehmens darstellt. Es kann Satzzeichen enthalten, um die Ziffern der Nummer zu gruppieren. Wählbarer Text (zum Beispiel „503-238-RIDE“ von TriMet) ist zulässig, das Feld darf jedoch keinen anderen beschreibenden Text enthalten. | 
 | „agency_fare_url“ | URL | Optional | URL einer Webseite, auf der ein Fahrgast online Fahrkarten oder andere Fahrkarteninstrumente für dieses agency kaufen kann. | 
 | „agency_email“ | Email | Optional | Email Adresse, die von der Kundendienstabteilung des Reisebüros aktiv überwacht wird. Diese E-Mail-Adresse sollte eine direkte Kontaktstelle sein, über die Fahrgäste einen Kundendienstmitarbeiter des agency erreichen können. | 
 
### stops.txt 
 
 Datei: **Erforderlich** 
 
 Primärschlüssel („`stop_id`“) 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `stop_id` | Eindeutige ID | **Erforderlich** | Identifiziert einen Standort: Haltestelle/Bahnsteig, Bahnhof, Eingang/Ausgang, allgemeiner Knoten oder Einstiegsbereich (siehe `location_type`).<br><br> Die ID muss für alle Werte „stops.stop_id“, „ locations.geojson `id`“ und „location_groups.location_group_id“ eindeutig sein.<br><br> Mehrere routes können dieselbe „`stop_id`“ verwenden. | 
 | „stop_code“ | Text | Optional | Kurztext oder Nummer, die den Standort für Fahrgäste identifiziert. Diese Codes werden häufig in telefonischen Transitinformationssystemen verwendet oder auf Schilder gedruckt, um Fahrgästen das Abrufen von Informationen zu einem bestimmten Standort zu erleichtern. Der „stop_code“ kann bei öffentlichen Verkehrsmitteln mit der „`stop_id`“ identisch sein. Für Standorte ohne Code, der den Fahrgästen angezeigt wird, sollte dieses Feld leer gelassen werden. | 
 | „stop_name“ | Text | **Bedingt erforderlich** | Name des Standorts. Der „stop_name“ sollte mit dem für Fahrgäste sichtbaren Namen des Unternehmens für den Standort übereinstimmen, wie er auf einem Fahrplan aufgedruckt, online veröffentlicht oder auf Schildern angegeben ist. Verwenden Sie für Übersetzungen in andere Sprachen [translations.txt](#translationstxt).<br><br> Wenn der Standort ein Einstiegsbereich ist (`location_type=4`), sollte der `stop_name` den Namen des Einstiegsbereichs enthalten, wie er von der agency angezeigt wird. Dies kann nur ein Buchstabe sein (wie bei einigen europäischen Intercity-Bahnhöfen) oder ein Text wie „Einstiegsbereich für Rollstuhlfahrer“ (U-Bahn von New York City) oder „Leiter von Kurzzügen“ (RER von Paris).<br><br> Bedingt erforderlich:<br> - **Erforderlich** für Standorte, die stops (`location_type=0`), Bahnhöfe (`location_type=1`) oder Ein-/Ausgänge (`location_type=2`) sind.<br> - Optional für Standorte, die generische Knoten (`location_type=3`) oder Einstiegsbereiche (`location_type=4`) sind.| 
 | `tts_stop_name` | Text | Optional | Lesbare Version von `stop_name`. Weitere Informationen finden Sie unter „Text-to-Speech-Feld“ in den [Begriffsdefinitionen](#term-definitions). | 
 | `stop_desc` | Text | Optional | Beschreibung des Standorts, die nützliche, hochwertige Informationen bietet. Sollte kein Duplikat von `stop_name` sein.| 
 | ` stop

lat` | Breitengrad | **Bedingt erforderlich** | Breitengrad des Standorts.<br><br> Bei stops/Bahnsteigen (`location_type=0) und Einstiegsbereichen (`location_type=4) müssen die Koordinaten diejenigen des Busmasts sein — sofern vorhanden — und ansonsten die Koordinaten der Stelle, an der die Reisenden in das vehicle einsteigen (auf dem Gehweg oder Bahnsteig und nicht auf der Fahrbahn oder dem Gleis, an der das vehicle stops).<br><br> Bedingt erforderlich:<br> - **Erforderlich** für Standorte, die stops (`location_type=0`), Bahnhöfe (`location_type=1`) oder Ein-/Ausgänge (`location_type=2`) sind.<br> - Optional für Standorte, die generische Knoten (`location_type=3`) oder Einstiegsbereiche (`location_type=4`) sind.| 
 | `stop_lon` | Längengrad | **Bedingt erforderlich** | Längengrad des Standorts.<br><br> Bei stops/Bahnsteigen (`location_type=0) und Einstiegsbereichen (`location_type=4) müssen die Koordinaten diejenigen des Busmasts sein — sofern vorhanden — und ansonsten die Koordinaten der Stelle, an der die Reisenden in das vehicle einsteigen (auf dem Gehweg oder Bahnsteig und nicht auf der Fahrbahn oder dem Gleis, an der das vehicle stops).<br><br> Bedingt erforderlich:<br> - **Erforderlich** für Standorte, die stops (`location_type=0`), Bahnhöfe (`location_type=1`) oder Ein-/Ausgänge (`location_type=2`) sind.<br> - Optional für Standorte, die generische Knoten (`location_type=3`) oder Einstiegsbereiche (`location_type=4`) sind. | 
 | `zone_id` | ID | Optional | Identifiziert die Tarifzone für eine Haltestelle. Wenn dieser Datensatz einen Bahnhof oder einen Bahnhofseingang darstellt, wird die `zone_id` ignoriert.| 
 | `stop_url` | URL | Optional | URL einer Webseite über den Standort. Dies sollte sich von den Feldwerten `agency.agency_url` und `routes.route_url` unterscheiden. | 
 | `location_type` | Enum | Optional | Standorttyp. Gültige Optionen sind:<br><br> `0` (oder leer) - **Haltestelle** (oder **Bahnsteig**). Ein Ort, an dem Passagiere in ein vehicle einsteigen oder aussteigen. Wird als Bahnsteig bezeichnet, wenn er innerhalb einer `parent_station` definiert ist.<br> `1` - **Station**. Eine physische Struktur oder ein Bereich, der einen oder mehrere Bahnsteige enthält.<br> `2` - **Eingang/Ausgang**. Ein Ort, an dem Passagiere einen Bahnhof von der Straße aus betreten oder verlassen können. Wenn ein Eingang/Ausgang zu mehreren Bahnhöfen gehört, kann er durch pathways mit beiden verbunden sein, aber der Datenanbieter muss einen davon als übergeordneten Ort auswählen.<br> `3` - **Allgemeiner Knoten**. Ein Standort innerhalb einer Station, der keinem anderen `location_type entspricht und der verwendet werden kann, um in [pathways.txt](#pathwaystxt) definierte pathways miteinander zu verknüpfen.<br> `4` - **Einstiegsbereich**. Ein bestimmter Ort auf einem Bahnsteig, an dem Passagiere in Fahrzeuge ein- und aussteigen können.| 
 | ` parent_station` | Ausländische ID mit Verweis auf `stops.stop_id` | **Bedingt erforderlich** | Definiert die Hierarchie zwischen den verschiedenen Orten, die in [stops.txt](#stopstxt) definiert sind. Es enthält die ID des übergeordneten Ortes wie folgt:<br><br> - **Haltestelle/Bahnsteig** (`location_type=0`): Das Feld `parent_station` enthält die ID einer Station.<br> - **Station** (`location_type=1`): Dieses Feld muss leer sein.<br> - **Ein-/Ausgang** (`location_type=2`) oder **generischer Knoten** (`location_type=3`): das Feld `parent_station` enthält die ID einer Station (`location_type=1`)<br> - **Einstiegsbereich** (`location_type=4`): Das Feld `parent_station` enthält die ID eines Bahnsteigs.<br><br> Bedingt erforderlich:<br> - **Erforderlich** für Standorte, die Eingänge (`location_type=2`), allgemeine Knoten (`location_type=3`) oder Einstiegsbereiche (`location_type=4`) sind.<br> - Optional für stops/Bahnsteige (`location_type=0).<br> - Verboten für Stationen (`location_type=1`).| 
 | `stop_timezone` | Zeitzone | Optional | Zeitzone des Standorts. Wenn der Standort eine übergeordnete Station hat, erbt er die Zeitzone der übergeordneten Station, anstatt seine eigene anzuwenden. Stationen und übergeordnete stops mit leerer `stop_timezone` erben die von `agency.agency_timezone` angegebene Zeitzone. Die in [stop_times.txt](#stop_timestxt) angegebenen Zeiten liegen in der von `agency.agency_timezone` angegebenen Zeitzone, nicht in `stop_timezone`. Dadurch wird sichergestellt, dass die Zeitwerte einer Fahrt im Laufe der Fahrt immer zunehmen, unabhängig davon, welche Zeitzonen die Fahrt durchquert. | 
 | `wheelchair_boarding` | Enum | Optional | Gibt an, ob Rollstuhlfahrer vom Standort aus einsteigen können. Gültige Optionen sind:<br><br> Für stops ohne Eltern:<br> „0“ oder leer – Keine Informationen zur Barrierefreiheit für die Haltestelle.<br> `1` - Einige Fahrzeuge an dieser Haltestelle sind für Rollstuhlfahrer zugänglich.<br> `2` - An dieser Haltestelle ist der Einstieg für Rollstuhlfahrer nicht möglich.<br><br> Für stops:<br> „0“ oder leer – die Haltestelle erbt ihr „wheelchair_boarding“-Verhalten von der übergeordneten Haltestelle, wenn es in der übergeordneten Haltestelle angegeben ist.<br> `1` – Es gibt einen barrierefreien Weg von außerhalb des Bahnhofs zur jeweiligen Haltestelle/zum jeweiligen Bahnsteig.<br> `2` - Es gibt keinen barrierefreien Weg von außerhalb des Bahnhofs zur jeweiligen Haltestelle/zum jeweiligen Bahnsteig.<br><br> Für Bahnhofsein-/ausgänge:<br> „0“ oder leer – Der Stationseingang erbt sein „wheelchair_boarding“-Verhalten von der übergeordneten Station, wenn dies für die übergeordnete Station angegeben ist.<br> `1` - Der Eingang der Station ist für Rollstuhlfahrer zugänglich.<br> `2` – Kein barrierefreier Weg vom Bahnhofseingang zu den stops/Bahnsteigen. | 
 | `level_id` | Ausländische ID, die auf `levels.level_id` verweist | Optional | Ebene des Standorts. Dieselbe Ebene kann von mehreren nicht verknüpften Bahnhöfen verwendet werden.| 
 | `platform_code` | Text | Optional | Bahnsteigkennung für eine Bahnsteighaltestelle (eine Haltestelle, die zu einem Bahnhof gehört). Dies sollte nur die Bahnsteigkennung sein (z. B. „G“ oder „3“). Wörter wie „Bahnsteig“ oder „Gleis“ (oder das sprachspezifische Äquivalent des Feeds) sollten nicht enthalten sein. Dadurch können Feed-Konsumenten die Bahnsteigkennung einfacher internationalisieren und in andere Sprachen lokalisieren. | 
 
 
### routes.txt 
 
 Datei: **Erforderlich** 
 
 Primärschlüssel (`route_id`) 
 
 | Feldname | Typ | Vorkommen | Beschreibung | 
 |------|------|------|------| 
 | `route_id` | Eindeutige ID | **Erforderlich** | Identifiziert eine Route. | 
 | `agency_id` | Fremd-ID mit Referenz auf `agency.agency_id` | **Bedingt erforderlich** | Agentur für die angegebene Route.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn mehrere Agenturen in [agency.txt](#agencytxt) definiert sind.<br> - Andernfalls empfohlen. | 
 | `route_short_name| Text | **Bedingt erforderlich** | Kurzname einer Route. Oft eine kurze, abstrakte Kennung (z. B. „32“, „100X“, „Grün“), die Fahrer verwenden, um eine Route zu identifizieren. Sowohl `route_short_name als auch `route_long_name können definiert werden.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn „routes.route_long_name“ leer ist.<br> - Empfohlen, wenn eine kurze Servicebezeichnung vorhanden ist. Dies sollte der allgemein bekannte Passagiername des Dienstes sein und nicht länger als 12 Zeichen sein. | 
 | `route_long_name` | Text | **Bedingt erforderlich** | Vollständiger Name einer Route. Dieser Name ist im Allgemeinen aussagekräftiger als der `route_short_name` und enthält häufig das Ziel oder die Haltestelle der Route. Sowohl `route_short_name` als auch `route_long_name` können definiert werden.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn „routes.route_short_name“ leer ist.<br> – Andernfalls optional. | 
 | „route_desc“ | Text | Optional | Beschreibung einer Route, die nützliche, hochwertige Informationen bietet. Sollte kein Duplikat von „route_short_name“ oder „route_long_name“ sein.<hr> _Beispiel: „A“-Züge verkehren ständig zwischen Inwood-207 St, Manhattan und Far Rockaway-Mott Avenue, Queens. Außerdem verkehren von etwa 6 Uhr morgens bis etwa Mitternacht zusätzliche „A“-Züge zwischen Inwood-207 St und Lefferts Boulevard (Züge wechseln normalerweise zwischen Lefferts Blvd und Far Rockaway)._ | 
 | `route_type` | Enum | **Erforderlich** | Gibt die Art des Transports an, das auf einer Route verwendet wird. Gültige Optionen sind:<br><br> `0` - Straßenbahn, Stadtbahn. Jedes Stadtbahn- oder Straßensystem innerhalb eines Ballungsraums.<br> `1` - U-Bahn, Metro. Jedes unterirdische Schienensystem innerhalb eines Ballungsraums.<br> `2` - Bahn. Wird für Reisen zwischen Städten oder über lange Strecken verwendet.<br> `3` - Bus. Wird für Kurz- und routes verwendet.<br> `4` - Fähre. Wird für den Kurz- und Langstreckenschiffsverkehr verwendet.<br> `5` - Cable Tram. Wird für Straßenbahnen auf Straßenniveau verwendet, bei denen das Kabel unter dem vehicle verläuft (z. B. Cable Car in San Francisco).<br> `6` - Luftseilbahn, Seilbahn (z. B. Gondelbahn, Pendelbahn). Seiltransport, bei dem Kabinen, Wagen, Gondeln oder offene Sessel mittels eines oder mehrerer Kabel aufgehängt sind.<br> `7` - Standseilbahn. Jedes Schienensystem, das für steile Steigungen ausgelegt ist.<br> `11` - Trolleybus. Elektrische Busse, die ihren Strom über Masten aus Oberleitungen beziehen.<br> `12` - Einschienenbahn. Eisenbahn, deren Gleis aus einer einzelnen Schiene oder einem Balken besteht. | 
 | `route_url` | URL | Optional | URL einer Webseite über die bestimmte Route. Muss sich vom Wert `agency.agency_url` unterscheiden. | 
 | `route_color` | Farbe | Optional | Routenfarbbezeichnung, die mit öffentlich zugänglichem Material übereinstimmt. Standardmäßig weiß (`FFFFFF`), wenn weggelassen oder leer gelassen. Der Farbunterschied zwischen `route_color` und `route_text_color` sollte bei Betrachtung auf einem Schwarzweißbildschirm ausreichend Kontrast bieten. | 
 | `route_text_color` | Farbe | Optional | Lesbare Farbe für Text, der vor einem Hintergrund aus `route_color` gezeichnet wird. Standardmäßig schwarz (` 000000 `), wenn weggelassen oder leer gelassen. Der Farbunterschied zwischen `route_color` und `route_text_color` sollte bei Betrachtung auf einem Schwarzweißbildschirm ausreichend Kontrast bieten. | 
 | `route_sort_order` | Nicht negative Ganzzahl | Optional | Sortiert die routes auf eine Weise, die für die Präsentation gegenüber Kunden optimal ist. Routen mit kleineren `route_sort_order`-Werten sollten zuerst angezeigt werden. | 
 | `continuous_pickup` | Enum | **Bedingt verboten** | Gibt an, dass der Fahrgast bei jeder Fahrt der vehicle an jedem Punkt entlang der Fahrtroute des Fahrzeugs einsteigen kann, wie in [shapes.txt](#shapestxt) beschrieben. Gültige Optionen sind:<br><br> „0“ – Kontinuierliches Anhalten der Abholung.<br> „`1`“ oder leer – Keine kontinuierliche Stoppabholung.<br> `2` - Sie müssen die agency anrufen, um die Abholung bei einem Dauerstopp zu vereinbaren.<br> `3` - Die Abholung bei kontinuierlichem Stopp muss mit dem Fahrer abgesprochen werden.<br><br> Werte für „routes.continuous_pickup“ können überschrieben werden, indem Werte in „stop_times.continuous_pickup“ für bestimmte „stop_time“ entlang der Route definiert werden.<br><br> **Bedingt verboten**:<br> - **Verboten**, wenn für eine Fahrt dieser Route „stop_times.start_pickup_drop_off_window“ oder „stop_times.end_pickup_drop_off_window“ definiert sind.<br> - Andernfalls optional. | 
 | `continuous_drop_off` | Enum | **Bedingt verboten** | Gibt an, dass der Fahrgast bei jeder Fahrt der vehicle an jedem Punkt entlang der Fahrtroute des Fahrzeugs aussteigen kann, wie in [shapes.txt](#shapestxt) beschrieben. Gültige Optionen sind:<br><br> „0“ – Kontinuierlicher Stoppabfall.<br> „`1`“ oder leer – Kein kontinuierliches Stoppen des Abfalls.<br> `2` - Sie müssen die agency anrufen, um eine kontinuierliche Unterbrechung der Abgabe zu vereinbaren.<br> `3` - Muss mit dem Fahrer abgestimmt werden, um einen kontinuierlichen Stopp beim Absetzen zu arrangieren.<br><br> Werte für „routes.continuous_drop_off“ können überschrieben werden, indem Werte in „stop_times.continuous_drop_off“ für bestimmte „stop_time“ entlang der Route definiert werden.<br><br> **Bedingt verboten**:<br> - **Verboten**, wenn für eine Fahrt dieser Route „stop_times.start_pickup_drop_off_window“ oder „stop_times.end_pickup_drop_off_window“ definiert sind.<br> - Andernfalls optional. | 
 | `network_id` | ID | **Bedingt verboten** | Identifiziert eine Gruppe von routes. Mehrere Zeilen in [routes.txt](#routestxt) können dieselbe `network_id` haben.<br><br> Bedingt verboten:<br> - **Verboten**, wenn die Datei [route_networks.txt](#route_networkstxt) vorhanden ist.<br> – Andernfalls optional. 
 
### trips.txt 
 
 Datei: **Erforderlich** 
 
 Primärschlüssel (`trip_id`) 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `route_id` | Ausländische ID mit Referenz auf `routes.route_id` | **Erforderlich** | Identifiziert eine Route. | 
 | `service_id` | Ausländische ID mit Referenz auf `calendar.service_id` oder `calendar_dates.service_id` | **Erforderlich** | Identifiziert eine Reihe von Daten, an denen der Service für eine oder mehrere routes verfügbar ist. | 
 | `trip_id` | Eindeutige ID | **Erforderlich** | Identifiziert eine Reise. | 
 | `trip_headsign` | Text | Optional | Text, der auf Schildern erscheint und den Fahrgästen das Fahrtziel mitteilt. Sollte verwendet werden, um zwischen verschiedenen Servicetypen auf derselben Route zu unterscheiden.<br><br> Wenn sich das Zielschild während einer Fahrt ändert, können Werte für `trip_headsign` überschrieben werden, indem Werte in `stop_times.stop_headsign` für bestimmte `stop_time`s entlang der Fahrt definiert werden. | 
 | `trip_short_name` | Text | Optional | Öffentlich sichtbarer Text, der verwendet wird, um Fahrgästen die Fahrt zu identifizieren, zum Beispiel um Zugnummern für Pendlerfahrten zu identifizieren. Wenn Fahrgäste sich nicht normalerweise auf Fahrtnamen verlassen, sollte `trip_short_name` leer sein. Ein `trip_short_name`-Wert, falls angegeben, sollte eine Fahrt innerhalb eines Betriebstages eindeutig identifizieren; er sollte nicht für Zielnamen oder begrenzte/ausdrückliche Bezeichnungen verwendet werden. | 
 | `direction_id` | Enum | Optional | Gibt die Fahrtrichtung für eine Fahrt an. Dieses Feld sollte nicht bei der Routenplanung verwendet werden; es bietet eine Möglichkeit, Fahrten bei der Veröffentlichung von Fahrplänen nach Richtung zu trennen. Gültige Optionen sind:<br><br> „0“ – Fahrt in eine Richtung (z. B. Hinfahrt).<br> `1` - Fahrt in die entgegengesetzte Richtung (zB Stadteinfahrt).<hr> *Beispiel: Die Felder `trip_headsign` und `direction_id` können zusammen verwendet werden, um einer Reihe von Fahrten einen Namen für jede Fahrtrichtung zuzuweisen. Eine Datei [trips.txt](#tripstxt) könnte diese Datensätze für die Verwendung in Fahrplänen enthalten:*<br> `trip_id,...,trip_headsign,direction_id`<br> `1234,...,Airport,0`<br> `1505,...,Downtown,1` | 
 | `block_id` | ID | Optional | Identifiziert den Block, zu dem die Fahrt gehört. Ein Block besteht aus einer einzelnen Fahrt oder vielen aufeinanderfolgenden Fahrten mit demselben vehicle, definiert durch gemeinsame Betriebstage und `block_id`. Eine `block_id` kann Fahrten mit unterschiedlichen Betriebstagen umfassen, wodurch unterschiedliche Blöcke entstehen. Siehe das [Beispiel unten](#example-blocks-and-service-day). Um Informationen zu transfers am Sitzplatz bereitzustellen, sollten stattdessen [transfers](#transferstxt) vom `transfer_type` `4` bereitgestellt werden. | 
 | `shape_id` | Ausländische ID, die auf `shapes.shape_id` verweist | **Bedingt erforderlich** | Identifiziert eine georäumliche shape, die die vehicle für eine Fahrt beschreibt.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn für die Fahrt ein kontinuierliches Abhol- oder Bringverhalten definiert ist, das entweder in [routes.txt](#routestxt) oder in [stop_times.txt](#stop_timestxt) ist.<br> – Andernfalls optional. | 
 | `wheelchair_accessible` | Enum | Optional | Zeigt Rollstuhlzugänglichkeit an. Gültige Optionen sind:<br><br> „0“ oder leer – Keine Informationen zur Barrierefreiheit für die Reise.<br> „`1`“ – Das für diese Reise verwendete Fahrzeug bietet Platz für mindestens einen Fahrer im Rollstuhl.<br> `2` - Auf dieser Reise können keine Rollstuhlfahrer mitgenommen werden. | 
 | `bikes_allowed` | Enum | Optional | Gibt an, ob Fahrräder erlaubt sind. Gültige Optionen sind:<br><br> „0“ oder leer – Keine Fahrradinformationen für die Fahrt.<br> „`1`“ – Das für diese Reise verwendete Fahrzeug bietet Platz für mindestens ein Fahrrad.<br> `2` – Auf dieser Fahrt sind keine Fahrräder erlaubt. | 
 
#### Beispiel: Blöcke und Betriebstage 
 
 Das folgende Beispiel ist gültig, mit unterschiedlichen Blöcken für jeden Wochentag. 
 
 | route_id-ID | trip_id | service_id | block_id | <span style="font-weight:normal">*(Zeit der ersten Haltestelle)*</span> | <span style="font-weight:normal">*(Zeit der letzten Haltestelle)*</span> | 
 |----------|---------|--------------------------------|----------|-----------------------------------------|-------------------------| 
 | rot | trip_1 | Mo-Di-Mi-Do-Fr-Sa-So | rote_Schleife | 22:00:00 | 22:55:00 | 
 | rot | trip_2 | Fr-Sa-So | rote_Schleife | 23:00:00 | 23:55:00 | 
 | rot | trip_3 | Fr-Sa | red_loop | 24:00:00 | 24:55:00 | 
 | rot | trip_4 | Mo-Di-Mi-Do | red_loop | 20:00:00 | 20:50:00 | 
 | rot | trip_5 | Mo-Di-Mi-Do | red_loop | 21:00:00 | 21:50:00 | 
 
 Hinweise zur obigen Tabelle: 
 
 * Vom Freitag bis Samstagmorgen beispielsweise fährt ein einzelnes vehicle „trip_1“, „trip_2“ und „trip_3“ (22:00 bis 00:55 Uhr). Beachten Sie, dass die letzte Fahrt am Samstag von 0:00 bis 0:55 Uhr stattfindet, aber Teil des „Betriebstages“ am Freitag ist, da die Zeiten von 24:00:00 bis 24:55:00 Uhr sind. 
 * Montags, Dienstags, Mittwochs und Donnerstags bedient ein einzelnes vehicle `trip_1`, `trip_4` und `trip_5` in einem Block von 20:00 bis 22:55 Uhr. 
 
### stop_times.txt 
 
 Datei: **Erforderlich** 
 
 Primärschlüssel (`trip_id`, `stop_sequence`) 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `trip_id` | Ausländische ID mit Referenz auf „`trips.trip_id`“ | **Erforderlich** | Identifiziert eine Fahrt. | 
 | „arrival_time“ | Uhrzeit | **Bedingt erforderlich** | Ankunftszeit an der Haltestelle (definiert durch „stop_times.stop_id“) für eine bestimmte Fahrt (definiert durch „stop_times.trip_id“) in der durch „agency.agency_timezone“ angegebenen Zeitzone, nicht durch „stops.stop_timezone“.<br><br> Wenn es für arrival und departure an einer Haltestelle keine unterschiedlichen Zeiten gibt, sollten `arrival_time und `departure_time` gleich sein.<br><br> Für Zeiten nach Mitternacht am Servicetag geben Sie die Zeit als Wert größer als 24:00:00 im Format HH:MM:SS ein.<br><br> Wenn genaue arrival und departure (`timepoint=1 oder leer) nicht verfügbar sind, sollten geschätzte oder interpolierte arrival und departure (`timepoint=0) angegeben werden.<br><br> Bedingt erforderlich:<br> - **Erforderlich** für die erste und letzte Haltestelle einer Fahrt (definiert durch „stop_times.stop_sequence“).<br> - **Erforderlich** für „timepoint=1“.<br> - **Verboten**, wenn „`start_pickup_drop_off_window`“ oder „`end_pickup_drop_off_window`“ definiert sind.<br> – Andernfalls optional.| 
 | „`departure_time`“ | Zeit | **Bedingt erforderlich** | Abfahrtszeit von der Haltestelle (definiert durch „stop_times.stop_id“) für eine bestimmte Fahrt (definiert durch „stop_times.trip_id“) in der durch „agency.agency_timezone“ angegebenen Zeitzone, nicht durch „stops.stop_timezone“.<br><br> Wenn es für arrival und departure an einer Haltestelle keine unterschiedlichen Zeiten gibt, sollten `arrival_time und `departure_time` gleich sein.<br><br> Für Zeiten nach Mitternacht am Servicetag geben Sie die Zeit als Wert größer als 24:00:00 im Format HH:MM:SS ein.<br><br> Wenn genaue arrival und departure (`timepoint=1 oder leer) nicht verfügbar sind, sollten geschätzte oder interpolierte arrival und departure (`timepoint=0) angegeben werden.<br><br> Bedingt erforderlich:<br> - **Erforderlich** für „timepoint=1“.<br> - **Verboten**, wenn „`start_pickup_drop_off_window`“ oder „`end_pickup_drop_off_window`“ definiert sind.<br> - Andernfalls optional. | 
 | `stop_id` | Ausländische ID, die auf `stops.stop_id` verweist | **Bedingt erforderlich** | Identifiziert die bediente Haltestelle. Alle während einer Fahrt bedienten stops müssen in [stop_times.txt](#stop_timestxt) verzeichnet sein. Referenzierte Standorte müssen stops/Plattformen sein, d.h. ihr `stops.location_type`-Wert muss `0` oder leer sein. Eine Haltestelle kann während derselben Fahrt mehrmals bedient werden, und mehrere Fahrten und routes können dieselbe Haltestelle bedienen.<br><br> Auf On-Demand-Dienste, die stops nutzen, sollte in der Reihenfolge verwiesen werden, in der der Dienst an diesen stops verfügbar ist. Ein Datenkonsument sollte davon ausgehen, dass die Reise von einer Haltestelle oder einem Ort zu jeder Haltestelle oder jedem Ort später auf der Reise möglich ist, vorausgesetzt, dass der `Abhol-/drop_off_type` jeder stop_time und die zeitlichen Einschränkungen jedes `Start-/end_pickup_drop_off_window/Abgabefensters ` dies nicht verbieten.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn „stop_times.location_group_id“ UND „stop_times.location_id“ NICHT definiert sind.<br> - **Verboten**, wenn `stop_times.location_group_id` oder `stop_times.location_id` definiert sind. | 
 | `location_group_id` | Ausländische ID mit Verweis auf `location_groups.location_group_id` | **Bedingt verboten** | Identifiziert die bediente Ortsgruppe, die Gruppen von stops angibt, an denen Fahrgäste abgeholt oder abgesetzt werden können. Alle während einer Fahrt bedienten Ortsgruppen müssen einen Eintrag in [stop_times.txt](#stop_timestxt) haben. Mehrere Fahrten und routes können dieselbe Ortsgruppe bedienen.<br><br> Auf On-Demand-Dienste, die Standortgruppen verwenden, sollte in der Reihenfolge verwiesen werden, in der der Dienst an diesen Standortgruppen verfügbar ist. Ein Datenkonsument sollte davon ausgehen, dass eine Reise von einer Haltestelle oder einem Standort zu jeder Haltestelle oder jedem Standort später auf der Reise möglich ist, vorausgesetzt, dass der `Abhol-/drop_off_type` jeder stop_time und die Zeitbeschränkungen jedes `Start-/end_pickup_drop_off_window` dies nicht verbieten.<br><br> **Bedingt verboten**:<br> - **Verboten**, wenn `stop_times.stop_id` oder `stop_times.location_id` definiert sind. | 
 | `location_id` | Ausländische ID, die `id` aus `locations.geojson` referenziert | **Bedingt verboten** | Identifiziert den GeoJSON-Standort, der der bedienten Zone entspricht, in der Fahrgäste eine Abholung oder einen Abtransport anfordern können. Alle GeoJSON-Standorte, die während einer Fahrt bedient werden, müssen einen Eintrag in [stop_times.txt](#stop_timestxt) haben. Mehrere Fahrten und routes können denselben GeoJSON-Standort bedienen.<br><br> On-Demand-Dienste innerhalb von Standorten sollten in der Reihenfolge referenziert werden, in der der Dienst an diesen Standorten verfügbar ist. Ein Datenkonsument sollte davon ausgehen, dass eine Reise von einer Haltestelle oder einem Standort zu jeder Haltestelle oder jedem Standort später auf der Reise möglich ist, vorausgesetzt, dass der `Abhol-/drop_off_type` jeder stop_time und die Zeitbeschränkungen jedes `Start-/end_pickup_drop_off_window/Abgabefensters ` dies nicht verbieten.<br><br> **Bedingt verboten**:<br> - **Verboten**, wenn `stop_times.stop_id` oder `stop_times.location_group_id` definiert sind. | 
 | `stop_sequence` | Nicht negative Ganzzahl | **Erforderlich** | Reihenfolge der stops, Standortgruppen oder GeoJSON-Standorte für eine bestimmte Fahrt. Die Werte müssen während der Fahrt zunehmen, müssen aber nicht aufeinander folgen.<hr> *Beispiel: Der erste Ort auf der Reise könnte eine `stop_sequence`= `1` haben, der zweite Ort auf der Reise könnte eine `stop_sequence`= `23` haben, der dritte Ort könnte eine `stop_sequence`= `40` haben und so weiter.*<br><br> Für Fahrten innerhalb derselben Standortgruppe oder desselben GeoJSON-Standorts sind zwei Datensätze in [stop_times.txt](#stop_timestxt) mit derselben `location_group_id` oder `location_id` erforderlich. | 
 | `stop_headsign` | Text | Optional | Text, der auf Schildern erscheint und den Fahrgästen das Fahrtziel anzeigt. Dieses Feld überschreibt das standardmäßige `trips.trip_headsign`, wenn sich das Zielschild zwischen den stops ändert. Wenn das Zielschild für eine gesamte Fahrt angezeigt wird, sollte stattdessen `trips.trip_headsign ` verwendet werden.<br><br> Ein für eine „ stop_time “ angegebener Wert für „ stop_headsign “ gilt nicht für nachfolgende „ stop_time“ in derselben Fahrt. Wenn Sie das „trip_headsign“ für mehrere „stop_time“ in derselben Fahrt überschreiben möchten, muss der Wert für „stop_headsign “ in jeder „ stop_time “-Zeile repeated werden. | 
 | „`start_pickup_drop_off_window`“ | Zeit | **Bedingt erforderlich** | Zeit, zu der der On-Demand-Service an einem GeoJSON-Standort, einer Standortgruppe oder einer Haltestelle verfügbar wird.<br><br> **Bedingt erforderlich**:<br> - **Erforderlich**, wenn „stop_times.location_group_id“ oder „stop_times.location_id“ definiert ist.<br> - **Erforderlich**, wenn „`end_pickup_drop_off_window`“ definiert ist.<br> - **Verboten**, wenn „arrival_time“ oder „`departure_time`“ definiert ist.<br> – Andernfalls optional. | 
 | „`end_pickup_drop_off_window`“ | Zeit | **Bedingt erforderlich** | Zeit, zu der der On-Demand-Dienst an einem GeoJSON-Standort, einer Standortgruppe oder einer Haltestelle endet.<br><br> **Bedingt erforderlich**:<br> - **Erforderlich**, wenn „stop_times.location_group_id“ oder „stop_times.location_id“ definiert ist.<br> - **Erforderlich**, wenn „`start_pickup_drop_off_window`“ definiert ist.<br> - **Verboten**, wenn „arrival_time“ oder „`departure_time`“ definiert ist.<br> – Andernfalls optional. | 
 | `pickup_type` | Enum | **Bedingt verboten** | Gibt die Abholmethode an. Gültige Optionen sind:<br><br> „0“ oder leer – Regelmäßig geplante Abholung.<br> `1` – Keine Abholung möglich.<br> `2` - Zur Vereinbarung der Abholung müssen Sie die agency anrufen.<br> `3` – Die Abholung muss mit dem Fahrer abgesprochen werden.<br><br> **Bedingt verboten**:<br> - `pickup_type=0` **verboten** wenn `start_pickup_drop_off_window` oder `end_pickup_drop_off_window` definiert sind.<br> - `pickup_type=3` **verboten** wenn `start_pickup_drop_off_window` oder `end_pickup_drop_off_window` definiert sind.<br> – Andernfalls optional. | 
 | `drop_off_type` | Enum | **Bedingt verboten** | Gibt die Drop-Off-Methode an. Gültige Optionen sind:<br><br> „0“ oder leer – Regelmäßig geplante Abgabe.<br> `1` – Keine Abgabe möglich.<br> `2` - Zur Vereinbarung der Rückgabe müssen Sie die agency anrufen.<br> `3` - Die Abgabe muss mit dem Fahrer abgesprochen werden.<br><br> **Bedingt verboten**:<br> - `drop_off_type=0` **verboten** wenn `start_pickup_drop_off_window` oder `end_pickup_drop_off_window` definiert sind.<br> - Andernfalls optional. | 
 | `continuous_pickup ` | Enum | **Bedingt verboten** | Gibt an, dass der Fahrgast an jedem Punkt entlang der in [shapes.txt](#shapestxt) beschriebenen Fahrtroute des Fahrzeugs von dieser `stop_time` bis zur nächsten `stop_time` in der `stop_sequence` ` der Fahrt in das vehicle einsteigen kann. Gültige Optionen sind:<br><br> „0“ – Kontinuierliches Anhalten der Abholung.

br> `1` oder leer- Keine kontinuierliche Stoppabholung.<br> `2` - Sie müssen die agency anrufen, um die Abholung bei einem Dauerstopp zu vereinbaren.<br> `3` - Die Abholung bei kontinuierlichem Stopp muss mit dem Fahrer abgesprochen werden.<br><br> Wenn dieses Feld ausgefüllt ist, überschreibt es jedes kontinuierliche Abholverhalten, das in [routes.txt](#routestxt) definiert ist. Wenn dieses Feld leer ist, erbt die `stop_time` jedes kontinuierliche Abholverhalten, das in [routes.txt](#routestxt) definiert ist.<br><br> **Bedingt verboten**:<br> - **Verboten**, wenn „`start_pickup_drop_off_window`“ oder „`end_pickup_drop_off_window`“ definiert sind.<br> - Andernfalls optional. | 
 | `continuous_drop_off ` | Enum | **Bedingt verboten** | Gibt an, dass der Fahrgast an jedem Punkt entlang der Fahrtroute des Fahrzeugs, wie in [shapes.txt](#shapestxt) beschrieben, von dieser `stop_time` bis zur nächsten `stop_time` in der `stop_sequence` der Fahrt aus dem vehicle aussteigen kann. Gültige Optionen sind:<br><br> „0“ – Kontinuierlicher Stoppabfall.<br> „`1`“ oder leer – Kein kontinuierliches Stoppen des Abfalls.<br> `2` - Sie müssen die agency anrufen, um eine kontinuierliche Unterbrechung der Abgabe zu vereinbaren.<br> `3` - Muss mit dem Fahrer abgestimmt werden, um einen kontinuierlichen Stopp beim Absetzen zu arrangieren.<br><br> Wenn dieses Feld ausgefüllt ist, überschreibt es jedes in [routes.txt](#routestxt) definierte kontinuierliche Abbruchverhalten. Wenn dieses Feld leer ist, erbt die `stop_time` jedes in [routes.txt](#routestxt) definierte kontinuierliche Abbruchverhalten.<br><br> **Bedingt verboten**:<br> - **Verboten**, wenn „`start_pickup_drop_off_window`“ oder „`end_pickup_drop_off_window`“ definiert sind.<br> - Andernfalls optional. | 
 | `shape_dist_traveled| Nicht negativer float | Optional | Tatsächlich zurückgelegte Distanz entlang der zugehörigen shape, von der ersten Haltestelle bis zur in diesem Datensatz angegebenen Haltestelle. Dieses Feld gibt an, wie viel von der shape während einer Fahrt zwischen zwei beliebigen stops gezeichnet werden soll. Muss in denselben Einheiten angegeben sein wie in [shapes.txt](#shapestxt). Für `shape_dist_traveled verwendete Werte müssen zusammen mit `stop_sequence` ansteigen; sie dürfen nicht verwendet werden, um die Rückwärtsfahrt entlang einer Route anzuzeigen.<br><br> Empfohlen für routes mit Schleifen oder Inline-Strecken (das vehicle überquert oder überfährt in einer Fahrt denselben Streckenabschnitt). Siehe [`shapes.shape_dist_traveled`](#shapestxt).<hr> *Beispiel: Wenn ein Bus eine Strecke von 5,25 Kilometern vom Startpunkt der shape bis zur Haltestelle zurücklegt, gilt `shape_dist_traveled`=`5.25`.*| 
 | `timepoint` | Enum | Empfohlen | Gibt an, ob arrival und departure für eine Haltestelle vom vehicle strikt eingehalten werden oder ob es sich stattdessen um ungefähre und/oder interpolierte Zeiten handelt. Dieses Feld ermöglicht es einem GTFS Produzenten, interpolierte Haltestellenzeiten anzugeben und gleichzeitig anzugeben, dass die Zeiten ungefähr sind. Gültige Optionen sind:<br><br> „0“ – Die Zeiten gelten als ungefähr.<br> `1` oder leer – Zeiten werden als exakt betrachtet. | 
 | `pickup_booking_rule_id` | ID mit Referenz auf `booking_rules.booking_rule_id` | Optional | Identifiziert die Boarding-Buchungsregel zu dieser Haltezeit.<br><br> Empfohlen, wenn „pickup_type=2“. | 
 | „`drop_off_booking_rule_id`“ | ID mit Referenz auf „booking_rules.booking_rule_id“ | Optional | Identifiziert die Ausstiegsbuchungsregel zu dieser Haltestellenzeit.<br><br> Empfohlen, wenn „drop_off_type=2“. | 
 
#### Routing-Verhalten von On-Demand-Services- Bei der Angabe von Routing oder Reisezeit zwischen Ausgangs- und Zielort sollten Datenkonsumenten Zwischendatensätze stop_times.txt mit der gleichen „`trip_id`“ ignorieren, für die „`start_pickup_drop_off_window`“ und „`end_pickup_drop_off_window`“ definiert sind. Beispiele, die zeigen, was ignoriert werden sollte, finden Sie auf [der Datenbeispielseite](../examples/flex/#ignoring-intermediate-stop-times-records-with-pickupdrop-off-windows). 
 - Gleichzeitige Überlappung der Geometrie „`id`“ von locations.geojson, der Zeit „start/end_pickup_drop_off_window“ und „pickup_type“ oder „drop_off_type“ zwischen zwei oder mehr Datensätzen stop_times.txt mit der gleichen „`trip_id`“ ist verboten. Beispiele, die zeigen, was verboten ist, finden Sie auf [der Datenbeispielseite](../examples/flex/#zone-overlap-constraint). 
 
### calendar.txt 
 
 Datei: **Bedingt erforderlich** 
 
 Primärschlüssel (`service_id`) 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `service_id` | Eindeutige ID | **Erforderlich** | Identifiziert eine Reihe von Daten, an denen der Service für eine oder mehrere routes verfügbar ist. | 
 | `monday` | Aufzählung | **Erforderlich** | Gibt an, ob der Service an allen Montagen im date verkehrt, der durch die Felder `start_date` und `end_date` angegeben ist. Beachten Sie, dass Ausnahmen für bestimmte Daten in [calendar_dates.txt](#calendar_datestxt) aufgeführt sein können. Gültige Optionen sind:<br><br> „`1`“ – Der Service ist für alle Montage im date verfügbar.<br> `0` – Der Dienst ist für Montage im date nicht verfügbar. | 
 | `tuesday| Enum | **Erforderlich** | Funktioniert auf die gleiche Weise wie `monday, gilt aber für Dienstage | 
 | `wednesday| Enum | **Erforderlich** | Funktioniert auf die gleiche Weise wie `monday, gilt aber für Mittwoche | 
 | `thursday| Enum | **Erforderlich** | Funktioniert auf die gleiche Weise wie `monday, gilt aber für Donnerstage | 
 | `friday| Enum | **Erforderlich** | Funktioniert auf die gleiche Weise wie `monday, gilt aber für Freitage | 
 | `saturday| Enum | **Erforderlich** | Funktioniert auf die gleiche Weise wie `monday, gilt aber für Samstage. | 
 | `sunday| Enum | **Erforderlich** | Funktioniert auf die gleiche Weise wie `monday`, gilt aber für Sonntage. | 
 | `start_date` ` | Datum | **Erforderlich** | Starttag des Serviceintervalls. | 
 | `end_date` | Datum | **Erforderlich** | Endtag des Serviceintervalls. Dieser Servicetag ist im Intervall enthalten. | 
 
### calendar_dates.txt 
 
 Datei: **Bedingt erforderlich** 
 
 Primärschlüssel (`service_id`, `date`) 
 
 Die Tabelle [calendar_dates.txt](#calendar_datestxt) aktiviert oder deaktiviert den Service explizit nach date. Sie kann auf zwei Arten verwendet werden. 
 
 * Empfohlen: Verwenden Sie [calendar_dates.txt](#calendar_datestxt) zusammen mit [calendar.txt](#calendartxt), um Ausnahmen von den in [calendar.txt](#calendartxt) definierten Standard-Gottesdienstmustern zu definieren. Wenn der Gottesdienst im Allgemeinen regelmäßig erfolgt und an bestimmten Tagen einige Änderungen vorgenommen werden (beispielsweise um Gottesdiensten für besondere Ereignisse oder einem Schulplan gerecht zu werden), ist dies eine gute Vorgehensweise. In diesem Fall ist „calendar_dates.service_id“ eine fremde ID, die auf „calendar.service_id“ verweist. 
 * Alternative: Lassen Sie [calendar.txt](#calendartxt) weg und geben Sie jedes date in [calendar_dates.txt](#calendartxt) an. Dies ermöglicht erhebliche Gottesdienstvariationen und berücksichtigt Gottesdienste ohne normale wöchentliche Fahrpläne. In diesem Fall ist „service_id“ eine ID. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `service_id` | Fremd-ID mit Verweis auf `calendar.service_id` oder ID | **Erforderlich** | Identifiziert eine Reihe von Daten, an denen eine Serviceausnahme für eine oder mehrere routes auftritt. Jedes Paar (`service_id`, `date`) darf nur einmal in [calendar_dates.txt](#calendar_datestxt) vorkommen, wenn [calendar.txt](#calendartxt) und [calendar_dates.txt](#calendar_datestxt) zusammen verwendet werden. Wenn ein `service_id`-Wert sowohl in [calendar.txt](#calendartxt) als auch in [calendar_dates.txt](#calendar_datestxt) vorkommt, ändern die Informationen in [calendar_dates.txt](#calendar_datestxt) die in [calendar.txt](#calendartxt) angegebenen Serviceinformationen. | 
 | `date` | Datum | **Erforderlich** | Datum, an dem die Serviceausnahme auftritt. | 
 | `exception_type ` | Enum | **Erforderlich** | Gibt an, ob der Service am im date angegebenen date verfügbar ist. Gültige Optionen sind:<br><br> `1` – Der Service wurde für das angegebene date hinzugefügt.<br> `2` – Der Dienst wurde für das angegebene date entfernt.<hr> *Beispiel: Angenommen, für eine Route ist an Feiertagen eine Reihe von Fahrten verfügbar und an allen anderen Tagen eine andere. Eine `service_id` könnte dem regulären Fahrplan entsprechen und eine andere `service_id` dem Feiertagsfahrplan. Für einen bestimmten Feiertag könnte die Datei [calendar_dates.txt](#calendar_datestxt) verwendet werden, um den Feiertag zur `service_id` des Feiertags hinzuzufügen und ihn aus dem regulären `service_id`-Fahrplan zu entfernen.* | 
 
### fare_attributes.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`fare_id`) 
 
 **Versionen**<br> 
 Es gibt zwei Modellierungsoptionen zur Beschreibung von Fahrpreisen. GTFS- Fares V1 ist die alte Option zur Beschreibung minimaler Fahrpreisinformationen. GTFS- Fares V2 ist eine aktualisierte Methode, die eine detailliertere Darstellung der Fahrpreisstruktur eines Reisebüros ermöglicht. Beide Methoden dürfen in einem Datensatz vorhanden sein, aber ein Datenkonsument sollte für einen bestimmten Datensatz nur eine Methode verwenden. Es wird empfohlen, dass GTFS- Fares V2 Vorrang vor GTFS- Fares V1 hat.<br><br> Die mit GTFS– Fares V1 verknüpften Dateien sind:<br> - [fare_attributes.txt](#fare_attributestxt)<br> - [fare_rules.txt](#fare_rulestxt)<br><br> Die mit GTFS– Fares V2 verknüpften Dateien sind:<br> - [.txt](#fare_mediatxt)<br> - [fare_products.txt](#fare_productstxt)<br> - [fare_leg_rules.txt](#fare_leg_rulestxt)<br> - [fare_transfer_rules.txt](#fare_transfer_rulestxt) 
 
<br> 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `fare_id` | Eindeutige ID | **Erforderlich** | Identifiziert eine Fahrpreisklasse. | 
 | `price` | Nicht negativer float | **Erforderlich** | price in der durch `currency_type` angegebenen Einheit. | 
 | `currency_type` | Währungscode | **Erforderlich** | Zur Bezahlung des Fahrpreises verwendete Währung. | 
 | `payment_method` | Aufzählung | **Erforderlich** | Gibt an, wann der Fahrpreis bezahlt werden muss. Gültige Optionen sind:<br><br> „0“ – Der Fahrpreis wird an Bord bezahlt.<br> `1` - Der Fahrpreis muss vor dem Einsteigen bezahlt werden. | 
 | `transfers` | Enum | **Erforderlich** | Gibt die Anzahl der mit diesem Fahrpreis zulässigen transfers an. Gültige Optionen sind:<br><br> „0“ – Bei diesem Tarif sind keine transfers zulässig.<br> „`1`“ – Fahrer dürfen einmal umsteigen.<br> „2“ – Fahrer dürfen zweimal umsteigen.<br> leer – Unbegrenzte transfers sind erlaubt. | 
 | `agency_id` | Ausländische ID mit Referenz auf `agency.agency_id` | **Bedingt erforderlich** | Identifiziert die relevante agency für einen Fahrpreis.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn mehrere Agenturen in [agency.txt](#agencytxt) definiert sind.<br> – Andernfalls empfohlen. | 
 | „transfer_duration“ | Nicht-negative Ganzzahl | Optional | Zeitspanne in Sekunden, bevor ein Transfer abläuft. Wenn „transfers“ = „0“ ist, kann dieses Feld verwendet werden, um anzugeben, wie lange ein Ticket gültig ist, oder es kann leer gelassen werden. | 
 
### fare_rules.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel („*“) 
 
 Die Tabelle [fare_rules.txt](#fare_rulestxt) gibt an, wie Fahrpreise in [fare_attributes.txt](#fare_attributestxt) auf eine Reiseroute angewendet werden. Die meisten Fahrpreisstrukturen verwenden eine Kombination der folgenden Regeln: 
 
 * Der Fahrpreis hängt von den Abfahrts- oder Zielbahnhöfen ab. 
 * Der Fahrpreis hängt davon ab, durch welche Zonen die Reiseroute führt. 
 * Der Fahrpreis hängt von der verwendeten Route ab. 
 
 Beispiele, die zeigen, wie eine Fahrpreisstruktur mit [fare_rules.txt](#fare_rulestxt) und [fare_attributes.txt](#fare_attributestxt) angegeben wird, finden Sie unter [FareExamples](https://web.archive.org/web/20111207224351/https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) im Wiki des Open-Source-Projekts GoogleTransitDataFeed. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `fare_id` | Ausländische ID mit Referenz auf `fare_attributes.fare_id` | **Erforderlich** | Identifiziert eine Fahrpreisklasse. | 
 | `route_id` | Fremd-ID mit Verweis auf `routes.route_id` | Optional | Identifiziert eine Route, die der Tarifklasse zugeordnet ist. Wenn mehrere routes mit denselben Tarifattributen vorhanden sind, erstellen Sie für jede Route einen Datensatz in [fare_rules.txt](#fare_rulestxt).<hr> *Beispiel: Wenn die Tarifklasse „b“ auf den Strecken „TSW“ und „TSE“ gültig ist, enthält die Datei [fare_rules.txt](#fare_rulestxt) diese Datensätze für die Tarifklasse:*<br> ` fare_id,route_id`<br> `b,TSW`<br> `b,TSE`| 
 | `origin_id` | Ausländische ID mit Verweis auf `stops.zone_id ` | Optional | Identifiziert eine Herkunftszone. Wenn eine Tarifklasse mehrere Herkunftszonen hat, erstellen Sie für jede ` origin_id ` einen Datensatz in [fare_rules.txt](#fare_rulestxt).<hr> *Beispiel: Wenn die Tarifklasse „b“ für alle Fahrten ab Zone „2“ oder Zone „8“ gültig ist, enthält die Datei [fare_rules.txt](#fare_rulestxt) folgende Datensätze für die Tarifklasse:*<br> `fare_id,...,origin_id`<br> `b,...,2`<br> `b,...,8` | 
 | `destination_id` | Ausländische ID mit Verweis auf `stops.zone_id ` | Optional | Identifiziert eine Zielzone. Wenn eine Tarifklasse mehrere Zielzonen hat, erstellen Sie für jede ` destination_id ` einen Datensatz in [fare_rules.txt](#fare_rulestxt).<hr> *Beispiel: Die Felder „ origin_id“ und „destination_id“ könnten zusammen verwendet werden, um anzugeben, dass die Tarifklasse „b“ für Reisen zwischen den Zonen 3 und 4 gültig ist, und für Reisen zwischen den Zonen 3 und 5 würde die Datei [fare_rules.txt](#fare_rulestxt) diese Datensätze für die Tarifklasse enthalten:*<br> `fare_id,...,origin_id,destination_id`<br> `b,...,3,4`<br> `b,...,3,5` | 
 | `contains_id` | Ausländische ID-Referenz `stops.zone_id` | Optional | Identifiziert die Zonen, die ein Fahrgast bei Verwendung einer bestimmten Fahrpreisklasse betritt. Wird in einigen Systemen verwendet, um die richtige Fahrpreisklasse zu berechnen.<hr> *Beispiel: Wenn die Tarifklasse „c“ allen Fahrten auf der GRT-Route zugeordnet ist, die durch die Zonen 5, 6 und 7 führen, enthält die Datei [fare_rules.txt](#fare_rulestxt) folgende Datensätze:*<br> `fare_id,route_id,...,contains_id`<br> `c,GRT,...,5`<br> `c,GRT,...,6`<br> `c,GRT,...,7`<br> *Da alle `contains_id`-Zonen übereinstimmen müssen, damit der Tarif angewendet wird, hätte eine Reiseroute, die durch die Zonen 5 und 6, aber nicht durch Zone 7 führt, nicht die Tarifklasse „c“. Weitere Einzelheiten finden Sie unter [https://code.google.com/p/googletransitdatafeed/wiki/FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) im GoogleTransitDataFeed-Projektwiki.* | 
 
### timeframes.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`*`) 
 
 Wird verwendet, um Tarife zu beschreiben, die je nach Tageszeit, Wochentag oder einem bestimmten Tag im Jahr variieren können. Zeitrahmen können in [fare_leg_rules.txt](#fare_leg_rulestxt) mit Tarifprodukten verknüpft werden.<br> 
 Es darf keine überlappenden Zeitintervalle für dieselben Werte „timeframe_group_id“ und „service_id“ geben. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | „timeframe_group_id“ | ID | **Erforderlich** | Identifiziert einen Zeitrahmen oder eine Reihe von Zeitrahmen. | 
 | „`start_time` “ | Zeit | **Bedingt erforderlich** | Definiert den Anfang eines Zeitrahmens. Das Intervall umfasst die Startzeit.<br> Werte größer als `24:00:00` sind verboten. Ein leerer Wert in `start_time` wird als `00:00:00` betrachtet.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn „timeframes.end_time“ definiert ist.<br> - Andernfalls **Verboten** | 
 | `end_time` | Zeit | **Bedingt erforderlich** | Definiert das Ende eines Zeitrahmens. Das Intervall umfasst nicht die Endzeit.<br> Werte größer als `24:00:00` sind verboten. Ein leerer Wert in `end_time` wird als `24:00:00` betrachtet.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn „timeframes.start_time“ definiert ist.<br> - Andernfalls **verboten** | 
 | `service_id` | Ausländische ID, die auf `calendar.service_id` oder `calendar_dates.service_id` verweist | **Erforderlich** | Identifiziert eine Reihe von Daten, für die ein Zeitrahmen gültig ist. | 
 
#### Semantik der lokalen Zeit von Zeitrahmen- Bei der Auswertung der Zeit eines Fahrpreisereignisses gegenüber [timeframes.txt](#timeframestxt) wird die Ereigniszeit in Ortszeit unter Verwendung der lokalen Zeitzone berechnet, die durch `stop_timezone` (falls angegeben) der Haltestelle oder des übergeordneten Bahnhofs für das Fahrpreisereignis bestimmt wird. Wenn nicht angegeben, sollte stattdessen die Zeitzone der agency des Feeds verwendet werden. 
 - Der „aktuelle Tag“ ist das aktuelle date der Zeit des Fahrpreisereignisses, berechnet relativ zur lokalen Zeitzone. Der „aktuelle Tag“ kann sich vom Betriebstag der Fahrt einer Fahrpreisstrecke unterscheiden, insbesondere bei Fahrten, die über Mitternacht hinausgehen. 
 – Die „Tagesuhrzeit“ für das Fahrpreisereignis wird relativ zum „aktuellen Tag“ berechnet, wobei die Feldtypsemantik von GTFS Time verwendet wird. 
 
### fare_media.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`fare_media_id`) 
 
 Zur Beschreibung der verschiedenen Fahrpreismedien, die für die Nutzung von Fahrpreisprodukten eingesetzt werden können. Fahrpreismedien sind physische oder virtuelle Halter, die für die Darstellung und/oder Validierung eines Fahrpreisprodukts verwendet werden. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `fare_media_id` | Eindeutige ID | **Erforderlich** | Identifiziert ein Fahrpreismedium. | 
 | `fare_media_name` | Text | Optional | Name des Fahrpreismediums.<br><br> Bei Fahrkarten (`fare_media_type =2`) oder mobilen Apps (`fare_media_type =4`) muss der `fare_media_name` enthalten sein und mit dem Namen übereinstimmen, der von den Organisationen verwendet wird, die die Fahrkarten ausstellen. | 
 | `fare_media_type` | Enum | **Erforderlich** | Der Typ des Fahrkartenmediums. Gültige Optionen sind:<br><br> `0` - Keine. Wird verwendet, wenn beim Kauf oder bei der Entwertung eines Fahrscheins kein Fahrscheinmedium verwendet wird, z. B. wenn beim Fahrer oder Schaffner Barzahlung erfolgt und kein physischer Fahrschein vorliegt.<br> `1` - Physisches Papierticket, das einem Passagier entweder eine bestimmte Anzahl im Voraus gekaufter Fahrten oder eine unbegrenzte Anzahl an Fahrten innerhalb eines festgelegten Zeitraums ermöglicht.<br> `2` - Physische Transitkarte, auf der Tickets, Pässe oder ein Geldwert gespeichert sind.<br> `3` – cEMV (kontaktloses Europay, Mastercard und Visa) als Open-Loop-Token-Container für kontobasiertes Ticketing.<br> `4` – Mobile App mit gespeicherten virtuellen Transitkarten, Tickets, Pässen oder Geldwerten.| 
 
### fare_products.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`fare_product_id`, `fare_media_id`) 
 
 Wird verwendet, um die Bandbreite der für Fahrgäste zum Kauf verfügbaren Fahrpreise zu beschreiben oder die bei der Berechnung des Gesamtfahrpreises für Fahrten mit mehreren Teilstrecken, wie z. B. Umsteigekosten, berücksichtigt wird. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `fare_product_id` | ID | **Erforderlich** | Identifiziert ein Fahrpreisprodukt oder eine Reihe von Fahrpreisprodukten.<br><br> Mehrere Datensätze in [fare_products.txt](#fare_productstxt) können dieselbe `fare_product_id` haben. In diesem Fall werden alle Datensätze mit dieser ID abgerufen, wenn von einer anderen Datei darauf verwiesen wird.<br><br> Mehrere Datensätze können dieselbe `fare_product_id`, aber unterschiedliche `fare_media_id` haben, was auf verschiedene Methoden hinweist, die zum Einsatz des Fahrpreisprodukts verfügbar sind, möglicherweise zu unterschiedlichen Preisen. | 
 | `fare_product_name` | Text | Optional | Der Name des Fahrpreisprodukts, wie er den Fahrgästen angezeigt wird. | 
 | `fare_media_id` | Ausländische ID mit Referenz auf `fare_media.fare_media_id` | Optional | Identifiziert ein Fahrpreismedium, das während der Fahrt zum Einsatz des Fahrpreisprodukts verwendet werden kann. Wenn `fare_media_id` leer ist, wird davon ausgegangen, dass das Fahrpreismedium unbekannt ist.| 
 | `amount` | amount | **Erforderlich** | Die Kosten des Fahrpreisprodukts. Kann negativ sein, um Transferrabatte darzustellen. Kann null sein, um ein kostenloses Fahrpreisprodukt darzustellen. | 
 | `currency` | Währungscode | **Erforderlich** | Die currency der Kosten des Fahrpreisprodukts. | 
 
 
### fare_leg_rules.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`network_id, from_area_id, to_area_id, from_timeframe_group_id, to_timeframe_group_id, fare_product_id`) 
 
 Tarifregeln für einzelne Reiseabschnitte. 
 
 Tarife in [`fare_leg_rules.txt`](#fare_leg_rulestxt) müssen abgefragt werden, indem alle Datensätze in der Datei gefiltert werden, um Regeln zu finden, die zu dem vom Fahrgast zurückzulegenden Abschnitt passen. 
 
 So verarbeiten Sie die Kosten einer Teilstrecke: 
 
 1. Die Datei [fare_leg_rules.txt](#fare_leg_rulestxt) muss nach den Feldern gefiltert werden, die die Reisemerkmale definieren. Diese Felder sind: 
 - `fare_leg_rules.network_id` 
 - `fare_leg_rules.from_area_id` 
 - `fare_leg_rules.to_area_id` 
 - `fare_leg_rules.from_timeframe_group_id` 
 - `fare_leg_rules.to_timeframe_group_id` 
<br/> 
 
 2. Wenn die Strecke aufgrund der Reisemerkmale genau mit einem Datensatz in [fare_leg_rules.txt](#fare_leg_rulestxt) übereinstimmt, muss dieser Datensatz verarbeitet werden, um die Kosten der Strecke zu ermitteln. Diese Datei verarbeitet leere Einträge auf zwei Arten: leere Semantik ODER Regelpriorität. 
<br/> 
 
 3. Wenn keine genauen Übereinstimmungen gefunden werden UND das Feld „rule_priority“ nicht existiert, dann müssen leere Einträge in „fare_leg_rules.network_id“, „fare_leg_rules.from_area_id“ und „fare_leg_rules.to_area_id“ geprüft werden, um die Kosten der Strecke zu verarbeiten: 
 - Ein leerer Eintrag in „fare_leg_rules.network_id“ entspricht allen Netzwerken, die in [routes.txt](#routestxt) oder [networks.txt](#networkstxt) definiert sind, mit Ausnahme derjenigen, die unter „fare_leg_rules.network_id“ aufgeführt sind. 
 
 - Ein leerer Eintrag in „fare_leg_rules.from_area_id“ entspricht allen Bereichen, die in „areas.area_id“ definiert sind, mit Ausnahme derjenigen, die unter „fare_leg_rules.from_area_id` 
 - Ein leerer Eintrag in `fare_leg_rules.to_area_id` entspricht allen in `areas.area_id` definierten Bereichen, mit Ausnahme der unter `fare_leg_rules.to_area_id` 
 aufgeführten.<br/> 
 
 4. Wenn das Feld „rule_priority“ vorhanden ist, dann- Ein leerer Eintrag in „fare_leg_rules.network_id“ zeigt an, dass das Netzwerk der Teilstrecke die Übereinstimmung mit dieser Regel nicht beeinflusst. 
 - Ein leerer Eintrag in „fare_leg_rules.from_area_id“ zeigt an, dass der departure der Teilstrecke die Übereinstimmung mit dieser Regel nicht beeinflusst. 
 - Ein leerer Eintrag in „fare_leg_rules.to_area_id“ zeigt an, dass der arrival der Teilstrecke die Übereinstimmung mit dieser Regel nicht beeinflusst. 
<br/> 
 
 5. Erfüllt die Strecke keine der oben beschriebenen Regeln, ist der Tarif unbekannt. 
 
<br/> 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `leg_group_id` | ID | Optional | Identifiziert eine Gruppe von Einträgen in [fare_leg_rules.txt](#fare_leg_rulestxt).<br><br> Wird verwendet, um Fahrpreisübertragungsregeln zwischen „fare_transfer_rules.from_leg_group_id“ und „fare_transfer_rules.to_leg_group_id“ zu beschreiben.<br><br> Mehrere Einträge in [fare_leg_rules.txt](#fare_leg_rulestxt) können zur gleichen `fare_leg_rules.leg_group_id` gehören.<br><br> Derselbe Eintrag in [fare_leg_rules.txt](#fare_leg_rulestxt) (ohne `fare_leg_rules.leg_group_id`) darf nicht zu mehreren `fare_leg_rules.leg_group_id` gehören.| 
 | `network_id` | Fremd-ID mit Verweis auf `routes.network_id` oder `networks.network_id`| Optional | Identifiziert ein Streckennetz, für das die Tarifregel gilt.<br><br> Wenn das Feld „rule_priority“ nicht vorhanden ist UND es keine passenden „fare_leg_rules.network_id“-Werte für die gefilterte „network_id“ gibt, wird standardmäßig eine leere „fare_leg_rules.network_id“-Werte verwendet.<br><br> Ein leerer Eintrag in `fare_leg_rules.network_id` entspricht allen Netzwerken, die in [routes.txt](#routestxt) oder [networks.txt](#networkstxt) definiert sind, mit Ausnahme derjenigen, die unter `fare_leg_rules.network_id` aufgeführt sind.<br><br> Wenn das Feld „rule_priority“ in der Datei vorhanden ist, zeigt eine leere „fare_leg_rules.network_id“ an, dass das Streckennetz der Etappe keinen Einfluss auf die Übereinstimmung mit dieser Regel hat. | 
 | „from_area_id“ | Ausländische ID mit Referenzierung auf „areas.area_id“ | Optional | Identifiziert einen departure .<br><br> Wenn das Feld „rule_priority“ nicht vorhanden ist UND es keine passenden „fare_leg_rules.from_area_id“-Werte für die gefilterte „area_id“ gibt, wird standardmäßig eine leere „fare_leg_rules.from_area_id“-Werte verwendet.<br><br> Ein leerer Eintrag in `fare_leg_rules.from_area_id` entspricht allen in `areas.area_id` definierten Bereichen, mit Ausnahme der unter `fare_leg_rules.from_area_id` aufgeführten.<br><br> Wenn das Feld „rule_priority“ in der Datei vorhanden ist, zeigt ein leeres „fare_leg_rules.from_area_id“ an, dass der departure des Abschnitts keinen Einfluss auf die Übereinstimmung mit dieser Regel hat. | 
 | „to_area_id“ | Ausländische ID mit Referenzierung auf „areas.area_id“ | Optional | Identifiziert einen arrival .<br><br> Wenn das Feld „rule_priority“ nicht vorhanden ist UND es keine passenden „fare_leg_rules.to_area_id“-Werte für die gefilterte „area_id“ gibt, wird standardmäßig eine leere „fare_leg_rules.to_area_id“-Werte verwendet.<br><br> Ein leerer Eintrag in `fare_leg_rules.to_area_id` entspricht allen in `areas.area_id` definierten Bereichen, mit Ausnahme der unter `fare_leg_rules.to_area_id` aufgeführten.<br><br> Wenn das Feld „rule_priority“ in der Datei vorhanden ist, zeigt ein leeres „fare_leg_rules.to_area_id“ an, dass der arrival des Abschnitts die Übereinstimmung mit dieser Regel nicht beeinflusst. | 
 | „from_timeframe_group_id“ | Ausländische ID mit Referenz auf „timeframes.timeframe_group_id“ | Optional | Definiert den Zeitrahmen für das Fahrpreisvalidierungsereignis zu Beginn des Fahrpreisabschnitts.<br><br> Die „Startzeit“ der Fahrstrecke ist die Zeit, zu der das Ereignis planmäßig stattfinden soll. Beispielsweise könnte die Zeit die planmäßige departure eines Busses zu Beginn einer Fahrstrecke sein, bei der der Fahrgast einsteigt und seinen Fahrpreis entwertet. Für die unten stehende Regelabgleichssemantik wird die Startzeit in Ortszeit berechnet, wie durch [Lokalzeitsemantik](#timeframe-local-time-semantics) von [timeframes.txt](#timeframestxt) bestimmt. Die Haltestelle oder Station des departure der Fahrstrecke sollte gegebenenfalls zur Zeitzonenauflösung verwendet werden.<br><br> Für eine Tarifregel für Strecken, die eine `from_timeframe_group_id` angibt, wird diese Regel auf eine bestimmte Strecke zutreffen, wenn t

hier existiert mindestens ein Datensatz in [timeframes.txt](#timeframestxt), bei dem alle der folgenden Bedingungen zutreffen<br> – Der Wert von „timeframe_group_id“ ist gleich dem Wert „from_timeframe_group_id“.<br> - Die durch die service_id des Datensatzes identifizierte Menge an Tagen enthält den „aktuellen Tag“ der Startzeit der Fahrstrecke.<br> - Die Tageszeit der Startzeit des Fahrabschnitts ist größer oder gleich dem Wert „timeframes.start_time“ des Datensatzes und kleiner als der Wert „timeframes.end_time“.<br><br> Eine leere `fare_leg_rules.from_timeframe_group_id` gibt an, dass die Startzeit der Teilstrecke keinen Einfluss auf die Übereinstimmung mit dieser Regel hat. | 
 | `to_timeframe_group_id` | Fremd-ID mit Referenz auf `timeframes.timeframe_group_id` | Optional | Definiert den Zeitrahmen für das Fahrpreisvalidierungsereignis am Ende der Teilstrecke.<br><br> Die „Endzeit“ der Fahrstrecke ist die Zeit, zu der das Ereignis planmäßig stattfinden soll. Beispielsweise könnte die Zeit die planmäßige arrival eines Busses am Ende einer Fahrstrecke sein, wo der Fahrgast aussteigt und seinen Fahrpreis entwertet. Für die unten stehende Regelabgleichssemantik wird die Endzeit in Ortszeit berechnet, wie durch [Lokalzeitsemantik](#timeframe-local-time-semantics) von [timeframes.txt](#timeframestxt) bestimmt. Die Haltestelle oder Station des arrival der Fahrstrecke sollte gegebenenfalls zur Zeitzonenauflösung verwendet werden.<br><br> Für eine Tarifabschnittsregel, die eine `to_timeframe_group_id` angibt, wird diese Regel auf einen bestimmten Abschnitt zutreffen, wenn mindestens ein Datensatz in [timeframes.txt](#timeframestxt) vorhanden ist, bei dem alle der folgenden Bedingungen erfüllt sind<br> – Der Wert von „timeframe_group_id“ ist gleich dem Wert „to_timeframe_group_id“.<br> - Die durch die service_id des Datensatzes identifizierte Menge an Tagen enthält den „aktuellen Tag“ der Endzeit der Fahrstrecke.<br> - Die Tageszeit der Endzeit des Fahrabschnitts ist größer oder gleich dem Wert „timeframes.start_time“ des Datensatzes und kleiner als der Wert „timeframes.end_time“.<br><br> Eine leere `fare_leg_rules.to_timeframe_group_id` gibt an, dass die Endzeit des Abschnitts keinen Einfluss auf die Übereinstimmung mit dieser Regel hat. | 
 | `fare_product_id` | Ausländische ID mit Referenz auf `fare_products.fare_product_id` | **Erforderlich** | Das für die Fahrt auf dem Abschnitt erforderliche Fahrpreisprodukt. | 
 | `rule_priority` | Nicht negative Ganzzahl | Optional | Definiert die Prioritätsreihenfolge, in der Übereinstimmungsregeln auf Abschnitte angewendet werden, wobei bestimmte Regeln Vorrang vor anderen haben können. Wenn mehrere Einträge in `fare_leg_rules.txt` übereinstimmen, wird die Regel oder der Regelsatz mit dem höchsten Wert für `rule_priority` ausgewählt.<br><br> Ein leerer Wert für „rule_priority“ wird als Null behandelt. | 
 
### fare_transfer_rules.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`from_leg_group_id, to_leg_group_id, fare_product_id, transfer_count, duration_limit`) 
 
 Tarifregeln für transfers zwischen Reiseabschnitten, definiert in [`fare_leg_rules.txt`](#fare_leg_rulestxt). 
 
 So verarbeiten Sie die Kosten einer Fahrt mit mehreren Abschnitten: 
 
 1. Die in „fare_leg_rules.txt“ definierten anwendbaren Tarifabschnittsgruppen sollten für alle einzelnen Reiseabschnitte basierend auf der Fahrt des Fahrgastes bestimmt werden. 
 2. Die Datei [fare_transfer_rules.txt](#fare_transfer_rulestxt) muss nach den Feldern gefiltert werden, die die Merkmale des Transfers definieren. Diese Felder sind: 
 - `fare_transfer_rules.from_leg_group_id` 
 - `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 
 3. Wenn die Überweisung hinsichtlich ihrer Merkmale genau mit einem Datensatz in [fare_transfer_rules.txt](#fare_transfer_rulestxt) übereinstimmt, muss dieser Datensatz verarbeitet werden, um die Überweisungskosten zu ermitteln. 
 4. Wenn keine exakten Übereinstimmungen gefunden werden, müssen zur Verarbeitung der Umsteigekosten leere Einträge in „from_leg_group_id“ oder „to_leg_group_id“ geprüft werden: 
 - Ein leerer Eintrag in „fare_transfer_rules.from_leg_group_id“ entspricht allen unter „fare_leg_rules.leg_group_id“ definierten Streckengruppen, mit Ausnahme der unter „fare_transfer_rules.from_leg_group_id“ aufgeführten. 
 - Ein leerer Eintrag in „fare_transfer_rules.to_leg_group_id“ entspricht allen unter „fare_leg_rules.leg_group_id“ definierten Streckengruppen, mit Ausnahme der unter „fare_transfer_rules.to_leg_group_id“ aufgeführten.<br/> 
<br/> 
 5. Erfüllt die Übertragung keine der oben beschriebenen Regeln, liegt keine Übertragungsvereinbarung vor und die beiden Zweige werden als getrennt betrachtet. 
 
<br/> 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `from_leg_group_id` | Ausländische ID mit Referenz auf `fare_leg_rules.leg_group_id` | Optional | Identifiziert eine Gruppe von Fahrpreisregeln vor dem Transfer.<br><br> Wenn es keine passenden `fare_transfer_rules.from_leg_group_id`-Werte für die gefilterte `leg_group_id` gibt, wird standardmäßig eine leere `fare_transfer_rules.from_leg_group_id`-Werte verwendet.<br><br> Ein leerer Eintrag in „fare_transfer_rules.from_leg_group_id“ entspricht allen unter „fare_leg_rules.leg_group_id“ definierten Streckengruppen, mit Ausnahme der unter „fare_transfer_rules.from_leg_group_id“ aufgeführten. | 
 | „to_leg_group_id“ | Ausländische ID mit Referenz auf „fare_leg_rules.leg_group_id“ | Optional | Identifiziert eine Gruppe von Fahrpreisstreckenregeln nach dem Transfer.<br><br> Wenn es keine passenden `fare_transfer_rules.to_leg_group_id`-Werte für die gefilterte `leg_group_id` gibt, wird standardmäßig eine Übereinstimmung mit leeren `fare_transfer_rules.to_leg_group_id` gefunden.<br><br> Ein leerer Eintrag in „fare_transfer_rules.to_leg_group_id“ entspricht allen unter „fare_leg_rules.leg_group_id“ definierten Streckengruppen, mit Ausnahme der unter „fare_transfer_rules.to_leg_group_id“ aufgeführten. | 
 | „transfer_count“ | Ganzzahl ungleich Null | **Bedingt verboten** | Definiert, auf wie viele aufeinanderfolgende transfers die Transferregel angewendet werden kann.<br><br> Gültige Optionen sind:<br> `-1` – Keine Begrenzung.<br> „`1`“ oder mehr – Definiert, wie viele transfers die Übertragungsregel umfassen darf.<br><br> Wenn eine Teilreise mit mehreren Datensätzen mit unterschiedlichen `transfer_count`s übereinstimmt, dann ist die Regel mit dem minimalen `transfer_count` auszuwählen, der größer oder gleich dem aktuellen Transfercount der Teilreise ist.<br><br> Bedingt verboten:<br> - **Verboten**, wenn „fare_transfer_rules.from_leg_group_id“ nicht gleich „fare_transfer_rules.to_leg_group_id“ ist.<br> - **Erforderlich**, wenn „fare_transfer_rules.from_leg_group_id“ gleich „fare_transfer_rules.to_leg_group_id“ ist. | 
 | „duration_limit“ | Positive Ganzzahl | Optional | Definiert die Zeitbegrenzung des Transfers.<br><br> Muss in ganzzahligen Sekundenschritten ausgedrückt werden.<br><br> Wenn keine Zeitbegrenzung vorhanden ist, muss „fare_transfer_rules.duration_limit“ leer sein. | 
 | „duration_limit_type“ | Enum | **Bedingt erforderlich** | Definiert den relativen Anfang und das Ende von „fare_transfer_rules.duration_limit“.<br><br> Gültige Optionen sind:<br> „0“ – Zwischen der departure des aktuellen Abschnitts und der arrival des nächsten Abschnitts.<br> „`1`“ – Zwischen der departure der aktuellen Strecke und der departure der nächsten Strecke.<br> „2“ – Zwischen der arrival des aktuellen Abschnitts und der departure des nächsten Abschnitts.<br> „3“ – Zwischen der arrival der aktuellen Strecke und der arrival der nächsten Strecke.<br><br> Bedingt erforderlich:<br> - **Erforderlich**, wenn „fare_transfer_rules.duration_limit“ definiert ist.<br> - **Verboten**, wenn „fare_transfer_rules.duration_limit“ leer ist. | 
 | „fare_transfer_type“ | Enum | **Erforderlich** | Gibt die Kostenverarbeitungsmethode für den Transfer zwischen Teilstrecken einer Reise an:<br> ![](../../assets/2-leg.svg)<br> Gültige Optionen sind:<br> `0` – Von-Teilstrecke `fare_leg_rules.fare_product_id` plus `fare_transfer_rules.fare_product_id`; A + AB.<br> `1` - Von-Teilstrecke `fare_leg_rules.fare_product_id` plus `fare_transfer_rules.fare_product_id` plus Rück-Teilstrecke `fare_leg_rules.fare_product_id`; A + AB + B.<br> `2` - `fare_transfer_rules.fare_product_id`; AB.<br><br> Kostenverarbeitungsinteraktionen zwischen mehreren transfers auf einer Reise:<br> ![](../../assets/3-leg.svg)<br><table><thead><tr><th> `fare_transfer_type`</th><th> Verarbeitung A > B</th><th> Verarbeitung B > C</th></tr></thead><tbody><tr><td> `0`</td><td> A + AB</td><td> S + BC</td></tr><tr><td> `1`</td><td> A + AB +B</td><td> S + BC + C</td></tr><tr><td> `2`</td><td> AB</td><td> S + BC</td></tr></tbody></table> Wobei S die gesamten verarbeiteten Kosten der vorhergehenden Strecke(n) und Umstiege angibt. | 
 | `fare_product_id` | Ausländische ID mit Referenz auf `fare_products.fare_product_id` | Optional | Das für den Umstieg zwischen zwei Fahrpreisstrecken erforderliche Fahrpreisprodukt. Wenn leer, betragen die Kosten der Umstiegsregel 0.| 
 
 
### areas.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`area_id`) 
 
 Definiert Bereichskennungen. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `area_id` | Eindeutige ID | **Erforderlich** | Identifiziert einen Bereich. Muss in [areas.txt](#areastxt) eindeutig sein. | 
 | `area_name` | Text | **Optional** | Der Name des Gebiets, wie er dem Fahrer angezeigt wird. | 
 
### stop_areas.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`*`) 
 
 Weist stops aus [stops.txt](#stopstxt) Gebieten zu. 
 
 | Feldname | Typ | Vorkommen | Beschreibung | 
 |------|------|------|------| 
 | `area_id` | Fremd-ID, die auf `areas.area_id` verweist | **Erforderlich** | Identifiziert ein Gebiet, zu dem eine oder mehrere `stop_id` gehören. Dieselbe „`stop_id`“ kann in vielen „area_id“ definiert sein. | 
 | „`stop_id`“ | Ausländische ID mit Referenz auf „stops.stop_id“ | **Erforderlich** | Identifiziert eine Haltestelle. Wenn in diesem Feld eine Station (d.h. eine Haltestelle mit „stops.location_type=1“) definiert ist, wird angenommen, dass alle ihre Bahnsteige (d.h. alle stops mit „stops.location_type=0“, bei denen diese Station als „stops.parent_station“ definiert ist) Teil desselben Bereichs sind. Dieses Verhalten kann überschrieben werden, indem Bahnsteige anderen Bereichen zugewiesen werden. | 
 
### networks.txt 
 
 Datei: **Bedingt verboten** 
 
 Primärschlüssel („network_id“) 
 
 Definiert Netzwerkkennungen, die für Fahrpreisregeln gelten. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `network_id` | Eindeutige ID | **Erforderlich** | Identifiziert ein Netzwerk. Muss in [networks.txt](#networkstxt) eindeutig sein. | 
 | `network_name` | Text | **Optional** | Der Name des Netzwerks, für das die Fahrpreisregeln gelten, wie sie von der örtlichen agency und ihren Fahrgästen verwendet werden. 
 
### route_networks.txt 
 
 Datei: **Bedingt verboten** 
 
 Primärschlüssel (`route_id`) 
 
 Weist Netzwerken routes aus [routes.txt](#routestxt) zu. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `network_id` | Fremd-ID mit Referenz auf `networks.network_id` | **Erforderlich** | Identifiziert ein Netzwerk, zu dem eine oder mehrere `route_id` s gehören. Eine `route_id` kann nur in einer `network_id` definiert werden. | 
 | `route_id` | Fremd-ID mit Referenz auf `routes.route_id` | **Erforderlich** | Identifiziert eine Route. | 
 
### shapes.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`shape_id`, `shape_pt_sequence`) 
 
 Shapes beschreiben den Weg, den ein vehicle entlang einer Routenführung zurücklegt, und werden in der Datei shapes.txt definiert. Shapes sind mit Fahrten verknüpft und bestehen aus einer Abfolge von Punkten, die das vehicle der Reihe nach durchfährt. Shapes müssen die Position der Haltestellen nicht exakt schneiden, aber alle Haltestellen einer Fahrt sollten in geringer Entfernung vom shape für diese Fahrt liegen, d.h. in der Nähe von geraden Liniensegmenten, die die shape Punkte verbinden. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `shape_id` | ID | **Erforderlich** | Identifiziert ein shape. | 
 | `shape_pt_lat` | Breitengrad | **Erforderlich** | Breitengrad eines shape Punkts. Jeder Datensatz in [shapes.txt](#shapestxt) stellt einen shape Punkt dar, der zum Definieren des shape verwendet wird. | 
 | `shape_pt_lon` | Längengrad | **Erforderlich** | Längengrad eines shape Punkts. | 
 | `shape_pt_sequence` | Nicht-negative Ganzzahl | **Erforderlich** | Reihenfolge, in der die shape verbunden werden, um die shape zu bilden. Die Werte müssen während der Reise zunehmen, müssen aber nicht aufeinander folgen.<hr> *Beispiel: Wenn die shape „A_shp“ drei Punkte in ihrer Definition hat, könnte die Datei [shapes.txt](#shapestxt) diese Datensätze zur Definition der shape enthalten:*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence`<br> `A_shp,37.61956,-122.48161,0`<br> `A_shp,37.64430,-122.41070,6`<br> `A_shp,37.65863,-122.30839,11` | 
 | `shape_dist_traveled` | Nicht negativer float | Optional | Tatsächlich zurückgelegte Distanz entlang der shape vom ersten shape bis zum in diesem Datensatz angegebenen Punkt. Wird von Reiseplanern verwendet, um den richtigen Teil der shape auf einer Karte anzuzeigen. Werte müssen zusammen mit `shape_pt_sequence` ansteigen; sie dürfen nicht verwendet werden, um die Rückwärtsfahrt entlang einer Route anzuzeigen. Entfernungseinheiten müssen mit denen in [stop_times.txt](#stop_timestxt) übereinstimmen.<br><br> Empfohlen für routes mit Schleifen oder Inline-Strecken (das vehicle kreuzt oder befährt denselben Streckenabschnitt in einer Fahrt). <br><img src="../../../assets/inlining.svg" width=200px style="display: block; margin-left: auto; margin-right: auto;"><br> Wenn ein vehicle im Verlauf einer Fahrt an bestimmten Punkten die Routenführung zurückverfolgt oder kreuzt, ist „shape_dist_traveled“ wichtig, um zu verdeutlichen, wie Teile der Punkte in der Reihe [shapes.txt](#shapestxt) mit den Datensätzen in [stop_times.txt](#stop_timestxt) übereinstimmen.<hr> *Beispiel: Wenn ein Bus entlang der drei oben für A_shp definierten Punkte fährt, würden die zusätzlichen `shape_dist_traveled`-Werte (hier in Kilometern angezeigt) wie folgt aussehen:*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shape_dist_traveled`<br> `A_shp,37.61956,-122.48161,0,0`<br> `A_shp,37.64430,-122.41070,6,6.8310`<br> `A_shp,37.65863,-122.30839,11,15.8765` | 
 
### frequencies.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`trip_id`, `start_time`) 
 
 [Frequencies.txt](#frequenciestxt) repräsentiert Fahrten mit regelmäßigen Taktzeiten (Zeit zwischen den Fahrten). Diese Datei kann verwendet werden, um zwei verschiedene Arten von Diensten darzustellen. 
 
 * Taktbasierter Dienst (`exact_times`=`0`), bei dem der Dienst nicht den ganzen Tag über einem festen Zeitplan folgt. Stattdessen versuchen die Betreiber, vorgegebene Taktzeiten für die Fahrten strikt einzuhalten. 
 * Eine komprimierte Darstellung eines fahrplanbasierten Services (`exact_times`= `1`), bei dem für Fahrten in angegebenen Zeiträumen exakt die gleiche Taktfrequenz eingehalten wird. Bei fahrplanbasierten Services versuchen die Betreiber, sich strikt an einen Zeitplan zu halten. 
 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `trip_id` | Ausländische ID mit Referenz auf `trips.trip_id` | **Erforderlich** | Identifiziert eine Fahrt, für die die angegebene Taktfrequenz gilt. | 
 | `start_time` | Uhrzeit | **Erforderlich** | Uhrzeit, zu der das erste vehicle mit der angegebenen Taktfrequenz von der ersten Haltestelle der Fahrt abfährt. | 
 | `end_time` | Uhrzeit | **Erforderlich** | Uhrzeit, zu der der Service an der ersten Haltestelle der Fahrt zu einer anderen Taktfrequenz wechselt (oder endet). | 
 | `headway_secs` | Positive Ganzzahl | **Erforderlich** | Zeit in Sekunden zwischen Abfahrten von derselben Haltestelle (Headway) für die Fahrt während des durch `start_time` und `end_time angegebenen Zeitintervalls. Für dieselbe Fahrt können mehrere Headways definiert werden, sie dürfen sich jedoch nicht überschneiden. Neue Headways können genau zu dem Zeitpunkt beginnen, zu dem das vorherige Headway endet. | 
 | `exact_times` | Enum | Optional | Gibt die Art des Dienstes für eine Fahrt an. Weitere Informationen finden Sie in der Dateibeschreibung. Gültige Optionen sind:<br><br> „0“ oder leer – Häufigkeitsbasierte Fahrten.<br> `1` - Fahrplanbasierte Fahrten mit exakt demselben Taktabstand über den ganzen Tag. In diesem Fall muss der Wert von `end_time größer sein als die `start_time` der letzten gewünschten Fahrt, aber kleiner als die `start_time der letzten gewünschten Fahrt + `headway_secs`. | 
 
### transfers.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`from_stop_id, `to_stop_id, `from_trip_id, `to_trip_id, `from_route_id, `to_route_id) 
 
 Beim Berechnen einer Reiseroute interpolieren GTFS-verwendende Anwendungen transfers basierend auf der zulässigen Zeit und der Haltestellennähe. [.txt](#transferstxt) gibt zusätzliche Regeln und Überschreibungen für ausgewählte transfers an. 
 
 Die Felder `from_trip_id`, `to_trip_id`, `from_route_id` und `to_route_id` ermöglichen höhere Spezifitätsgrade für Umsteigeregeln. Zusammen mit `from_stop_id` und `to_stop_id` ist die Rangfolge der Spezifität wie folgt: 
 
 1. Beide `trip_id` s sind definiert: `from_trip_id` und `to_trip_id`. 
 2. Ein `trip_id` und `route_id` Satz definiert: (`from_trip_id` und `to_route_id`) oder (`from_route_id` und `to_trip_id`). 
 3. Eine `trip_id` definiert: `from_trip_id` oder `to_trip_id`. 
 4. Beide `route_id` s sind definiert: `from_route_id` und `to_route_id`. 
 5. Eine „`route_id`“ definiert: „from_route_id“ oder „to_route_id“. 
 6. Nur „from_stop_id“ und „to_stop_id“ definiert: keine routen- oder fahrtbezogenen Felder festgelegt. 
 
 Für ein gegebenes geordnetes Paar aus ankommender und abfahrender Fahrt wird der Umstieg mit der größten Spezifität ausgewählt, der zwischen diesen beiden Fahrten gilt. Für kein Fahrtpaar sollten zwei transfers mit gleich maximaler Spezifität gelten können. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | „from_stop_id“ | Ausländische ID mit Referenz auf „stops.stop_id“ | **Bedingt erforderlich** | Identifiziert eine Haltestelle oder Station, an der eine Verbindung zwischen routes beginnt. Wenn sich dieses Feld auf eine Station bezieht, gilt die Umstiegsregel für alle ihre untergeordneten stops. Die Bezugnahme auf einen Bahnhof ist für die `transfer_types` 4 und 5. verboten. | 
 | `to_stop_id` | Fremd-ID mit Bezugnahme auf `stops.stop_id` | **Bedingt erforderlich** | Identifiziert eine Haltestelle oder einen Bahnhof, an dem eine Verbindung zwischen routes endet. Wenn dieses Feld auf einen Bahnhof verweist, gilt die Umsteigeregel für alle untergeordneten stops. Die Bezugnahme auf einen Bahnhof ist für die `transfer_types` 4 und 5. verboten. | 
 | `from_route_id` | Fremd-ID mit Bezugnahme auf `routes.route_id` | Optional | Identifiziert eine Route, an der eine Verbindung beginnt.<br><br> Wenn „from_route_id“ definiert ist, gilt der Umstieg für die ankommende Fahrt auf der Route für die angegebene „from_stop_id“.<br><br> Wenn sowohl „from_trip_id“ als auch „from_route_id“ definiert sind, muss die „`trip_id`“ zur „`route_id`“ gehören und „from_trip_id“ hat Vorrang. | 
 | „to_route_id“ | Fremd-ID mit Referenzierung auf „routes.route_id“ | Optional | Identifiziert eine Route, an der eine Verbindung endet.<br><br> Wenn „to_route_id“ definiert ist, gilt der Umstieg für die Abfahrtsfahrt auf der Route mit der angegebenen „to_stop_id“.<br><br> Wenn sowohl „to_trip_id“ als auch „to_route_id“ definiert sind, muss die „`trip_id`“ zur „`route_id`“ gehören und „to_trip_id“ hat Vorrang. | 
 | „from_trip_id“ | Fremd-ID mit Referenz auf „`trips.trip_id` “ | **Bedingt erforderlich** | Identifiziert eine Fahrt, bei der eine Verbindung zwischen routes beginnt.<br><br> Wenn „from_trip_id“ definiert ist, gilt der Transfer für die ankommende Fahrt zur angegebenen „from_stop_id“.<br><br> Wenn sowohl „from_trip_id“ als auch „from_route_id“ definiert sind, muss die „`trip_id`“ zur „`route_id`“ gehören und „from_trip_id“ hat Vorrang. ERFORDERLICH, wenn „transfer_type“ „4“ oder „5“ ist. | 
 | „to_trip_id“ | Fremd-ID mit Referenz auf „`trips.trip_id` “ | **Bedingt erforderlich** | Identifiziert eine Fahrt, bei der eine Verbindung zwischen routes endet.<br><br> Wenn „to_trip_id“ definiert ist, gilt der Transfer für die Abfahrtsfahrt zur angegebenen „to_stop_id“.<br><br> Wenn sowohl `to_trip_id` als auch `to_route_id` definiert sind, muss die `trip_id` zur `route_id` gehören und `to_trip_id` hat Vorrang. ERFORDERLICH, wenn `transfer_type` `4` oder `5` ist. | 
 | `transfer_type` | Enum | **Erforderlich** | Gibt den Verbindungstyp für das angegebene Paar (`from_stop_id`, `to_stop_id`) an. Gültige Optionen sind:<br><br> „0“ oder leer – Empfohlener Umsteigepunkt zwischen routes.<br> `1` - Zeitlich festgelegter Umsteigepunkt zwischen zwei routes. Das abfahrende vehicle muss auf das ankommende warten und dem Fahrgast ausreichend Zeit zum Umsteigen zwischen den routes lassen.<br> `2` - Beim Umsteigen ist eine amount zwischen arrival und departure erforderlich, um einen Anschluss zu gewährleisten. Die zum Umsteigen benötigte Zeit wird durch `min_transfer_time` angegeben.<br> `3` - Umsteigen zwischen den routes ist am Standort nicht möglich.<br> `4` - Passagiere können von einer Fahrt auf eine andere umsteigen, indem sie im selben vehicle bleiben (ein „Umsteigen am Sitzplatz“). Weitere Einzelheiten zu dieser Art des Umsteigens [unten](#linked-trips).<br> `5` - transfers im Sitz ist zwischen aufeinanderfolgenden Fahrten nicht erlaubt. Der Fahrgast muss das vehicle aussteigen und wieder einsteigen. Weitere Einzelheiten zu dieser Art des Umsteigens [unten](#linked-trips). | 
 | `min_transfer_time` | Nicht-negative Ganzzahl | Optional | Zeitdauer in Sekunden, die für ein Umsteigen zwischen routes an den angegebenen stops zur Verfügung stehen muss. Die `min_transfer_time` sollte ausreichen, damit sich ein typischer Fahrgast zwischen den beiden stops bewegen kann, einschließlich Pufferzeit für Fahrplanabweichungen auf jeder Route. | 
 
#### Verknüpfte Fahrten 
 
 Folgendes gilt für `transfer_type=4` und `=5`, die zum Verknüpfen von Fahrten mit oder ohne transfers im Sitz verwendet werden. 
 
 Die verknüpften Fahrten MÜSSEN mit demselben vehicle durchgeführt werden. Das vehicle DARF an andere Fahrzeuge angekoppelt oder von ihnen abgekoppelt werden. 
 
 Wenn sowohl eine Übertragung für verknüpfte Fahrten als auch eine block_id angegeben werden und diese zu widersprüchlichen Ergebnissen führen, ist die Übertragung für verknüpfte Fahrten zu verwenden. 
 
 Die letzte Haltestelle von „from_trip_id“ SOLLTE geografisch nahe an der ersten Haltestelle von „to_trip_id“ liegen, und die letzte arrival von „from_trip_id“ SOLLTE vor, aber nahe an der ersten departure von „to_trip_id“ liegen. Die letzte arrival von „from_trip_id“ KANN später als die erste departure von „to_trip_id“ sein, falls die Fahrt mit „to_trip_id“ am darauffolgenden Betriebstag stattfindet. 
 
 Fahrten KÖNNEN im Normalfall 1-zu-1 verknüpft werden, KÖNNEN aber auch 1-zu-n, n-zu-1 oder n-zu-n verknüpft werden, um komplexere Fahrtfortsetzungen darzustellen. Beispielsweise können zwei Zugfahrten (Fahrt A und Fahrt B im Diagramm unten) nach einem vehicle an einem gemeinsamen Bahnhof zu einer einzigen Zugfahrt (Fahrt C) zusammengeführt werden: 
 
 - In einer 1-zu-n-Fortsetzung MUSS die `trips.service_id` für jede `to_trip_id` identisch sein. 
 - In einer n-zu-1-Fortsetzung MUSS die `trips.service_id` für jede `from_trip_id` identisch sein. 
 - n-zu-n-Fortsetzungen müssen beide Einschränkungen einhalten. 
 - Fahrten können als Teil mehrerer einzelner Fortsetzungen miteinander verknüpft werden, vorausgesetzt, dass sich die `trip.service_id` an keinem Betriebstag überschneiden DÜRFEN. 
 
<pre> 
 Störung A 
 ──────────────────\ 
 \ Störung C 
 ─────────────── 
 Störung B/
 ────────────────────/
</pre> 
 
### pathways.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`pathway_id`) 
 
 Die Dateien [pathways.txt](#pathwaystxt) und [levels.txt](#levelstxt) verwenden eine grafische Darstellung zur Beschreibung von U-Bahn- oder Bahnhöfen, wobei Knoten Standorte und Kanten pathways darstellen. 
 
 Um vom Eingang/Ausgang der Station (ein Knoten, der als Standort mit `location_type=2` dargestellt wird) zu einem Bahnsteig (ein Knoten, der als Standort mit `location_type=0` oder leer dargestellt wird) zu navigieren, bewegt sich der Passagier über Gehwege, Fahrkartenschranken, Treppen und andere Kanten, die als pathways dargestellt werden. Generische Knoten (Knoten, die mit `location_type=3` dargestellt werden) können verwendet werden, um pathways in einer Station zu verbinden. 
 
 In einem Bahnhof müssen Wege vollständig definiert sein. Wenn pathways definiert sind, wird davon ausgegangen, dass alle pathways im gesamten Bahnhof vertreten sind. Daher gelten die folgenden Richtlinien: 
 
 - Keine offenen Standorte: Wenn ein Standort innerhalb eines Bahnhofs einen Weg hat, dann sollten alle Standorte innerhalb dieses Bahnhofs pathways haben, mit Ausnahme von Bahnsteigen mit Einstiegsbereichen (`location_type=4`, siehe Richtlinie unten). 
 - Keine pathways für einen Bahnsteig mit Einstiegsbereichen: Ein Bahnsteig (`location_type=0` oder leer), der Einstiegsbereiche (`location_type=4`) hat, wird als übergeordnetes Objekt und nicht als Punkt behandelt. In solchen Fällen dürfen dem Bahnsteig keine pathways zugewiesen sein. Alle pathways sollten für jeden Einstiegsbereich des Bahnsteigs zugewiesen sein. 
 - Keine gesperrten Bahnsteige: Jeder Bahnsteig (`location_type=0` oder leer) oder Einstiegsbereich (`location_type=4 `) muss über eine Kette von pathways mit mindestens einem Eingang/Ausgang (` location_type=2 `) verbunden sein. Bahnhöfe, die von einem bestimmten Bahnsteig aus keinen Weg nach draußen zulassen, sind selten. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | ` pathway_id` | Eindeutige ID | **Erforderlich** | Identifiziert einen Weg. Wird von Systemen als interne Kennung für den Datensatz verwendet. Muss im Datensatz eindeutig sein.<br><br> Verschiedene pathways können die gleichen Werte für „from_stop_id“ und „to_stop_id“ haben.<hr> _Beispiel: Wenn zwei Rolltreppen in entgegengesetzter Richtung nebeneinander liegen oder wenn eine Treppe und ein Aufzug vom selben Ort zum selben Ort führen, können unterschiedliche „pathway_id“ dieselben Werte für „from_stop_id“ und „to_stop_id“ haben._| 
 | „from_stop_id“ | Fremd-ID mit Referenz auf „stops.stop_id“ | **Erforderlich** | Ort, an dem der Weg beginnt.<br><br> Muss eine „`stop_id`“ enthalten, die eine Plattform identifiziert („lo

cation_type=0` oder leer), Eingang/Ausgang (`location_type=2`), generischer Knoten (`location_type=3`) oder Einstiegsbereich (`location_type=4`).<br><br> Werte für `stop_id`, die Stationen identifizieren (`location_type=1`), sind verboten.| 
 | `to_stop_id` | Ausländische ID mit Referenz auf `stops.stop_id` | **Erforderlich** | Ort, an dem der Weg endet.<br><br> Muss eine „`stop_id`“ enthalten, die einen Bahnsteig („location_type=0“ oder leer), einen Eingang/Ausgang („location_type=2“), einen allgemeinen Knoten („location_type=3“) oder einen Einstiegsbereich („location_type=4“) identifiziert.<br><br> Werte für `stop_id`, die Stationen identifizieren (`location_type=1`), sind verboten.| 
 | `pathway_mode` | Enum | **Erforderlich** | Art des Pfades zwischen dem angegebenen Paar (`from_stop_id`, `to_stop_id`). Gültige Optionen sind:<br><br> `1` - Gehweg.<br> `2` - Treppe.<br> `3` - Fahrsteig/Fahrsteig.<br> `4` - Rolltreppe.<br> `5` - Aufzug.<br> `6` - Fahrkartenschranke (oder Zahlungsschranke): Ein Weg, der in einen Bereich der Station führt, in dem zum Überqueren ein Zahlungsnachweis erforderlich ist. Fahrkartenschranken können gebührenpflichtige Bereiche der Station von ungebührenpflichtigen trennen oder verschiedene Zahlungsbereiche innerhalb derselben Station voneinander trennen. Diese Informationen können verwendet werden, um zu vermeiden, dass Passagiere über Abkürzungen durch Stationen geleitet werden, die von den Passagieren unnötige Zahlungen require würden, wie z. B. wenn ein Passagier angewiesen wird, über einen U-Bahnsteig zu einer Bushaltestelle zu gehen.<br> `7`- Ausgangstor: Ein Weg, der aus einem gebührenpflichtigen Bereich in einen ungebührenpflichtigen Bereich führt und für dessen Überquerung kein Zahlungsnachweis erforderlich ist.| 
 | `ist is_bidirectional` | Enum | **Erforderlich** | Gibt die Richtung an, in der der Weg genommen werden kann:<br><br> `0` – Unidirektionaler Pfad, der nur von `from_stop_id` bis `to_stop_id` verwendet werden kann.<br> „`1`“ – Bidirektionaler Pfad, der in beide Richtungen verwendet werden kann.<br><br> Ausgänge (`pathway_mode=7`) dürfen nicht bidirektional sein.| 
 | `Länge` | Nicht negativer float | Optional | Horizontale Länge des Pfads in Metern vom Ausgangsort (definiert in `from_stop_id`) zum Zielort (definiert in `to_stop_id`).<br><br> Dieses Feld wird für Gehwege (`pathway_mode=1`), Fahrkartenschranken (`pathway_mode=6`) und Ausgänge (`pathway_mode=7`) empfohlen.| 
 | `traversal_time` | Positive Ganzzahl | Optional | Durchschnittliche Zeit in Sekunden, die benötigt wird, um den Weg vom Ausgangspunkt (definiert in `from_stop_id`) zum Zielort (definiert in `to_stop_id`) zu gehen.<br><br> Dieses Feld wird für Fahrsteige (`pathway_mode=3`), Rolltreppen (`pathway_mode=4`) und Aufzüge (`pathway_mode=5`) empfohlen.| 
 | `stair_count` | Ganzzahl ungleich Null | Optional | Anzahl der Stufen des Gehwegs.<br><br> Ein positiver `stair_count` bedeutet, dass der Fahrer von `from_stop_id` nach `to_stop_id` hochläuft. Und ein negativer `stair_count` bedeutet, dass der Fahrer von `from_stop_id` nach `to_stop_id` herunterläuft.<br><br> Dieses Feld wird für Treppen empfohlen (`pathway_mode=2`).<br><br> Wenn nur eine geschätzte Treppenanzahl angegeben werden kann, wird empfohlen, 15 Treppen für 1 Stockwerk zu schätzen.| 
 | `max_slope` | Float | Optional | Maximales Steigungsverhältnis des Weges. Gültige Optionen sind:<br><br> „0“ oder leer – Keine Steigung.<br> „Float“ – Steigungsverhältnis des Pfades, positiv für aufwärts, negativ für abwärts.<br><br> Dieses Feld sollte nur bei Gehwegen (`pathway_mode=1`) und Fahrsteigen (`pathway_mode=3`) verwendet werden.<hr> _Beispiel: In den USA beträgt 0,083 (auch 8,3 % geschrieben) die maximale Steigungsrate für handbetriebene Rollstühle, was einer Zunahme von 0,083 m (also 8,3 cm) pro Meter entspricht._| 
 | `min_width` | Positiver float | Optional | Mindestbreite des Weges in Metern.<br><br> Dieses Feld wird empfohlen, wenn die Mindestbreite weniger als 1 Meter beträgt.| 
 | `signposted_as` | Text | Optional | Öffentlich sichtbarer Text von physischer Beschilderung, der für Fahrer sichtbar ist.<br><br> Kann verwendet werden, um Fahrern Textanweisungen zu geben, z. B. „Folgen Sie den Schildern nach“. Der Text in „singposted_as“ sollte genau so erscheinen, wie er auf den Schildern gedruckt ist.<br><br> Wenn die physische Beschilderung mehrsprachig ist, kann dieses Feld nach dem Beispiel von „stops.stop_name“ in der Felddefinition von „feed_info.feed_lang“ ausgefüllt und übersetzt werden.| 
 | „reversed_signposted_as“ | Text | Optional | Dasselbe wie „signposted_as“, aber wenn der Weg von „to_stop_id“ zur „from_stop_id“ verwendet wird.| 
 
### levels.txt 
 
 Datei: **Bedingt erforderlich** 
 
 Primärschlüssel („level_id“) 
 
 Beschreibt die Ebenen in einer Station. Nützlich in Verbindung mit [pathways.txt](#pathwaystxt). 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `level_id` | Eindeutige ID | **Erforderlich** | Identifiziert eine Ebene in einer Station.| 
 | `level_index` | Float | **Erforderlich** | Numerischer Index der Ebene, der ihre relative position angibt.<br><br> Das Erdgeschoss sollte den Index „0“ haben, wobei Ebenen über der Erde durch positive Indizes und Ebenen unter der Erde durch negative Indizes gekennzeichnet sind.| 
 | „level_name“ | Text | Optional | Name der Ebene, wie er vom Benutzer im Gebäude oder in der Station gesehen wird.<hr> _Beispiel: Nehmen Sie den Aufzug zum „Mezzanin“ oder „Bahnsteig“ oder „-1“._| 
 
### location_groups.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`location_group_id`) 
 
 Definiert Standortgruppen, also Gruppen von stops, an denen ein Fahrgast jemanden abholen oder absetzen kann. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |----------|----|------------|-----------| 
 | `location_group_id` | Eindeutige ID | **Erforderlich** | Identifiziert eine Standortgruppe. Die ID muss für alle Werte von `stops.stop_id, locations.geojson `id` und `location_groups.location_group_id` eindeutig sein.<br><br> Eine Standortgruppe ist eine Gruppe von stops, die zusammen Standorte anzeigen, an denen ein Fahrgast eine Abholung oder einen Abtransport anfordern kann. | 
 | „location_group_name“ | Text | Optional | Der Name der Standortgruppe, wie er dem Fahrgast angezeigt wird. | 
 
### location_group_stops.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`*`) 
 
 Weist stops aus stops.txt Standortgruppen zu. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |----------|----|------------|-----------| 
 | „location_group_id“ | Fremd-ID mit Referenz auf „location_groups.location_group_id“ | **Erforderlich** | Identifiziert eine Standortgruppe, zu der eine oder mehrere „`stop_id`“ gehören. Dieselbe „`stop_id`“ kann in vielen „location_group_ids“ definiert sein. | 
 | „`stop_id`“ | Ausländische ID, die auf „stops.stop_id“ verweist | **Erforderlich** | Identifiziert eine Haltestelle, die zur Standortgruppe gehört. | 
 
 
### locations.geojson 
 
 Datei: **Optional** 
 
 Definiert Zonen, in denen Fahrgäste von On-Demand-Diensten abgeholt oder abgesetzt werden können. Diese Zonen werden als GeoJSON-Polygone dargestellt. 
 
 – Diese Datei verwendet eine Teilmenge des GeoJSON-Formats, das in [RFC 7946](https://tools.ietf.org/html/rfc7946) beschrieben wird. 
 – Die Datei „`locations.geojson`“ muss eine „FeatureCollection“ enthalten. 
 – Eine „FeatureCollection“ definiert verschiedene Haltestellen, an denen Fahrgäste Personen abholen oder absetzen können. 
 – Jedes GeoJSON-„Feature“ muss eine „`id`“ haben. Die „`id`“ muss für alle „stops.stop_id“-, „locations.geojson „`id`“- und „location_group_id“-Werte eindeutig sein. 
 – Jedes GeoJSON-„Feature“ sollte Objekte und zugehörige Schlüssel gemäß der folgenden Tabelle haben: 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 |- „Typ“ | Zeichenfolge | **Erforderlich** | „FeatureCollection“ von Standorten. | 
 |- „Features“ | Array | **Erforderlich** | Sammlung von „Feature“-Objekten, die die Standorte beschreiben. | 
 | \- „Typ“ | Zeichenfolge | **Erforderlich** | `"Feature"` | 
 | \- `id` | String | **Erforderlich** | Identifiziert einen Standort. Die ID muss für alle Werte von `stops.stop_id`, locations.geojson `id` und `location_groups.location_group_id` eindeutig sein. | 
 | \- `properties` | Objekt | **Erforderlich** | Standorteigenschaftsschlüssel. | 
 | \- `stop_name` | String | Optional | Gibt den Namen des Standorts an, wie er den Fahrgästen angezeigt wird. | 
 | \- `stop_desc` | String | Optional | Aussagekräftige Beschreibung des Standorts zur Orientierung der Fahrgäste. | 
 | \- `geometry` | Objekt | **Erforderlich** | Geometrie des Standorts. | 
 | \- `type` | String | **Erforderlich** | Muss vom Typ sein:<br> - `"Polygon"`<br> - „MultiPolygon““ | 
 | \- „coordinates“ | Array | **Erforderlich** | Geografische Koordinaten (latitude und longitude), die die Geometrie des Standorts definieren. | 
 
### booking_rules.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel („booking_rule_id“) 
 
 Definiert die Buchungsregeln für vom Fahrer angeforderte Dienste 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | „booking_rule_id“ | Eindeutige ID | **Erforderlich** | Identifiziert eine Regel. | 
 | „booking_type“ | Enum | **Erforderlich** | Gibt an, wie weit im Voraus gebucht werden kann. Gültige Optionen sind:<br><br> `0` – Buchung in Echtzeit.<br> `1` - Bis zur tagesgleichen Buchung mit Voranmeldung.<br> `2` – Bis zur Buchung des/der vorherigen Tages/Tage. | 
 | `prior_notice_duration_min` | Ganzzahl | **Bedingt erforderlich** | Mindestanzahl von Minuten vor Reiseantritt, um die Anfrage zu stellen.<br><br> **Bedingt erforderlich**:<br> - **Erforderlich** für „booking_type=1“.<br> - Andernfalls **verboten**. | 
 | `prior_notice_duration_max` | Integer | **Bedingt verboten** | Maximale Anzahl von Minuten vor Reiseantritt, um die Buchungsanfrage zu stellen.<br><br> **Bedingt verboten**:<br> - **Verboten** für `booking_type=0` und `booking_type=2`.<br> – Optional für „booking_type=1“.| 
 | „prior_notice_last_day“ | Ganzzahl | **Bedingt erforderlich** | Letzter Tag vor Reiseantritt, um die Buchungsanfrage zu stellen.<br><br> Beispiel: „Die Fahrt muss 1 Tag im Voraus vor 17:00 Uhr gebucht werden“ wird als „prior_notice_last_day=1“ codiert.<br><br> **Bedingt erforderlich**:<br> - **Erforderlich** für „booking_type=2“.<br> - Andernfalls **verboten**. | 
 | `prior_notice_last_time` | Uhrzeit | **Bedingt erforderlich** | Letzter Zeitpunkt am letzten Tag vor Reiseantritt, um die Buchungsanfrage zu stellen.<br><br> Beispiel: „Die Fahrt muss 1 Tag im Voraus vor 17:00 Uhr gebucht werden“ wird als „prior_notice_last_time=17:00:00“ kodiert.<br><br> **Bedingt erforderlich**:<br> - **Erforderlich**, wenn „prior_notice_last_day“ definiert ist.<br> - Andernfalls **verboten**. | 
 | `prior_notice_start_day` | Integer | **Bedingt verboten** | Frühester Tag vor Reiseantritt, um die Buchungsanfrage zu stellen.<br><br> Beispiel: „Fahrt kann frühestens eine Woche im Voraus um Mitternacht gebucht werden“ wird als „prior_notice_start_day=7“ kodiert.<br><br> **Bedingt verboten**:<br> - **Verboten** für `booking_type=0`.<br> - **Verboten** für „booking_type=1“, wenn „prior_notice_duration_max“ definiert ist.<br> – Andernfalls optional. | 
 | „prior_notice_start_time“ | Zeit | **Bedingt erforderlich** | Früheste Zeit am frühesten Tag vor Reiseantritt, um die Buchungsanfrage zu stellen.<br><br> Beispiel: „Fahrt kann frühestens eine Woche im Voraus um Mitternacht gebucht werden“ wird als „prior_notice_start_time=00:00:00“ kodiert.<br><br> **Bedingt erforderlich**:<br> - **Erforderlich**, wenn „prior_notice_start_day“ definiert ist.<br> - Andernfalls **verboten**. | 
 | „prior_notice_service_id“ | ID mit Referenz auf „calendar.service_id“ | **Bedingt verboten** | Gibt die Servicetage an, an denen „prior_notice_last_day“ oder „prior_notice_start_day“ gezählt werden.<br><br> Beispiel: Wenn leer, bedeutet `prior_notice_start_day=2` zwei Kalendertage im Voraus. Wenn `service_id` definiert, die nur Werktage enthält (Wochentage ohne Feiertage), bedeutet `prior_notice_start_day=2` zwei Werktage im Voraus.<br><br> **Bedingt verboten**:<br> – Optional, wenn „booking_type=2“.<br> - Andernfalls **verboten**. | 
 | „message“ | Text | Optional | Nachricht an Fahrgäste, die den Service zu einer „stop_time“ nutzen, wenn sie Abholung und Absetzen auf Abruf buchen. Soll minimale Informationen bereitstellen, die innerhalb einer Benutzeroberfläche über die Aktion übermittelt werden, die ein Fahrgast ausführen muss, um den Service zu nutzen. | 
 | „pickup_message“ | Text | Optional | Funktioniert auf die gleiche Weise wie „message“, wird aber verwendet, wenn Fahrgäste nur Abholung auf Abruf haben. | 
 | „drop_off_message“ | Text | Optional | Funktioniert auf die gleiche Weise wie „message“, wird aber verwendet, wenn Fahrgäste nur Absetzen auf Abruf haben. | 
 | „phone_number“ | Phone number | Optional | Phone number, die für die Buchungsanfrage angerufen werden muss. | 
 | „info_url“ | URL | Optional | URL mit Informationen zur Buchungsregel. | 
 | „booking_url“ | URL | Optional | URL zu einer Online-Schnittstelle oder App, wo die Buchungsanfrage gestellt werden kann. | 
 
### translations.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`table_name`, `field_name`, ` language`, `record_id`, `record_sub_id`, `field_value`) 
 
 In Regionen mit mehreren Amtssprachen haben Verkehrsbetriebe/-betreiber normalerweise sprachspezifische Namen und Webseiten. Um Fahrgäste in diesen Regionen optimal zu bedienen, ist es sinnvoll, wenn der Datensatz diese sprachabhängigen Werte enthält. 
 
 Wenn beide Referenzierungsmethoden (`record_id`, `record_sub_id`) und `field_value` verwendet werden, um denselben Wert in zwei verschiedenen Zeilen zu übersetzen, hat die mit (`record_id`, `record_sub_id`) bereitgestellte Übersetzung Vorrang. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `table_name` | Enum | **Erforderlich** | Definiert die Tabelle, die das zu übersetzende Feld enthält. Zulässige Werte sind:<br><br> - `agency<br> - `stops`<br> - `routes`<br> - `Reisen`<br> - `stop_times<br> - `pathways<br> - `Ebenen`<br> - `feed_info<br> - `attributions<br><br> Jede zu GTFS hinzugefügte Datei hat einen `table_name`-Wert, der dem Dateinamen entspricht, wie oben aufgeführt (d.h. ohne die Dateierweiterung `.txt`). | 
 | `field_name` | Text | **Erforderlich** | Name des zu übersetzenden Felds. Felder vom Typ `Text` können übersetzt werden, Felder vom Typ `URL`, `Email` und `Phone number` können auch „übersetzt“ werden, um Ressourcen in der richtigen Sprache bereitzustellen. Felder mit anderen Typen sollten nicht übersetzt werden. | 
 | `language` | Sprachcode | **Erforderlich** | Sprache der Übersetzung.<br><br> Wenn die Sprache dieselbe ist wie in „feed_info.feed_lang“, wird angenommen, dass der ursprüngliche Wert des Felds der Standardwert ist, der in Sprachen ohne spezifische Übersetzungen verwendet wird (sofern „default_lang“t anderes angibt).<hr> _Beispiel: In der Schweiz heißt eine Stadt in einem offiziell zweisprachigen Kanton offiziell „Biel/Bienne“, würde auf Französisch aber einfach „Bienne“ und auf Deutsch „Biel“ heißen._ | 
 | `translation` | Text oder URL oder Email oder Phone number | **Erforderlich** | Übersetzter Wert. | 
 | `record_id` | Ausländische ID | **Bedingt erforderlich** | Definiert den Datensatz, der dem zu übersetzenden Feld entspricht. Der Wert in `record_id` muss das erste oder einzige Feld des Primärschlüssels einer Tabelle sein, wie im Primärschlüsselattribut für jede Tabelle und unten definiert:<br><br> - `agency_id` für [agency.txt](#agencytxt)<br> - `stop_id` für [stops.txt](#stopstxt);<br> - `route_id` für [routes.txt](#routestxt);<br> - `trip_id` für [trips.txt](#tripstxt);<br> - „`trip_id`“ für [stop_times.txt](#stop_timestxt);<br> - `pathway_id für [pathways.txt](#pathwaystxt);<br> - `level_id für [levels.txt](#levelstxt);<br> - „attribution_id“ für [attributions.txt](#attributionstxt).<br><br> Felder in Tabellen, die oben nicht definiert sind, sollten nicht übersetzt werden. Allerdings fügen Hersteller manchmal zusätzliche Felder hinzu, die außerhalb der offiziellen Spezifikation liegen, und diese inoffiziellen Felder können übersetzt werden. Nachfolgend finden Sie die empfohlene Verwendung von `record_id` für diese Tabellen:<br><br> - `service_id für [calendar.txt](#calendartxt);<br> - `service_id für [calendar_dates.txt](#calendar_datestxt);<br> - `fare_id` für [fare_attributes.txt](#fare_attributestxt);<br> - `fare_id` für [fare_rules.txt](#fare_rulestxt);<br> - „`shape_id`“ für [shapes.txt](#shapestxt);<br> - „`trip_id`“ für [frequencies.txt](#frequenciestxt);<br> - „from_stop_id“ für [transfers.txt](#transferstxt).<br><br> Bedingt erforderlich:<br> - **Verboten**, wenn „table_name“ „feed_info“ ist.<br> - **Verboten**, wenn „field_value“ definiert ist.<br> - **Erforderlich**, wenn `field_value` leer ist. | 
 | `record_sub_id` | Fremd-ID | **Bedingt erforderlich** | Hilft dem Datensatz, der das zu übersetzende Feld enthält, wenn die Tabelle t eindeutige ID hat. Daher ist der Wert in `record_sub_id` die sekundäre ID der Tabelle, wie in der folgenden Tabelle definiert:<br><br> – Keine für [agency.txt](#agencytxt);<br> - Keine für [stops.txt](#stopstxt);<br> – Keine für [routes.txt](#routestxt);<br> - Keine für [trips.txt](#tripstxt);<br> - `stop_sequence` für [stop_times.txt](#stop_timestxt);<br> – Keine für [pathways.txt](#pathwaystxt);<br> – Keine für [levels.txt](#levelstxt);<br> – Keine für [attributions.txt](#attributionstxt).<br><br> Felder in Tabellen, die oben nicht definiert sind, sollten nicht übersetzt werden. Allerdings fügen Hersteller manchmal zusätzliche Felder hinzu, die außerhalb der offiziellen Spezifikation liegen, und diese inoffiziellen Felder können übersetzt werden. Nachfolgend finden Sie die empfohlene Verwendung von `record_sub_id` für diese Tabellen:<br><br> – Keine für [calendar.txt](#calendartxt);<br> - `date für [calendar_dates.txt](#calendar_datestxt);<br> – Keine für [fare_attributes.txt](#fare_attributestxt);<br> - `route_id` für [fare_rules.txt](#fare_rulestxt);<br> – Keine für [shapes.txt](#shapestxt);<br> - „`start_time`“ für [frequencies.txt](#frequenciestxt);<br> - „to_stop_id“ für [transfers.txt](#transferstxt).<br><br> Bedingt erforderlich:<br> - **Verboten**, wenn „table_name“ „feed_info“ ist.<br> - **Verboten**, wenn „field_value“ definiert ist.<br> - **Erforderlich** wenn `table_name=stop_times` und `record_id` definiert sind. | 
 | `field_value` | Text oder URL oder Email oder Phone number | **Bedingt erforderlich** | Anstatt mit `record_id` und `record_sub_id` zu definieren, welcher Datensatz übersetzt werden soll, kann dieses Feld verwendet werden, um den zu übersetzenden Wert zu definieren. Bei Verwendung wird die Übersetzung angewendet, wenn die durch `table_name` und `field_name` identifizierten Felder genau denselben Wert enthalten, der in field_value definiert ist.<br><br> Das Feld muss **genau** den in `field_value` definierten Wert haben. Wenn nur eine Teilmenge des Wertes mit `field_value` übereinstimmt, wird die Übersetzung t angewendet.<br><br> Wenn zwei Übersetzungsregeln auf denselben Datensatz zutreffen (eine mit „field_value“ und die andere mit „record_id“), hat die Regel mit „record_id“ Vorrang.<br><br> Bedingt erforderlich:<br> - **Verboten**, wenn „table_name“ „feed_info“ ist.<br> - **Verboten**, wenn „record_id“ definiert ist.<br> - **Erforderlich**, wenn „record_id“ leer ist. | 
 
### feed_info.txt 
 
 Datei: **Empfohlen** (**Erforderlich**, wenn [translations.txt](#translationstxt) angegeben wird) 
 
 Primary key (none) 
 
 Die Datei enthält Informationen über den Datensatz selbst, nicht über die Dienste, die der Datensatz beschreibt. In manchen Fällen ist der Herausgeber des Datensatzes eine andere entity als eine der Agenturen. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | „feed_publisher_name“ | Text | **Erforderlich** | Vollständiger Name der Organisation, die den Datensatz veröffentlicht. Dies kann derselbe sein wie einer der „agency.agency_name“-Werte. | 
 | `feed_publisher_url` | URL | **Erforderlich** | URL der Website der Organisation, die den Datensatz veröffentlicht. Dies kann mit einem der Werte von `agency.agency_url` identisch sein. | 
 | `feed_lang` | Sprachcode | **Erforderlich** | Standardsprache für den Text in diesem Datensatz. Diese Einstellung hilft GTFS Benutzern, Groß-/Kleinschreibungsregeln und andere sprachspezifische Einstellungen für den Datensatz auszuwählen. Die Datei `translations.txt` kann verwendet werden, wenn der Text in andere Sprachen als die Standardsprache übersetzt werden muss.<br><br> Bei Datensätzen mit mehrsprachigem Originaltext kann die Standardsprache mehrsprachig sein. In solchen Fällen sollte das Feld `feed_lang` den in der Norm ISO 639-2 definierten Sprachencode `mul` enthalten und in `translations.txt` eine Übersetzung für jede im Datensatz verwendete Sprache bereitgestellt werden. Wenn der gesamte Originaltext im Datensatz in derselben Sprache vorliegt, sollte `mul` nicht verwendet werden.<hr> _Beispiel: Betrachten Sie einen Datensatz aus einem mehrsprachigen Land wie der Schweiz, wobei das ursprüngliche Feld „stops.stop_name“ mit Haltestellennamen in verschiedenen Sprachen gefüllt ist. Jeder Haltestellenname wird entsprechend der vorherrschenden Sprache am geografischen Standort dieser Haltestelle geschrieben, z. B. „Genève“ für die französischsprachige Stadt Geneva, „Zürich“ für die deutschsprachige Stadt Zurich und „Biel/Bienne“ für die zweisprachige Stadt Biel/Bienne. Der Datensatz „feed_lang“ sollte „mul“ sein und Übersetzungen würden in „translations.txt“ bereitgestellt, auf Deutsch: „Genf“, „Zürich“ und „Biel“, auf Französisch: „Genève“, „Zurich“ und „Bienne“, auf Italienisch: „Ginevra“, „Zurigo“ und „Bienna“, und auf Englisch: „Geneva“, „Zurich“ und „Biel/Bienne“._ | 
 | „default_lang“ | Sprachcode | Optional | Definiert die Sprache, die verwendet werden soll, wenn der Datenkonsument die Sprache des Fahrers t kennt. Dies ist häufig „en“ (Englisch). | 
 | „feed_start_date“ | Datum | Empfohlen | Der Datensatz bietet vollständige und zuverlässige Fahrplaninformationen für den Zeitraum vom Beginn des „feed_start_date“-Tages bis zum Ende des „feed_end_date“-Tages. Beide Tage können leer gelassen werden, wenn sie nicht verfügbar sind. Das „feed_end_date“ date darf nicht vor dem „feed_start_date“ date liegen, wenn beide angegeben sind. Es wird empfohlen, dass Datensatzanbieter Fahrplandaten außerhalb dieses Zeitraums bereitstellen, um über wahrscheinliche zukünftige Dienste zu informieren, aber Datensatzkonsumenten sollten sich dessen nicht autoritativen Status bewusst sein. Wenn „feed_start_date“ oder „feed_end_date“ über die aktiven Kalenderdaten hinausgehen, die in [calendar.txt](#calendartxt) und [calendar_dates.txt](#calendar_datestxt) definiert sind, gibt der Datensatz explizit an, dass für Daten innerhalb des Bereichs „feed_start_date“ oder „feed_end_date“, die jedoch nicht in den aktiven Kalenderdaten enthalten sind, kein Dienst verfügbar ist. | 
 | „feed_end_date“ | Datum | Empfohlen | (siehe oben) | 
 | „feed_version“ | Text | Empfohlen | Zeichenfolge, die die aktuelle Version ihres GTFS Datensatzes angibt. GTFS-nutzende Anwendungen können diesen Wert anzeigen, um Datensatzherausgebern dabei zu helfen, festzustellen, ob der neuste Datensatz integriert wurde. | 
 | „feed_contact_email“ | Email | Optional | Email Adresse für die Kommunikation bezüglich des GTFS Datensatzes und der Datenveröffentlichungspraktiken. „feed_contact_email“ ist ein technischer Kontakt für GTFS-nutzende Anwendungen. Geben Sie die Kontaktinformationen für den Kundenservice über [agency.txt](#agencytxt) an. Es wird empfohlen, mindestens eines der folgenden Elemente anzugeben: `feed_contact_email` oder `feed_contact_url`. | 
 | `feed_contact_url` | URL | Optional | URL für Kontaktinformationen, ein Webformular, einen Supportdesk oder andere Tools für die Kommunikation in Bezug auf den GTFS Datensatz und Datenveröffentlichungspraktiken. `feed_contact_url` ist ein technischer Kontakt für GTFS-nutzende Anwendungen. Geben Sie die Kontaktinformationen für den Kundenservice über [agency.txt](#agencytxt) an. Es wird empfohlen, mindestens eines der folgenden Elemente anzugeben: `feed_contact_url` oder `feed_contact_email`. | 
 
### attributions.txt 
 
 Datei: **Optional** 
 
 Primärschlüssel (`attribution_id`) 
 
 Die Datei definiert die auf den Datensatz angewendeten attributions. 
 
 | Feldname | Typ | Vorhandensein | Beschreibung | 
 |------|------|------|------| 
 | `attribution_id` | Eindeutige ID | Optional | Identifiziert eine Attribution für den Datensatz oder eine Teilmenge davon. Dies ist vor allem für Übersetzungen nützlich. | 
 | `agency_id` | Ausländische ID, die auf `agency.agency_id` verweist | Optional | Agentur, für die die Attribution gilt.<br><br> Wenn eine Zuordnung „agency_id“, „`route_id`“ oder „`trip_id`“ definiert ist, müssen die anderen leer sein. Wird keine angegeben, gilt die Zuordnung für den gesamten Datensatz. | 
 | „`route_id`“ | Fremd-ID mit Referenz auf „routes.route_id“ | Optional | Funktioniert genauso wie „agency_id“, außer dass die Zuordnung für eine Route gilt. Für die gleiche Route können mehrere attributions gelten. | 
 | „`trip_id`“ | Fremd-ID mit Referenz auf „`trips.trip_id`“ | Optional | Funktioniert genauso wie „agency_id“, außer dass die Zuordnung für eine Reise gilt. Für die gleiche Reise können mehrere attributions gelten. | 
 | „organization_name“ | Text | **Erforderlich** | Name der Organisation, der der Datensatz zugeordnet ist. | 
 | „is_producer“ | Aufzählung | Optional | Die Rolle der Organisation ist Produzent. Gültige Optionen sind:<br><br> „0“ oder leer – Die Organisation hat diese Rolle t .<br> `1` – Die Organisation hat diese Rolle.<br><br> Mindestens eines der Felder „is_producer“, „is_operator“ oder „is_authority“ sollte auf „`1`“ gesetzt sein. | 
 | „is_operator“ | Enum | Optional | Funktioniert auf die gleiche Weise wie „is_producer“, außer dass die Rolle der Organisation „Betreiber“ ist. | 
 | „is_authority“ | Enum | Optional | Funktioniert auf die gleiche Weise wie „is_producer“, außer dass die Rolle der Organisation „Autorität“ ist. | 
 | „attribution_url“ | URL | Optional | URL der Organisation. |

 
 | `attribution_email` | Email | Optional | Email der Organisation. | 
 | `attribution_phone` | Phone number | Optional | Phone number der Organisation. | 
 

