# Liaisons de langage JavaScript GTFS-realtime 
 
 [![version npm](https://badge.fury.io/js/gtfs-realtime-bindings.svg)](http://badge.fury.io/js/gtfs-realtime-bindings) 
 
 Fournit des classes JavaScript et leurs types associés générés à partir du 
 [GTFS-realtime](https://github.com/google/transit/tree/master/gtfs-realtime) Protocole 
 Spécification du tampon. Ces classes vous permettront d’analyser un flux de données binaires en temps réel Protocol 
 Buffer GTFS dans des objets JavaScript. 
 
 Ces liaisons sont conçues pour être utilisées dans l’environnement [Node.js](http://nodejs.org/) 
, mais avec quelques efforts, elles peuvent probablement être utilisées dans d’autres 
 environnements JavaScript également. 
 
 Nous utilisons la bibliothèque [ProtoBuf.js](https:) pour la prise en charge 
 du tampon de protocole JavaScript. 
 
## Ajouter la dépendance 
 
 Pour utiliser les classes `gtfs-realtime-bindings` dans votre propre projet, vous devez 
 d’abord installer notre [package Node.js npm](https://www.npmjs.com/package/gtfs-realtime-bindings) : 
 
 ``` 
 npm install gtfs-realtime-bindings 
 ``` 
 
## Exemple de code 
 
 Le nœud suivant L’extrait de code.js montre le téléchargement d’un flux de données GTFS en temps réel 
 à partir d’une URL particulière, son analyse en tant que FeedMessage (le type racine du 
 du schéma GTFS en temps réel) et l’itération sur les résultats. 
 
 Pour que cet exemple fonctionne, vous devez d’abord installer `node-fetch` avec NPM. 
 
 _Remarque : cet exemple utilise des modules ES (syntaxe `import`/`export` ) et n’est pas compatible 
 avec CommonJS (syntaxe `require` ). Vous pouvez utiliser CommonJS en convertissant `import` en `require` 
 et en installant `node-fetch@2`. En savoir plus sur les modules ES [ici](https://nodejs.org/api/esm.html)._ 
 
 ```javascript 
 importer GtfsRealtimeBindings depuis "gtfs-realtime-bindings" ; 
 importer la récupération depuis "node-fetch" ; 
 
 (async() => { 
 try { 
 const réponse = wait fetch("<GTFS-realtime source URL> ", { 
 en-têtes : { 
 "x-api-key": "<redacted> ", 
//remplacer par le jeton d’authentification de votre source GTFS-realtime 
//par exemple, x-api-key est la valeur d’en-tête utilisée pour les API GTFS MTA de New York 
 }, 
 }); 
 if (!response.ok) { 
 const error = new Error(`${response.url}: ${response.status} ${response.statusText}`); 
 error.response = réponse 
 throw error ; process.exit(1); 
 } 
 const buffer = wait réponse.arrayBuffer(); 
 const feed = GtfsRealtimeBindings.transit_realtime FeedMessage( 
 new Uint8Array(buffer) 
 ); Entity.forEach((entity) => { 
 if (entity.tripUpdate) { 
 console.log(entity.tripUpdate); 
 } 
 } 
 catch (erreur) { 
); console.log(error); 
 process.exit(1); 
 } 
 })(); 
 ``` 
 
 Pour plus de détails sur les conventions de dénomination des classes JavaScript générées 
 le 
 [gtfs-realtime.proto](https://github.com/google/transit/blob/master/gtfs-realtime/proto/gtfs-realtime.proto), 
 consultez le [projet ProtoBuf.js](https://github.com/dcodeIO/ProtoBuf.js/wiki) 
 que nous utilisons pour gérer la sérialisation de notre tampon de protocole. 