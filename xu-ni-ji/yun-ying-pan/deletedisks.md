# DeleteDisks

## 1. 接口描述

本接口（DeleteDisks）用于删除单个或多个云硬盘。

{% hint style="info" %}
**注意事项**

* 如果当前云硬盘不在回收站会被放入回收站。
* 如果当前云硬盘在回收站，则会从回收站中彻底释放。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称    | 必选 | 类型              | 描述            |
| ------- | -- | --------------- | ------------- |
| diskIds | 是  | Array of String | 将要删除的云硬盘ID集合。 |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **删除单个或多个云硬盘。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: DeleteDisks
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                | 说明          |
| ------- | ---------------------------------- | ----------- |
| **404** | DISK\_NOT\_FOUND                   | 无法找到指定的云硬盘。 |
| **400** | INVALID\_NOT\_IN\_NO\_SUBSCRIPTION | 不在非订阅模式下。   |

