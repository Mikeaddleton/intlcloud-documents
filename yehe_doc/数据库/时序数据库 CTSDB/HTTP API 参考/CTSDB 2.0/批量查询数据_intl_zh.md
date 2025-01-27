#### 请求地址

地址为实例的 IP 和 PORT，可从控制台获取到，例如10.13.20.15:9200。

#### 请求路径和方法

路径：`/_msearch`
方法：GET

#### 请求参数

可通过设置写入数据时的 _routing 参数值来提高查询效率，具体请参照示例。也可通过设置 filter_path 参数来过滤并简化返回结果，其参数值为按照逗号分隔的多个 json 路径，其中单个 json 路径用点号连接，可以使用 * 通配符来适配任意字符， ** 通配符可以用来匹配任意路径，可以使用 - 前缀来去除某些返回字段。

例如，responses._shard.f* 表示 responses 下 _shards 中的以 f 开头的字段； responses.**._score 表示 responses 中所有 _score 的字段。

#### 请求内容

查询主要有普通查询和聚合查询，查询请求完全兼容 Elasticsearch api，具体请求内容请参照示例。

#### 返回内容

需要通过 error 字段判断请求是否成功，若返回内容有 error 字段则请求失败，具体错误详情请参照 error 字段描述。这里列举几个查询通用返回字段，详情见下表，若需要简化查询返回结果，可设置 filter_path 参数。

| 字段名称  | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| hits      | 返回匹配的查询结果，其中 total 字段表示匹配到的数据条数。里面的 hits 字段为数组结构，若无指定，则包含所有查询结果的前十条。hits 数组里的每个结果中包含 _index（查询涉及到的 [子表](https://intl.cloud.tencent.com/document/product/1100/45525)），若查询中指定了 docvalue_fields，则会返回 fields 字段具体指明每个字段的值。 |
| took      | 整个查询耗费的毫秒数。                                       |
| _shards   | 参与查询的分片数。其中 total 标识总分片数，successful 标识执行成功的数量，failed 标识执行失败的数量，skipped 标识跳过执行的分片数。 |
| timed_out | 查询是否超时，取值有 false 和 true。                         |
| status    | 查询返回的状态码，2XX 代表成功。                             |

#### CURL 示例说明

##### **无 filter_path 参数的请求**

请求：

```
curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/_msearch -d'
{"index" : "amyli_weather","routing":"host_20"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
{"index" : "ctsdb_test2017","routing":"host_100"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
'
```

返回：

```
{
     "responses": 
    [
        {
          "took": 0,
          "timed_out": false,
          "_shards": {
            "total": 0,
            "successful": 0,
            "skipped": 0,
            "failed": 0
          },
          "hits": {
            "total": 0,
            "max_score": 0,
            "hits": []
          },
          "status": 200
        },
        {
          "took": 1,
          "timed_out": false,
          "_shards": {
            "total": 3,
            "successful": 3,
            "skipped": 0,
            "failed": 0
          },
          "hits": {
            "total": 1,
            "max_score": 1,
            "hits": [
              {
                "_index": "ctsdb_test2017@-979200000_30",
                "_type": "doc",
                "_id": "AV_8fBhlUAkC9PF9L-2t",
                "_score": 1
              }
            ]
          },
          "status": 200
        }
      ]
}
```

##### **有 filter_path 参数的请求**

请求：

```
curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/_msearch?filter_path=responses.\*\*.hits,responses._shards.f\*,-responses.\*\*._score -d'
{"index" : "amyli_weather","routing":"host_20"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
{"index" : "ctsdb_test2017","routing":"host_100"}
{"query" : {"match_all" : {}}, "from" : 0, "size" : 10}
'
```

返回：

```
{
     "responses": [
   {
     "_shards": {
       "failed": 0
     }
   },
   {
     "_shards": {
       "failed": 0
     },
     "hits": {
       "hits": [
         {
           "_index": "ctsdb_test2017@-979200000_30",
           "_type": "doc",
           "_id": "AV_8fBhlUAkC9PF9L-2t"
         }
       ]
     }
   }
     ]
}
```

> 说明：
>
> 如果 filter_path 参数同时设置了匹配条件和去除条件，则返回结果先执行去除条件再执行匹配条件。

