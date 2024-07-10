# GTFS: Tornando os dados de transporte público universalmente acessíveis## Um padrão de dados abertos para informações de passageiros em trânsito 
 
 A General Transit Feed Specification, também conhecida como GTFS, é um formato de dados padronizado que fornece uma estrutura para o transporte público agências descrevam os detalhes de seus serviços, como horários, stops, tarifas, etc. 
 
 Permite que agências de transporte público publiquem seus dados de trânsito em um formato que pode ser consumido por uma ampla variedade de aplicativos de software, mais comumente viagens planejadores. Isso significa que os usuários podem obter facilmente informações de viagem para acessar os serviços de transporte público usando seus smartphones ou dispositivos similares. 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 Hoje, GTFS é o [Padrão Aberto](https:) preferido para milhares de provedores de transporte público em todo o mundo. Algumas agências produzem elas próprias esses dados, enquanto outras empregam um fornecedor para criar e manter os dados para elas. 
 
## Suporte para dados estáticos e dinâmicos 
 
 GTFS consiste em duas partes principais: [GTFS Schedule](../../documentation/schedule/reference) e [GTFS Realtime](../../documentação/tempo real/referência). 
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 A GTFS Schedule contém informações sobre routes, horários, tarifas e detalhes geográficos de trânsito, entre muitos outros recursos, e é apresentada em arquivos de texto simples[^1]. Este formato simples permite fácil criação e manutenção sem depender de software complexo ou proprietário. 
 
 GTFS Realtime contém atualizações de viagem, posições de vehicle e alertas de serviço, usando o formato [Buffers de protocolo](https://developers.google.com/protocol-buffers/). Esta parte da GTFS funciona em conjunto com o GTFS Schedule para informar os passageiros sobre interrupções no serviço e horários de arrival atualizados. 
 
 A documentação de referência GTFS Schedule e GTFS Realtime está disponível na [seção Documentação Técnica](../../documentation/overview). 
 
 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="Reprodutor de vídeo do YouTube" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Ícones por Freepik">Ícones criados por Freepik- Flaticon</a> 
 
 [^1]: Além de arquivos de texto, o formato [GeoJSON](https:) agora também é suportado no GTFS para representar certos elementos de serviços responsivos à demanda. 
 

