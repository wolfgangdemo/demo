# TerminateDisk

## 1. 接口描述

本接口（TerminateDisk）用于取消订阅。

{% hint style="info" %}
**注意事项**

* 取消订阅后服务将不会自动续费。
* 可以通过重新订阅或者手动续订的方式继续使用。
* 如果已经取消订阅过，并且当前硬盘已在回收站，则会从回收站中彻底释放。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称   | 类型     | 描述         |
| ------ | ------ | ---------- |
| diskId | String | 将要释放的云硬盘ID |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **终止云硬盘。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: TerminateDisk
<Common Request Params>

Response:
```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                        | 说明          |
| ------- | -------------------------- | ----------- |
| **400** | INVALID\_DISK\_NOT\_FOUND  | 没有找到对应的云硬盘。 |
| **404** | INVALID\_ORDER\_NOT\_FOUND | 没有找到对应的订单。  |
