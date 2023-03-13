# DescribeAvailableResources

## 1. 接口描述

调用本接口用于查询售卖实例和带宽的可用资源。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称               | 必选 | 类型      | 描述                                                                                                                        |
| ------------------ | -- | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| instanceChargeType | 是  |  String | <p>实例计费类型。 </p><p>PREPAID：预付费，即包年包月。 POSTPAID：后付费。</p>                                                                    |
| zoneId             | 否  | String  | 可用区ID。                                                                                                                    |
| instanceTypeId     | 否  | String  | 实例机型ID。                                                                                                                   |
| sellStatus         | 否  | String  | <p>售卖的状态。</p><ul><li>SELL：表示实例可购买，且库存>10。</li><li>SELL_SHORTAGE: 表示可购买，但是库存&#x3C;10台。</li><li>SOLD_OUT：表示实例已售罄。</li></ul> |

&#x20;

## 3. 响应结果

| 参数名称               | 类型                                                                  | 描述                                                       |
| ------------------ | ------------------------------------------------------------------- | -------------------------------------------------------- |
| availableResources | Array of [AvailableResource](../datastructure.md#availableresource) | 可用资源的集合。                                                 |
| requestId          | String                                                              | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |

&#x20;

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **获取所有的可用资源。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeAvailableResources
<Common Request Params>

Request:
{
  "instanceTypeId": "MDE",
  "instanceChargeType": "PREPAID",
  "zoneId": "MOW-B"
}

Response:
{
  "requestId": "T001A67B7-C345-4B0E-A9B0-FB0C859C9075",
  "response": {
    "requestId": "T001A67B7-C345-4B0E-A9B0-FB0C859C9075",
    "availableResources": [
      {
        "zoneId": "MOW-B",
        "status": "SELL",
        "internetChargeTypes": [
          "ByBandwidth",
          "ByTrafficPackage"
        ],
        "instanceTypeId": "MDE",
        "maximumBandwidthOut": 10000,
        "defaultBandwidthOut": 50,
        "defaultTrafficPackageSize": 5.0
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}



## &#x20;5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                       | 说明         |
| ------- | ------------------------- | ---------- |
| **404** | INVALID\_ZONE\_NOT\_FOUND | 指定的可用区不存在。 |

##
