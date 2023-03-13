# InquiryPriceCreateInstance

## 1. 接口描述

调用本接口用于创建一个实例询价。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称                    | 必选 | 类型                                                 | 描述                                                                                                    |
| ----------------------- | -- | -------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| zoneId                  | 是  | String                                             | 实例所属的可用区ID。                                                                                           |
| instanceTypeId          | 是  | String                                             | <p>实例机型ID。<br>具体取值可通过调用接口<code>DescribeInstanceTypes</code>来获得最新的规格表。</p>                             |
| instanceChargeType      | 是  | String                                             | <p>实例计费类型。</p><p>PREPAID：预付费，即包年包月。 POSTPAID：后付费。</p>                                                 |
| internetChargeType      | 是  | String                                             | <p>网络计费类型。</p><p>取值范围请看<a href="../datastructure.md#internetchargetype">InternetChargeType</a>。</p>   |
| InstanceChargePrepaid   | 否  | [ChargePrepaid](../datastructure.md#chargeprepaid) | <p>预付费模式，即包年包月相关参数设置。</p><p>通过该参数可以指定包年包月实例的购买时长等属性。</p><p>若指定实例的付费模式为预付费则该参数必传。</p>                  |
| trafficPackageSize      | 否  | Float                                              | <p>流量包订购大小。</p><p>单位为TB。该值仅限当 <code>internetChargeType</code> = <code>ByTrafficPackage</code> 生效。</p> |
| internetMaxBandwidthOut | 否  | Integer                                            | <p>公网出带宽上限。</p><p>单位：Mbps。</p><p>默认值：1Mbps。</p><p>不同机型带宽上限范围不一致，具体限制详见购买网络带宽。</p>                     |



## 3. 响应结果

| 参数名称           | 类型                                          | 描述                                                       |
| -------------- | ------------------------------------------- | -------------------------------------------------------- |
| instancePrice  | [Price](../datastructure.md#price)          | 实例价格。                                                    |
| bandwidthPrice | Array of [Price](../datastructure.md#price) | <p>公网带宽价格。<br>可能有多个价格，比如流量包计费，包含包的价格和用量超出包后的价格</p>       |
| requestId      | String                                      | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 查询创建预付费实例的询价，带宽计费为固定带宽。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceCreateInstance
<Common Request Params>

Request:
{
  "zoneId": "SEL-A",
  "instanceTypeId": "M6C",
  "instanceChargeType": "PREPAID",
  "instanceChargePrepaid": {
    "period": 1
  },
  "trafficPackageSize": 100,
  "internetMaxBandwidthOut": 200,
  "internetChargeType": "ByBandwidth"
}

Response:
{
  "requestId": "T01F25348-DA67-4726-97C1-538BAE714F8B",
  "response": {
    "requestId": "T01F25348-DA67-4726-97C1-538BAE714F8B",
    "instancePrice": {
      "discount": 95.0,
      "discountPrice": 426.55,
      "originalPrice": 449.0,
      "unitPrice": null,
      "discountUnitPrice": null,
      "chargeUnit": null,
      "stepPrices": null
    },
    "bandwidthPrice": [
      {
        "discount": 95.0,
        "discountPrice": 1444.0,
        "originalPrice": 1520.0,
        "unitPrice": null,
        "discountUnitPrice": null,
        "chargeUnit": null,
        "stepPrices": null
      }
    ]
  }
}

```

2\. **查询创建后付费实例的询价，带宽计费为固定带宽。**

<pre class="language-json"><code class="lang-json"><strong>POST / HTTP/1.1
</strong>Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceCreateInstance
&#x3C;Common Request Params>

Request:
{
  "zoneId": "SEL-A",
  "instanceTypeId": "M6C",
  "instanceChargeType": "POSTPAID",
  "trafficPackageSize": 100,
  "internetMaxBandwidthOut": 200,
  "internetChargeType": "ByBandwidth"
}

Response:
{
  "requestId": "T3105EE4C-30C5-4FF2-9A34-688C8455376D",
  "response": {
    "requestId": "T3105EE4C-30C5-4FF2-9A34-688C8455376D",
    "instancePrice": {
      "discount": 100.0,
      "discountPrice": null,
      "originalPrice": null,
      "unitPrice": 0.63,
      "discountUnitPrice": 0.63,
      "chargeUnit": "HOUR",
      "stepPrices": null
    },
    "bandwidthPrice": [
      {
        "discount": 100.0,
        "discountPrice": null,
        "originalPrice": null,
        "unitPrice": 1.32,
        "discountUnitPrice": 1.32,
        "chargeUnit": "HOUR",
        "stepPrices": null
      }
    ]
  }
}
</code></pre>

**3. 查询创建预付费实例的询价，带宽计费为流量包。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceCreateInstance
<Common Request Params>

Request:
{
  "zoneId": "SEL-A",
  "instanceTypeId": "M6C",
  "instanceChargeType": "PREPAID",
  "instanceChargePrepaid": {
    "period": 1
  },
  "trafficPackageSize": 100,
  "internetMaxBandwidthOut": 200,
  "internetChargeType": "ByTrafficPackage"
}

Response:
{
  "requestId": "T8CF9A34A-ECA2-4192-8515-CAC51C40592B",
  "response": {
    "requestId": "T8CF9A34A-ECA2-4192-8515-CAC51C40592B",
    "instancePrice": {
      "discount": 95.0,
      "discountPrice": 426.55,
      "originalPrice": 449.0,
      "unitPrice": null,
      "discountUnitPrice": null,
      "chargeUnit": null,
      "stepPrices": null
    },
    "bandwidthPrice": [
      {
        "discount": 95.0,
        "discountPrice": 7524.0,
        "originalPrice": 7920.0,
        "unitPrice": null,
        "discountUnitPrice": null,
        "chargeUnit": null,
        "stepPrices": null
      },
      {
        "discount": 100.0,
        "discountPrice": null,
        "originalPrice": null,
        "unitPrice": null,
        "discountUnitPrice": null,
        "chargeUnit": null,
        "stepPrices": [
          {
            "stepStart": 0.0,
            "stepEnd": null,
            "unitPrice": 0.08,
            "discountUnitPrice": 0.08
          }
        ]
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

| HTTP状态码 | 错误码                                          | 说明                  |
| ------- | -------------------------------------------- | ------------------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND                    | 指定的可用区不存在。          |
| 404     | INVALID\_INSTANCE\_TYPE\_NOT\_FOUND          | 未找到指定的实例规格。         |
| 400     | INVALID\_INSTANCE\_TYPE\_ZONE\_NO\_SELL      | 指定实例规格在指定的 可用区未售卖   |
| 400     | INVALID\_INSTANCE\_BANDWIDTH\_ZONE\_NO\_SELL | 指定的公网计费类型在所选的可用区不支持 |

##
