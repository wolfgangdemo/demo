# ReleaseInstances

## 1. 接口描述

本接口用于释放一个或多个实例。

{% hint style="info" %}
**注意事项**

* 只有在回收站中的实例才支持该操作。
* 支持批量操作。每次请求批量实例的上限为100。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型              | 描述                                                                                                             |
| ----------- | -- | --------------- | -------------------------------------------------------------------------------------------------------------- |
| instanceIds | 是  | Array of String | <p>一个或多个待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。每次请求批量实例的上限为100。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **批量释放实例**

同时释放两个实例。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: ReleaseInstances
<Common Request Params>

Request:
{
  "instanceIds": [
    "instanceId1",
    "instanceId2"
  ]
}

Response:
{
  "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453",
  "response": {
    "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                        | 说明               |
| ------- | ------------------------------------------ | ---------------- |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND              | 指定的实例不存在。        |
| 403     | OPERATION\_DENIED\_INSTANCE\_NOT\_RECYCLED | 不在回收站中的实例不支持该操作。 |

