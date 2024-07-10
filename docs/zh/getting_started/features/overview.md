# GTFS Schedule功能 
 
 随着GTFS参考格式不断发展以满足当前交通系统的需求，其功能也变得越来越复杂。**GTFS功能**旨在提供对GTFS参考格式所支持功能的清晰而明确的解释。这有助于交通机构、供应商、消费者和研究人员了解GTFS的功能并回答以下问题：**我可以用GTFS做什么？** 
 
 以下功能组解释了每个功能的用途以及与它们相关的文件和字段，帮助用户了解支持特定功能所需的数据。
 
## 基础 
 这些基本功能构成了GTFS供稿的核心。它们是表示交通服务所需的最小元素。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __机构__ 
 
 传达负责交通服务机构的详细信息。 
 
 [:octicons-arrow-right-24: 了解更多](../base/# agency) 
 
 - :material-subway-variant:{ .lg.middle } __站点__ 
 
 定义交通服务接送乘客的地点。 
 
 [:octicons-arrow-right-24: 了解更多](../base/# stops) 
 
 - :material-subway-variant:{ .lg.middle } __路线__ 
 
 定义交通路线的元素，例如名称和服务类型。 
 
 [:octicons-arrow-right-24: 了解更多](../base/# routes) 
 
 - :material-subway-variant:{ .lg.middle } __服务日期__ 
 
 创建结构来安排行程和服务豁免。 
 
 [:octicons-arrow-right-24: 了解更多](../base/#service-dates) 
 
 - :material-subway-variant:{ .lg.middle } __Trips__ 
 
 表示在预定时间沿规定路线行驶的交通车辆。 
 
 [:octicons-arrow-right-24: 了解更多](../base/#trips) 
 
 - :material-subway-variant:{ .lg.middle } __停靠时间__ 
 
 定义每个站点的每趟行程的arrival和departure时间。
 
 [:octicons-arrow-right-24: 了解更多](../base/#stop-times) 
 
</div> 
 
## 基础附加组件 
 这些功能增强了GTFS数据集，改善了乘客体验并促进了机构、供应商和数据再利用者之间的协作。它们可能涉及向现有文件添加新字段或创建新文件。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __Feed 信息__ 
 
 传达关于 feed 本身的重要信息。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#feed-information) 
 
 - :material-subway-variant:{ .lg.middle } __形状__ 
 
 定义vehicle在行程中行驶的地理路径。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#shapes) 
 
 - :material-subway-variant:{ .lg.middle } __路线颜色__ 
 
 准确描述和传达分配给特定routes的配色方案。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#route-colors) 
 
 - :material-subway-variant:{ .lg.middle } __允许自行车__ 
 
 告知车辆是否能够容纳自行车。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#bike-allowed) 
 
 - :material-subway-variant:{ .lg.middle } __头部标志__ 
 
 告知车辆使用的标牌，指示行程目的地。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#headsigns) 
 
 - :material-subway-variant:{ .lg.middle } __位置类型__ 
 
 对交通站内的关键区域（如入口和出口）进行分类。
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#location-types) 
 
 - :material-subway-variant:{ .lg.middle } __频率__ 
 
 表示以固定频率或特定间隔运行的服务。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#frequency-based-service) 
 
 - :material-subway-variant:{ .lg.middle } __Transfers__ 
 
 描述不同交通服务之间允许的transfers。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/# transfers) 
 
 - :material-subway-variant:{ .lg.middle } __Translations__ 
 
 以多种语言传达服务信息。 
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/#translations) 
 
 - :material-subway-variant:{ .lg.middle } __Attributions__ 
 
 沟通参与创建数据集的人员。
 
 [:octicons-arrow-right-24: 了解更多](../base_add-ons/# attributions) 
 
</div> 
 
 
## 可访问性 
 可访问性功能为残障人士提供访问服务的基本信息。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __站点轮椅无障碍设施__ 
 
 表明某个位置是否可以供轮椅上车。 
 
 [:octicons-arrow-right-24: 了解更多](../accessibility/#stops-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __行程轮椅无障碍设施__ 
 
 表明vehicle是否可容纳使用轮椅的乘客。 
 
 [:octicons-arrow-right-24: 了解更多](../accessibility/#trips-wheelchair-accessibility) 
 
 - :material-subway-variant:{ .lg.middle } __文本转语音__ 
 
 提供必要的输入，将站点名称的文本转换为音频。
 
 [:octicons-arrow-right-24: 了解更多](../accessibility/#text-to-speech) 
 
</div> 
 
 
## 票价 
 GTFS可以模拟各种票价结构，例如区域、距离或基于一天中的时间的票价。它告知乘客行程价格和付款方式。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __票价产品__ 
 
 定义可供用户使用的车票或票价类型的列表。 
 
 [:octicons-arrow-right-24: 了解更多](../fares/#fare-products) 
 
 - :material-subway-variant:{ .lg.middle } __票价媒体__ 
 
 定义可用于保存和/或验证票价产品的媒体。 
 
 [:octicons-arrow-right-24: 了解更多](../fares/#fare-media) 
 
 - :material-subway-variant:{ .lg.middle } __基于路线的票价__ 
 
 描述用于对特定routes组应用不同票价的规则。 
 
 [:octicons-arrow-right-24: 了解更多](../fares/#route-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __基于时间的票价__ 
 
 描述按一天中的时间或一周中的日子区分的票价。
 
 [:octicons-arrow-right-24: 了解更多](../fares/#time-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __基于区域的票价__ 
 
 描述从一个区域到另一个区域旅行时的区分票价。 
 
 [:octicons-arrow-right-24: 了解更多](../fares/#zone-based-fares) 
 
 - :material-subway-variant:{ .lg.middle } __票价转乘__ 
 
 定义从一段行程转到另一段行程时适用的费用。 
 
 [:octicons-arrow-right-24: 了解更多](../fares/#fares-transfers) 
 
 - :material-subway-variant:{ .lg.middle } __票价 V1__ 
 
 允许更简单地表示票价信息的旧功能。 
 
 [:octicons-arrow-right-24: 了解更多](../fares/#fares-v1) 
 
</div> 
 
 
## 路径 
 
 路径功能允许对大型交通站进行建模，以便引导乘客从入口到登车区。它们提供路径详细信息、估计导航时间和寻路系统。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __路径连接__ 
 
 模拟连接交通站内相关点的路径。 
 
 [:octicons-arrow-right-24: 了解更多](../pathways/#pathway-connections) 
 
 - :material-subway-variant:{ .lg.middle } __路径详情__ 
 
 提供有关路径物理特性的更多详细信息。 
 
 [:octicons-arrow-right-24: 了解更多](../pathways/#pathway-details) 
 
 - :material-subway-variant:{ .lg.middle } __级别__ 
 
 描述并列出交通站内的所有不同级别。 
 
 [:octicons-arrow-right-24: 了解更多](../pathways/#levels) 
 
 - :material-subway-variant:{ .lg.middle } __站内遍历时间__ 
 
 传达在交通站内导航路径的预计时间。 
 
 [:octicons-arrow-right-24: 了解更多](../pathways/#in-station-traversal-time) 
 
 - :material-subway-variant:{ .lg.middle } __路径标志__ 
 
 传达与路径相关的站内标志。 
 
 [:octicons-arrow-right-24: 了解更多](../pathways/#pathway-signs) 
 
</div> 
 
## 灵活的服务 
 灵活的服务，或不遵循固定时间表或固定routes的需求响应服务。
 
<div class="grid cards" markdown> 
 
 - :material-subway-variant:{ .lg.middle } __连续站点__ 
 
 表明用户是否可以在stops之间上车和/或下车。 
 
 [:octicons-arrow-right-24: 了解更多](../flexible_services/#continuous-stops) 
 
 - :material-subway-variant:{ .lg.middle } __预订规则__ 
 
 表明用户是否可以预订需求响应式服务的行程。 
 
 [:octicons-arrow-right-24: 了解更多](../flexible_services/#booking-rules) 
 
 - :material-subway-variant:{ .lg.middle } __带有偏差的预定义路线__ 
 
 可以短暂偏离路线接送乘客的车辆。 
 
 [:octicons-arrow-right-24: 了解更多](../flexible_services/#predefined-routes-with-deviation) 
 
 - :material-subway-variant:{ .lg.middle } __基于区域的需求响应服务__ 
 
 允许在特定区域内任何地点接送乘客的服务。 
 
 [:octicons-arrow-right-24: 了解更多](../flexible_services/#zone-based-demand-responsive-services) 
 
 - :material-subway-variant:{ .lg.middle } __固定站点需求响应服务__ 
 
 允许在stops组内的任何位置上车/下车的服务。
 
 [:octicons-arrow-right-24: 了解更多](../flexible_services/#fixed-stops-demand-responsive-services) 
 
</div> 
 

