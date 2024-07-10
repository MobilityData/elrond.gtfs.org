# 创建GTFS数据集 
 
## GTFS提要概述 
 所有GTFS提要都以GTFS参考格式的数据集开头，该数据集是一系列以.txt文件扩展名保存的 CSV 文件[^1]。在最基本的实现中， GTFS数据集通常以七个基础文件开头，组合成一个 .zip 文件，该文件托管在稳定且公开的URL上：这是GTFS提要。
 
<img class="center" width="560" height="100%" src="../../../assets/create_001.png"> 
 
 每个文件由多条记录（数据行）和多个信息字段组成。例如，[routes.txt](../../documentation/schedule/reference/#routestxt) 中列出的每行代表一条公共交通路线，其字段描述该路线的多个元素，如其名称、描述、运营agency等。
 
<img class="center" width="560" height="100%" src="../../../assets/create_002.png"> 
 
 GTFS数据集的基础文件可描述如下： GTFS时刻表数据集具有一条或多条routes([routes.txt](../../documentation/schedule/reference/#routestxt))，每条路线具有一趟或多趟行程 ([trips.txt](../../documentation/schedule/reference/#tripstxt))，每次行程会在指定时间 ([stops.txt](../../documentation/schedule/reference/#stop_timestxt)) 访问一系列stops([stop_times.txt](../../documentation/schedule/reference/#stop_timestxt))。行程和停靠时间仅包含一天中的时间信息；日历用于确定特定行程在哪几天运行（[calendar.txt](../../documentation/schedule/reference/#calendartxt) 和 [calendar_dates.txt](../../documentation/schedule/reference/#calendar_datestxt))。此外，多个旅行社（[agency.txt](../../documentation/schedule/reference/#agencytxt)) 可以运营多条routes。这些文件通过相互引用的字段相互链接。
 
<img class="center" width="560" height="100%" src="../../../assets/create_003.png"> 
 
 一旦设置了这些文件以创建基本的GTFS数据集，就可以添加其他（optional）文件以启用其他功能或满足交通运输机构和供应商之间的特定需求。这些文件的一些示例包括：
 
 - [shapes.txt](../../documentation/schedule/reference/#shapestxt) 允许以图形方式表示行程路径，
 - [pathways.txt](../../documentation/schedule/reference/#pathwaystxt) 提供信息，可以生成方向来帮助用户导航车站，
 - [frequencies.txt](../../documentation/schedule/reference/#frequenciestxt) 提供另一种指定停车时间的方法。
 
 有关可启用的所有GTFS功能的更多信息，请参阅 [“ GTFS能做什么？”](../features/overview/) 部分。 
 
 GTFS Schedule数据集可以通过vehicle位置和服务更新等实时信息进行补充。为此，需要独立于现有的GTFS Schedule数据集创建GTFS Realtime供稿。
 
 GTFS Realtime供稿由通过 HTTP 提供并经常更新的常规二进制文件组成，任何类型的网络服务器都可以托管和提供该文件。GTFS GTFS Realtime数据交换格式基于 [协议缓冲区](https:)，这是一种与语言和平台无关的结构化数据序列化机制。GTFS GTFS Realtime可以提供三种类型的信息：行程更新、服务警报和车辆位置，这些信息可以根据需要传达的服务信息进行组合。
 
 由于GTFS Realtime允许呈现车队的实际状态，因此需要定期更新供稿 - 最好是每当服务的自动车辆定位系统有新数据时更新。 GTFS Schedule数据集和GTFS Realtime信息流相结合，使消费应用程序能够为乘客提供准确且最新的信息。有关更多信息，请参阅技术文档。
 
## 制作您的第一个GTFS信息流？
 
 如果您是一家希望制作第一个GTFS信息流的agency，您需要做的第一件事就是阅读现有文档。
 
 首先在 [“ GTFS能做什么？”](../features/overview) 部分探索GTFS的功能，并确定您想要使用GTFS格式表示的交通服务的不同功能。如需更深入的探索，[GTFS Schedule](../../documentation/schedule/reference) 和 [GTFS Realtime](../../documentation/realtime/reference) 的官方参考文档提供了有关建模这些功能和确保合规性的详细指导。
 
 接下来，从您的系统收集所有必需的数据。这包括所有stops、routes、时间表、票价等信息，因为其中许多详细信息将成为填充GTFS数据集的输入。
 
 根据系统的规模和复杂程度，您可以选择内部创建数据，也可以聘请外部GTFS供应商将数据转换为GTFS格式。
 
 在某些情况下，拥有少量routes的小型机构会使用常用软件（如电子表格和文本编辑器）自行创建数据。
 
 在处理更大的系统范围时，大多数机构会从专业供应商处购买专门的GTFS管理软件，但有些机构可能会选择开发自己的内部工具。最后，当系统特性证明机构难以自行编写数据集时，可以将GTFS制作完全外包给专门生产GTFS数据的公司。 
 
<a href="https://www.flaticon.com/authors/freepik" title="Freepik 图标">由 Freepik- Flaticon 创建的图标</a>
 
 [^1]: 除了文本文件之外， GTFS现在还支持 [GeoJSON](https: ) 格式，以表示需求响应服务的某些元素。
 

