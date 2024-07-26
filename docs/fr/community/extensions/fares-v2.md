# GTFS-Fares v2 
 
 Tarifs v2 est un projet d’extension GTFS Schedule qui vise à répondre aux limitations de [Tarifs v1](../../../documentation/schedule/examples/fares-v1/). 
 
 Les principaux concepts que Tarifs v2 prévoit de représenter sont

 - Produits tarifaires (par exemple billets et pass) 
 - Catégories de passagers (par exemple seniors et enfants) 
 - Supports tarifaires (par exemple laissez-passer de transport en commun, billets papier, cartes bancaires sans contact) 
 - Plafonnement tarifaire 
 
 Ces concepts permettront aux producteurs de données de modéliser des tarifs zonalisés, dépendants du temps et inter-agences. Ce projet d’extension est adopté par itérations. 
 
 Vous pouvez voir [exemples ici](../../../documentation/schedule/examples/fares-v2) qui montrent ce qui peut être modélisé en utilisant ce qui a été officiellement adopté dans GTFS. 
 
 Les producteurs peuvent implémenter Tarifs v2 dans le même ensemble de données avec Tarifs v1, puisqu’il n’y a pas de conflit technique entre les deux. Les consommateurs peuvent choisir quelle version utiliser indépendamment de l’autre. Avec l’adoption et l’approbation suffisante de Tarifs v2, Tarifs v1 pourrait être obsolète à l’avenir. 
 
 [Voir la proposition complète](https://share.mobilitydata.org/gtfs-fares-v2){ .md-button .md-button--primary } 
 
## Participer à la conversation 
 Vous pouvez rester date et participer aux discussions autour de Tarifs v2 en rejoignant notre Slack Chanel et les réunions récurrentes des groupes de travail. 

 [Rejoignez #gtfs-fares sur Slack](https://share.mobilitydata.org/slack){ .md-button .md-button--primary} [Voir le calendrier des réunions](https://www.eventbrite.ca/e/specifications-discussions-gtfs-fares-v2-monthly-meetings-tickets-522966225057){ .md-button .md-button--primary } [Voir les notes de réunion](https://docs.google.com/document/d/1d3g5bMXupdElCKrdv6rhFNN11mrQgEk-ibA7wdqVLTU/edit){ .md-button .md-button--primary } 
 
## Premiers adoptants 
 
 🎉 Bravo aux premiers adoptants de Tarifs v2 ! Au moins 1 producteur de données et 1 application réutilisatrice doivent s’engager à mettre en œuvre une fonctionnalité expérimentale avant qu’un vote public ne soit ouvert pour l’ajouter à la spécification officielle. Ces organisations investissent beaucoup de temps et d’énergie dans des changements expérimentaux pour s’assurer que GTFS continue d’évoluer. 
 
 - Producteurs : <a href="https://www.interline.io/" target="_blank">Interline</a>, <a href="https://www.mta.maryland.gov/developer-resources" target="_blank">Maryland Department of Transportation</a>, <a href="https://dot.ca.gov/cal-itp/cal-itp-gtfs" target="_blank">Cal-ITP</a>, <a href="https://trilliumtransit.com/" target="_blank">Trillium Solutions</a>, <a href="https://www.itoworld.com/" target="_blank">ITO World</a>, <a href="https://www.mbta.com/" target="_blank">MBTA</a>, <a href="http://www.pvta.com/" target="_blank">PVTA</a> 
 - Consommateurs : <a href="https://transitapp.com/" target="_blank">Transit</a>, <a href="https://www.apple.com/">Apple Maps</a> 
 
## Suivi des adoptions
### Actuel 

 <iframe class="airtable-embed" src="https://airtable.com/embed/shrZzYzPYao7iExlW?backgroundColor=red&viewControls=on" frameborder="0" onmousewheel="" width="100%" height="533" style="background: transparent; border: 1px solid#ccc;"></iframe> 
 
 [Demander une modification](https://airtable.com/shr8aT0K9bpncmy0V){ .md-button .md-button--primary } [Ajoutez votre organisation (consommateurs)](https://airtable.com/shr5B6Pl1r9KH9qMX){ .md-button .md-button--primary } [Ajoutez votre organisation (producteurs)](https://airtable.com/shrn0Afa3TPNkOAEh){ .md-button .md-button--primary } 
 
### Avenir

 <iframe class="airtable-embed" src="https://airtable.com/embed/shrUrgZTO1noUF66R?backgroundColor=red&viewControls=on" frameborder="0" onmousewheel="" width="100%" height="533" style="background: transparent; border: 1px solid#ccc;"></iframe> 
 
 [Ajoutez vos projets futurs](https://airtable.com/shrvnI40zuFXmDsQI){ .md-button .md-button--primary } 
 
## Tarifs v2 Fonctionnalités en discussion 
 
 <iframe src="https://portal.productboard.com/rhk8dbtic1iqakfznucry448" frameborder="0" width="100%", style="min-height:1060px;"></iframe> 
 
## Historique
- **2017** : Recherche industrielle et modélisation des données
- **Octobre 2021** : <a href="https://github.com/google/transit/pull/286#issue-1026848880" target="_blank">Implémentation de Base rédigée et partagée</a> 
- **Décembre 2021** : <a href="https://github.com/google/transit/pull/286#issuecomment-990258396" target="_blank">Vote ouvert #1 → n’a pas réussi</a> 
 - **Mars 2022** : <a href="https://github.com/google/transit/pull/286#issuecomment-1080716109" target="_blank">Vote ouvert #2 → n’a pas réussi</a> 
 - **Mai 2022** : <a href="https://github.com/google/transit/pull/286#issuecomment-1121392932" target="_blank">Vote ouvert #3 → a réussi</a> 
 - **Août 2022** : <a href="https://github.com/google/transit/issues/341" target="_blank">Début des discussions de la communauté sur la prochaine phase de Tarifs v2</a> 
 - **Novembre 2022** : <a href="https://github.com/google/transit/pull/355" target="_blank">demande d’extraction de projet de support tarifaire ouverte pour commentaires</a> 
 - **Décembre 2022** : <a href="https://github.com/google/transit/issues/341#issuecomment-1339947915" target="_blank">La communauté identifie l’ordre des fonctionnalités classées dans la pile pour prioriser les itérations</a> 
 - **Mars 2023** : <a href="https://github.com/google/transit/pull/355#issuecomment-1468326858" target="_blank">Forfaits média</a> 
 - **Juillet 2023** : <a href="https://github.com/google/transit/pull/357#issuecomment-1653561813" target="_blank">Tarifs variables selon les horaires/jours</a> 
 - **Novembre 2023** : <a href="https://github.com/google/transit/pull/405#issuecomment-1830665141" target="_blank">Fichiers dédiés à la définition des réseaux</a> 
