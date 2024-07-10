# Base 
 Os recursos a seguir fornecem os elementos mais básicos e essenciais que uma GTFS precisa para representar um serviço de trânsito. Uma GTFS consiste em routes, cada uma com viagens associadas. Essas viagens visitam uma ou mais stops em horários específicos. As viagens contêm apenas informações sobre a hora do dia e os dias em que operam são determinados por calendários. 
 Todos esses recursos devem ser implementados em conjunto para permitir um feed GTFS funcional. 
 
## Agência 
 
 As agências contêm informações básicas sobre as agências responsáveis ​​pelo serviço de transporte público, como nome, URL do site e idioma e fuso horário em que o serviço opera. Isto permite combinar serviços específicos com a agency correspondente. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[agency.txt](../../../documentation/schedule/reference/#agencytxt)|`agency_id`, `agency_name`, `agency_url`, `agency_timezone`, `agency_lang`, `agency_phone`, `agency_fare_url, `agency_email| 
 
 **Pré-requisitos**: 
 
 - Todos os outros recursos da Base 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#agencytxt"><b>agency.txt</b></a><br> 
</p> 
 
 | agency_id | agency_name | agency_url | agency_timezone | agency_lang | agency_phone | agency_fare_url | agency_email | 
 |-----------|-------------|----------------------------|---------------------|-------------|----------------|----------------------------------|------------------------| 
 | tb | Ônibus de trânsito | https://www.transitbus.org | America/Los_Angeles | PT | (777) 555-7777 | https://www.transitbus.org/fares | contact@transitbus.org | 
 
 
 
## Paradas 
 
 As paradas representam os elementos básicos usados ​​para identificar onde um serviço de transporte público pega e desembarca passageiros. Pode ser uma estação de metrô ou um ponto de ônibus. Cada parada tem, entre outros atributos, coordenadas geográficas para identificar sua localização em um mapa e um nome que corresponde aos materiais da agência voltados para os passageiros. As paradas são associadas às viagens usando Stop Times. 
 Com GTFS, também é possível descrever o interior de estações maiores, como uma estação de trem ou uma estação de ônibus, usando [Pathways](/getting_started/features/pathways). 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)| `stop_id`, `stop_code`, `stop_name`, `stop_desc`, `stop_lat`, `stop_lon`, `stop_url`, `stop_timezone`, `platform_code` | 
 
 **Pré-requisitos**: 
 
 - Todos os outros recursos da Base 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_code | stop_desc | stop_name | stop_lat | stop_lon | stop_url | stop_timezone | platform_code | 
 |---------|-----------|-----------------------------------------------|------------|-----------|------------|-------------------------------------------------------|---------------|---------------| 
 | TAS001 | TAS001 | Esquina sudoeste da Avenida 5 com Rua 53 | 5 Av/53 St | 45.503568 |-73.587079 | https://www.transitbus.org/stops/TAS001 | | | 
 
 
## Rotas 
 
 Uma rota é um grupo de viagens sob a mesma marca que são exibidas aos passageiros como um único serviço. Cada rota tem, entre outros atributos, um nome que corresponde aos materiais da agência voltados para o passageiro e ao tipo de serviço que está sendo representado (como ônibus, metrô ou metrô, balsa, etc.). 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)| `route_id`, `agency_id`, `route_desc`, `route_type`, `route_url`, `route_sort_order`, `route_short_name`, `route_long_name`| 
 
 **Pré-requisitos**: 
 
 - Todos os outros recursos da Base 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir define uma rota de ônibus (`route_type=3`). 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_desc | route_type | route_url | route_sort_order | 
 |----------|-----------|------------------|--------------------|-------------------------------------------|------------|--------------------------------------|------------------| 
 | RA | tb | 17 | Missão- Centro | A rota "A" viaja de Lower Mission até Downtown. | 3 | https://www.transitbus.org/routes/ra | 12 | 
 
 
## Datas de serviço 
 
 As datas de serviço indicam o intervalo de datas em que um serviço está em execução, bem como criam isenções de serviço, como feriados e outros serviços especiais em datas específicas. 
 Funciona definindo uma date de início e uma date de término em `calendars.txt`, depois um marcador para cada dia da semana em que opera. Se houver alterações na programação de um único dia durante esse período, o arquivo `calendar_dates.txt` poderá ser usado para substituir a programação de cada um desses dias. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[calendar.txt](../../../documentation/schedule/reference/#calendartxt)|`service_id`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `start_date`, `end_date`| 
 |[calendar_dates.txt](../../../documentation/schedule/reference/#calendar_datestxt)|`service_id`, `date`, `exception_type`| 
 
 **Pré-requisitos**: 
 
 - Todos os outros recursos da Base 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir define dois serviços (dia útil e fim de semana) para o mês de julho de 2024, incluindo um serviço especial de feriado no dia 4 de julho, funcionando como serviço de fim de semana. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendartxt"><b>calendar.txt</b></a><br> 
</p> 
 
 | service_id | monday | tuesday | wednesday | thursday | friday | saturday | sunday | start_date | end_date | 
 |--------|----|---------|-----------|----------|--------|----------|--------|------------|----------| 
 | NÓS | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 20240701 | 20240731 | 
 | WD | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 20240701 | 20240731 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#calendar_datestxt"><b>calendar_dates.txt</b></a><br> 
</p> 
 
 | service_id | date | exception_type | 
 |------------|----------|----------------| 
 | WD | 20240704 | 2 | 
 | NÓS | 20240704 | 1 | 
 
## Trips 
 
 Trips reúne Rotas e datas de serviço para criar viagens que podem ser realizadas pelos passageiros. As viagens são associadas às paradas através dos tempos de parada. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)| `route_id`, `service_id`, `trip_id`, `trip_short_name`, `direction_id`, `block_id`| 
 
 **Pré-requisitos**: 
 
 - Todos os outros recursos da Base 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir define duas viagens em ambos os sentidos para a rota RA. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_short_name | direction_id | block_id | 
 |----------|------------|---------|-----------------|-------------|----------| 
 | RA | NÓS | AWE1 | 3885 | 0 | 1 | 
 | RA | NÓS | AWE2 | 3887 | 1 | 2 | 
 
## Horários de parada 
 
 Os horários de parada são usados ​​para representar os horários individuais de arrival e departure de cada viagem, permitindo que os passageiros saibam com precisão a que horas o ônibus, trem ou balsa está chegando e saindo de um local específico. O arquivo `stop_times.txt` normalmente é o maior em um feed GTFS. 
 Certos serviços operam com frequência regular (por exemplo, uma linha de metrô que passa a cada 5 minutos) em vez de terem horários específicos de arrival e departure. Isso pode ser modelado usando [serviços baseados em frequência](../base_add-ons/#frequency-based-service) e pode ser modelado em conjunto com `stop_times.txt`. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)| `trip_id`, `arrival_time`, `departure_time`, `stop_id`, `stop_sequence`, `pickup_type`, `drop_off_type`, `timepoint` | 
 
 **Pré-requisitos**: 
 
 - Todos os outros recursos da Base 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir define o cronograma para uma viagem com 5 stops. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | pickup_type | drop_off_type | timepoint | 
 |--------|--------------|----------------|---------|---------------|-------------|---------------|-----------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | 0 | 0 | 1 | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | 0 | 0 | 1 | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | 0 | 0 | 1 | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | 0 | 0 | 1 | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | 0 | 0 | 1 | 
 

