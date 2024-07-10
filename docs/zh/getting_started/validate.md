# 评估GTFS信息的质量 
 
 高质量的GTFS是完整、准确和最新的。这意味着它代表了服务当前的运行方式并提供尽可能多的信息。
 
## 完整的数据 
 
 高质量的GTFS包括重要的服务详情，例如假期和夏季时刻表变更、准确的停靠站点位置以及与其他面向乘客的材料相匹配的routes名称和头牌。即使agency与供应商合作制作GTFS，最终还是由agency来确保印刷版、车上和在线呈现的信息是一致的。
 
## 准确的数据 
 
 准确的数据对于为乘客提供可靠且用户友好的交通体验至关重要。数据中的错误可能会阻止使用部分或全部数据集。
 
## 最新数据 
 
 过时的数据可能比没有可用的信息更成问题。仅仅发布信息是不够的——它必须与乘客的所见所闻相匹配。一些最大的交通运输机构每周甚至每天更新他们的GTFS ，但大多数机构需要每隔几个月或每年几次在服务发生变化时更新他们的GTFS 。这包括新routes或stops、时间表变更或票价结构更新等内容。
 
 许多机构聘请供应商为他们创建和管理GTFS 。一些供应商可能会主动询问服务变化，但重要的是机构要与供应商沟通即将发生的服务变化。可以提前发布包含服务变更的GTFS ，确保每个人（机构、供应商、行程规划人员和乘客）都能顺利过渡！
 
## 使用官方验证器
 
 官方GTFS验证器根据官方规范评估数据集的质量，确保业内对什么是高质量数据集达成共识。 
 
 由 [MobilityData](https://mobilitydata.org/) 维护的免费开源 [规范GTFS Schedule验证器](https://mobilitydata.org/)[^1] 可确保您的GTFS数据符合官方 [GTFS Schedule参考](../../documentation/schedule/reference/) 和 [最佳实践](../../documentation/schedule/schedule_best_practices)。它提供可与其他方共享的易于使用的报告和全面的文档。
 
<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li>前往<a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a> 。</li> 
<li>加载您的GTFS数据集：您可以选择或拖放一个 ZIP 文件，或者复制/粘贴一个URL。</li> 
<li>验证完成后，将提供打开报告的选项。</li> 
<li>您将看到验证器是否发现数据问题，以及有关如何修复这些问题的文档链接。验证报告的URL将有效期为 30 天，并且可以与其他人共享。</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 同样，使用免费开源规范的 [GTFS Realtime验证器](https:) 可确保您的GTFS数据符合官方的 [GTFS Realtime参考](../../documentation/realtime/reference/) 和 [最佳实践](../../documentation/realtime/realtime_best_practices)。
 
 有关创建高质量数据的信息，请参阅 [加州交通数据指南](https:)、[GTFS Schedule最佳实践](../../documentation/schedule/schedule_best_practices) 和 [GTFS Realtime最佳实践](../../documentation/realtime/realtime_best_practices)。 
 
 [^1]: 要查看有关如何在数据管道中使用此工具并为该项目做出贡献的更多说明，请访问 [GitHub 存储库](https:)。
 

