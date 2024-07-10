# Fonctionnalités du GTFS Schedule 
 
 À mesure que le format de référence GTFS évolue pour répondre aux besoins actuels des systèmes de transport en commun, ses fonctions peuvent devenir de plus en plus complexes. Les **Fonctionnalités GTFS ** sont destinées à fournir une explication claire et définitive des fonctionnalités activées par le format de référence GTFS. Cela aide les agences de transport en commun, les vendeurs, les consommateurs et les chercheurs à comprendre les capacités de GTFS et à répondre à la question : **Que puis-je faire avec GTFS?** 
 
 Les groupes de fonctionnalités suivants expliquent l’objectif de chaque fonctionnalité ainsi que le les fichiers et les champs qui leur sont associés, aidant les utilisateurs à comprendre quelles données sont nécessaires pour prendre en charge une fonctionnalité spécifique. 
 
## Base 
 Ces fonctionnalités essentielles constituent le cœur d’un flux GTFS. Ce sont les éléments minimaux nécessaires pour représenter un service de transport en commun. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 Communiquer des détails sur les agences responsables du service de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Stops__ 
 
 Définir les endroits où un service de transport en commun prend et dépose les passagers. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Routes__ 
 
 Définir les éléments d’un itinéraire de transit tels que le nom et le type de service. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __Dates de service__ 
 
 Créez la structure pour planifier les déplacements et les exemptions de service. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trips__ 
 § § Représente les véhicules de transport en commun circulant le long d’un itinéraire défini à des heures programmées. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Horaires d’arrêt__ 
 
 Définissez les heures arrival et de departure de chaque trajet pour chaque arrêt. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#stop-times) 
 
</div> 
 
## Modules complémentaires de base 
 Ces fonctionnalités améliorent un ensemble de données GTFS, améliorant l’expérience du passager et facilitant la collaboration entre les agences, les fournisseurs et les réutilisateurs de données. Elles peut impliquer l’ajout de nouveaux champs aux fichiers existants ou la création de nouveaux fichiers. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Feed Information__ 
 
 Communiquer des informations importantes sur le flux lui-même. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ § § 
 Définir le trajet géographique suivi par un vehicle au cours d’un trajet. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __Route Colors__ 
 
 Décrire et communiquer avec précision la palette de couleurs attribuée à des routes spécifiques. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __Vélo autorisé__ 
 
 Communiquer si les véhicules peuvent accueillir des vélos ou non. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 Communiquer la signalisation utilisée par les véhicules indiquant la destination du voyage. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __Types d’emplacement__ 
 
 Classer les zones clés dans les gares de transport en commun telles que les entrées et les sorties. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Fréquences__ § § 
 Représentent les services qui fonctionnent sur une fréquence régulière ou des avancées spécifiques. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/# Frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __Transferts__ 
 
 Décrire les transfers autorisés entre différents services de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Traductions__ 
 § § Communiquer des informations de service dans plusieurs langues. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Attributions__ 
 § § Communiquer qui a été impliqué dans la création de l’ensemble de données. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/# attributions) 
 
</div> 
 
 
## Accessibilité 
 Les fonctionnalités d’accessibilité fournissent des informations essentielles permettant aux personnes handicapées d’accéder au service. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Arrêts accessibles aux fauteuils roulants__ 
 
 Indiquez si l’embarquement en fauteuil roulant est possible à partir d’un endroit. 
 
 [:octicons-arrow-right-24 : En savoir plus](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Trips Fauteuil roulant Accessibilité__ 
 
 Indiquer si un vehicle peut accueillir des passagers en fauteuil roulant. 
 
 [:octicons-arrow-right-24 : En savoir plus](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Text- to-Speech__ 
 
 Fournissez les entrées nécessaires pour convertir le texte des noms d’arrêt en audio. 
 
 [:octicons-arrow-right-24 : En savoir plus](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Tarifs 
 GTFS peut modéliser diverses structures tarifaires, telles que les tarifs basés sur la zone, la distance ou l’heure de la journée. Il informe les voyageurs des prix des trajets et des modes de paiement. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Fare Products__ 
 
 Définir la liste des billets ou des types de tarifs disponibles pour les utilisateurs. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ 
 
 Définir les supports pouvant être utilisés pour détenir et/ou valider un produit tarifaire. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __Tarifs basés sur l’itinéraire__ 
 
 Décrire les règles utilisées pour appliquer différents tarifs pour des groupes spécifiques d’ routes. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Time- Tarifs basés__ 
 
 Décrire les tarifs différenciés selon l’heure de la journée ou le jour de la semaine. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone- Tarifs basés__ 
 
 Décrire les tarifs différenciés lorsque vous voyagez d’une zone à une autre. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Tarifs Transferts__ 
 
 Définir les frais applicables lors du transfert d’une étape du voyage à une autre. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 Fonctionnalité héritée qui permet une représentation plus simple des informations tarifaires. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fares-v1) 
 
</div> 
 
 
## Pathways 
 
 Les fonctionnalités de Pathways permettent de modéliser de grandes gares de transport en commun, afin que les usagers soient guidés depuis les entrées jusqu’aux zones d’embarquement. Ils fournissent des détails sur le chemin, les temps de navigation estimés et les systèmes d’orientation. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Pathway Connections__ 
 
 Modélisez des chemins reliant des points pertinents dans une station de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __Détails du chemin__ 
 
 Fournir des détails supplémentaires concernant les caractéristiques physiques d’un parcours. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Levels__ 
 § § Décrire et énumérer tous les différents niveaux d’une station de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __In-Station Traversal Time__ § § 
 Communiquer le temps estimé pour parcourir les chemins dans une station de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __Panneaux de chemin__ 
 
 Communiquer la signalisation en station associée à un chemin. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#pathway-signs) 
 
</div> 
 
## Services flexibles 
 Services flexibles, ou services répondant à la demande, qui ne suivent pas d’horaires réguliers ni routes fixes. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Continuous Stops__ 
 
 Indique si un utilisateur·rice peut être pris en charge et/ou déposé entre les stops. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __Règles de réservation__ 
 
 Indiquer si les utilisateurs peuvent réserver un voyage sur un service à la demande. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __Itinéraires prédéfinis avec déviation__ 
 
 Véhicules pouvant s’écarter brièvement d’un itinéraire pour être pris en charge ou déposé. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __Services sensibles à la demande basés sur la zone__ 
 
 Services permettant la prise en charge/le dépôt à n’importe quel endroit dans une zone spécifique. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.milieu } __Services adaptés à la demande aux arrêts fixes__ 
 
 Services qui permettent de prendre/déposer à n’importe quel endroit au sein d’un groupe d’ stops. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

