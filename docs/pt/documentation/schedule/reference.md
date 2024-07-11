## Referência General Transit Feed Specification 
 
 **Revisado em 22 de maio de 2024. Consulte [Histórico de revisões](../change_history/revision_history) para obter mais detalhes.** 
 
 Este documento define o formato e a estrutura de os arquivos que compõem um conjunto de dados GTFS. 
 
## Índice 
 
 1. [Convenções de documentos](#document-conventions) 
 2. [Arquivos de conjunto de dados](#dataset-files) 
 3. [Requisitos de arquivo](#file-requisitos) 
 4. [Publicação de conjunto de dados e práticas gerais](#dataset-publishing-general-practices) 
 5. [Definições de campo](#field-definitions) 
 - [agency.txt](#agênciatxt) 
 - [stops.txt](#stopstxt) 
 - [routes.txt](#routestxt) 
 - [trips.txt](#tripstxt) 
 - [paradas\_times.txt](#stop_timestxt) 
 - [calendar.txt](#calendartxt) 
 - [calendar\_dates.txt](#calendar_datestxt) 
 - [fare\_attributes.txt](#fare_attributestxt) 
 - [fare\_rules.txt](#fare_rulestxt) 
 - [prazos.txt](#timeframestxt) 
 - [fare\_media.txt](#fare_mediatxt) 
 - [fare\_products.txt](#fare_productstxt) 
 - [fare\ _leg\_rules.txt](#fare_leg_rulestxt) 
 - [fare\_transfer\_rules.txt](#fare_transfer_rulestxt) 
 - [areas.txt](#areastxt) 
 - [stop_areas.txt](#stop_areastxt) 
 - [redes.txt](#networkstxt) 
 - [route_networks.txt](#route_networkstxt) 
 - [shapes.txt](#shapestxt) 
 - [frequencies.txt](#frequênciastxt) 
 - [transfers.txt](#transferstxt) 
 - [pathways.txt](#pathwaystxt) 
 - [levels.txt](#levelstxt) 
 - [location_groups.txt](#location_groupstxt) 
 - [location_group_stops.txt](#location_group_stopstxt) 
 - [locations.geojson](#locationsgeojson) 
 - [booking_rules.txt](#booking_rulestxt) 
 - [translations.txt](#translationstxt) 
 - [feed\ _info.txt](#feed_infotxt) 
 - [attributions.txt](#attributionstxt) 
 
## Convenções de documentos 
 As palavras-chave "DEVE", "NÃO DEVE", "OBRIGATÓRIO", "DEVE", “NÃO DEVE”, “DEVE”, “NÃO DEVE”, “RECOMENDADO”, “PODE” e “OPCIONAL” neste documento devem ser interpretados conforme descrito em [RFC 2119](https://tools.ietf.org/html/rfc2119). 
 
 
### Definições de termos 
 
 Esta seção define os termos usados ​​ao longo deste documento. 
 
 * **Dataset** - Um conjunto completo de arquivos definidos por esta referência de especificação. A alteração do conjunto de dados cria uma nova versão do conjunto de dados. Os conjuntos de dados devem ser publicados em um URL público e permanente, incluindo o nome do arquivo zip. (por exemplo, https: agency). 
 * **Registro** - Uma estrutura de dados básica composta por vários valores de campo diferentes que descrevem uma única entity (por exemplo, agency de trânsito, parada, rota, etc.). Representado, em uma tabela, como uma linha. 
 * **Campo** - Uma propriedade de um objeto ou entity. Representado, em uma tabela, como uma coluna. O campo existe se adicionado em um arquivo como header. Pode ou não ter valores de campo definidos. 
 * **Valor do campo** - Uma entrada individual em um campo. Representado, em uma tabela, como uma única célula. 
 * **Dia de serviço** - Um dia de serviço é um período de tempo usado para indicar a programação da rota. A definição exata de dia de serviço varia de agency para agency, mas os dias de serviço muitas vezes não correspondem aos dias corridos. Um dia de serviço pode exceder as 24h00 se o serviço começar num dia e terminar no dia seguinte. Por exemplo, o serviço que funciona das 08:00:00 de sexta-feira às 02:00:00 de sábado pode ser indicado como sendo executado das 08:00:00 às 26:00:00 em um único dia de serviço. 
 * **Campo de conversão de texto em fala** - O campo deve conter as mesmas informações que seu campo pai (ao qual recorrerá se estiver vazio). Destina-se a ser lido como texto para fala, portanto, a abreviatura deve ser removida ("St" deve ser lida como "Rua" ou "Santa"; "Isabel I" deve ser "Isabel a primeira") ou mantido para ser lido como ("Aeroporto JFK" é abreviado). 
 * **Leg** - Viagem em que um passageiro embarca e desembarca entre dois locais subsequentes ao longo de uma viagem. 
 * **Viagem** - Viagem geral da origem ao destino, incluindo todos os trechos e transfers intermediárias. 
 * **Sub-viagem** - Dois ou mais trechos que compõem um subconjunto de uma viagem. 
 * **Produto tarifário** - Produtos tarifários compráveis ​​que podem ser usados ​​para pagar ou validar viagens. 
 
### Presença 
 Condições de presença aplicáveis ​​a campos e arquivos: 
 
 * **Obrigatório** - O campo ou arquivo deve estar incluído no conjunto de dados e conter um valor válido para cada registro. 
 * **Opcional** - O campo ou arquivo pode ser omitido do conjunto de dados. 
 * **Condicionalmente Obrigatório** - O campo ou arquivo deve ser incluído nas condições descritas na descrição do campo ou arquivo. 
 * **Condicionalmente Proibido** - O campo ou arquivo não deve ser incluído nas condições descritas na descrição do campo ou arquivo. 
 * **Recomendado** - O campo ou arquivo pode ser omitido do conjunto de dados, mas é uma prática recomendada incluí-lo. Antes de omitir este campo ou arquivo, as melhores práticas devem ser cuidadosamente avaliadas e todas as implicações da omissão devem ser compreendidas. 
 
### Tipos de campo- **Cor** - Uma cor codificada como um número hexadecimal de seis dígitos. Consulte [https://htmlcolorcodes.com](https://htmlcolorcodes.com) para gerar um valor válido (o "#" inicial não deve ser incluído).<br> *Exemplo: `FFFFFF` para branco, `000000` para preto ou `0039A6` para as linhas A, C, E em NYMTA.* 
 - **Código de moeda** - Um código de currency alfabético ISO 4217. Para obter a lista da currency atual, consulte [https://en.wikipedia.org/wiki/ISO_4217#Active\_codes](https:( https://en.wikipedia.org/wiki/ISO_4217#Active_codes).<br> *Exemplo: `CAD` para dólares canadenses, `EUR` para euros ou `JPY` para ienes japoneses.* 
 - **amount da moeda ** - Um valor decimal indicando o amount da currency. O número de casas decimais é especificado por [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217#Active_codes) para o código de moeda que o acompanha. Todos os cálculos financeiros devem ser processados ​​como decimal, currency ou outro tipo equivalente adequado para cálculos financeiros, dependendo da linguagem de programação usada para consumir os dados. O processamento de valores currency como float é desencorajado devido a ganhos ou perdas de dinheiro durante os cálculos. 
 - **Data** - Dia de atendimento no formato AAAAMMDD. Como o horário de um dia de serviço pode ser superior às 24h00, um dia de serviço pode conter informações para o(s) dia(s) subsequente(s).<br> *Exemplo: `20180913` para 13 de setembro de 2018.* 
 - **Email** - Um endereço de email.<br> *Exemplo: `example@example.com`* 
 - **Enum** - Uma opção de um conjunto de constantes predefinidas definidas na coluna "Descrição".<br> *Exemplo: O campo `route_type` contém um `0` para bonde, um `1` para metrô...* 
 - **ID** - Um valor de campo de ID é um ID interno, não destinado a ser mostrado a pilotos e é uma sequência de quaisquer caracteres UTF-8. Recomenda-se usar apenas caracteres ASCII imprimíveis. Um ID é rotulado como "ID exclusivo" quando deve ser exclusivo em um arquivo. Os IDs definidos em um arquivo.txt geralmente são referenciados em outro arquivo.txt. IDs que fazem referência a um ID em outra tabela são rotulados como "ID estrangeiro".<br> *Exemplo: O campo `stop_id` em [stops.txt](#stopstxt) é um "ID exclusivo". O campo `parent_station` em [stops.txt](#stopstxt) é um "ID estrangeiro referenciando `stops.stop_id`".* 
 - **Código de idioma** - Um código de idioma IETF BCP 47. Para obter uma introdução ao IETF BCP 47, consulte [http://www.rfc-editor.org/rfc/bcp/bcp47 .txt](http: .txt) e [http://www.w3.org/International/articles/language-tags/](http ://www.w3.org/International/articles/language-tags/).<br> *Exemplo: `en` para inglês, `en-US` para inglês americano ou `de` para alemão.* 
 - **Latitude** - latitude WGS84 em graus decimais. O valor deve ser maior ou igual a-90,0 e menor ou igual a 90,0. *<br> Exemplo: `41.890169` para o Coliseu de Roma.* 
 - **Longitude** - longitude WGS84 em graus decimais. O valor deve ser maior ou igual a-180,0 e menor ou igual a 180,0.<br> *Exemplo: `12.492269` para o Coliseu de Roma.* 
 - **Float** - Um número de ponto flutuante. 
 - **Inteiro** - Um número inteiro. 
 - **Phone number** - Um número de telefone. 
 - **Hora** - Hora no formato HH:MM:SS (H:MM:SS também é aceito). O horário é medido a partir de "meio-dia menos 12h" do dia de serviço (efetivamente meia-noite, exceto nos dias em que ocorrem mudanças no horário de verão). Para horários que ocorram após a meia-noite do dia de atendimento, insira o horário como um valor maior que 24:00:00 em HH:MM:SS.<br> *Exemplo: `14:30:00` para 14h30 ou `25:35:00` para 1h35 do dia seguinte.* 
 - **Text** - Uma string de caracteres UTF-8, que destina-se a ser exibido e que deve, portanto, ser legível por humanos. 
 - **Fuso horário** - Fuso horário TZ de [https://www.iana.org/time-zones](https:( https://www.iana.org/time-zones). Os nomes dos fusos horários nunca contêm o caractere de espaço, mas podem conter um sublinhado. Consulte [http://en.wikipedia.org/wiki/List\_of\_tz\_zones](http://en.wikipedia.org/wiki/List\_of\_tz\_zones) para obter uma lista de valores válidos .<br> *Exemplo: `Asia/Tokyo`, `America/Los_Angeles` ou `Africa/Cairo`.* 
 - **URL** - Um URL totalmente qualificado que inclui http://ou https://, e qualquer URL especial caracteres no URL devem ter escape correto. Consulte o seguinte [http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html](http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html) para uma descrição de como criar valores de URL totalmente qualificados. 
 
### Sinais de Campo 
 Sinais aplicáveis ​​aos tipos de campo Float ou Inteiro: 
 
 * **Não negativo** - Maior ou igual a 0. 
 * **Diferente de zero** - Diferente de 0. 
 * **Positivo** - Maior que 0. 
 
 _Exemplo: **float não negativo ** - Um número de ponto flutuante maior ou igual a 0._ 
 
### Atributos do conjunto de dados 
 A **chave primária** de um conjunto de dados é o campo ou combinação de campos que identificam exclusivamente uma linha. `Primary key (*)` é usada quando todos os campos fornecidos para um arquivo são usados ​​para identificar exclusivamente uma linha. `Primary key (none)` significa que o arquivo permite apenas uma linha. 
 
 _Exemplo: os campos `trip_id` e `stop_sequence` formam a chave primária de [stop_times.txt](#stop_timestxt)._ 
 
## Arquivos de conjunto de dados 
 
 Esta especificação define os seguintes arquivos: 
 
 | Nome do arquivo | Presença | Descrição | 
 |------|------|------| 
 | [agency.txt](#agênciatxt) | **Obrigatório** | Agências de transporte público com serviços representados neste conjunto de dados. | 
 | [stops.txt](#paradastxt) | **Obrigatório** | Paradas onde os veículos pegam ou deixam os passageiros. Também define estações e entradas de estações. | 
 | [routes.txt](#routestxt) | **Obrigatório** | routes de trânsito. Uma rota é um grupo de viagens exibidas aos passageiros como um único serviço. | 
 | [trips.txt](#tripstxt) | **Obrigatório** | Viagens para cada rota. Uma viagem é uma sequência de duas ou mais stops que ocorrem durante um período específico. | 
 | [stop_times.txt](#stop_timestxt) | **Obrigatório** | Horários em que um vehicle chega e sai das stops de cada viagem. | 
 | [calendar.txt](#calendartxt) | **Condicionalmente Obrigatório** | Datas de serviço especificadas usando uma programação semanal com datas de início e término.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** a menos que todas as datas de serviço estejam definidas em [calendar_dates.txt](#calendar_datestxt).<br> - Opcional caso contrário. | 
 | [calendar_dates.txt](#calendar_datestxt) | **Condicionalmente Obrigatório** | Exceções para os serviços definidos em [calendar.txt](#calendartxt).<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se [calendar.txt](#calendartxt) for omitido. Nesse caso [calendar_dates.txt](#calendar_datestxt) deve conter todas as datas de serviço.<br> - Opcional caso contrário. | 
 | [fare_attributes.txt](#fare_attributestxt) | Opcional | Informações sobre tarifas para routes de uma agência de transporte público. | 
 | [fare_rules.txt](#fare_rulestxt) | Opcional | Regras para aplicação de tarifas de itinerários. | 
 | [.txt](#timeframestxt) | Opcional | Períodos de data e hora a serem usados ​​nas regras tarifárias para tarifas que dependem de fatores de date e hora. | 
 | [.txt](#fare_mediatxt) | Opcional | Descrever os meios tarifários que podem ser empregados para utilizar produtos tarifários.<br><br> O arquivo [fare_media.txt](#fare_mediatxt) descreve conceitos que não são representados em [fare_attributes.txt](#fare_attributestxt) e [fare_rules.txt](#fare_rulestxt). Como tal, o uso de [fare_media.txt](#fare_mediatxt) é totalmente separado dos arquivos [fare_attributes.txt](#fare_attributestxt) e [fare_rules.txt](#fare_rulestxt). | 
 | [fare_products.txt](#fare_productstxt) | Opcional | Descrever os diferentes tipos de bilhetes ou tarifas que podem ser adquiridos pelos passageiros.<br><br> O arquivo [fare_products.txt](#fare_productstxt) descreve produtos tarifários que não estão representados em [fare_attributes.txt](#fare_attributestxt) e [fare_rules.txt](#fare_rulestxt). Como tal, o uso de [fare_products.txt](#fare_productstxt) é totalmente separado dos arquivos [fare_attributes.txt](#fare_attributestxt) e [fare_rules.txt](#fare_rulestxt). | 
 | [fare_leg_rules.txt](#fare_leg_rulestxt) | Opcional | Regras tarifárias para trechos individuais da viagem.<br><br> O arquivo [fare_leg_rules.txt](#fare_leg_rulestxt) fornece um método mais detalhado para modelar estruturas tarifárias. Como tal, o uso de [fare_leg_rules.txt](#fare_leg_rulestxt) é totalmente separado dos arquivos [fare_attributes.txt](#fare_attributestxt) e [fare_rules.txt](#fare_rulestxt). | 
 | [fare_transfer_rules.txt](#fare_transfer_rulestxt) | Opcional | Regras tarifárias para transfers entre trechos de viagem.<br><br> Junto com [fare_leg_rules.txt](#fare_leg_rulestxt), o arquivo [fare_transfer_rules.txt](#fare_transfer_rulestxt) fornece um método mais detalhado para modelar estruturas tarifárias. Como tal, o uso de [fare_transfer_rules.txt](#fare_transfer_rulestxt) é totalmente separado dos arquivos [fare_attributes.txt](#fare_attributestxt) e [fare_rules.txt](#fare_rulestxt). | 
 | [areas.txt](#áreastxt) | Opcional | Agrupamento de áreas de locais. | 
 | [stop_areas.txt](#stop_areastxt) | Opcional | Regras para atribuir stops às áreas. | 
 | [redes.txt](#redestxt) | **Condicionalmente Proibido** | Agrupamento de routes em rede.<br><br> Condicionalmente Proibido:<br> - **Proibido** se `network_id` existir em [routes.txt](#routestxt).<br> - Opcional caso contrário. | 
 | [.txt](#route_networkstxt) | **Condicionalmente Proibido** | Regras para atribuir routes às redes.<br><br> Condicionalmente Proibido:<br> - **Proibido** se `network_id` existir em [routes.txt](#routestxt).<br> - Opcional caso contrário. | 
 | [shapes.txt](#formastxt) | Opcional | Regras para mapear caminhos de deslocamento de vehicle, às vezes chamados de alinhamentos de rotas. | 
 | [frequencies.txt](#frequênciastxt) | Opcional | Intervalo (tempo entre viagens) para serviço baseado em intervalo ou uma representação compactada de serviço com horário fixo. | 
 | [transfers.txt](#transferstxt) | Opcional | Regras para fazer conexões em pontos de transferência entre routes. | 
 | [pathways.txt](#caminhostxt) | Opcional | Caminhos que ligam locais dentro das estações. | 
 | [levels.txt](#níveistxt) | **Condicionalmente Obrigatório** | Níveis dentro das estações.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** ao descrever pathways com elevadores (`pathway_mode=5`).<br> - Opcional caso contrário. | 
 | [.txt](#location_groupstxt) | Opcional | Um grupo de stops que juntas indicam locais onde um passageiro pode solicitar embarque ou desembarque. | 
 | [.txt](#location_group_stopstxt) | Opcional | Regras para atribuir stops a grupos de locais. | 
 | [locations.geojson](#locaisgeojson) | Opcional | Zonas para solicitações de embarque ou desembarque de passageiros por serviços sob demanda, representadas como polígonos GeoJSON. | 
 | [booking_rules.txt](#booking_rulestxt) | Opcional | Informações de reserva para serviços solicitados pelo passageiro. | 
 | [translations.txt](#traduçõestxt) | Opcional | Traduções de valores de conjuntos de dados voltados para o cliente. | 
 | [feed_info.txt](#feed_infotxt) | Opcional | Metadados do conjunto de dados, incluindo informações sobre editor, versão e expiração. | 
 | [attributions.txt](#atribuiçãostxt) | Opcional | attributions do conjunto de dados. | 
 
## Requisitos de arquivo 
 
 Os seguintes requisitos se aplicam ao formato e ao conteúdo dos arquivos do conjunto de dados: 
 
 * Todos os arquivos devem ser salvos como texto delimitado por vírgulas. 
 * A primeira linha de cada arquivo deve conter nomes de campos. Cada subseção da seção [Definições de campo](#field-definitions) corresponde a um dos arquivos em um conjunto de dados GTFS e lista os nomes de campos que podem ser usados ​​nesse arquivo. 
 * Todos os nomes de arquivos e campos diferenciam maiúsculas de minúsculas. 
 * Os valores dos campos não devem conter tabulações, retornos de carro ou novas linhas. 
 * Os valores dos campos que contêm aspas ou vírgulas devem ser colocados entre aspas. Além disso, cada aspa no valor do campo deve ser precedida por aspas. Isso é consistente com a maneira como o Microsoft Excel gera arquivos delimitados por vírgula (CSV). Para obter mais informações sobre o formato de arquivo CSV, consulte [http://tools.ietf.org/html/rfc4180](http:). 
 O exemplo a seguir demonstra como um valor de campo apareceria em um arquivo delimitado por vírgula: 
 * **Valor do campo original:** `Contains "quotes", commas and text` 
 * **Valor do campo no arquivo CSV :** `"Contains ""quotes"", commas and text"` 
 * Os valores dos campos não devem conter tags HTML, comentários ou sequências de escape. 
 * Espaços extras entre campos ou nomes de campos devem ser removidos. Muitos analisadores consideram os espaços como parte do valor, o que pode cause erros. 
 * Cada linha deve terminar com um caractere de quebra de linha CRLF ou LF. 
 * Os arquivos devem ser codificados em UTF-8 para suportar todos os caracteres Unicode. Arquivos que incluem o caractere BOM (marca de ordem de byte) Unicode são aceitáveis. Consulte [http://unicode.org/faq/utf_bom.html#BOM](http:) para obter mais informações sobre o caractere BOM e UTF-8. 
 * Todos os arquivos do conjunto de dados devem ser compactados juntos. Os arquivos devem residir diretamente no nível raiz, não em uma subpasta. 
 * Todas as sequências de texto voltadas para o cliente (incluindo nomes de paradas, nomes de rotas e sinais de trânsito) devem usar maiúsculas e minúsculas (não TODAS EM MAIÚSCULAS), seguindo as convenções locais para capitalização de nomes de lugares em displays capazes de exibir caracteres minúsculos (por exemplo, “Brighton Churchill Square”, “Villiers-sur-Marne”, “Market Street”). 
 * O uso de abreviaturas deve ser evitado em todo o feed para nomes e outros textos (por exemplo, St.para Rua), a menos que um local seja chamado pelo seu nome abreviado (por exemplo, “Aeroporto JFK”). As abreviações podem ser problemáticas para acessibilidade por software leitor de tela e interfaces de usuário de voz. O software de consumo pode ser projetado para converter de forma confiável palavras completas em abreviações para exibição, mas a conversão de abreviações em palavras completas está sujeita a maior risco de erro. 
 
## Publicação de conjuntos de dados e práticas gerais 
 
 * Os conjuntos de dados devem ser publicados em um URL público e permanente, incluindo o nome do arquivo zip. (por exemplo, agency/gtfs/gtfs.zip). Idealmente, o URL deve poder ser baixado diretamente, sem a necessidade de login para acessar o arquivo, para facilitar o download pelo consumo de aplicativos de software. Embora seja recomendado (e a prática mais comum) tornar um conjunto de dados GTFS disponível para download abertamente, se um provedor de dados precisar controlar o acesso à GTFS por licenciamento ou outros motivos, é recomendado controlar o acesso ao conjunto de dados GTFS usando chaves de API, o que facilitará downloads automáticos. 
 *Os dados GTFS devem ser publicados em iterações para que um único arquivo em um local estável sempre contenha a descrição oficial mais recente do serviço de uma agency (ou agências) de trânsito. 
 * Os conjuntos de dados devem manter identificadores persistentes (campos de id ) para `stop_id`, `route_id` e `agency_id` nas iterações de dados sempre que possível. 
 * Um conjunto de dados GTFS deve conter serviços atuais e futuros (às vezes chamado de conjunto de dados “mesclado”). Existem diversas [ferramentas de mesclagem](../../../resources/gtfs/#gtfs-merge-tools) disponíveis que podem ser usadas para criar um conjunto de dados mesclado de dois feeds GTFS diferentes. 
 *A qualquer momento, o conjunto de dados GTFS publicado deverá ser válido por pelo menos os próximos 7 dias e, idealmente, enquanto o operador estiver confiante de que o cronograma continuará a ser operado. 
 *Se possível, o conjunto de dados GTFS deverá abranger pelo menos os próximos 30 dias de serviço. 
 *Serviços antigos (calendários expirados) deverão ser removidos do feed. 
 * Se uma modificação de serviço entrar em vigor em 7 dias ou menos, essa alteração de serviço deverá ser expressa por meio de um feed GTFS em tempo real (avisos de serviço ou atualizações de viagem) em vez de um conjunto de dados GTFS estático. 
 * O servidor web que hospeda os dados GTFS deve ser configurado para informar corretamente a date de modificação do arquivo (ver [HTTP/1.1- Solicitação de comentários 2616, na Seção 14.29](https://tools.ietf.org/html/rfc2616#seção-14.29)). 
 
## Definições de campo### agency.txt 
 
 Arquivo: **Obrigatório** 
 
 Chave primária (`agency_id`) 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `agency_id| ID exclusivo | **Condicionalmente Obrigatório** | Identifica uma marca de transporte público que geralmente é sinônimo de agency de transporte público. Observe que em alguns casos, como quando uma única agency opera vários serviços separados, as agências e marcas são distintas. Este documento utiliza o termo “agency” no lugar de “marca”. Um conjunto de dados pode conter dados de várias agências.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** quando o conjunto de dados contém dados de diversas agências de transporte público.<br> - Recomendado de outra forma. | 
 | `agency_name| Text | **Obrigatório** | Nome completo da agency de trânsito. | 
 | `agency_url| URL | **Obrigatório** | URL da agency de transporte público. | 
 | `agency_timezone| Fuso horário | **Obrigatório** | Fuso horário onde a agency de transporte público está localizada. Se várias agências forem especificadas no conjunto de dados, cada uma deverá ter o mesmo `agency_timezone. | 
 | `agency_lang| Código do idioma | Opcional | Idioma principal usado por esta agency de transporte público. Deve ser fornecido para ajudar os consumidores da GTFS a escolher regras de capitalização e outras configurações específicas de idioma para o conjunto de dados. | 
 | `agency_phone| Phone number | Opcional | Um número de telefone de voz da agency especificada. Este campo é um valor de string que apresenta o número de telefone típico da área de atendimento da agência. Pode conter sinais de pontuação para agrupar os dígitos do número. Texto discável (por exemplo, "503-238-RIDE" da TriMet) é permitido, mas o campo não deve conter nenhum outro texto descritivo. | 
 | `agency_fare_url| URL | Opcional | URL de uma página da web que permite ao passageiro comprar passagens ou outros instrumentos tarifários para essa agency on-line. | 
 | `agency_email| E-Email | Opcional | Endereço de e-Email monitorado ativamente pelo departamento de atendimento ao cliente da agência. Este endereço de e-mail deve ser um ponto de contato direto onde os passageiros do transporte público possam entrar em contato com um representante de atendimento ao cliente da agency. | 
 
### stops.txt 
 
 Arquivo: **Obrigatório** 
 
 Chave primária (`stop_id`) 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `stop_id` | ID exclusivo | **Obrigatório** | Identifica uma localização: paragem/plataforma, estação, entrada/saída, nó genérico ou área de embarque (ver `location_type`).<br><br> O ID deve ser exclusivo em todos os valores `stops.stop_id`, locations.geojson `id` e `location_groups.location_group_id`.<br><br> Várias routes podem usar o mesmo `stop_id`. | 
 | `stop_code| Text | Opcional | Texto curto ou um número que identifica a localização dos passageiros. Esses códigos são frequentemente usados ​​em sistemas de informações de trânsito baseados em telefone ou impressos em sinalização para facilitar aos passageiros a obtenção de informações sobre um local específico. O `stop_code` pode ser o mesmo que `stop_id` se for voltado ao público. Este campo deve ser deixado em branco para locais sem código apresentado aos passageiros. | 
 | `stop_name| Text | **Condicionalmente Obrigatório** | Nome do local. O `stop_name` deve corresponder ao nome da agência voltado para o passageiro no local, conforme impresso em um horário, publicado on-line ou representado na sinalização. Para traduções para outros idiomas, use [translations.txt](#translationstxt).<br><br> Quando o local for uma área de embarque (`location_type=4`), o `stop_name` deverá conter o nome da área de embarque conforme exibido pela agency. Pode ser apenas uma letra (como em algumas estações ferroviárias intermunicipais europeias) ou um texto como “Área de embarque para cadeiras de rodas” (metrô de Nova York) ou “Chefe de trens curtos” (RER de Paris).<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** para locais que são stops (`location_type=0`), estações (`location_type=1`) ou entradas/saídas (`location_type=2`).<br> - Opcional para locais que sejam nós genéricos (`location_type=3`) ou áreas de embarque (`location_type=4`).| 
 | `tts_stop_name` | Text | Opcional | Versão legível do `stop_name`. Consulte "Campo de conversão de texto em fala" em [Definições de termos](#term-definitions) para obter mais informações. | 
 | `stop_desc| Text | Opcional | Descrição do local que fornece informações úteis e de qualidade. Não deve ser uma duplicata de `stop_name`.| 
 | `parar

lat` | Latitude | **Condicionalmente Obrigatório** | Latitude do local.<br><br> Para stops/plataformas (`location_type=0`) e área de embarque (`location_type=4`), as coordenadas devem ser as do poste de ônibus — se existir — e caso contrário do local onde os viajantes estão embarcando no vehicle (na calçada ou na plataforma, e não na estrada ou na pista onde o vehicle stops).<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** para locais que são stops (`location_type=0`), estações (`location_type=1`) ou entradas/saídas (`location_type=2`).<br> - Opcional para locais que sejam nós genéricos (`location_type=3`) ou áreas de embarque (`location_type=4`).| 
 | `stop_lon` | Longitude | **Condicionalmente Obrigatório** | Longitude do local.<br><br> Para stops/plataformas (`location_type=0`) e área de embarque (`location_type=4`), as coordenadas devem ser as do poste de ônibus — se existir — e caso contrário do local onde os viajantes estão embarcando no vehicle (na calçada ou na plataforma, e não na estrada ou na pista onde o vehicle stops).<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** para locais que são stops (`location_type=0`), estações (`location_type=1`) ou entradas/saídas (`location_type=2`).<br> - Opcional para locais que sejam nós genéricos (`location_type=3`) ou áreas de embarque (`location_type=4`). | 
 | `zone_id` | ID | Opcional | Identifica a zona tarifária para uma parada. Se este registro representa uma estação ou entrada de estação, o `zone_id é ignorado.| 
 | `stop_url| URL | Opcional | URL de uma página da web sobre o local. Isso deve ser diferente dos valores dos campos `agency.agency_url e `routes.route_url. | 
 | `location_type` | Enum | Opcional | Tipo de localização. As opções válidas são:<br><br> `0` (ou em branco) - **Parar** (ou **Plataforma**). Um local onde os passageiros embarcam ou desembarcam de um vehicle de trânsito. É chamada de plataforma quando definida dentro de uma `parent_station.<br> `1` - **Estação**. Uma estrutura física ou área que contém uma ou mais plataformas.<br> `2` - **Entrada/Saída**. Um local onde os passageiros podem entrar ou sair de uma estação pela rua. Se uma entrada/saída pertencer a múltiplas estações, ela poderá estar ligada por pathways a ambas, mas o provedor de dados deverá escolher uma delas como pai.<br> `3` - **Nó genérico**. Um local dentro de uma estação, que não corresponde a nenhum outro `location_type`, que pode ser usado para vincular pathways definidos em [pathways.txt](#pathwaystxt).<br> `4` - **Área de embarque**. Local específico de uma plataforma onde os passageiros podem embarcar e/ou desembarcar dos veículos.| 
 | `parent_station| ID estrangeiro referenciando `stops.stop_id` | **Condicionalmente Obrigatório** | Define a hierarquia entre os diferentes locais definidos em [stops.txt](#stopstxt). Ele contém o ID do local pai, conforme a seguir:<br><br> - **Stop/platform** (`location_type=0`): o campo `parent_station` contém o ID de uma estação.<br> - **Estação** (`location_type=1`): este campo deve estar vazio.<br> - **Entrada/saída** (`location_type=2`) ou **nó genérico** (`location_type=3`): o campo `parent_station` contém o ID de uma estação (`location_type=1`)<br> - **Área de Embarque** (`location_type=4`): o campo `parent_station contém o ID de uma plataforma.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** para locais que sejam entradas (`location_type=2`), nós genéricos (`location_type=3`) ou áreas de embarque (`location_type=4`).<br> - Opcional para stops/plataformas (`location_type=0`).<br> - Proibido para estações (`location_type=1`).| 
 | `stop_timezone| Fuso horário | Opcional | Fuso horário do local. Se o local tiver uma estação pai, ele herdará o fuso horário da estação pai em vez de aplicar o seu próprio. Estações e stops sem pai com `stop_timezone` vazio herdam o fuso horário especificado por `agency.agency_timezone`. Os horários fornecidos em [stop_times.txt](#stop_timestxt) estão no fuso horário especificado por `agency.agency_timezone`, não por `stop_timezone`. Isso garante que os valores de tempo em uma viagem sempre aumentem ao longo da viagem, independentemente dos fusos horários que a viagem atravessa. | 
 | `wheelchair_boarding` | Enum | Opcional | Indica se o embarque para cadeiras de rodas é possível no local. As opções válidas são:<br><br> Para stops sem pais:<br> `0` ou vazio- Nenhuma informação de acessibilidade para a parada.<br> `1` - Alguns veículos nesta parada podem ser abordados por um passageiro em cadeira de rodas.<br> `2` - O embarque para cadeiras de rodas não é possível nesta parada.<br><br> Para stops infantis:<br> `0` ou vazio- Stop herdará seu comportamento `wheelchair_boarding` da estação pai, se especificado no pai.<br> `1` - Existe algum caminho acessível de fora da estação até a parada/plataforma específica.<br> `2` - Não existe nenhum caminho acessível de fora da estação para a parada/plataforma específica.<br><br> Para entradas/saídas de estações:<br> `0` ou vazio- A entrada da estação herdará seu comportamento `wheelchair_boarding` da estação pai, se especificado para o pai.<br> `1` - A entrada da estação é acessível para cadeiras de rodas.<br> `2` - Não há caminho acessível da entrada da estação até as stops/plataformas. | 
 | `level_id| ID estrangeiro referenciando `levels.level_id| Opcional | Nível do local. O mesmo nível pode ser usado por múltiplas estações desvinculadas.| 
 | `platform_code| Text | Opcional | Identificador de plataforma para uma parada de plataforma (uma parada pertencente a uma estação). Deve ser apenas o identificador da plataforma (por exemplo, "G" ou "3"). Palavras como “plataforma” ou “faixa” (ou o equivalente específico do idioma do feed) não devem ser incluídas. Isso permite que os consumidores de feeds internacionalizem e localizem mais facilmente o identificador da plataforma para outros idiomas. | 
 
 
### routes.txt 
 
 Arquivo: **Obrigatório** 
 
 Chave primária (`route_id`) 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `route_id` | ID exclusivo | **Obrigatório** | Identifica uma rota. | 
 | `agency_id| ID estrangeiro com referência `agency.agency_id` | **Condicionalmente Obrigatório** | Agência para a rota especificada.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se diversas agências estiverem definidas em [agency.txt](#agencytxt).<br> - Recomendado de outra forma. | 
 | `route_short_name` | Text | **Condicionalmente Obrigatório** | Nome abreviado de uma rota. Freqüentemente, um identificador curto e abstrato (por exemplo, "32", "100X", "Verde") que os passageiros usam para identificar uma rota. Ambos `route_short_name` e `route_long_name` podem ser definidos.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se `routes.route_long_name estiver vazio.<br> - Recomendado se houver uma breve designação de serviço. Este deve ser o nome comumente conhecido do passageiro do serviço e não deve ter mais de 12 caracteres. | 
 | `route_long_name` | Text | **Condicionalmente Obrigatório** | Nome completo de uma rota. Este nome é geralmente mais descritivo do que `route_short_name` e geralmente inclui o destino ou parada da rota. Ambos `route_short_name` e `route_long_name` podem ser definidos.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se `routes.route_short_name estiver vazio.<br> - Opcional caso contrário. | 
 | `route_desc` | Text | Opcional | Descrição de uma rota que fornece informações úteis e de qualidade. Não deve ser uma duplicata de `route_short_name` ou `route_long_name`.<hr> _Exemplo: os trens "A" operam entre Inwood-207 St, Manhattan e Far Rockaway-Mott Avenue, Queens em todos os momentos. Também das 6h até cerca da meia-noite, trens "A" adicionais operam entre Inwood-207 St e Lefferts Boulevard (os trens normalmente alternam entre Lefferts Blvd e Far Rockaway)._ | 
 | `route_type` | Enum | **Obrigatório** | Indica o tipo de transporte utilizado em uma rota. As opções válidas são:<br><br> `0` - Bonde, bonde, metrô leve. Qualquer sistema ferroviário leve ou de nível viário dentro de uma área metropolitana.<br> `1` - Metrô, Metrô. Qualquer sistema ferroviário subterrâneo dentro de uma área metropolitana.<br> `2` - Trilho. Usado para viagens intermunicipais ou de longa distância.<br> `3` - Ônibus. Usado para routes de ônibus de curta e longa distância.<br> `4` - Balsa. Usado para serviços de barco de curta e longa distância.<br> `5` - Teleférico. Usado para vagões de nível de rua onde o cabo passa por baixo do vehicle (por exemplo, teleférico em São Francisco).<br> `6` - Elevador aéreo, teleférico suspenso (por exemplo, teleférico, teleférico). Transporte por cabo onde cabines, carros, gôndolas ou cadeiras abertas são suspensas por meio de um ou mais cabos.<br> `7` - Funicular. Qualquer sistema ferroviário projetado para inclinações íngremes.<br> `11` - Trólebus. Ônibus elétricos que extraem energia de fios aéreos por meio de postes.<br> `12` - Monotrilho. Ferrovia em que a via consiste em um único trilho ou viga. | 
 | `route_url` | URL | Opcional | URL de uma página da web sobre uma rota específica. Deve ser diferente do valor `agency.agency_url. | 
 | `route_color| Cor | Opcional | Designação de cores da rota que corresponda ao material voltado para o público. O padrão é branco (`FFFFFF`) quando omitido ou deixado em branco. A diferença de cor entre `route_color e `route_text_color deve fornecer contraste suficiente quando visualizado em uma tela preto e branco. | 
 | `route_text_color` | Cor | Opcional | Cor legível para usar em texto desenhado contra um fundo de `route_color. O padrão é preto (`000000`) quando omitido ou deixado em branco. A diferença de cor entre `route_color e `route_text_color deve fornecer contraste suficiente quando visualizado em uma tela preto e branco. | 
 | `route_sort_order` | Inteiro não negativo | Opcional | Ordena as routes de forma ideal para apresentação aos clientes. Rotas com valores `route_sort_order menores devem ser exibidas primeiro. | 
 | `continuous_pickup` | Enum | **Condicionalmente Proibido** | Indica que o passageiro pode embarcar no vehicle de transporte público em qualquer ponto ao longo do trajeto de viagem do veículo, conforme descrito por [shapes.txt](#shapestxt), em cada viagem do trajeto. As opções válidas são:<br><br> `0` - Partida de parada contínua.<br> `1` ou vazio- Sem pickup de parada contínua.<br> `2` - É necessário telefonar para a agency para combinar a coleta com parada contínua.<br> `3` - Deve coordenar com o motorista para organizar a coleta de parada contínua.<br><br> Os valores para `routes.continuous_pickup` podem ser substituídos definindo valores em `stop_times.continuous_pickup` para `stop_time`s específicos ao longo da rota.<br><br> **Condicionalmente Proibido**:<br> - **Proibido** se `stop_times.start_pickup_drop_off_window` ou `stop_times.end_pickup_drop_off_window` são definidos para qualquer viagem desta rota.<br> - Opcional caso contrário. | 
 | `continuous_drop_off` | Enum | **Condicionalmente Proibido** | Indica que o passageiro pode descer do vehicle de transporte público em qualquer ponto ao longo do trajeto de viagem do veículo, conforme descrito por [shapes.txt](#shapestxt), em cada viagem da rota. As opções válidas são:<br><br> `0` - Queda de parada contínua.<br> `1` ou vazio- Sem queda de parada contínua.<br> `2` - Deve telefonar para a agency para providenciar a parada contínua.<br> `3` - Deve coordenar com o motorista para organizar a parada contínua.<br><br> Os valores para `routes.continuous_drop_off podem ser substituídos definindo valores em `stop_times.continuous_drop_off para `stop_time específicos ao longo da rota.<br><br> **Condicionalmente Proibido**:<br> - **Proibido** se `stop_times.start_pickup_drop_off_window` ou `stop_times.end_pickup_drop_off_window` são definidos para qualquer viagem desta rota.<br> - Opcional caso contrário. | 
 | `network_id| ID | **Condicionalmente Proibido** | Identifica um grupo de routes. Várias linhas em [routes.txt](#routestxt) podem ter o mesmo `network_id.<br><br> Condicionalmente Proibido:<br> - **Proibido** se o arquivo [route_networks.txt](#route_networkstxt) existir.<br> - Opcional caso contrário. 
 
### trips.txt 
 
 Arquivo: **Obrigatório** 
 
 Chave primária (`trip_id`) 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `route_id` | ID estrangeiro referenciando `routes.route_id` | **Obrigatório** | Identifica uma rota. | 
 | `service_id` | ID estrangeiro referenciando `calendar.service_id ou `calendar_dates.service_id| **Obrigatório** | Identifica um conjunto de datas em que o serviço está disponível para uma ou mais routes. | 
 | `trip_id` | ID exclusivo | **Obrigatório** | Identifica uma viagem. | 
 | `trip_headsign| Text | Opcional | Text que aparece na sinalização identificando o destino da viagem aos passageiros. Deve ser usado para distinguir entre diferentes padrões de serviço na mesma rota.<br><br> Se o sinal de direção mudar durante uma viagem, os valores de `trip_headsign podem ser substituídos definindo valores em `stop_times.stop_headsign para `stop_time específicos ao longo da viagem. | 
 | `trip_short_name` | Text | Opcional | Texto voltado ao público usado para identificar a viagem aos passageiros, por exemplo, para identificar os números dos trens para viagens de trens suburbanos. Se os passageiros normalmente não confiam nos nomes das viagens, `trip_short_name deve estar vazio. Um valor `trip_short_name, se fornecido, deve identificar exclusivamente uma viagem dentro de um dia de serviço; não deve ser usado para nomes de destinos ou designações limitadas/expressas. | 
 | `direction_id` | Enum | Opcional | Indica a direção de deslocamento de uma viagem. Este campo não deve ser utilizado em roteamento; ele fornece uma maneira de separar viagens por direção ao publicar tabelas de horários. As opções válidas são:<br><br> `0` - Viagem em uma direção (por exemplo, viagem de ida).<br> `1` - Viagem na direção oposta (por exemplo, viagem de entrada).<hr> *Exemplo: Os campos `trip_headsign` e `direction_id` podem ser usados ​​juntos para atribuir um nome para viajar em cada direção para um conjunto de viagens. Um arquivo [trips.txt](#tripstxt) pode conter estes registros para uso em tabelas de horários:*<br> `trip_id,...,trip_headsign,direction_id`<br> `1234,...,Airport,0`<br> `1505,...,Downtown,1` | 
 | `block_id` | ID | Opcional | Identifica o bloco ao qual pertence a viagem. Um bloco consiste em uma única viagem ou em várias viagens sequenciais feitas utilizando o mesmo vehicle, definidas por dias de serviço compartilhado e `block_id. Um `block_id pode ter viagens com dias de atendimento diferentes, formando blocos distintos. Veja o [exemplo abaixo](#example-blocks-and-service-day). Para fornecer informações de transfers no assento, [transfers](#transferstxt) de `transfer_type` `4` devem ser fornecidas. | 
 | `shape_id` | ID estrangeiro referenciando `shapes.shape_id` | **Condicionalmente Obrigatório** | Identifica uma shape geoespacial que descreve o caminho de deslocamento do vehicle para uma viagem.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se a viagem tiver um comportamento contínuo de embarque ou desembarque definido em [routes.txt](#routestxt) ou em [stop_times.txt](#stop_timestxt).<br> - Opcional caso contrário. | 
 | `wheelchair_accessible` | Enum | Opcional | Indica acessibilidade para cadeiras de rodas. As opções válidas são:<br><br> `0` ou vazio- Nenhuma informação de acessibilidade para a viagem.<br> `1` - O veículo utilizado nesta viagem específica pode acomodar pelo menos um passageiro em cadeira de rodas.<br> `2` - Nenhum passageiro em cadeira de rodas poderá ser acomodado nesta viagem. | 
 | `bikes_allowed` | Enum | Opcional | Indica se bicicletas são permitidas. As opções válidas são:<br><br> `0` ou vazio- Nenhuma informação de bicicleta para a viagem.<br> `1` - O veículo utilizado nesta viagem específica pode acomodar pelo menos uma bicicleta.<br> `2` - Não são permitidas bicicletas nesta viagem. | 
 
#### Exemplo: Bloqueios e dia de atendimento 
 
 O exemplo abaixo é válido, com bloqueios distintos em todos os dias da semana. 
 
 | route_id | trip_id | service_id | block_id | <span style="font-weight:normal">*(horário da primeira parada)*</span> | <span style="font-weight:normal">*(horário da última parada)*</span> | 
 |----------|------------|--------------------------------|----------|-----------------------------------------|--------------| 
 | vermelho | trip_1 | segunda-terça-qua-qui-sexta-sábado-dom | loop_vermelho | 22:00:00 | 22:55:00 | 
 | vermelho | trip_2 | sexta-feira-dom | loop_vermelho | 23:00:00 | 23:55:00 | 
 | vermelho | trip_3 | sexta-sábado | loop_vermelho | 24:00:00 | 24:55:00 | 
 | vermelho | trip_4 | segunda-feira-qua-qui | loop_vermelho | 20:00:00 | 20:50:00 | 
 | vermelho | trip_5 | segunda-feira-qua-qui | loop_vermelho | 21:00:00 | 21:50:00 | 
 
 Notas na tabela acima: 
 
 * De sexta a sábado de manhã, por exemplo, um único vehicle opera `trip_1, `trip_2 e `trip_3(das 22h00 às 00h55). Observe que a última viagem ocorre no sábado, das 12h00 às 00h55, mas faz parte do “dia de atendimento” de sexta-feira porque o horário é das 24h00 às 24h55. 
 * Às segundas, terças, quartas e quintas-feiras, um único vehicle opera `trip_1, `trip_4 e `trip_5 em um bloco das 20h00 às 22h55. 
 
### stop_times.txt 
 
 Arquivo: **Obrigatório** 
 
 Chave primária (`trip_id`, `stop_sequence`) 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `trip_id` | ID estrangeiro com referência a `trips.trip_id` | **Obrigatório** | Identifica uma viagem. | 
 | `arrival_time| Tempo | **Condicionalmente Obrigatório** | Hora de chegada na parada (definida por `stop_times.stop_id`) para uma viagem específica (definida por `stop_times.trip_id`) no fuso horário especificado por `agency.agency_timezone`, não por `stops.stop_timezone`.<br><br> Se não houver horários separados para arrival e departure em uma parada, `arrival_time e `departure_time` deverão ser iguais.<br><br> Para horários que ocorram após a meia-noite do dia de atendimento, insira o horário como um valor maior que 24:00:00 em HH:MM:SS.<br><br> Se os horários exatos de arrival e departure (`timepoint=1` ou vazio) não estiverem disponíveis, os horários de arrival e departure estimados ou interpolados (`timepoint=0`) deverão ser fornecidos.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** para a primeira e última parada de uma viagem (definida por `stop_times.stop_sequence`).<br> - **Obrigatório** para `timepoint=1`.<br> - **Proibido** quando `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estão definidos.<br> - Opcional caso contrário.| 
 | `departure_time` | Tempo | **Condicionalmente Obrigatório** | Hora de partida da parada (definida por `stop_times.stop_id`) para uma viagem específica (definida por `stop_times.trip_id`) no fuso horário especificado por `agency.agency_timezone`, não por `stops.stop_timezone`.<br><br> Se não houver horários separados para arrival e departure em uma parada, `arrival_time e `departure_time` deverão ser iguais.<br><br> Para horários que ocorram após a meia-noite do dia de atendimento, insira o horário como um valor maior que 24:00:00 em HH:MM:SS.<br><br> Se os horários exatos de arrival e departure (`timepoint=1` ou vazio) não estiverem disponíveis, os horários de arrival e departure estimados ou interpolados (`timepoint=0`) deverão ser fornecidos.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** para `timepoint=1`.<br> - **Proibido** quando `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estão definidos.<br> - Opcional caso contrário. | 
 | `stop_id` | ID estrangeiro referenciando `stops.stop_id` | **Condicionalmente Obrigatório** | Identifica a parada atendida. Todas as stops atendidas durante uma viagem devem ter um registro em [stop_times.txt](#stop_timestxt). Os locais referenciados devem ser stops/plataformas, ou seja, seu valor `stops.location_type deve ser `0` ou vazio. Uma parada pode ser atendida diversas vezes na mesma viagem, e diversas viagens e routes podem atender a mesma parada.<br><br> O serviço sob demanda usando stops deve ser referenciado na sequência em que o serviço está disponível nessas stops. Um consumidor de dados deve assumir que a viagem é possível de uma parada ou local para qualquer parada ou local posterior na viagem, desde que o `drop_off_type de cada stop_time e as restrições de tempo de cada janela de início/end_pickup_drop_off_window não o proíbam..<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se `stop_times.location_group_id` E `stop_times.location_id` NÃO estiverem definidos.<br> - **Proibido** se `stop_times.location_group_id` ou `stop_times.location_id` estiverem definidos. | 
 | `location_group_id` | ID estrangeiro referenciando `location_groups.location_group_id` | **Condicionalmente Proibido** | Identifica o grupo de locais atendidos que indica grupos de stops onde os passageiros podem solicitar embarque ou desembarque. Todos os grupos de locais atendidos durante uma viagem devem ter um registro em [stop_times.txt](#stop_timestxt). Várias viagens e routes podem atender o mesmo grupo de locais.<br><br> O serviço sob demanda usando grupos de locais deve ser referenciado na sequência em que o serviço está disponível nesses grupos de locais. Um consumidor de dados deve assumir que a viagem é possível de uma parada ou local para qualquer parada ou local posterior na viagem, desde que o `drop_off_type de cada stop_time e as restrições de tempo de cada janela de início/end_pickup_drop_off_window não o proíbam..<br><br> **Condicionalmente Proibido**:<br> - **Proibido** se `stop_times.stop_id` ou `stop_times.location_id` estiverem definidos. | 
 | `local_id` | ID estrangeiro referenciando `id` de `locations.geojson` | **Condicionalmente Proibido** | Identifica o local GeoJSON que corresponde à zona atendida onde os passageiros podem solicitar coleta ou entrega. Todos os locais GeoJSON atendidos durante uma viagem devem ter um registro em [stop_times.txt](#stop_timestxt). Várias viagens e routes podem atender ao mesmo local GeoJSON.<br><br> O serviço sob demanda dentro dos locais deve ser referenciado na sequência em que o serviço está disponível nesses locais. Um consumidor de dados deve assumir que a viagem é possível de uma parada ou local para qualquer parada ou local posterior na viagem, desde que o `drop_off_type de cada stop_time e as restrições de tempo de cada janela de início/end_pickup_drop_off_window não o proíbam..<br><br> **Condicionalmente Proibido**:<br> - **Proibido** se `stop_times.stop_id` ou `stop_times.location_group_id` estiverem definidos. | 
 | `stop_sequence` | Inteiro não negativo | **Obrigatório** | Ordem das stops, grupos de locais ou locais GeoJSON para uma viagem específica. Os valores devem aumentar ao longo da viagem, mas não precisam ser consecutivos.<hr> *Exemplo: o primeiro local da viagem pode ter uma `stop_sequence`= `1`, o segundo local da viagem pode ter uma `stop_sequence`=`23`, o terceiro local pode ter uma `stop_sequence`=`40`, e assim por diante.*<br><br> Viajar dentro do mesmo grupo de locais ou localização GeoJSON requer dois registros em [stop_times.txt](#stop_timestxt) com o mesmo `location_group_id` ou `location_id`. | 
 | `stop_headsign| Text | Opcional | Text que aparece na sinalização identificando o destino da viagem aos passageiros. Este campo substitui o padrão `trips.trip_headsign quando o headsign muda entre as stops. Se o headsign for exibido para uma viagem inteira, `trips.trip_headsign deverá ser usado.<br><br> Um valor `stop_headsign` especificado para um `stop_time` não se aplica a `stop_time`s subsequentes na mesma viagem. Se você deseja substituir o `trip_headsign` para vários `stop_time`s na mesma viagem, o valor `stop_headsign` deve ser repeated em cada linha `stop_time`. | 
 | `start_pickup_drop_off_window` | Tempo | **Condicionalmente Obrigatório** | Hora em que o serviço sob demanda fica disponível em um local, grupo de locais ou parada GeoJSON.<br><br> **Condicionalmente obrigatório**:<br> - **Obrigatório** se `stop_times.location_group_id` ou `stop_times.location_id` estiver definido.<br> - **Obrigatório** se `end_pickup_drop_off_window` estiver definido.<br> - **Proibido** se `arrival_time ou `departure_time` estiver definido.<br> - Opcional caso contrário. | 
 | `end_pickup_drop_off_window` | Tempo | **Condicionalmente Obrigatório** | Hora em que o serviço sob demanda termina em um local, grupo de locais ou parada GeoJSON.<br><br> **Condicionalmente obrigatório**:<br> - **Obrigatório** se `stop_times.location_group_id` ou `stop_times.location_id` estiver definido.<br> - **Obrigatório** se `start_pickup_drop_off_window` estiver definido.<br> - **Proibido** se `arrival_time ou `departure_time` estiver definido.<br> - Opcional caso contrário. | 
 | `pickup_type` | Enum | **Condicionalmente Proibido** | Indica o método de coleta. As opções válidas são:<br><br> `0` ou vazio- coleta programada regularmente.<br> `1` - Nenhuma coleta disponível.<br> `2` - É necessário telefonar para a agency para combinar a coleta.<br> `3` - Deve coordenar com o motorista para organizar a coleta.<br><br> **Condicionalmente Proibido**:<br> - `pickup_type=0` **proibido** se `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estiverem definidos.<br> - `pickup_type=3` **proibido** se `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estiverem definidos.<br> - Opcional caso contrário. | 
 | `drop_off_type` | Enum | **Condicionalmente Proibido** | Indica o método de entrega. As opções válidas são:<br><br> `0` ou vazio- entrega programada regularmente.<br> `1` - Não há entrega disponível.<br> `2` - É necessário telefonar para a agency para combinar a entrega.<br> `3` - Deve coordenar com o motorista para organizar a entrega.<br><br> **Condicionalmente Proibido**:<br> - `drop_off_type=0` **proibido** se `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estiverem definidos.<br> - Opcional caso contrário. | 
 | `continuous_pickup` | Enum | **Condicionalmente Proibido** | Indica que o passageiro pode embarcar no vehicle de transporte público em qualquer ponto ao longo do trajeto de viagem do veículo, conforme descrito por [shapes.txt](#shapestxt), deste `stop_time` até o próximo `stop_time` na `stop_sequence` da viagem. As opções válidas são:<br><br> `0` - Partida de parada contínua.

br> `1` ou vazio- Sem pickup de parada contínua.<br> `2` - É necessário telefonar para a agency para combinar a coleta com parada contínua.<br> `3` - Deve coordenar com o motorista para organizar a coleta de parada contínua.<br><br> Se este campo for preenchido, ele substituirá qualquer comportamento de coleta contínua definido em [routes.txt](#routestxt). Se este campo estiver vazio, o `stop_time` herda qualquer comportamento de coleta contínua definido em [routes.txt](#routestxt).<br><br> **Condicionalmente Proibido**:<br> - **Proibido** se `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estiverem definidos.<br> - Opcional caso contrário. | 
 | `continuous_drop_off` | Enum | **Condicionalmente Proibido** | Indica que o passageiro pode descer do vehicle de transporte público em qualquer ponto ao longo do caminho de viagem do veículo, conforme descrito por [shapes.txt](#shapestxt), deste `stop_time` até o próximo `stop_time` na `stop_sequence` da viagem. As opções válidas são:<br><br> `0` - Queda de parada contínua.<br> `1` ou vazio- Sem queda de parada contínua.<br> `2` - Deve telefonar para a agency para providenciar a parada contínua.<br> `3` - Deve coordenar com o motorista para organizar a parada contínua.<br><br> Se este campo for preenchido, ele substituirá qualquer comportamento de entrega contínua definido em [routes.txt](#routestxt). Se este campo estiver vazio, o `stop_time` herda qualquer comportamento de entrega contínua definido em [routes.txt](#routestxt).<br><br> **Condicionalmente Proibido**:<br> - **Proibido** se `start_pickup_drop_off_window` ou `end_pickup_drop_off_window` estiverem definidos.<br> - Opcional caso contrário. | 
 | `shape_dist_traveled` | float não negativa | Opcional | Distância real percorrida ao longo do shape associado, desde a primeira parada até a parada especificada neste registro. Este campo especifica quanto da shape será desenhada entre duas stops durante uma viagem. Deve estar nas mesmas unidades usadas em [shapes.txt](#shapestxt). Os valores usados ​​para `shape_dist_traveled` devem aumentar junto com `stop_sequence`; eles não devem ser usados ​​para mostrar deslocamento reverso ao longo de uma rota.<br><br> Recomendado para routes que possuem looping ou inlining (o vehicle cruza ou percorre a mesma parte do alinhamento em uma viagem). Consulte [`shapes.shape_dist_traveled](#shapestxt).<hr> *Exemplo: Se um ônibus percorre uma distância de 5,25 quilômetros do início do shape até a parada, `shape_dist_traveled`=`5,25`.*| 
 | `timepoint| Enum | Recomendado | Indica se os horários de arrival e departure de uma parada são rigorosamente respeitados pelo vehicle ou se são horários aproximados e/ou interpolados. Este campo permite que um produtor de GTFS forneça tempos de parada interpolados, ao mesmo tempo que indica que os tempos são aproximados. As opções válidas são:<br><br> `0` - Os tempos são considerados aproximados.<br> `1` ou vazio- Os tempos são considerados exatos. | 
 | `pickup_booking_rule_id` | ID que faz referência a `booking_rules.booking_rule_id` | Opcional | Identifica a regra de reserva de embarque neste horário de parada.<br><br> Recomendado quando `pickup_type=2`. | 
 | `drop_off_booking_rule_id` | ID que faz referência a `booking_rules.booking_rule_id` | Opcional | Identifica a regra de reserva de desembarque neste horário de parada.<br><br> Recomendado quando `drop_off_type=2`. | 
 
#### Comportamento de roteamento do serviço sob demanda- Ao fornecer roteamento ou tempo de viagem entre a origem e o destino, os consumidores de dados devem ignorar registros intermediários stop_times.txt com o mesmo `trip_id` que possuem `start_pickup_drop_off_window` e `end_pickup_drop_off_window` definido. Para obter exemplos que demonstram o que deve ser ignorado, consulte [a página de exemplo de dados](../examples/flex/#ignoring-intermediate-stop-times-records-with-pickupdrop-off-windows). 
 - É proibida a sobreposição simultânea de geometria `id` locations.geojson, horário `start/end_pickup_drop_off_window e `pickup_type ou `drop_off_type entre dois ou mais registros stop_times.txt com o mesmo `trip_id`. Para exemplos que demonstram o que é proibido, consulte [a página de exemplo de dados](../examples/flex/#zone-overlap-constraint). 
 
### calendar.txt 
 
 Arquivo: **Condicionalmente Obrigatório** 
 
 Chave primária (`service_id`) 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `service_id` | ID exclusivo | **Obrigatório** | Identifica um conjunto de datas em que o serviço está disponível para uma ou mais routes. | 
 | `monday| Enum | **Obrigatório** | Indica se o serviço funciona todas as segundas-feiras no intervalo de date especificado pelos campos `start_date` e `end_date. Observe que exceções para datas específicas podem ser listadas em [calendar_dates.txt](#calendar_datestxt). As opções válidas são:<br><br> `1` - O serviço está disponível todas as segundas-feiras do intervalo de date .<br> `0` - O serviço não está disponível às segundas-feiras no intervalo de date. | 
 | `tuesday| Enum | **Obrigatório** | Funciona da mesma forma que `monday exceto se aplica às terças-feiras | 
 | `wednesday| Enum | **Obrigatório** | Funciona da mesma forma que `monday exceto se aplica às quartas-feiras | 
 | `thursday| Enum | **Obrigatório** | Funciona da mesma forma que `monday exceto se aplica às quintas-feiras | 
 | `friday| Enum | **Obrigatório** | Funciona da mesma forma que `monday exceto se aplica às sextas-feiras | 
 | `saturday` | Enum | **Obrigatório** | Funciona da mesma forma que `monday exceto se aplica aos sábados. | 
 | `sunday| Enum | **Obrigatório** | Funciona da mesma forma que `monday exceto se aplica aos domingos. | 
 | `start_date` | Data | **Obrigatório** | Inicie o dia de serviço para o intervalo de serviço. | 
 | `end_date| Data | **Obrigatório** | Finalize o dia de serviço para o intervalo de serviço. Este dia de serviço está incluído no intervalo. | 
 
### calendar_dates.txt 
 
 Arquivo: **Condicionalmente Obrigatório** 
 
 Chave primária (`service_id`, `date`) 
 
 O [calendar_dates.txt](#calendar_datestxt ) tabela ativa ou desativa explicitamente o serviço por date. Pode ser usado de duas maneiras. 
 
 * Recomendado: Use [calendar_dates.txt](#calendar_datestxt) em conjunto com [calendar.txt](#calendartxt) para definir exceções aos padrões de serviço padrão definidos em [calendar.txt](#calendartxt). Se o serviço for geralmente regular, com algumas alterações em datas explícitas (por exemplo, para acomodar serviços de eventos especiais ou horários escolares), esta é uma boa abordagem. Neste caso, `calendar_dates.service_id` é um ID estrangeiro que faz referência a `calendar.service_id`. 
 * Alternativa: Omitir [calendar.txt](#calendartxt) e especificar cada date de serviço em [calendar_dates.txt](#calendar_datestxt). Isto permite uma variação considerável de serviço e acomoda serviços sem horários semanais normais. Neste caso, `service_id é um ID. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `service_id` | ID estrangeiro referenciando `calendar.service_id ou ID | **Obrigatório** | Identifica um conjunto de datas em que ocorre uma exceção de serviço para uma ou mais routes. Cada par (`service_id`, `date`) só pode aparecer uma vez em [calendar_dates.txt](#calendar_datestxt) se usar [calendar.txt](#calendartxt) e [calendar_dates.txt](#calendar_datestxt) em conjunto. Se um valor `service_id aparecer em [calendar.txt](#calendartxt) e [calendar_dates.txt](#calendar_datestxt), as informações em [calendar_dates.txt](#calendar_datestxt) modificam as informações de serviço especificadas em [calendar.txt](#calendartxt). | 
 | `date| Data | **Obrigatório** | Data em que ocorre a exceção de serviço. | 
 | `exception_type` | Enum | **Obrigatório** | Indica se o serviço está disponível na date especificada no campo de date. As opções válidas são:<br><br> `1` - O serviço foi adicionado para a date especificada.<br> `2` - O serviço foi removido na date especificada.<hr> *Exemplo: suponha que uma rota tenha um conjunto de viagens disponíveis nos feriados e outro conjunto de viagens disponíveis nos outros dias. Um `service_id pode corresponder à programação de serviço regular e outro `service_id pode corresponder à programação de feriados. Para um feriado específico, o arquivo [calendar_dates.txt](#calendar_datestxt) pode ser usado para adicionar o feriado ao feriado `service_id` e para remover o feriado da programação regular `service_id`.* | 
 
### fare_attributes.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`fare_id`) 
 
 **Versões**<br> 
 Existem duas opções de modelagem para descrição de tarifas. GTFS- Fares V1 é a opção legada para descrever informações mínimas sobre tarifas. GTFS- Fares V2 é um método atualizado que permite um relato mais detalhado da estrutura tarifária de uma agência. Ambos podem estar presentes em um conjunto de dados, mas apenas um método deve ser usado por um consumidor de dados para um determinado conjunto de dados. Recomenda-se que a GTFS- Fares V2 tenha precedência sobre a GTFS- Fares V1.<br><br> Os arquivos associados ao GTFS- Fares V1 são:<br> - [fare_attributes.txt](#fare_attributestxt)<br> - [fare_rules.txt](#fare_rulestxt)<br><br> Os arquivos associados ao GTFS- Fares V2 são:<br> - [.txt](#fare_mediatxt)<br> - [fare_products.txt](#fare_productstxt)<br> - [fare_leg_rules.txt](#fare_leg_rulestxt)<br> - [fare_transfer_rules.txt](#fare_transfer_rulestxt) 
 
<br> 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `fare_id` | ID exclusivo | **Obrigatório** | Identifica uma classe de tarifa. | 
 | `price| float não negativa | **Obrigatório** | price da tarifa, na unidade especificada por `currency_type. | 
 | `currency_type` | Código da moeda | **Obrigatório** | Moeda usada para pagar a tarifa. | 
 | `payment_method| Enum | **Obrigatório** | Indica quando a tarifa deve ser paga. As opções válidas são:<br><br> `0` - A tarifa é paga a bordo.<br> `1` - A tarifa deverá ser paga antes do embarque. | 
 | `transfers` | Enum | **Obrigatório** | Indica o número de transfers permitidas nesta tarifa. As opções válidas são:<br><br> `0` - Não são permitidas transfers nesta tarifa.<br> `1` - Os pilotos podem transferir uma vez.<br> `2` - Os pilotos podem transferir duas vezes.<br> vazio- São permitidas transfers ilimitadas. | 
 | `agency_id| ID estrangeiro com referência `agency.agency_id` | **Condicionalmente Obrigatório** | Identifica a agency relevante para uma tarifa.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se diversas agências estiverem definidas em [agency.txt](#agencytxt).<br> - Recomendado de outra forma. | 
 | `transfer_duration` | Inteiro não negativo | Opcional | Período de tempo em segundos antes que uma transferência expire. Quando `transfers`=`0` este campo pode ser usado para indicar por quanto tempo um bilhete é válido ou pode ser deixado em branco. | 
 
### fare_rules.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`*`) 
 
 A tabela [fare_rules.txt](#fare_rulestxt) especifica como as tarifas em [fare_attributes.txt](#fare_attributestxt) aplicam-se a um itinerário. A maioria das estruturas tarifárias usa alguma combinação das seguintes regras: 
 
 * A tarifa depende das estações de origem ou destino. 
 *A tarifa depende das zonas por onde passa o itinerário. 
 *A tarifa depende da rota utilizada pelo itinerário. 
 
 Para exemplos que demonstram como especificar uma estrutura tarifária com [fare_rules.txt](#fare_rulestxt) e [fare_attributes.txt](#fare_attributestxt), consulte [FareExamples](https://web.archive.org/web/20111207224351/https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) no wiki do projeto de código aberto GoogleTransitDataFeed. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `fare_id` | ID estrangeiro referenciando `fare_attributes.fare_id` | **Obrigatório** | Identifica uma classe de tarifa. | 
 | `route_id` | ID estrangeiro referenciando `routes.route_id` | Opcional | Identifica uma rota associada à classe de tarifa. Se existirem diversas routes com os mesmos atributos de tarifa, crie um registro em [fare_rules.txt](#fare_rulestxt) para cada rota.<hr> *Exemplo: Se a classe tarifária "b" for válida na rota "TSW" e "TSE", o arquivo [fare_rules.txt](#fare_rulestxt) conteria estes registros para a classe tarifária:*<br> ` fare_id,route_id`<br> `b,TSW<br> `b,TSE| 
 | `origin_id` | ID estrangeiro referenciando `stops.zone_id` | Opcional | Identifica uma zona de origem. Se uma classe de tarifa tiver múltiplas zonas de origem, crie um registro em [fare_rules.txt](#fare_rulestxt) para cada `origin_id`.<hr> *Exemplo: se a classe tarifária "b" for válida para todas as viagens originadas da zona "2" ou da zona "8", o arquivo [fare_rules.txt](#fare_rulestxt) conteria estes registros para a classe tarifária:*<br> `fare_id,...,origin_id`<br> `b,...,2<br> `b,...,8` | 
 | `destination_id| ID estrangeiro referenciando `stops.zone_id` | Opcional | Identifica uma zona de destino. Se uma classe de tarifa tiver múltiplas zonas de destino, crie um registro em [fare_rules.txt](#fare_rulestxt) para cada `destination_id`.<hr> *Exemplo: Os campos `origin_id` e `destination_id` podem ser usados ​​juntos para especificar que a classe de tarifa "b" é válida para viagens entre as zonas 3 e 4, e para viagens entre as zonas 3 e 5, o [fare_rules.txt](#fare_rulestxt) conteria estes registros para a classe de tarifa:*<br> `fare_id,...,origin_id,destination_id`<br> `b,...,3,4<br> `b,...,3,5` | 
 | `contains_id` | ID estrangeiro referenciando `stops.zone_id` | Opcional | Identifica as zonas nas quais um passageiro entrará ao usar uma determinada classe de tarifa. Usado em alguns sistemas para calcular a classe de tarifa correta.<hr> *Exemplo: se a classe tarifária "c" estiver associada a todas as viagens na rota GRT que passa pelas zonas 5, 6 e 7, o [fare_rules.txt](#fare_rulestxt) conteria estes registros:*<br> `fare_id,route_id,...,contains_id`<br> `c,GRT,...,5`<br> `c,GRT,...,6`<br> `c,GRT,...,7`<br> *Como todas as zonas `contains_id` devem ser correspondidas para que a tarifa seja aplicada, um itinerário que passa pelas zonas 5 e 6, mas não pela zona 7, não teria classe de tarifa "c". Para obter mais detalhes, consulte [https://code.google.com/p/googletransitdatafeed/wiki/FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples) na wiki do projeto GoogleTransitDataFeed.* | 
 
### timeframes.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`*`) 
 
 Usada para descrever tarifas que podem variar de acordo com a hora do dia, o dia da semana ou um determinado dia do ano. Os prazos podem ser associados a produtos tarifários em [fare_leg_rules.txt](#fare_leg_rulestxt).<br> 
 Não deve haver intervalos de tempo sobrepostos para os mesmos valores `timeframe_group_id e `service_id. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `timeframe_group_id` | ID | **Obrigatório** | Identifica um período ou conjunto de prazos. | 
 | `start_time` | Tempo | **Condicionalmente Obrigatório** | Define o início de um período de tempo. O intervalo inclui a hora de início.<br> Valores maiores que `24:00:00` são proibidos. Um valor vazio em `start_time` é considerado `00:00:00`.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se `timeframes.end_time` estiver definido.<br> - **Proibido** caso contrário | 
 | `end_time| Tempo | **Condicionalmente Obrigatório** | Define o final de um período de tempo. O intervalo não inclui o horário de término.<br> Valores maiores que `24:00:00` são proibidos. Um valor vazio em `end_time é considerado `24:00:00`.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se `timeframes.start_time` estiver definido.<br> - **Proibido** caso contrário | 
 | `service_id` | ID estrangeiro referenciando `calendar.service_id ou `calendar_dates.service_id| **Obrigatório** | Identifica um conjunto de datas em que um período está em vigor. | 
 
#### Semântica do horário local do período- Ao avaliar o horário de um evento de tarifa em relação a [timeframes.txt](#timeframestxt), o horário do evento é calculado no horário local usando o fuso horário local, conforme determinado pelo `stop_timezone`, se especificado, da parada ou estação pai do evento de tarifa. Se não for especificado, o fuso horário da agency do feed deverá ser usado. 
 - O “dia atual” é a date atual do horário do evento tarifário, computado em relação ao fuso horário local. O “dia atual” pode ser diferente do dia de serviço da viagem de um trecho tarifário, especialmente para viagens que vão além da meia-noite. 
 - O “horário do dia” do evento tarifário é calculado em relação ao “dia atual” usando a semântica do tipo campo Horário GTFS. 
 
### fare_media.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`fare_media_id`) 
 
 Para descrever as diferentes mídias tarifárias que podem ser empregadas para usar produtos tarifários. Os meios tarifários são suportes físicos ou virtuais utilizados para a representação e/ou validação de um produto tarifário. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `fare_media_id` | ID exclusivo | **Obrigatório** | Identifica uma mídia tarifária. | 
 | `fare_media_name` | Text | Opcional | Nome da mídia tarifária.<br><br> Para mídias tarifárias que são cartões de transporte público (`fare_media_type =2`) ou aplicativos móveis (`fare_media_type =4`), o `fare_media_name` deve ser incluído e deve corresponder ao nome do passageiro usado pelas organizações que os entregam. | 
 | `fare_media_type` | Enum | **Obrigatório** | O tipo de mídia tarifária. As opções válidas são:<br><br> `0` - Nenhum. Usado quando não há mídia tarifária envolvida na compra ou validação de um produto tarifário, como pagamento em dinheiro a um motorista ou cobrador sem bilhete físico fornecido.<br> `1` - Bilhete físico em papel que permite ao passageiro realizar um determinado número de viagens pré-adquiridas ou viagens ilimitadas dentro de um período fixo de tempo.<br> `2` - Cartão de trânsito físico que contém bilhetes, passes ou valor monetário armazenados.<br> `3` - cEMV (Europay, Mastercard e Visa sem contato) como um contêiner de token de circuito aberto para emissão de bilhetes com base em conta.<br> `4` - Aplicativo móvel que armazena cartões de trânsito virtuais, passagens, passes ou valores monetários.| 
 
### fare_products.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`fare_product_id`, `fare_media_id`) 
 
 Usada para descrever a gama de tarifas disponíveis para compra pelos passageiros ou tidos em conta no cálculo da tarifa total para viagens com vários percursos, tais como custos de transferência. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `fare_product_id` | ID | **Obrigatório** | Identifica um produto tarifário ou conjunto de produtos tarifários.<br><br> Vários registros em [fare_products.txt](#fare_productstxt) podem compartilhar o mesmo `fare_product_id`, caso em que todos os registros com esse ID serão recuperados quando referenciados em outro arquivo.<br><br> Vários registros podem compartilhar o mesmo `fare_product_id`, mas com diferentes `fare_media_id`s, indicando vários métodos disponíveis para empregar o produto tarifário, potencialmente a preços diferentes. | 
 | `fare_product_name` | Text | Opcional | O nome do produto tarifário exibido aos passageiros. | 
 | `fare_media_id` | ID estrangeiro referenciando `fare_media.fare_media_id` | Opcional | Identifica uma mídia tarifária que pode ser empregada para usar o produto tarifário durante a viagem. Quando `fare_media_id` está vazio, considera-se que a mídia da tarifa é desconhecida.| 
 | `amount| amount em moeda | **Obrigatório** | O custo do produto tarifário. Pode ser negativo para representar descontos de transferência. Pode ser zero para representar um produto tarifário gratuito. | 
 | `currency| Código da moeda | **Obrigatório** | A currency do custo do produto tarifário. | 
 
 
### fare_leg_rules.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`network_id, from_area_id, to_area_id, from_timeframe_group_id, to_timeframe_group_id, fare_product_id`) 
 
 Regras tarifárias para trechos individuais de viagem. 
 
 As tarifas em [`fare_leg_rules.txt`](#fare_leg_rulestxt) devem ser consultadas filtrando todos os registros do arquivo para encontrar regras que correspondam ao trecho a ser percorrido pelo passageiro. 
 
 Para processar o custo de um trecho: 
 
 1. O arquivo [fare_leg_rules.txt](#fare_leg_rulestxt) deve ser filtrado pelos campos que definem as características da viagem, esses campos são: 
 - `fare_leg_rules.network_id` 
 - `fare_leg_rules.from_area_id` 
 - `fare_leg_rules.to_area_id` 
 - `fare_leg_rules.from_timeframe_group_id` 
 - `fare_leg_rules.to_timeframe_group_id` 
<br/> 
 
 2. Se o trecho corresponder exatamente a um registro em [fare_leg_rules.txt](#fare_leg_rulestxt) com base nas características da viagem, esse registro deverá ser processado para determinar o custo do trecho. Este arquivo trata entradas vazias de duas maneiras: semântica vazia OU prioridade_regra. 
<br/> 
 
 3. Se nenhuma correspondência exata for encontrada E o campo `rule_priority` não existir, então as entradas vazias em `fare_leg_rules.network_id`, `fare_leg_rules.from_area_id` e `fare_leg_rules.to_area_id` devem ser verificadas para processar o custo do trecho: 
 - Uma entrada vazia em `fare_leg_rules.network_id` corresponde a todas as redes definidas em [routes.txt](#routestxt) ou [networks.txt](#networkstxt) excluindo as listadas em `fare_leg_rules.network_id` 
 
 - Uma entrada vazia em `fare_leg_rules.from_area_id` corresponde a todas as áreas definidas em `areas.area_id` excluindo as listadas em `fare_leg_rules.from_area_id` 
 - Uma entrada vazia em `fare_leg_rules.to_area_id` corresponde para todas as áreas definidas em `areas.area_id excluindo as listadas em `fare_leg_rules.to_area_id 
<br/> 
 
 4. Se o campo `rule_priority` existir, então- Uma entrada vazia em `fare_leg_rules.network_id` indica que a rede do trecho não afeta a correspondência desta regra. 
 - Uma entrada vazia em `fare_leg_rules.from_area_id` indica que a área de departure do trecho não afeta o cumprimento desta regra. 
 - Uma entrada vazia em `fare_leg_rules.to_area_id` indica que a área de arrival do trecho não afeta a correspondência desta regra. 
<br/> 
 
 5. Se o trecho não atender a nenhuma das regras descritas acima, a tarifa é desconhecida. 
 
<br/> 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `leg_group_id` | ID | Opcional | Identifica um grupo de entradas em [fare_leg_rules.txt](#fare_leg_rulestxt).<br><br> Usado para descrever regras de transferência de tarifas entre `fare_transfer_rules.from_leg_group_id` e `fare_transfer_rules.to_leg_group_id`.<br><br> Múltiplas entradas em [fare_leg_rules.txt](#fare_leg_rulestxt) podem pertencer ao mesmo `fare_leg_rules.leg_group_id`.<br><br> A mesma entrada em [fare_leg_rules.txt](#fare_leg_rulestxt) (não incluindo `fare_leg_rules.leg_group_id`) não deve pertencer a vários `fare_leg_rules.leg_group_id`.| 
 | `network_id| ID estrangeiro referenciando `routes.network_id` ou `networks.network_id`| Opcional | Identifica uma rede de rotas que se aplica à regra do trecho tarifário.<br><br> Se o campo `rule_priority` não existir E não houver valores `fare_leg_rules.network_id` correspondentes ao `network_id` que está sendo filtrado, `fare_leg_rules.network_id` vazio será correspondido por padrão.<br><br> Uma entrada vazia em `fare_leg_rules.network_id` corresponde a todas as redes definidas em [routes.txt](#routestxt) ou [networks.txt](#networkstxt) excluindo aquelas listadas em `fare_leg_rules.network_id`<br><br> Se o campo `rule_priority` existir no arquivo, um `fare_leg_rules.network_id` vazio indica que a rede de rotas do trecho não afeta a correspondência desta regra. | 
 | `from_area_id` | ID estrangeiro referenciando `areas.area_id| Opcional | Identifica uma área de departure .<br><br> Se o campo `rule_priority` não existir E não houver valores `fare_leg_rules.from_area_id` correspondentes ao `area_id` que está sendo filtrado, `fare_leg_rules.from_area_id` vazio será correspondido por padrão.<br><br> Uma entrada vazia em `fare_leg_rules.from_area_id` corresponde a todas as áreas definidas em `areas.area_id` excluindo aquelas listadas em `fare_leg_rules.from_area_id`<br><br> Se o campo `rule_priority` existir no arquivo, um `fare_leg_rules.from_area_id` vazio indica que a área de departure do trecho não afeta a correspondência desta regra. | 
 | `to_area_id| ID estrangeiro referenciando `areas.area_id| Opcional | Identifica uma área de arrival .<br><br> Se o campo `rule_priority` não existir E não houver valores `fare_leg_rules.to_area_id` correspondentes ao `area_id` que está sendo filtrado, `fare_leg_rules.to_area_id` vazio será correspondido por padrão.<br><br> Uma entrada vazia em `fare_leg_rules.to_area_id` corresponde a todas as áreas definidas em `areas.area_id` excluindo aquelas listadas em `fare_leg_rules.to_area_id`<br><br> Se o campo `rule_priority` existir no arquivo, um `fare_leg_rules.to_area_id` vazio indica que a área de arrival do trecho não afeta a correspondência desta regra. | 
 | `from_timeframe_group_id` | ID estrangeiro referenciando `timeframes.timeframe_group_id` | Opcional | Define o prazo para o evento de validação de tarifa no início do trecho tarifário.<br><br> O “horário de início” do trecho tarifário é o horário em que o evento está programado para ocorrer. Por exemplo, o horário pode ser o horário programado de departure de um ônibus no início de um trecho tarifário onde o passageiro embarca e valida sua tarifa. Para a semântica de correspondência de regras abaixo, o horário de início é calculado na hora local, conforme determinado pela [Semântica de horário local](#timeframe-local-time-semantics) de [timeframes.txt](#timeframestxt). A parada ou estação do evento de departure do trecho tarifário deve ser usada para resolução de fuso horário, quando apropriado.<br><br> Para uma regra de trecho tarifário que especifica um `from_timeframe_group_id, essa regra corresponderá a um trecho específico se t

aqui existe pelo menos um registro em [timeframes.txt](#timeframestxt) onde todas as condições a seguir são verdadeiras<br> - O valor de `timeframe_group_id é igual ao valor de `from_timeframe_group_id.<br> - O conjunto de dias identificado pelo `service_id` do registro contém o “dia atual” do horário de início do trecho tarifário.<br> - A “hora do dia” do horário de início do trecho tarifário é maior ou igual ao valor `timeframes.start_time` do registro e menor que o valor `timeframes.end_time`.<br><br> Um `fare_leg_rules.from_timeframe_group_id` vazio indica que o horário de início do trecho não afeta a correspondência desta regra. | 
 | `to_timeframe_group_id` | ID estrangeiro referenciando `timeframes.timeframe_group_id` | Opcional | Define o prazo para o evento de validação de tarifa no final do trecho tarifário.<br><br> O “horário de término” do trecho tarifário é o horário em que o evento está programado para ocorrer. Por exemplo, o horário pode ser o horário programado de arrival de um ônibus no final de um trecho tarifário onde o passageiro desce e valida sua tarifa. Para a semântica de correspondência de regras abaixo, o horário de término é calculado na hora local, conforme determinado pela [Semântica de horário local](#timeframe-local-time-semantics) de [timeframes.txt](#timeframestxt). A parada ou estação do evento de arrival do trecho tarifário deve ser usada para resolução de fuso horário, quando apropriado.<br><br> Para uma regra de trecho de tarifa que especifica um `to_timeframe_group_id`, essa regra corresponderá a um trecho específico se existir pelo menos um registro em [timeframes.txt](#timeframestxt) onde todas as condições a seguir são verdadeiras<br> - O valor de `timeframe_group_id é igual ao valor de `to_timeframe_group_id.<br> - O conjunto de dias identificado pelo `service_id` do registro contém o “dia atual” do horário de término do trecho tarifário.<br> - A “hora do dia” do horário de término do trecho tarifário é maior ou igual ao valor `timeframes.start_time` do registro e menor que o valor `timeframes.end_time`.<br><br> Um `fare_leg_rules.to_timeframe_group_id` vazio indica que o horário de término do trecho não afeta a correspondência desta regra. | 
 | `fare_product_id` | ID estrangeiro referenciando `fare_products.fare_product_id` | **Obrigatório** | O produto tarifário necessário para percorrer o trecho. | 
 | `rule_priority` | Inteiro não negativo | Opcional | Define a ordem de prioridade na qual as regras de correspondência são aplicadas aos trechos, permitindo que certas regras tenham precedência sobre outras. Quando múltiplas entradas em `fare_leg_rules.txt` corresponderem, a regra ou conjunto de regras com o valor mais alto para `rule_priority` será selecionado.<br><br> Um valor vazio para `rule_priority` é tratado como zero. | 
 
### fare_transfer_rules.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`from_leg_group_id, to_leg_group_id, fare_product_id, transfer_count, duration_limit`) 
 
 Regras tarifárias para transfers entre trechos de viagem definido em [`fare_leg_rules.txt`](#fare_leg_rulestxt). 
 
 Para processar o custo de uma viagem com vários trechos: 
 
 1. Os grupos de trechos tarifários aplicáveis ​​definidos em `fare_leg_rules.txt` devem ser determinados para todos os trechos individuais da viagem com base na jornada do passageiro. 
 2. O arquivo [fare_transfer_rules.txt](#fare_transfer_rulestxt) deverá ser filtrado pelos campos que definem as características da transferência, esses campos são: 
 - `fare_transfer_rules.from_leg_group_id` 
 - `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 
 3. Se a transferência corresponder exatamente a um registro em [fare_transfer_rules.txt](#fare_transfer_rulestxt) com base nas características da transferência, então esse registro deverá ser processado para determinar o custo da transferência. 
 4. Se nenhuma correspondência exata for encontrada, então as entradas vazias em `from_leg_group_id` ou em `to_leg_group_id` devem ser verificadas para processar o custo de transferência: 
 - Uma entrada vazia em `fare_transfer_rules.from_leg_group_id` corresponde a todos os grupos de trechos definidos em `fare_leg_rules.leg_group_id` excluindo os listados em `fare_transfer_rules.from_leg_group_id` 
 - Uma entrada vazia em `fare_transfer_rules.to_leg_group_id` corresponde a todos os grupos de trechos definidos em `fare_leg_rules.leg_group_id` excluindo os listados em `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 5. Se a transferência não atender a nenhuma das regras descritas acima, não há acordo de transferência e os trechos são considerados separados. 
 
<br/> 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `from_leg_group_id` | ID estrangeiro referenciando `fare_leg_rules.leg_group_id` | Opcional | Identifica um grupo de regras de trecho tarifário pré-transferência.<br><br> Se não houver valores `fare_transfer_rules.from_leg_group_id` correspondentes ao `leg_group_id` que está sendo filtrado, `fare_transfer_rules.from_leg_group_id` vazio será correspondido por padrão.<br><br> Uma entrada vazia em `fare_transfer_rules.from_leg_group_id` corresponde a todos os grupos de trechos definidos em `fare_leg_rules.leg_group_id` excluindo aqueles listados em `fare_transfer_rules.from_leg_group_id`| 
 | `to_leg_group_id` | ID estrangeiro referenciando `fare_leg_rules.leg_group_id` | Opcional | Identifica um grupo de regras de trecho tarifário pós-transferência.<br><br> Se não houver valores `fare_transfer_rules.to_leg_group_id` correspondentes ao `leg_group_id` que está sendo filtrado, `fare_transfer_rules.to_leg_group_id` vazio será correspondido por padrão.<br><br> Uma entrada vazia em `fare_transfer_rules.to_leg_group_id` corresponde a todos os grupos de trechos definidos em `fare_leg_rules.leg_group_id` excluindo aqueles listados em `fare_transfer_rules.to_leg_group_id` | 
 | `transfer_count| Inteiro diferente de zero | **Condicionalmente Proibido** | Define a quantas transfers consecutivas a regra de transferência pode ser aplicada.<br><br> As opções válidas são:<br> `-1` - Sem limite.<br> `1` ou mais- Define quantas transfers a regra de transferência pode abranger.<br><br> Se uma subjornada corresponder a vários registros com `transfer_count diferentes, então a regra com o `transfer_count mínimo que seja maior ou igual à contagem de transferência atual da subjornada deve ser selecionada.<br><br> Condicionalmente Proibido:<br> - **Proibido** se `fare_transfer_rules.from_leg_group_id` não for igual a `fare_transfer_rules.to_leg_group_id`.<br> - **Obrigatório** se `fare_transfer_rules.from_leg_group_id` for igual a `fare_transfer_rules.to_leg_group_id`. | 
 | `duration_limit| Inteiro positivo | Opcional | Define o limite de duração da transferência.<br><br> Deve ser expresso em incrementos inteiros de segundos.<br><br> Se não houver limite de duração, `fare_transfer_rules.duration_limit` deverá estar vazio. | 
 | `duration_limit_type| Enum | **Condicionalmente Obrigatório** | Define o início e o fim relativos de `fare_transfer_rules.duration_limit`.<br><br> As opções válidas são:<br> `0` - Entre a validação da tarifa de departure do trecho atual e a validação da tarifa de arrival do trecho seguinte.<br> `1` - Entre a validação da tarifa de departure do trecho atual e a validação da tarifa de departure do trecho seguinte.<br> `2` - Entre a validação da tarifa de arrival do trecho atual e a validação da tarifa de departure do trecho seguinte.<br> `3` - Entre a validação da tarifa de arrival do trecho atual e a validação da tarifa de arrival do trecho seguinte.<br><br> Condicionalmente obrigatório:<br> - **Obrigatório** se `fare_transfer_rules.duration_limit` estiver definido.<br> - **Proibido** se `fare_transfer_rules.duration_limit` estiver vazio. | 
 | `fare_transfer_type` | Enum | **Obrigatório** | Indica o método de processamento de custos de transferência entre trechos em uma viagem:<br> ![](../../assets/2-leg.svg)<br> As opções válidas são:<br> `0` - perna de origem `fare_leg_rules.fare_product_id` mais `fare_transfer_rules.fare_product_id`; A + AB.<br> `1` - Do trecho `fare_leg_rules.fare_product_id` mais `fare_transfer_rules.fare_product_id` mais até o trecho `fare_leg_rules.fare_product_id`; A + AB + B.<br> `2` - `fare_transfer_rules.fare_product_id`; AB.<br><br> Interações de processamento de custos entre múltiplas transfers em uma jornada:<br> ![](../../assets/3-leg.svg)<br><table><thead><tr><th> `fare_transfer_type`</th><th> Processando A > B</th><th> Processando B > C</th></tr></thead><tbody><tr><td> `0`</td><td> A + AB</td><td> S + BC</td></tr><tr><td> `1`</td><td> A +AB +B</td><td> S + BC + C</td></tr><tr><td> `2`</td><td> AB</td><td> S + BC</td></tr></tbody></table> Onde S indica o custo total processado da(s) etapa(s) e transferência(s) anteriores. | 
 | `fare_product_id` | ID estrangeiro referenciando `fare_products.fare_product_id` | Opcional | O produto tarifário necessário para transferência entre dois trechos tarifários. Se estiver vazio, o custo da regra de transferência será 0.| 
 
 
### areas.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`area_id`) 
 
 Define identificadores de área. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `area_id` | ID exclusivo | **Obrigatório** | Identifica uma área. Deve ser exclusivo em [areas.txt](#areastxt). | 
 | `area_name| Text | **Opcional** | O nome da área conforme exibido ao piloto. | 
 
### stop_areas.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`*`) 
 
 Atribui stops de [stops.txt](#stopstxt) às áreas. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `area_id` | ID estrangeiro referenciando `areas.area_id| **Obrigatório** | Identifica uma área à qual pertencem um ou vários `stop_id` s. O mesmo `stop_id` pode ser definido em muitos `area_id`s. | 
 | `stop_id` | ID estrangeiro referenciando `stops.stop_id` | **Obrigatório** | Identifica uma parada. Se uma estação (ou seja, uma parada com `stops.location_type=1`) for definida neste campo, presume-se que todas as suas plataformas (ou seja, todas as stops com `stops.location_type=0` que tenham esta estação definida como `stops.parent_station`) fazem parte da mesma área. Este comportamento pode ser substituído atribuindo plataformas a outras áreas. | 
 
### redes.txt 
 
 Arquivo: **Condicionalmente Proibido** 
 
 Chave primária (`network_id`) 
 
 Define identificadores de rede que se aplicam às regras de trecho tarifário. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `network_id| ID exclusivo | **Obrigatório** | Identifica uma rede. Deve ser exclusivo em [networks.txt](#networkstxt). | 
 | `network_name| Text | **Opcional** | O nome da rede que aplica as regras de trecho tarifário, conforme usado pela agency local e seus passageiros. 
 
### route_networks.txt 
 
 Arquivo: **Condicionalmente Proibido** 
 
 Chave primária (`route_id`) 
 
 Atribui routes de [routes.txt](#routestxt) para redes. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `network_id| ID estrangeiro referenciando `networks.network_id| **Obrigatório** | Identifica uma rede à qual pertencem um ou vários `route_id` s. Um `route_id` só pode ser definido em um `network_id`. | 
 | `route_id` | ID estrangeiro referenciando `routes.route_id` | **Obrigatório** | Identifica uma rota. | 
 
### shapes.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`shape_id`, `shape_pt_sequence`) 
 
 As formas descrevem o caminho que um vehicle percorre ao longo de um alinhamento de rota e são definidos no arquivo shapes.txt. As formas estão associadas às viagens e consistem em uma sequência de pontos pelos quais o vehicle passa em ordem. As formas não precisam interceptar exatamente a localização das paradas, mas todas as paradas em uma viagem devem estar a uma pequena distância da shape dessa viagem, ou seja, próximas aos segmentos de linha reta que conectam os pontos da shape. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `shape_id` | ID | **Obrigatório** | Identifica uma shape. | 
 | `shape_pt_lat` | Latitude | **Obrigatório** | Latitude de um ponto de shape. Cada registro em [shapes.txt](#shapestxt) representa um ponto de shape usado para definir a shape. | 
 | `shape_pt_lon` | Longitude | **Obrigatório** | Longitude de um ponto de shape. | 
 | `shape_pt_sequence` | Inteiro não negativo | **Obrigatório** | Sequência na qual os pontos da shape se conectam para formar a shape. Os valores devem aumentar ao longo da viagem, mas não precisam ser consecutivos.<hr> *Exemplo: Se a shape "A_shp" tiver três pontos em sua definição, o arquivo [shapes.txt](#shapestxt) poderá conter estes registros para definir a shape:*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence`<br> `A_shp,37.61956,-122.48161,0`<br> `A_shp,37.64430,-122.41070,6`<br> `A_shp,37.65863,-122.30839,11` | 
 | `shape_dist_traveled` | float não negativa | Opcional | Distância real percorrida ao longo da shape desde o primeiro ponto da shape até o ponto especificado neste registro. Usado por planejadores de viagens para mostrar a parte correta da shape em um mapa. Os valores devem aumentar junto com `shape_pt_sequence`; eles não devem ser usados ​​para mostrar deslocamento reverso ao longo de uma rota. As unidades de distância devem ser consistentes com aquelas usadas em [stop_times.txt](#stop_timestxt).<br><br> Recomendado para routes que possuem looping ou inlining (o vehicle cruza ou percorre a mesma parte do alinhamento em uma viagem). <br><img src="../../../assets/inlining.svg" width=200px style="display: block; margin-left: auto; margin-right: auto;"><br> Se um vehicle refaz ou cruza o alinhamento da rota em pontos no curso de uma viagem, `shape_dist_traveled` é importante para esclarecer como partes dos pontos na linha [shapes.txt](#shapestxt) correspondem aos registros em [stop_times.txt](#stop_timestxt).<hr> *Exemplo: Se um ônibus viaja ao longo dos três pontos definidos acima para A_shp, os valores adicionais `shape_dist_traveled` (mostrados aqui em quilômetros) ficariam assim:*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shape_dist_traveled`<br> `A_shp,37.61956,-122.48161,0,0<br> `A_shp,37.64430,-122.41070,6,6.8310<br> `A_shp,37.65863,-122.30839,11,15.8765` | 
 
### frequencies.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`trip_id`, `start_time`) 
 
 [Frequências.txt](#frequenciestxt) representa viagens que operam em intervalos regulares (tempo entre viagens). Este arquivo pode ser usado para representar dois tipos diferentes de serviço. 
 
 * Atendimento baseado em frequência (`exact_times`=`0`) em que o atendimento não segue horário fixo ao longo do dia. Em vez disso, os operadores tentam manter estritamente intervalos predeterminados para viagens. 
 * Uma representação compactada de serviço baseado em programação (`exact_times`= `1`) que tem exatamente o mesmo intervalo para viagens em períodos de tempo especificados. Nos serviços baseados em horários, os operadores tentam cumprir rigorosamente um horário. 
 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `trip_id` | ID estrangeiro com referência a `trips.trip_id` | **Obrigatório** | Identifica uma viagem à qual se aplica o intervalo de serviço especificado. | 
 | `start_time` | Tempo | **Obrigatório** | Hora em que o primeiro vehicle sai da primeira parada da viagem com o intervalo especificado. | 
 | `end_time| Tempo | **Obrigatório** | Hora em que o serviço muda para um intervalo diferente (ou cessa) na primeira parada da viagem. | 
 | `headway_secs` | Inteiro positivo | **Obrigatório** | Tempo, em segundos, entre partidas da mesma parada (intervalo) da viagem, durante o intervalo de tempo especificado por `start_time` e `end_time. Vários intervalos podem ser definidos para a mesma viagem, mas não devem se sobrepor. Novos intervalos podem começar no momento exato em que o intervalo anterior termina. | 
 | `exact_times` | Enum | Opcional | Indica o tipo de serviço para uma viagem. Consulte a descrição do arquivo para obter mais informações. As opções válidas são:<br><br> `0` ou vazio- viagens baseadas em frequência.<br> `1` - Viagens baseadas em programação com exatamente o mesmo intervalo ao longo do dia. Neste caso o valor `end_time deve ser maior que a última viagem desejada `start_time` mas menor que o último start_time desejado + `headway_secs`. | 
 
### transfers.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`from_stop_id`, `to_stop_id`, `from_trip_id`, `to_trip_id`, `from_route_id`, `to_route_id`) 
 
 Ao calcular um itinerário, os aplicativos que consomem GTFS interpolam as transfers com base no tempo permitido e na proximidade da parada. [Transfers.txt](#transferstxt) especifica regras e substituições adicionais para transfers selecionadas. 
 
 Os campos `from_trip_id`, `to_trip_id`, `from_route_id` e `to_route_id` permitem ordens mais altas de especificidade para regras de transferência. Junto com `from_stop_id` e `to_stop_id`, a classificação de especificidade é a seguinte: 
 
 1. Ambos `trip_id` s definidos: `from_trip_id` e `to_trip_id`. 
 2. Um conjunto `trip_id` e `route_id` definido: (`from_trip_id` e `to_route_id`) ou (`from_route_id` e `to_trip_id`). 
 3. Um `trip_id` definido: `from_trip_id ou `to_trip_id. 
 4. Ambos `route_id` s definidos: `from_route_id` e `to_route_id`. 
 5. Um `route_id` definido: `from_route_id` ou `to_route_id`. 
 6. Apenas `from_stop_id e `to_stop_id definidos: nenhum campo relacionado à rota ou viagem definido. 
 
 Para um determinado par ordenado de viagem de chegada e viagem de partida, escolhe-se o transfer com maior especificidade que se aplica entre estas duas viagens. Para qualquer par de viagens, não deve haver duas transfers com especificidade igualmente máxima que possam ser aplicadas. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `from_stop_id| ID estrangeiro referenciando `stops.stop_id` | **Condicionalmente Obrigatório** | Identifica uma parada ou estação onde começa uma conexão entre routes. Se este campo se referir a uma estação, a regra de transferência se aplica a todas as suas stops filhas. Fazer referência a uma estação é proibido para `transfer_types` 4 e 5. | 
 | `to_stop_id| ID estrangeiro referenciando `stops.stop_id` | **Condicionalmente Obrigatório** | Identifica uma parada ou estação onde termina uma conexão entre routes. Se este campo se referir a uma estação, a regra de transferência se aplica a todas as stops secundárias. Fazer referência a uma estação é proibido para `transfer_types` 4 e 5. | 
 | `from_route_id` | ID estrangeiro referenciando `routes.route_id` | Opcional | Identifica uma rota onde uma conexão começa.<br><br> Se `from_route_id` for definido, a transferência será aplicada à viagem de chegada na rota para o `from_stop_id` fornecido.<br><br> Se `from_trip_id` e `from_route_id` forem definidos, `trip_id` deve pertencer a `route_id` e `from_trip_id` terá precedência. | 
 | `to_route_id` | ID estrangeiro referenciando `routes.route_id` | Opcional | Identifica uma rota onde uma conexão termina.<br><br> Se `to_route_id` for definido, a transferência será aplicada à viagem de partida na rota para o `to_stop_id` fornecido.<br><br> Se `to_trip_id` e `to_route_id` forem definidos, o `trip_id` deve pertencer ao `route_id` e `to_trip_id` terá precedência. | 
 | `from_trip_id` | ID estrangeiro com referência a `trips.trip_id` | **Condicionalmente Obrigatório** | Identifica uma viagem onde começa uma conexão entre routes .<br><br> Se `from_trip_id` for definido, a transferência será aplicada à viagem de chegada para o `from_stop_id` fornecido.<br><br> Se `from_trip_id` e `from_route_id` forem definidos, `trip_id` deve pertencer a `route_id` e `from_trip_id` terá precedência. OBRIGATÓRIO se `transfer_type for `4` ou `5`. | 
 | `to_trip_id| ID estrangeiro com referência a `trips.trip_id` | **Condicionalmente Obrigatório** | Identifica uma viagem onde termina uma conexão entre routes .<br><br> Se `to_trip_id` for definido, a transferência será aplicada à viagem de partida para o `to_stop_id` fornecido.<br><br> Se `to_trip_id` e `to_route_id` forem definidos, o `trip_id` deve pertencer ao `route_id` e `to_trip_id` terá precedência. OBRIGATÓRIO se `transfer_type for `4` ou `5`. | 
 | `transfer_type` | Enum | **Obrigatório** | Indica o tipo de conexão para o par especificado (`from_stop_id`, `to_stop_id`). As opções válidas são:<br><br> `0` ou vazio- Ponto de transferência recomendado entre routes.<br> `1` - Ponto de transferência cronometrado entre duas routes. Espera-se que o vehicle que parte espere pelo que chega e deixe tempo suficiente para que o passageiro faça a transferência entre as routes.<br> `2` - A transferência requer um amount mínimo entre a arrival e a departure para garantir a conexão. O tempo necessário para a transferência é especificado por `min_transfer_time.<br> `3` - Não são possíveis transferências entre routes no local.<br> `4` - Os passageiros podem fazer transferência de uma viagem para outra permanecendo a bordo do mesmo vehicle (uma “transferência no assento”). Mais detalhes sobre esse tipo de transfer [abaixo](#linked-trips).<br> `5` - Não são permitidas transfers em assento entre viagens sequenciais. O passageiro deverá descer do vehicle e embarcar novamente. Mais detalhes sobre esse tipo de transfer [abaixo](#linked-trips). | 
 | `min_transfer_time| Inteiro não negativo | Opcional | Quantidade de tempo, em segundos, que deve estar disponível para permitir uma transferência entre routes nas stops especificadas. O `min_transfer_time deve ser suficiente para permitir que um passageiro típico se mova entre as duas stops, incluindo tempo de buffer para permitir variações de horário em cada rota. | 
 
#### Viagens vinculadas 
 
 O seguinte se aplica a `transfer_type=4` e `=5`, que são usados ​​para vincular viagens, com ou sem transfers em assentos. 
 
 As viagens interligadas DEVEM ser realizadas no mesmo vehicle. O vehicle PODE ser acoplado ou desacoplado de outros veículos. 
 
 Se uma transferência de viagens vinculadas e um block_id forem fornecidos e produzirem resultados conflitantes, a transferência de viagens vinculadas deverá ser usada. 
 
 A última parada de `from_trip_id DEVE ser geograficamente próxima à primeira parada de `to_trip_id, e o último horário de arrival de `from_trip_id DEVE ser anterior, mas próximo ao primeiro horário de departure de `to_trip_id. O último horário de arrival de `from_trip_id` PODE ser posterior ao primeiro horário de departure de `to_trip_id` caso a viagem `to_trip_id` ocorra no dia de serviço subsequente. 
 
 As viagens PODEM ser vinculadas 1 para 1 no caso normal, mas também PODEM ser vinculadas 1 para n, n para 1 ou n para n para representar continuações de viagem mais complexas. Por exemplo, duas viagens de trem (viagem A e viagem B no diagrama abaixo) podem se fundir em uma única viagem de trem (viagem C) após uma operação de acoplamento de vehicle em uma estação comum: 
 
 - Em uma operação 1 para n continuação, o `trips.service_id para cada `to_trip_id DEVE ser idêntico. 
 - Em uma continuação n para 1, o `trips.service_id para cada `from_trip_id DEVE ser idêntico. 
 - as continuações n-para-n devem respeitar ambas as restrições. 
 - As viagens poderão ser interligadas como parte de múltiplas continuações distintas, desde que o `trip.service_id` NÃO DEVE se sobrepor em nenhum dia de serviço. 
 
<pre> 
 Viagem A 
 ───────────────────\ 
 \ Viagem C 
 ───────────── 
 Viagem B/
 ───────────────────/
</pre> 
 
### pathways.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`pathway_id`) 
 
 Arquivos [pathways.txt](#pathwaystxt) e [levels.txt](#levelstxt) usam uma representação gráfica para descrever estações de metrô ou trem, com nós representando locais e arestas representando pathways. 
 
 Para navegar da entrada/saída da estação (um nó representado como um local com `location_type=2`) até uma plataforma (um nó representado como um local com `location_type=0` ou vazio), o passageiro se moverá através de passarelas, portões de passagem, escadas e outras arestas representadas como pathways. Nós genéricos (nós representados com `location_type=3`) podem ser usados ​​para conectar pathways em uma estação. 
 
 Os percursos devem ser definidos exaustivamente numa estação. Se algum pathways for definido, presume-se que todos os pathways ao longo da estação estejam representados. Portanto, aplicam-se as seguintes diretrizes: 
 
 - Sem locais pendentes: Se qualquer local dentro de uma estação tiver um caminho, então todos os locais dentro dessa estação deverão ter pathways, exceto para plataformas que possuem áreas de embarque (`location_type=4`, veja a diretriz abaixo). 
 - Não há pathways para uma plataforma com áreas de embarque: Uma plataforma (`location_type=0` ou vazia) que possui áreas de embarque (`location_type=4`) é tratada como um objeto pai e não como um ponto. Nestes casos, a plataforma não deve ter pathways atribuídos. Todos os pathways deverão ser atribuídos para cada uma das áreas de embarque da plataforma. 
 - Não há plataformas bloqueadas: Cada plataforma (`location_type=0` ou vazia) ou área de embarque (`location_type=4`) deve estar conectada a pelo menos uma entrada/saída (`location_type=2`) através de alguma cadeia de pathways. As estações que não permitem um caminho para o exterior da estação a partir de uma determinada plataforma são raras. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `pathway_id` | ID exclusivo | **Obrigatório** | Identifica um caminho. Usado pelos sistemas como um identificador interno do registro. Deve ser exclusivo no conjunto de dados.<br><br> pathways diferentes podem ter os mesmos valores para `from_stop_id e `to_stop_id.<hr> _Exemplo: Quando duas escadas rolantes estão lado a lado em direções opostas, ou quando um conjunto de escadas e um elevador vão do mesmo lugar para o mesmo lugar, diferentes `pathway_id podem ter os mesmos valores `from_stop_id e `to_stop_id| 
 | `from_stop_id` | ID estrangeiro referenciando `stops.stop_id` | **Obrigatório** | Local onde o caminho começa.<br><br> Deve conter um `stop_id` que identifica uma plataforma (`lo

cation_type=0` ou vazio), entrada/saída (`location_type=2`), nó genérico (`location_type=3`) ou área de embarque (`location_type=4`).<br><br> Valores para `stop_id` que identificam estações (`location_type=1`) são proibidos.| 
 | `to_stop_id| ID estrangeiro referenciando `stops.stop_id` | **Obrigatório** | Local onde o caminho termina.<br><br> Deve conter um `stop_id` que identifique uma plataforma (`location_type=0` ou vazia), entrada/saída (`location_type=2`), nó genérico (`location_type=3`) ou área de embarque (`location_type=4`) .<br><br> Valores para `stop_id` que identificam estações (`location_type=1`) são proibidos.| 
 | `pathway_mode` | Enum | **Obrigatório** | Tipo de caminho entre o par especificado (`from_stop_id`, `to_stop_id`). As opções válidas são:<br><br> `1` - Passarela.<br> `2` - Escadas.<br> `3` - Calçada móvel/viajante.<br> `4` - Escada rolante.<br> `5` - Elevador.<br> `6` - Portão de tarifa (ou portão de pagamento): Caminho que atravessa uma área da estação onde é necessário o comprovante de pagamento para atravessar. As barreiras tarifárias podem separar as áreas pagas da estação das não pagas ou separar diferentes áreas de pagamento dentro da mesma estação umas das outras. Essas informações podem ser usadas para evitar o encaminhamento de passageiros pelas estações usando atalhos que require que os passageiros fizessem pagamentos desnecessários, como orientar um passageiro a caminhar por uma plataforma do metrô para chegar a uma via de ônibus.<br> `7`- Portão de saída: Um caminho que sai de uma área paga para uma área não paga onde não é necessário passar comprovante de pagamento.| 
 | `is_bidirectional| Enum | **Obrigatório** | Indica a direção que o caminho pode ser tomado:<br><br> `0` - Caminho unidirecional que só pode ser usado de `from_stop_id` para `to_stop_id`.<br> `1` - Caminho bidirecional que pode ser usado em ambas as direções.<br><br> As portas de saída (`pathway_mode=7) não devem ser bidirecionais.| 
 | `comprimento` | float não negativa | Opcional | Comprimento horizontal em metros do caminho desde o local de origem (definido em `from_stop_id`) até o local de destino (definido em `to_stop_id`).<br><br> Este campo é recomendado para passarelas (`pathway_mode=1), portões tarifários (`pathway_mode=6) e portões de saída (`pathway_mode=7).| 
 | `traversal_time| Inteiro positivo | Opcional | Tempo médio em segundos necessário para percorrer o caminho desde o local de origem (definido em `from_stop_id) até o local de destino (definido em `to_stop_id).<br><br> Este campo é recomendado para calçadas móveis (`pathway_mode=3), escadas rolantes (`pathway_mode=4) e elevadores (`pathway_mode=5).| 
 | `stair_count` | Inteiro não nulo | Opcional | Número de escadas do caminho.<br><br> Um `stair_count positivo implica que o ciclista sobe de `from_stop_id para `to_stop_id. E um `stair_count negativo implica que o ciclista desce de `from_stop_id para `to_stop_id.<br><br> Este campo é recomendado para escadas (`pathway_mode=2).<br><br> Se apenas uma contagem estimada de escadas puder ser fornecida, recomenda-se aproximadamente 15 escadas para 1 andar.| 
 | `max_slope| Float | Opcional | Razão de inclinação máxima do caminho. As opções válidas são:<br><br> `0` ou vazio- Sem inclinação.<br> `Float` - Razão de inclinação do caminho, positiva para cima, negativa para baixo.<br><br> Este campo só deve ser utilizado com passarelas (`pathway_mode=1) e calçadas móveis (`pathway_mode=3).<hr> _Exemplo: Nos EUA, 0,083 (também escrito 8,3%) é a razão de inclinação máxima para cadeiras de rodas movidas manualmente, o que significa um aumento de 0,083m (ou seja, 8,3cm) para cada 1m._| 
 | `min_width| float positiva | Opcional | Largura mínima do caminho em metros.<br><br> Este campo é recomendado se a largura mínima for inferior a 1 metro.| 
 | `signposted_as` | Text | Opcional | Texto voltado para o público em sinalização física visível para os passageiros.<br><br> Pode ser usado para fornecer instruções de texto aos passageiros, como ’siga as placas para’. O texto em `singposted_as` deve aparecer exatamente como está impresso nas placas.<br><br> Quando a sinalização física for multilíngue, este campo poderá ser preenchido e traduzido seguindo o exemplo de `stops.stop_name` na definição de campo de `feed_info.feed_lang`.| 
 | `reversed_signposted_as` | Text | Opcional | O mesmo que `signposted_as`, mas quando o caminho é usado de `to_stop_id` para `from_stop_id`.| 
 
### levels.txt 
 
 Arquivo: **Condicionalmente Obrigatório** 
 
 Chave primária (`level_id`) 
 
 Descreve os níveis em uma estação. Útil em conjunto com [pathways.txt](#pathwaystxt). 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `level_id| ID exclusivo | **Obrigatório** | Identifica um nível em uma estação.| 
 | `level_index| Float | **Obrigatório** | Índice numérico do nível que indica sua position relativa.<br><br> O nível do solo deve ter índice `0`, com os níveis acima do solo indicados por índices positivos e os níveis abaixo do solo por índices negativos.| 
 | `level_name| Text | Opcional | Nome do nível visto pelo piloto dentro do prédio ou estação.<hr> _Exemplo: Pegue o elevador até "Mezanino" ou "Plataforma" ou "-1"._| 
 
### location_groups.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`location_group_id`) 
 
 Define grupos de locais, que são grupos de stops onde um passageiro pode solicitar retirada ou entrega. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |----------|----|------------|-----------| 
 | `location_group_id` | ID exclusivo | **Obrigatório** | Identifica um grupo de locais. O ID deve ser exclusivo em todos os valores `stops.stop_id`, locations.geojson `id` e `location_groups.location_group_id`.<br><br> Um grupo de locais é um grupo de stops que, juntas, indicam locais onde um passageiro pode solicitar embarque ou desembarque. | 
 | `local_grupo_nome` | Text | Opcional | O nome do grupo de locais exibido ao passageiro. | 
 
### location_group_stops.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`*`) 
 
 Atribui stops de stops.txt a grupos de locais. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |----------|----|------------|-----------| 
 | `location_group_id` | ID estrangeiro referenciando `location_groups.location_group_id` | **Obrigatório** | Identifica um grupo de locais ao qual pertencem um ou vários `stop_id` s. O mesmo `stop_id` pode ser definido em muitos `location_group_id`s. | 
 | `stop_id` | ID estrangeiro referenciando `stops.stop_id` | **Obrigatório** | Identifica uma parada pertencente ao grupo de locais. | 
 
 
### locations.geojson 
 
 Arquivo: **Opcional** 
 
 Define zonas onde os passageiros podem solicitar coleta ou entrega por serviços sob demanda. Essas zonas são representadas como polígonos GeoJSON. 
 
 - Este arquivo usa um subconjunto do formato GeoJSON, descrito em [RFC 7946](https://tools.ietf.org/html/rfc7946). 
 - O arquivo `locations.geojson` deve conter um `FeatureCollection`. 
 - Um `FeatureCollection` define vários locais de parada onde os passageiros podem solicitar embarque ou desembarque. 
 - Todo `Feature` do GeoJSON deve ter um `id`. O `id` deve ser exclusivo em todos os valores `stops.stop_id`, locations.geojson `id` e `location_group_id`. 
 - Todo `Feature` GeoJSON deverá possuir objetos e chaves associadas conforme tabela abaixo: 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 |- `tipo` | Corda | **Obrigatório** | `"FeatureCollection"` de locais. | 
 |- `recursos` | Matriz | **Obrigatório** | Coleção de objetos `"Feature"` que descrevem os locais. | 
 |     \- `tipo` | Corda | **Obrigatório** | `"Recurso"` | 
 |     \- `id` | Corda | **Obrigatório** | Identifica um local. O ID deve ser exclusivo em todos os valores `stops.stop_id`, locations.geojson `id` e `location_groups.location_group_id`. | 
 |     \- `propriedades` | Objeto | **Obrigatório** | Chaves de propriedade de localização. | 
 |         \- `stop_name| Corda | Opcional | Indica o nome do local exibido aos passageiros. | 
 |         \- `stop_desc` | Corda | Opcional | Descrição significativa do local para ajudar a orientar os passageiros. | 
 |     \- `geometria` | Objeto | **Obrigatório** | Geometria do local. | 
 |         \- `tipo` | Corda | **Obrigatório** | Deve ser do tipo:<br> - `"Polygon"`<br> - `"MultiPolígono"` | 
 |         \- `coordenadas` | Matriz | **Obrigatório** | Coordenadas geográficas (latitude e longitude) definindo a geometria do local. | 
 
### booking_rules.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`booking_rule_id`) 
 
 Define as regras de reserva para serviços solicitados pelo passageiro 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `booking_rule_id` | ID exclusivo | **Obrigatório** | Identifica uma regra. | 
 | `tipo_reserva` | Enum | **Obrigatório** | Indica com que antecedência a reserva pode ser feita. As opções válidas são:<br><br> `0` - Reserva em tempo real.<br> `1` - Até reserva no mesmo dia com aviso prévio.<br> `2` - Até dia(s) anterior(es) de reserva. | 
 | `prior_notice_duration_min` | Inteiro | **Condicionalmente Obrigatório** | Número mínimo de minutos antes da viagem para fazer a solicitação.<br><br> **Condicionalmente obrigatório**:<br> - **Obrigatório** para `booking_type=1`.<br> - **Proibido** caso contrário. | 
 | `prior_notice_duration_max` | Inteiro | **Condicionalmente Proibido** | Número máximo de minutos antes da viagem para efetuar o pedido de reserva.<br><br> **Condicionalmente Proibido**:<br> - **Proibido** para `booking_type=0` e `booking_type=2`.<br> - Opcional para `booking_type=1`.| 
 | `prior_notice_last_day` | Inteiro | **Condicionalmente Obrigatório** | Último dia antes da viagem para fazer o pedido de reserva.<br><br> Exemplo: “A viagem deve ser reservada com 1 dia de antecedência antes das 17h” será codificada como `prior_notice_last_day=1`.<br><br> **Condicionalmente obrigatório**:<br> - **Obrigatório** para `booking_type=2`.<br> - **Proibido** caso contrário. | 
 | `prior_notice_last_time` | Tempo | **Condicionalmente Obrigatório** | Última hora no último dia antes da viagem para fazer o pedido de reserva.<br><br> Exemplo: “A viagem deve ser reservada com 1 dia de antecedência antes das 17h” será codificada como `prior_notice_last_time=17:00:00`.<br><br> **Condicionalmente obrigatório**:<br> - **Obrigatório** se `prior_notice_last_day` estiver definido.<br> - **Proibido** caso contrário. | 
 | `prior_notice_start_day` | Inteiro | **Condicionalmente Proibido** | Primeiro dia antes da viagem para fazer o pedido de reserva.<br><br> Exemplo: “A viagem pode ser reservada com no mínimo uma semana de antecedência à meia-noite” será codificado como `prior_notice_start_day=7`.<br><br> **Condicionalmente Proibido**:<br> - **Proibido** para `booking_type=0`.<br> - **Proibido** para `booking_type=1` se `prior_notice_duration_max` estiver definido.<br> - Opcional caso contrário. | 
 | `prior_notice_start_time` | Tempo | **Condicionalmente Obrigatório** | Horário mais cedo no primeiro dia antes da viagem para fazer a solicitação de reserva.<br><br> Exemplo: “A viagem pode ser reservada com no mínimo uma semana de antecedência à meia-noite” será codificado como `prior_notice_start_time=00:00:00`.<br><br> **Condicionalmente obrigatório**:<br> - **Obrigatório** se `prior_notice_start_day` estiver definido.<br> - **Proibido** caso contrário. | 
 | `prior_notice_service_id` | ID referenciando `calendar.service_id| **Condicionalmente Proibido** | Indica os dias de serviço em que são contados `prior_notice_last_day` ou `prior_notice_start_day`.<br><br> Exemplo: Se estiver vazio, `prior_notice_start_day=2` terá dois dias corridos de antecedência. Se definido como um `service_id contendo apenas dias úteis (dias úteis sem feriados), `prior_notice_start_day=2` será com dois dias úteis de antecedência.<br><br> **Condicionalmente Proibido**:<br> - Opcional se `booking_type=2`.<br> - **Proibido** caso contrário. | 
 | `message` | Text | Opcional | Mensagem para os passageiros que utilizam o serviço em um `stop_time ao reservar a coleta e entrega sob demanda. Destina-se a fornecer informações mínimas a serem transmitidas dentro de uma interface de usuário sobre a ação que um passageiro deve realizar para utilizar o serviço. | 
 | `pickup_message` | Text | Opcional | Funciona da mesma forma que `message`, mas é usado quando os passageiros têm coleta apenas sob demanda. | 
 | `drop_off_message` | Text | Opcional | Funciona da mesma maneira que `message, mas é usado quando os passageiros têm entrega somente sob demanda. | 
 | `número_telefone` | Phone number | Opcional | Phone number para ligar para fazer o pedido de reserva. | 
 | `info_url` | URL | Opcional | URL que fornece informações sobre a regra de reserva. | 
 | `url_reserva` | URL | Opcional | URL para uma interface ou aplicativo online onde a solicitação de reserva pode ser feita. | 
 
### translations.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`table_name`, `field_name`, `linguagem`, `record_id`, `record_sub_id`, `field_value`) 
 
 Em regiões que possuem vários idiomas oficiais, as agências/operadoras de trânsito normalmente têm nomes e páginas da web específicos para cada idioma. Para melhor servir os passageiros nessas regiões, é útil que o conjunto de dados inclua estes valores dependentes do idioma. 
 
 Se ambos os métodos de referência (`record_id`, `record_sub_id`) e `field_value` forem usados ​​para traduzir o mesmo valor em 2 linhas diferentes, a tradução fornecida com (`record_id`, `record_sub_id`) terá precedência. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `table_name| Enum | **Obrigatório** | Define a tabela que contém o campo a ser traduzido. Os valores permitidos são:<br><br> - `agency<br> - `stops<br> - `routes<br> - `viagens`<br> - `stop_times<br> - `pathways<br> - `níveis`<br> - `feed_info<br> - `attributions<br><br> Qualquer arquivo adicionado à GTFS terá um valor `table_name` equivalente ao nome do arquivo, conforme listado acima (ou seja, sem incluir a extensão de arquivo `.txt`). | 
 | `field_name| Text | **Obrigatório** | Nome do campo a ser traduzido. Campos do tipo `Text podem ser traduzidos, campos do tipo `URL, `E-Email e `Phone number também podem ser “traduzidos” para fornecer recursos no idioma correto. Campos com outros tipos não devem ser traduzidos. | 
 | `linguagem` | Código do idioma | **Obrigatório** | Idioma da tradução.<br><br> Se o idioma for o mesmo de `feed_info.feed_lang`, o valor original do campo será assumido como o valor padrão para usar em idiomas sem traduções específicas (se `default_lang`t especificar o contrário).<hr> _Exemplo: Na Suíça, uma cidade em um cantão oficialmente bilíngue é oficialmente chamada de “Biel/Bienne”, mas seria simplesmente chamada de “Bienne” em francês e “Biel” em alemão._ | 
 | `tradução` | Text ou URL ou e-Email ou Phone number | **Obrigatório** | Valor traduzido. | 
 | `record_id` | Carteira de Identidade Estrangeira | **Condicionalmente Obrigatório** | Define o registro que corresponde ao campo a ser traduzido. O valor em `record_id deve ser o primeiro ou único campo da chave primária de uma tabela, conforme definido no atributo de chave primária de cada tabela e abaixo:<br><br> - `agency_id para [agency.txt](#agênciatxt)<br> - `stop_id` para [stops.txt](#stopstxt);<br> - `route_id` para [routes.txt](#routestxt);<br> - `trip_id` para [trips.txt](#tripstxt);<br> - `trip_id` para [stop_times.txt](#stop_timestxt);<br> - `pathway_id para [pathways.txt](#pathwaystxt);<br> - `level_id para [levels.txt](#levelstxt);<br> - `attribution_id para [attributions.txt](#attributionstxt).<br><br> Os campos das tabelas não definidos acima não devem ser traduzidos. No entanto, os produtores por vezes adicionam campos extra que estão fora da especificação oficial e estes campos não oficiais podem ser traduzidos. Abaixo está a maneira recomendada de usar `record_id para essas tabelas:<br><br> - `service_id para [calendar.txt](#calendartxt);<br> - `service_id para [calendar_dates.txt](#calendar_datestxt);<br> - `fare_id` para [fare_attributes.txt](#fare_attributestxt);<br> - `fare_id` para [fare_rules.txt](#fare_rulestxt);<br> - `shape_id` para [shapes.txt](#shapestxt);<br> - `trip_id` para [frequencies.txt](#frequencietxt);<br> - `from_stop_id para [transfers.txt](#transferstxt).<br><br> Condicionalmente obrigatório:<br> - **Proibido** se `table_name` for `feed_info`.<br> - **Proibido** se `field_value estiver definido.<br> - **Obrigatório** se `field_value estiver vazio. | 
 | `record_sub_id` | Carteira de Identidade Estrangeira | **Condicionalmente Obrigatório** | Ajuda o registro que contém o campo a ser traduzido quando a tabela t possui um ID único. Portanto, o valor em `record_sub_id é o ID secundário da tabela, conforme definido pela tabela abaixo:<br><br> - Nenhum para [agency.txt](#agênciatxt);<br> - Nenhum para [stops.txt](#stopstxt);<br> - Nenhum para [routes.txt](#routestxt);<br> - Nenhum para [trips.txt](#tripstxt);<br> - `stop_sequence` para [stop_times.txt](#stop_timestxt);<br> - Nenhum para [pathways.txt](#pathwaystxt);<br> - Nenhum para [levels.txt](#levelstxt);<br> - Nenhum para [attributions.txt](#attributionstxt).<br><br> Os campos das tabelas não definidos acima não devem ser traduzidos. No entanto, os produtores por vezes adicionam campos extra que estão fora da especificação oficial e estes campos não oficiais podem ser traduzidos. Abaixo está a maneira recomendada de usar `record_sub_id para essas tabelas:<br><br> - Nenhum para [calendar.txt](#calendartxt);<br> - `date para [calendar_dates.txt](#calendar_datestxt);<br> - Nenhum para [fare_attributes.txt](#fare_attributestxt);<br> - `route_id` para [fare_rules.txt](#fare_rulestxt);<br> - Nenhum para [shapes.txt](#shapestxt);<br> - `start_time` para [frequencies.txt](#frequenciestxt);<br> - `to_stop_id para [transfers.txt](#transferstxt).<br><br> Condicionalmente obrigatório:<br> - **Proibido** se `table_name` for `feed_info`.<br> - **Proibido** se `field_value estiver definido.<br> - **Obrigatório** se `table_name=stop_times e `record_id estiverem definidos. | 
 | `field_value` | Text ou URL ou e-Email ou Phone number | **Condicionalmente Obrigatório** | Em vez de definir qual registro deve ser traduzido usando `record_id e `record_sub_id, este campo pode ser usado para definir o valor que deve ser traduzido. Quando usada, a tradução será aplicada quando os campos identificados por `table_name e `field_name contiverem exatamente o mesmo valor definido em field_value.<br><br> O campo deve ter **exatamente** o valor definido em `field_value. Se apenas um subconjunto do valor corresponder a `field_value`, a tradução t será aplicada.<br><br> Se duas regras de tradução corresponderem ao mesmo registro (uma com `field_value` e outra com `record_id`), a regra com `record_id` terá precedência.<br><br> Condicionalmente obrigatório:<br> - **Proibido** se `table_name` for `feed_info`.<br> - **Proibido** se `record_id estiver definido.<br> - **Obrigatório** se `record_id estiver vazio. | 
 
### feed_info.txt 
 
 Arquivo: **Recomendado** (**Obrigatório** se [translations.txt](#translationstxt) for fornecido) 
 
 Primary key (none) § § 
 O arquivo contém informações sobre o próprio conjunto de dados, em vez dos serviços que o conjunto de dados descreve. Em alguns casos, o editor do conjunto de dados é uma entity diferente de qualquer uma das agências. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `feed_publisher_name` | Text | **Obrigatório** | Nome completo da organização que publica o conjunto de dados. Pode ser igual a um dos valores `agency.agency_name`. | 
 | `feed_publisher_url` | URL | **Obrigatório** | URL do site da organização que publica o conjunto de dados. Pode ser igual a um dos valores `agency.agency_url. | 
 | `feed_lang` | Código do idioma | **Obrigatório** | Idioma padrão usado para o texto neste conjunto de dados. Essa configuração ajuda os consumidores da GTFS a escolher regras de capitalização e outras configurações específicas de idioma para o conjunto de dados. O arquivo `translations.txt pode ser usado se o texto precisar ser traduzido para idiomas diferentes do padrão.<br><br> O idioma padrão pode ser multilíngue para conjuntos de dados com o texto original em vários idiomas. Nesses casos, o campo `feed_lang deverá conter o código do idioma `mul definido pela norma ISO 639-2, e uma tradução para cada idioma utilizado no conjunto de dados deverá ser fornecida em `translations.txt. Se todo o texto original no conjunto de dados estiver no mesmo idioma, então `mul` não deverá ser usado.<hr> _Exemplo: Considere um conjunto de dados de um país multilíngue como a Suíça, com o campo original `stops.stop_name` preenchido com nomes de parada em diferentes idiomas. Cada nome de parada é escrito de acordo com o idioma dominante na localização geográfica da parada, por exemplo, `Genève para a cidade francófona de Geneva, `Zürich para a cidade alemã de Zurich e `Biel/Bienne para a cidade bilíngue.cidade de Biel/Bienne. O conjunto de dados `feed_lang deveria ser `mul e as traduções seriam fornecidas em `translations.txt, em alemão: `Genf, `Zürich e `Biel; em francês: `Genève, `Zurich e `Bienne; em italiano: `Ginevra, `Zurigo e `Bienna; e em inglês: `Geneva`, `Zurich` e `Biel/Bienne`._ | 
 | `default_lang| Código do idioma | Opcional | Define o idioma que deve ser usado quando o consumidor de dados t conhece o idioma do passageiro. Freqüentemente será `en` (inglês). | 
 | `feed_start_date` | Data | Recomendado | O conjunto de dados fornece informações de programação completas e confiáveis ​​para atendimento no período que vai do início do dia `feed_start_date até o final do dia `feed_end_date. Ambos os dias podem ficar vazios se não estiverem disponíveis. A date ` feed_end_date ` não deve preceder a date ` feed_start_date ` se ambas forem fornecidas. Recomenda-se que os fornecedores de conjuntos de dados forneçam dados de programação fora deste período para avisar sobre o provável serviço futuro, mas os consumidores do conjunto de dados devem tratá-los conscientes do seu estatuto não oficial. Se ` feed_start_date ou `feed_end_date se estenderem além das datas ativas do calendário definidas em [calendar.txt](#calendartxt) e [calendar_dates.txt](#calendar_datestxt), o conjunto de dados está fazendo uma afirmação explícita de que não há serviço para datas dentro do intervalo `feed_start_date` ou `feed_end_date`, mas não incluído nas datas ativas do calendário. | 
 | `feed_end_date` | Data | Recomendado | (veja acima) | 
 | `feed_version` | Text | Recomendado | String que indica a versão atual do conjunto de dados GTFS. Os aplicativos que consomem GTFS podem exibir esse valor para ajudar os editores de conjuntos de dados a determinar se o conjunto de dados mais recente foi incorporado. | 
 | `feed_contact_email| E-Email | Opcional | Endereço de e-Email para comunicação sobre o conjunto de dados GTFS e práticas de publicação de dados. `feed_contact_email é um contato técnico para aplicativos que consomem GTFS. Forneça informações de contato de atendimento ao cliente por meio de [agency.txt](#agencytxt). É recomendado que pelo menos um dos `feed_contact_email` ou `feed_contact_url` seja fornecido. | 
 | `feed_contact_url` | URL | Opcional | URL para informações de contato, formulário web, suporte técnico ou outras ferramentas para comunicação sobre o conjunto de dados GTFS e práticas de publicação de dados. `feed_contact_url é um contato técnico para aplicativos que consomem GTFS. Forneça informações de contato de atendimento ao cliente por meio de [agency.txt](#agencytxt). É recomendado que pelo menos um dos `feed_contact_url` ou `feed_contact_email` seja fornecido. | 
 
### attributions.txt 
 
 Arquivo: **Opcional** 
 
 Chave primária (`attribution_id`) 
 
 O arquivo define as attributions aplicadas ao conjunto de dados. 
 
 | Nome do campo | Tipo | Presença | Descrição | 
 |------|------|------|------| 
 | `attribution_id| ID exclusivo | Opcional | Identifica uma atribuição para o conjunto de dados ou um subconjunto dele. Isso é útil principalmente para traduções. | 
 | `agency_id| ID estrangeiro com referência `agency.agency_id` | Opcional | Agência à qual a atribuição se aplica.<br><br> Se uma atribuição `agency_id, `route_id` ou `trip_id` for definida, as outras deverão estar vazias. Se nenhum deles for especificado, a atribuição será aplicada a todo o conjunto de dados. | 
 | `route_id` | ID estrangeiro referenciando `routes.route_id` | Opcional | Funciona da mesma forma que `agency_id exceto que a atribuição se aplica a uma rota. Várias attributions podem ser aplicadas à mesma rota. | 
 | `trip_id` | ID estrangeiro com referência a `trips.trip_id` | Opcional | Funciona da mesma forma que `agency_id`, exceto que a atribuição se aplica a uma viagem. Várias attributions podem ser aplicadas à mesma viagem. | 
 | `organization_name` | Text | **Obrigatório** | Nome da organização à qual o conjunto de dados é atribuído. | 
 | `is_producer| Enum | Opcional | O papel da organização é produtor. As opções válidas são:<br><br> `0` ou vazio- A organização t tem esta função.<br> `1` - A organização tem essa função.<br><br> Pelo menos um dos campos `is_producer, `is_operator ou `is_authority deve ser definido como `1`. | 
 | `is_operator| Enum | Opcional | Funciona da mesma maneira que `is_producer` exceto que a função da organização é operadora. | 
 | `is_authority| Enum | Opcional | Funciona da mesma maneira que `is_producer exceto que o papel da organização é autoridade. | 
 | `attribution_url| URL | Opcional | URL da organização. |

 
 | `attribution_email| E-Email | Opcional | E-Email da organização. | 
 | `attribution_phone| Phone number | Opcional | Phone number da organização. | 
 

