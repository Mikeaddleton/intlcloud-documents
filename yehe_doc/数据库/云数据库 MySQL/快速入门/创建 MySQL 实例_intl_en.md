
This document describes how to create a TencentDB for MySQL instance in the console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>

- To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to the [TencentDB for MySQL purchase page](https://buy.intl.cloud.tencent.com/cdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: select the region that you want your TencentDB for MySQL instance to be deployed in. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Database Version**: currently, TencentDB for MySQL supports MySQL 8.0, 5.7, 5.6, and 5.5. For more information on the features of each version, see [official documentation](https://dev.mysql.com/doc/refman/5.7/en/).
  - **Architecture**: single-node, two-node, or three-node. For more information, see [Database Architecture](https://intl.cloud.tencent.com/document/product/236/38328).
  - **Data Replication Mode**: async, semi-sync, and strong sync replication modes are supported. For more information, see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Source AZ** and **Replica AZ**: select different source and replica AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) to protect your database from failures and AZ outages.
>?
>- If the source and replica nodes are in different AZs, there may be an additional network sync delay of 2–3 ms.
>- When you purchase Tencent Cloud services, we recommend you select the region closest to you to minimize access latency and improve download speed.
>
 - **Instance Type**: general or dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specs**: select specifications as needed.
 - **Hard Disk**: the disk space is used to store the files required by MySQL execution.
 - **Network**: select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default. We recommend that you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Custom Port**: the database access port, which is 3306 by default.
 - **Security Group**: for more information on security group creation and management, see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
>?Port 3306 must be opened for the MySQL instance through the inbound rule of the security group. The MySQL instance uses private network port 3306 by default and supports custom port. If the default port is changed, the new port should be opened in the security group.
 - **Parameter Template**: besides the system parameter template provided by TencentDB, you can create a custom parameter template. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).
  - **Character Set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is UTF8. After purchasing the instance, you can change the character set on the instance details page in the console. For more information, see [Use Limits > Notes on character set](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity**: whether the table name is case sensitive. The default value is **Enabled**.
 - **Root Password**: set the password of the root account (the default user name for a new MySQL database is "root"). If you select **Auto-generated Password**, you can [reset the password](https://intl.cloud.tencent.com/document/product/236/31901) after creating the instance.
 - **Alarm Policy**: you can create an alarm policy to trigger alarms and send messages when the Tencent Cloud resource state changes. For more information, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project**: select a project to which the TencentDB instance belongs. The default project is used.
 - **Tag**: categorize and manage resources with tags. For more information, see [Tag > Overview](https://intl.cloud.tencent.com/document/product/236/31917).
 - **Instance Name**: name the instance now or later.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
 - **Purchase Period**: select the desired duration according to your business needs. The billing mode is monthly subscription, and the longer the purchase period, the higher the discount.
 - **Terms of Service**: for more information, see [Terms of Service](https://intl.cloud.tencent.com/document/product/236/35543).
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can operate the instance after around 3-5 minutes when its status changes to **Running**.

## Subsequent Operations
You can access the TencentDB for MySQL instance over both private and public networks from a Windows or Linux CVM instance. For more information, see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).

