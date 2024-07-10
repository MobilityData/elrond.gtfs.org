# GTFS：使公共交通数据普遍可访问

## 公共交通乘客信息的开放数据标准

通用公共General Transit Feed Specification，也称为GTFS，是一种标准化数据格式，为公共交通机构提供了一种结构来描述其服务的详细信息，例如时刻表、stops、票价等。

它允许公共交通机构以一种可被各种软件应用程序（最常见的是行程规划器）使用的格式发布其公共交通数据。这意味着用户可以使用智能手机或类似设备轻松获取旅行信息以访问公共交通服务。

<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_001.png"> 
 
 如今， GTFS已成为全球数千家公共交通提供商的首选 [开放标准](https:)。一些机构自己生成这些数据，而其他机构则聘请供应商为他们创建和维护数据。
 
## 支持静态和动态数据 
 
 GTFS由两个主要部分组成：[GTFS Schedule](../../documentation/schedule/reference) 和 [GTFS Realtime](../../documentation/realtime/reference)。
 
<img class="center" width="560" height="100%" src="../../../assets/what_is_gtfs_002.png"> 
 
 GTFS Schedule包含有关routes、时刻表、票价和地理交通详情等众多功能的信息，并以简单的文本文件形式呈现[^1]。这种简单的格式可以轻松创建和维护，而无需依赖复杂或专有软件。
 
 GTFS GTFS Realtime包含行程更新、vehicle位置和服务警报，使用 [Protocol Buffers](https://developers.google.com/protocol-buffers/) 格式。GTFS 的这一部分与GTFS Schedule配合使用，以便通知乘客服务中断和更新的arrival时间。
 
 GTFS Schedule和GTFS Realtime参考文档可在 [技术文档部分](../../documentation/overview) 中找到。
 
 <iframe class="center" width="560" height="315" src="https://www.youtube-nocookie.com/embed/SDz2460AjNo?si=wFsaN4_Hr3ypxWdp" title="YouTube 视频播放器" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> 
 
<a href="https://www.flaticon.com/authors/freepik" title="Freepik 的图标">由 Freepik- Flaticon 创建的图标</a>
 
 [^1]: 除了文本文件之外， GTFS现在还支持 [GeoJSON](https: ) 格式，以表示需求响应服务的某些元素。
 

