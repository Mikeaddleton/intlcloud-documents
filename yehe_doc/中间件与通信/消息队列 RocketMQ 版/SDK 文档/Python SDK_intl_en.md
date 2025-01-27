## Overview 

This document describes how to use open-source SDK to send and receive messages using the SDK for Python as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1112/43069).
- [You have installed Python](https://www.python.org/downloads/)
- [You have installed pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-python-sdk-demo.zip)

## Directions

### Step 1. Prepare the environment

As RocketMQ-client Python is lightweight wrapper around [rocketmq-client-cpp](https://github.com/apache/rocketmq-client-cpp), you need to install **librocketmq** first.

1. Install `librocketmq` 2.0.0 or later as instructed in [Install librocketmq](https://github.com/apache/rocketmq-client-python).
2. Run the following command to install `rocketmq-client-python`.
<dx-codeblock>
:::  shell
   pip install rocketmq-client-python
:::
</dx-codeblock>


### Step 2. Produce messages

Create, compile, and run a message production program.
<dx-codeblock>
:::  python
from rocketmq.client import Producer, Message

# Initialize the producer and set the producer group information
producer = Producer(groupName)
# Set the service address
producer.set_name_server_address(nameserver)
# Set permissions (role name and token)
producer.set_session_credentials(
 	accessKey,  # Role token
    secretKey,  # Role name
    ''
)
# Start the producer
producer.start()

# Assemble messages. The topic name must be a full name concatenated by the full namespace name and the topic name, such as “rocketmq-xxx|namespace_python%topic1”.
msg = Message(topicName)
# Set keys
msg.set_keys(TAGS)
# Set tags
msg.set_tags(KEYS)
# Message content
msg.set_body('This is a new message.')

# Send messages in sync mode
ret = producer.send_sync(msg)
print(ret.status, ret.msg_id, ret.offset)
# Release resources
producer.shutdown()
:::
</dx-codeblock>
</dx-codeblock>
<table>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>groupName</td>
        <td>Producer group name, which can be obtained under the **Group** tab on the cluster details page in the console.</td>
    </tr>
    <tr>
        <td>nameserver</td>
        <td>Cluster access address, which can be obtained by clicking <b>Access Address</b> in the **Operation** column of the cluster list on the <b>Cluster</b> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/88046dcc0b052e11dc5c7c2ee8a901e4.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>secretKey</td>
        <td>Role name, which can be copied on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.</td>
    </tr>
    <tr>
        <td>accessKey</td>
        <td>Role token, which can be copied in the <b>Token</b> column on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/738800581043835d6123385964281f37.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>topicName</td>
        <td>`topicName` is in the format of <code>full namespace name</code>+<code>%</code>+<code>topic name</code>.
				<ul style = "margin-bottom: 0px;"><li>The full namespace name, which is in the format of <code>cluster ID</code> +<code>｜</code>+<code>namespace</code>, can be copied under the **Namespace** tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/c483d23c09d2f728aaa08b195d9ddd40.png" style="width: 100%"></li><li>The topic name can be copied under the **Topic** tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/4b096254ae2fa8db0f45c1f864718915.png" style="width: 100%">
						</li>
						</ul>
        </td>
    </tr>
    <tr>
        <td>TAGS</td>
        <td>A parameter used to set the tag of messages that are subscribed to.</td>
    </tr>
		 <tr>
        <td>KEYS</td>
        <td>A parameter used to set the message key.</td>
    </tr>
</table>

### Step 3. Consume messages

Create, compile, and run a message consumption program.
<dx-codeblock>
:::  python
import time

from rocketmq.client import PushConsumer, ConsumeStatus


# Message processing callback
def callback(msg):
    # Simulate the business processing logic
    print('Received message. messageId: ', msg.id, ' body: ', msg.body)
    # Return CONSUME_SUCCESS if the consumption is successful
    return ConsumeStatus.CONSUME_SUCCESS
    # Return the consumption status if the consumption is successful
    # return ConsumeStatus.RECONSUME_LATER


# Initialize the consumer and set the consumer group information (consumer group information refers to the full namespace name concatenated by the group name, such as “rocketmq-xxx|namespace_python%group11”)
consumer = PushConsumer(groupName)
# Set the service address
consumer.set_name_server_address(nameserver)
# Set permissions (role name and token)
consumer.set_session_credentials(
	accessKey,  # Role token
    secretKey,  # Role name
    ''
)
# Subscribe to a topic
consumer.subscribe(topicName, callback, TAGS)
print(' [Consumer] Waiting for messages.')
# Start the consumer
consumer.start()

while True:
    time.sleep(3600)
# Release resources
consumer.shutdown()
:::
</dx-codeblock>
<table>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>groupName</td>
        <td>The consumer group information refers to the full namespace name concatenated by the group name, such as <code>rocketmq-xxx|namespace_python%group11</code>. The namespace name and group name can be obtained respectively under the **Namespace** and **Group** tab on the cluster details page in the console.</td>
    </tr>
    <tr>
        <td>nameserver</td>
        <td>Cluster access address, which can be obtained by clicking <b>Access Address</b> in the **Operation** column of the cluster list on the <b>Cluster</b> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/88046dcc0b052e11dc5c7c2ee8a901e4.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>secretKey</td>
        <td>Role name, which can be copied on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.</td>
    </tr>
    <tr>
        <td>accessKey</td>
        <td>Role token, which can be copied in the <b>Token</b> column on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/738800581043835d6123385964281f37.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>topicName</td>
        <td>`topicName` is in the format of <code>full namespace name</code>+<code>%</code>+<code>topic name</code>.
				<ul style = "margin-bottom: 0px;"><li>The full namespace name, which is in the format of <code>cluster ID</code> +<code>｜</code>+<code>namespace</code>, can be copied under the **Namespace** tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/c483d23c09d2f728aaa08b195d9ddd40.png" style="width: 100%"></li><li>The topic name can be copied under the **Topic** tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/4b096254ae2fa8db0f45c1f864718915.png" style="width: 100%">
						</li>
						</ul>
        </td>
    </tr>
    <tr>
        <td>TAGS</td>
        <td>A parameter used to set the tag of messages that are subscribed to. The default value is set to <code>*</code>, which means subscribing to all messages.</td>
    </tr>
</table>



### Step 4. View consumption details

Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![](https://qcloudimg.tencent-cloud.cn/raw/924898b7a5568be778449bf51034396d.png)

>?Above is a brief introduction to message publishing and subscription. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-python-sdk-demo.zip) or [RocketMQ-Client-Python Sample](https://github.com/apache/rocketmq-client-python/tree/master/samples).

