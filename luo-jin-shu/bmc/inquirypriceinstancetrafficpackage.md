# InquiryPriceInstanceTrafficPackage

## 1. 接口描述

调用本接口用于实例修改流量包询价。

{% hint style="info" %}
**注意事项**

* 仅当机器的[`internetChargeType`](../datastructure.md#internetchargetype)为`ByTrafficPackage时可用`
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称               | 必选 | 类型         | 描述                                                                                        |
| ------------------ | -- | ---------- | ----------------------------------------------------------------------------------------- |
| instanceId         | 是  | String     | <p>待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p> |
| trafficPackageSize | 是  | BigDecimal | 流量包大小。                                                                                    |



## 3. 响应结果

| 参数名称                | 类型                                 | 描述                                                 |
| ------------------- | ---------------------------------- | -------------------------------------------------- |
| trafficPackagePrice | [Price](../datastructure.md#price) | <p>流量包价格。<br>可能有多个价格，比如流量包计费，包含包的价格和用量超出包后的价格。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 实例修改流量包询价

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceInstanceTrafficPackage
<Common Request Params>

Request：
{
  "instanceId": "instanceId",
  "trafficPackageSize": 100
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": {  
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "trafficPackagePrice": [
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

| HTTP状态码 | 错误码                                                         | 说明                                                                       |
| ------- | ----------------------------------------------------------- | ------------------------------------------------------------------------ |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND                               | 指定的实例不存在。                                                                |
| 403     | OPERATION\_DENIED\_INTERNET\_CHARGE\_TYPE\_NOT\_BY\_TRAFFIC | 指定的[实例网络模型](../datastructure.md#internetchargetype)不是`ByTrafficPackage`。 |
| 400     | INVALID\_INSTANCE\_TYPE\_ZONE\_NO\_SELL                     | 指定的实例的流量包暂不支持售卖。                                                         |
