# 使您的GTFS信息流公开可用 
 
## 共享您的GTFS 的好处 
 
 GTFS数据有多种利用方式，公开共享您机构的GTFS数据可为您的乘客和整个agency带来诸多好处。这些包括：
 
 - 将您的信息流集成到移动和基于网络的行程计划应用程序中，让乘客在您的系统上计划行程 
 - 将您的信息流提交给GTFS聚合器（如移动数据库），这可为您的agency提供更广泛的受众和更高的可见性 
 - 使用允许在地理信息系统（GIS）和其他基于地图的分析程序中可视化和分析GTFS数据的工具 
 
### 行程计划应用程序 
 
 当您机构的GTFS数据公开共享时，除了 Google 地图之外，各种行程计划应用程序都可以使用它。这些可以包括其他导航应用，例如 Bing Maps、Apple Maps，以及 Transit、Moovit、Transportr 和 Citymapper 等交通专用平台。此外，访问开放供稿数据使开发人员能够制作面向特定区域的应用，或者可以包含标准旅行规划器中t包含的功能，例如：Vamos（加利福尼亚州圣华金县和斯坦尼斯劳斯县）、MetroHero（华盛顿特区）、Entur（挪威）等。 
 
### 信息聚合器 
 
 共享您的GTFS数据还可以被GTFS信息聚合平台编入索引，这些平台可以包括GTFS信息的国家或地区级目录，以及国际信息聚合器，如 [移动数据库](https://database.mobilitydata.org/) 和 [Transitland](https://www.transit.land/)（更多信息聚合器请参见[此处](../../resources/data)）。被信息聚合器编入索引可以提高您机构的知名度，并允许开发人员、研究人员和其他相关方轻松访问您机构的数据以用于各种目的，包括开发新的应用程序。 
 
### 与 GIS、分析和其他平台和工具集成 
 
 GTFS数据还可以导入并用于各种地理空间分析平台。地理信息系统 (GIS) 程序（例如 Esri 的 ArcGIS）以及开源 QGIS 都有自己的插件和扩展，可以import和可视化GTFS站点和路线数据。 
 
 - Esri 有 [各种各样的工具和插件](https://github.com/Esri/public-transit-tools) 使用GTFS数据，包括可视化时间表数据 
 - 在 QGIS 中，[GTFS-GO](https://plugins.qgis.org/plugins/GTFS-GO-master/) 和 [GTFS Loader](https://plugins.qgis.org/plugins/GTFS_Loader/) 允许您在平台内可视化routes+stops- [附加分析工具](../../resources/agency-tools) 
 
 其他平台允许您以独特的方式可视化和分析GTFS数据：
 
 - [Conveyal](https://conveyal.com/) 是一个开源程序，允许用户importGTFS数据来可视化时间表、routes和模式，并分析影响潜在的服务变化。用户还可以import和使用人口统计数据进行分析，例如，不同的routes或时间表如何影响特定城市地区的就业机会。
 - [GTFS转 HTML](https:) 是一个开源工具，可以将GTFS时间表数据转换为 HTML 时间表。它允许机构自动在其网站上发布和更新他们的时间表，格式也可以被屏幕阅读器读取，使视障人士可以访问数据。
 
## 共享您的数据：提示和最佳实践
 
### 创建和维护永久获取链接
 
 获取链接是一个永久的URL ，您的机构的GTFS Schedule文件存储在此。通常，它托管在您的机构网站上，或者由您的供应商托管（如果您与供应商签订了GTFS制作合同）。这是旅行计划应用程序（如 Google 地图）访问您的数据的方式。理想情况下，您的GTFS Schedule文件应该可直接从此URL下载，而无需登录。但是，如果由于许可限制而无法做到这一点，您的agency可以通过使用和向数据用户颁发 API 密钥来控制对数据的访问。
 
### URL和文件名
 
 一致的获取链接和GTFS文件名对于确保对供稿数据的访问至关重要。如果您的agency没有对其数据使用一致的 URL 和文件名，则意味着行程计划应用、供稿聚合器和其他用户将无法获得最准确和最新的数据，从长远来看这将cause问题。
 
 一旦为永久获取链接设置了URL ，请不要更改它。这意味着即使文件本身已更新， URL名称也应保持一致。因此，请尽可能保持 URL 简单和通用，并避免使用包含日期或版本号的 URL。 
 
 - **好**：http://www.bart.gov/dev/schedules/google_transit.zip，
 - **避免**：http://www.bart.gov/dev/schedules/google_transit_Fall_2021.zip 
 
 同样，即使您对 feed 本身进行了任何更新，也要保持包含GTFS Schedule文件的 ZIP 文件夹名称一致。例如，当您更新 feed 时，您不应在 ZIP 文件夹名称中添加任何类型的date或版本号。如果您想在 feed 中包含有关 feed 版本或 feed 开始和结束日期的数据，您可以将其包含在feed_info.txt文件中。 
 
 - **好**：“YourAgency_gtfs.zip”、“google_transit.zip”、“gtfs.zip”， 
 - **避免**：“YourAgency_gtfs_092921.zip”、“YourAgency_Fall2021.zip” 
 
 
### 文件配置和完整性 
 
 您的GTFS是一个 zip 文件，包含几个相互关联的文本文件（.txt）。为了确保格式正确，请始终执行以下操作： 
 
 1.打开文本文件时，请确保将值保留为文本。GTFS 中有很多字段，Excel 等应用程序会错误读取或缩写。 
 2.文件以逗号分隔，而不是制表符分隔。这意味着每个文件GTFS包含行中的记录，并且不同的字段以逗号分隔。 
 3.多余的行或列将cause使用应用程序出错，因此请确保保存文件时没有空行或空列。
 4.不要丢弃GTFS中的任何文件 - 它们协同工作，任何丢失的文件都可能cause使用应用程序出错。
 5.重新压缩文件时，请确保压缩文件而不是包含文件夹。解压缩文件后，您可以立即看到该文件夹​​中的文件，而不是包含文件的另一个文件夹，以此确保您已正确完成此操作。
 
 
### 其他注意事项
 
 如果多个机构共享具有不同名称或代码的同一站点，则 Google 地图等应用程序可能需要选择一个。为避免混淆，请与其他机构协调以就名称和代码达成一致。这可以最大限度地减少不同GTFS数据集之间的冲突。 
 
 如果您有多个可用的GTFS数据集（通常一个是为公共应用程序（如 Transit App）生成的，另一个是为内部操作CAD/AVL 系统生成的），您可能需要决定哪一个是已发布的GTFS。建议您选择推广包含最多面向乘客的信息的提要。尽可能让您的GTFS数据集匹配（stops和行程等的 ID 相同），以便内部数据集不会与公共数据集冲突，并且可以集成其他提要，如GTFS-RT。
 

