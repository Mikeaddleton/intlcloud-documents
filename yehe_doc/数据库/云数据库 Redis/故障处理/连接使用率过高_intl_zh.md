
## 现象描述
- 现象1：连接使用率指标过高。
![](https://qcloudimg.tencent-cloud.cn/raw/69734df69d793cce934c05b89a6d83b4.png)
- 现象2：无法连接。

## 可能原因
- 连接泄露。
- 最大连接数设置不足。

## 解决思路
您可以检查是否存在连接泄露。对于第三方网络连接，必须要有 finally 块执行，否则后续很容易由于不规范的编码，出现连接未正常释放的问题。

## 处理步骤
### [修改代码逻辑](id:xgdmlj)
检查是否存在连接泄露，如果存在泄露，您可以释放无效连接，并修正导致连接泄露的不规范代码。

### [修改连接配置](id:xgljpz)
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例详情页面。
2. 在实例详情页面的“网络信息”>“最大连接数”栏，单击【调整】调整最大连接数。
![](https://qcloudimg.tencent-cloud.cn/raw/ed736808880fdd4f3ad4f86b69e0a617.png)
3. 在弹出的对话框，调整最大连接数，单击【确定】。

>?如果以上方法仍未解决问题，您还可以通过 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 联系售后。
