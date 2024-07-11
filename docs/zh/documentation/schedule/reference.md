##General Transit Feed Specification参考 
 
 **2024 年 5 月 22 日修订。有关更多详细信息，请参阅[修订历史记录](../change_history/revision_history)。** 
 
 本文档定义了组成GTFS数据集的文件的格式和结构。 
 
## 目录 
 
 1. [文档约定](#document-conventions) 
 2. [数据集文件](#dataset-files) 
 3. [文件要求](#file-requirements) 
 4. [数据集发布和一般做法](#dataset-publishing-general-practices) 
 5. [字段定义](#field-definitions) 
 - [agency.txt](#agencytxt) 
 - [stops.txt](#stopstxt) 
 - [routes.txt](#routestxt) 
 - [trips.txt](#tripstxt) 
 - [stop\_times.txt](#stop_timestxt) 
 - [calendar.txt](#calendartxt) 
 - [calendar\_dates.txt](#calendar_datestxt) 
 - [fare\_attributes.txt](#fare_attributestxt) 
 - [fare\_rules.txt](#fare_rulestxt) 
 - [timeframes.txt](#timeframestxt) 
 - [fare\_media.txt](#fare_mediatxt) 
 - [fare\_products.txt](#fare_productstxt) 
 - [fare\_leg\_rules.txt](#fare_leg_rulestxt) 
 - [fare\_transfer\_rules.txt](#fare_transfer_rulestxt) 
 - [areas.txt](#areastxt) 
 - [stop_areas.txt](#stop_areastxt) 
 - [networks.txt](#networkstxt) 
 - [route_networks.txt](#route_networkstxt) 
 - [shapes.txt](#shapestxt) 
 - [frequencies.txt](#frequenciestxt) 
 - [transfers.txt](#transferstxt) 
 - [pathways.txt](#pathwaystxt) 
 - [levels.txt](#levelstxt) 
 - [location_groups.txt](#location_groupstxt) 
 - [location_group_stops.txt](#location_group_stopstxt) 
 - [locations.geojson](#locationsgeojson) 
 - [booking_rules.txt](#booking_rulestxt) 
 - [translations.txt](#translationstxt) 
 - [feed\_info.txt](#feed_infotxt) 
 - [attributions.txt](#attributionstxt) 
 
## 文档约定 
 本文档中的关键词“必须”、“不得”、“要求”、“应”、“不应”、“应该”、“不应该”、“推荐”、“可以”和“可选”应按照[RFC 2119](https:)中所述进行解释。 
 
 
### 术语定义 
 
 本节定义了本文档中使用的术语。 
 
 * **数据集** - 本规范参考定义的一套完整的文件。更改数据集将创建该数据集的新版本。数据集应发布在公共的永久URL上，包括 zip 文件名。（例如，https: agency）。 
 * **记录**——由描述单个entity（例如，交通运输agency、站点、路线等）的多个不同字段值组成的基本数据结构。在表中表示为一行。
 * **字段**——对象或entity的属性。在表中表示为一列。如果在文件中添加为header，则该字段存在。它可能有或没有定义的字段值。
 * **字段值**——字段中的单个条目。在表中表示为单个单元格。
 * **服务日**——服务日是用来指示路线安排的时间段。服务日的具体定义因agency而异，但服务日通常与日历日不对应。如果服务在一天开始并在第二天结束，则服务日可能超过 24:00:00。例如，从周五 08:00:00 运行到周六 02:00:00 的服务，可以表示为在单个服务日内从 08:00:00 运行到 26:00:00。
 * **文本转语音字段** - 该字段应包含与其父字段相同的信息（如果为空，则返回父字段）。它旨在被阅读为文本转语音，因此，缩写应该被删除（“St”应该读作“Street”或“Saint”；“Elizabeth I”应该是“Elizabeth the first”）或保留原样（“JFK Airport”被缩写）。
 * **行程** - 乘客在旅途中的一对后续地点之间上车和下车的旅行。
 * **旅程** - 从出发地到目的地的总体旅行，包括所有行程和中途transfers。 
 * **子旅程** - 组成旅程子集的两个或多个航段。
 * **票价产品** - 可用于支付或验证旅行的可购买票价产品。
 
### 存在
 适用于字段和文件的存在条件：
 
 * **必需** - 字段或文件必须包含在数据集中，且包含每条记录的有效值。
 * **可选** - 字段或文件可以从数据集中省略。
 * **有条件必需** - 必须在字段或文件描述中概述的条件下包含字段或文件。
 * **有条件禁止** - 在字段或文件描述中概述的条件下不得包含字段或文件。
 * **推荐** - 可以从数据集中省略字段或文件，但最佳做法是将其包含进去。在省略此字段或文件之前，应仔细评估最佳实践，并了解省略的全部含义。
 
### 字段类型 
 
 - **颜色** - 编码为六位十六进制数的颜色。请参阅 [https://htmlcolorcodes.com](https:) 以生成有效值（不得包含前导“#”）。<br> *例如：`FFFFFF` 表示白色，` 000000` 表示黑色，或 `0039A6` 表示 NYMTA 中的 A、C、E 线。* 
 - **货币代码** - ISO 4217 字母currency代码。有关当前currency的列表，请参阅 [https://en.wikipedia.org/wiki/ISO_4217#Active\_codes](https:)。<br> *例如：`CAD` 表示加拿大元、`EUR` 表示欧元或 `JPY` 表示日元。* 
 - **货币amount** - 表示currencyamount的十进制值。小数位数由随附货币代码的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217#Active_codes) 指定。所有财务计算都应以十进制、currency或适用于财务计算的其他等效类型处理，具体取决于用于使用数据的编程语言。由于计算过程中会出现资金盈亏，因此不鼓励将currency金额处理为float。
 - **日期** - YYYYMMDD 格式的服务日。由于服务日内的时间可能高于 24:00:00，因此服务日可能包含后续日期的信息。<br> *例如：`20180913` 表示 2018 年 9 月 13 日。*
 - **Email** - 电子邮件地址。<br> *示例：`example@example.com`* 
 - **Enum** - “描述”列中定义的一组预定义常量中的一个选项。<br> *示例：`route_type字段包含 `0` 表示有轨电车， `1`表示地铁...* 
 - **ID** - ID 字段值是内部 ID，不打算显示给乘客，并且是任意 UTF-8 字符的序列。建议仅使用可打印的 ASCII 字符。当 ID 在文件中必须是唯一的时，它被标记为“唯一 ID”。一个.txt文件中定义的 ID 通常会在另一个.txt文件中引用。引用另一个表中的 ID 的 ID 被标记为“外部 ID”。<br> *示例：[stops.txt](#stopstxt) 中的`stop_id`字段是“唯一 ID”。[stops.txt](#stopstxt) 中的 ` parent_station字段是“引用 ` stops.stop_id的外部 ID”。* 
 - **语言代码** - IETF BCP 47 语言代码。有关 IETF BCP 47 的介绍，请参阅 [http://www.rfc-editor.org/rfc/bcp/bcp47 .txt](http://www.rfc-editor.org/rfc/bcp/bcp47 .txt) 和 [http://www.w3.org/International/articles/language-tags/](http ://www.w3.org/International/articles/language-tags/)。<br> *例如：`en` 表示英语，`en-US` 表示美式英语，`de` 表示德语。* 
 - **纬度** - 十进制度的 WGS84latitude。该值必须大于或等于 -90.0 且小于或等于 90.0。*<br>例如：罗马斗兽场的经度为 `41.890169`。* 
 - **经度** - 十进制度的 WGS84longitude。该值必须大于或等于 -180.0 且小于或等于 180.0。<br> *例如：罗马斗兽场的“12.492269”。* 
 - **Float** - 浮点数。 
 - **整数** - 整数。 
 - **Phone number** - 电话号码。 
 - **时间** - HH:MM:SS 格式的时间（也接受 H:MM:SS）。时间从服务日的“中午减 12 点”开始计算（除夏令时变更的日子外，实际上是午夜）。对于服务日午夜之后的时间，请以 HH:MM:SS 格式输入大于 24:00:00 的值。<br> *例如：`14:30:00` 表示下午 2:30，或 `25:35:00` 表示第二天凌晨 1:35。* 
 - **Text** - UTF-8string，用于显示，因此必须易于阅读。 
 - **时区** - [https://www.iana.org/time-zones](https://www.iana.org/time-zones) 中的 TZ 时区。时区名称从不包含空格字符，但可以包含下划线。请参阅 [http://en.wikipedia.org/wiki/List\_of\_tz\_zones](http://en.wikipedia.org/wiki/List\_of\_tz\_zones) 获取有效值列表。<br> *示例：`Asia/Tokyo`、`America/Los_Angeles` 或 `Africa/Cairo`。* 
 - **URL** - 包含 http://或 https://的完全限定URL ，并且URL中的任何特殊字符都必须正确转义。有关如何创建完全限定URL值的说明，请参阅以下 [http://www.w3.org/Addressing/URL/4\_URI\_Recommentations.html](http: URL/4\_URI\_Recommentations.html)。 
 
### 字段符号 
 适用于Float或整数字段类型的符号：
 
 * **非负** - 大于或等于 0。
 * **非零** - 不等于 0。
 * **正** - 大于 0。
 
 _示例：**非负float** - 大于或等于 0 的浮点数。_ 
 
### 数据集属性 
 数据集的**主键**是唯一标识一行的字段或字段组合。当文件提供的所有字段都用于唯一标识一行时，使用`Primary key (*)`。`Primary key (none)` 表示文件只允许一行。 
 
 _示例： `trip_id`和`stop_sequence`字段构成 [stop_times.txt](#stop_timestxt) 的主键。_ 
 
## 数据集文件 
 
 本规范定义了以下文件：
 
 | 文件名 | 存在 | 说明 | 
 |------|------|------| 
 | [agency.txt](#agencytxt) | **必需** | 本数据集中提供服务的交通运输机构。| 
 | [stops.txt](#stopstxt) | **必需** | 车辆接送乘客的站点。还定义了车站和车站入口。| 
 | [routes.txt](#routestxt) | **必需** | 交通routes。路线是向乘客显示为单一服务的一组行程。| 
 | [trips.txt](#tripstxt) | **必需** | 每条路线的行程。行程是在特定时间段内发生的两个或多个stops的序列。| 
 | [stop_times.txt](#stop_timestxt) | **必需** |vehicle每次行程到达和离开stops的时间。| 
 | [calendar.txt](#calendartxt) | **有条件必需** | 使用每周时间表指定的服务日期，包括开始日期和结束日期。<br><br>有条件要求：<br> - **必需**，除非所有服务日期均在 [calendar_dates.txt](#calendar_datestxt) 中定义。<br> - 其他情况下为可选。| 
 | [calendar_dates.txt](#calendar_datestxt) | **有条件要求** | [calendar.txt](#calendartxt) 中定义的服务的例外情况。<br><br>有条件要求：<br> - 如果省略 [calendar.txt](#calendartxt)，则 **必需**。在这种情况下，[calendar_dates.txt](#calendar_datestxt) 必须包含所有服务日期。<br> - 否则为可选。| 
 | [fare_attributes.txt](#fare_attributestxt) | 可选 | 交通运输机构routes的票价信息。| 
 | [fare_rules.txt](#fare_rulestxt) | 可选 | 适用于行程票价的规则。| 
 | [timeframes.txt](#timeframestxt) | 可选 | 票价规则中使用的日期和时间段，取决于date和时间因素。| 
 | [fare_media.txt](#fare_mediatxt) | 可选 | 描述可用于使用票价产品的票价媒体。<br><br>文件 [fare_media.txt](#fare_mediatxt) 描述了 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 中未表示的概念。因此，[fare_media.txt](#fare_mediatxt) 的使用与文件 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全不同。| 
 | [fare_products.txt](#fare_productstxt) | 可选 | 描述乘客可以购买的不同类型的车票或票价。<br><br>文件 [fare_products.txt](#fare_productstxt) 描述了 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 中未表示的票价产品。因此，[fare_products.txt](#fare_productstxt) 的使用与文件 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全不同。| 
 | [fare_leg_rules.txt](#fare_leg_rulestxt) | 可选 | 各段旅行的票价规则。<br><br>文件 [fare_leg_rules.txt](#fare_leg_rulestxt) 提供了一种更详细的票价结构建模方法。因此，[fare_leg_rules.txt](#fare_leg_rulestxt) 的使用与文件 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全不同。| 
 | [fare_transfer_rules.txt](#fare_transfer_rulestxt) | 可选 | 行程间transfers的票价规则。<br><br>与 [fare_leg_rules.txt](#fare_leg_rulestxt) 一起，文件 [fare_transfer_rules.txt](#fare_transfer_rulestxt) 提供了一种更详细的票价结构建模方法。 因此，[fare_transfer_rules.txt](#fare_transfer_rulestxt) 的使用与文件 [fare_attributes.txt](#fare_attributestxt) 和 [fare_rules.txt](#fare_rulestxt) 完全分开。 | 
 | [areas.txt](#areastxt) | 可选 | 位置的区域分组。 | 
 | [stop_areas.txt](#stop_areastxt) | 可选 | 将stops分配到区域的规则。 | 
 | [networks.txt](#networkstxt) | **有条件禁止** |routes的网络分组。<br><br>有条件禁止：<br> - 如果 [routes.txt](#routestxt) 中存在 ` network_id `，则**禁止**。<br> - 否则为可选。| 
 | [route_networks.txt](#route_networkstxt) | **有条件禁止** | 将routes分配给网络的规则。<br><br>有条件禁止：<br> - 如果 [routes.txt](#routestxt) 中存在 ` network_id `，则**禁止**。<br> - 其他情况下为可选。| 
 | [shapes.txt](#shapestxt) | 可选 | 绘制vehicle行驶路径的规则，有时也称为路线对齐。| 
 | [frequencies.txt](#frequenciestxt) | 可选 | 基于间隔时间的服务或固定时间表服务的压缩表示的间隔时间（行程间隔时间）。| 
 | [transfers.txt](#transferstxt) | 可选 | 在routes之间的换乘点建立连接的规则。| 
 | [pathways.txt](#pathwaystxt) | 可选 | 连接车站内各个位置的路径。| 
 | [levels.txt](#levelstxt) | **有条件要求** | 车站内的级别。<br><br>有条件要求：<br> - 描述带有电梯的pathways时**必需**（`pathway_mode=5）。<br> - 其他情况下为可选。| 
 | [location_groups.txt](#location_groupstxt) | 可选 | 一组stops，共同指示乘客可能请求接送的位置。| 
 | [location_group_stops.txt](#location_group_stopstxt) | 可选 | 将stops分配到位置组的规则。| 
 | [locations.geojson](#locationsgeojson) | 可选 | 按需服务的乘客接送请求区域，以 GeoJSON 多边形表示。| 
 | [booking_rules.txt](#booking_rulestxt) | 可选 | 乘客请求服务的预订信息。| 
 | [translations.txt](#translationstxt) | 可选 | 面向客户的数据集值的翻译。| 
 | [feed_info.txt](#feed_infotxt) | 可选 | 数据集元数据，包括发布者、版本和到期信息。 | 
 | [attributions.txt](#attributionstxt) | 可选 | 数据集attributions。| 
 
## 文件要求 
 
 以下要求适用于数据集文件的格式和内容： 
 
 * 所有文件必须保存为逗号分隔的文本。 
 * 每个文件的第一行必须包含字段名称。[字段定义](#field-definitions) 部分的每个小节对应于GTFS数据集中的一个文件，并列出了该文件中可能使用的字段名称。 
 * 所有文件和字段名称均区分大小写。 
 * 字段值不得包含制表符、回车符或换行符。 
 * 包含引号或逗号的字段值必须用引号括起来。此外，字段值中的每个引号前面都必须有一个引号。这与 Microsoft Excel 输出逗号分隔 (CSV) 文件的方式一致。有关 CSV 文件格式的更多信息，请参阅 [http://tools.ietf.org/html/rfc4180](http:)。
 以下示例演示了字段值在逗号分隔文件中的显示方式：
 * **原始字段值：** `Contains "quotes", commas and text` 
 * **CSV 文件中的字段值：** `"Contains ""quotes"", commas and text"` 
 * 字段值不得包含 HTML 标记、注释或转义序列。
 * 应删除字段或字段名称之间的多余空格。许多解析器将空格视为值的一部分，这可能cause错误。
 * 每行必须以 CRLF 或 LF 换行符结尾。 
 * 文件应使用 UTF-8 编码以支持所有 Unicode 字符。包含 Unicode 字节顺序标记 (BOM) 字符的文件是可以接受的。有关 BOM 字符和 UTF-8 的更多信息，请参阅 [http://unicode.org/faq/utf_bom.html#BOM](http:)。
 * 所有数据集文件必须压缩在一起。文件必须直接位于根目录，而不是子文件夹中。
 * 所有面向客户的文本字符串（包括站点名称、路线名称和路标）都应使用混合大小写（而非全部大写），并遵循当地惯例，在能够显示小写字符的显示器上将地名大写（例如“Brighton Churchill Square”、“Villiers-sur-Marne”、“Market Street”）。 
 * 在整个名称和其他文本的提要中应避免使用缩写（例如，将街道缩写为 St.），除非某个位置使用其缩写名称（例如，“JFK 机场”）。缩写可能会给屏幕阅读器软件和语音用户界面带来可访问性问题。消费软件可以设计为可靠地将完整单词转换为缩写以供显示，但从缩写转换为完整单词更容易出现错误。
 
## 数据集发布和一般做法
 
 * 数据集应在公共的永久URL上发布，包括 zip 文件名。（例如， agency/gtfs/gtfs.zip）。理想情况下， URL应该可直接下载，而无需登录即可访问文件，以方便消费软件应用程序下载。虽然建议（也是最常见的做法）将GTFS数据集公开下载，但如果数据提供商确实需要出于许可或其他原因控制对GTFS的访问，则建议使用 API 密钥控制对GTFS数据集的访问，这将有助于自动下载。
 * GTFS数据应以迭代形式发布，以便稳定位置的单个文件始终包含交通agency（或多个机构）的最新官方服务描述。
 * 数据集应尽可能在数据迭代中维护`stop_id`、 `route_id`和 `agency_id ` 的持久标识符（ id字段）。
 * 一个GTFS数据集应包含当前和即将推出的服务（有时称为“合并”数据集）。有多个[合并工具](../../../resources/gtfs/#gtfs-merge-tools)可用于从两个不同的GTFS供稿创建合并的数据集。 
 * 在任何时候，发布的GTFS数据集都应至少在接下来的 7 天内有效，理想情况下，只要运营商有信心该计划将继续运行，它就应该一直有效。
 * 如果可能， GTFS数据集应至少涵盖接下来 30 天的服务。
 * 应从供稿中删除旧服务（过期的日历）。
 * 如果服务修改将在 7 天或更短的时间内生效，则应通过GTFS实时供稿（服务咨询或行程更新）而不是静态GTFS数据集来表达此服务更改。
 * 应配置托管GTFS数据的 Web 服务器以正确报告文件修改date（请参阅[HTTP/1.1- 征求意见 2616，第 14.29 节](https:))。 
 
## 字段定义 
 
### agency.txt 
 
 文件：**必需** 
 
 主键（`agency_id`）
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `agency_id` | 唯一 ID | **有条件必需** | 标识通常与交通agency同义的交通品牌。请注意，在某些情况下，例如当单个agency运营多个独立服务时，机构和品牌是不同的。本文档使用术语“agency”代替“品牌”。数据集可能包含来自多个机构的数据。<br><br>有条件要求：<br> - 当数据集包含多个运输机构的数据时**必需**。<br> - 否则推荐。 | 
 | `agency_name` |Text| **必填** | 交通agency的全名。 | 
 | `agency_url` | URL | **必填** | 交通agency的URL 。 | 
 | ` agency_timezone` | 时区 | **必填** | 交通agency所在的时区。如果在数据集中指定了多个机构，则每个机构必须具有相同的 `agency_timezone`。 | 
 | `agency_lang` | 语言代码 | 可选 | 此交通agency使用的主要语言。应提供帮助GTFS消费者为数据集选择大写规则和其他特定于语言的设置。 | 
 | `agency_phone` |Phone number| 可选 | 指定agency的语音电话号码。此字段是一个string值，显示该机构服务区域的典型电话号码。它可能包含标点符号来对号码的数字进行分组。允许使用可拨号文本（例如，TriMet 的“503-238-RIDE”），但该字段不得包含任何其他描述性文本。| 
 | `agency_fare_url` | URL | 可选 | 允许乘客在线购买该agency的车票或其他票价工具的网页URL 。| 
 | ` agency_email` |Email| 可选 | 机构客户服务部门积极监控的Email地址。此电子邮件地址应是公交乘客可以联系agency客户服务代表的直接联系点。| 
 
### stops.txt 
 
 文件：**必填** 
 
 主键（`stop_id`）
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `stop_id` | 唯一 ID | **必填** |标识位置：站点/站台、车站、入口/出口、通用节点或登车区（参见“`location_type`”）。<br><br>在所有 `stops.stop_id、 locations.geojson `id`和 `location_groups.location_group_id` 值中，ID 必须是唯一的。<br><br>多条routes可能使用相同的`stop_id`。| 
 | `stop_code|Text| 可选 | 用于为乘客识别位置的简短文本或数字。这些代码通常用于基于电话的交通信息系统或印在标牌上，以便乘客更轻松地获取特定位置的信息。如果是面向公众的，`stop_code可能与`stop_id`相同。对于没有向乘客显示代码的位置，此字段应留空。| 
 | `stop_name|Text| **有条件必需** | 位置的名称。`stop_name应与机构面向乘客的位置名称相匹配，该名称印在时刻表上、在线发布或标牌上。要翻译成其他语言，请使用 [translations.txt](#translationstxt)。<br><br>当位置为登车区（`location_type=4`）时，`stop_name应包含agency显示的登车区名称。它可以只是一个字母（例如在欧洲的一些城际火车站），也可以是文本，例如“轮椅登车区”（纽约地铁）或“短途列车头”（巴黎 RER）。<br><br>有条件要求：<br> - 对于stops（`location_type=0`）、车站（`location_type=1`）或入口/出口（`location_type=2`）的位置，**必需**。<br> - 对于一般节点 (`location_type=3`) 或登机区 (`location_type=4`) 的位置，为可选。| 
 | `tts_stop_name` |Text| 可选 | `stop_name` 的可读版本。有关更多信息，请参阅 [术语定义](#term-definitions) 中的“文本转语音字段”。| 
 | `stop_desc` |Text| 可选 | 提供有用、高质量信息的位置描述。不应与 `stop_name` 重复。| 
 | `stop

lat` | 纬度 | **有条件要求** | 位置的纬度。<br><br>对于stops/站台（`location_type=0`）和上车区域（`location_type=4`），坐标必须是公交车杆的坐标（如果存在），否则必须是旅客上vehicle的位置（在人行道或站台上，而不是在vehiclestops的道路或轨道上）。<br><br>有条件要求：<br> - 对于stops（`location_type=0`）、车站（`location_type=1`）或入口/出口（`location_type=2`）的位置，**必需**。<br> - 对于通用节点（`location_type=3`）或登机区域（`location_type=4`）的位置是可选的。| 
 | `stop_lon` | 经度 | **有条件要求** | 位置的经度。<br><br>对于stops/站台（`location_type=0`）和上车区域（`location_type=4`），坐标必须是公交车杆的坐标（如果存在），否则必须是旅客上vehicle的位置（在人行道或站台上，而不是在vehiclestops的道路或轨道上）。<br><br>有条件要求：<br> - 对于stops（`location_type=0`）、车站（`location_type=1`）或入口/出口（`location_type=2`）的位置，**必需**。<br> - 对于通用节点（`location_type=3`）或登机区（`location_type=4`）的位置，可选。|
|`zone_id|ID|可选|标识站点的票价区域。如果此记录代表车站或车站入口，则忽略`zone_id。|
|`stop_url| URL |可选|有关该位置的网页的URL 。这应该与`agency.agency_url和`routes.route_url字段值不同。|
| `location_type` |枚举|可选|位置类型。有效选项为：<br><br> `0`（或空白）- **站点**（或 **站台**）。乘客上vehicle或下车的地点。在 `parent_station中定义时称为站台。<br> `1` - **车站**。包含一个或多个平台的物理结构或区域。<br> `2` - **入口/出口**。乘客可以从街道进入或离开车站的位置。如果一个入口/出口属于多个车站，则可以通过pathways将其连接到两个车站，但数据提供者必须选择其中一个作为父级。<br> `3` - **通用节点**。车站内的一个位置，不匹配任何其他`location_type` ，可用于将 [pathways.txt](#pathwaystxt) 中定义的pathways链接在一起。<br> `4` - **登车区**。站台上的特定位置，乘客可在此上下车。| 
 | ` parent_station` | 引用 `stops.stop_id` 的外部 ID | **有条件要求** | 定义 [stops.txt](#stopstxt) 中定义的不同位置之间的层次结构。它包含父位置的 ID，如下所示：<br><br> - **Stop/platform**（`location_type=0`）：`parent_station字段包含车站的 ID。<br> - **Station** (`location_type=1`)：此字段必须为空。<br> - **入口/出口** (`location_type=2`) 或 **通用节点** (`location_type=3`): `parent_station字段包含车站 ID (`location_type=1`)<br> - **登机区** (`location_type=4`): `parent_station字段包含站台的 ID。<br><br>有条件要求：<br> - 对于入口（`location_type=2`）、通用节点（`location_type=3`）或登机区（`location_type=4`）的位置，**必需**。<br> -stops/平台可选（`location_type=0`）。<br> - 禁止用于车站（`location_type=1`）。| 
 |`stop_timezone| 时区 | 可选 | 位置的时区。如果位置有父站，它将继承父站的时区，而不是应用自己的时区。`stop_timezone` 为空的车站和无父stops将继承` agency.agency_timezone指定的时区。[stop_timezone](# stop_times.txt) 中提供的时间在`agency.agency_timezone指定的时区中，而不是`stop_timezone。这可确保行程中的时间值始终在行程过程中增加，无论行程穿越哪些时区。|
 |`wheelchair_boarding|枚举|可选|表示是否可以从该位置登上轮椅。有效选项为：<br><br>对于无父母stops：<br> `0` 或空 - 没有关于站点的可达性信息。<br> `1` - 此站的某些车辆可供坐轮椅的乘客搭乘。<br> `2` — 此站无法搭乘轮椅。<br><br>对于儿童stops：<br> `0` 或空 - 如果在父级中指定，站点将从父站继承其 `wheelchair_boarding行为。<br> `1` - 从车站外到特定站点/站台存在某条可达的路径。<br> `2` - 从车站外到特定站点/站台没有可访问的路径。<br><br>对于车站入口/出口：<br> `0` 或空 - 如果为父站指定了，车站入口将从父站继承其 `wheelchair_boarding行为。<br> `1`车站入口适合轮椅通行。<br> `2` - 从车站入口到stops/站台没有可访问的路径。| 
 | `level_id` | 引用 `levels.level_id` 的外部 ID | 可选 | 位置的级别。多个未链接的车站可以使用相同的级别。| 
 | `platform_code` |Text| 可选 | 站台站点（属于车站的站点）的平台标识符。这应该只是平台标识符（例如“G”或“3”）。不应包括“平台”或“轨道”（或供稿的特定语言等效词）等词。这允许供稿消费者更轻松地将平台标识符国际化和本地化为其他语言。| 
 
 
### routes.txt 
 
 文件：**必需** 
 
 主键（`route_id`）
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `route_id` |唯一 ID | **必需** | 标识一条路线。| 
 | `agency_id` | 引用 `agency.agency_id` 的外部 ID | **有条件必需** | 指定路线的代理机构。<br><br>有条件要求：<br> - 如果在 [agency.txt](#agencytxt) 中定义了多个机构，则 **必需**。<br> - 否则建议使用。| 
 | `route_short_name` |Text| **有条件要求** | 路线的简称。通常是乘客用来识别路线的简短抽象标识符（例如“32”、“100X”、“Green”）。可以同时定义 `route_short_name` 和 `route_long_name`。<br><br>有条件要求：<br> - 如果 `routes.route_long_name为空，则**必需**。<br> - 如果有简短的服务名称，则建议使用。这应该是该服务的乘客常用名称，并且不应超过 12 个字符。| 
 | `route_long_name` |Text| **有条件要求** | 路线的全名。此名称通常比 `route_short_name` 更具描述性，并且通常包括路线的目的地或站点。`route_short_name` 和 `route_long_name` 都可以定义。<br><br>有条件要求：<br> - 如果 `routes.route_short_name为空，则**必需**。<br> - 否则为可选。| 
 | `route_desc` |Text| 可选 | 提供有用、优质信息的路线描述。不应与 `route_short_name` 或 `route_long_name` 重复。<hr> _示例：“A”列车始终在曼哈顿 Inwood-207 街和皇后区 Far Rockaway-Mott Avenue 之间运行。此外，从早上 6 点到午夜左右，额外的“A”列车在 Inwood-207 街和 Lefferts Boulevard 之间运行（列车通常在 Lefferts Blvd 和 Far Rockaway 之间交替运行）。_ | 
 | `route_type` | 枚举 | **必需** | 表示路线上使用的交通类型。有效选项为：<br><br> `0` - 有轨电车、有轨电车、轻轨。大都市区域内的任何轻轨或街道级系统。<br> `1` - 地铁。大都市区域内的任何地下铁路系统。<br> `2` - 铁路。用于城际或长途旅行。<br> `3` - 巴士。用于短途和长途巴士routes。<br> `4` - 渡轮。用于短途和长途船舶服务。<br> `5` - 缆车。用于电缆在vehicle下方运行的街道轨道车（例如旧金山的缆车）。<br> `6` - 空中缆车、悬挂式缆车（例如，缆车、空中索道）。缆车是一种缆车运输方式，其中车厢、车厢、缆车或敞篷车通过一条或多条缆绳悬挂起来。<br> `7` - 缆车。任何专为陡坡设计的轨道系统。<br> `11` - 无轨电车。利用电线杆从架空电线获取电力的电动公交车。<br> `12` - 单轨铁路。轨道由单轨或梁组成的铁路。| 
 | `route_url` | URL | 可选 | 有关特定路线的网页的URL 。应与 `agency.agency_url` 值不同。| 
 | `route_color` | 颜色 | 可选 | 与面向公众的材料相匹配的路线颜色指定。省略或留空时默认为白色（`FFFFFF`）。在黑白屏幕上查看时，`route_color` 和 `route_text_color` 之间的颜色差异应提供足够的对比度。| 
 | `route_text_color` | 颜色 | 可选 | 用于在 `route_color` 背景下绘制的文本的清晰颜色。省略或留空时默认为黑色（`000000`）。在黑白屏幕上查看时，`route_color` 和 `route_text_color` 之间的颜色差异应提供足够的对比度。| 
 | `route_sort_order` | 非负整数 |可选 | 以最适合向客户展示的方式对routes进行排序。`route_sort_order` 值较小的路线应首先显示。| 
 | `continuous_pickup` | 枚举 | **有条件禁止** | 表示乘客可以在路线的每次行程中，按照 [shapes.txt](#shapestxt) 描述的车辆行驶路径上的任何一点登上vehicle。有效选项包括：<br><br> `0`-连续停止拾音。<br> “`1`”或空 – 无连续停止拾音。<br> `2` – 必须打电话agency安排连续停止取货。<br> `3` – 必须与司机协调安排连续停车接送。<br><br>可以通过在“`stop_times.continuous_pickup`”中定义沿途特定“stop_time ”的值来覆盖“`routes.continuous_pickup`”的值。<br><br> **有条件禁止**：<br> - 如果此路线的任何行程定义了 ` stop_times或 ` stop_times ，则**禁止** 。<br> - 其他情况下可选。| 
 | `continuous_drop_off` | 枚举 | **有条件禁止** | 表示乘客可以在路线的每次行程中，按照 [shapes.txt](#shapestxt) 描述的vehicle行驶路径上的任何一点下车。有效选项包括：<br><br> `0`-连续停止下降。<br> “`1`”或空 - 没有连续停止下降。<br> `2` – 必须打电话给agency安排连续停车送达。<br> `3` – 必须与司机协调安排连续停车下车。<br><br>可以通过在“ stop_times.continuous_drop_off”中定义沿途特定“stop_time ”的值来覆盖“ routes.continuous_drop_off ”的值。<br><br> **有条件禁止**：<br> - 如果此路线的任何行程定义了 ` stop_times或 ` stop_times ，则**禁止** 。<br> - 其他情况下可选。| 
 | `network_id` | ID | **有条件禁止** | 标识一组routes。[routes.txt](#routestxt) 中的多行可能具有相同的 `network_id`。<br><br>有条件禁止：<br> - 如果 [route_networks.txt](#route_networkstxt) 文件存在，则 **禁止**。<br> - 其他情况下为可选。
 
### trips.txt 
 
 文件：**必需** 
 
 主键（`trip_id`）
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `route_id` | 引用`routes.route_id的外部 ID | **必需** | 标识路线。|
 |`service_id| 引用`calendar.service_id或`calendar_dates.service_id的外部 ID |**必需** | 标识一条或多条routes可提供服务的一组日期。|
 | `trip_id` |唯一 ID |**必需** | 标识一次旅行。|
 |`trip_headsign|Text|可选 | 出现在标牌上的Text，向乘客标识旅行的目的地。应用于区分同一路线上的不同服务模式。<br><br>如果车头标志在行程中发生变化，则可以通过在 ` stop_times.stop_headsign中为行程中的特定 `stop_time定义值来覆盖 ` trip_headsign的值。|
|` trip_short_name|Text|可选|用于向乘客识别行程的面向公众的文本，例如，识别通勤铁路行程的列车号码。如果乘客通常不依赖行程名称，则`trip_short_name应该为空。如果提供了`trip_short_name值，则该值应该唯一地标识服务日内的行程；它不应该用于目的地名称或有限/特快指定。|
| `direction_id` |枚举|可选|表示行程的行进方向。此字段不应在路线规划中使用；它提供了一种在发布时间表时按方向分开行程的方法。有效选项为：<br><br> `0`-单向行驶（例如出站行驶）。<br> `1`向相反方向行驶（例如入境行驶）。<hr> *示例：`trip_headsign和`direction_id`字段可一起使用，为一系列行程的每个方向指定一个名称。[trips.txt](#tripstxt) 文件可包含这些记录，用于时间表：*<br> `trip_id,...,trip_headsign,direction_id`<br> `1234,...,Airport,0`<br> `1505,...,Downtown,1` | 
 | `block_id` | ID | 可选 | 标识行程所属的区块。区块由单次行程或使用同一vehicle进行的多次连续行程组成，由共享的服务日和 `block_id` 定义。`block_id` 可能包含服务日不同的行程，从而构成不同的区块。请参阅[下面的示例](#example-blocks-and-service-day)。若要提供座位内transfers信息，应提供 ` transfer_type ` `4` 的 [transfers](#transferstxt)。| 
 | `shape_id` | 引用 `shapes.shape_id ` 的外部 ID | **有条件要求** | 标识描述行程vehicle行驶路径的地理空间shape。<br><br>有条件要求：<br> - 如果行程在 [routes.txt](#routestxt) 或 [stop_times.txt](#stop_timestxt) 中定义了连续的接送行为，则 **必需**。<br> - 否则为可选。| 
 | `wheelchair_accessible` | 枚举 | 可选 | 表示轮椅可访问性。有效选项包括：<br><br> `0` 或空 — 没有关于此行程的可达性信息。<br> `1`本次行程所使用的车辆至少可容纳一名坐轮椅的乘客。<br> `2` - 此行程不允许坐轮椅的乘客。| 
 | `bikes_allowed` | 枚举 | 可选 | 表示是否允许骑自行车。有效选项包括：<br><br> `0` 或空 - 此行程没有自行车信息。<br> `1`本次行程所使用的车辆至少可容纳一辆自行车。<br> `2` - 此行程不允许骑自行车。| 
 
#### 示例：区块和服务日 
 
 以下示例有效，每周每天都有不同的区块。
 
 | route_id | trip_id | service_id | block_id | <span style="font-weight:normal">*(第一次停止时间)*</span> | <span style="font-weight:normal">*(最后一次停止时间)*</span> | 
 |----------|---------|--------------------------------|-------------------------|-----------------------------------------|-----------------------------------------| 
 | red | trip_1 | 周一-周二-周三-周四-周五-周六-周日 | red_loop | 22:00:00 | 22:55:00 | 
 | red | trip_2 | 周五-周六-周日 | red_loop | 23:00:00 | 23:55:00 | 
 | red | trip_3 | 周五-周六 | red_loop 24:00:00 | 24:55:00 | 
 | red | trip_4 | 周一-周二-周三-周四 | red_loop | 20:00:00 | 20:50:00 | 
 | red | trip_5 | 周一-周二-周三-周四 | red_loop | 21:00:00 | 21:50:00 | 
 
 上表注释：
 
 * 例如，从周五到周六早上，一辆vehicle运行 `trip_1、`trip_2和 `trip_3（晚上 10:00 到凌晨 12:55）。请注意，最后一次行程发生在周六凌晨 12:00 到凌晨 12:55，但它是周五“服务日”的一部分，因为时间为 24:00:00 到 24:55:00。 
 * 周一、周二、周三和周四，一辆vehicle在晚上 8:00 到 10:55 的时间段内运行 `trip_1、`trip_4和 `trip_5### stop_times.txt 
 
 文件：**必需** 
 
 主键（`trip_id`， `stop_sequence`）
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `trip_id` | 引用`trips.trip_id`的外部 ID | **必需** | 标识一次行程。| 
 | `arrival_time | 时间 | **有条件必需** |在由 ` agency.agency_timezone指定的时区内（由 ` stop_times.stop_id定义），特定行程（由 `stop_times.trip_id定义）到达站点（由 `stop_times.stop_id` 定义）的时间，而不是由 ` stops.stop_timezone定义。<br><br>如果站点没有单独的arrival和departure时间，则“arrival_time”和“`departure_time`”应该相同。<br><br>对于服务日午夜之后的时间，请以 HH:MM:SS 格式输入大于 24:00:00 的值。<br><br>如果没有准确的arrival和departure时间（`timepoint=1` 或空），则应提供估计或插入的arrival和departure时间（`timepoint=0`）。<br><br>有条件要求：<br> - 行程中的第一站和最后一站**必需**（由“stop_times.stop_sequence”定义）。<br> - 对于 `timepoint=1来说**是必需的**。<br> - 当定义“`start_pickup_drop_off_window`”或“`end_pickup_drop_off_window`”时**禁止**。<br> - 其他情况下可选。| 
 | `departure_time` | 时间 | **有条件要求** | 在由 ` agency.agency_timezone指定的时区内（由 ` stop_times.stop_id定义），特定行程（由 `stop_times.trip_id定义）从站点（由 `stop_times.stop_id` 定义）出发的时间，而不是由 ` stops.stop_timezone定义的时区。<br><br>如果站点没有单独的arrival和departure时间，则“arrival_time”和“`departure_time`”应该相同。<br><br>对于服务日午夜之后的时间，请以 HH:MM:SS 格式输入大于 24:00:00 的值。<br><br>如果没有准确的arrival和departure时间（`timepoint=1` 或空），则应提供估计或插入的arrival和departure时间（`timepoint=0`）。<br><br>有条件要求：<br> - 对于 `timepoint=1来说**是必需的**。<br> - 当定义“`start_pickup_drop_off_window`”或“`end_pickup_drop_off_window`”时**禁止**。<br> - 其他情况下可选。| 
 | `stop_id` | 引用 `stops.stop_id的外部 ID | **有条件必需** | 标识服务的站点。行程期间服务的所有stops都必须在 [stop_times.txt](#stop_timestxt) 中有记录。引用的位置必须是stops/平台，即它们的 `stops.location_type值必须为 `0` 或空。一个站点可能在同一行程中服务多次，并且多个行程和routes可能为同一站点提供服务。<br><br>使用stops的按需服务应按stops提供服务的顺序引用。数据消费者应假设可以从一个站点或地点到行程中的任意站点或地点旅行，前提是每个stop_time的“pickup/drop_off_type ”和每个“start/end_pickup_drop_off_window”的时间限制不禁止这样做。<br><br>有条件要求：<br> - 如果 `stop_times和 `stop_times未定义，则**必需**。<br> - 如果定义了 `stop_times.location_group_id` 或 `stop_times.location_id`，则**禁止**。| 
 | `location_group_id` | 引用 `location_groups.location_group_id` 的外部 ID | **有条件禁止** | 标识服务地点组，该组指示乘客可以请求接送的stops组。行程期间服务的所有地点组都必须在 [stop_times.txt](#stop_timestxt) 中有记录。多个行程和routes可以为同一地点组提供服务。<br><br>使用位置组的按需服务应按照这些位置组提供的服务的顺序引用。数据消费者应假设可以从一个站点或位置到行程中的任意站点或位置，前提是每个stop_time的“pickup/drop_off_type ”和每个“start/end_pickup_drop_off_window”的时间限制不禁止这样做。<br><br> **有条件禁止**：<br> - 如果定义了 `stop_times.stop_id` 或 `stop_times.location_id`，则**禁止**。| 
 | `location_id` | 引用`locations.geojson`中的`id`的外部 ID | **有条件禁止** | 标识与乘客可能请求接送的服务区域相对应的 GeoJSON 位置。行程期间服务的所有 GeoJSON 位置都必须在 [stop_times.txt](#stop_timestxt) 中有记录。多条行程和routes可能为同一个 GeoJSON 位置提供服务。<br><br>应按照这些位置的服务可用顺序引用位置内的按需服务。数据消费者应假设可以从一个站点或位置到行程中的任意站点或位置，前提是每个stop_time的“pickup/drop_off_type ”和每个“start/end_pickup_drop_off_window”的时间限制不禁止这样做。<br><br> **有条件禁止**：<br> - 如果定义了 `stop_times.stop_id` 或 `stop_times.location_group_id`，则**禁止**。| 
 | `stop_sequence` | 非负整数 | **必需** | 特定行程的stops、位置组或 GeoJSON 位置的顺序。值必须沿行程增加，但不必连续。<hr> *示例：行程中的第一个地点可以有`stop_sequence`= `1`，行程中的第二个地点可以有`stop_sequence`=`23`，第三个地点可以有`stop_sequence`=`40`，等等。*<br><br>在同一位置组或 GeoJSON 位置内旅行需要 [stop_times.txt](#stop_timestxt) 中具有相同 `location_group_id` 或 `location_id` 的两个记录。| 
 | `stop_headsign` |Text| 可选 | 出现在标牌上的Text，用于向乘客标识行程目的地。当标牌在stops之间变化时，此字段将覆盖默认的 ` trips.trip_headsign 。如果标牌在整个行程中都显示，则应使用 ` trips.trip_headsign 。<br><br>为一个 ` stop_time指定的 ` stop_headsign值不适用于同一行程中的后续 ` stop_time 。如果您想覆盖同一行程中多个 ` stop_time的 ` trip_headsign ，则必须在每个 ` stop_time行中repeated` stop_headsign值。| 
 | `start_pickup_drop_off_window` | 时间 | **有条件要求** | 按需服务在 GeoJSON 位置、位置组或站点中可用的时间。<br><br> **有条件要求**：<br> - 如果定义了 `stop_times或 `stop_times，则**必需**。<br> - 如果定义了“`end_pickup_drop_off_window`” ，则**必需**。<br> - 如果定义了“arrival_time”或“`departure_time`” ，则**禁止**。<br> - 其他情况下可选。| 
 | `end_pickup_drop_off_window` | 时间 | **有条件要求** | 按需服务在 GeoJSON 位置、位置组或停止处结束的时间。<br><br> **有条件要求**：<br> - 如果定义了 `stop_times或 `stop_times，则**必需**。<br> - 如果定义了“`start_pickup_drop_off_window`” ，则**必需**。<br> - 如果定义了“arrival_time”或“`departure_time`” ，则**禁止**。<br> - 否则为可选。| 
 | `pickup_type` | 枚举 | **有条件禁止** | 表示拾取方法。有效选项为：<br><br> `0` 或空 – 定期安排取货。<br> `1` — 没有可用的拾取物。<br> `2` – 必须打电话给agency安排取货。<br> `3` – 必须与司机协调安排接送。<br><br> **有条件禁止**：<br> - 如果定义了`start_pickup_drop_off_window`或`end_pickup_drop_off_window` ，则 **禁止** ` pickup_type =0`。<br> - 如果定义了`start_pickup_drop_off_window`或`end_pickup_drop_off_window` ，则 **禁止** ` pickup_type =3`。<br> - 否则为可选。| 
 | ` drop_off_type` | 枚举 | **有条件禁止** | 表示丢弃方法。有效选项为：<br><br> `0` 或空 – 定期下车。<br> `1` – 没有可用的下车地点。<br> `2` – 必须打电话给agency安排送达。<br> `3` – 必须与司机协调安排下车。<br><br> **有条件禁止**：<br> - 如果定义了`start_pickup_drop_off_window`或`end_pickup_drop_off_window` ，则 **禁止** ` drop_off_type =0`。<br> - 其他情况下为可选项。| 
 | `continuous_pickup` | 枚举 | **有条件禁止** | 表示乘客可以在 [shapes.txt](#shapestxt) 描述的车辆行驶路径上的任何一点登上vehicle，从此 ` stop_time ` 到行程`stop_sequence`中的下一个 ` stop_time `。有效选项包括：<br><br> `0`-连续停止拾音。

br> `1`或空 - 没有连续停止拾音。<br> `2` – 必须打电话agency安排连续停止取货。<br> `3` – 必须与司机协调安排连续停车接送。<br><br>如果此字段已填充，它将覆盖 [routes.txt](#routestxt) 中定义的任何连续接送行为。如果此字段为空，则 `stop_time` 将继承 [routes.txt](#routestxt) 中定义的任何连续接送行为。<br><br> **有条件禁止**：<br> - 如果定义了“`start_pickup_drop_off_window`”或“`end_pickup_drop_off_window`” ，则**禁止**。<br> - 其他情况下可选。| 
 | `continuous_drop_off` | 枚举 | **有条件禁止** | 表示乘客可以在 [shapes.txt](#shapestxt) 描述的车辆行驶路径上的任何一点vehicle，从此 ` stop_time ` 到行程`stop_sequence`中的下一个 ` stop_time `。有效选项包括：<br><br> `0`-连续停止下降。<br> “`1`”或空 - 没有连续停止下降。<br> `2` – 必须打电话给agency安排连续停车送达。<br> `3` – 必须与司机协调安排连续停车下客。<br><br>如果此字段已填充，它将覆盖 [routes.txt](#routestxt) 中定义的任何连续下车行为。如果此字段为空，则 `stop_time` 将继承 [routes.txt](#routestxt) 中定义的任何连续下车行为。<br><br> **有条件禁止**：<br> - 如果定义了“`start_pickup_drop_off_window`”或“`end_pickup_drop_off_window`” ，则**禁止**。<br> - 否则为可选。| 
 | `shape_dist_traveled` | 非负float| 可选 | 从第一个站点到此记录中指定的站点沿相关shape行驶的实际距离。此字段指定在行程中任意两个stops之间绘制的shape范围。必须采用与 [shapes.txt](#shapestxt) 相同的单位。用于`shape_dist_traveled`的值必须与`stop_sequence`一起增加；它们不得用于显示沿路线的反向旅行。<br><br>建议用于有环路或内联的routes（vehicle在一次行程中穿过或行驶过相同的路线部分）。请参阅 [`shapes.shape_dist_traveled`](#shapestxt)。<hr> *示例：如果公交车从shape起点到站点行驶 5.25 公里，`shape_dist_traveled`=`5.25`。*| 
 | `timepoint ` | 枚举 | 推荐 | 表示vehicle是否严格遵守站点的arrival和departure时间，或者它们是否是近似值和/或插值时间。此字段允许GTFS生产者提供插值的停止时间，同时指示时间为近似值。有效选项为：<br><br> `0`-时间被视为近似值。<br> `1`或空 - 时间被视为准确时间。| 
 | `pickup_booking_rule_id` | 引用 `booking_rules.booking_rule_id` 的 ID | 可选 | 标识此停止时间的登机预订规则。<br><br>当 `pickup_type=2` 时推荐使用。| 
 | `drop_off_booking_rule_id` | 引用 `booking_rules.booking_rule_id` 的 ID | 可选 | 标识此停止时间的下车预订规则。<br><br>当 `drop_off_type =2` 时推荐使用。| 
 
#### 按需服务路线行为 
 - 在提供出发地和目的地之间的路线或旅行时间时，数据消费者应忽略具有相同`trip_id`且定义了`start_pickup_drop_off_window`和`end_pickup_drop_off_window`的中间stop_times.txt记录。有关应忽略内容的示例，请参阅[数据示例页面](../examples/flex/#ignoring-intermediate-stop-times-records-with-pickupdrop-off-windows)。 
 - 禁止两个或多个具有相同`trip_id`的stop_times.txt记录之间同时重叠locations.geojson `id`几何、`start/end_pickup_drop_off_window时间和 `pickup_type或 `drop_off_type 。有关禁止行为的示例，请参阅[数据示例页面](../examples/flex/#zone-overlap-constraint)。
 
### calendar.txt 
 
 文件：**有条件必需** 
 
 主键（`service_id`）
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `service_id` | 唯一 ID | **必需** | 标识一个或多个routes可提供服务的日期集合。| 
 | `monday ` | 枚举 | **必需** | 指示服务是否在`start_date`和 `end_date ` 字段指定的date范围内的所有星期一运行。请注意，特定日期的例外情况可能会列在 [calendar_dates.txt](#calendar_datestxt) 中。有效选项包括：<br><br> `1`服务在该date范围内的所有星期一可用。<br> `0` -date范围内的星期一不提供服务。| 
 | `tuesday` | 枚举 | **必需** | 功能与 `monday` 相同，但适用于星期二 | 
 | `wednesday` | 枚举 | **必需** | 功能与 `monday` 相同，但适用于星期三 | 
 | `thursday` | 枚举 | **必需** | 功能与 `monday` 相同，但适用于星期四 | 
 | `friday` | 枚举 | **必需** | 功能与 `monday` 相同，但适用于星期五 | 
 | `saturday` | 枚举 | **必需** | 功能与 `monday` 相同，但适用于星期六。| 
 | `sunday` | 枚举 | **必需** | 功能与 `monday` 相同，但适用于星期日。| 
 | `start_date` | 日期 | **必填** | 服务间隔的开始服务日。 | 
 | `end_date` | 日期 | **必填** | 服务间隔的结束服务日。此服务日包含在间隔内。 | 
 
### calendar_dates.txt 
 
 文件：**有条件必填** 
 
 主键（`service_id`，`date`）
 
 [calendar_dates.txt](#calendar_datestxt) 表明确按date激活或禁用服务。它可以用两种方式使用。
 
 * 推荐：将 [calendar_dates.txt](#calendar_datestxt) 与 [calendar.txt](#calendartxt) 结合使用，以定义 [calendar.txt](#calendartxt) 中定义的默认服务模式的例外情况。如果服务通常是定期的，但在具体的日期会有一些变化（例如，为了适应特殊活动服务或学校时间表），这是一个很好的方法。在这种情况下，`calendar_dates.service_id` 是一个引用 `calendar.service_id` 的外部 ID。
 * 替代方案：省略 [calendar.txt](#calendartxt)，并在 [calendar_dates.txt](#calendar_datestxt) 中指定每个服务date。这允许相当大的服务变化，并适应没有正常每周时间表的服务。在这种情况下，` service_id` 是一个 ID。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `service_id` | 引用 `calendar.service_id` 的外部 ID 或 ID | **必需** | 标识一个或多个routes发生服务异常的日期集合。如果同时使用 [calendar_dates.txt](#calendartxt) 和 [calendar_dates.txt](#calendar_datestxt)，则每个 (` service_id`, `date `) 对只能在 [calendar.txt](#calendar_datestxt) 中出现一次。如果 ` service_id ` 值同时出现在 [calendar.txt](#calendartxt) 和 [calendar_dates.txt](#calendar_datestxt) 中，则 [calendar_dates.txt](#calendar_datestxt) 中的信息将修改 [calendar.txt](#calendartxt) 中指定的服务信息。| 
 | `date` | 日期 | **必需** | 服务异常发生的日期。| 
 | `exception_type ` | 枚举 | **必需** | 指示服务是否在date字段中指定的date可用。有效选项为：<br><br> `1` — 已添加指定date的服务。<br> `2` — 指定date的服务已被取消。<hr> *示例：假设某条路线在节假日有一组行程，在其他日子有另一组行程。一个 `service_id` 可以对应于常规服务时间表，另一个 `service_id` 可以对应于节假日时间表。对于特定节假日，可以使用 [calendar_dates.txt](#calendar_datestxt) 文件将节假日添加到节假日 `service_id` 中，并从常规 `service_id` 时间表中删除节假日。* | 
 
### fare_attributes.txt 
 
 文件：**可选** 
 
 主键（`fare_id`）
 
 **版本**<br> GTFS有两种建模选项可用于描述票价。GTFS- Fares V1是用于描述最少票价信息的传统选项。GTFS- Fares V2是一种更新的方法，可以更详细地说明代理商的票价结构。两者都可以存在于数据集中，但数据消费者对于给定的数据集只能使用一种方法。建议GTFS- Fares V2优先于GTFS- Fares V1。<br><br>与GTFS- Fares V1相关的文件是：<br> - [fare_attributes.txt](#票价属性txt)<br> - [fare_rules.txt](#票价规则txt)<br><br>与GTFS- Fares V2相关的文件是：<br> - [票价媒体.txt](#票价媒体txt)<br> - [fare_products.txt](#fare_productstxt)<br> - [fare_leg_rules.txt](#fare_leg_rulestxt)<br> - [fare_transfer_rules.txt](#票价转移规则txt) 
 
<br> 
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `fare_id` | 唯一 ID | **必填** | 标识票价等级。 | 
 | `price` | 非负float| **必填** |price，以 `currency_type` 指定的单位表示。 | 
 | `currency_type` | 货币代码 | **必填** | 用于支付票价的货币。 | 
 | `payment_method` | 枚举 | **必填** | 指示必须何时支付票价。有效选项为：<br><br> `0`-车费在车上支付。<br> `1` - 必须在登机前支付票价。| 
 | `transfers` | 枚举 | **必需** | 表示此票价允许的transfers次数。有效选项为：<br><br> `0`—此票价不允许transfers。<br> `1`乘客可以转乘一次。<br> `2`-乘客可以换乘两次。<br>空 – 允许无限制transfers。| 
 | `agency_id` | 引用 `agency.agency_id` 的外国 ID | **有条件要求** | 识别票价的相关agency。<br><br>有条件要求：<br> - 如果在 [agency.txt](#agencytxt) 中定义了多个机构，则 **必需**。<br> - 否则推荐。| 
 | `transfer_duration` | 非负整数 | 可选 | 换乘到期前的时间长度（以秒为单位）。当`transfers`=`0` 时，此字段可用于指示票的有效期，也可以留空。| 
 
### fare_rules.txt 
 
 文件：**可选** 
 
 主键（`*`）
 
 [fare_rules.txt](#fare_rulestxt) 表指定 [fare_attributes.txt](#fare_attributestxt) 中的票价如何应用于行程。大多数票价结构使用以下规则的某种组合：
 
 * 票价取决于出发站或目的地站。
 * 票价取决于行程经过哪些区域。
 * 票价取决于行程使用的路线。 
 
 有关如何使用 [fare_rules.txt](#fare_rulestxt) 和 [fare_attributes.txt](#fare_attributestxt) 指定票价结构的示例，请参阅 GoogleTransitDataFeed 开源项目 wiki 中的 [FareExamples](https://web.archive.org/web/20111207224351/https://code.google.com/p/googletransitdatafeed/wiki/FareExamples)。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `fare_id` | 引用 `fare_attributes.fare_id` 的外部 ID | **必需** | 标识票价类别。| 
 | `route_id` | 引用 `routes.route_id` 的外部 ID | 可选 |标识与票价等级关联的路线。如果存在多条具有相同票价属性的routes，则在 [fare_rules.txt](#fare_rulestxt) 中为每条路线创建一条记录。<hr> *示例：如果票价等级“b”在航线“TSW”和“TSE”上有效，则 [fare_rules.txt](#fare_rulestxt) 文件将包含该票价等级的以下记录：*<br> `fare_id,route_idID`<br> `b,TSW`<br> `b,TSE`| 
 | `origin_id` | 引用 `stops.zone_id` 的外部 ID | 可选 | 标识出发区域。如果票价等级有多个出发区域，则在 [fare_rules.txt](#fare_rulestxt) 中为每个 `origin_id` 创建一条记录。<hr> *示例：如果票价等级“b”适用于从区域“2”或区域“8”出发的所有旅行，则 [fare_rules.txt](#fare_rulestxt) 文件将包含该票价等级的以下记录：*<br> `fare_id,...,origin_idID`<br> `b,...,2<br> `b,...,8` | 
 | `destination_id` | 引用 `stops.zone_id` 的外部 ID | 可选 | 标识目的地区域。如果票价等级有多个目的地区域，则在 [fare_rules.txt](#fare_rulestxt) 中为每个 `destination_id` 创建一条记录。<hr> *示例：`origin_id` 和 `destination_id` 字段可一起使用，以指定票价等级“b”适用于区域 3 和 4 之间的旅行，以及区域 3 和 5 之间的旅行，[fare_rules.txt](#fare_rulestxt) 文件将包含该票价等级的以下记录：*<br> `fare_id,...,origin_id,destination_idID`<br> `b,...,3,4<br> `b,...,3,5` | 
 | `contains_id` | 引用 `stops.zone_id` 的外部 ID | 可选 | 标识乘客在使用给定票价等级时将进入的区域。在某些系统中用于计算正确的票价等级。<hr> *示例：如果票价等级“c”与经过区域 5、6 和 7 的 GRT 路线上的所有旅行相关，则 [fare_rules.txt](#fare_rulestxt) 将包含以下记录：*<br> `fare_id,route_id,...,contains_idID`<br> `c,GRT,...,5<br> `c,GRT,...,6<br> `c,GRT,...,7<br> *由于所有 `contains_id区域必须匹配才能应用票价，](https:经过区域 5 和 6 但不经过区域 7 的行程不会有票价等级“c”。有关更多详细信息，请参阅 GoogleTransitDataFeed 项目 wiki 中的 [https://code.google.com/p/googletransitdatafeed/wiki/FareExamples](https://code.google.com/p/googletransitdatafeed/wiki/FareExamples)。* | 
 
### timeframes.txt 
 
 文件：**可选** 
 
 主键（`*`）
 
 用于描述可能根据一天中的时间、一周中的某一天或一年中的某一天而变化的票价。时间范围可以与 [fare_leg_rules.txt](#fare_leg_rulestxt) 中的票价产品相关联。<br> 
 相同 `timeframe_group_id` 和 `service_id` 值的时间间隔不得重叠。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `timeframe_group_id` | ID | **必需** | 标识时间范围或时间范围集。| 
 | `start_time` | 时间 | **有条件必需** | 定义时间范围的开始。间隔包括开始时间。<br>禁止使用大于 `24:00:00`的值。`start_time` 中的空值将被视为 `00:00:00`。<br><br>有条件要求：<br> - 如果定义了 `timeframes.end_time，则**必需**。<br> - **禁止** 否则 | 
 | `end_time` | 时间 | **有条件要求** | 定义时间范围的结束时间。间隔不包括结束时间。<br>禁止使用大于 `24:00:00`的值。`end_time` 中的空值将被视为 `24:00:00`。<br><br>有条件要求：<br> - 如果定义了 `timeframes.start_time，则**必需**。<br> - 否则**禁止** | 
 | `service_id` | 引用 `calendar.service_id` 或 `calendar_dates.service_id` 的外部 ID | **必需** | 标识时间范围有效的一组日期。| 
 
#### 时间范围本地时间语义 
 - 在根据 [timeframes.txt](#timeframestxt) 评估票价事件的时间时，事件时间以本地时间计算，使用本地时区，由 `stop_timezone`（如果指定）确定，该时区是票价事件的停靠站或父站。如果未指定，则应使用供稿的agency时区。
 - “当前日期”是票价事件时间的当前date，相对于当地时区计算。“当前日期”可能与票价航段行程的服务日不同，尤其是对于延长到午夜之后的行程。 
 - 使用GTFS时间字段类型语义计算票价事件的“一天中的时间”相对于“当前日期”。
 
### fare_media.txt 
 
 文件：**可选** 
 
 主键（`fare_media_id`）
 
 描述可用于使用票价产品的不同票价媒体。票价媒体是用于表示和/或验证票价产品的物理或虚拟持有者。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `fare_media_id` | 唯一 ID | **必填** | 标识票价媒体。| 
 | `fare_media_name` |Text| 可选 | 票价媒体的名称。<br><br>对于交通卡 (`fare_media_type =2`) 或移动应用程序 (`fare_media_type =4`) 形式的票价媒体，应包含 `fare_media_name`，并且应与提供这些媒体的组织使用的面向乘客的名称相匹配。| 
 | `fare_media_type` | 枚举 | **必需** | 票价媒体的类型。有效选项包括：<br><br> `0` - 无。当购买或验证票价产品时无需使用票价媒介时使用，例如向司机或售票员支付现金，而不提供实体车票。<br> `1` - 实体纸质车票，允许乘客在固定时间内进行一定数量的预购行程或无限制行程。<br> `2`-已存储票证、通行证或货币价值的实体交通卡。<br> `3`——cEMV（非接触式 Europay、Mastercard 和 Visa）作为基于账户票务的开环令牌容器。<br> `4` - 存储了虚拟交通卡、车票、通行证或货币价值的移动应用程序。| 
 
### fare_products.txt 
 
 文件：**可选** 
 
 主键（`fare_product_id`，`fare_media_id`）
 
 用于描述乘客可购买的票价范围或在计算多程旅程总票价时考虑的票价范围，例如换乘费用。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `fare_product_id` | ID | **必需** | 标识票价产品或一组票价产品。<br><br> [fare_products.txt](#fare_productstxt) 中的多条记录可能共享相同的 `fare_product_id`，在这种情况下，从另一个文件引用时将检索具有该 ID 的所有记录。<br><br>多条记录可能共享相同的 `fare_product_id` 但具有不同的 `fare_media_id`，表示可使用多种方法使用票价产品，价格可能不同。| 
 | `fare_product_name` |Text| 可选 | 向乘客显示的票价产品名称。| 
 | `fare_media_id` | 引用 `fare_media.fare_media_id` 的外部 ID | 可选 | 标识可用于在行程中使用票价产品的票价媒体。当 `fare_media_id` 为空时，则认为票价媒体未知。| 
 | `amount` | 货币amount| **必填** | 票价产品的成本。可以为负数，以表示转账折扣。可以为零，以表示免费的票价产品。| 
 | `currency` | 货币代码 | **必填** | 票价产品成本的currency。| 
 
 
### fare_leg_rules.txt 
 
 文件：**可选** 
 
 主键（`network_id, from_area_id, to_area_id, from_timeframe_group_id, to_timeframe_group_id, fare_product_id`）
 
 各个行程的票价规则。
 
 必须通过过滤文件中的所有记录来查询 [`fare_leg_rules.txt`](#fare_leg_rulestxt) 中的票价，以找到与乘客要旅行的行程相匹配的规则。 
 
 要处理某段航程的费用：
 
 1.文件 [fare_leg_rules.txt](#fare_leg_rulestxt) 必须通过定义旅行特征的字段进行过滤，这些字段为：
 - `fare_leg_rules.network_id` 
 - `fare_leg_rules.from_area_id` 
 - `fare_leg_rules.to_area_id` 
 - `fare_leg_rules.from_timeframe_group_id` 
 - `fare_leg_rules.to_timeframe_group_id` 
<br/> 
 
 2.如果根据旅行特征，该航段与 [fare_leg_rules.txt](#fare_leg_rulestxt) 中的记录完全匹配，则必须处理该记录以确定航段的费用。此文件以两种方式处理空条目：空语义或规则优先级。
<br/> 
 
 3.如果未找到精确匹配且 `rule_priority` 字段不存在，则必须检查 `fare_leg_rules.network_id`、`fare_leg_rules.from_area_id` 和 `fare_leg_rules.to_area_id` 中的空条目，以处理航段费用： 
 - `fare_leg_rules.network_id` 中的空条目对应于 [routes.txt](#routestxt) 或 [networks.txt](#networkstxt) 中定义的所有网络，但不包括 `fare_leg_rules.network_id` 下列出的网络 
 
 - `fare_leg_rules.from_area_id` 中的空条目对应于 `areas.area_id` 中定义的所有区域，但不包括 `fare_leg_rules.from_area_id` 下列出的区域 
 - `fare_leg_rules.to_area_id对应于 `areas.area_id中定义的所有区域，但不包括 `fare_leg_rules.to_area_id下列出的区域
<br/> 
 
 4.如果 `rule_priority` 字段存在，则 
 - `fare_leg_rules.network_id中的空条目表示该航段的网络不影响该规则的匹配。 
 - `fare_leg_rules.from_area_id中的空条目表示该航段的departure区域不影响该规则的匹配。 
 - `fare_leg_rules.to_area_id中的空条目表示该航段的arrival区域不影响该规则的匹配。 
<br/> 
 
 5.如果航段不符合上述任何一条规定，则票价未知。
 
<br/> 
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `leg_group_id` | ID | 可选 | 标识 [fare_leg_rules.txt](#fare_leg_rulestxt) 中的一组条目。<br><br>用于描述 `fare_transfer_rules.from_leg_group_id` 和 `fare_transfer_rules.to_leg_group_id` 之间的票价转移规则。<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt) 中的多个条目可能属于同一个 `fare_leg_rules.leg_group_id`。<br><br> [fare_leg_rules.txt](#fare_leg_rulestxt) 中的相同条目（不包括 `fare_leg_rules.leg_group_id`）不得属于多个 `fare_leg_rules.leg_group_id`。| 
 | `network_id` | 引用 `routes.network_id` 或 `networks.network_id ` 的外部 ID | 可选 | 标识适用于票价航段规则的路线网络。<br><br>如果 `rule_priority` 字段不存在，且没有与正在过滤的 ` network_id匹配的 ` fare_leg_rules.network_id值，则默认匹配空的 ` fare_leg_rules.network_id。<br><br> `fare_leg_rules.network_id` 中的空条目对应于 [routes.txt](#routestxt) 或 [networks.txt](#networkstxt) 中定义的所有网络，但不包括 `fare_leg_rules.network_id` 下列出的网络<br><br>如果文件中存在 `rule_priority` 字段，则空的 `fare_leg_rules.network_id` 表示该航段的路线网络不影响该规则的匹配。| 
 | `from_area_id` | 引用 `areas.area_id` 的外部 ID | 可选 | 标识departure区域。<br><br>如果 `rule_priority` 字段不存在，且没有与正在过滤的 ` area_id匹配的 ` fare_leg_rules.from_area_id值，则默认匹配空的 ` fare_leg_rules.from_area_id。<br><br> `fare_leg_rules.from_area_id` 中的空条目对应于 `areas.area_id` 中定义的所有区域（不包括 `fare_leg_rules.from_area_id` 下列出的区域）<br><br>如果文件中存在 `rule_priority` 字段，则空的 `fare_leg_rules.from_area_id` 表示航程的departure区域不影响此规则的匹配。| 
 | `to_area_id` | 引用 `areas.area_id` 的外部 ID | 可选 | 标识arrival区域。<br><br>如果 `rule_priority` 字段不存在，且没有与正在过滤的 ` area_id匹配的 ` fare_leg_rules.to_area_id值，则默认匹配空的 ` fare_leg_rules.to_area_id。<br><br> `fare_leg_rules.to_area_id` 中的空条目对应于 `areas.area_id` 中定义的所有区域（不包括 `fare_leg_rules.to_area_id` 下列出的区域）<br><br>如果文件中存在 `rule_priority` 字段，则空的 `fare_leg_rules.to_area_id` 表示航段的arrival区域不影响此规则的匹配。| 
 | `from_timeframe_group_id` | 引用 `timeframes.timeframe_group_id` 的外部 ID | 可选 | 定义票价航段开始时票价验证事件的时间范围。<br><br>票价段的“开始时间”是事件预定发生的时间。例如，该时间可以是票价段开始时公交车的预定departure时间，乘客在此时间上车并验证票价。对于以下规则匹配语义，开始时间以当地时间计算，由 [timeframes.txt](#timeframestxt) 的 [本地时间语义](#timeframes-local-time-semantics) 确定。票价段departure事件的站点或车站应在适当的情况下用于时区解析。<br><br>对于指定“from_timeframe_group_id”的票价航段规则，t

[timeframes.txt](#timeframestxt) 中至少存在一条记录，满足以下所有条件<br>- `timeframe_group_id的值等于 `from_timeframe_group_id的值。<br> - 记录的“service_id”所标识的日期集合包含票价航段开始时间的“当前日期”。<br> - 票价航段的“时间”开始时间大于或等于记录的 `timeframes.start_time` 值，且小于 `timeframes.end_time` 值。<br><br>空的 `fare_leg_rules.from_timeframe_group_id` 表示航段的开始时间不影响此规则的匹配。| 
 | `to_timeframe_group_id` | 引用 `timeframes.timeframe_group_id` 的外部 ID | 可选 | 定义票价航段结束时票价验证事件的时间范围。<br><br>票价段的“结束时间”是事件预计发生的时间。例如，该时间可以是公交车在票价段终点的预计arrival时间，乘客下车并验证票价。对于下面的规则匹配语义，结束时间以当地时间计算，由 [timeframes.txt](#timeframestxt) 的 [本地时间语义](#timeframes-local-time-semantics) 确定。票价段arrival事件的站点或车站应在适当的情况下用于时区解析。<br><br>对于指定 `to_timeframe_group_id` 的票价航段规则，如果 [timeframes.txt](#timeframestxt) 中存在至少一条满足以下所有条件的记录，则该规则将匹配特定航段<br>- `timeframe_group_id的值等于 `to_timeframe_group_id的值。<br> - 记录的“service_id”所标识的日期集合包含票价航段结束时间的“当前日期”。<br> - 票价航段的结束时间的“时间”大于或等于记录的 `timeframes.start_time` 值，且小于 `timeframes.end_time` 值。<br><br>空的 `fare_leg_rules.to_timeframe_group_id` 表示航程的结束时间不影响此规则的匹配。| 
 | `fare_product_id` | 引用 `fare_products.fare_product_id` 的外部 ID | **必需** | 行驶该航程所需的票价产品。| 
 | `rule_priority` | 非负整数 | 可选 | 定义匹配规则应用于航程的优先级顺序，允许某些规则优先于其他规则。当 `fare_leg_rules.txt` 中的多个条目匹配时，将选择 `rule_priority` 值最高的规则或规则集。<br><br> `rule_priority` 的空值被视为零。| 
 
### fare_transfer_rules.txt 
 
 文件：**可选** 
 
 主键（`from_leg_group_id, to_leg_group_id, fare_product_id, transfer_count, duration_limit `）
 
 在 [` fare_leg_rules.txt `](#fare_leg_rulestxt) 中定义的旅行行程之间的transfers票价规则。
 
 处理多程旅程的费用：
 
 1.应根据乘客的旅程为所有单独的旅行行程确定在 `fare_leg_rules.txt` 中定义的适用票价行程组。 
 2.文件 [fare_transfer_rules.txt](#fare_transfer_rulestxt) 必须通过定义转乘特征的字段进行过滤，这些字段为：
 - `fare_transfer_rules.from_leg_group_id` 
 - `fare_transfer_rules.to_leg_group_id`<br/> 
<br/> 
 
 3.如果根据换乘特征，该换乘与 [fare_transfer_rules.txt](#fare_transfer_rulestxt) 中的记录完全匹配，则必须处理该记录以确定换乘费用。 
 4.如果没有找到精确匹配项，则必须检查 `from_leg_group_id` 或 `to_leg_group_id` 中的空条目，以处理转乘费用： 
 - `fare_transfer_rules.from_leg_group_id` 中的空条目对应于 `fare_leg_rules.leg_group_id` 下定义的所有航段组，但不包括 `fare_transfer_rules.from_leg_group_id` 下列出的航段组 
 - `fare_transfer_rules.to_leg_group_id` 中的空条目对应于 `fare_leg_rules.leg_group_id` 下定义的所有航段组，但不包括 `fare_transfer_rules.to_leg_group_id` 下列出的航段组<br/>
<br/> 
 5.如果转机不符合上述任何规则，则不存在转机安排，且各航段将被视为独立航段。
 
<br/> 
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `from_leg_group_id` | 引用 `fare_leg_rules.leg_group_id ` 的外部 ID | 可选 | 标识一组转乘前票价航段规则。<br><br>若没有与所过滤的 ` leg_group_id ` 匹配的 ` fare_transfer_rules.from_leg_group_id ` 值，则默认匹配空的 ` fare_transfer_rules.from_leg_group_id`。<br><br> `fare_transfer_rules.from_leg_group_id` 中的空条目对应于 `fare_leg_rules.leg_group_id` 下定义的所有航段组，但 `fare_transfer_rules.from_leg_group_id` 下列出的航段组除外 | 
 | `to_leg_group_id` | 引用 `fare_leg_rules.leg_group_id ` 的外部 ID | 可选 | 标识一组转乘后票价航段规则。<br><br>若没有与所过滤的 ` leg_group_id ` 匹配的 ` fare_transfer_rules.to_leg_group_id ` 值，则默认匹配空的 ` fare_transfer_rules.to_leg_group_id`。<br><br> `fare_transfer_rules.to_leg_group_id` 中的空条目对应于 `fare_leg_rules.leg_group_id` 下定义的所有航段组，但 `fare_transfer_rules.to_leg_group_id` 下列出的航段组除外 | 
 | `transfer_count` | 非零整数 | **有条件禁止** | 定义可将转乘规则应用于多少次连续transfers。<br><br>有效选项为：<br> `-1` — 无限制。<br> `1`或更多 - 定义转移规则可以跨越多少个transfers。<br><br>如果一个子旅程匹配多个具有不同 `transfer_count的记录，则将选择具有最小 `transfer_count且大于或等于该子旅程当前转移计数的规则。<br><br>有条件禁止：<br> - 如果“fare_transfer_rules.from_leg_group_id”不等于“fare_transfer_rules.to_leg_group_id”，则**禁止**。<br> - 如果 `fare_transfer_rules.from_leg_group_id` 等于 `fare_transfer_rules.to_leg_group_id`，则 **必需**。| 
 | `duration_limit` | 正整数 | 可选 | 定义转乘的持续时间限制。<br><br>必须以秒的整数增量来表示。<br><br>如果没有时长限制，`fare_transfer_rules.duration_limit` 必须为空。| 
 | `duration_limit_type` | 枚举 | **有条件要求** | 定义 `fare_transfer_rules.duration_limit` 的相对开始和结束。<br><br>有效选项为：<br> `0` - 当前航程的departure票价验证与下一航程的arrival票价验证之间。<br> `1` - 当前航段的departure票价验证与下一航段的departure票价验证之间。<br> `2` - 当前航段的arrival票价验证与下一航段的departure票价验证之间。<br> `3` - 当前航段的arrival票价验证与下一航段的arrival票价验证之间。<br><br>有条件要求：<br> - 如果定义了“fare_transfer_rules.duration_limit”，则**必需**。<br> - 如果 `fare_transfer_rules.duration_limit` 为空，则**禁止**。| 
 | `fare_transfer_type` | 枚举 | **必需** | 表示旅程中各段之间转乘的费用处理方式：<br> ![](../../assets/2-leg.svg)<br>有效选项为：<br> `0` - 出发航段 `fare_leg_rules.fare_product_id` 加上 `fare_transfer_rules.fare_product_id`；A + AB。<br> `1` - 出发航段 `fare_leg_rules.fare_product_id` 加上 `fare_transfer_rules.fare_product_id` 加上目的地航段 `fare_leg_rules.fare_product_id`；A + AB + B。<br> `2` - `fare_transfer_rules.fare_product_id`；AB.<br><br>一次旅程中多次transfers之间的费用处理交互：<br> ![](../../assets/3-leg.svg)<br><table><thead><tr><th> `fare_transfer_type`</th><th>处理 A > B</th><th>处理B>C</th></tr></thead><tbody><tr><td> `0`</td><td> A + AB</td><td>星+BC</td></tr><tr><td> `1`</td><td> A+AB+B</td><td>时间 + 公元前 + 年份</td></tr><tr><td>`2`</td><td> AB</td><td>星+BC</td></tr></tbody></table>其中 S 表示前一航段和换乘的总处理费用。| 
 | `fare_product_id` | 引用 `fare_products.fare_product_id` 的外部 ID | 可选 | 两个票价航段之间换乘所需的票价产品。如果为空，换乘规则的费用为 0。| 
 
 
### areas.txt 
 
 文件：**可选** 
 
 主键（`area_id`）
 
 定义区域标识符。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `area_id` | 唯一 ID | **必填** | 标识一个区域。在 [areas.txt](#areastxt) 中必须是唯一的。| 
 | `area_name` |Text| **可选** | 向乘客显示的区域名称。| 
 
### stop_areas.txt 
 
 文件：**可选** 
 
 主键（`*`）
 
 将 [stops.txt]（#stopstxt）中的stops分配给区域。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | ` area_id` | 引用 `areas.area_id` 的外部 ID | **必填** | 标识一个或多个`stop_id`所属的区域。相同的`stop_id`可以在许多 `area_id` 中定义。| 
 | `stop_id` | 引用 `stops.stop_id` 的外部 ID | **必填** | 标识一个站点。如果在此字段中定义了一个车站（即，具有`stops.location_type=1` 的站点），则假定其所有stops（即，所有具有`stops.location_type=0`且将此车站定义为 `stops.parent_station的站点）都属于同一区域。 可以通过将站台分配给其他区域来覆盖此行为。 | 
 
### networks.txt 
 
 文件：**有条件禁止** 
 
 主键（`network_id`）
 
 定义适用于票价段规则的网络标识符。 
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `network_id` | 唯一 ID | **必填** | 标识网络。在 [networks.txt](#networkstxt) 中必须是唯一的。 | 
 | `network_name` |Text| **可选** |适用于票价航段规则的网络名称，由当地agency及其乘客使用。
 
### route_networks.txt 
 
 文件：**有条件禁止** 
 
 主键（`route_id` ）
 
 将 [routes.txt](#routestxt) 中的routes分配给网络。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 |` network_id` | 引用`networks.network_id的外部 ID | **必填** | 标识一个或多个`route_id`所属的网络。一个`route_id`只能在一个`network_id中定义。|
 | `route_id` | 引用`routes.route_id的外部 ID | **必填** | 标识一条路线。| 
 
### shapes.txt 
 
 文件：**可选** 
 
 主键（`shape_id`，`shape_pt_sequence）
 
 形状描述vehicle沿路线行驶的路径，并在文件shapes.txt中定义。形状与行程相关联，由vehicle按顺序经过的一系列点组成。形状不需要精确拦截站点的位置，但行程中的所有站点都应位于该行程shape的较小距离内，即靠近连接shape点的直线段。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `shape_id` | ID | **必填** | 标识shape。| 
 | `shape_pt_lat| 纬度 | **必填** |shape点的纬度。 [shapes.txt](#shapestxt) 中的每条记录代表一个用于定义shape的shape点。| 
 | ` shape_pt_lon` | 经度 | **必需** |shape点的经度。| 
 | `shape_pt_sequence` | 非负整数 | **必需** |shape点连接形成shape的序列。值必须沿着行程增加，但不必连续。<hr> *示例：如果shape“A_shp”在其定义中有三个点，则 [shapes.txt](#shapestxt) 文件可能包含这些记录来定义shape：*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence`<br> `A_shp,37.61956,-122.48161,0<br> `A_shp,37.64430,-122.41070,6<br> `A_shp,37.65863,-122.30839,11` | 
 | `shape_dist_traveled` | 非负float| 可选 | 从第一个shape点到此记录中指定的点沿shape行进的实际距离。行程规划人员使用它来在地图上显示shape的正确部分。值必须随 `shape_pt_sequence增加；不得用于显示沿路线的反向行进。距离单位必须与 [stop_times.txt](#stop_timestxt) 中使用的单位一致。<br><br>建议用于有环路或内联的routes（vehicle在一次行程中穿过或行驶过相同部分的路线）。 <br><img src="../../../assets/inlining.svg" width=200px style="display: block; margin-left: auto; margin-right: auto;"><br>如果vehicle在行程中的某些点折返或越过路线，则`shape_dist_traveled`非常重要，它可明确 [shapes.txt](#shapestxt) 中各点的部分如何与 [stop_times.txt](#stop_timestxt) 中的记录相对应。<hr> *示例：如果一辆公交车沿着上面为 A_shp 定义的三个点行驶，则额外的“`shape_dist_traveled`”值（此处以公里为单位显示）将如下所示：*<br> `shape_id,shape_pt_lat,shape_pt_lon,shape_pt_sequence,shape_dist_traveled`<br> `A_shp,37.61956,-122.48161,0,0<br> `A_shp,37.64430,-122.41070,6,6.8310<br> `A_shp,37.65863,-122.30839,11,15.8765` | 
 
### frequencies.txt 
 
 文件：**可选** 
 
 主键（`trip_id`， `start_time`）
 
 [Frequencies.txt]（#frequenciestxt）表示以固定间隔时间（行程间隔时间）运行的行程。此文件可用于表示两种不同类型的服务。
 
 * 基于频率的服务（`exact_times`=`0`），其中服务不遵循全天固定的时间表。相反，运营商试图严格保持预定的行程间隔时间。
 * 基于时间表的服务的压缩表示（`exact_times`= `1`），在指定时间段内的行程具有完全相同的间隔时间。在基于时间表的服务中，运营商会尝试严格遵守时间表。 
 
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `trip_id` | 引用`trips.trip_id`的外部 ID | **必需** | 标识适用指定服务间隔的行程。| 
 | `start_time` | 时间 | **必需** | 第一vehicle以指定间隔从行程的第一个站点出发的时间。| 
 | `end_time` | 时间 | **必需** | 服务在行程的第一个站点更改为不同间隔（或停止）的时间。| 
 | `headway_secs` | 正整数 | **必需** | 在`start_time`和 `end_time` 指定的时间间隔内，行程从同一站点（间隔）出发之间的时间，以秒为单位。可以为同一次行程定义多个间隔，但不得重叠。新的间隔时间可能在前一个间隔时间结束的准确时间开始。| 
 | `exact_times` | 枚举 | 可选 | 表示行程的服务类型。有关更多信息，请参阅文件说明。有效选项包括：<br><br> `0` 或空 – 基于频率的行程。<br> `1` - 基于时间表的行程，全天间隔时间完全相同。在这种情况下，`end_time` 值必须大于最后一次期望行程`start_time` ，但小于最后一次期望行程start_time + `headway_secs`。| 
 
### transfers.txt 
 
 文件：**可选** 
 
 主键（`from_stop_id`、`to_stop_id`、`from_trip_id`、`to_trip_id`、`from_route_id`、`to_route_id`）
 
 计算行程时，使用GTFS的应用程序会根据允许的时间和停靠点距离插入transfers。[Transfers.txt](#transferstxt) 为选定transfers指定附加规则和覆盖。 
 
 字段 `from_trip_id`、`to_trip_id`、`from_route_id` 和 `to_route_id` 允许换乘规则按更高顺序排列特异性。 连同 `from_stop_id` 和 `to_stop_id`，特异性的排序如下：
 
 1.定义了两个`trip_id`：`from_trip_id` 和 `to_trip_id`。
 2.定义了一个`trip_id`和`route_id`集合：(`from_trip_id` 和 `to_route_id`) 或 (`from_route_id ` 和 ` to_trip_id `)。
 3.定义了一个`trip_id` ：`from_trip_id ` 或 ` to_trip_id `。
 4.定义了两个`route_id`：`from_route_id` 和 `to_route_id`。 
 5.定义了一个`route_id` ：`from_route_id` 或 `to_route_id`。
 6.仅定义了 `from_stop_id` 和 `to_stop_id`：未设置路线或行程相关字段。
 
 对于给定的有序到达行程和出发行程对，选择在这两个行程之间适用的最大特异性的换乘。对于任何一对行程，不应该有两个具有相同最大特异性的transfers。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `from_stop_id` | 引用 `stops.stop_id的外部 ID | **有条件要求** | 标识routes连接开始的站点或车站。如果此字段引用车站，则换乘规则适用于其所有子stops。对于 `transfer_types` 4 和5.禁止引用车站。| 
 | `to_stop_id` | 引用 `stops.stop_id` 的外部 ID | **有条件要求** | 标识routes之间连接结束的站点或车站。如果此字段引用车站，则换乘规则适用于所有子stops。对于 `transfer_types` 4 和5.禁止引用车站。| 
 | `from_route_id` | 引用 `routes.route_id` 的外部 ID | 可选 | 标识连接开始的路线。<br><br>如果定义了“from_route_id”，则转乘将适用于给定“from_stop_id”路线上的到达行程。<br><br>如果同时定义了 `from_trip_id` 和 `from_route_id` ，则`trip_id`必须属于`route_id`，并且 `from_trip_id` 将优先。| 
 | `to_route_id` | 引用 `routes.route_id` 的外部 ID | 可选 | 标识连接结束的路线。<br><br>如果定义了“to_route_id”，则转乘将适用于给定“to_stop_id”路线上的出发行程。<br><br>如果同时定义了 `to_trip_id` 和 `to_route_id` ，则`trip_id`必须属于`route_id`，并且 `to_trip_id` 将优先。| 
 | `from_trip_id` | 引用`trips.trip_id`的外部 ID | **有条件要求** | 标识routes之间连接开始的行程。<br><br>如果定义了“from_trip_id”，则转乘将适用于给定“from_stop_id”的到达行程。<br><br>如果同时定义了 `from_trip_id` 和 `from_route_id` ，则`trip_id`必须属于`route_id`，并且 `from_trip_id` 将优先。如果 `transfer_type` 为 ` 4 ` 或 ` 5 `，则必需。| 
 | `to_trip_id` | 引用`trips.trip_id` 的外部 ID | **有条件要求** | 标识routes之间连接结束的行程。<br><br>如果定义了“to_trip_id”，则转乘将适用于给定“to_stop_id”的出发行程。<br><br>如果同时定义了 `to_trip_id` 和 `to_route_id` ，则`trip_id`必须属于`route_id`，并且 `to_trip_id` 将优先。如果 `transfer_type` 为 ` 4` 或 ` 5` ，则为必需。| 
 | `transfer_type` | 枚举 | **必需** | 指示指定（`from_stop_id`，`to_stop_id`）对的连接类型。有效选项为：<br><br> `0` 或空 – 推荐routes间的换乘点。<br> `1` - 两条routes之间的定时换乘点。出发vehicle应等待到达车辆，并留出足够的时间让乘客在routes之间换乘。<br> `2` - 转机要求在arrival和departure之间留出最少的时间来确保连接。转机所需的时间由 ` min_transfer_time指定。<br> `3` - 该地点的routes之间无法转乘。<br> `4` - 乘客可以留在同一辆vehicle上，从一个行程换乘到另一个行程（“座位内换乘”）。有关此类换乘的更多详细信息，请参见[下文](#linked-trips)。<br> `5` - 连续的行程之间不允许在座位上transfers。乘客必须vehicle并重新登机。有关此类转乘的更多详细信息，请参见[下面](#linked-trips)。| 
 | `min_transfer_time ` | 非负整数 | 可选 | 在指定stops的routes之间转乘所必须具有的时间量（以秒为单位）。` min_transfer_time` 应足以让普通乘客在两个stops之间移动，包括缓冲时间以允许每条路线的时间安排差异。| 
 
#### 链接行程 
 
 以下内容适用于 `transfer_type=4` 和 `=5`，用于将行程链接在一起，无论是否有座位上transfers。
 
 链接在一起的行程必须由同一vehicle运营。vehicle可以与其他车辆连接或分离。 
 
 如果同时提供了链接行程转接和block_id ，并且它们产生冲突的结果，则应使用链接行程转接。
 
 `from_trip_id` 的最后一站应在地理位置上接近 `to_trip_id ` 的第一站，并且 ` from_trip_id ` 的最后arrival时间应早于但接近 ` to_trip_id ` 的第一departure时间。如果 ` to_trip_id ` 行程发生在下一个服务日，则 ` from_trip_id ` 的最后arrival时间可能晚于 ` to_trip_id ` 的第一departure时间。
 
 在常规情况下，行程可以 1 对 1 链接，但也可以 1 对 n、n 对 1 或 n 对 n 链接，以表示更复杂的行程延续。例如，两次火车行程（下图中的行程 A 和行程 B）可以在一个公共车站进行vehicle耦合操作后合并为一次火车行程（行程 C）：
 
 - 在 1 对 n 的延续中，每个 ` to_trip_id ` 的 ` trips.service_id ` 必须相同。
 - 在 n 对 1 的延续中，每个 ` from_trip_id ` 的 ` trips.service_id ` 必须相同。
 - n 对 n 的延续必须遵守这两个约束。
 - 行程可以作为多个不同延续的一部分链接在一起，前提是 ` trip.service_id` 在任何服务日期都不得重叠。
 
<pre> 
 行程 A 
 ────────────────────\ 
 \ 行程 C 
 ────────────── 
 行程 B/
 ──────────────────/
</pre> 
 
### pathways.txt 
 
 文件：**可选** 
 
 主键（`pathway_id`） 
 
 文件 [pathways.txt](#pathwaystxt) 和 [levels.txt](#levelstxt) 使用图形表示来描述地铁站或火车站，节点表示位置，边表示pathways。 
 
 为了从车站入口/出口（用`location_type=2`表示的位置节点）导航到站台（用`location_type=0`或空表示的位置节点），乘客将穿过人行道、检票口、楼梯和其他用pathways表示的边。 通用节点（用`location_type=3`表示的节点）可用于连接整个车站的pathways。 
 
 必须在车站内详尽定义路径。 如果定义了任何pathways，则假定整个车站的所有pathways都已表示。因此，适用以下准则：
 
 - 无悬垂位置：如果车站内的任何位置都有通道，则该车站内的所有位置都应有pathways，设有登车区的站台除外（`location_type=4`，请参阅以下准则）。
 - 设有登车区的站台无pathways：设有登车区（`location_type= `location_type=4`= `location_type=0`或空）将被视为父对象，而不是点。在这种情况下，站台不得分配pathways。应为站台的每个登车区分配所有pathways。
 - 无锁定站台：每个站台（`location_type=0`或空）或登车区（`location_type=4` ）必须通过某些pathways链连接到至少一个入口/出口（ `location_type=2` ）。不允许从特定站台到车站外部有通道的车站很少见。
 
 | 字段名称 | 类型 |存在 | 描述 | 
 |------|------|------|------| 
 | ` pathway_id` | 唯一 ID | **必需** | 标识路径。系统将其用作记录的内部标识符。在数据集中必须是唯一的。<br><br>不同pathways的“from_stop_id”和“to_stop_id”可能具有相同的值。<hr> _示例：当两部自动扶梯并排以相反的方向行驶时，或者当一组楼梯和电梯从同一个地方到达同一个地方时，不同的 `pathway_id可能具有相同的 `from_stop_id和 `to_stop_id值。_|
|`from_stop_id| 引用`stops.stop_id的外部 ID |**必需**| 通道开始的位置。<br><br>必须包含标识平台的“`stop_id`” （“lo”）

cation_type=0` 或空）、入口/出口（`location_type=2`）、通用节点（`location_type=3`）或登机区（`location_type=4` ）。<br><br>禁止使用标识车站（ `location_type=1` ）的`stop_id`值。|
|` to_stop_id|引用`stops.stop_id的外部ID|**必需**|路径结束的位置。<br><br>必须包含一个“`stop_id`” ，用于标识平台（“`location_type=0`”或空）、入口/出口（“`location_type=2`”）、通用节点（“`location_type=3`”）或登机区域（“`location_type=4`” ）。<br><br>禁止使用标识站点（ `location_type=1` ）的`stop_id`值。|
|` pathway_mode|枚举|**必需**|指定（`from_stop_id，`to_stop_id）对之间的路径类型。有效选项包括：<br><br> `1`走道。<br> `2` - 楼梯。<br> `3`——移动人行道/自动人行道。<br> `4`-自动扶梯。<br> `5`——电梯。<br> `6` - 检票口（或付款口）：一条通往车站区域的通道，需要出示付款证明才能通过。检票口可能会将车站的付费区域与非付费区域分开，或将同一车站内的不同付款区域分开。此信息可用于避免使用require乘客进行不必要付款的捷径引导乘客通过车站，例如引导乘客穿过地铁站台到达公交专用道。<br> `7`- 出口门：从付费区域进入非付费区域的通道，无需付款证明即可通过。| 
 | `is_bidirectional` | 枚举 | **必需** | 指示可以采取该通道的方向：<br><br> `0` - 仅可从 `from_stop_id` 到 `to_stop_id` 使用的单向路径。<br> `1`双向通道，可在两个方向使用。<br><br>出口门（`pathway_mode=7）不能是双向的。| 
 | `length` | 非负float| 可选 | 从原点位置（在 `from_stop_id中定义）到目的地位置（在 `to_stop_id中定义）的通道水平长度（以米为单位）。<br><br>建议将此字段用于人行道（`pathway_mode=1）、检票口（`pathway_mode=6）和出口口（`pathway_mode=7）。| 
 | `traversal_time| 正整数 | 可选 | 从原点位置（在`from_stop_id中定义）走到目的地位置（在`to_stop_id中定义）穿过通道所需的平均时间（以秒为单位）。<br><br>建议将此字段用于移动人行道（`pathway_mode=3）、自动扶梯（`pathway_mode=4）和电梯（`pathway_mode=5）。| 
 | `stair_count| 非空整数 | 可选 | 通道的楼梯数量。<br><br>正数 `stair_count` 表示骑行者从 `from_stop_id` 向上走到 `to_stop_id`。负数 `stair_count` 表示骑行者从 `from_stop_id` 向下走到 `to_stop_id`。<br><br>建议将此字段用于楼梯（`pathway_mode=2）。<br><br>如果只能提供估计的楼梯数量，建议每层楼大约有 15 个楼梯。| 
 | `max_slope` |Float| 可选 | 通道的最大坡度比。有效选项包括：<br><br> `0` 或空 - 无斜率。<br> `Float` - 路径的坡度比，向上为正，向下为负。<br><br>该字段仅应与人行道（`pathway_mode=1）和移动人行道（`pathway_mode=3）一起使用。<hr> _示例：在美国，0.083（也写作 8.3%）是手推轮椅的最大坡度比，即每 1 米增加 0.083 米（即 8.3 厘米）。_| 
 | `min_width` | 正float| 可选 | 通道的最小宽度（以米为单位）。<br><br>如果最小宽度小于 1 米，建议使用此字段。| 
 | `signposted_as` |Text| 可选 | 乘客可见的物理标牌上的面向公众的文本。<br><br>可用于向乘客提供文字指引，例如“按照标志前往”。`singposted_as ` 中的文字应与标志上印刷的文字完全一致。<br><br>当物理标牌是多语言的时，可以按照 ` feed_info.feed_lang ` 字段定义中的 ` stops.stop_name ` 的示例填充和翻译此字段。| 
 | ` reversed_signposted_as` |Text| 可选 | 与 `signposted_as` 相同，但当路径从 `to_stop_id` 到 `from_stop_id` 使用时。| 
 
### levels.txt 
 
 文件：**有条件要求** 
 
 主键（`level_id`）
 
 描述车站内的楼层。与 [pathways.txt](#pathwaystxt) 结合使用。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `level_id` | 唯一 ID | **必需** | 标识车站内的楼层。| 
 | `level_index` |Float| **必需** | 指示其相对position的级别的数字索引。<br><br>地面高度应具有索引“0”，地上高度用正索引表示，地下高度用负索引表示。| 
 | `level_name` |Text| 可选 | 乘客在建筑物或车站内看到的楼层名称。<hr> _示例：乘坐电梯到“夹层”或“站台”或“-1”。_| 
 
### location_groups.txt 
 
 文件：**可选** 
 
 主键（`location_group_id`）
 
 定义位置组，即乘客可以请求接送的stops组。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |----------|----|------------|-----------| 
 | `location_group_id` | 唯一 ID | **必填** | 标识位置组。ID 在所有 `stops.stop_id、 locations.geojson `id`和 `location_groups.location_group_id` 值中必须是唯一的。<br><br>位置组是一组stops，它们共同指示乘客可能请求接送的位置。| 
 | `location_group_name` |Text| 可选 | 向乘客显示的位置组名称。| 
 
### location_group_stops.txt 
 
 文件：**可选** 
 
 主键（`*`）
 
 将stops.txt中的stops分配给位置组。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |----------|----|------------|-----------| 
 | `location_group_id` | 引用 `location_groups.location_group_id` 的外部 ID | **必填** | 标识一个或多个`stop_id`所属的位置组。相同的`stop_id`可以在许多 `location_group_id` 中定义。| 
 | `stop_id` |引用 `stops.stop_id的外部 ID | **必需** | 标识属于位置组的站点。| 
 
 
### locations.geojson 
 
 文件：**可选** 
 
 定义乘客可以请求按需服务接送的区域。这些区域以 GeoJSON 多边形表示。
 
 - 此文件使用 GeoJSON 格式的子集，如[RFC 7946](https:) 中所述。
 - `locations.geojson`文件必须包含 `FeatureCollection`。
 - `FeatureCollection` 定义了乘客可以请求接送的各种站点位置。
 - 每个 GeoJSON `Feature` 都必须有一个`id`。 `id`在所有 `stops.stop_id、 locations.geojson `id`和 `location_group_id` 值中必须是唯一的。
 - 每个 GeoJSON `Feature` 都应根据下表具有对象和关联键：
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 |- `type` | 字符串 | **必需** | 位置的 `"FeatureCollection"`。|
 |- `features` | 数组 | **必需** | 描述位置的 `"Feature"` 对象集合。|
 | \- `type` | 字符串 | **必需** | `"Feature"` |
 | \- `id` | 字符串 | **必需** | 标识位置。 ID 在所有 `stops.stop_id、 locations.geojson `id`和 `location_groups.location_group_id` 值中必须是唯一的。|
|\-`properties`|对象|**必需**|位置属性键。|
|\ stop_name|字符串|可选|表示向乘客显示的位置名称。|
|\ stop_desc|字符串|可选|位置的有意义的描述，以帮助乘客定位。|
|\-`geometry`|对象|**必需**|位置的几何形状。|
|\-`type`|字符串|**必需**|必须是以下类型：<br> - ``Polygon’’<br> - `"MultiPolygon"` | 
 | \- `coordinates` | 数组 | **必需** | 定义位置几何形状的地理坐标（latitude和longitude）。 | 
 
### booking_rules.txt 
 
 文件：**可选** 
 
 主键（`booking_rule_id`）
 
 定义乘客请求服务的预订规则 
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `booking_rule_id` | 唯一 ID | **必需** | 标识规则。| 
 | `booking_type` | 枚举 | **必需** | 表示可以提前多久进行预订。有效选项为：<br><br> `0` – 实时预订。<br> `1` - 最多可提前通知当天预订。<br> `2` - 最多可提前几天预订。| 
 | `prior_notice_duration_min` | 整数 | **有条件要求** | 旅行前提出请求的最少分钟数。<br><br> **有条件要求**：<br> - `booking_type=1` 为 **必需**。<br> - 否则**禁止**。| 
 | `prior_notice_duration_max` | 整数 | **有条件禁止** | 旅行前提出预订请求的最大分钟数。<br><br> **有条件禁止**：<br> - **禁止** `booking_type=0` 和 `booking_type=2`。<br> - 对于 `booking_type=1`，可选。| 
 | `prior_notice_last_day` | 整数 | **有条件要求** | 旅行前最后一天提出预订请求。<br><br>例如：“必须提前 1 天下午 5 点之前预订行程”将被编码为“prior_notice_last_day=1”。<br><br> **有条件要求**：<br> - `booking_type=2` 为 **必需**。<br> - 否则**禁止**。| 
 | `prior_notice_last_time` | 时间 | **有条件要求** | 旅行前最后一天最后一次提出预订请求。<br><br>例如：“必须提前 1 天下午 5 点之前预订行程”将被编码为“prior_notice_last_time=17:00:00”。<br><br> **有条件要求**：<br> - 如果定义了“prior_notice_last_day”，则**必需**。<br> - 否则**禁止**。| 
 | `prior_notice_start_day` | 整数 | **有条件禁止** | 旅行前最早一天提出预订请求。<br><br>例如：“最早可提前一周在午夜预订行程”将被编码为“prior_notice_start_day=7”。<br><br> **有条件禁止**：<br> - **禁止** `booking_type=0`。<br> - 如果定义了“prior_notice_duration_max”，则**禁止**使用“booking_type=1”。<br> - 其他情况可选。| 
 | `prior_notice_start_time` | 时间 | **有条件要求** | 旅行前最早一天的最早时间提出预订请求。<br><br>例如：“最早可提前一周在午夜预订行程”将被编码为“prior_notice_start_time=00:00:00”。<br><br> **有条件要求**：<br> - 如果定义了“prior_notice_start_day”，则**必需**。<br> - 否则**禁止**。| 
 | `prior_notice_service_id` | 引用 `calendar.service_id的 ID | **有条件禁止** | 表示计算 `prior_notice_last_day` 或 `prior_notice_start_day` 的服务日。<br><br>示例：如果为空，`prior_notice_start_day=2` 将提前两个日历日。如果定义为仅包含工作日（无节假日的工作日）的 `service_id，`prior_notice_start_day=2` 将提前两个工作日。<br><br> **有条件禁止**：<br> - 如果“booking_type=2”，则为可选。<br> - 否则**禁止**。| 
 | `message` |Text| 可选 | 在预订按需接送服务时，向在 `stop_time` 使用服务的乘客发送消息。旨在提供在用户界面内传输的关于乘客必须采取的操作才能使用该服务的最少信息。| 
 | `pickup_message` |Text| 可选 | 功能与 `message` 相同，但仅在乘客按需接送时使用。| 
 | `drop_off_message` |Text| 可选 | 功能与 `message` 相同，但仅在乘客按需接送时使用。| 
 | `phone_number` |Phone number| 可选 | 拨打预订请求的Phone number。| 
 | `info_url` | URL | 可选 | 提供有关预订规则信息的URL 。| 
 | `booking_url` | URL | 可选 | 可以进行预订请求的在线界面或应用程序的URL 。| 
 
### translations.txt 
 
 文件：**可选** 
 
 主键（`table_name`、`field_name`、` language `、`record_id`、`record_sub_id`、`field_value`） 
 
 在有多种官方语言的地区，交通运输机构/运营商通常具有特定于语言的名称和网页。为了更好地服务这些地区的乘客，数据集包含这些与语言相关的值很有用。 
 
 如果使用两种引用方法（`record_id`、`record_sub_id`）和`field_value`来翻译两行不同行中的相同值，则（`record_id`、`record_sub_id`）提供的翻译优先。 
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `table_name` | 枚举 | **必需** |定义包含要翻译的字段的表。允许的值为：<br><br> -`agency`<br> -`stops`<br> -`routes`<br> - `旅行`<br> - `stop_times`<br> - `pathways`<br> - `级别`<br> -`feed_info`<br> - `attributions`<br><br>任何添加到GTFS的文件都会有一个与文件名等同的 `table_name` 值，如上所列（即不包括 `.txt` 文件扩展名）。| 
 | `field_name` | Text | **必填** | 要翻译的字段名称。类型为 `Text` 的字段可以翻译，类型为 `URL`、`Email` 和 `Phone number` 的字段也可以“翻译”以提供正确语言的资源。其他类型的字段不应翻译。| 
 | `language` | 语言代码 | **必填** | 翻译语言。<br><br>如果语言与 `feed_info.feed_lang` 中的语言相同，则该字段的原始值将被视为在没有特定翻译的语言中使用的默认值（如果 `default_lang`t另行指定）。<hr> _示例：在瑞士，一个官方双语州的城市的官方名称是“Biel/Bienne”，但在法语中会简单地称为“Bienne”，在德语中则称为“Biel”。_ | 
 | `translation` |Text或URL或Email或Phone number| **必填** | 翻译的值。| 
 | `record_id` | 外国 ID | **有条件必填** | 定义与要翻译的字段相对应的记录。`record_id ` 中的值必须是表主键的第一个或唯一字段，如每个表的主键属性中所定义的那样，如下所示：<br><br> - [agency.txt](#agencytxt) 的 ` agency_id `<br> - [stops.txt](#stopstxt) 的`stop_id` ；<br> - [routes.txt](#routestxt) 的`route_id` ；<br> - [trips.txt](#tripstxt) 的`trip_id` ；<br> - `trip_id`用于 [stop_times.txt](#stop_timestxt)；<br> - [pathways.txt](#pathwaystxt) 的 ` pathway_id `；<br> - [levels.txt](#levelstxt) 的 ` level_id `；<br> - [attributions.txt](#attributionstxt) 的 ` attribution_id `。<br><br>上面未定义的表中的字段不应翻译。但是，生产者有时会添加超出官方规范的额外字段，这些非官方字段可能会被翻译。以下是这些表使用 ` record_id ` 的推荐方法：<br><br> - [calendar.txt](#calendartxt) 的 ` service_id `；<br> - [calendar_dates.txt](#calendar_datestxt) 的 ` service_id `；<br> - [fare_attributes.txt](#fare_attributestxt) 的 ` fare_id `；<br> - [fare_rules.txt](#fare_rulestxt) 的 ` fare_id `；<br> - [shapes.txt](#shapestxt) 的`shape_id` ；<br> - [frequencies.txt](#frequenciestxt) 的`trip_id` ；<br> - [transfers.txt](#transferstxt) 中的 ` from_stop_id `。<br><br>有条件要求：<br> - 如果 ` table_name是 `feed_info，则**禁止**。<br> - 如果定义了“field_value”，则**禁止**。<br> - 如果 `field_value为空，则**必填**。|
|`record_sub_id| 外部 ID |**有条件必填**|当表t唯一 ID 时，帮助翻译包含该字段的记录。因此，`record_sub_id中的值是表的辅助 ID，如下表所定义：<br><br> - [agency.txt](#agencytxt) 无；<br> - [stops.txt](#stopstxt) 无；<br> - [routes.txt](#routestxt) 无；<br> - [trips.txt](#tripstxt) 无；<br> - `stop_sequence`用于 [stop_times.txt](#stop_timestxt)；<br> - [pathways.txt](#pathwaystxt) 无；<br> - [levels.txt](#levelstxt) 无；<br> - [attributions.txt](#attributionstxt) 无。<br><br>上面未定义的表中的字段不应翻译。但是，生产者有时会添加超出官方规范的额外字段，这些非官方字段可能会被翻译。以下是这些表使用“record_sub_id”的推荐方法：<br><br> - [calendar.txt](#calendartxt) 无；<br> - [calendar_dates.txt](#calendar_datestxt) 的 ` date `；<br> - [fare_attributes.txt](#fare_attributestxt) 无；<br> - [fare_rules.txt](#fare_rulestxt) 的`route_id` ；<br> - [shapes.txt](#shapestxt) 无；<br> - [frequencies.txt](#frequenciestxt) 的`start_time` ；<br> - [transfers.txt](#transferstxt) 的 ` to_stop_id `。<br><br>有条件要求：<br> - 如果 ` table_name是 `feed_info，则**禁止**。<br> - 如果定义了“field_value”，则**禁止**。<br> - 如果定义了 `table_name=stop_times` 和 `record_id`，则 **必填**。| 
 | `field_value` |Text或URL或Email或Phone number| **有条件必填** | 除了使用 `record_id` 和 `record_sub_id` 来定义应该翻译哪条记录之外，此字段还可用于定义应翻译的值。使用时，当 `table_name` 和 `field_name` 标识的字段包含与field_value中定义的完全相同的值时，将应用翻译。<br><br>该字段必须具有 `field_value` 中定义的**完全**值。如果只有值的子集与 `field_value` 匹配，则t应用转换。<br><br>如果两个翻译规则与同一条记录匹配（一个与 `field_value，另一个与 `record_id匹配），则与 `record_id匹配的规则优先。<br><br>有条件要求：<br> - 如果 `table_name是 `feed_info，则**禁止**。<br> - 如果定义了“record_id”，则**禁止**。<br> - 如果 `record_id` 为空，则**必填**。| 
 
### feed_info.txt 
 
 文件：**推荐**（如果提供了 [translations.txt](#translationstxt)，则**必填**）
 
Primary key (none) 
 
 该文件包含有关数据集本身的信息，而不是数据集描述的服务。在某些情况下，数据集的发布者与任何机构都是不同的entity。
 
 | 字段名称 | 类型 | 存在 | 描述 | 
 |------|------|------|------| 
 | `feed_publisher_name` |Text| **必填** | 发布数据集的组织的全名。这可能与 `agency.agency_name` 值之一相同。| 
 | `feed_publisher_url` | URL | **必填** | 数据集发布组织网站的URL 。这可能与 `agency.agency_url` 值之一相同。| 
 | `feed_lang` | 语言代码 | **必需** | 此数据集中文本使用的默认语言。此设置可帮助GTFS消费者为数据集选择大写规则和其他特定于语言的设置。如果需要将文本翻译成默认语言以外的其他语言，则可以使用文件 `translations.txt。<br><br>对于原始文本为多种语言的数据集，默认语言可能是多语言的。在这种情况下，`feed_lang` 字段应包含由标准 ISO 639-2 定义的语言代码 `mul`，并且应在 `translations.txt` 中提供数据集中使用的每种语言的翻译。如果数据集中的所有原始文本都是同一种语言，则不应使用 `mul`。<hr> _示例：考虑来自瑞士等多语言国家/地区的数据集，原始 `stops.stop_name字段填充了不同语言的站点名称。每个站点名称均根据该站点地理位置的主要语言编写，例如 `Genève表示法语城市Geneva，`Zürich表示德语城市Zurich，`Biel/Bienne表示双语城市Biel/Bienne。数据集 `feed_lang应为 `mul，翻译将在 `translations.txt中提供，德语：`Genf、`Zürich和 `Biel；法语：`Genève、`Zurich和 `Bienne；意大利语：`Ginevra、`Zurigo和 `Bienna；英语：`Geneva、`Zurich和 `Biel/Bienne| 
 | `default_lang| 语言代码 | 可选 |定义当数据消费者t知道骑手的语言时应使用的语言。通常为 `en`（英语）。| 
 | `feed_start_date` | 日期 | 推荐 | 数据集提供从 `feed_start_date` 日开始到 `feed_end_date` 日结束期间完整可靠的服务时间表信息。如果不可用，则可以将两天留空。如果同时提供 `feed_end_date` 日期和 ` feed_start_date `date不得早于`feed_start_date`date。建议数据集提供者提供此期间之外的时间表数据，以告知可能的未来服务，但数据集消费者应注意其非权威状态。如果 `feed_start_date` 或 `feed_end_date` 超出了 [calendar.txt](#calendartxt) 和 [calendar_dates.txt](#calendar_datestxt) 中定义的活动日历日期，则数据集明确断言，在 `feed_start_date` 或 `feed_end_date` 范围内但不包含在活动日历日期中的日期没有服务。| 
 | `feed_end_date` | 日期 | 推荐 | （参见上文）| 
 | `feed_version` |Text| 推荐 | 表示其GTFS数据集当前版本的字符串。使用GTFS的应用程序可以显示此值，以帮助数据集发布者确定是否已合并最新数据集。| 
 | `feed_contact_email` |Email| 可选 | 用于就GTFS数据集和数据发布实践进行沟通的Email地址。` feed_contact_email` 是使用GTFS的应用程序的技术联系人。通过 [agency.txt](#agencytxt) 提供客服联系信息。建议至少提供 `feed_contact_email` 或 `feed_contact_url` 之一。| 
 | `feed_contact_url` | URL | 可选 | 联系信息、Web 表单、支持台或其他有关GTFS数据集和数据发布实践的沟通工具的URL feed_contact_url` 是GTFS使用应用程序的技术联系人。通过 [agency.txt](#agencytxt) 提供客户服务联系信息。建议至少提供 `feed_contact_url` 或 `feed_contact_email` 之一。| 
 
### attributions.txt 
 
 文件：**可选** 
 
 主键（`attribution_id`）
 
 该文件定义应用于数据集的attributions。
 
 | 字段名称 | 类型 | 存在 | 说明 | 
 |------|------|------|------| 
 | `attribution_id` | 唯一 ID |可选 | 标识数据集或其子集的归属。这对翻译非常有用。| 
 | `agency_id` | 外部 ID 引用 `agency.agency_id` | 可选 | 归属适用的机构。<br><br>如果定义了一个 `agency_id` 、 `route_id`或`trip_id`归因，则其他的必须为空。如果均未指定，则归因将应用于整个数据集。| 
 | `route_id` | 引用 `routes.route_id` 的外部 ID | 可选 | 功能与 `agency_id` 相同，只是归因适用于路线。多个attributions可能适用于同一条路线。| 
 | `trip_id` | 引用`trips.trip_id`的外部 ID | 可选 | 功能与 `agency_id` 相同，只是归因适用于一次旅行。多个attributions可能适用于同一次旅行。| 
 | `organization_name` |Text| **必填** | 数据集所属的组织的名称。| 
 | `is_producer` | 枚举 | 可选 | 组织的角色是生产者。有效选项为：<br><br> `0` 或空 - 组织t此角色。<br> `1`组织确实有这个角色。<br><br>字段 `is_producer`、`is_operator` 或 `is_authority` 中至少一个应设置为`1`。| 
 | `is_operator` | Enum | 可选 | 功能与 `is_producer` 相同，只是组织的角色是操作员。| 
 | `is_authority` | Enum | 可选 | 功能与 `is_producer` 相同，只是组织的角色是权威机构。| 
 | `attribution_url` | URL | 可选 | 组织的URL 。|

 
 | `attribution_email` |Email| 可选 | 组织的Email。| 
 | `attribution_phone` |Phone number| 可选 | 组织的Phone number。| 
 

