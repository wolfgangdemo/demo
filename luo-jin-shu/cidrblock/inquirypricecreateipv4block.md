# InquiryPriceCreateIpv4Block

## 1. 接口描述

调用本接口用于创建Ipv4 CidrBlock询价。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称          | 必选 | 类型                                                 | 描述                                                                                             |
| ------------- | -- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| zoneId        | 是  | String                                             | Cidr Block所属的可用区ID。                                                                            |
| chargeType    | 是  | String                                             | <p>付费类型。</p><p>PREPAID：预付费，即包年包月</p><p>POSTPAID：后付费。</p>                                       |
| chargePrepaid | 否  | [ChargePrepaid](../datastructure.md#chargeprepaid) | <p>预付费模式。</p><p>即包年包月相关参数设置。通过该参数可以指定包年包月实例的购买时长等属性。若指定实例的付费模式为预付费则该参数必传。</p>                  |
| netmask       | 是  | Integer                                            | <p>购买的掩码。</p><p>取值范围1~32。</p><p>可以从<code>DescribeAvailableIpv4Resource</code>接口中获取可用的掩码列表。</p> |
| amount        | 否  | Integer                                            | <p>购买的数量。</p><p>默认为1。</p>                                                                      |



## 3. 响应结果

| 参数名称      | 类型                                 | 描述                                                       |
| --------- | ---------------------------------- | -------------------------------------------------------- |
| requestId | String                             | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| price     | [Price](../datastructure.md#price) | Cidr Block价格。                                            |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 查询指定区域指定掩码的后付费Ipv4 Cidr Block价格**

查询区域**`CHI-A`**掩码为**`28`**的后付费Ipv4 Cidr Block价格，购买数量为**`1`**。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceCreateIpv4Block
<Common Request Params>

Request:
{
  "zoneId": "CHI-A",
  "chargeType": "POSTPAID",
  "netmask": 28
}

Response:
{
  "requestId": "TCB52F216-374D-4895-AF29-A3E29E5403E2",
  "response": {
    "requestId": "TCB52F216-374D-4895-AF29-A3E29E5403E2",
    "price": {
      "discount": 100.0,
      "discountPrice": null,
      "originalPrice": null,
      "unitPrice": 0.06,
      "discountUnitPrice": 0.06,
      "chargeUnit": "HOUR",
      "stepPrices": null
    }
  }
}
```

****

**2. 查询指定区域指定掩码的预付费Ipv4 Cidr Block价格**

查询区域**`HKG-A`**掩码为**`29`**的预付费Ipv4 Cidr Block价格，购买周期为**`1`**，购买数量为**`2`**。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceCreateIpv4Block
<Common Request Params>

Request:
{
  "zoneId": "HKG-A",
  "chargeType": "PREPAID",
  "chargePrepaid": {
    "period": 1
  },
  "netmask": 29,
  "amount": 2
}

Response:
{
  "requestId": "TA2741058-301C-4E1A-8158-C05981F8808B",
  "response": {
    "requestId": "TA2741058-301C-4E1A-8158-C05981F8808B",
    "price": {
      "discount": 95.0,
      "discountPrice": 22.8,
      "originalPrice": 24.0,
      "unitPrice": null,
      "discountUnitPrice": null,
      "chargeUnit": null,
      "stepPrices": null
    }
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                     | 说明        |
| ------- | --------------------------------------- | --------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND               | 指定的区域不存在。 |
| 403     | OPERATION\_DENIED\_UNAVAILABLE\_NETMASK | 指定的掩码不可用。 |
