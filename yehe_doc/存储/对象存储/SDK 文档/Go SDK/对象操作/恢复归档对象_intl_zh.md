## 简介
本文档提供关于恢复归档对象操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 恢复归档对象 | 将归档类型的对象取回访问                      |

## 恢复归档对象 

#### 功能说明

将归档类型的对象取回访问（POST Object restore）。

#### 方法原型

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### 请求示例

[//]: # (.cssg-snippet-restore-object)
```go
key := "example_restore"
f, err := os.Open("../test")
if err != nil {
    panic(err)
}
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType:      "text/html",
        XCosStorageClass: "ARCHIVE", //归档类型
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        // 如果不是必要操作，建议上传文件时不要给单个文件设置权限，避免达到限制。若不设置默认继承桶的权限。
        XCosACL: "private",
    },
}
// 归档直传
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}

opts := &cos.ObjectRestoreOptions{
    Days: 2,
    Tier: &cos.CASJobParameters{
        // Standard, Exepdited and Bulk
        Tier: "Expedited",
    },
}
// 归档恢复
_, err = client.Object.PostRestore(context.Background(), key, opts)
if err != nil {
    panic(err)
}
```

#### 参数说明

```go
type ObjectRestoreOptions struct {        
    Days    int               
    Tier    *CASJobParameters 
}
type CASJobParameters struct {
    Tier    string 
}
```

| 参数名称             | 参数描述                                                     | 类型   | 是否必填 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                  | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，对象键为 doc/pic.jpg | string | 是   |
| ObjectRestoreOptions | 描述取回的临时文件的规则                                     | struct | 是   |
| Days                 | 描述临时文件的过期时间                                       | int    | 是   |
| CASJobParameters     | 描述恢复类型的配置信息                                       | struct | 否   |
| Tier                 | 描述取回临时文件的模式。若恢复的是归档存储类型数据，可选值为 Expedited、Standard、Bulk，分别对应极速模式、标准模式以及批量模式这三种模式；若恢复的是深度归档存储类型数据，则可选值为 Standard、Bulk。 | string | 否   |

