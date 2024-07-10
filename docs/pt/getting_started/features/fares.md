# Tarifas 
 O GTFS permite modelar com precisão uma ampla variedade de estruturas tarifárias usadas por diferentes agências de trânsito ao redor do mundo, como tarifas baseadas por zona, por distância percorrida ou por horário. A GTFS Fares informa aos passageiros o price aplicável à sua viagem e a mídia que eles podem usar para pagar. 
 
## Produtos Tarifários 
 
 Produtos Tarifários lista os tipos de passagens ou tarifas (ou seja, tarifa de viagem única, passe mensal, taxas de transferência, etc.) oferecidas por uma agency de transporte público para acessar um serviço. Os Produtos Tarifários servem como base para a modelagem da estrutura tarifária de uma agência e estão vinculados ao serviço de transporte público por meio de mecanismos descritos em `fare_leg_rules.txt`. A associação de Produtos Tarifários a diversas condições de viagem, como routes, áreas e horários, determina os custos tarifários para segmentos de viagem individuais e transfers. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_product_id`, `fare_product_name`, `amount`, `currency`, `fare_media_id` | 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`| 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir apresenta um produto de tarifa simples (viagem única $2,75 USD). 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | 
 |------------------|--------------------|---|---| 
 | passeio único | Tarifa de viagem única | 2,75 | USD | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | fare_product_id | 
 |------------------| 
 | passeio único | 
 
 
## Fare Media 
 
 Fare Media define a mídia suportada que pode ser usada para armazenar e/ou validar um produto tarifário. Refere-se a recipientes físicos ou virtuais, como um bilhete em papel, um cartão de trânsito recarregável ou mesmo pagamento sem contato com cartões de crédito ou smartphones. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[fare_media.txt](../../../documentation/schedule/reference/#fare_mediatxt)|`fare_media_id`, `fare_media_name`, `fare_media_type`| 
 |[fare_products.txt](../../../documentation/schedule/reference/#fare_productstxt)|`fare_media_id`| 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra um trecho de diferentes mídias tarifárias na área da baía de São Francisco. `Clipper` é descrito como um cartão de transporte público físico com `fare_media_type=2`. `SFMTA Munimobile` é descrito como um aplicativo móvel com `fare_media_type= 2`. `Dinheiro` que é dado diretamente ao motorista sem bilhete, é `fare_media_type=0`. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_mediatxt"><b>.txt</b></a><br> 
</p> 
 
 | fare_media_id | fare_media_name | fare_media_type | 
 |---------------|------------------|----------------| 
 | cortador | Cortador | 2 | 
 | munimóvel | SFMTA MuniMobile | 4 | 
 | dinheiro | Dinheiro | 0 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_productstxt"><b>fare_products.txt</b></a><br> 
</p> 
 
 | fare_product_id | fare_product_name | amount | currency | fare_media_id | 
 |------------------|--------------------|---|---|---| 
 | passeio único | Tarifa de viagem única | 2,75 | USD | munimóvel | 
 
 
 
 
## Tarifas baseadas em rota 
 
 Tarifas baseadas em rota são usadas para atribuir tarifas diferentes para grupos específicos de routes, como tarifas especiais para serviços expressos ou tarifas diferenciadas entre um Bus Rapid Serviço de transporte público versus serviços tradicionais de ônibus. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[routes.txt](../../../documentation/schedule/reference/#routestxt)|`network_id`| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `network_id`| 
 |[netowrks.txt](../../../documentation/schedule/reference/#networkstxt)|`network_id`, `network_name`| 
 |[route_networks.txt](../../../documentation/schedule/reference/#route_networkstxt)|`network_id`, `route_id`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Recurso de produtos tarifários](#fare-products) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra um sistema que categoriza routes em categorias expressas e locais, cada uma associada a produtos tarifários distintos.</p> 
 
<p style="font-size:16px"> **Usando `redes.txt` + `route_networks.txt`**</p> 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#networkstxt"><b>redes.txt</b></a><br> 
</p> 
 
 | network_id | network_name | 
 |------------|-----------------| 
 | expresso | Expresso | 
 | locais | Locais | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#route_networkstxt"><b>.txt</b></a><br> 
</p> 
 
 | network_id | route_id | 
 |------------|-----------| 
 | expresso | expresso_a | 
 | expresso | expresso_b | 
 | locais | local_1 | 
 | locais | local_2 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | expresso | expresso_single_ride | 
 | locais | local_single_ride | 
 
<p style="font-size:16px"> **OU usando `routes.networks_id`**</p> 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#routestxt"><b>routes.txt</b></a><br> 
</p> 
 
 | route_id | network_id | 
 |------------|------------| 
 | expresso_a | expresso | 
 | expresso_b | expresso | 
 | local_1 | locais | 
 | local_2 | locais | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | network_id | fare_product_id | 
 |------------|-----------------| 
 | expresso | expresso_single_ride | 
 | locais | local_single_ride | 
 
 
## Tarifas Baseadas no Tempo 
 
 Tarifas Baseadas no Tempo são usadas para atribuir tarifas para horários específicos do dia ou dias da semana, como tarifas de pico e fora de pico e/ou tarifas de fim de semana. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_timeframe_group_id`, `to_timeframe_group_id`| 
 |[timeframes.txt](../../../documentation/schedule/reference/#timeframestxt)|`timeframe_group_id`, `start_time`, `end_time`, `service_id`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Recurso de produtos tarifários](../fares/#fare-products) 
 
 ?? ? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir apresenta um sistema onde o horário de pico é das 8h00 às 10h00 e os demais horários são fora de pico.</p> 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#timeframestxt"><b>prazos.txt</b></a><br> 
</p> 
 
 | timeframe_group_id | start_time | end_time | service_id | 
 |--------------------|------------|----------|------------| 
 | pico | 8:00:00 | 10:00:00 | todo_dia | 
 | normal | 0:00:00 | 08:00:00 | todo_dia | 
 | normal | 10:00:00 | 24:00:00 | todo_dia | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_timeframe_group_id | fare_product_id | 
 |------------------------|---------------------| 
 | pico | pico_single_ride | 
 | normal | passeio_single_regular | 
 
 
## Tarifas baseadas em zona 
 
 Tarifas baseadas em zona são usadas para representar sistemas baseados em zona onde uma tarifa específica se aplica ao viajar de uma zona específica para outra. Uma zona é definida por um grupo de stops. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`fare_product_id`, `from_area_id`, `to_area_id`| 
 |[areas.txt](../../../documentation/schedule/reference/#areastxt)|`area_id`, `area_name`| 
 |[stop_areas.txt](../../../documentation/schedule/reference/#stop_areastxt)|`area_id`, `stop_id`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Recurso de produtos tarifários](../fares/#fare-products) 
 
 ?? ? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra a tarifa da Zona A para a Zona B.</p> 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#areastxt"><b>areas.txt</b></a><br> 
</p> 
 
 | area_id | area_name | 
 |---------|-----------| 
 | zona_a | Zona A | 
 | zona_b | Zona B | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stop_areastxt"><b>stop_areas.txt</b></a><br> 
</p> 
 
 | area_id | stop_id | 
 |---------|-----| 
 | zona_a | pare_a | 
 | zona_a | parar_b | 
 | zona_b | parar_c | 
 | zona_b | parar_d | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | from_area_id | to_area_id | fare_product_id | 
 |-------------|------------|-----------------| 
 | zona_a | zona_b | zona_a_b_single | 
 
## Transferências Tarifárias 
 
 As Transferências Tarifárias são usadas para definir regras aplicáveis ​​em transferências entre trechos (ou segmentos de viagem individuais). Isto permite modelar o custo total de uma viagem de vários trechos, contabilizando políticas de transferência especiais, como transfers gratuitas por um limite de tempo específico, ou aplicando descontos tarifários com base nos trechos já percorridos. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[fare_leg_rules.txt](../../../documentation/schedule/reference/#fare_leg_rulestxt)|`leg_group_id`| 
 |[fare_transfer_rules.txt](../../../documentation/schedule/reference/#fare_transfer_rulestxt)|`from_leg_group_id`, `to_leg_group_id`, `transfer_count`, `duration_limit`, `duration_limit_type`, `fare_transfer_type`, `fare_product_id`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Recurso de produtos tarifários](../fares/#fare-products) 
 
 ?? ? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir ilustra que dentro de uma janela de 2 horas, transfers gratuitas ilimitadas são permitidas entre a Etapa A dentro do sistema.</p> 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_leg_rulestxt"><b>fare_leg_rules.txt</b></a><br> 
</p> 
 
 | leg_group_id | 
 |---------------| 
 | um | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_transfer_rulestxt"><b>fare_transfer_rules.txt</b></a><br> 
</p> 
 
 | from_leg_group_id | to_leg_group_id | transfer_count | duration_limit | duration_limit_type | fare_transfer_type | fare_product_id | 
 |-------------------|-----------------|----------------|----------------|---------------------|--------------------|-----------------| 
 | um | um |-1 | 7200 | 1 | 0 | transferência_livre | 
 
 
## Tarifas v1 
 
 Tarifas v1 é uma alternativa legada a outros recursos de Tarifas descritos acima. Ele permite modelar informações básicas de tarifas, como preços de tarifas, transfers de métodos de pagamento e tarifas baseadas em zona usando os arquivos `fare_rules.txt` e `fare_attributes.txt`. Embora mais simples de produzir, é menos capaz de modelar estruturas tarifárias mais complexas e pode ser descontinuado com endosso suficiente de outros recursos de tarifa (que fazem parte do que é chamado de Fares v2). 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`zone_id`| 
 |[fare_attributes.txt](../../../documentation/schedule/reference/#fare_attributestxt)|`fare_id` `price` `currency_type` `payment_method` `transfers` `agency_id` `transfer_duration`| 
 |[fare_rules.txt](../../../documentation/schedule/reference/#fare_rulestxt)|`fare_id` `route_id` `origin_id` `destination_id` `contains_id`| 
 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir ilustra que uma viagem em uma rede custa CAD $ 3,20 usando um cartão pré-pago, permitindo transfers gratuitas em um período de 2 horas.</p> 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_attributestxt"><b>fare_attributes.txt</b></a><br> 
</p> 
 
 | fare_id | price | currency_type | payment_method | transfers | transfer_duration | 
 |----|-------|---------------|----------------|-----------|-------------------| 
 | cartão_fare pré-pago | 3.2 | CAD | 1 | | 7200 | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#fare_rulestxt"><b>fare_rules.txt</b></a><br> 
</p> 
 
 | fare_id | route_id | origin_id | destination_id | 
 |-------------------|----------|-----------------|-----------------| 
 | cartão_fare pré-pago | linha1 | estações_de_metrô | estações_de_metrô | 
 | cartão_fare pré-pago | linha2 | estações_de_metrô | estações_de_metrô | 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | Um | pararA | 43.670049 |-79.385389 | estações_de_metrô | 
 | B | pararB | 43.671049 |-79.386789 | estações_de_metrô | 
 
 
 | stop_id | stop_name | stop_lat | stop_lon | zone_id | 
 |---------|-----------|-----------|------------|-----------------| 
 | Um | pararA | 43.670049 |-79.385389 | estações_de_metrô | 
 | B | pararB | 43.671049 |-79.386789 | estações_de_metrô | 
 
 

