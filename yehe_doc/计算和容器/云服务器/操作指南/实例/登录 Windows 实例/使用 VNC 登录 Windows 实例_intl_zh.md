## 操作场景

VNC 登录是腾讯云为用户提供的一种通过 Web 浏览器远程连接云服务器的方式。在没有安装或者无法使用远程登录客户端，以及通过其他方式均无法登录的情况下，用户可以通过 VNC 登录连接到云服务器，观察云服务器状态，并且可通过云服务器账户进行基本的云服务器管理操作。

## 使用限制

- VNC 登录的云服务器暂时不支持复制粘贴功能、中文输入法以及文件的上传、下载。
- VNC 登录云服务器时，需要使用主流浏览器，例如 Chrome，Firefox，IE 10及以上版本等。
- VNC 登录为独享终端，即同一时间只有一个用户可以使用 VNC 登录。


## 前提条件
已获取远程登录 Windows 实例需要使用实例的管理员帐号和对应的密码。
 - 如在创建实例时选择系统随机生成密码，则请往 [站内信](https://console.cloud.tencent.com/message) 获取。
 - 如已设置登录密码，则请使用该密码登录。如忘记密码，则请  [重置实例密码](https://intl.cloud.tencent.com/document/product/213/16566)。


## 操作步骤

1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 在实例的管理页面，根据实际使用的视图模式进行操作：
<dx-tabs>
::: 列表视图
找到需要登录的 Windows 云服务器，单击右侧的**登录**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: 页签视图
选择需要登录的 Windows 云服务器页签，单击**登录**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)
:::
</dx-tabs>

3. 在打开的“标准登录 | Windows 实例”窗口中，选择 **VNC登录**。如下图所示：
![](https://main.qcloudimg.com/raw/9f964c1ebdec90f7e371b42340e13662.png)
4. 在弹出的登录窗口中，选择左上角的**发送远程命令**，单击 **Ctrl-Alt-Delete** 进入系统登录界面。如下图所示：
![](https://main.qcloudimg.com/raw/c07755c1e0d0040e2ecb87f048b8be1b.png)
5. 输入登录密码，按 **Enter**，即可登录到 Windows 云服务器。

