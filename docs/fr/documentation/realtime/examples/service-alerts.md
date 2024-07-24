# Alerte de service 
 
 L’exemple suivant est une représentation ASCII d’un flux d’alerte. 
 
 ```python#informations d’en-tête 
 en-tête { 
# version de la spécification de vitesse. Actuellement "2.0". Les versions valides sont "2.0", "1.0". 
 gtfs_realtime_version : "2.0" 
 
# détermine si l’ensemble de données est incrémentiel ou complet 
 incrémentalité : FULL_DATASET#l’heure à laquelle cet ensemble de données a été généré sur le serveur#pour déterminer la séquence des flux d’alerte 
 timestamp : 1284457468 
 } 
# plusieurs entités peuvent être incluses dans le flux 
 entité { 
# identifiant unique de l’entité 
 id : "0" 
 
# "type" de l’entité 
 alerte { 
# plusieurs périodes peuvent être définies lorsque l’alerte est active 
 active_period { 
# heure de début au format d’époque POSIX 
 début : 1284457468#heure de fin au format d’époque POSIX 
 fin : 1284468072 
 } 
# sélectionne quelles entités GTFS seront affectées 
 informé_entity { 
# paramètres valides : 
# Agency_id, route_id, route_type, stop_id, trip (voir TripDescriptor) 
 route_id: "219" 
 } 
# sélecteurs multiples ( informé_entity) peut être inclus dans une seule entité d’alerte 
 informé_entity { 
 stop_id: "16230" 
 } 
# plusieurs champs peuvent être inclus dans une seule informé_entity 
 informé_entity { 
 stop_id: "16299" 
 route_id: " 100" 
# Cet exemple signifie l’itinéraire 100 à l’arrêt 16299. 
# Ceci ne s’applique à aucun autre arrêt sur l’itinéraire 100 ni à tout autre itinéraire à l’arrêt 16299. 
 } 
 
# cause de l’alerte- voir gtfs-realtime.proto pour les valeurs valides 
 cause : CONSTRUCTION#effet de l’alerte- voir gtfs-realtime.proto pour les valeurs valides 
 effet : DÉTOUR#l’url donnée fournit des informations supplémentaires 
 url { 
# plusieurs langues/traductions prises en charge 
 traduction { 
# page hébergée en dehors de Google (chez le fournisseur/l’agence, etc.) 
 texte : "http://www.sometransitagency/alerts" 
 langue : "en " 
 } 
 } 
 
# l’en-tête de l’alerte sera mis en surbrillance 
 header_text { 
# plusieurs langues/traductions prises en charge 
 traduction { 
 texte : "L’arrêt à la rue Elm est fermé, arrêt temporaire à Oak street" 
 langue : "fr" 
 } 
 } 
 
# Description de l’alerte. Informations supplémentaires sur le texte d’en-tête 
 description_text { 
# plusieurs langues/traductions prises en charge 
 traduction { 
 texte : "En raison de travaux sur la rue Elm, l’arrêt est fermé. L’arrêt temporaire se trouve à 300 mètres au nord de la rue Oak " 
 langue : "fr" 
 } 
 } 
 } 
 } 
 ``` 
 
 
