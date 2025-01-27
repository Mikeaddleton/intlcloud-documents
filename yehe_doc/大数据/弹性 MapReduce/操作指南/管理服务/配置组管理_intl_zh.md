## 功能介绍
配置组用于将部署同一服务的不同规格或用途的节点进行分组配置管理，本文主要介绍如何使用配置组对服务配置进行管理。

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在**集群列表**中选择对应的集群单击**详情**进入集群详情页。
2. 在集群详情页中选择**集群服务**单击对应的组件卡页右上角**操作**>**配置管理**，以 HDFS 为例。
3. 单击**配置管理**，设置“维度范围”为**配置组**，并选择对应的配置组以及变更参数所在的文件，单击**修改配置**即可对参数进行新增、修改和删除操作。
>?集群创建完后，每个组件会生成一个默认的配置组，默认配置组支持修改不支持删除，默认配置组初始化时继承集群维度配置，可根据需要增加新的配置组，每个组件配置组不超过10个。
4. 单击**管理配置组**设置配置组，进入“管理配置组”页，可分别单击**添加配置组**、**修改**和**删除**对配置组进行新增、修改和删除。
![](https://main.qcloudimg.com/raw/ff447e9c6676627682ca593f857900b9.png)
![](https://main.qcloudimg.com/raw/a0b2473ce46ffa36cf7ee5c090777b65.png)
![](https://main.qcloudimg.com/raw/e2e544be85fca345a0b3a461c02e55fd.png)
5. 配置组中存在节点配置与当前配置组配置不一致时，可单击右上角**同步配置**将配置组配置下发到配置不一致的节点。
![](https://main.qcloudimg.com/raw/7286e6eb52685a59dfb0e53eed087dd5.png)
进入“同步配置”页面，可单击**详情**查看详细信息，也可单击**同步配置**完成配置组的同步。
![](https://main.qcloudimg.com/raw/7a6e3b61a7c61ba94ab9b45a0481765a.png)
