# Caminhos 
 Os recursos de caminhos podem modelar grandes estações de transporte público, guiando os passageiros desde as entradas e saídas das estações até o local onde eles embarcam ou desembarcam de um vehicle de transporte público. Alguns desses recursos tornam possível comunicar as características físicas de um caminho e o tempo estimado de navegação, além de sistemas de orientação do mundo real empregados nas estações. 
 
## Conexões de caminhos 
 
 Em seu nível fundamental, o Pathways oferece funcionalidade básica para conectar áreas-chave definidas em Tipos de localização dentro de uma estação. Essas conexões formam pathways, permitindo aos usuários obter direções precisas (por exemplo, de uma entrada até a área de embarque), o que é particularmente útil na navegação em estações de trânsito grandes e complexas. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`pathway_id`, `from_stop_id`, `to_stop_id`, `pathway_mode`, `is_bidirectional` | 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Tipos de localização](../base_add-ons/#location-types) 
 
 ? ?? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir define múltiplas conexões (também chamadas de pathways) entre locais pré-estabelecidos (definidos como stops): passarelas (`pathway_mode=1), escadas (`pathway_mode=2) e portão de passagem (`pathway_mode=6`). A bidirecionalidade também é especificada. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | from_stop_id | to_stop_id | pathway_mode | is_bidirectional | 
 |------------|--------------|------------|--------------|------------------| 
 | PrincipalSt-001 | A102_E01 | A102_S01 | 1 | 1 | 
 | PrincipalSt-002 | A102_S01 | A102_S02 | 2 | 1 | 
 | PrincipalSt-003 | A102_S02 | A102_F02 | 1 | 1 | 
 | PrincipalSt-004 | A102_F02 | A102_F01 | 6 | 1 | 
 | PrincipalSt-005 | A102_F01 | A102_S03 | 1 | 1 | 
 | PrincipalSt-006 | A102_S03 | A102_S04 | 2 | 1 | 
 | PrincipalSt-007 | A102_F01 | A102_S05 | 1 | 1 | 
 | PrincipalSt-008 | A102_S05 | A102_S06 | 2 | 1 | 
 | PrincipalSt-009 | A102_S04 | A102_B01 | 1 | 1 | 
 | PrincipalSt-010 | A102_S06 | A102_B02 | 1 | 1 | 
 
 
## Detalhes do caminho 
 
 Mais detalhes podem ser adicionados em relação às características físicas dos pathways de uma estação, incluindo comprimento, largura e inclinação (para rampas) ou o número de escadas (para escadas). Isso ajuda os ciclistas a antecipar as condições e a acessibilidade do caminho que precisam percorrer. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`max_slope`, `min_width`, `length`, `stair_count`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Conexões de caminho](#conexões de caminho) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir define detalhes adicionais para pathways pré-estabelecidos, incluindo largura mínima, contagem de passos para escadas e comprimento e inclinação máxima para passarelas. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | max_slope | min_width | comprimento | stair_count | 
 |--------|-----------|-----------|--------|-------------| 
 | PrincipalSt-001 | 0 | 4.3 | 3.6 | | 
 | PrincipalSt-002 | | 2.2 | | 15 | 
 | PrincipalSt-003 | 0,06 | 4 | 3.1 | | 
 | PrincipalSt-004 | | 0,9 | 2.9 | | 
 | PrincipalSt-005 | 0 | 3.5 | 5 | | 
 | PrincipalSt-006 | | 2.2 | | 18 | 
 | PrincipalSt-007 | 0 | 3.5 | 5 | | 
 | PrincipalSt-008 | | 2.2 | | 18 | 
 | PrincipalSt-009 | 0 | 6 | 2 | | 
 | PrincipalSt-010 | 0 | 6 | 2 | | 
 
 
## Níveis 
 
 Os níveis podem ser usados ​​para listar todos os diferentes níveis dentro de uma estação, fornecendo aos usuários uma camada adicional de informações para as estações. Esse recurso também permite o uso de elevadores em conjunto com o recurso de conexões Pathways. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[levels.txt](../../../documentation/schedule/reference/#levelstxt)|`level_id`, `level_index`, `level_name`| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`level_id`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Tipos de localização](../base_add-ons/#location-types) 
 
 ? ?? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra os diferentes níveis de uma estação. Os locais (definidos como stops) são então atribuídos ao seu nível correspondente. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | level_id | level_index | level_name | 
 |----|-------------|------------| 
 | nível_0_rua | 0 | Na rua | 
 | level_-1_lobby |-1 | Átrio | 
 | nível_-2_plataforma |-2 | Plataforma | 
 
 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | stop_id | level_id | 
 |-------------|----------| 
 | Estação_A102 | | 
 | A102_B01 |-2 | 
 | A102_B02 |-2 | 
 | A102_E01 | 0 | 
 | A102_S01 | 0 | 
 | A102_S02 |-1 | 
 | A102_S03 |-1 | 
 | A102_S04 |-2 | 
 | A102_S05 |-1 | 
 | A102_S06 |-2 | 
 | A102_F01 |-1 | 
 | A102_F02 |-1 | 
 
 
## Tempo de travessia na estação 
 
 O tempo de travessia na estação fornece um nível adicional de detalhe para direções na estação, dando aos usuários um tempo estimado necessário para navegar pelas estações, resultando em melhores direções de viagem e tempos de viagem. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`traversal_time`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Conexões de caminho](#conexões de caminho) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir mostra o tempo estimado de viagem (em segundos) necessário para navegar em cada caminho. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | traversal_time | 
 |------------|----------------| 
 | PrincipalSt-001 | 3 | 
 | PrincipalSt-002 | 20 | 
 | PrincipalSt-003 | 2 | 
 | PrincipalSt-004 | 2 | 
 | PrincipalSt-005 | 4 | 
 | PrincipalSt-006 | 25 | 
 | PrincipalSt-007 | 4 | 
 | PrincipalSt-008 | 25 | 
 | PrincipalSt-009 | 2 | 
 | PrincipalSt-010 | 2 | 
 
 
## Sinais de trânsito 
 
 Os sinais de trânsito podem unir as informações exibidas nos planejadores de viagem com sinais do mundo real. Se isso for representado em um feed, os planejadores de viagem podem fornecer instruções como ’siga as placas para’. 
 
 | Arquivos incluídos | Campos incluídos | 
 |----------------------------------|------------------| 
 |[pathways.txt](../../../documentation/schedule/reference/#pathwaystxt)|`signposted_as`, `reversed_signposted_as`| 
 
 **Pré-requisitos**: 
 
 - [Recursos básicos](../base) 
 - [Conexões de caminho](#conexões de caminho) 
 
 ??? observe "Dados de amostra" 
 
<p style="font-size:16px"> 
 O exemplo a seguir especifica as informações de navegação associadas aos pathways pré-estabelecidos, refletindo o texto exibido na sinalização física da estação. 
</p> 
!!! observação "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#pathwaystxt"><b>pathways.txt</b></a><br> 
</p> 
 
 | pathway_id | signposted_as | reversed_signposted_as | 
 |------------|------------------|------------------------| 
 | PrincipalSt-001 | fazer lobby | Sair | 
 | PrincipalSt-002 | | | 
 | PrincipalSt-003 | Para plataformas | Sair | 
 | PrincipalSt-004 | | | 
 | PrincipalSt-005 | Trens no sentido oeste | Sair | 
 | PrincipalSt-006 | | | 
 | PrincipalSt-007 | Trens para o leste | Sair | 
 | PrincipalSt-008 | | | 
 | PrincipalSt-009 | Trens no sentido oeste | Para fazer lobby | 
 | PrincipalSt-010 | Trens para o leste | Para fazer lobby | 
 
 

