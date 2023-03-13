# DescribeEipAvailableResources

## 1. 接口描述

调用本接口用于查询区域可购买EIP资源。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称          | 必选 | 类型     | 描述                                                        |
| ------------- | -- | ------ | --------------------------------------------------------- |
| eipChargeType | 是  | String | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p> |
| zoneId        | 否  | String | <p>EIP所属的可用区ID。</p><p>不传则查询所有区域可用的EIP。</p>                |



## 3. 响应结果

| 参数名称      | 类型                                                        | 描述                                                       |
| --------- | --------------------------------------------------------- | -------------------------------------------------------- |
| requestId | String                                                    | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| dataSet   | Array of [EipAvailable](../datastructure.md#eipavailable) | 购买EIP区域列表。                                               |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 查询区域可购买EIP资源

获取SEL-A区域EIP资源能否支持预付费购买。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeEipAvailableResources
<Common Request Params>

Request：
{
    "eipChargeType": "PREPAID",
    "zoneId": "SEL-A"
}

Response：
{
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "response": {
        "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
        "dataSet": [
            {
                 "zoneId"："SEL-A"，
                 "status"："SELL"
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

| HTTP状态码 | 错误码                       | 说明         |
| ------- | ------------------------- | ---------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND | 指定的可用区不存在。 |

