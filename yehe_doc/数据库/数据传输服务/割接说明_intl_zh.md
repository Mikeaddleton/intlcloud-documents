
## 注意事项
- 为便于区分会话信息以及提升数据安全性，建议单独创建一个数据库帐号以供数据迁移使用。
- 为了避免因业务割接失败，导致源库和目标库数据不一致性，请在割接之前将源库业务切换到一个备份的数据库上。
- 由于割接需要暂停源库的数据写入，建议您选择一个业务低峰期进行业务割接。 

## 操作步骤
1. 登录 [DTS 控制台](https://console.cloud.tencent.com/dts/migration)，根据有无增量迁移，选择如下步骤：
   - 有增量迁移：请执行步骤 [2](#step2)。
   - 无增量迁移：请执行步骤 [6](#step6)。
2. [](id:step2)等待数据迁移任务的【迁移步骤】显示为【同步增量】，并且目标与源库数据差距为0MB，目标与源库时间延迟为0秒。
![](https://qcloudimg.tencent-cloud.cn/raw/c32cafc476ba23e39456ea7cd2219170.png)
3. 暂停源库业务，停止新的数据写入。
4. 根据源数据库的不同类型，选择如下对应代码查看是否有新的会话信息。如果1分钟 - 5分钟内显示结果除 DTS 迁移实例的连接外，无任何新的会话执行，即可认为业务已经完全停止。
 - MySQL 
```
show processlist  
```
 - SQL Server
```
select * from sys.dm_exec_connections;
```
 - PostgreSQL
```
select * from pg_stat_activity;
```
 - MongoDB
```
use admin
db.runCommand({currentOp: 1, $all:[{"active" : true}]})
```
5. 结束增量迁移任务。
再次查看迁移任务，等待目标与源库数据差距为0MB，目标与源库时间延迟为0秒，并保持1分钟以上，单击【完成】，结束增量迁移任务。
![](https://qcloudimg.tencent-cloud.cn/raw/1ffcd386bc18f2f7296ff172ded02faa.png)
6. [](id:step6)验证源库和目标库的数据一致后，确定割接时机，将业务系统指向目标数据库，恢复业务使用。

