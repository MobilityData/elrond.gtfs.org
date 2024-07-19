# Fonctionnalités du calendrier GTFS 
 
 À mesure que le format de référence GTFS évolue pour répondre aux besoins actuels des systèmes de transport en commun, ses fonctions peuvent devenir de plus en plus complexes. Les **Fonctionnalités GTFS** sont destinées à fournir une explication claire et définitive des fonctionnalités activées par le format de référence GTFS. Cela aide les agences de transport en commun, les vendeurs, les consommateurs et les chercheurs à comprendre les capacités de GTFS et à répondre à la question : **Que puis-je faire avec GTFS ?** 
 
 Les groupes de fonctionnalités suivants expliquent l’objectif de chaque fonctionnalité ainsi que le les fichiers et les champs qui leur sont associés, aidant les utilisateurs à comprendre quelles données sont nécessaires pour prendre en charge une fonctionnalité spécifique. 
 
## Base 
 Ces fonctionnalités essentielles constituent le cœur d’un flux GTFS. Ce sont les éléments minimaux nécessaires pour représenter un service de transport en commun. 

<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agence__ 
 
 Communiquer des détails sur les agences responsables du service de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#agency) 
 
 - :material-subway-variant:{ .lg.middle } __Arrêts__ 
 
 Définir les endroits où un service de transport en commun prend et dépose les passagers. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#stops) 
 
 - :material-subway-variant:{ .lg.middle } __Lignes__ 
 
 Définir les éléments d’un itinéraire de transit tels que le nom et le type de service. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#routes) 
 
 - :material-subway-variant:{ .lg.middle } __Dates de service__ 
 
 Créez la structure pour planifier les déplacements et les exemptions de service. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trajets__ 
 § § Représente les véhicules de transport en commun circulant le long d’un itinéraire défini à des heures programmées. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Horaires d’arrêt__ 
 
 Définissez les heures d’arrivée et de départ de chaque trajet pour chaque arrêt. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base/#stop-times) 
 
</div> 
 
## Modules Complémentaires à Base 
 Ces fonctionnalités améliorent un ensemble de données GTFS, améliorant l’expérience du passager et facilitant la collaboration entre les agences, les fournisseurs et les réutilisateurs de données. Elles peuvent impliquer l’ajout de nouveaux champs aux fichiers existants ou la création de nouveaux fichiers. 

<div class="grid cards" markdown> 
 
 - :material-plus-box-multiple-outline:{ .lg.middle } __Informations sur le Flux__ 
 
 Communiquer des informations importantes sur le flux lui-même. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#feed-information) 
 
 - :material-plus-box-multiple-outline:{ .lg.milieu } __Tracé des lignes__ 
 
 Définir le trajet géographique suivi par un véhicule au cours d’un trajet. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#shapes) 
 
 - :material-plus-box-multiple-outline :{ .lg.middle } __Couleurs des lignes__ 
 
 Décrivez et communiquez avec précision la palette de couleurs attribuée à des itinéraires spécifiques. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#route-colors) 
 
 - :material-plus-box-multiple-outline:{ .lg.milieu } __Vélo Autorisé__ 
 
 Communiquer si les véhicules peuvent accueillir des vélos ou non. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#bike-allowed) 
 
 - :material-plus-box-multiple-outline:{ .lg.milieu } __Girouette__ 
 
 Communiquer la signalisation utilisée par les véhicules indiquant la destination du voyage. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#headsigns) 
 
 - :material-plus-box-multiple-outline :{ .lg.middle } __Types d’emplacement__ 
 
 Classez les zones clés dans les gares de transport en commun telles que les entrées et les sorties. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#location-types) 
 
 - :material-plus-box-multiple-outline:{ .lg.milieu } __Fréquences__ 
 
 Représentent les services qui fonctionnent sur une fréquence régulière ou des intervalles spécifiques. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/# Frequency-based-service) 
 
 - :material-plus-box-multiple-outline:{. lg.middle } __Transferts__ 
 
 Décrire les transferts autorisés entre différents services de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#transfers) 
 
 - :material-plus-box-multiple-outline :{ .lg.middle } __Traductions__ 
 
 Communiquer des informations de service dans plusieurs langues. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#translations) 
 
 - :material-plus-box-multiple-outline :{ .lg.middle } __Attributions__ 
 
 Indiquer qui a été impliqué dans la création de l’ensemble de données. 
 
 [:octicons-arrow-right-24 : En savoir plus](../base_add-ons/#attributions) 
 
</div> 
 
 
## Accessibilité 
 Les fonctionnalités Accessibilité fournissent des informations essentielles permettant aux personnes handicapées d’accéder au service. 

<div class="grid cards" markdown> 
 
 - :material-wheelchair:{ .lg.middle } __Arrêts Accessibilité en fauteuil roulant__ 
 
 Indiquez si l’embarquement en fauteuil roulant est possible à partir d’un endroit. 
 
 [:octicons-arrow-right-24 : En savoir plus](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-wheelchair:{ .lg.middle } __Trips Accessibilité en fauteuil roulant__ § § 
 Indiquer si un véhicule peut accueillir des passagers en fauteuil roulant. 
 
 [:octicons-arrow-right-24 : En savoir plus](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-wheelchair:{ .lg.middle } __Synthèse Vocale__ 
 
 Fournissez les entrées nécessaires pour convertir le texte des noms d’arrêt en audio. 
 
 [:octicons-arrow-right-24 : En savoir plus](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Tarifs 
 GTFS peut modéliser diverses structures tarifaires, telles que les tarifs basés sur la zone, la distance ou l’heure de la journée. Il informe les voyageurs des prix des trajets et des modes de paiement. 

<div class="grid cards" markdown> 
 
 - :material-cash:{ .lg.middle } __Produits tarifaires__ 
 
 Définir la liste des billets ou des types de tarifs disponibles pour les utilisateurs. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fare-products) 
 
 - :material-cash:{ .lg.middle } __Tarif Média__ 
 
 Définir les supports pouvant être utilisés pour détenir et/ou valider un produit tarifaire. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fare-media) 
 
 - :material-cash:{ .lg.middle } __Tarifs Basés sur l’Itinéraire__ 
 
 Décrire les règles utilisées pour appliquer différents tarifs pour des groupes spécifiques d’itinéraires. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#route-based-fares) 
 
 - :material-cash:{ .lg.middle } __Tarifs Basés sur le Temps__ 
 
 Décrire les tarifs différenciés selon l’heure de la journée ou le jour de la semaine. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#time-based-fares) 
 
 - :material-cash:{ .lg.middle } __Tarifs Basés sur les Zones__ 
 
 Décrire les tarifs différenciés lors des déplacements d’une zone à une autre. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#zone-based-fares) 
 
 - :material-cash:{ .lg.middle } __Tarifs Transferts__ 
 
 Définir les frais applicables lors du transfert d’une étape du voyage à une autre. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fares-transfers) 
 
 - :material-cash:{ .lg.middle } __Tarifs V1__ 
 
 Fonctionnalité héritée qui permet une représentation plus simple des informations tarifaires. 
 
 [:octicons-arrow-right-24 : En savoir plus](../fares/#fares-v1) 
 
</div> 
 
 
## Parcours 
 
 Les fonctionnalités de Parcours permettent de modéliser de grandes gares de transport en commun, afin que les usagers soient guidés depuis les entrées jusqu’aux zones d’embarquement. Ils fournissent des détails sur le chemin, les temps de navigation estimés et les systèmes d’orientation. 

<div class="grid cards" markdown> 
 
 - :material-escalator:{ .lg.middle } __Connexions du Parcours__ 
 
 Modélisez des chemins reliant les points pertinents dans une station de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#pathway-connections) 
 
 - :material-escalator:{ .lg.middle } __Détails du Parcours__ 
 
 Fournir des détails supplémentaires concernant les caractéristiques physiques d’un parcours. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#pathway-details) 
 
 - :material-escalator:{ .lg.middle } __Niveaux__ 
 
 Décrire et répertoriez tous les différents niveaux d’une station de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#levels) 
 
 - :material-escalator:{ .lg.middle } __In-Station Traversal Time__ 
 § § Communiquer le temps estimé pour parcourir les chemins dans une station de transport en commun. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#in-station-traversal-time) 
 
 - :material-escalator:{ .lg.middle } __Signalisation du Parcours__ 
 
 Communiquer la signalétique en station associée à un parcours. 
 
 [:octicons-arrow-right-24 : En savoir plus](../pathways/#pathway-signs) 
 
</div> 
 
## Services flexibles 
 Services flexibles, ou services répondant à la demande, qui ne suivent pas d’horaires réguliers ni d’itinéraires fixes. 

<div class="grid cards" markdown> 
 
 - :material-transit-detour:{ .lg.middle } __Arrêts Continus__ 
 
 Indiquer si un utilisateur·rice peut être pris en charge et/ou déposé entre les arrêts. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#continuous-stops) 
 
 - :material-transit-detour:{ .lg.middle } __Règles de réservation__ 
 
 Indiquer si les utilisateurs peuvent réserver un voyage sur un service à la demande. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#booking-rules) 
 
 - :material-transit-detour:{ .lg.middle } Lignes prédéfinis avec déviation__ 
 
 Véhicules pouvant s’écarter brièvement d’un itinéraire pour être pris en charge ou déposé. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-transit-detour :{ .lg.middle } __Services à la Demande Basés sur les Zones__ 
 
 Services qui permettent la prise en charge/le dépôt à n’importe quel endroit dans une zone spécifique. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-transit-detour:{ .lg.milieu } __Services à la Demande avec Arrêts Fixes__ 
 
 Services qui permettent de prendre en charge/déposer à n’importe quel endroit au sein d’un groupe d’arrêts. 
 
 [:octicons-arrow-right-24 : En savoir plus](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
