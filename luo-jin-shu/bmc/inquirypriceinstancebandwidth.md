# InquiryPriceInstanceBandwidth

## 1. 接口描述

调用本接口用于实例修改带宽询价。

{% hint style="info" %}
**注意事项**

* 仅当机器的[`internetChargeType`](../datastructure.md#internetchargetype)为`ByBandwidth时可用`，且当修改的带宽大于默认带宽时，接口会返回价格。
* 机器的`instanceChargeType`不同，返回的价格结构是不同的。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称             | 必选 | 类型      | 描述                                                                                        |
| ---------------- | -- | ------- | ----------------------------------------------------------------------------------------- |
| instanceId       | 是  | String  | <p>待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p> |
| bandwidthOutMbps | 是  | Integer | 带宽大小。                                                                                     |



## 3. 响应结果

| 参数名称           | 类型                                 | 描述                                                       |
| -------------- | ---------------------------------- | -------------------------------------------------------- |
| bandwidthPrice | [Price](../datastructure.md#price) | <p>公网带宽价格。<br>可能有多个价格，比如流量包计费，包含包的价格和用量超出包后的价格。</p>      |
| requestId      | String                             | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 实例修改带宽询价

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: InquiryPriceInstanceBandwidth
<Common Request Params>

Request：
{
  "instanceId": "instanceId",
  "bandwidthOutMbps": 100
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": {  
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "bandwidthPrice": {
        "discount": 100.0,
        "discountPrice": null,
        "originalPrice": null,
        "unitPrice": 1.32,
        "discountUnitPrice": 1.32,
        "chargeUnit": "HOUR",
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

| HTTP状态码 | 错误码                                                                | 说明                                                                  |
| ------- | ------------------------------------------------------------------ | ------------------------------------------------------------------- |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND                                      | 指定的实例不存在。                                                           |
| 403     | OPERATION\_DENIED\_INTERNET\_CHARGE\_TYPE\_NOT\_BY\_FIX\_BANDWIDTH | 指定的[实例网络模型](../datastructure.md#internetchargetype)不是`ByBandwidth。` |
| 400     | INVALID\_INSTANCE\_TYPE\_ZONE\_NO\_SELL                            | 指定的实例的带宽暂不支持售卖。                                                     |
