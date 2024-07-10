# Avalie a qualidade do seu feed GTFS 
 
 Uma GTFS de alta qualidade é completa, precisa e atualizada. Isso significa que representa como os serviços estão operando atualmente e fornece o máximo de informações possível. 
 
## Dados completos 
 
 O GTFS de qualidade inclui detalhes importantes do serviço, como mudanças na programação de feriados e verão, locais de parada precisos e nomes de routes e sinais de trânsito que correspondem a outros materiais voltados para o passageiro. Mesmo que uma agency trabalhe com um fornecedor para produzir GTFS, em última análise, cabe à agency garantir que as informações apresentadas impressas, on-line e on-line sejam consistentes. 
 
## Dados precisos 
 
 Dados precisos são essenciais para fornecer aos passageiros do transporte público uma experiência de transporte confiável e fácil de usar. Erros nos dados podem bloquear o uso de uma parte ou da totalidade de um conjunto de dados. 
 
## Dados atualizados 
 
 Dados desatualizados podem ser mais problemáticos do que não ter feed disponível. Não basta simplesmente publicar informações – é necessário que correspondam ao que o motociclista vê e vivencia. Algumas das maiores agências de transporte público atualizam sua GTFS semanalmente, ou mesmo diariamente, mas a maioria das agências precisará atualizar sua GTFS a cada poucos meses ou algumas vezes por ano quando o serviço mudar. Isso inclui coisas como novas routes ou stops, alterações de horários ou atualizações na estrutura tarifária. 
 
 Muitas agências contratam um fornecedor para criar e gerenciar sua GTFS para elas. Alguns fornecedores podem ser proativos ao perguntar sobre mudanças nos serviços, mas é importante que as agências comuniquem com os fornecedores sobre mudanças futuras nos serviços. É possível publicar GTFS com alterações de serviço com antecedência, garantindo que a transição ocorra sem problemas para todos: agências, fornecedores, planejadores de viagens e passageiros! 
 
## Usando validadores oficiais 
 
 Os validadores oficiais do GTFS avaliam a qualidade de um conjunto de dados em relação à especificação oficial, garantindo um entendimento comum dentro da indústria sobre o que constitui um conjunto de dados de alta qualidade. 
 
 O [Canonical GTFS Schedule validator](https://gtfs-validator.mobilitydata.org/)[^1] gratuito e de código aberto mantido por [MobilityData](https://mobilitydata.org/) garante seus dados GTFS estão em conformidade com a [Referência de GTFS Schedule](../../documentation/schedule/reference/) e [Práticas recomendadas](../../documentation/schedule/schedule_best_practices) oficiais. Ele fornece um relatório fácil de usar que pode ser compartilhado com outras partes e documentação abrangente. 
 
<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li> Acesse <a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a> .</li> 
<li> Carregue seu conjunto de dados GTFS : você pode selecionar ou arrastar e soltar um arquivo ZIP ou copiar/colar um URL.</li> 
<li> Ao final da validação, será disponibilizada a opção de abertura do relatório.</li> 
<li> Você verá se o validador encontrou problemas com os dados e links para nossa documentação sobre como corrigi-los. A URL do relatório de validação funcionará por 30 dias e poderá ser compartilhada com outras pessoas.</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 Da mesma forma, usar o [GTFS Realtime Validator](https:) garante que seus dados GTFS estejam em conformidade com o [GTFS Realtime Reference] oficial (../../documentation/realtime/reference/) e [Práticas recomendadas](../../documentation/realtime/realtime_best_practices). 
 
 Para obter informações sobre como criar dados de alta qualidade, consulte as [Diretrizes de dados de trânsito da Califórnia](https://dot.ca.gov/cal-itp/california-transit-data-guidelines), as [Práticas recomendadas do GTFS Schedule](../../documentation/schedule/schedule_best_practices) e as [Práticas recomendadas em GTFS Realtime](../../documentation/realtime/realtime_best_practices). 
 
 [^1]: Para ver mais instruções sobre como usar esta ferramenta em seu pipeline de dados e contribuir com este projeto, visite o [repositório GitHub](https://github.com/MobilityData/gtfs-validator ). 
 

