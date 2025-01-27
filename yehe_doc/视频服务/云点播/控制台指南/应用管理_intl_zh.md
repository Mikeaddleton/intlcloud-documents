## 操作场景
通过应用管理，用户可以停用和销毁该应用内的资源，便于用户更灵活的管理自己的应用。点播的应用存在三种状态分别为正常、停用、销毁状态，应用的生命周期和相关状态含义如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5d453fecd052b987f8219a2fe4e331a2.png)



| 状态 | 含义 |
|---------|---------|
| 正常 | 该状态下应用处于标准使用的情况下，用户可以变更配置，进行相关视频处理，媒资管理等操作。 | 
|已停用|该状态下用户的应用被停用，该应用的资源以及配置文件都会被保留，相应的资源都会按照对应的计费项收费，但在该状态下的应用无法进行配置的变更，也无法在公网上进行访问。|
|已销毁|该状态下的应用内资源被完全销毁，所有的资源和配置文件都被清除，且资源和配置无法被找回。适用于停服场景。|

>!
>- 销毁后的应用支持再次启用，启用的应用其ID（appid/subappid）不会产生变更。
>- 由于统计数据有一定的延迟，故在销毁应用后数据统计存在一定延迟，属于正常现象，不会影响用户的费用结算。
>- 应用的状态变更需要5-10分钟，用户请勿频繁进行变更操作。

由于应用涉及到点播用户对资源管理的权限，故针对应用的停用、销毁操作属于强制敏感权限，需要用户校验身份后才允许操作，身份校验通过半小时内无需二次校验。
应用管理能力的操作页面会依据用户是否开启子应用而变更，针对这两种场景的控制台指南分别如下：

## 账号无子应用

若账号无子应用，则应用管理位于【常用工具】下，用户可以直接对账号新增子应用，并查看详情。
![](https://qcloudimg.tencent-cloud.cn/raw/6f80829605ee04ce07b6414f2fc2c405.png)

此时用户可以立即创建和查看详情。

## 账号有多个子应用

若账号存在多个子应用，则应用管理位于管理员 >【应用管理】下，用户可以对整个应用进行状态变更。用户可以在子应用状态中进行当前应用状态的确认。
![](https://qcloudimg.tencent-cloud.cn/raw/279d7be223412490b95bb0d73e2ed55d.png)

用户可通过开关键来开启和关闭子应用。

## 特别说明：
1. 若用户没有子应用的情况下：
	- 若销毁主应用，则点播账号内的资源和配置会被清空。
	- 若主应用销毁后重新启用，则点播账号会重新启用，如用户账号欠费，请保证您的余额为0，否则无法使用。

2. 当用户有子应用的情况下：
	- 若希望销毁主应用，用户必须首先停用全部主/子应用，否则无法执行该操作。
	- 若主应用销毁后，用户希望重新启用某个子应用，则用户必须首先启用主应用后，才可以重新启用其他子应用，否则无法执行该操作。

