## 地域

### 简介

地域（Region）是指物理的数据中心的地理区域。腾讯云不同地域之间完全隔离，保证不同地域间最大程度的稳定性和容错性。为了降低访问时延、提高下载速度，建议您选择最靠近您客户的地域。

您可以通过下表查看弹性容器服务 EKS 当前支持的地域、可用区及资源类型，其他地域将相继开放。

### 相关特性

- 不同地域之间的网络完全隔离，不同地域之间的云产品**默认不能通过内网通信**。
- 不同地域之间的云产品，可以通过 [公网 IP](https://intl.cloud.tencent.com/document/product/213/5224) 访问 Internet 的方式进行通信。处于不同私有网络的云产品，可以通过 [云联网](https://intl.cloud.tencent.com/document/product/1003) 进行通信，此通信方式较为高速、稳定。
- [负载均衡](https://intl.cloud.tencent.com/document/product/214 ) 当前默认支持同地域流量转发，绑定本地域的云服务器。如果开通 [跨地域绑定](https://intl.cloud.tencent.com/document/product/214/38441) 功能，则可支持负载均衡跨地域绑定云服务器。

## 可用区

### 简介

可用区（Zone）是指腾讯云在同一地域内电力和网络互相独立的物理数据中心。其目标是能够保证可用区间故障相互隔离（大型灾害或者大型电力故障除外），不出现故障扩散，使得用户的业务持续在线服务。通过启动独立可用区内的实例，用户可以保护应用程序不受单一位置故障的影响。
您可以通过 API 接口 [查询可用区列表](https://intl.cloud.tencent.com/document/product/213/35071) 查看完整的可用区列表。

### 相关特性

处于相同地域不同可用区，但在同一个私有网络下的云产品之间均通过内网互通，可以直接使用 [内网 IP](https://intl.cloud.tencent.com/document/product/213/5225) 访问。
>? 内网互通是指同一账户下的资源互通，不同账户的资源内网完全隔离。



## 中国
<table class="table-striped">
<tbody>
	<tr>
		<th>地域</th>
		<th>可用区</th>
	</tr>
	<tr>
		<td rowspan="3">华南地区（广州）<br> ap-guangzhou</td>
		<td>广州三区<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>广州四区<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>广州六区<br> ap-guangzhou-6</td>
	</tr>
	<tr>
	</tr>
	<tr>
		<td rowspan="4">华东地区（上海）<br>ap-shanghai</td>
		<td>上海二区<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>上海三区<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>上海四区<br>ap-shanghai-4</td>
	</tr>
	<tr>
		<td>上海五区<br>ap-shanghai-5</td>
	</tr>
		<tr>
			<td rowspan="2">华东地区（南京）<br>ap-nanjing</td>
			<td>南京一区<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>南京二区<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="5">华北地区（北京）<br>ap-beijing</td>
			<td>北京三区<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>北京四区<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>北京五区<br>ap-beijing-5</td>
	</tr>
	     <tr>
			<td>北京六区<br>ap-beijing-6</td>
	</tr>
	     <tr>
			<td>北京七区<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">西南地区（成都）<br>ap-chengdu</td>
		<td>成都一区<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>成都二区<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td rowspan="1">港澳台地区（中国香港）<br>ap-hongkong</td>
			<td>香港二区（中国香港节点可用于覆盖港澳台地区）<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>
## 其他国家和地区	
<table class="table-striped">
	<tbody>
	<tr>
			<th>地域</th>
			<th>可用区</th>
		</tr>
			<tr>
			<td  rowspan="2">亚太东南（新加坡）<br>ap-singapore</td>
			<td>新加坡一区（新加坡节点可用于覆盖亚太东南地区）<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>新加坡二区（新加坡节点可用于覆盖亚太东南地区）<br>ap-singapore-2</td>
		</tr>
		<tr>
		<tr>
			<td>亚太东南（雅加达）<br>ap-jakarta</td>
			<td>雅加达一区（雅加达节点可用于覆盖亚太东南地区）<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td  rowspan="2">亚太东北（首尔）<br>ap-seoul</td>
			<td>首尔一区（首尔节点可用于覆盖亚太东北地区）<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>首尔二区（首尔节点可用于覆盖亚太东北地区）<br>ap-seoul-2</td>
		</tr>
		<tr >
			<td >亚太东北（东京）<br>ap-tokyo</td>
			<td>东京二区（东京节点可用区覆盖亚太东北地区）<br>ap-tokyo-2</td>
		</tr>
		<tr>
			<td  rowspan="2">亚太南部（孟买）<br>ap-mumbai</td>
			<td>孟买一区（孟买节点可用于覆盖亚太南部地区）<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>孟买二区（孟买节点可用于覆盖亚太南部地区）<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >亚太东南（曼谷）<br>ap-bangkok </td>
			<td >曼谷一区  （曼谷节点用户覆盖亚太东南地区）<br>ap-bangkok-1</td>
		</tr>
		<tr>
			<td>北美地区（多伦多）<br>na-toronto</td>
			<td>多伦多一区（多伦多节点可用于覆盖北美地区）<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">美国东部（弗吉尼亚）<br>na-ashburn</td>
			<td>弗吉尼亚一区 （弗吉尼亚节点用户覆盖美国东部地区）<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>弗吉尼亚二区 （弗吉尼亚节点用户覆盖美国东部地区）<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>欧洲地区（法兰克福）<br>eu-frankfurt</td>
			<td>法兰克福一区（法兰克福节点可用于覆盖欧洲地区）<br>eu-frankfurt-1</td>
		</tr>
		<td >欧洲地区（莫斯科）<br>eu-moscow</td>
		<td>莫斯科一区（莫斯科节点可用区覆盖欧洲地区）<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>
