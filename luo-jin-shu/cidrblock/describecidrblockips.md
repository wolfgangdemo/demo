# DescribeCidrBlockIps

## 1. 接口描述

调用本接口用于查询一个Cidr Block的IP列表。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型     | 描述                                                                                               |
| ----------- | -- | ------ | ------------------------------------------------------------------------------------------------ |
| cidrBlockId | 是  | String | <p>Cidr Block ID。</p><p>可通过<code>DescribeCidrBlocks</code>接口返回值中的<code>cidrBlockId</code>获取。</p> |
| instanceId  | 否  | String | <p>实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p>            |
| ip          | 否  | String | IP。                                                                                              |



## 3. 响应结果

| 参数名称         | 类型                                                      | 描述                                                       |
| ------------ | ------------------------------------------------------- | -------------------------------------------------------- |
| requestId    | String                                                  | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| cidrBlockIps | Array of [CidrBlockIp](../datastructure.md#cidrblockip) | 结果集。                                                     |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 查询指定Cidr Block包含的IP**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeCidrBlockIps
<Common Request Params>

Request:
{
  "cidrBlockId": "aCidrBlockId"
}

Response:
{
  "requestId": "T91F2EF61-762D-4401-A18B-3D626386C4CC",
  "response": {
    "requestId": "T91F2EF61-762D-4401-A18B-3D626386C4CC",
    "cidrBlockIps": [
      {
        "cidrBlockId": "aCidrBlockId",
        "cidrBlockType": "IPV6",
        "ip": "2602:ffe4:1:11::1",
        "instanceId": "bindedInstanceId",
        "status": "BINDED"
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码 | 说明 |
| ------- | --- | -- |
|         |     |    |
