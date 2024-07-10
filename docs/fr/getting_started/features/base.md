# Base 
 Les fonctionnalités suivantes fournissent les éléments les plus basiques et essentiels dont un GTFS a besoin pour représenter un service de transit. Un GTFS se compose d’ routes, chacun avec des trajets associés. Ces voyages visitent un ou plusieurs stops à des heures précises. Les voyages ne contiennent que des informations sur l’heure et les jours pendant lesquels ils fonctionnent sont déterminés par des calendriers. 
 Toutes ces fonctionnalités doit être implémentées ensemble pour permettre un flux GTFS fonctionnel. 
 
## Agence 
 
 Les agences contiennent des informations de base sur les agences responsables du service de transport en commun, telles que leur nom, URL de leur site Web, ainsi que la langue et le fuseau horaire dans lesquels le service fonctionne. Cela permet de faire correspondre des services spécifiques avec leur agency correspondante. 
 
 | Fichiers inclus | Champs inclus | 
 |------------------------|-------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url`, `agency_email` | 
 
 **Prérequis** : 
 
 - Toutes les autres fonctionnalités de la Base 
 
 ??? remarque "Exemples de données" 
 
<p style="font-size:16px"> 
</p> 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 
 
 | agency_id | agency_name | agency_url | agency_timezone | agency_lang | agency_phone | agency_fare_url | agency_email | 
 |-----------|-------------|---------------------------------|-----------|-------------|----------------|----------------------------------|------------------------| 
 | tuberculose | Autobus de transport en commun | https://www.transitbus.org | America/Los_Angeles | FR | (777) 555-7777 | https://www.transitbus.org/fares | contact@transitbus.org | 
 
 
 
## Arrêts 
 
 Les arrêts représentent les éléments de base utilisés pour identifier l’endroit où un service de transport en commun prend et dépose les passagers. Cela peut être une station de métro ou un arrêt de bus. Chaque arrêt possède, entre autres attributs, des coordonnées géographiques permettant de localiser son emplacement sur une carte et un nom qui correspond au matériel destiné aux usagers de l’agence. Les arrêts sont associés aux trajets à l’aide des heures d’arrêt. 
 Avec GTFS, il est également possible de décrire l’intérieur de gares plus grandes, comme une gare ferroviaire ou un dépôt de bus, en utilisant [Pathways](/getting_started/features/pathways). 
 
 | Fichiers inclus | Champs inclus | 
 |------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`, `stop_code`, `stop_name`, `stop_desc`, `stop_lat`, `stop_lon`, `stop_url`, `stop_timezone`, `platform_code` | 
 
 **Prérequis** : 
 
 - Toutes les autres fonctionnalités de la Base 
 
 ??? remarque "Exemples de données" 
 
<p style="font-size:16px"> 

</p> 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_code | stop_desc | stop_name | stop_lat | stop_lon | stop_url | stop_timezone | platform_code | 
 |---------|-----------|------------------------------------------------------|------------|-----------|------------|---------------------------------------------|---------------|--------------------| 
 | TAS001 | TAS001 | Coin sud-ouest de la 5e Avenue et de la 53e rue | 5 Av/53 Rue | 45.503568 |-73.587079 | https://www.transitbus.org/stops/TAS001 | | | 
 
 
## Itinéraires 
 
 Un itinéraire est un groupe de voyages sous la même marque qui sont présentés aux passagers comme un service unique. Chaque itinéraire possède, entre autres attributs, un nom qui correspond au matériel destiné aux usagers de l’agence et au type de service représenté (comme un bus, un métro, un ferry, etc.). 
 
 | Fichiers inclus | Champs inclus | 
 |------------------------|-------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`, `agency_id`, `route_desc`, `route_type`, `route_url`, `route_sort_order`, `route_short_name`, `route_long_name`| 
 
 **Prérequis** : 
 
 - Toutes les autres fonctionnalités de la Base 
 
 ??? remarque "Exemples de données" 
 
<p style="font-size:16px"> 
 L’exemple suivant définit un itinéraire de bus (`route_type=3`). 
</p> 
 !!! note "" 
<p style="font-size:16px"> <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |----------|-----------|------------------|------------------------|---------------------------------------------|------------|-------------------------------------------|------------------| 
 | RA | tuberculose | 17 | Mission- Centre-ville | L’itinéraire « A » relie Lower Mission au centre-ville. | 3 | https://www.transitbus.org/routes/ra | 12 | 
 
 
## Dates de service 
 
 Les dates de service indiquent la plage de dates auxquelles un service est exécuté, ainsi que la création d’exemptions de service telles que les jours fériés et autres services spéciaux à des dates spécifiques. 
 Il fonctionne en définissant une date de début et une date de fin dans `calendriers.txt`, puis un marqueur pour chaque jour de la semaine sur lequel il fonctionne. Si des changements de planification d’un seul jour se produisent pendant cette période, le fichier « `calendar_dates.txt` » peut être utilisé pour remplacer le calendrier de chacun de ces jours. 
 
 | Fichiers inclus | Champs inclus | 
 |------------------------|-------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **Prérequis** : 
 
 - Toutes les autres fonctionnalités de la Base 
 
 ??? remarque "Exemples de données" 
 
<p style="font-size:16px"> 
 L’exemple suivant définit deux services (en semaine et en week-end) pour le mois de juillet 2024, dont un service spécial jours fériés le 4 juillet, fonctionnant comme un service de week-end. 
</p> 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 
 
 | service_id | monday | tuesday | wednesday | thursday | friday | saturday | sunday | start_date | end_date | 
 |------------|--------|--------------|-----------|----------|--------|----------|--------|------------|----------| 
 | NOUS | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | DEO | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 
 
 | service_id | date | exception_type | 
 |------------|----------|----------------| 
 | DEO | 20240704 | 2 | 
 | NOUS | 20240704 | 1 | 
 
## Trips 
 
 Trips regroupe les itinéraires et les dates de service pour créer des trajets pouvant être effectués par les passagers. Les trajets sont associés aux arrêts à l’aide des heures d’arrêt. 
 
 | Fichiers inclus | Champs inclus | 
 |------------------------|-------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **Prérequis** : 
 
 - Toutes les autres fonctionnalités de la Base 
 
 ??? remarque "Exemples de données" 
 
<p style="font-size:16px"> 
 L’exemple suivant définit deux trajets dans les deux sens pour l’itinéraire RA. 
</p> 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |--------------|------------|---------|-----------------|--------------|--------------| 
 | RA | NOUS | AWE1 | 3885 | 0 | 1 | 
 | RA | NOUS | AWE2 | 3887 | 1 | 2 | 
 
## Heures d’arrêt 
 
 Les heures d’arrêt sont utilisées pour représenter les heures arrival et de departure des arrêts individuels pour chaque trajet, permettant aux usagers de savoir précisément à quelle heure le bus, le train ou le ferry arrive et part d’un endroit spécifique..Le fichier « `stop_times.txt` » est généralement le plus volumineux d’un flux GTFS. 
 Certains services fonctionnent à une fréquence régulière (par exemple une ligne de métro qui circule toutes les 5 minutes) plutôt que d’avoir des heures arrival et de departure spécifiques. Cela peut être modélisé à l’aide de [Frequency-based services](../base_add-ons/# Frequency-based-service), et cela peut être modélisé en conjonction avec `stop_times.txt`. 
 
 | Fichiers inclus | Champs inclus | 
 |------------------------|-------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`, `arrival_time`, `departure_time`, `stop_id`, `stop_sequence`, `pickup_type`, `drop_off_type`, `timepoint` | 
 
 **Prérequis** : 
 
 - Toutes les autres fonctionnalités de la Base 
 
 ??? remarque "Exemples de données" 
 
<p style="font-size:16px"> 
 L’exemple suivant définit l’horaire d’un trajet à 5 stops. 
</p> 
 !!! note "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | pickup_type | drop_off_type | timepoint | 
 |---------|--------------|----------------|---------|---------------|-------------|---------------|---------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 0 | 0 | 1 | 
 

