# Liaisons de langage Golang GTFS-realtime 
 
 Fournit des structures Golang générées à partir du protocole 
 [GTFS-realtime](https://github.com/google/transit/tree/master/gtfs-realtime) 
 Spécification du tampon. Ces structures vous permettront d’analyser un flux de données binaires en temps réel Protocol 
 Buffer GTFS dans des objets Golang. 
 
## Ajouter la dépendance 
 
 Pour utiliser les structures `gtfs-realtime-bindings` dans votre propre projet, vous devez 
 d’abord installer cette bibliothèque avec : 
 
 ``` 
 go récupérez github.com/MobilityData/gtfs-realtime-bindings/golang/gtfs 
 ``` 
 
 Et installez la dépendance de la bibliothèque golang protobuf avec : 
 ``` 
 allez chercher google.golang.org/protobuf/proto 
 ``` 
 
## Exemple de code 
 
 L’extrait de code suivant montre le téléchargement d’un flux de données GTFS en temps réel 
 à partir d’une URL particulière, en l’analysant comme un FeedMessage (le type racine du § § Schéma GTFS-temps réel) et itération sur les résultats. 
 
 ```golang 
 package main 
 
 import ( 
 "fmt" 
 "google.golang.org/protobuf/proto" 
 "github.com/MobilityData/gtfs-realtime-bindings/golang/gtfs" 
 "io/ioutil" 
 "log" 
 "net/http" 
 ) 
 
 func main() { 
 var ( 
 username = "YOUR_ACCESS_KEY" 
 mot de passe = "VOTRE_SECRET_KEY" 
 ) 
 
 client := &amp;http.Client{} 
 req, err := http.NewRequest("GET", "L’URL DE VOTRE SOURCE GTFS-REALTIME VA ICI", nil) 
 req.SetBasicAuth(nom d’utilisateur, mot de passe) 
 resp, err := client.Do(req) 
 defer resp.Body.Close() 
 if err != nil { 
 log.Fatal(err) 
 } 
 corps, err := ioutil.ReadAll(resp.Body) 
 if err != nil { 
 log.Fatal(err) 
 } 
 
 feed := gtfs. FeedMessage{} 
 err = proto.Unmarshal(body, &amp;feed) 
 if err != nil { 
 log.Fatal(err) 
 } 
 
 pour _, entité := range feed.Entity { § § tripUpdate := Entity.GetTripUpdate() 
 trip := tripUpdate.GetTrip() 
 tripId := trip.GetTripId() 
 fmt.Printf("ID de voyage : %s\n", tripId) 
 } 
 } 
 ``` 
 
 Pour plus de détails sur les conventions de dénomination des structures Golang générées 
 à partir du 
 [gtfs-realtime.proto](https://github.com/google/transit/blob/master/gtfs-realtime/proto/gtfs-realtime.proto), 
 consultez le 
 [Golang Generated Code](https://developers.google.com/protocol-buffers/docs/reference/go- généré) 
 section du site des développeur·euse de Protocol Buffers. 
