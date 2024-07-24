# Services réactifs à la demande 
 
 GTFS Flex est un projet d’extension GTFS qui a été officiellement adopté dans la spécification GTFS en mars 2024, ses objectifs sont de faciliter la découverte des services de transport réactifs à la demande (DRT). 
 Notez qu’il existe différents termes pour les services répondant à la demande en fonction de la région du monde. Consultez le [Glossaire](#glossaire) pour en savoir plus. 
 
 L’exemple suivant montre comment modéliser différents cas d’utilisation de services répondant à la demande à l’aide de Flex. **Veuillez noter que les exemples suivants ne constituent pas nécessairement une représentation précise ou complète des services des agences.** 
 
## Services à la demande au sein d’une seule zone 
 
 Les services à la demande peuvent fonctionner dans une zone spécifique, permettant aux passagers de réserver des prises en charge à n’importe quel point A de la zone et des déposes à n’importe quel point B de la même zone. Un exemple de ceci est le service [Heartland Express Transit](https://www.co.brown.mn.us/heartland-express-transit?view=category&amp;id=56) dans le Minnesota, aux États-Unis. 
 
 <sup>[Télécharger l’exemple de données Heartland Express](../../../assets/on-demand_services_within_a_single_zone.zip)</sup> 
 
### Définir les trajets 
 
 Les heures de service Heartland Express sont les suivantes : 
 
 - En semaine : 
 - 8h00- 17h00- 6h15- 17h45 (zone New Ulm uniquement) 
 - Dimanche : 8h00- Midi (Nouvelle zone Ulm Zone d’Ulm uniquement) 
 
 La zone de la ville de New Ulm est contenue dans la zone du comté de Brown. Pour éviter le problème de ["zone chevauchement contrainte"](#zone-overlap-constraint), Heartland Express peut être défini avec quatre trajets : 
 
 - Service dans la zone New Ulm de 6h15 à 8h00 le jours de la semaine. 
 - Service dans tout le département de 8h00 à 17h00 en semaine. 
 - Service dans la zone New Ulm de 17h00 à 17h45 en semaine. 
 - Service dans la zone New Ulm de 8h00 à 12h00 le dimanche. 
 
 [** trips.txt**](../../reference/#tripstxt) 
 
 route_id | service_id | trip_id--|--|-- 
 74362 | c_67295_b_77497_d_31 | t_5374945_b_77497_tn_0
74362 | c_67295_b_77497_d_31 | t_5374946_b_77497_tn_0
74362 | c_67295_b_77497_d_31 | t_5374944_b_77497_tn_0
74362 | c_67295_b_77497_d_64 | t_5374947_b_77497_tn_0 
 
 `service_id = c_67295_b_77497_d_31` fait référence aux jours de la semaine, `service_id = c_67295_b_77497_d_64` fait référence au dimanche. 
 
### Définir la zone (emplacements GeoJSON) 
 
 En utilisant [locations.geojson](../../reference/#locationsgeojson) pour définir la zone opérationnelle du service Heartland Express, des zones distinctes doivent être définies pour le comté de Brown et la ville de New Ulm. Ci-dessous un GeoJSON simplifié définissant la zone du Comté de Brown : 
 ```json 
 { 
 "type": "FeatureCollection", 
 "fonctionnalités": [
 { 
 "id": "area_708", 
 "type": "Feature", 
 "geometry": { 
 "type": "Polygon", 
# Simplifié, ne présentant ici que 3 coordonnées. 
 "coordonnées" : [
 [
 [
 -94.7805702, 
 44.4560958 
], 
 [
 -94.7805608, 
 44.4559928 
], 
 [
 -94.7805218, 
 44.4559649 
] 
] 
] 
 }, 
 "propriétés" : {} 
 } 
] 
 ``` 
 
### Définir les règles de réservation 
 
 Voici les réservations règles qui s’appliquent à tous les services Heartland Express : 
 
 - Les demandes de trajet doivent être effectuées entre 8h00 et 15h00 en semaine. 
 - Les courses doivent être demandées un jour ouvrable avant le jour de la course. 
 - Les demandes de courses peuvent être effectuées jusqu’à 14 jours à l’avance. 
 
 L’utilisation de `booking_type = 2` indique que le service nécessite une réservation jusqu’au(x) jour(s) précédent(s). `prior_notice_last_day = 1` et `prior_notice_start_day = 14` indiquent que le service peut être réservé dès 14 jours à l’avance et au plus tard la veille. 
 
 [** booking_rules.txt**](../../reference/#booking_rulestxt) 
 
 booking_rule_id | booking_type | prior_notice_start_day | prior_notice_start_time | prior_notice_last_day | prior_notice_last_time | message | phone_number | info_url--|--|--|--|--|--|--|--|-- 
 booking_route_74362 | 2 | 14 | 8:00:00 | 1 | 15:00:00 | Brown County Heartland Express propose un transport porte-à-porte à la demande. Pour demander un trajet, appelez le 1-507-359-2717 ou le 1-800-707-2717 avant 15 heures au moins un jour ouvrable avant votre voyage. | (507) 359-2717 | https://www.co.brown.mn.us/heartland-express-transit### Définir les horaires d’arrêts 
 
 Les heures de fonctionnement sont définies à l’aide des champs `start_pickup_drop_off_window` et `end_pickup_drop_off_window`. Les voyages dans la même zone nécessitent deux enregistrements dans stop_times.txt avec le même `location_id`. 
 
 - Le premier enregistrement avec `pickup_type = 2` et `drop_off_type = 1` indique que le ramassage des réservations est autorisé dans la zone. 
 - Le deuxième enregistrement avec `pickup_type = 1` et `drop_off_type = 2` indique que le dépôt de réservation est autorisé dans la zone. 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id--|--|--|--|--|--|--|--|--
 t_5374944_b_77497_tn_0 | zone_715 | 1 | 06:15:00 | 08:00:00 | 2 | 1 | booking_route_74362 | booking_route_74362 
 t_5374944_b_77497_tn_0 | zone_715 | 2 | 06:15:00 | 08:00:00 | 1 | 2 | booking_route_74362 | booking_route_74362 
 t_5374945_b_77497_tn_0 | zone_708 | 1 | 08:00:00 | 17:00:00 | 2 | 1 | booking_route_74362 | booking_route_74362 
 t_5374945_b_77497_tn_0 | zone_708 | 2 | 08:00:00 | 17:00:00 | 1 | 2 | booking_route_74362 | booking_route_74362 
 t_5374946_b_77497_tn_0 | zone_715 | 1 | 17:00:00 | 17:45:00 | 2 | 1 | booking_route_74362 | booking_route_74362 
 t_5374946_b_77497_tn_0 | zone_715 | 2 | 17:00:00 | 17:45:00 | 1 | 2 | booking_route_74362 | booking_route_74362 
 t_5374947_b_77497_tn_0 | zone_715 | 1 | 08:00:00 | 12:00:00 | 2 | 1 | booking_route_74362 | booking_route_74362 
 t_5374947_b_77497_tn_0 | zone_715 | 2 | 08:00:00 | 12:45:00 | 1 | 2 | booking_route_74362 | booking_route_74362 
 
 `area_715` fait référence à la zone de New Ulm City, `area_708` fait référence à la zone du comté de Brown. 
 
## Services à la demande dans plusieurs zones 
 
 Certains services à la demande fonctionnent dans plusieurs zones distinctes, où les passagers peuvent réserver des prises en charge à n’importe quel endroit A dans une zone et des retours à n’importe quel endroit dans une autre zone..Par exemple, [Minnesota River Valley Transit](https://www.saintpetermn.gov/330/Dial-a-Ride) propose des services à la demande entre les villes de Saint Peter et Kasota : 
 
 <sup>[Télécharger l’exemple de River Valley Transit dataset](../../../assets/on-demand_services_between_multiple_zones(r).zip)</sup> 
 
### Définir les trajets 
 
 Semblable à l’exemple précédent, car les heures de service varient selon les jours, il est nécessaire de définir les déplacements séparément pour les jours de semaine et les samedis. 
 
 [** trips.txt**](../../reference/#tripstxt) 
 
 route_id | service_id | trip_id--|--|-- 
 74375 | en semaine | t_5298036_b_77503_tn_0
74375 | samedi | t_5298041_b_77503_tn_0 
 
 (Définissez les règles et les zones de réservation en utilisant [booking_rules.txt](../../reference/#booking_rulestxt) et [locations.geojson](../../reference/#locationsgeojson) dans le même comme dans l’exemple précédent) 
 
### Définir les horaires d’arrêts 
 
 Les données suivantes indiquent que le ramassage n’est autorisé que dans une zone et le dépôt n’est autorisé que dans une autre zone. Les prises en charge et les retours dans la même zone ne sont pas autorisés. 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id--|--|--|--|--|--|--|--|--
 t_5298036_b_77503_tn_0 | zone_713 | 1 | 06:30:00 | 20:00:00 | 2 | 1 | booking_route_74375 | booking_route_74375 
 t_5298036_b_77503_tn_0 | zone_714 | 2 | 06:30:00 | 20:00:00 | 1 | 2 | booking_route_74375 | booking_route_74375 
 t_5298041_b_77503_tn_0 | zone_713 | 1 | 09:00:00 | 19:00:00 | 2 | 1 | booking_route_74375 | booking_route_74375 
 t_5298041_b_77503_tn_0 | zone_714 | 2 | 09:00:00 | 19:00:00 | 1 | 2 | booking_route_74375 | booking_route_74375## Services à la demande où les passagers doivent être pris en charge et déposés à des endroits spécifiques 
 
 Dans certains services à la demande, les passagers ne peuvent pas spécifier de prise en charge et de dépôt à un endroit quelconque dans une zone. Au lieu de cela, les passagers ne peuvent réserver que pour être récupérés et déposés à des arrêts spécifiques désignés (points de collecte/arrêts virtuels). Un exemple en est le [service RufBus](https://uvg-online.com/rufbus-angermuende/) à Angermünde et Gartz, Allemagne : 
 
### Définir les trajets 
 
 Offres de la route 476 sur-services à la demande entre chaque arrêt dans la région d’Angermünde. Ils exploitent deux services (un pour la semaine et l’autre pour le week-end), chacun étant associé à un seul trip_id. 
 
 [** trips.txt**](../../reference/#tripstxt) 
 
 route_id | service_id | trip_id--|--|-- 
 476 | on_demand_weekdays | 476_jours de la semaine 
 476 | on_demand_weekends | 476_weekends### Définir des groupes d’emplacements 
 
 Comme les usagers peuvent réserver des services entre chaque arrêt, pour éviter de définir toutes les combinaisons d’arrêt à arrêt dans stop_times.txt, l’approche appropriée consiste à définir ces arrêts en tant qu’emplacement groupe en utilisant location_groups.txt et location_group_stops.txt. 
 
 [** location_groups.txt**](../../reference/#location_groupstxt) 
 
 location_group_id | location_group_name--|-- 
 476_stops | par le RufBus 476 Bedientes Gebiet im Raum Angermünde 
 
 [** location_group_stops.txt**](../../reference/#location_group_stopstxt) 
 
 location_group_id | stop_id--|-- 
 476_stops | de:12073:900340004::1 
 476_stops | de:12073:900340004::2 
 476_stops | de:12073:900340004::3 
 476_stops | de:12073:900340004::4 
 476_stops | de:12073:900340100::1 
 476_stops | de:12073:900340100::2 
 476_stops |...
 
### Définir les règles de réservation 
 
 Le service de ligne 476 nécessite une réservation au moins une heure à l’avance. L’utilisation de `booking_type = 1` indique que le service nécessite une réservation jusqu’au jour même avec un préavis. Le `prior_notice_duration_min = 60` indique une obligation de réservation au moins 60 minutes à l’avance. 
 
 Il existe de légères différences entre les réservations en semaine et les réservations le week-end, des règles de réservation distinctes peuvent donc être définies pour les services en semaine et pendant les jours fériés. Plus de détails peuvent être fournis dans le champ « `message` ». Des liens vers des informations et des pages de réservation peuvent être fournis dans les champs `info_url` et `booking_url`. 
 
 [** booking_rules.txt**](../../reference/#booking_rulestxt) 
 
 booking_rule_id | booking_type | prior_notice_duration_min | message | phone_number | info_url | booking_url--|--|--|--|--|--|-- 
 flächenrufbus_angermünde_weekdays | 1 | 60 | Anmeldung esprit. 60min à venir, par an entre 08h00 et 24h00, ou en ligne pendant la montre | +49 3332 442 755 | https://uvg-online.com/rufbus-angermuende/| https://uvg.tdimo.net/bapp/#/astBuchungenView 
 flächenrufbus_angermünde_weekends | 1 | 60 | 1€ Komfortzuschlag par personne; Anmeldung esprit. 60min à venir, par an entre 08h00 et 24h00, ou en ligne pendant la montre | +49 3332 442 755 | https://uvg-online.com/rufbus-angermuende/| https://uvg.tdimo.net/bapp/#/astBuchungenView### Définir les horaires d’arrêts 
 
 La ligne 476 circule de 17h30 à 22h00 en semaine et à partir de 20h00 Du matin à 22h00 le week-end. Les heures de fonctionnement sont définies à l’aide des champs `start_pickup_drop_off_window` et `end_pickup_drop_off_window`. Les voyages au sein du même groupe de localisation nécessitent deux enregistrements dans stop_times.txt avec le même `location_group_id`. 
 
 - Le premier enregistrement avec `pickup_type = 2` et `drop_off_type = 1` indique que le retrait de la réservation est autorisé au niveau du groupe d’emplacements. 
 - Le deuxième enregistrement avec `pickup_type = 1` et `drop_off_type = 2` indique que le dépôt de réservation est autorisé au niveau du groupe d’emplacements. 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_group_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | pickup_booking_rule_id | drop_off_booking_rule_id--|--|--|--|--|--|--|--|-- 
 476_weekdays | 476_arrêts | 1 | 17:30:00 | 22:00:00 | 2 | 1 | flächenrufbus_angermünde_weekdays | flächenrufbus_angermünde_weekdays 
 476_weekdays | 476_arrêts | 2 | 17:30:00 | 22:00:00 | 1 | 2 | flächenrufbus_angermünde_weekdays | flächenrufbus_angermünde_weekdays 
 476_weekends | 476_arrêts | 1 | 08:00:00 | 22:00:00 | 2 | 1 | flächenrufbus-angermünde_weekdays | flächenrufbus_angermünde_weekends 
 476_weekends | 476_arrêts | 2 | 08:00:00 | 22:00:00 | 1 | 2 | flächenrufbus-angermünde_weekdays | flächenrufbus-angermünde_weekends## Itinéraire dévié 
 
 "Déviation d’itinéraire" fait référence aux services dans lesquels le véhicule suit un itinéraire fixe avec une séquence d’arrêts définie mais a la possibilité de s’écarter de cet itinéraire pour prendre ou déposer coureurs entre les arrêts. En règle générale, les écarts sont limités pour maintenir la ponctualité du service, et une réservation préalable est requise pour les prises en charge et les retours déviés. 
 
 Dans cet exemple, le service [Hermann Express](https://www.newulmmn.gov/553/Hermann-Express-City-Bus-Service) de New Ulm City permet aux utilisateurs d’être récupérés uniquement à des heures fixes arrêts et être déposé à tout moment dans une zone de déviation spécifique entre ces arrêts. 
 
 **L’exemple ci-dessous a été simplifié, téléchargez l’[exemple de jeu de données Hermann Express](../../../assets/deviated _drop-off _route.zip) pour plus de détails.** 
 § §### Définir les trajets 
 
 Étant donné que ce type de service implique toujours une série d’arrêts fixes et un horaire fixe, la définition des trajets est similaire aux services de bus normaux à itinéraire fixe. Cela nécessite de définir les déplacements desservis par chaque itinéraire tout au long de toutes les périodes de service pertinentes. 
 
 [** trips.txt**](../../reference/#tripstxt) 
 
 route_id | service_id | trip_id | share_id--|--|--|-- 
 74513 | c_67295_b_77497_d_31 | t_5374704_b_77497_tn_0 | p_1426044 
74513 | c_67295_b_77497_d_31 | t_5374699_b_77497_tn_0 | p_1426044 
74513 | c_67295_b_77497_d_31 | t_5374698_b_77497_tn_0 | p_1426044 
74513 | c_67295_b_77497_d_31 | t_5374697_b_77497_tn_0 | p_1426044 
...|...|...|...
 
### Définir des zones (localisation GeoJSON) 
 
 Utiliser [locations.geojson](../../reference/#locationsgeojson) pour définir des zones pour l’itinéraire dévié. En règle générale, les écarts sont limités pour maintenir le service dans les délais. Par conséquent, au fur et à mesure du déplacement du véhicule, la zone d’écart entre chaque arrêt fixe peut varier en conséquence. La zone de déviation d’itinéraire peut ressembler à l’image ci-dessous : 
 
<div class="flex-photos"> 
<img src="../../../../assets/deviated_route_zones.png" alt="zones d’itinéraire déviées"> 
</div> 
 
### Définir les horaires d’arrêts 
 
 Pour les arrêts fixes, définissez des champs tels que `arrival_time`, `departure_time` et `stop_id` d’une manière similaire aux itinéraires de bus normaux. Entre les arrêts fixes, définissez les zones où l’écart est autorisé. `pickup_type = 1` et `drop_off_type = 3` indiquent que la prise en charge déviée n’est pas autorisée (en limitant la prise en charge aux arrêts fixes uniquement) et que les passagers doivent se coordonner avec le conducteur pour être déposés dans la zone de déviation. 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | heure_arrivée | heure_depart | stop_id | location_id | stop_sequence | start_pickup_drop_off_window | end_pickup_drop_off_window | pickup_type | drop_off_type | shape_dist_traveled | pickup_booking_rule_id | drop_off_booking_rule_id--|--|--|--|--|--|--|--|--|--|--|--|-- 
 t_5374696_b_77497_tn_0 | 08:00:00 | 08:00:00 | 4149546 | | 1 | | | | | 0 | | 
 t_5374696_b_77497_tn_0 | | | | rayon_300_s_4149546_s_4149547 | 2 | 08:00:00 | 8:02:22 | 1 | 3 | | booking_route_74513 | booking_route_74513 
 t_5374696_b_77497_tn_0 | 08:02:22 | 08:02:22 | 4149547 | | 3 | | | | | 1221.627114 | | 
 t_5374696_b_77497_tn_0 | | | | rayon_300_s_4149546_s_4149548 | 4 | 08:02:22 | 8:03:00 | 1 | 3 | | booking_route_74513 | booking_route_74513 
 t_5374696_b_77497_tn_0 | 08:03:22 | 08:03:22 | 4149548 | | 5 | | | | | 1548.216356 | | 
 t_5374696_b_77497_tn_0 | | | | rayon_300_s_4149546_s_4149549 | 6 | 08:03:22 | 8:05:00 | 1 | 3 | | booking_route_74513 | booking_route_74513 
...|...|...|...|...|...|...|...|...|...|...|...|...
t_5374696_b_77497_tn_0 | 08:50:00 | 08:50:00 | 4210601 | | 35 | | | | | 23429.19558 | | 
 t_5374696_b_77497_tn_0 | 08:56:00 | 08:56:00 | 4149564 | | 36 | | | | | 25320.8471 | | 
 
## Comportement d’itinéraire### Ignorer les enregistrements d’ horaires d’arrêts intermédiaires avec les fenêtres de prise en charge/dépôt 
 
 Lorsqu’ils fournissent un itinéraire ou un temps de trajet entre l’origine et la destination, les consommateurs de données doivent ignorer les stop_times.txt.enregistrements txt pour lesquels `start_pickup_drop_off_window` et `end_pickup_drop_off_window` sont définis. Par exemple : 
 
 trip_id | location_id | stop_sequence | pickup_type | drop_off_type | start_pickup_drop_off_window | end_pickup_drop_off_window--|--|--|--|--|--|-- 
 voyageA | Zone1 | 1 | 2 | 1 | 08:00:00 | 18:00:00 
 voyageA | Zone2 | 2 | 1 | 2 | 08:00:00 | 14:00:00 
 voyageA | Zone3 | 3 | 1 | 2 | 10:00:00 | 18:00:00 
 
 Les consommateurs ne devraient pas prendre en compte la Zone2 lorsqu’ils fournissent un itinéraire ou un temps de trajet pour un trajet de la Zone1 à la Zone3. 
 
### Contrainte de chevauchement de zone 
 
 Chevauchement simultané de la géométrie locations.geojson `id`, de l’heure `start/end_pickup_drop_off_window` et `pickup_type` ou `drop_off_type` entre deux ou plusieurs enregistrements stop_times.txt avec le le même `trip_id` est interdit. 
 
 Par exemple : 
 (Où `northportland` fait référence à une zone au sein de `portland`) 
 
 **Interdit** 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_id | stop_sequence | pickup_type | drop_off_type | start_pickup_drop_off_window | end_pickup_drop_off_window--|--|--|--|--|--|-- 
 voyageA | Portland | 1 | 2 | 1 | 08:00:00 | 12:00:00 
 voyageA | Northportland | 2 | 2 | 1 | 10:00:00 | 14:00:00 
 voyageA | Vancouver | 3 | 1 | 2 | 10:00:00 | 14:00:00 
 
 **Autorisé** 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_id | stop_sequence | pickup_type | drop_off_type | start_pickup_drop_off_window | end_pickup_drop_off_window--|--|--|--|--|--|-- 
 voyageA | Portland | 1 | 2 | 1 | 08:00:00 | 12:00:00 
 voyageA | Northportland | 2 | 2 | 1 | 12:00:00 | 14:00:00 
 voyageA | Vancouver | 3 | 1 | 2 | 10:00:00 | 14:00:00 
 
 ou 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_id | stop_sequence | pickup_type | drop_off_type | start_pickup_drop_off_window | end_pickup_drop_off_window--|--|--|--|--|--|-- 
 voyageA | Portland | 1 | 2 | 1 | 08:00:00 | 12:00:00 
 voyageA | Northportland | 2 | 1 | 2 | 10:00:00 | 14:00:00 
 voyageA | Vancouver | 3 | 1 | 2 | 10:00:00 | 14:00:00 
 
 ou 
 
 [** stop_times.txt**](../../reference/#stop_timestxt) 
 
 trip_id | location_id | stop_sequence | pickup_type | drop_off_type | start_pickup_drop_off_window | end_pickup_drop_off_window--|--|--|--|--|--|-- 
 voyageA | Portland | 1 | 2 | 1 | 08:00:00 | 12:00:00 
 voyageA | Gresham | 2 | 2 | 1 | 10:00:00 | 14:00:00 
 voyageA | Vancouver | 3 | 1 | 2 | 10:00:00 | 14:00:00## Glossaire 
 
 📲 Dial-a-ride est une variante de plusieurs termes utilisés dans toute l’Europe. 
 
 🇨🇭 En Suisse, cela relèverait du terme Rufbus/On-call bus. Il y a aussi la disponibilité du [système PubliCar de CarPostal](https://www.postauto.ch/fr/timetable-and-network/publicar). Dans le cadre de cette proposition, l’application et le service PubliCar seraient visibles dans l’application de planification de voyage préférée de l’utilisateur. 
 
 🇦🇹 En Autriche, le service de transport à distance serait également Rufbus et sous l’égide plus large de Bedarfsverkehr (Transport à réponse à la demande) et Mikro-ÖV (Microtransit). 
 
 - [bedarfsverkehr.at](https://www.bedarfsverkehr.at/) 
 - [Wiener Linien](https://www.wienerlinien.at/documents/843721/4770179/Anleitung_Rufbus_359531.pdf/df430b95-9dd4-0d13-ffdf-bdace15932a8?t=1614165175643) 
 - Rufbus (anglais : dial-a-bus, anciennement Anruf-Sammel-Taxi ou ASTAX call-collect-taxi) 
 - Implémentation actuelle de GTFS [en tant que alerte de service d’un an](https://www.google.com/maps/dir/S%C3%BC%C3%9Fenbrunner+Pl.,+1220+Wien,+Austria/2201+Gerasdorf,+Austria/@ 48.2867283,16.4429959,13z/am=t/data=!4m15!4m14!1m5!1m1!1s0x476d0393b15bc6d9:0x517f69839511fb31!2m2!1d16.4958186!2d48.2772635!1 m5!1m1!1s0x476d0488292e6f61:0xeee80d3d2bb6b1f5!2m2!1d16.4690073!2d48 .2962096!3e3!5i1?entry=ttu ) 
 
 🇩🇰 Au Danemark, on peut faire référence à NT/midttrafik/sydtrafik/FYNBUS/movia (https://flextur.dk/) 
 
 - flextur (anglais : flex trip) 
 - anciennement flextrafik (anglais : flex transit) 
 
 🇫🇷 ⚠️ En France les termes TDA (Transport à la Demande) et PMR (Personnes à Mobilité Réduite) pour les services de Transport adapté 
 
 - [Réseau Mistral](https://www.reseaumistral.com/services/service-appel-bus) 
 - Appel bus (anglais : call bus) 
 
 🇩🇪 En Allemagne, on l’appelle On- Demand-Angebot, Flexible Fahrt et AST- [BVG](https://www.bvg.de/de/verbindungen/bvg-muva/flexible-fahrt) 
 - Marque : Muva- On- Demand-Angebot (anglais : on-demand-service) 
 - Flexible Fahrt (anglais : trajet flexible) 
 - Autres zones- Anruf-sammel-taxi ou AST (anglais : call-collect-taxi) 
 § § 🇫🇷 Au Royaume-Uni, il existe le service suivant : 
 
 - [go2 Sevenoaks](https://www.go-coach.co.uk/go2/) 
 - Service à la demande 
 
 La terminologie varie d’un pays à l’autre, mais en général, nous pouvons supposer que le service de numérotation est tout service répondant à la demande qui nécessite une certaine forme de contact du passager avec l’opérateur. 
<hr> 
