# Recursos de GTFS Schedule 
 
 À medida que o formato de referência GTFS evolui para atender às necessidades atuais dos sistemas de transporte público, suas funções podem se tornar cada vez mais complexas. Os **Recursos GTFS ** têm como objetivo fornecer uma explicação clara e definitiva das funcionalidades habilitadas pelo formato de referência GTFS. Isso ajuda agências de transporte público, fornecedores, consumidores e pesquisadores a compreender os recursos da GTFS e a responder à pergunta: **O que posso fazer com a GTFS?** 
 
 Os grupos de recursos a seguir explicam a finalidade de cada recurso, bem como o arquivos e campos associados a eles, ajudando os usuários a entender quais dados são necessários para oferecer suporte a um recurso específico. 
 
## Base 
 Esses recursos essenciais formam o núcleo de um feed GTFS. São os elementos mínimos necessários para representar um serviço de trânsito. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 Comunicar detalhes sobre as agências responsáveis ​​pelo serviço de transporte público. 
 
 [:octicons-arrow-right-24: Saiba mais](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Paradas__ 
 
 Definir os locais onde um serviço de transporte público pega e deixa passageiros. 
 
 [:octicons-arrow-right-24: Saiba mais](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Rotas__ 
 
 Definir os elementos de uma rota de trânsito, como nome e tipo de serviço. 
 
 [:octicons-arrow-right-24: Saiba mais](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __Datas de serviço__ 
 
 Criar a estrutura para agendamento de viagens e isenções de serviços. 
 
 [:octicons-arrow-right-24: Saiba mais](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Viagens__ 
 § § Representam veículos de trânsito viajando ao longo de uma rota definida em horários programados. 
 
 [:octicons-arrow-right-24: Saiba mais](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Tempos de parada__ 
 
 Defina os horários de arrival e departure de cada viagem para cada parada. 
 
 [:octicons-arrow-right-24: Saiba mais](../base/#stop-times) 
 
</div> 
 
## Complementos básicos 
 Esses recursos aprimoram um conjunto de dados GTFS, melhorando a experiência do passageiro e facilitando a colaboração entre agências, fornecedores e reutilizadores de dados. Eles podem envolver a adição de novos campos a arquivos existentes ou a criação de novos arquivos. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Feed Information__ 
 
 Comunique informações importantes sobre o próprio feed. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Formas__ § § 
 Definir o caminho geográfico percorrido por um vehicle ao longo de uma viagem. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __Cores da rota__ 
 
 Representar e comunicar com precisão o esquema de cores atribuído a routes específicas. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __Bicicleta permitida__ 
 
 Comunicar se os veículos têm capacidade para acomodar bicicletas ou não. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 Comunicar a sinalização utilizada pelos veículos indicando o destino da viagem. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __Tipos de localização__ 
 
 Classifique as principais áreas das estações de transporte público, como entradas e saídas. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frequências__ § § 
 Representam serviços que operam em frequência regular ou em intervalos específicos. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __Transferências__ 
 
 Descrever as transfers permitidas entre diferentes serviços de trânsito. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Traduções__ 
 § § Comunicar informações de serviço em vários idiomas. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Atribuições__ 
 § § Comunicar quem esteve envolvido na criação do conjunto de dados. 
 
 [:octicons-arrow-right-24: Saiba mais](../base_add-ons/# attributions) 
 
</div> 
 
 
## Acessibilidade 
 Os recursos de acessibilidade fornecem informações essenciais para pessoas com deficiência acessarem o serviço. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Paradas Acessibilidade para cadeiras de rodas__ 
 
 Indique se o embarque para cadeiras de rodas é possível a partir de um local. 
 
 [:octicons-arrow-right-24: Saiba mais](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Trips Cadeira de rodas Acessibilidade__ 
 
 Indique se um vehicle pode acomodar passageiros em cadeiras de rodas. 
 
 [:octicons-arrow-right-24: Saiba mais](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Texto- to-Speech__ 
 
 Fornece as entradas necessárias para converter o texto dos nomes das paradas em áudio. 
 
 [:octicons-arrow-right-24: Saiba mais](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Tarifas 
 O GTFS pode modelar diversas estruturas tarifárias, como tarifas baseadas em zona, distância ou horário do dia. Informa os passageiros sobre preços de viagens e formas de pagamento. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Produtos tarifários__ 
 
 Definir a lista de passagens ou tipos de tarifas disponíveis aos usuários. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ 
 
 Definir os meios que podem ser utilizados para armazenar e/ou validar um produto tarifário. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __Tarifas baseadas em rota__ 
 
 Descrever as regras utilizadas para aplicar diferentes tarifas para grupos específicos de routes. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Tempo- Tarifas Baseadas__ 
 
 Descrever tarifas diferenciadas por horário do dia ou dia da semana. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone- Tarifas Baseadas__ 
 
 Descrever tarifas diferenciadas ao viajar de uma área para outra. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Fares Transfers__ 
 
 Definir taxas aplicáveis ​​na transferência de um trecho da viagem para outro. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 Recurso legado que permite uma representação mais simples das informações tarifárias. 
 
 [:octicons-arrow-right-24: Saiba mais](../fares/#fares-v1) 
 
</div> 
 
 
## Caminhos 
 
 Os recursos de caminhos permitem modelar grandes estações de transporte público, para que os passageiros sejam guiados desde as entradas até as áreas de embarque. Eles fornecem detalhes do caminho, tempos de navegação estimados e sistemas de orientação. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Conexões de caminhos__ 
 
 Modele caminhos conectando pontos relevantes dentro de uma estação de transporte público. 
 
 [:octicons-arrow-right-24: Saiba mais](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __Detalhes do caminho__ 
 
 Fornecer detalhes adicionais sobre as características físicas de uma via. 
 
 [:octicons-arrow-right-24: Saiba mais](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Levels__ 
 § § Descrever e listar todos os diferentes níveis dentro de uma estação de transporte público. 
 
 [:octicons-arrow-right-24: Saiba mais](../pathways/#níveis) 
 
 - :material-subway-variant:{ .lg.middle } __Tempo de travessia na estação__ § § 
 Comunicar o tempo estimado para percorrer caminhos dentro de uma estação de transporte público. 
 
 [:octicons-arrow-right-24: Saiba mais](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __Sinais de Caminho__ 
 
 Comunicam a sinalização na estação associada a um caminho. 
 
 [:octicons-arrow-right-24: Saiba mais](../pathways/#pathway-signs) 
 
</div> 
 
## Serviços flexíveis 
 Serviços flexíveis, ou serviços que respondem à demanda, que não seguem horários regulares ou routes fixas. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Paradas Contínuas__ 
 
 Indica se um usuário pode ser pego e/ou deixado entre as stops. 
 
 [:octicons-arrow-right-24: Saiba mais](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __Regras de reserva__ 
 
 Indicar se os usuários podem reservar uma viagem em um serviço que responda à demanda. 
 
 [:octicons-arrow-right-24: Saiba mais](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __Rotas predefinidas com desvio__ 
 
 Veículos que podem desviar-se brevemente de uma rota para embarque ou desembarque. 
 
 [:octicons-arrow-right-24: Saiba mais](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __Serviços responsivos à demanda baseados em zona__ 
 
 Serviços que permitem coleta/entrega em qualquer local dentro de uma área específica. 
 
 [:octicons-arrow-right-24: Saiba mais](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.meio } __Paradas fixas exigem serviços responsivos__ 
 
 Serviços que permitem embarque/desembarque em qualquer local dentro de um grupo de stops. 
 
 [:octicons-arrow-right-24: Saiba mais](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

