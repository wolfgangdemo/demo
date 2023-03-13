# DescribeAvailableIpv4Resources

## 1. 接口描述

调用本接口用于查询可售的Ipv4 Cidr Block资源。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型     | 描述                                                        |
| ---------- | -- | ------ | --------------------------------------------------------- |
| chargeType | 是  | String | <p>计费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p> |
| zoneId     | 否  | String | Cidr Block所属的可用区ID。                                       |



## 3. 响应结果

| 参数名称                   | 类型                                                                          | 描述                                                       |
| ---------------------- | --------------------------------------------------------------------------- | -------------------------------------------------------- |
| requestId              | String                                                                      | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| availableIpv4Resources | Array of [AvailableIpv4Resource](../datastructure.md#availableipv4resource) | 可用资源的集合。                                                 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 查询预付费Ipv4 Cidr Block的可用资源**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeAvailableIpv4Resources
<Common Request Params>

Request:
{
  "chargeType": "PREPAID"
}

Response:
{
  "requestId": "T9681F843-24B6-4926-86BA-F3D5C25563E3",
  "response": {
    "requestId": "T9681F843-24B6-4926-86BA-F3D5C25563E3",
    "availableIpv4Resources": [
      {
        "zoneId": "HKG-A",
        "netmask": 29,
        "sellStatus": "SELL"
      },
      {
        "zoneId": "SEL-A",
        "netmask": 29,
        "sellStatus": "SOLD_OUT"
      },
      {
        "zoneId": "HKG-A",
        "netmask": 26,
        "sellStatus": "SELL_SHORTAGE"
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

| HTTP状态码 | 错误码                       | 说明        |
| ------- | ------------------------- | --------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND | 指定的区域不存在。 |
