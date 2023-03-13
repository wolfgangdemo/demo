# InquiryPriceCreateDdosIpAddress

## 1. 接口描述

调用本接口用于创建Ddos IP询价。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称                | 必选 | 类型                                                 | 描述                                                                                       |
| ------------------- | -- | -------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| zoneId              | 是  | String                                             | Ddos IP所属的可用区ID。                                                                         |
| ddosIpChargeType    | 是  | String                                             | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p>                                |
| ddosIpChargePrepaid | 否  | [ChargePrepaid](../datastructure.md#chargeprepaid) | <p>预付费模式。<br>即包年包月相关参数设置。</p><p>通过该参数可以指定包年包月实例的购买时长等属性。</p><p>若指定实例的付费模式为预付费则该参数必传。</p> |
| amount              | 否  | Integer                                            | <p>指定创建Ddos IP的数量。</p><p>范围为 1-100。</p><p>默认值：1。</p>                                     |



## 3. 响应结果

| 参数名称        | 类型                                 | 描述                                                       |
| ----------- | ---------------------------------- | -------------------------------------------------------- |
| requestId   | String                             | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| ddosIpPrice | [Price](../datastructure.md#price) | Ddos IP价格。                                               |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. Ddos IP后付费询价

查询SEL-A区域后付费Ddos IP价格。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceCreateDdosIpAddress
<Common Request Params>

Request：
{
    "zoneId": "SEL-A"，
    "ddosIpChargeType": "POSTPAID"
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": { 
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "ddosIpPrice": {
      "discount": 100.0,
      "discountPrice": null,
      "originalPrice": null,
      "unitPrice": 0.63,
      "discountUnitPrice": 0.63,
      "chargeUnit": "HOUR",
      "stepPrices": null
    },
  }
}
```

#### 2. 购买2个Ddos IP预付费询价

查询SEL-A区域预付费2个Ddos IP、1个月价格。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: InquiryPriceCreateDdosIpAddress
<Common Request Params>

Request：
{
    "zoneId": "SEL-A"，
    "ddosIpChargeType": "PREPAID",
    "ddosIpChargePrepaid" {
        "period": 1
    },
    "amount": 2
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": { 
      "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
      "ddosIpPrice": {
        "discount": 95.0,
        "discountPrice": 426.55,
        "originalPrice": 449.0,
        "unitPrice": null,
        "discountUnitPrice": null,
        "chargeUnit": null,
        "stepPrices": null
    },
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                     | 说明                   |
| ------- | --------------------------------------- | -------------------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND               | 指定的可用区不存在。           |
| 400     | INVALID\_DDOS\_IP\_TYPE\_ZONE\_NO\_SELL | 指定Ddos IP在指定的可用区未售卖。 |
| 400     | MISSING\_PARAMETER                      | 指定的参数为空。             |
