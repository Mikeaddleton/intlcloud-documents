## 现象描述
慢查询现象出现的时候，一般伴随着多个监控指标同时飙升，如 CPU 使用率、慢查询数量。

## 可能原因
通常情况下是 SQL 语句的执行效率不够高，导致大量的请求堆积在云数据库 MySQL 中，常见原因有两个：
- [](id:yy1)原因1：SQL 语句没有利用索引或者没有用较佳的索引。
- [](id:yy2)原因2：QPS 压力超过当前实例的承载上限。

## 解决思路
针对两个可能的原因，分别有不同的解决思路：
- 解决思路1：优化 SQL 语句，提升 SQL 语句的执行效率。详情请参见 [措施1](#cs1)。
- 解决思路2：提升云数据库 MySQL 的配置。详情请参见 [措施2](#cs2)。

## 处理步骤
### [措施1：优化 SQL 语句](id:cs1)
可以直接用数据库智能管家 DBbrain 来进行慢查询优化。DBbrain 会分析 SQL 语句并给出加索引的建议。
1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/performance/analysis)，在左侧导航选择**诊断优化**，在上方选择对应数据库，然后选择**慢 SQL 分析**页。
2. 单击（选择单一时间段）或拉选（选择多个时间段）**SQL 统计**图表的慢查询（柱形图），下方会显示聚合 SQL 模板以及执行信息（包括执行次数、总耗时执行时间、扫描行数、返回行数等）。
![](https://main.qcloudimg.com/raw/0659dcb5dfb47bf00c4df2646946f0ce.png)
3. 单击某条聚合的 SQL 模板行，右侧边会弹出 SQL 的具体分析和统计数据，可查看对应索引建议。
![](https://main.qcloudimg.com/raw/f72dcf38d05fc7381007502e930f3014.png)

### [措施2：提升云数据库 MySQL 配置](id:cs2)
查看各规格对应的 [QPS 官方压测数据](https://intl.cloud.tencent.com/document/product/236/8842)，与当前实例的 QPS 数据进行比较，调整对应的 [MySQL CPU 和内存规格](https://intl.cloud.tencent.com/document/product/236/19707)。
