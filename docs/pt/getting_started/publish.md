# Disponibilizar publicamente seu feed GTFS## Benefícios de compartilhar seu GTFS 
 
 Os dados GTFS podem ser utilizados de várias maneiras, e compartilhar publicamente os dados GTFS de sua agência oferece muitos benefícios para seus passageiros e para sua agency como um todo. Isso inclui: 
 
 - Integrar seu feed em aplicativos de planejamento de viagens móveis e baseados na web, permitindo que os passageiros planejem viagens em seu sistema- Enviar seu feed para um agregador GTFS, como o Mobility Database, que fornece uma visão mais ampla público e mais visibilidade para sua agency- Utilização de ferramentas que permitem a visualização e análise de dados GTFS em Sistemas de Informações Geográficas (GIS) e outros programas de análise baseados em mapas### Aplicativos de planejamento de viagens 
 
 Quando os dados GTFS da sua agência são compartilhados publicamente e podem ser utilizados por vários aplicativos de planejamento de viagens, além do Google Maps. Isso pode incluir outros aplicativos de navegação, como Bing Maps, Apple Maps, bem como plataformas específicas de transporte público, como Transit, Moovit, Transportr e Citymapper. Além disso, o acesso a dados de feed abertos permite que os desenvolvedores criem aplicativos voltados para regiões específicas ou que possam ter recursos que t estão incluídos nos planejadores de viagem padrão, como: Vamos (condados de San Joaquin e Stanislaus, Califórnia), MetroHero (Washington DC área), Entur (Noruega) e muito mais. 
 
### Agregadores de feeds 
 
 Compartilhar seus dados GTFS também permite que eles sejam indexados por plataformas de agregação de feeds GTFS, que podem incluir diretórios de feeds GTFS em nível estadual ou regional, bem como agregadores de feeds internacionais, como o [Mobility Database](https://database.mobilitydata.org/) e [Transitland](https://www.transit.land/) (veja mais agregadores de feed [aqui](../../resources/dados)). Ser indexado em um agregador de feeds aumenta a visibilidade da sua agência e permite que desenvolvedores, pesquisadores e outras partes interessadas acessem facilmente os dados da sua agência para diversos fins, incluindo o desenvolvimento de novos aplicativos. 
 
### Integração com GIS, análise e outras plataformas e ferramentas 
 
 Os dados GTFS também podem ser importados e usados ​​em uma variedade de plataformas de análise geoespacial. Programas de Sistemas de Informação Geográfica (GIS), como o ArcGIS da Esri, bem como o QGIS de código aberto, têm seus próprios plug-ins e extensões que podem import e visualizar dados de parada e rota GTFS. 
 
 - A Esri possui uma [ampla variedade de ferramentas e plugins](https://github.com/Esri/public-transit-tools) que usam dados GTFS, incluindo a visualização de dados de cronograma- No QGIS, [GTFS-GO](https://plugins.qgis.org/plugins/GTFS-GO-master/) e [GTFS Loader](https://plugins.qgis.org/plugins/GTFS_Loader/) permitem visualizar routes + para dentro da plataforma- [Ferramentas de análise adicionais](../../resources/agency-tools) 
 
 Outras plataformas permitem visualizar e analisar dados GTFS de maneiras exclusivas: 
 
 - [Transmitir](https://conveyal.com/) é um programa de código aberto que permite aos usuários import dados GTFS para visualizar programações, routes e padrões, além de analisar os impactos de possíveis alterações no serviço. Os usuários também podem import e trabalhar com dados demográficos para realizar análises sobre, por exemplo, como diferentes routes ou horários afetariam o acesso a empregos em uma determinada área urbana. 
 - [GTFS para HTML](https://gtfstohtml.com/) é uma ferramenta de código aberto que permite a conversão de dados de agendamento GTFS em horários HTML. Permite que as agências publiquem e atualizem automaticamente suas programações em seu site em um formato que também pode ser lido por leitores de tela, tornando os dados acessíveis a pessoas com deficiência visual. 
 
## Compartilhando seus dados: dicas e práticas recomendadas### Crie e mantenha um link de busca permanente 
 
 Um link de busca é um URL permanente no qual os arquivos de GTFS Schedule da sua agência são armazenados. Normalmente, ele é hospedado no site da sua agência ou pelo seu fornecedor, se você contratar um para produção de GTFS. É assim que aplicativos de planejamento de viagens como o Google Maps acessam seus dados. O ideal é que seus arquivos de GTFS Schedule possam ser baixados diretamente deste URL, sem a necessidade de login. No entanto, se isso não for viável devido a restrições de licenciamento, sua agency poderá controlar o acesso aos dados usando e emitindo chaves de API aos usuários dos dados. 
 
### URL e nomes de arquivos 
 
 Links de busca consistentes e nomes de arquivos GTFS são cruciais para garantir o acesso aos dados do seu feed. Se sua agency não usar URLs e nomes de arquivos consistentes para seus dados, isso significa que aplicativos de planejamento de viagens, agregadores de feeds e outros usuários não obterão os dados mais precisos e atualizados, o que cause problemas no longo prazo. 
 
 Depois de definir um URL para seu link de busca permanente, NÃO MUDE-O. Isso significa que o nome da URL deve permanecer consistente, mesmo que os próprios arquivos sejam atualizados. Dessa forma, mantenha seus URLs tão simples e genéricos quanto possível e evite usar URLs que contenham datas ou números de versão. 
 
 - **BOM:** http://www.bart.gov/dev/schedules/google_transit.zip, 
 - **EVITAR:** http://www.bart.gov/dev/Schedules/google_transit_Fall_2021.zip 
 
 Da mesma forma, mantenha consistente o nome da pasta ZIP que contém os arquivos de GTFS Schedule, mesmo se você fizer atualizações no próprio feed. Por exemplo, ao atualizar um feed, você não deve adicionar nenhum tipo de date ou número de versão ao nome da pasta ZIP. Se desejar incluir dados sobre a versão do feed ou as datas de início e término do feed no feed, você poderá incluí-los no arquivo feed_info.txt. 
 
 - **BOM:** “YourAgency_gtfs.zip”, “google_transit.zip”, “gtfs.zip”, 
 - **EVITAR:** “YourAgency_gtfs_092921.zip”, “YourAgency_Fall2021.zip” § § 
 
### Configuração e integridade do arquivo 
 
 Sua GTFS é um arquivo zip contendo vários arquivos de texto interconectados (.txt). Para garantir que o formato esteja correto, faça sempre o seguinte: 
 
 1. Ao abrir um arquivo de texto, certifique-se de manter os valores como texto. Existem muitos campos em uma GTFS que aplicativos como o Excel irão ler incorretamente ou abreviar. 
 2. Os arquivos são delimitados por vírgulas e não por tabulações. Isso significa que cada arquivo contém registros em linhas e os diferentes campos são separados por vírgulas. 
 3. Linhas ou colunas extras cause erros no consumo das aplicações, portanto certifique-se de que não haja linhas ou colunas vazias ao salvar o arquivo. 
 4. Não descarte nenhum dos arquivos da sua GTFS- eles funcionam juntos e quaisquer arquivos ausentes podem cause erros no consumo de aplicativos. 
 5. Ao compactar novamente os arquivos, certifique-se de compactar os arquivos e não a pasta que os contém. Você pode ter certeza de que fez isso corretamente descompactando o arquivo e vendo imediatamente os arquivos nessa pasta, e não em outra pasta que contém os arquivos. 
 
 
### Considerações adicionais 
 
 Se várias agências compartilham a mesma parada com nomes ou códigos diferentes, aplicativos como o Google Maps podem precisar escolher um. Para evitar confusão, coordene com outras agências para chegar a um acordo sobre os nomes e códigos. Isso minimiza conflitos entre diferentes conjuntos de dados GTFS. 
 
 Caso você tenha vários conjuntos de dados GTFS disponíveis, geralmente o resultado de um produzido para aplicativos públicos, como o Transit App, e outro produzido para sistemas operacionais internos de CAD/AVL, talvez seja necessário decidir qual deles será ser a GTFS publicada. É recomendável que você opte por promover o feed que contém mais informações voltadas para os passageiros. Sempre que possível, procure combinar seus conjuntos de dados GTFS (mesmos IDs para coisas como stops e viagens) para que os internos não entrem em conflito com os públicos e seja possível integrar outros feeds como GTFS-RT. 
 

