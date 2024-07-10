# Особенности GTFS Schedule 
 
 По мере того, как справочный формат GTFS развивается в соответствии с текущими потребностями транспортных систем, его функции могут становиться все более сложными. **Функции GTFS ** предназначены для предоставления четкого и исчерпывающего объяснения функций, предоставляемых справочным форматом GTFS. Это помогает транспортным агентствам, продавцам, потребителям и исследователям понять возможности GTFS и ответить на вопрос: **Что я могу делать с GTFS?** 
 
 Следующие группы функций объясняют назначение каждой функции, а также файлы и поля, связанные с ними, помогая пользователям понять, какие данные необходимы для поддержки конкретной функции. 
 
## Base 
 Эти важные функции составляют основу фида GTFS. Это минимальные элементы, необходимые для представления транзитной услуги. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Agency__ 
 
 Сообщите подробную информацию об агентствах, ответственных за транзитную услугу. 
 
 [:octicons-arrow-right-24: Узнать больше](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __Stops__ 
 
 Определить места, где транзитная служба забирает и высаживает пассажиров. 
 
 [:octicons-arrow-right-24: Узнать больше](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __Routes__ 
 
 Определить элементы транзитного маршрута, такие как название и тип услуги. 
 
 [:octicons-arrow-right-24: Узнать больше](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __Даты обслуживания__ 
 
 Создайте структуру для планирования поездок и исключений из обслуживания. 
 
 [:octicons-arrow-right-24: Узнать больше](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trips__ 
 § § Представляют транзитные транспортные средства, следующие по определенному маршруту в установленное время. 
 
 [:octicons-arrow-right-24: Узнать больше](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __Stop Times__ 
 
 Определите время arrival и departure каждой поездки для каждой остановки. 
 
 [:octicons-arrow-right-24: Узнать больше](../base/#stop-times) 
 
</div> 
 
## Базовые дополнения 
 Эти функции расширяют набор данных GTFS, улучшая качество обслуживания пассажиров и облегчая сотрудничество между агентствами, поставщиками и повторными пользователями данных. Они могут включать добавление новых полей в существующие файлы или создание новых файлов. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Информация о канале__ 
 
 Сообщайте важную информацию о самом канале. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __Shapes__ § § 
 Определите географический путь, по которому следует vehicle во время поездки. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __Route Colors__ 
 
 Точно отображать и передавать цветовую схему, присвоенную конкретным routes. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __Велосипед разрешен__ 
 
 Сообщите, могут ли транспортные средства вмещать велосипеды или нет. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __Headsigns__ § § 
 Сообщите о знаках, используемых транспортными средствами, указывающих пункт назначения поездки. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __Типы местоположения__ 
 
 Классифицируйте ключевые зоны на транзитных станциях, такие как входы и выходы. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __Frequency__ § § 
 Представляют службы, которые работают на регулярной частоте или с определенными интервалами. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/# Frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __Трансферы__ 
 
 Опишите transfers, разрешенные между различными транзитными службами. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Translations__ 
 § § Передача служебной информации на нескольких языках. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Attributions__ 
 § § Сообщите, кто участвовал в создании набора данных. 
 
 [:octicons-arrow-right-24: Узнать больше](../base_add-ons/# attributions) 
 
</div> 
 
 
## Доступность 
 Функции доступности предоставляют людям с ограниченными возможностями необходимую информацию для доступа к услуге. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Остановка доступности для инвалидных колясок__ 
 
 Укажите, возможна ли посадка на инвалидной коляске из определенного места. 
 
 [:octicons-arrow-right-24: Узнать больше](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Trips Инвалидная коляска Доступность__ 
 
 Укажите, может ли vehicle вместить пассажиров в инвалидных колясках. 
 
 [:octicons-arrow-right-24: Узнать больше](../accessibility/#trips-installer-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __Text- to-Speech__ 
 
 Предоставьте необходимые входные данные для преобразования текста названий остановок в аудио. 
 
 [:octicons-arrow-right-24: Узнать больше](../accessibility/#text-to-speech) 
 
</div> 
 
 
## Тарифы 
 GTFS может моделировать различные структуры тарифов, такие как тарифы на основе зоны, расстояния или времени суток. Он информирует пассажиров о стоимости поездки и способах оплаты. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Fare Products__ 
 
 Определите список билетов или типов тарифов, доступных пользователям. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __Fare Media__ 
 
 Определите носитель, который можно использовать для хранения и/или проверки тарифного продукта. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __Тарифы на основе маршрута__ 
 
 Описать правила, используемые для применения различных тарифов на определенных группах routes. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Time- Базовые тарифы__ 
 
 Опишите тарифы, различающиеся по времени суток или дням недели. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Zone- Базовые тарифы__ 
 
 Опишите тарифы, дифференцированные при путешествии из одного региона в другой. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __Тарифы на трансферы__ 
 
 Определить сборы, взимаемые при переходе с одного этапа поездки на другой. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Fares V1__ 
 
 Устаревшая функция, позволяющая упростить представление информации о тарифах. 
 
 [:octicons-arrow-right-24: Узнать больше](../fares/#fares-v1) 
 
</div> 
 
 
## Pathways 
 
 Функции Pathways позволяют моделировать большие транзитные станции, так что пассажиры направляются от входов к зонам посадки. Они предоставляют подробную информацию о пути, расчетное время навигации и системы навигации. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Pathway Connections__ 
 
 Моделируйте пути, соединяющие соответствующие точки внутри транзитной станции. 
 
 [:octicons-arrow-right-24: Узнать больше](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __Pathway Details__ 
 
 Предоставьте дополнительную информацию о физических характеристиках пути. 
 
 [:octicons-arrow-right-24: Узнать больше](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __Levels__ 
 § § Опишите и перечислите все уровни транзитной станции. 
 
 [:octicons-arrow-right-24: Узнать больше](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __Время прохождения внутри станции__ § § 
 Сообщите расчетное время навигации по маршруту внутри транзитной станции. 
 
 [:octicons-arrow-right-24: Узнать больше](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __Путьовые знаки__ 
 
 Сообщают о знаках на станции, связанных с маршрутом. 
 
 [:octicons-arrow-right-24: Узнать больше](../pathways/#путевые знаки) 
 
</div> 
 
## Гибкие услуги 
 Гибкие услуги или услуги, реагирующие на спрос, которые не следуют регулярным расписаниям или фиксированным routes. 
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Постоянные остановки__ 
 
 Укажите, можно ли забрать и/или высадить пользователя между stops. 
 
 [:octicons-arrow-right-24: Узнать больше](../flexible_services/#continious-stops) 
 
 - :material-subway-variant:{ .lg.middle } __Правила бронирования__ 
 
 Укажите, могут ли пользователи забронировать поездку с помощью услуги, реагирующей на спрос. 
 
 [:octicons-arrow-right-24: Узнать больше](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __Предопределенные маршруты с отклонениями__ 
 
 Транспортные средства, которые могут ненадолго отклониться от маршрута для посадки или высадки. 
 
 [:octicons-arrow-right-24: Узнать больше](../flexible_services/#predefine-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __Услуги реагирования на спрос в зависимости от зоны__ 
 
 Услуги, которые позволяют забрать/высадить груз в любом месте в пределах определенной области. 
 
 [:octicons-arrow-right-24: Узнать больше](../flexible_services/#zone-based-demand-response-services) 
 
 - :material-subway-variant:{ .lg.middle } __Услуги, реагирующие на спрос с фиксированными остановками__ 
 
 Услуги, позволяющие посадку/высадку в любом месте в пределах группы stops. 
 
 [:octicons-arrow-right-24: Узнать больше](../flexible_services/#fixed-stops-demand-response-services) 
 
</div> 
 

