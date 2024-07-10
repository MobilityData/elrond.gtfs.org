# Criando um conjunto de dados GTFS## Visão geral de um feed GTFS 
 Todos os feeds GTFS começam com um conjunto de dados no formato de referência GTFS, que é uma série de arquivos CSV salvos com uma extensão de arquivo.txt [^1]. Em sua implementação mais básica, um conjunto de dados GTFS normalmente começa com sete arquivos base, combinados em um arquivo.zip hospedado em uma URL estável e pública: este é o feed GTFS. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_001.png"> 
 
 Cada arquivo consiste em uma lista de múltiplos registros (linhas de dados) com diversos campos de informação. Por exemplo, cada linha listada em [routes.txt](../../documentation/schedule/reference/#routestxt) representa uma rota de transporte público e seus campos descrevem vários elementos dessa rota, como nome, descrição, operação agency, etc. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_002.png"> 
 
 Os arquivos base para um conjunto de dados GTFS podem ser descritos da seguinte forma: Um conjunto de dados de cronograma GTFS tem uma ou mais routes ([routes.txt](../../documentation/schedule/reference/#routestxt)), cada rota tem uma ou mais viagens ([trips.txt](../../documentation/schedule/reference/#tripstxt)), cada viagem visita uma série de stops ([stops.txt](../../documentation/schedule/reference/#stopstxt)) em horários especificados ([stop_times.txt](../../documentation/schedule/reference/#stop_timestxt)). Os horários de viagens e paradas contêm apenas informações sobre a hora do dia; o calendário é usado para determinar em quais dias uma determinada viagem será executada ([calendar.txt](../../documentation/schedule/reference/#calendartxt) e [calendar_dates.txt](../../documentation/agendamento/referência/#calendar_datestxt)). Além disso, diversas agências ([agency.txt](../../documentation/schedule/reference/#agencytxt)) podem operar diversas routes. Esses arquivos são vinculados entre si por campos com referências cruzadas entre eles. 
 
<img class="center" width="560" height="100%" src="../../../assets/create_003.png"> 
 
 Depois que esses arquivos forem configurados para criar um conjunto de dados GTFS básico, arquivos adicionais (optional) podem ser adicionados para permitir outras funcionalidades ou necessidades específicas entre agências de trânsito e fornecedores. Alguns exemplos desses arquivos incluem: 
 
 - [shapes.txt](../../documentation/schedule/reference/#shapestxt) que permite representar graficamente o caminho de uma viagem, 
 - [pathways.txt](../../documentation/schedule/reference/#pathwaystxt) que fornece informações que permitem gerar rotas para ajudar os usuários a navegar nas estações, 
 - [frequencies.txt](../../documentation/schedule/reference/#frequenciestxt) que fornece uma maneira alternativa de especificar horários de parada. 
 
 Para obter mais informações sobre todas as funcionalidades do GTFS que podem ser habilitadas, consulte a seção [“O que o GTFS pode fazer?”](../features/overview/). 
 
 Um conjunto de dados de GTFS Schedule pode ser complementado com informações em tempo real, como posições de vehicle e atualizações de serviços. Para fazer isso, um feed GTFS Realtime precisa ser criado separadamente do conjunto de dados de GTFS Schedule existente. 
 
 Um feed GTFS Realtime consiste em um arquivo binário regular servido via HTTP e atualizado com frequência. Qualquer tipo de servidor web pode hospedar e servir o arquivo. O formato de troca de dados GTFS Realtime é baseado em [Buffers de protocolo](https:), um mecanismo neutro em linguagem e plataforma para serializar dados estruturados. O GTFS Realtime pode fornecer três tipos de informações: atualizações de viagem, alertas de serviço e posições de veículos, que podem ser combinadas dependendo das informações de serviço que precisam ser comunicadas. 
 
 Como o GTFS Realtime permite apresentar o status real de uma frota, o feed precisa ser atualizado regularmente- de preferência sempre que novos dados vierem do sistema de Localização Automática de Veículos do serviço. Combinados, o conjunto de dados GTFS Schedule e um feed GTFS Realtime permitem que os aplicativos de consumo forneçam informações precisas e atualizadas aos passageiros. Para mais informações consulte a Documentação Técnica. 
 
## Produzindo seu primeiro feed GTFS ? 
 
 Se você é uma agency que deseja produzir seu primeiro feed GTFS, a primeira coisa que você precisa fazer é ler a documentação existente. 
 
 Comece explorando os recursos da GTFS na seção ["O que a GTFS pode fazer?"](../features/overview) e determine os diferentes recursos do seu serviço de transporte público que você deseja representar usando o formato GTFS. Para uma exploração mais aprofundada, a documentação de referência oficial para [GTFS Schedule](../../documentation/schedule/reference) e [GTFS Realtime](../../documentation/realtime/reference) oferece informações detalhadas orientação sobre como modelar esses recursos e garantir a conformidade. 
 
 Em seguida, colete todos os dados necessários do seu sistema. Isso inclui informações de todas as stops, routes, horários, tarifas, etc., já que muitos desses detalhes serão as entradas que preencherão o conjunto de dados GTFS. 
 
 Dependendo do tamanho e da complexidade do seu sistema, você tem a opção de criar os dados internamente ou contratar um fornecedor externo de GTFS para transformar os dados no formato GTFS. 
 
 Em alguns casos, pequenas agências com poucas routes criam elas próprias os dados usando software comumente disponível, como planilhas e editores de texto. 
 
 Ao lidar com um escopo de sistema mais amplo, a maioria das agências adquire software de gerenciamento GTFS especializado de fornecedores especializados, mas algumas podem optar por desenvolver suas próprias ferramentas internas. Finalmente, quando as características do sistema se revelam um desafio para as agências escreverem conjuntos de dados por conta própria, a produção de GTFS pode ser totalmente terceirizada para empresas especializadas na produção de dados GTFS. 
 
 <a href="https://www.flaticon.com/authors/freepik" title="Ícones por Freepik">Ícones criados por Freepik- Flaticon</a> 
 
 [^1]: Além de arquivos de texto, o formato [GeoJSON](https:) agora também é suportado no GTFS para representar certos elementos de serviços responsivos à demanda. 
 

