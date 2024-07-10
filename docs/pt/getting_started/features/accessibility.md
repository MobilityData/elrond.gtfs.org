# Acessibilidade 
 As funcionalidades de Acessibilidade destinam-se a fornecer às pessoas com deficiência as informações de que necessitam para aceder ao serviço. 
 
## Paradas Acessibilidade para cadeiras de rodas 
 
 Paradas Acessibilidade para cadeiras de rodas permite indicar se o embarque para cadeiras de rodas é possível a partir do local especificado. Para atender passageiros que utilizam cadeiras de rodas, especificar que o embarque em cadeira de rodas é possível é tão importante quanto especificar que t é. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Tipos de localização](../base_add-ons/#location-types) ao definir informações de acessibilidade para localizações das estações, como entradas/saídas ou áreas de embarque. 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra que o embarque para cadeiras de rodas está disponível na parada `TAS001` usando `wheelchair_boarding=1`. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|-----------|------------|---------------|---------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 | | 1 | 
 
 
## Viagens Acessibilidade para Cadeirantes 
 
 As Viagens Acessibilidade para Cadeirantes permitem indicar se um vehicle pode acomodar passageiros em cadeiras de rodas. Para atender passageiros que usam cadeiras de rodas, especificar que um vehicle pode acomodar passageiros em cadeiras de rodas é tão importante quanto especificar que um vehicle t pode. Tanto a parada quanto a viagem devem ser acessíveis para cadeiras de rodas para que o passageiro possa acessar a viagem na parada determinada. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra que o vehicle utilizado na viagem `AWE1 está equipado para acomodar pelo menos uma cadeira de rodas, e o vehicle utilizado na viagem `AWE2 não. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | wheelchair_accessible | 
 |----------|------------|---------|-----------------------| 
 | RA | NÓS | AWE1 | 1 | 
 | RA | NÓS | AWE2 | 2 | 
 
 
## Text-to-Speech 
 
 O Text-to-Speech permite fornecer as entradas necessárias para converter texto em áudio, garantindo que os passageiros que usam tecnologia assistiva para ler texto em voz alta obtenham os nomes de parada corretos ao usar o serviço de trânsito. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name` | 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir fornece uma versão legível do nome da parada, permitindo que ferramentas de conversão de texto em fala leiam o nome em voz alta. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|------------|-------------|------------|--------------------------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 | Avenida 5 e rua 53 | 
 

