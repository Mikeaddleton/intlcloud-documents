对象存储（Cloud Object Storage，COS）是腾讯云提供的一种存储海量文件的分布式存储服务，用户可通过网络随时存储和查看数据。腾讯云 COS 使所有用户都能使用具备高扩展性、低成本、可靠和安全的数据存储服务。

COS 通过控制台、API、SDK 和工具等多样化方式简单、快速地接入，实现了海量数据存储和管理。通过 COS 可以进行任意格式文件的上传、下载和管理。腾讯云提供了直观的 Web 管理界面，同时遍布全国范围的 CDN 节点可以对文件下载进行加速。


## 产品功能

对象存储 COS 为广大企业和个人用户提供数据管理、异地容灾、数据访问加速和数据处理等功能，涵盖诸多场景，详情请参见 [功能概览](https://intl.cloud.tencent.com/document/product/436/8186) 文档。

## 基本概念

下面通过几个名词概念，帮助您进一步了解腾讯云对象存储 COS：

- [存储桶（bucket）](https://intl.cloud.tencent.com/document/product/436/13312) ：是对象的载体，可理解为存放对象的“容器”。一个存储桶可容纳无数个对象。
- [对象（Object）](https://intl.cloud.tencent.com/document/product/436/13324)：是对象存储的基本单元，可理解为任何格式类型的数据，例如图片、文档和音视频文件等。
- [地域（Region）](https://intl.cloud.tencent.com/document/product/436/6224)：是腾讯云托管机房的分布地区，对象存储 COS 的数据存放在这些地域的存储桶中。
- [访问域名（Endpoint）](https://intl.cloud.tencent.com/document/product/436/6224)：对象被存放到存储桶中，用户可通过访问域名访问和下载对象。



## 存储类型

存储类型可体现对象在 COS 中的存储级别和活跃程度。COS 提供多种对象的存储类型：智能分层存储、标准存储、低频存储、归档存储、深度归档存储。每种存储类型拥有不同的特性，例如对象访问频度、数据持久性、数据可用性和访问时延等。用户可根据自身场景选择以哪种存储类型将数据上传至 COS。

> ?关于不同存储类型的对比介绍，请参见 [存储类型概述](https://intl.cloud.tencent.com/document/product/436/30925)。

### 标准存储

标准存储（STANDARD）属于热数据类型，拥有低访问时延、高吞吐量的性能，可为用户提供高可靠性、高可用性、高性能的对象存储服务。


**适用场景**

标准存储适用于实时访问大量热点文件、频繁的数据交互等业务场景，例如热点视频、社交图片、移动应用、游戏程序、静态网站等。


### 低频存储

低频存储（STANDARD_IA）可为用户提供高可靠性、较低存储成本和较低访问时延的对象存储服务。在降低存储价格的基础上，保持首字节访问时间在毫秒级，保证用户在取回数据的场景下无需等待，高速读取。与标准存储有明显区别的是，用户访问数据时会收取数据取回费用。


**适用场景**

低频存储适用于较低访问频率（例如平均每月访问频率1到2次）的业务场景，例如网盘数据、大数据分析、政企业务数据、低频档案、监控数据。

### 智能分层存储

智能分层存储（INTELLIGENT_TIERING）类型的对象可存放在标准存储层和低频存储层两个存储层，COS 可根据智能分层存储类型对象的访问频次自动在两个存储层之间变换，无数据取回费用，可降低用户的存储成本。

**适用场景**

智能分层存储适用于访问模式不固定的对象，如果您的业务对成本要求较为严格，且对文件读取性能较不敏感，您可以使用该存储类型来降低使用成本。

### 归档存储

归档存储（ARCHIVE）属于冷数据类型，数据取回时需要提前恢复（解冻），可为用户提供高可靠性、极低存储成本和长期保存的对象存储服务。归档存储有最低90天的存储时间要求，并且在读取数据前需要先进行数据恢复（解冻）。

**适用场景**

归档存储适用于需要长期保存数据的业务场景，例如档案数据、医疗影像、科学资料等合规性文件归档、生命周期文件归档、操作日志归档以及异地容灾。

### 深度归档存储

深度归档存储（DEEP_ARCHIVE）可为用户提供高可靠性、比其他存储类型都低的存储成本和长期保存的对象存储服务。深度归档存储有最低180天的存储时间要求，并且在读取数据前需要先进行数据恢复。

**适用场景**

深度归档存储适用于需要长期保存数据的业务场景。例如医疗影像数据、视图数据、日志数据。

## 如何使用 COS？

对象存储 COS 为用户提供多种使用方式，具体介绍请见下表：

<table>
<thead>
<tr>
<th align="left" width="30%">入门方式</th>
<th align="left" width="70%">功能说明</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/32955">控制台</a></td>
<td align="left" width="70%">对象存储控制台是 COS 为用户提供的最简单且易于上手的操作方式。用户无需编写代码或运行程序，可直接通过 COS 控制台使用 COS 服务。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser 工具</a></td>
<td align="left" width="70%">本工具支持用户通过可视化界面，方便地进行数据的上传、下载、生成访问链接等操作。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/10976">COSCMD 工具</a></td>
<td align="left" width="70%">本工具支持用户使用简单的命令行指令实现对对象的批量上传、下载、删除等操作。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">API 方式</a></td>
<td align="left" width="70%">COS 使用 XML API，这是一种轻量级的、无连接状态的接口，调用此接口您可以直接通过 HTTP/HTTPS 发出请求和接受响应，实现与腾讯云对象存储后台的交互操作。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 方式</a></td>
<td align="left" width="70%">支持多种主流开发语言：Android、C、C++、.NET、Go、iOS、Java、JavaScript、Node.js、PHP、Python、小程序 SDK。</td>
</tr>
</tbody></table>




## COS 如何收费？

COS 的默认计费方式为按量计费（后付费），详情请参见 [计费概述](https://intl.cloud.tencent.com/document/product/436/16871) 文档。


## 相关文档

其他介绍文档请参见 [开发者指南](https://intl.cloud.tencent.com/document/product/436/14102)。
