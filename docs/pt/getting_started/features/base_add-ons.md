# Complementos do Base 
 Esses recursos expandem os recursos descritos no Base, servindo para aprimorar a abrangência de um conjunto de dados GTFS para fornecer uma melhor experiência aos passageiros ou facilitar a colaboração entre agências, fornecedores de dados e reutilizadores de dados. Essas melhorias podem implicar a introdução de novos campos nos arquivos descritos no Base ou a criação de novos arquivos. 
 
## Feed Information 
 
 Feed Information comunica informações importantes sobre o feed, como sua validade ( date de início e término), a organização de publicação e informações de contato para consultas sobre o conjunto de dados GTFS e práticas de publicação de dados. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[feed_info.txt](../../../documentation/schedule/reference/#feed_infotxt)|`feed_publisher_name`, `feed_publisher_url`, `feed_lang`, `default_lang`, `feed_start_date`, `feed_end_date`, `feed_version`, `feed_contact_email`, `feed_contact_url` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#feed_infotxt"><b>feed_info.txt</b></a><br> 
</p> 
 
 | feed_publisher_name | feed_publisher_url | feed_lang | default_lang | feed_start_date | feed_end_date | feed_version | feed_contact_email | feed_contact_url | 
 |--------------------------|----------------------|-----------|--------------|-----------------|---------------|--------------|-----------------------|------------------------------| 
 | Transportes da Grande Região | https://www.gra1.org | pt | pt | 20240101 | 20241231 | 3.1 | suporte@gra1.org | https://www.gra1.org/support | 
 
## Formas 
 As formas podem ser definidas e associadas a viagens, permitindo que aplicativos de planejamento de viagens exibam viagens em um mapa e informem os passageiros sobre a distância que eles precisam percorrer em um vehicle de transporte público. Os campos `shape_dist_traveled` são usados ​​para determinar programaticamente quanto de uma shape desenhar ao mostrar um mapa aos passageiros. 
 Ao definir Shapes, existe um equilíbrio entre o seu nível de detalhe (por exemplo, seguindo a curvatura exacta das estradas) e transmitindo apenas a informação necessária de forma eficiente. 
 
 |Arquivos incluídos |Campos incluídos | 
 |----------------------------------|------------------| 
 |[shapes.txt](../../../documentation/schedule/reference/#shapestxt) | `shape_id`, `shape_pt_lat`, `shape_pt_lon`, `shape_pt_sequence`, `shape_dist_traveled` | 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt) | `shape_id` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt) |`shape_dist_traveled`| 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra uma parte de uma shape do feed TriMet GTFS (baixe <a     href="https://developer.trimet.org/GTFS.shtml">aqui</a> ).<br><br> 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#shapestxt">shapes.txt</a><br> 
</p> 
 
 | shape_id | shape_pt_lat | shape_pt_lon | shape_pt_sequence | shape_dist_traveled | 
 |---------|-------------|-------------|------------------|-------------------| 
 | 558674 | 45.47623 |-122.721885 | 1 | 0,0 | 
 | 558674 | 45.476235 |-122.72236 | 2 | 121,9 | 
 | 558674 | 45.476237 |-122.722523 | 3 | 163,7 | 
 | 558674 | 45.476242 |-122.723024 | 4 | 292,2 | 
 | 558674 | 45.476244 |-122.72316 | 5 | 327,1 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt">trips.txt</a><br> 
</p> 
 
 | trip_id | shape_id| 
 |--------|--------| 
 |13302375|558674 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt">stop_times.txt</a><br> 
</p> 
 
 | trip_id | stop_sequence| shape_dist_traveled| 
 |--------|-------------|-------------------| 
 |13302375|1 |0 | 
 |13302375|2 |461,7 | 
 |13302375|3 |1245 | 
 
## Cores da Rota 
 
 Usar Cores da Rota permite representar e comunicar com precisão o esquema de cores atribuído a routes específicas pelas diretrizes de design da agência. Isso permite que os usuários identifiquem facilmente os serviços de transporte público pela cor oficial. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`route_color`, `route_text_color` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra que a rota `RA` é laranja usando um código de cor HEX `D95700`, e que o texto deve ser renderizado em preto usando um código de cor HEX `0`. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | agency_id | route_short_name | route_long_name | route_type | route_color | route_text_color | 
 |----------|-----------|------------------|--------------------|------------|------------|------------------| 
 | RA | agência001 | 17 | Missão- Centro | 3 | D95700 | 0 | 
 
## Bicicleta Permitida 
 
 Bicicleta Permitida indica se os veículos que atendem viagens específicas têm condições de acomodar bicicletas ou não, auxiliando os usuários a planejar e acessar serviços que lhes permitam realizar viagens multimodais. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`bikes_allowed` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir especifica que o vehicle utilizado na viagem `AWE1` pode acomodar pelo menos uma bicicleta a bordo (`bikes_allowed=1`), e o vehicle utilizado na viagem `AWE2` não pode (`bikes_allowed=2`). 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | bikes_allowed | 
 |----------|------------|---------|---------------| 
 | RA | NÓS | AWE1 | 1 | 
 | RA | NÓS | AWE2 | 2 | 
 
## Headsigns 
 
 Headsigns permite comunicar a sinalização utilizada pelos veículos indicando o destino da viagem, facilitando aos usuários a identificação do serviço de trânsito correto. Este recurso oferece suporte a alterações de sinalização ao longo de uma rota específica. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`trip_headsign` | 
 |[stop_times.txt](../../../documentation/schedule/reference/#stop_timestxt)|`stop_headsign`| 
 
 **Pré-requisito**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 No exemplo a seguir, a primeira tabela especifica os headsigns a serem utilizados pelas viagens `AWE1` e `AWE2`, e a segunda indica que o headsign de `AWE1` será modificado após a parada `TAS004`, substituindo aquele especificado em `trips.txt. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | trip_headsign | 
 |----------|------------|---------|---------------| 
 | RA | NÓS | AWE1 | Centro da cidade | 
 | RA | NÓS | AWE2 | Missão | 
 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_timestxt"><b>stop_times.txt</b></a><br> 
</p> 
 
 | trip_id | arrival_time | departure_time | stop_id | stop_sequence | stop_headsign | 
 |--------|--------------|----------------|---------|---------------|------------| 
 | AWE1 | 6:10:00 | 6:10:00 | TAS001 | 1 | | 
 | AWE1 | 6:14:00 | 6:14:00 | TAS002 | 2 | | 
 | AWE1 | 6:20:00 | 6:20:00 | TAS003 | 3 | | 
 | AWE1 | 6:23:00 | 6:23:00 | TAS004 | 4 | Centro- Praça Principal | 
 | AWE1 | 6:25:00 | 6:25:00 | TAS005 | 5 | Centro- Praça Principal | 
 
## Tipos de localização 
 
 Os tipos de localização são usados ​​para classificar áreas-chave dentro de estações de transporte público, como saídas/entradas, nós ou áreas de embarque, bem como seu relacionamento. Os tipos de localização servem como base para a modelagem de estações de transporte público usando Pathways. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`location_type`, `parent_station` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra vários locais dentro de uma estação de transporte público em `stops.txt`: a estação pai, representando o local principal, e seus locais filhos, como plataformas, entradas/existências e nós genéricos. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | location_type | parent_station | 
 |--------------|-------------------------------------------------------|---------------|----------------| 
 | Estação_A102 | Estação da rua principal | 1 | | 
 | A102_B01 | Estação Main Street- Plataforma Norte | 0 | Estação_A102 | 
 | A102_B02 | Estação Main Street- Plataforma Sul | 0 | Estação_A102 | 
 | A102_E01 | Estação Main Street- Entrada/Saída | 2 | Estação_A102 | 
 | A102_S01 | Estação Main Street- Topo da escada de entrada | 3 | Estação_A102 | 
 | A102_S02 | Estação Main Street- Parte inferior da escada de entrada | 3 | Estação_A102 | 
 | A102_S03 | Estação Main Street- Topo das escadas da plataforma norte | 3 | Estação_A102 | 
 | A102_S04 | Estação Main Street- Parte inferior das escadas da plataforma norte | 3 | Estação_A102 | 
 | A102_S05 | Estação Main Street- Topo das escadas da plataforma sul | 3 | Estação_A102 | 
 | A102_S06 | Estação Main Street- Parte inferior das escadas da plataforma sul | 3 | Estação_A102 | 
 | A102_F01 | Estação Main Street- Lado pago da tarifa | 3 | Estação_A102 | 
 | A102_F02 | Estação Main Street- lado não pago da tarifa | 3 | Estação_A102 | 
 
## Serviço Baseado em Frequência 
 
 O Serviço Baseado em Frequência pode ser usado para modelar serviços que operam em uma frequência regular, como ônibus operando a cada 10 minutos ou serviços de metrô operando 2 minutos dentro de intervalos de tempo especificados. 
 Ao modelar um serviço baseado em frequência, `stop_times.txt` contém os tempos relativos entre as stops para determinar os tempos a serem exibidos aos passageiros. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[frequencies.txt](../../../documentation/schedule/reference/#frequenciestxt)| `trip_id`, `start_time`, `end_time`, `headway_secs`, `exact_times` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra duas viagens distintas: viagem `AWE1` que ocorre a cada 30 minutos (`headway_secs=1800`), e viagem `AWE2` que ocorre a cada 15 minutos (`headway_secs=900`). 
<p style="font-size:16px"> 
 O campo `exact_times` indica se a programação segue o horário exato de início informado no campo ’ start_time’: 
 - A viagem `AWE1 sai a cada 30min das 6h10 às 12h00. 
 - a viagem `AW2` sai às 6h00, 6h15, 6h30 e assim por diante. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#frequenciestxt"><b>frequencies.txt</b></a><br> 
</p> 
 
 | trip_id | start_time | end_time | headway_secs | exact_times | 
 ---------|-----------|----------|--------------|------------| 
 AWE1 | 6:10:00 | 12:00:00 | 1800 | 0 | 
 AWE2 | 6:00:00 | 19:50:00 | 900 | 1 | 
 
## Transferências 
 
 As transferências fornecem detalhes sobre as transições entre diferentes segmentos (ou trechos) de viagem, permitindo que os planejadores de viagem determinem a viabilidade de viagens que incluem transfers. Especificar transfers não significa que os passageiros t possam fazer transferência para outro lugar, apenas mostra se certas transfers não são possíveis ou require um tempo mínimo para transferência. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[transfers.txt](../../../documentation/schedule/reference/#transferstxt)|`from_stop_id`, `to_stop_id`, `from_route_id`, `to_route_id`, `from_trip_id`, `to_trip_id`, `transfer_type, `min_transfer_time| 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra três transfers diferentes: uma entre stops que requer um tempo mínimo de transferência de 5 minutos, um ponto de transferência cronometrado entre duas routes e uma transferência no assento entre duas viagens feitas pelo mesmo vehicle. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#transferstxt"><b>transfers.txt</b></a><br> 
</p> 
 
 | from_stop_id | to_stop_id | from_route_id | to_route_id | from_trip_id | to_trip_id | transfer_type | min_transfer_time | 
 |-------------|------------|---------------|-------------|-------------|------------|---------------|-------------------| 
 | s6 | s7 | | | | | 2 | 300 | 
 | | | | | PL04-003 | DL57-008 | 4 | | 
 | | | BR09 | CR01 | BR09-012 | CR01-005 | 1 | | 
 
## Traduções 
 
 As traduções permitem que informações de serviço, como nomes de estações, sejam fornecidas em vários idiomas, permitindo que os planejadores de viagens exibam as informações em um idioma específico, dependendo do idioma do usuário e das configurações de localização. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[translations.txt](../../../documentation/schedule/reference/#translationstxt)|`table_name`,`field_name`,`idioma`,`translation`,`record_id`,`record_sub_id`,`field_value` | 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra traduções em francês e espanhol sendo fornecidas para dois campos usados ​​em `routes.txt`: `route_long_name` e `route_desc`. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#translationstxt"><b>translations.txt</b></a><br> 
</p> 
 
 | table_name | field_name | idioma | tradução | record_id | record_sub_id | field_value | 
 |------------|-----------------|----------|-------------------------------------------------------|-----------|---------------|------------| 
 | routes | route_long_name | ES | Missão- Centro | RA | | | 
 | routes | route_long_name | França | Missão- Centro da cidade | RA | | | 
 | routes | route_desc | ES | La ruta "A" viaja de Lower Mission até o centro | RA | | | 
 | routes | route_desc | França | A rota «A» depende da Lower Mission no centro da cidade. | RA | | | 
 
## Atribuições 
 
 As atribuições permitem compartilhar detalhes adicionais sobre as organizações envolvidas na criação do conjunto de dados (produtores, operadores e/ou autoridades, etc.). 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[attributions.txt](../../../documentation/schedule/reference/#attributionstxt) |`attribution_id`, `agency_id`, `route_id`, `trip_id`, `organization_name`, `is_producer`, `is_operator, `is_authority, `attribution_url, `attribution_email, `attribution_phone| 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#attributionstxt"><b>attributions.txt</b></a><br> 
</p> 
 
 | attribution_id | agency_id | route_id | trip_id | organization_name | is_producer | is_operator | is_authority | attribution_url | attribution_email | attribution_phone | 
 |----------------|-----------|----------|---------|--------------------------|-------------|-------------|--------------|----------------------------------|----------------------------|-------------------| 
 | op01 | tb | | | Ônibus de trânsito | | 1 | | https://www.transitbus.org/fares | contact@transitbus.org | (777) 555-7777 | 
 | au01 | gra | | | Transportes da Grande Região | 1 | | 1 | https://www.gra1.org | contact@gra1.org | (555) 555-5555 | 
 | op02 | | rtd023 | | Empresa de ônibus A | | 1 | | https://www.buscompanya.com | contact@buscompanya.com | (333) 333-3333 | 
 | op03 | | rtd025 | | Empresa de ônibus B | | 1 | | https://www.buscompanyb.com | contact@buscompanyb.com | (888) 888-8888 | 
 

