# UnbindCidrBlockIps

## 1. 接口描述

调用本接口用于实例解绑一个或多个Cidr Block IP。

****

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型     | 描述                                                                                                   |
| ----------- | -- | ------ | ---------------------------------------------------------------------------------------------------- |
| cidrBlockId | 是  | String | <p>待操作的Cidr Block ID。</p><p>可通过<code>DescribeCidrBlocks</code>接口返回值中的<code>cidrBlockId</code>获取。</p> |
| ipList      | 是  | String | 待解绑的IP列表。                                                                                            |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 解绑指定Cidr Block的一个IP**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: UnbindCidrBlockIps
<Common Request Params>

Request:
{
  "cidrBlockId": "cidrBlockId",
  "ipList": [
    "2602:ffe4:1:11::1"
  ]
}

Response:
{
  "requestId": "TEE694662-1428-4330-91ED-9D5800206E20",
  "response": {
    "requestId": "TEE694662-1428-4330-91ED-9D5800206E20"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                    | 说明                      |
| ------- | -------------------------------------- | ----------------------- |
| 403     | OPERATION\_DENIED\_IP\_NOT\_BELONG     | 待解绑的IP不属于指定的Cidr Block。 |
| 403     | OPERATION\_DENIED\_INVALID\_STATUS     | 该IP当前状态不支持解绑。           |
| 403     | OPERATION\_DENIED\_CIDRBLOCK\_RECYCLED | 在回收站中的Cidr Block不支持该操作。 |
