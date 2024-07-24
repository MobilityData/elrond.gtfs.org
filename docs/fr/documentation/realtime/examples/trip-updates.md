# Trip Update 
 
 L’exemple suivant est une représentation ASCII d’un flux Trip Update complet. 
 
 ```python#informations d’en-tête 
 en-tête { 
# version de la spécification de vitesse. Actuellement "2.0". Les versions valides sont "2.0", "1.0". 
 gtfs_realtime_version : "2.0" 
# détermine si l’ensemble de données est incrémentiel ou complet 
 incrémentalité : FULL_DATASET#le moment où cet ensemble de données a été généré sur le serveur 
 horodatage : 1284457468 
 } 
 
# plusieurs entités peuvent être inclus dans le flux 
 entité { 
# identifiant unique de l’entité 
 id : "simple-trip" 
 
# "type" de l’entité 
 trip_update { 
 trip { 
# sélectionne lequel L’entité GTFS (voyage) sera affectée 
 trip_id: "trip-1" 
 } 
# mise à jour des informations du planning 
 stop_time_update { 
# sélection de l’arrêt concerné 
 stop_sequence: 3#pour l’arrivée du véhicule heure 
 arrivée { 
# à retarder de 5 secondes 
 retard : 5 
 } 
 } 
#...le retard de ce véhicule se propage à ses arrêts suivants. 
 
# Prochaine mise à jour des informations sur l’horaire du véhicule 
 stop_time_update { 
# sélectionné par stop_sequence. Il mettra à jour 
 stop_sequence: 8#l’heure d’arrivée initiale (prévue) du véhicule avec un 
 arrivée { 
# 1 seconde de retard. 
 retard : 1 
 } 
 } 
#...de même le retard se propage aux arrêts suivants. 
 
# Prochaine mise à jour des informations sur l’horaire du véhicule 
 stop_time_update { 
# sélectionné par stop_sequence. Il mettra à jour l’heure d’arrivée du véhicule 
 stop_sequence: 10#avec le délai par défaut de 0 (à l’heure) et propagera cette mise à jour#pour le reste des arrêts du véhicule. 
 } 
 } 
 } 
 
# deuxième entité contenant des informations de mise à jour pour un autre voyage 
 entité { 
 id : "3" 
 trip_update { 
 trip { 
# les voyages basés sur la fréquence sont définis par leur#trip_id dans GTFS et 
 trip_id: "fréquence-expanded-trip" 
# start_time 
 start_time : "11:15:35" 
 } 
 stop_time_update { 
 stop_sequence: 1 
 arrivage { 
# délai négatif signifie que le véhicule a 2 secondes d’avance sur l’horaire prévu. 
 délai : -2 
 } 
 } 
 stop_time_update { 
 stop_sequence: 9 
 } 
 } 
 } 
 ``` 
 

