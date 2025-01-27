### 往单个 metric 批量写入数据

此接口同时适用于批量和非批量写入数据至单个 metric 的场景，为提高写入性能，建议批量写入数据。

#### 请求地址

地址为实例的 IP 和 PORT，可从控制台获取到，例如10.13.20.15:9200。

#### 请求路径和方法

请求路径：`/${metric_name}/_doc/_bulk`，${metric_name}为 metric 的名称。
方法：POST

> 说明：
>
> _doc 关键字为写入数据的 _type，为了便于以后系统做解析和升级，请务必加上 _doc 关键字。

#### 请求参数

可通过设置 filter_path 参数来过滤并简化返回结果，具体请参考 [批量查询数据](https://intl.cloud.tencent.com/document/product/1100/45519)。

#### 请求内容

批量写入 metric 需要一种 NDJSON 格式的结构数据，类似于如下：

```
元数据\n
需要写入的数据\n
....
元数据\n
需要写入的数据\n
```

元数据的格式如下所示：

```
{ 
"index" : 
{ 
"_id" : "1",                #文档 ID(选填)
}
}
```

写入数据的格式类似于：

```
{ 
"field1" : "value1",
"field2" : "value2"
}
```

#### 返回内容

需要注意的是，批量写入数据接口与其他接口返回结果稍有不同。请优先关注 json 结果的 errors（注意不是 error）字段，如果为 false，代表所有数据写入成功；如果为 true，代表有部分写入失败，具体失败的详情可以通过 items 字段得到。
items 字段为一个数组，数组中每一个元素与写入请求一一对应，可通过每个元素是否有 error 字段判断请求是否成功，若有 error 字段则表示请求失败，具体错误内容在 error 字段内，若无 error 字段表示请求成功。

#### CURL 示例说明

##### **返回成功的示例：**

请求：

```
curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/ctsdb_test/_doc/_bulk -d'
 {"index":{"routing": "sh" }}
 {"region":"sh","cpuUsage":2.5,"timestamp":1505294654}
 {"index":{"routing": "sh" }}
 {"region":"sh","cpuUsage":2.0,"timestamp":1505294654}
'
```

返回：

```
{
   "took": 134,
   "errors": false,
   "items": 
[
    {
        "index": 
        {
            "_index": "ctsdb_test@1505232000000_1",
            "_type": "_doc",
            "_id": "AV_8eeo_UAkC9PF9L-2q",
            "_version": 1,
            "result": "created",
            "_shards":
             {
                "total": 2,
                "successful": 2,
                "failed": 0
            },
            "created": true,
            "status": 201
            }
        },
        {
        "index": 
        {
            "_index": "ctsdb_test2@1505232000000_1",
            "_type": "_doc",
            "_id": "AV_8eeo_UAkC9PF9L-2r",
            "_version": 1,
            "result": "created",
            "_shards": 
            {
                "total": 2,
                "successful": 2,
                "failed": 0
            },
            "created": true,
            "status": 201
        }
    }
   ]
}
```

> 说明：
>
> 上面返回中的 errors 为 false，代表所有数据写入成功。items 数组标识每一条记录写入结果，与 bulk 请求中的每一条写入顺序对应。items 的单条记录中，status 为 2XX 代表此条记录写入成功，_index 标识了写入的 metric [子表](https://intl.cloud.tencent.com/document/product/1100/45525)，_shards 记录副本写入情况，上例中 total 表示两副本，successful 代表两副本均写入成功。

##### **返回失败的示例：**

请求：

```
curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/hcbs_client_trace/_doc/_bulk -d'
    {"index":{"_id":"5"}}
    {"vol_id":"c57e008c-0ae0-41cd-8da8-6989d0522fc6","io_type":2,"data_len":4096,"latency":3,"try_times":1,"errcode":0,"start_time":1503404266}
    {"index":{"_id":"6"}}
    {"vol_id":"c57e008c-0ae0-41cd-8da8-6989d0522fc6","io_type":"abc","data_len":4096,"latency":1,"try_times":1,"errcode":0,"start_time":1503404266}
'
```

返回：

```
{
    "took":71,
    "errors":true,
    "items":[
        {
            "index":{
                "_index":"hcbs_client_trace@1505232000000_1",
                "_type":"_doc",
                "_id":"5",
                "_version":1,
                "result":"created",
                "_shards":{
                    "total":2,
                    "successful":2,
                    "failed":0
                },
                "_seq_no":0,
                "_primary_term":1,
                "status":201
            }
        },
        {
            "index":{
                "_index":"hcbs_client_trace@1505232000000_1",
                "_type":"_doc",
                "_id":"6",
                "status":400,
                "error":{
                    "type":"illegal_argument_exception",
                    "reason":"mapper [io_type] cannot be changed from type [long] to [keyword]"
                }
            }
        }
    ]
}
```

> 说明：
>
> 上面返回中的 errors 为 true，代表部分数据写入失败。items 数组标识每一条记录写入结果，与 bulk 请求中的每一条写入顺序对应。items 的单条记录中，status 为 2XX 代表此条记录写入成功，error 字段详细给出了错误内容，_index 标识了写入的 metric 子表，_shards 记录副本写入情况，上例中 total 表示两副本，successful 代表两副本均写入成功。

### 往多个 metric 批量写入数据

此接口同时适用于批量和非批量写入单个 metric 或者多个 metric 的场景。为提高写入性能，建议批量写入数据。

#### 请求地址

地址为实例的 IP 和 PORT，可从控制台获取到，例如10.13.20.15:9200。

#### 请求路径和方法

请求路径：`_bulk`
方法：PUT

#### 请求参数

可通过设置 filter_path 参数来过滤并简化返回结果，具体请参考 [批量查询数据](https://intl.cloud.tencent.com/document/product/1100/45519)。

#### 请求内容

批量写入 metric 需要一种 NDJSON 格式的结构数据，类似于如下：

```
元数据\n
需要写入的数据\n
....
元数据\n
需要写入的数据\n
```

元数据的格式如下所示：

```
{ 
"index" : 
{ 
    "_index" :"metric_name",    #要写入的 metric
    "_id" : "1",                #文档 ID(选填)
}
}
```

写入数据的格式类似于：

```
{ 
"field1" : "value1",
"field2" : "value2"
}
```

#### 返回内容

需要通过 error 字段判断请求是否成功，若返回内容有 error 字段则请求失败，具体错误内容在 error 字段内。注意：若请求成功，但是 errors（注意不是 error）字段非等于 false，则该 errors 字段具体指出写入失败的具体数据。

#### CURL 示例说明

请求：

```
curl -u root:le201909 -H 'Content-Type:application/json' -X PUT 172.16.345.14:9201/_bulk -d'
{"index":{"_index" : "ctsdb_test"}}
{"region":"sh","cpuUsage":2.5,"timestamp":1505294654}
{"index":{"_index" : "ctsdb_test2"}}
{"region":"sh","cpuUsage":2.0,"timestamp":1505294654}
'
```

返回：

```
{
    "took":494,
    "errors":false,
    "items":[
        {
            "index":{
                "_index":"ctsdb_test_ay@1505232000000_1",
                "_type":"_doc",
                "_id":"GgJiyXsBE2F__WP8B_ik",
                "_version":1,
                "result":"created",
                "_shards":{
                    "total":2,
                    "successful":1,
                    "failed":0
                },
                "_seq_no":0,
                "_primary_term":1,
                "status":201
            }
        },
        {
            "index":{
                "_index":"ctsdb_test2_ay@1505232000000_1",
                "_type":"_doc",
                "_id":"GwJiyXsBE2F__WP8B_ik",
                "_version":1,
                "result":"created",
                "_shards":{
                    "total":2,
                    "successful":1,
                    "failed":0
                },
                "_seq_no":0,
                "_primary_term":1,
                "status":201
            }
        }
    ]
}
```

> 说明：
>
> 上面返回中的 errors 为 false，代表所有数据写入成功。items 数组标识每一条记录写入结果，与 bulk 请求中的每一条写入顺序对应。items 的单条记录中，status 为 2XX 代表此条记录写入成功，_index 标识了写入的 metric 子表，_shards 记录副本写入情况，上例中 total 表示两副本，successful 代表两副本均写入成功。

