本文介绍嵌套子查询的语法使用与操作示例。

## 语法格式

针对一些复杂的统计分析场景，需要先对原始数据进行一次统计分析，再针对该分析结果进行二次统计分析，这时候需要在一个 SELECT 语句中嵌套另一个 SELECT 语句，这种查询方式称为嵌套子查询。

```
* | SELECT key FROM (subquery)
```

- subquery：子查询，需被包裹在括号中。
- key：需要从子查询中获取哪些字段进行二次统计分析。
- 支持多层嵌套，不局限于两层。


## 语法示例

计算当前1小时和昨天同时段的网站访问量比值：
选择查询和分析的时间范围为近1小时，并执行如下查询和分析语句，其中86400表示当前时间减去86400秒（1天）。

**查询和分析语句**

```
* | SELECT compare(PV, 86400) FROM (SELECT count(*) AS PV)
```
- `SELECT count(*) AS PV`为第一层统计分析，针对原始日志统计获得网站访问量 PV。
- `SELECT compare(PV, 86400) FROM`为第二层统计分析，针对第一层统计分析的结果，对 PV 进行二次统计，使用 [同环比函数compare](https://intl.cloud.tencent.com/document/product/614/43575) 获得1天前的网站访问量 PV。

**查询和分析结果**
![image-20211108045216150](https://qcloudimg.tencent-cloud.cn/raw/70a9de0c7c2c4c0a345a935b55c1873b.png)

- 1860表示当前1小时的网站访问量。
- 1656表示昨天同时段的网站访问量。
- 1.1231884057971016表示当前1小时与昨天同时段的网站访问量比值。



如需查询和分析结果为分列显示，则可进一步嵌套查询：

**查询和分析语句**

```
* | 
SELECT compare[1] AS today, compare[2] AS yesterday, compare[3] AS ratio
FROM (
    SELECT compare(PV, 86400) AS compare
    FROM (
        SELECT COUNT(*) AS PV
    )
)
```
`SELECT compare[1] AS today, compare[2] AS yesterday, compare[3] AS ratio FROM` 针对 compare 函数的结果，通过数组下标获取其中特定位置的数值。

**查询和分析结果**
![image-20211108045502511](https://qcloudimg.tencent-cloud.cn/raw/e8dd894470cb045dc5cc5e6a86f3abd3.png)
