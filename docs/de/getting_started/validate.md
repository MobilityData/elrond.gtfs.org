# Bewerten Sie die Qualität Ihres GTFS Feeds 
 
 Ein qualitativ hochwertiges GTFS ist vollständig, genau und aktuell. Das heißt, es stellt dar, wie die Dienste derzeit betrieben werden, und bietet möglichst viele Informationen. 
 
## Vollständige Daten 
 
 Qualitativ hochwertiges GTFS enthält wichtige Servicedetails wie Fahrplanänderungen an Feiertagen und im Sommer, genaue Haltestellenstandorte und routes und Hinweisschilder, die mit anderen Materialien für Fahrgäste übereinstimmen. Auch wenn eine agency zur Erstellung von GTFS mit einem Anbieter zusammenarbeitet, muss die agency letztendlich sicherstellen, dass die in gedruckter Form, an Bord und online präsentierten Informationen einheitlich sind. 
 
## Genaue Daten 
 
 Genaue Daten sind unverzichtbar, um Fahrgästen ein zuverlässiges und benutzerfreundliches Transport-Erlebnis zu bieten. Fehler in den Daten können die Nutzbarkeit eines Teils oder des gesamten Datensatzes verhindern. 
 
## Aktuelle Daten 
 
 Veraltete Daten können problematischer sein, als gar keinen Feed zur Verfügung zu haben. Es reicht nicht, einfach nur Informationen zu veröffentlichen – sie müssen dem entsprechen, was der Fahrgast sieht und erlebt. Einige der größten Verkehrsbetriebe aktualisieren ihr GTFS wöchentlich oder sogar täglich, aber die meisten Betriebe müssen ihr GTFS alle paar Monate oder ein paar Mal im Jahr aktualisieren, wenn sich das Angebot ändert. Dazu gehören Dinge wie neue routes oder stops, Fahrplanänderungen oder Aktualisierungen der Tarifstruktur. 
 
 Viele Betriebe beauftragen einen Anbieter mit der Erstellung und Verwaltung ihres GTFS. Einige Anbieter fragen möglicherweise proaktiv nach Serviceänderungen, es ist jedoch wichtig, dass die Betriebe mit den Anbietern über bevorstehende Serviceänderungen kommunizieren. Es ist möglich, GTFS mit Serviceänderungen im Voraus zu veröffentlichen und so sicherzustellen, dass die Umstellung für alle reibungslos verläuft – Betriebe, Anbieter, Reiseplaner und Fahrgäste! 
 
## Verwendung offizieller Validatoren 
 
 Offizielle GTFS Validatoren bewerten die Qualität eines Datensatzes anhand der offiziellen Spezifikation und sorgen so für ein einheitliches Verständnis innerhalb der Branche, was einen qualitativ hochwertigen Datensatz ausmacht. 
 
 Der kostenlose und quelloffene [Canonical GTFS Schedule Validator](https://gtfs-validator.mobilitydata.org/)[^1], der von [MobilityData](https://mobilitydata.org/) gepflegt wird, stellt sicher, dass Ihre GTFS Daten mit der offiziellen [GTFS Schedule Reference](../../documentation/schedule/reference/) und [Best Practices](../../documentation/schedule/schedule_best_practices) kompatibel sind. Er bietet einen benutzerfreundlichen Bericht, der mit anderen Parteien geteilt werden kann, sowie eine umfassende Dokumentation. 
 
<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li> Gehen Sie zu <a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a> .</li> 
<li> Laden Sie Ihren GTFS Datensatz: Sie können eine ZIP-Datei auswählen oder per Drag &amp; Drop verschieben oder eine URL kopieren/einfügen.</li> 
<li> Wenn die Validierung abgeschlossen ist, wird eine Option zum Öffnen des Berichts bereitgestellt.</li> 
<li> Sie sehen, ob der Validator Probleme mit den Daten gefunden hat, und erhalten Links zu unserer Dokumentation, wie diese behoben werden können. Die URL des Validierungsberichts ist 30 Tage lang gültig und kann mit anderen geteilt werden.</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 Ebenso stellt die Verwendung des kostenlosen und quelloffenen [GTFS Realtime Validator](https:) sicher, dass Ihre GTFS Daten mit der offiziellen [GTFS Realtime Reference](../../documentation/realtime/reference/) und den [Best Practices](../../documentation/realtime/realtime_best_practices) kompatibel sind. 
 
 Informationen zum Erstellen qualitativ hochwertiger Daten finden Sie in den [California Transit Data Guidelines](https:), den [GTFS Schedule Best Practices](../../documentation/schedule/schedule_best_practices) und den [GTFS Realtime Best Practices](../../documentation/realtime/realtime_best_practices). 
 
 [^1]: Weitere Anweisungen zur Verwendung dieses Tools in Ihrer Datenpipeline und zur Mitwirkung an diesem Projekt finden Sie im [GitHub-Repository](https:). 
 

